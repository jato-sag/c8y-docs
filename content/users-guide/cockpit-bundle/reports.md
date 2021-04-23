---
weight: 60
title: Managing reports and exports
layout: redirect
---

### <a name="reports"></a>Managing reports

Dashboard reports enable you to track applications, alarms, assets, events and many other widgets.

Dashboard reports are global dashboard pages, regardless of the asset hierarchy.

To see all existing reports, expand the **Reports** menu in the navigator.

![Reports menu](/images/users-guide/cockpit/cockpit-reports-navigator.png)

Click a report in the navigator to open it.

#### To create a report

1. Click the **Plus** button in the top bar and then click **New report**.
2. Enter a name for the report and optionally select an icon from the dropdown list.
3. Click **Save** to save your settings.

Next, widgets can be added to the report.

#### To add widgets to reports

You can add widgets to reports in the same way as adding widgets to dashboards.

1. Open the report you want to edit from the navigator.
2. Click **Add widget** in the top menu bar and select a widget type from the list.

For details on all widgets types available, refer to [Widgets collection](#widgets).

#### To delete a report

1. Open the report you want to delete.
2. Click **More...** at the right of the top menu bar and then click **Remove report**.


### <a name="export"></a>Exporting data

The export functionality lets you export specific data to either CSV or Excel files.

With this feature, you can request data for the whole tenant. Additionally, you can choose to filter for specific devices, time ranges or fields. The export data contains information about all specified filters and enabled fields.

>**Info:** The maximum number of documents that can be exported into a single file is 1 million. If the number of documents for defined filters exceeds this limit, only the first 1 million documents will be taken.

To show all exports, click **Export** in the **Reports** menu.

In the **Export** page you will find a list displaying all exports with their names and time range.

![Exports](/images/users-guide/cockpit/cockpit-exports.png)


#### <a name="add-export"></a>To add an export

1. Click **Add export** in the top menu bar.<br>
	![Create export](/images/users-guide/cockpit/cockpit-export-create.png)

2. Enter a name for the export and select the file type (CSV or XLSX) for the report output.


**Filters**

In the **Filter** section, you can select filters to request object- or time-specific data.

To filter for a particular object, enter a name or property value into the search field and click the search icon. All matching devices or groups will be displayed below the **Value** field. Click an object to select it (highlighted in green).

>**Info:** If you select a group, the data of direct child devices will be included. However the export will not contain the data of devices in subgroups (indirect children).

The **Time range** filter can filter data for a specific time range. Select a time range from the dropdown field. This may be one of "Last year", "Last month", "Last week" or select "Custom" and enter a custom from/to range in the additional fields.

Select the **Object to export** and **Time range** checkboxes to enable the respective filters.

**Fields**

Apart from object- and time-specific filtering you may filter data for specific fields:

- Alarms
- Events
- Managed objects
- Measurements

Use the toggle to enable/disable a field.

![Filter fields](/images/users-guide/cockpit/cockpit-export-fields.png)

>**Info:** The time range filter only applies to alarms, events and measurements but not to managed objects. If selected, managed objects will appear in the export, regardless of any specified time range.

When a field is enabled, predefined or empty properties can be added.

##### To add a property

Click **Add** to add empty properties. To enter a label or path, click **Column** or **Path** and edit the field. For example, if you enable the **Alarms** field you could enter "Severity" in column and path to receive data for alarm severities.

Click **Add predefined**, to add predefined properties. Simply select the desired properties from the list and click **Select**. Use the search field at the top to search for a specific property.

![Select properties](/images/users-guide/cockpit/cockpit-export-properties.png)

If you have at least one field that is not originating from the "Add predefined" list but defined as a custom property, then you need to set up at least one property for the custom values to appear in the export.

Example:
An export has 4 fields defined: time range, device name, type and c8y&#95;SpeedMeasurement.speed.value. The first 3 are predefined properties, while the last one is a custom property. If any measurement for export does not have a custom property c8y_SpeedMeasurement.speed.value, then it will not appear in the export file.

If your field is a valid.key.with.dot then refer to it as ['fragment.key.with.dot'] in the path, e.g.: ['fragment.key.with.dot'].series.value

In case of measurements enabled, you can also choose **Add from data point**. For details on how to add data points see [Adding data points](#add-data-points).

#### <a name="schedule-export"></a>To schedule an export

To schedule an export to a CSV or XLSX file to any point in time, open the respective export and click **Add schedule**.

![Export details](/images/users-guide/cockpit/cockpit-export-add-schedule.png)

In the resulting dialog box provide the following information to receive the scheduled export via email.

![Schedule export](/images/users-guide/cockpit/cockpit-export-new-schedule.png)

**1 - Frequency**

Select the frequency for sending the export from the dropdown list, i.e. every hour, day, week, month or year. Depending on the frequency selected, provide additional timing information. For example, if you have selected "every month", provide the day of month, hour and minute.

>**Info:** Schedule intervals need to be provided in Coordinated Universal Time (UTC).

**2 - Send email:**

Complete the email information.

In the **Send to** field, provide the email address of the recipient. This field is mandatory. Optionally, you can provide email addresses for recipients of copies (CC) or blind copies (BCC). Use comma as separator to enter multiple recipients.

Optionally, add the email address of the sender for reply.

Specify the subject of the email. This field is pre-filled, but may be modified.

Enter the actual email message. Available placeholders are {host}, {binaryId}. The default value is "File with exported data can be downloaded from {host}/inventory/binaries/{binaryId}".

>**Info:** Note that the corresponding emails are send with "text/html" as content type.

Click **Create** to create the new export schedule.

The export schedule will be added to the export details.

![Scheduled exports list](/images/users-guide/cockpit/cockpit-export-schedule-list.png)

##### Migration of scheduled exports

With version 10.6.2, a new reporting agent has been implemented to allow scheduled reports with [Apama Streaming Analytics](/apama/overview-analytics/). The export schedules functionality based on smart rules has been deprecated.

Previously existing configurations of schedulers may be migrated to the new agent by opening the respective report and confirm to migrate the included export schedules.

![Export schedule migration message1](/images/users-guide/cockpit/cockpit-export-migrate1.png)

> **Info:** To use the new export schedule feature and for the migration to work, the report-agent microservice needs to be subscribed. New tenants will be subscribed to it automatically. Existing tenants should make sure that they are subscribed to it.

#### To export data

To export data to a CSV or XLSX file, select the checkbox in front of the respective row in the list and at the left of the top menu bar click **Export**.

You will receive an e-mail containing links to each export file.

Standard time properties of documents (like time or creationTime in alarms) are exported to

* xlsx file in the format: 03/13/2016 00:00:24
* CSV file in the format: 2016-03-13T00:01:24.000Z

Only CSV time contains milliseconds and timezone.

#### To edit an export

Just click the respective row or click the menu icon at the end of the row and then click **Edit**.

For details on the fields see [To add an export](#add-export).


#### To duplicate an export

1. Click the menu icon at the end of the row and then click **Duplicate**.
2. Modify at least the name.
3. Click **Save & close** to save the export and return to the export list.

#### To delete an export

Click the menu icon at the end of the row and then click **Delete**.