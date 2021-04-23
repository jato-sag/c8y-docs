---
weight: 60
title: Managing data

---

### <a name="retention-rules"></a>Retention rules

Retention rules gives you control on how long data is stored in your account. By default, all historical data is deleted after 60 days (configurable in the system settings).

You might however want to store measurements for 90 days for example, but delete alarms already after 10 days.

Retention rules are usually run during the night. When you edit a retention rule, you will not see an immediate effect in the **Usage** section on the **Home** screen of the Administration application.

Click **Retention rules** in the **Management** menu to view a list of retention rules configured for your account.

<img src="/images/users-guide/Administration/admin-retention-rules.png" alt="Retention rules">

For each rule, the rule name, details on the data to be deleted (fragment type, type and source, see below) and the maximum age in days is provided.

The asterisk ("*") indicates that data with any value will be cleaned up.


#### <a name="add-retention-rule"></a>To add a retention rule

1. Click **Add rule** in the top menu bar.
2. In the resulting dialog box, select the type of data to be cleaned up (alarms, measurements, events, operations, audit logs or all).
3. Enter a fragment type if you want to be more specific about the data to be cleaned up. To clean up all connection loss alarms with this rule, select "alarms" and enter "c8y_UnavailabilityAlarm" as property into the **Type** field.
4. If you want to remove data only from a specific device, enter the device ID into the **Source** field.
5. Enter the **Maximum age** in days (max. allowed value is 10 years in days).
6. Click **Save** to save your settings.

The retention rule will be added to the list.

>**Info:** Per default, an asterisk ("*") is set in all fields except the **Maximum age** field, to include all values.

>**Info:** Alarms are only removed if they are in CLEARED state.

#### To edit a retention rule

Simply click the row of the rule you want to edit or click the menu icon at the right of the respective row and then click **Edit**.

For details on the fields, see [To add a retention rule](#add-retention-rule).


#### To delete a retention rule

Hover over the rule you want to delete and click the delete icon at the right.

<img src="/images/users-guide/Administration/admin-retention-rules-delete.png" alt="Delete retention rule">


### <a name="files"></a>Managing files in the file repository

The file repository provides an overview of the files stored in your account.

Click **Files repository** in the **Management** menu to see a list of files.

The files listed can come from various sources. They can be software images, configuration snapshots taken from devices, log files from devices or web applications uploaded from the **Own applications** page.

For each file, the name of the file, its owner, the file type (i.e. image/bmp, text/csv), its size and the date when it was last updated is provided.

<img src="/images/users-guide/Administration/admin-files-repository.png" alt="Files Repository" style="max-width: 100%">

#### To upload a file from your computer

Click **Upload file** in the top menu bar.

#### To download a file from your account

Click the menu icon at the right of the respective row and then click **Download**.


#### To delete a file from your account

Click the menu icon at the right of the respective row and then click **Delete**.

>**Info:** If the file corresponds to an active application, it cannot be deleted. You first need to remove or upgrade the application to be able to delete it.