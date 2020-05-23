---
layout: post
mathjax: true
title:  Hosting Wordpress with Amazon Lightsail
date:   2020-05-23
tags: [wordpress]
---

<center><img src="/images/wpamazon/wpamazon.png" width="500" /></center>

Some programming hobby. Let's attempt to build a [wordpress](https://wordpress.com/) website using [Amazon Lightsail](https://aws.amazon.com/lightsail/). This is an easy tutorial and we should be able to build it in less than 10 minutes.

### Sign Up for Amazon AWS

First of course, head over to [Amazon AWS](https://aws.amazon.com/) and sign yourself up! You'll be prompted to give a credit card, but if used right the charges should be minimal.
After that, you'll be prompted with the AWS management console. On the "find services" tab, put in "Amazon Lightsail". You'll be shown the lightsail page.

<center><img src="/images/wpamazon/lightsail.png" width="800" /></center>

### Creating a wordpress instance

To create a VPN instannce, just click on "create an instance", then choose an instance location (usually it is default to whichever closest to your current location). Select "linux/unix" platform, and select a blueprint "wordpress".
In this case the VPN will be pre-installed with Linux and [Bitnami](https://bitnami.com/stack/wordpress) version of wordpress.

<center><img src="/images/wpamazon/lightsail2.png" width="450" /></center>

Scroll further downwards and you'll be presented with choices, such as launch script or SSH key pairs. You'll be fine not doing any of them for now. Also you can choose your instance plan. For starter, let's use the cheapest $3.5 plan. It'll generally work for websites with low volumes.
Finally click on "create instance".

### Assign a static address

Next, we'll need to assign a static address to the VPN instance. It's free of charge, as long as you keep the VPN server up and running. To do that, go to the "lightsail" page, then choose "networking".
Next click on "create static IP". Remember to attach the IP to the VPN instance you've just created. Oh yes, remember the IP address!

<center><img src="/images/wpamazon/static.png" width="800" /></center>

### Get the password and login

