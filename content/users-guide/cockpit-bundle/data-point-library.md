---
weight: 75
title: Data point library
layout: redirect
helpcontent: >-
  The data point library provides a collection of data points with default values for data point properties, which serve as templates that can be applied easily to your data points from different devices. To find default values for a data point like color or label, the Cumulocity IoT platform searches the data point library for a matching entry. If an entry matches, the corresponding data point properties are used for the default visualization.


  Either select one of the existing data points from the list or add a new data point to the library to meet your individual needs.
---


The data point library provides a collection of data points with default values for data point properties.

Data point properties are similar to paragraph formats in word processing applications. You do not want to format each paragraph individually. Instead you want to define a set of default formats and apply them to your paragraphs in your document. The data point library provides the same functionality for data points. It provides a number of default data point templates that can be applied easily to your data points from different devices.

How does the Cockpit application use the data point library? To find the default visualization for a data point like color or label, the Cumulocity IoT platform searches the data point library and tries to find a matching entry. An entry is considered as "matching", if the values for fragment and series in the data point library match those of the measurement. If a matching entry is found, the corresponding data point properties are used for a default visualization.

Additionally, the properties of the data point library are used by threshold business rules: The red and yellow values configured in the data point library are used by the threshold rules to raise alarms.

To open the data point library, click **Data point library** in the **Configuration** menu of the navigator.

![Data point library](/images/users-guide/cockpit/cockpit-data-point-library.png)

A list of available data points will be opened. For each data point, the following information is provided in the list:

* Color and label for the data point
* Fragment name and series
* Measurement unit
* Values (minimum, maximum, red/yellow ranges)

### To add a data point to the library

1. Click **Add data point** in the top menu bar.
2. Provide the following information:

  |Field|Description|
|:---|:---|
|Color|Color for the data point visualization
|Label|Label to identify the data point
|Fragment|Name of the fragment
|Series|Name of the series
|Unit|Unit used for the measurement
|Target|Target value
|Minimum|Minimum value shown on the y-axis
|Maximum|Minimum value shown on the y-axis
|Yellow range|Min/max values for the yellow range (MINOR alarms)
|Red range|Min/max values for the red range (CRITICAL alarms)

3. Click **Save** to add the data point to the library.

### To edit a data point

Simply click the respective entry in the list or click the menu icon at the right of an entry and then click **Edit**.


### To delete a data point

Click the menu icon at the right of an entry and then click **Delete**.