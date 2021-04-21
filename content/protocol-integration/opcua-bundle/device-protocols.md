---
weight: 80
title: Device protocols
layout: redirect
---

### Adding a new device protocol

1. In the Device protocols page, click **New device protocol** in the top menu bar and select OPC UA as device protocol type.

2. In the resulting dialog box, enter a name and an optional description for the device protocol.

3. Optionally, a reference server can be selected. Selecting a reference server allows you to create device protocols based on the OPC UA model stored on an OPC UA server. This greatly simplifies the mapping process, as device protocols can be created based on OPC UA browse paths being actually present on the server.

4. Click **Create**.<br>
   ![Add new device protocol](/images/device-protocols/opcua/opcua-add-protocol.png)

> **Info:** Selecting a reference server will require you to select a reference node.

Once the device protocol is created, various configuration settings such as variables, data reporting and constraints can be applied. Initially, the device protocol will be inactive. When active, the gateway will scan the address space of all servers and will automatically apply the device protocol to all nodes which match the criteria. When the device protocol is configured, click **Save**.

### Adding a new variable

1. Click **Add variable** under the **Variables** section.
2. Enter the path and the name of the variable. The path can be the exact browse path or a regular expression of the browse path. If it is a regular expression, it must be wrapped inside *regex(...)*. For example: `regex(2:Objects)` or `regex(urn:test.namespace:Objects\\d)`. Note that the namespace index and the namespace URI are not part of the regular expression itself but they will be quoted as literal strings.
When using a regular expression, keep in mind that it might be matching many nodes in the address space and resulting in unexpected incoming data. Our recommendation is to use it with great care and together with other exact browse paths in the same mapping if possible. For example, `&#91;"2:Objects", "regex(2:MyDevice\\d)", "..."&#93;`
3. Choose either the default or the custom data reporting. The default option uses the data reporting mechanism used in the device protocol. The custom option will let you configure a data reporting mechanism only for the current variable.
4. Additionally, different functionalities such as sending measurements, creating alarms, sending events and custom actions for each variable can be selected.
5. Click **Save** to save your settings.

The gateway has a scheduling job and after the variables are saved, the gateway will check whether the variables exist under the subtree of the node. Afterwards, for each node a child device of the server is created. The child devices will contain data based on the configuration of the device protocol. The node child devices will also be listed in the **All devices** page.

> **Info:** If no reference server was selected during the device protocol creation, the path should be given with a namespace URI representation. In the OPC UA server the index value can be taken from the namespace array. An example namespace URI representation for browse path “5:Counter1” would be: *http://www.prosysopc.com/OPCUA/SimulationNodes:Counter1*. Node id equal to “ns=5;s=Simulation” will have the following namespace representation *'nsu=http://www.prosysopc.com/OPCUA/SimulationNodes;s=Simulation*. In both examples the server’s namespace array, the 5th element has the value of “http://www.prosysopc.com/OPCUA/SimulationNodes”.

![OPC UA device protocol](/images/device-protocols/opcua/opcua-device-protocol.png)

The functionalities that can be enabled are the following:

**Send measurement**

Turn on **Send measurement** to specify a measurement.

Specify the following parameters:

- Enter the type of the measurement, for example, “c8y_AccelerationMeasurement”.
- Series are any fragments in measurements that contain a “value” property, for example, “c8y_AccelerationMeasurement.acceleration”.
- Specify the unit of the given measurement, for example, “m/s” for velocity.

**Create alarm**

Turn on **Create alarm** if you want to create an alarm out of the resource.

Specify the following parameters (all mandatory):

- Severity - One of CRITICAL, MAJOR, MINOR, WARNING
- Type
- Status - One of ACTIVE, ACKNOWLEDGED, CLEARED
- Text

**Send Event**

Turn on **Send event** to send an event each time you receive a resource value.

Specify the following parameters:

- Enter the type of the event, for example, “com_cumulocity_model_DoorSensorEvent”.
- Enter the text which will be sent, for example, “Door sensor was triggered”. You can also get the resource value populated to the event text by defining the value placeholder:

	```plain
Door sensor was triggered, event value: ${value}
```

The value will also be populated as a fragment of the created event, under a static fragment name as the following:

