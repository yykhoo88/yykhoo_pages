---
layout: post
mathjax: true
title: Bootstrapping SOFR Curve with QuantLib
date:   2023-09-03
tags: [QuantLib]
---
<center><img src="/images/2023-09-03/YieldCurve.png" width="450" /></center>

I have been a valuation quant for the past 10 years. I have used numerous tools, especially C# and Python when it comes to modelling. However, we had always built codes from scratch, module by module.

This is the first time after years of hearing [QuantLib](https://www.quantlib.org/) that I decided to learn how to use them. They are surprisingly similar to how I would imagine an object-oriented derivative valuation module should look like. In this first exploratory post, I will try to bootstrap a SOFR swap curve (Bloomberg S490) and reprice the indices. Also, I am adopting the "just-publish-it" mindset for now. I will just publish anything with minimal verification - ping me if I have missed anything!

```python
#Start by importing quantlib
import QuantLib as ql
import pandas as pd
import numpy as np
```

<center><img src="/images/2023-09-03/datatable.png" width="300" /></center>

```python
#loading curve data from Excel
curveData = pd.read_excel("SOFR.xlsx")
systemDate = ql.Date(30,8,2023)
ql.Settings.instance().evaluationDate = systemDate

myIndex = ql.Sofr()
myCalendar = ql.UnitedStates(1)
myDayCount = ql.Actual360()
mySettlementDays = 2
```

```python
#Here we use OISRateHelper to build a PiecewiseLinearZero curve. 
#Notice that OISRateHelper take in (SettlementDays,Period,Quote,Index)

ois_helpers = [ql.OISRateHelper(mySettlementDays,ql.Period(tenor),ql.QuoteHandle(ql.SimpleQuote(rate/100)),myIndex) 
               for rate,tenor in list(curveData[["MarketQuote","Tenor"]].itertuples(index=False))]
sofr_curve = ql.PiecewiseLinearZero(systemDate,ois_helpers,myDayCount)
sofr_curve.enableExtrapolation()

#sofr_curve.nodes() supposedly show the zero rates of the curve, however I am unable to verify it as of now.
print(sofr_curve.nodes())
```

```python
#Now I attempt to reprice the OIS swaps
valuation_curve = ql.YieldTermStructureHandle(sofr_curve)
myIndex2 = ql.Sofr(valuation_curve)
swap_engine = ql.DiscountingSwapEngine(valuation_curve)
effective_date = myCalendar.advance(systemDate,mySettlementDays,ql.Days)

ois_swaps = []
for rate, tenor in list(curveData[["MarketQuote","Tenor"]].itertuples(index=False)):
    schedule = ql.MakeSchedule(effective_date,myCalendar.advance(effective_date,ql.Period(tenor)), #effective date, termination date
                            ql.Period("1Y"),calendar=myCalendar) #fixed rate frequency, calendar
    fixedRate = rate/100
    temp_oisswap = ql.MakeOIS(ql.Period(tenor),myIndex2,fixedRate,nominal=10000000)
    temp_oisswap.setPricingEngine(swap_engine)
    ois_swaps.append(temp_oisswap)
	
#we reprint the NPV of each swaps, expecting zeros
for a in ois_swaps:
    print(a.NPV())
```

As expected, the NPV is zero! The next step would be to double check the zero rates. Until next time.