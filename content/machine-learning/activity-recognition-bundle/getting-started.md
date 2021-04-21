---
title: Getting Started
layout: redirect
weight: 30

aliases:
  - /predictive-analytics/activity-recognition/#getting-started
---

We have added a *CONFIG.INI* file to the zip. This file is meant for capturing the tenant details and credentials which will be used by the demo scripts.

First of all, update the *CONFIG.INI* with the appropriate values and save it. Replace `c_url` with your tenant URL, `c_user` with your tenant username and `c_pass` with your tenant password. Leave the `c_device_source` as is for now.

	CONFIG.INI
	[cumulocity]
	c_url=https://yourtenant.cumulocity.com
	c_user=user@company.com
	c_pass=password
	c_device_source=deviceID


For this particular demo, a phone or a phone-like device needs to be used, so that the measurement data for that particular device can be captured and be used for recognizing activities.

Therefore, the documentation has been split up into two parts:

* [Activity recognition using an iPhone](#activity-recognition-using-iphone)
* [Activity recognition using a simulated demo device](#activity-recognition-using-demo-device)