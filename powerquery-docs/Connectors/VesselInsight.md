---
title: Power Query Vessel Insight connector
description: Provides basic information and prerequisites for the connector, descriptions of the optional input parameters, and discusses limitations and issues you might encounter.
author: cecilib

ms.topic: conceptual
ms.date: 1/05/2022
ms.author: 
LocalizationGroup: reference
---

# Vessel Insight
 
## Summary

| Item | Description |
| ---- | ----------- |
| Release State | General Availability |
| Products | Power BI (datasets)
| Authentication Types Supported | Organizational account |
|

## Prerequisites
Before you can sign in to Vessel Insight, you must have an organization account (username/password) connected to a tenant.

 
## Capabilities Supported
* Import

## Connect to Vessel Insight

To connect to Vessel Insight:

1. Select **Get Data** from the **Home** ribbon in Power BI Desktop. Select **Other** from the categories on the left, select **VesselInsight**, and then select **Connect**.

   ![Get Data from Vessel Insight.](./media/VesselInsight/get-vi-data.png)

2. If this is the first time you're getting data through the Adobe Analytics connector, a third-party notice will be displayed. Select **Don't warn me again with this connector** if you don't want this message to be displayed again, and then select **Continue**.

3. To sign in to your Vessel Insight account, select **Sign in**.

   ![Select sign in button.](./media/VesselInsight/sign-in.png)

4. In the window that appears, provide your Vessel Insight tenant URL in the format "[companyname].kognif.ai". Click **Validate**

    ![Insert Vessel Insight tenant.](./media/VesselInsight/tenant-url.png)

5. In the window that appears, provide your credentials to sign in to your Vessel Insight account. 

   ![Sign in to Vessel Insight.](./media/VesselInsight/vi-sign-in.png)

   If you entered an email address and password, select **Continue**.

6. Once you've successfully signed in, select **Save**.

   ![Signed in and ready to connect.](./media/VesselInsight/signed-in.png)

Once the connection is established, you can preview and select data within the **Navigator** dialog box to create a single tabular output. 

![Select data using Navigator.](./media/VesselInsight/navigator-view.png)



Here you have the options to select:
* **Advanced** - write custom TQL queries (native). For advanced Kongsberg users
* **Vessel Insight Data (deprecated)** - time series data for your fleets in old asset hierarchy
* **Vessel Insight Data 2.0** - time series data for your fleets in new asset hierarchy. Only tags with data will be shown
* **Voyage** - voyage history and location data from AIS


You can provide any optional input parameters required for the selected items. For more information about these parameters, see [Optional input parameters](#optional-input-parameters). 

If you don't input parameters for **Vessel Insight Data 2.0**, you will get the latest value by default. 

![Default value.](./media/VesselInsight/navigator-default.png)

For **Voyage**, you need to input IMOs that you want to fetch data for.
![Voyage IMO parameter.](./media/VesselInsight/navigator-options-voyage-IMO.PNG)

You can **Load** the selected time series data, which brings the one table for each selected time series tag into Power BI Desktop, or you can select **Transform Data** to edit the query, which opens Power Query Editor. You can then filter and refine the set of data you want to use, and then load that refined set of data into Power BI Desktop. 

![Load or transform data.](./media/VesselInsight/load-transform.png)




## Optional input parameters


#### Vessel Insight Data 2.0
When you import time series data through the Vessel Insight Data 2.0 node and you've selected the tags you want to load or transform in the Power Query **Navigator** dialog box, you can also limit the amount of data by selecting a set of optional input parameters.

![Optional input parameters for Vessel Insight Data.](./media/VesselInsight/navigator-options.png)

These input parameters are:

* **Interval** (optional) - how you want the data to be aggregated when displayed (1s, 5s, >=30s, 1m, 1h, 1d )
* **Time** (optional) - set time filter type of you want to filter on time. 
  * Latest: Get latest value only. Will return 1 value
  * Period: Filter on time range. Requires setting Start and End date below 
  * Custom: custom query to filter on number of values to return
* **Start** (Time:Period), e.g. 2019-10-08T00:00:00Z (optional) - filter on range by inserting start date and time here. Possible to set "yesterday" and "today". Requires setting Time: Period.
* **End** (Time:Period), e.g. 2019-10-08T01:00:00Z (optional) -  filter on range by inserting end date and time here. Possible to set "today" and "now". Requires setting Time: Period. 
* **Custom** (Time: Custom), e.g. |> takebefore now 5 (optional) - add custom query to filter on number of values. "|> takebefore now 5" means take 5 values before the time now. Requires Time: Custom

 When importing aggregated timeseries, the connector will return avg, min, max and count by default.

If you are importing multiple tags, it can be cumbersome to input the parameters manually for each tag. In this case, we recommend to use **Power Query parameters** for Start and End date in the Power Query Editor: [Power Query parameters](https://docs.microsoft.com/en-us/power-query/power-query-query-parameters)

#### Voyage
When you import voyage data through the Voyage node, you can limit the amount of data for "History" and "Location History" table by setting a set of optional input parameters.

![Optional input parameters for voyage .](./media/VesselInsight/navigator-options-voyage.png)

These input parameters are:
* **Comma Separated IMOs** - Input one or multiple IMO numbers you want voyage data for
* **Start** (Time:Period), e.g. 2019-10-08T00:00:00Z (optional) - filter on range by inserting start date and time here. Possible to set "yesterday" and "today". Requires setting Time: Period.
* **End** (Time:Period), e.g. 2019-10-08T01:00:00Z (optional) -  filter on range by inserting end date and time here. Possible to set "today" and "now". Requires setting Time: Period. 

## Limitations and issues

You should be aware of the following limitations and issues associated with accessing Vessel Insight data.

* There is a general limit of 1GB data that is imported into Power BI, unless the workspace is in a Power BI Premium capacity. It is recommended to aggregate and choose short date range when importing time series data as it can become heavy.

* Each time series tag with associated values will be outputted in a separate table in Power BI. If it is necessary to combine tags and values into one single table, they need to be merged in Power Query Editor or with TQL queries.

* The time series data is currently stored in Couchbase which might have weaknesses that impacts the Power BI connector. 

* The API request timeout is by default 1 minute.

For additional guidelines on accessing Vessel Insight data, see [The Getting started guide](https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fwww.kongsberg.com%2Fglobalassets%2Fdigital%2Fsolutions%2Fvessel-insight%2Fpowerbi-gsx.pptx&wdOrigin=BROWSELINK).

## Recommended content

You may also find the following Vessel Insight information useful:

* [About Vessel Insight Power BI connector](https://www.kongsberg.com/digital/solutions/vessel-insight/vessel-insight-power-bi-connector/)
* [About Vessel Insight](https://www.kongsberg.com/digital/solutions/vessel-insight/)
* [Vessel Insight API](https://developer.kognif.ai/)