---
title: Setting up and registering the device
weight: 30
---

### <a name="install-agent"></a> To install the agent

1. Download the agent software, which includes the CA root certificate bundle, Cloud Remote Access software, and our package public key. For the link see the table below.
2. Log in to the web user interface of the NTC-200 series.
3. Navigate to the **System** menu. Click **System configuration** > **Firmware signature**.
4. Turn **Enable firmware signature check** to OFF.

    > **Info:** If you don´t turn the signature check off, the software installation will fail. After you have installed the agent package, the signature check will automatically be turned on again.
  In case of firmware version 2.0.84.0 you can ignore this step as this version does not support the firmware signature.

5. Navigate to the **System** menu. Click **System configuration** > **Upload** > **Choose a file** and select the downloaded software. Click **Upload** to upload the software to the router.
6. Click the **Install** button for the uploaded software which you want to install.

The routers of the NTC-200 series will reboot automatically after the installation.

The agent will automatically start and the router can then be [registered with Cumulocity IoT](#register-device). Subsequent upgrades or downgrades can be performed remotely via the agent’s software management feature, or locally via the router’s web user interface.

#### NTC-200 series agent software

|Version|Download|
|:---|:---|
|1.0.0|[download](http://resources.cumulocity.com/ntc/cumulocity-ntc-agent_1.0.0_arm-signed.ipk)|


### <a name="register-device"></a> Registering the router as a device to Cumulocity IoT

#### <a name="configure"></a> To configure the router

The support for Cumulocity IoT can be configured through the router’s web user interface. To do so, log in to the user interface as described in the router’s manual. Navigate to the **System** tab and click the **Internet of Things** menu item.

![Web Interface](/images/device-demos/casa-system-router/router-web-interface.png)

Verify that the **Agent** toggle is set to **ON**.

The URL in the **Server** field must point to the Cumulocity IoT instance that you want to connect to. The URL has to be of the format `https://<my-tenant>.<instance-url>`, where &lt;instance-url&gt; refers to the URL of the Cumulocity IoT instance, for example `https://mqtt.cumulocity.com/`.

Optionally, you can activate data collecting for the following functionalities:

* GPIO analog measurements: Send the voltages of the analog inputs [seconds].
* GPS position interval: Update the current GPS position [seconds].
* GPS position event: Send a location trace of the GPS position [seconds].
* System resources measurements: Get information about CPU usage, memory usage and network traffic [seconds].
* Connection signal measurements: Get information about cellular signal strength [seconds].

All these options are disabled by default (the interval is set to 0).

The web interface also shows the status of the connection to Cumulocity IoT:

* Checking network connection: Waiting for mobile network connection at boot.
* Bootstrapping: Load credentials or request credentials from Cumulocity IoT.
* Integrating: Connecting to Cumulocity IoT.
* Loading plugins: Loading Lua plugins.
* Connected: The agent is successfully connected to Cumulocity IoT.
* No server URL: No or invalid server URL.
* Bootstrap failed: Cannot get credentials from Cumulocity IoT.
* Integration failed: Cannot connect to Cumulocity IoT.
* Create threads failed: Not able to start reporter or device push.

#### <a name="connect"></a> To connect the router

To register your NetComm router to Cumulocity IoT, you need the router’s serial number as device ID. The serial number is printed on the back side of the router as shown below. Alternatively, it is also available in the router’s web user interface. Navigate to **System** > **Internet of Things** and view the **Device ID** field.

![Serial Number](/images/device-demos/casa-system-router/router-serial-number.png)

You can find detailed information on the registration process in the User guide. Follow the description on how to connect a device manually in [Device Management > Connecting devices](/users-guide/device-management/#device-registration-manually). 

After clicking the **Accept** button on the Cumulocity IoT platform, navigate to **All devices**. The router should appear here after registration. The default name of a router is "&#60;model&#62; (S/N &#60;serial number&#62;)", where &#60;model&#62; is the device model name. For example, the above router would appear as “NTC-221 (S/N 191611192800580)”.

Click on the router to view the detailed information and to access the functionality described in the remaining sections of this document. In order to distinguish a registered router from other devices in the listing, you can change the router’s name on the **Info** tab, which also displays basic information such as serial number of the router and SIM card data on the "Device data" widget. After clicking the edit icon at the bottom of the widget and changing the name, remember to click **Save** at the bottom of the "Device data" widget on the **Info** page.

![Device Info](/images/device-demos/casa-system-router/router-device-info.png)