```json
{
 "type": "com_cumulocity_model_DoorSensorEvent",
 "text": "Door sensor was triggered",
 "c8y_ua_DataValue": {
     "serverTimestamp": 132403410091850000,
     "sourceTimestamp": 132403410091850000,
     "value": {
         "value": 381632714
     },
     "statusCode": 0
 }
}
```
> **Info:** The measurements, events and alarms are added to a queue by the gateway, and they are flushed at once to create the respective elements. If the server is deleted, but there are still some items to be flushed, then the request is failed with a response code 403.
Thereafter, the exception is handled by validating the existence of the source. If the source is missing then the elements will be removed from the queue.

**Custom Actions**

Custom actions are HTTP POST requests which the gateway will send to a defined custom URL. You can define custom headers and body template with the following placeholders available:

- ${value}: value of specific node
- ${serverId}: ID of OPC-UA server
- ${nodeId}: ID of source node
- ${deviceId}: ID of source device

Below there is an example of a full device protocol that configures a custom action:

```json
{
   "name": "My device protocol for HttpPost",
   "referencedServerId": "{serverId}",
   "referencedRootNodeId": "ns=2;s=HelloWorld/Dynamic",
   "enabled": true,
   "subscriptionType" : {
     "type": "Subscription",
     "subscriptionParameters": {
       "samplingRate": 1000
     }
   },
   "applyConstraints": {
     "matchesNodeIds": [
       "ns=2;s=HelloWorld/Dynamic1"
     ]
   },
   "mappings": [
       {
           "browsePath": [
               "2:Double"
           ],
           "customAction": {
               "type": "HttpPost",
               "endpoint": "http://my.endpoint.local",
               "bodyTemplate": "{\"text\": \"I am coming from Http POST, value: ${value} \", \"type\": \"HttpPostMO\"}",
               "headers": {
                   "Authorization": "Basic MYAUTHCREDENTIALS==",
                   "Content-Type": "application/json"
               }
           }
       }
   ]
}
```

### Monitoring events for device protocol application

When a device protocol has been applied to or un-applied from a node, a monitoring event is generated as the following:

#### Device type has been applied

- Event type - c8y_ua_DeviceTypeApplied
- Event text - *Device type: {device type ID} is applied to root node: {root node ID} of server: {server ID}*
- Event source - The server managed object

![OPC UA device protocol applied](/images/device-protocols/opcua/opcua-device-protocol-applied.png)

#### Device type has been un-applied

- Event type - c8y_ua_DeviceTypeUnapplied
- Event text - 
    * If the device type has been un-applied from all nodes on the server: *Device type: {device type ID} is un-applied from all nodes of server: {server ID}*
    * If the device type has been un-applied from a specific node on the server: *Device type: {device type ID} is un-applied from root node: {root node ID} of server: {server ID}*
    * If all device types have been un-applied for the server: *All device types are un-applied for server: {server ID}* 
- Event source - The server managed object

![OPC UA device protocol un-applied](/images/device-protocols/opcua/opcua-device-protocol-unapplied.png)

#### Custom action retry mechanism on external server failure

If a custom action fails, a retry mechanism will be processed. This is configured in the application YAML file, and the queues will be stored in the event repository. 
 
Queues are collections of failed custom actions, including the complete HTTP request of this custom action. Each entry of the queue is one failed custom action. The collection has a defined size in _failedCustomActionQueueSize_ and a maximum number of retries in _maxRetries_.  

A background scheduler task will retry each queue up to the number of _maxRetries_. If _maxRetries_ is reached the queue will be stored as a permanently failed queue in the event repository. 

All elements of the queue will be retried, so the count of the elements in the queue will be decreasing with each successful retried custom action. These queues are also timing out when the reach they _pendingMaxAge_ to reduce the load of the scheduler task.

The following parameters can be set:  

In the section _mappingExecution_ - _http_ - _failureHandling_  

- enabled[boolean] - Activate or deactivate the fail over for custom actions, default is true.

- flushQueueDelay[seconds] - Time until a queue will be cleared automatically, default is 60.

- reScheduleDelay[seconds] - Time until the stored queues will be rescheduled, should be higher than _flushQueueDelay_ and not a multiple value of _flushQueueDelay_, default is 150.

- reScheduleElements[number] - Number of queues loaded for retry at the same time, default is 100.

- failedCustomActionQueueSize[number] - Size of maximum elements in one queue; if the limit is reached the queue will be saved, default is 100.

- maxRetries[number] - Number of retries for failed queues; if the maximum is reached the queue will be saved as permanently failed and never retried again, default is 5.

- pendingMaxAge[seconds] - Queues with a timestamp older than this will not be retried regardless of the retry status, default is 86400 .