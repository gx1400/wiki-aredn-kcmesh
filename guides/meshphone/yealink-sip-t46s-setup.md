---
title: Meshphone - Yealink SIP-T46S Setup
description: 
published: true
date: 2023-01-14T13:41:01.701Z
tags: 
editor: markdown
dateCreated: 2023-01-14T13:41:01.701Z
---

# Yealink SIP-T46S Setup
## Author
Derek Rowland KE0PRY
Created 2023-01-14

## Overview

I was given a Yealink SIP phone by a local ham to setup for use on the KC Mesh/AREDN network. This document is my attempt to document the setup process.

## Requesting Access

Contact Chuck Chamberlin (KD0VXN) at kd0vxn@gmail.com and request access.

Include:
Name
Call Sign
Whether you are in Missouri or Kansas (determines your assigned phone number prefix)
A valid email for voicemail and setup information


As of January 2023, the Grandstream PBX system email looked like this:

![meshphone-email.png](/meshphone/yealink-sip-t46s/meshphone-email.png)

## Accessing SIP-T46S via network

My phone is powered via POE.  On the back of the phone there are two ports, “PC” and “Internet”.  Plug your ethernet cable into the “Internet” port.  If you have an POE switch that is properly figured, the phone should boot.

After booting, the phone will be on the main page.  Select “Menu” then “Status” to find your IP address.

![ip-addr.png](/meshphone/yealink-sip-t46s/ip-addr.png)

If your computer is on the same network, you should be able to connect to the phone at http://(IP Address)

The login page of my phone looks like this:

![loginpage.png](/meshphone/yealink-sip-t46s/loginpage.png)

Default username and password are “**admin**” and “**admin**”
If this username and password does not work you will need to factory reset the phone.

The photo below shows the default screen after logging in.

![statuspage.png](/meshphone/yealink-sip-t46s/statuspage.png)

## Updating Firmware

Initially my phone was running a version of the firmware that only supported Skype for Business, and did not support SIP.  The firmware was 66.9.0.78, which is also very old.

Perusing Yealink's support website, I found some firmware downloads: https://support.yealink.com/en/portal/docList?archiveType=software&productCode=95ef8c9dce7c98ba

In some forums I read that some Yealink phones do not like making large leaps in firmware version, and sometimes update successfully in small steps.

I downloaded two version:
- The newest: 66.86.0.15
- The oldest: 66.81.0.25

Initially I upgraded to 66.81.0.25.  The firmware is upgraded in the “Settings” tab, then the “Upgrade” link on the left:

![update.png](/meshphone/yealink-sip-t46s/update.png)

The downloaded firmware file should be uploaded with the Browse button.  Upon upload and confirmation, the phone will begin to automatically update the firmware.

There is a warning on the web browser to leave the browser open and ensure the phone does not lose power.

The upgrade, reboot, and initialization takes several minutes, monitor the screen of the phone for status.

After successfully upgrading to 66.81.0.25, I upgraded to the most recent firmware 66.86.0.15 using the same process.

Upon successful upgrade to 66.86.0.15, the settings screen looks a little different and will begin to warn that the admin password needs to be changed (see this at the top of the photo above).

## SIP Setup

For reference again, below is the email for setup:

![meshphone-email.png](/meshphone/yealink-sip-t46s/meshphone-email.png)

Use the settings from the “General Settings” section of the email.

SIP Settings are on the “Account” tab

![accountsettings.png](/meshphone/yealink-sip-t46s/accountsettings.png)

Hit apply and phone should accept the new configuration and connect if successful.  The "Register Status" should be "Registered"

## Call Someone!
Find someone to call or call you!

![connected.png](/meshphone/yealink-sip-t46s/connected.png)
