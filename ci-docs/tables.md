---
title: "Tables in Customer Insights"
description: "View data on the Tables page."
ms.date: 12/7/2022
ms.reviewer: mhart
ms.topic: conceptual
author: mukeshpo
ms.author: mukeshpo
searchScope: 
  - ci-entities
  - customerInsight
---

# Tables in Customer Insights

After [configuring your data sources](data-sources.md), evaluate the quality of the ingested data on the **Tables** page. Multiple capabilities of Dynamics 365 Customer Insights are built around these tables. Reviewing them closely can help you validate the output of those capabilities.

As you work in Customer Insights enriching your data or creating segments, measures, and activities, the tables that are created from those actions display on the **Tables** page.

> [!TIP]
> Tables were previously called entities.

## View a list of tables

Go to **Data** > **Tables** to view a list of tables. The following information displays for each table.

- **Name**: Name of the data table. If you see a warning symbol next to a table name, it means that the data for that table didn't load successfully.
- **Source**: Type of data source that ingested the table.
- **Updated**: Time the table was last updated.
- **Status**: Details about the last update of the table.

For more information about the **Relationships** tab, see [Relationships](relationships.md).

## Explore a specific table's data

1. Go to **Data** > **Tables**.
1. Select a table to open the details page.  
1. Explore the different fields and records included for that table.

- The **Attributes** tab is selected by default and shows details for the selected table, such as field names, data types, and types. The **Type** column shows Common Data Model associated types, which are either auto-identified by the system or [manually mapped](data-unification-map-tables.md) by users. These types are semantic types that can differ from the attributes' data types. For example, the field *Email* below has a data type *String* but its (semantic) Common Data Model type might be *Email*, *EmailAddress*, or *Identity.Service.Email*.

   :::image type="content" source="media/data-manager-tables-fields.png" alt-text="Fields table.":::

   > [!NOTE]
   > This page shows only a sample of your table's data. To view the full data set, go to the **Data sources** page, select a table, select **Edit**, and then view this table's data with the Power Query editor as explained in [Data sources](data-sources.md).

   To learn more about the data ingested in the table, the **Summary** column provides some important data characteristics, such as nulls, missing values, unique values, counts, and distributions, whatever is applicable to your data. Select the chart icon to see the summary of the data.

- The **Data** tab shows details about individual records of the table. Details listed depend on the table's data type.

   :::image type="content" source="media/data-manager-tables-data.png" alt-text="Select a table.":::

- The **Reports** tab (available for some tables) enables you to visualize your data by creating a report, which includes these columns:

  - **Report name**: Name of the report.
  - **Created by**: Name of the person who created the table.
  - **Created**: Date and time of the table creation.
  - **Edited by**: Name of the person who modified the table.
  - **Edited**: Date and time of the table modification.

## Customer Insights tables in Dataverse

Some Customer Insights tables are available in Dataverse. The sections below describe the expected schema of these tables.

- [CustomerProfile](#customerprofile)
- [UnifiedContact](#unifiedcontact)
- [AlternateKey](#alternatekey)
- [UnifiedActivity](#unifiedactivity)
- [CustomerMeasure](#customermeasure)
- [Enrichment](#enrichment)
- [Prediction](#prediction)
- [Segment membership](#segment-membership)

### CustomerProfile

This table contains the unified customer profile from Customer Insights. The schema for a unified customer profile depends on the tables and attributes used in the data unification process. A customer profile schema usually contains a subset of the attributes from the [Common Data Model definition of CustomerProfile](/common-data-model/schema/core/applicationcommon/foundationcommon/crmcommon/solutions/customerinsights/customerprofile). For the B-to-B scenario, the customer profile contains unified accounts, and the schema usually contains a subset of the attributes from the [Common Data Model definition of Account](/common-data-model/schema/core/applicationcommon/foundationcommon/crmcommon/account).

### UnifiedContact

A UnifiedContact contains unified information about a contact. Contacts are [individuals that are mapped to an account](data-unification-contacts.md) in a B-to-B scenario.

| Column                       | Type                | Description     |
| ---------------------------- | ------------------- | --------------- |
|  BirthDate            | DateTime       |  Date of birth of the contact               |
|  City                 | Text |  City of the contact address               |
|  ContactId            | Text |  ID of the contact profile               |
|  CountryOrRegion      | Text |  Country/Region of the contact address               |
|  CustomerId           | Text |  ID of the account the contact is mapped to               |
|  TableName            | Text |  Name of the table               |
|  FirstName            | Text |  First name of the contact               |
|  FK_AccountID         | Text |  GUID representing the unified account  |
|  FK_ContactToAccountID| Text |  Unified source value for the contact's associated account |
|  Gender               | Text |  Gender of the contact               |
|  Id                   | Text |  Deterministic GUID based on `Identifier`               |
|  Identifier           | Text |  Internal ID of the contact profile: `UnifiedContact|CustomerId|ContactId`               |
|  JobTitle             | Text |  Job title of the contact               |
|  LastName             | Text |  Last name of the contact               |
|  PostalCode           | Text |  ZIP code of the contact address               |
|  PrimaryEmail         | Text |  Email address of the contact               |
|  PrimaryPhone         | Text |  Telephone number of the contact               |
|  StateOrProvince      | Text |  State or province of the contact address               |
|  StreetAddress        | Text |  Street of the contact address               |
|  UnifiedContactId     | Unique identifier   |  GUID for the contact               |

### AlternateKey

The AlternateKey table contains keys of the tables, which participated in the unify process.

|Column  |Type  |Description  |
|---------|---------|---------|
|DataSourceName    |Text         | Name of the data source. For example: `datasource5`        |
|TableName        | Text        | Name of the table in Customer Insights. For example: `contact1`        |
|AlternateValue    |Text         |Alternative ID that is mapped to the customer ID. Example: `cntid_1078`         |
|KeyRing           | Text        | JSON value  </br> Sample: [{"dataSourceName":" datasource5 ",</br>"tableName":" contact1",</br>"preferredKey":" cntid_1078",</br>"keys":[" cntid_1078"]}]       |
|CustomerId         | Text        | ID of the unified customer profile.         |
|AlternateKeyId     | Unique identifier        |  AlternateKey deterministic GUID based on `Identifier`      |
|Identifier |   Text      |   `DataSourceName|TableName|AlternateValue`  </br> Sample: `testdatasource|contact1|cntid_1078`    |

### UnifiedActivity

This table contains activities by users that are available in Customer Insights.

| Column            | Type        | Description                                                                              |
|-------------------|-------------|------------------------------------------------------------------------------------------|
| CustomerId        | Text      | Customer profile ID                                                                      |
| ActivityId        | Text      | Internal ID of the customer activity (primary key)                                       |
| SourceTableName  | Text      | Name of the source table                                                                |
| SourceActivityId  | Text      | Primary key from the source table                                                       |
| ActivityType      | Text      | Semantic activity type or name of custom activity                                        |
| ActivityTimeStamp | DateTime    | Activity time stamp                                                                      |
| Title             | Text      | Title or name of the activity                                                               |
| Description       | Text      | Activity description                                                                     |
| URL               | Text      | Link to an external URL specific to the activity                                         |
| SemanticData      | Text | Includes a list of key value pairs for semantic mapping fields specific to the type of activity |
| RangeIndex        | Text      | Unix timestamp used for sorting activity timeline and effective range queries |
| UnifiedActivityId   | Unique identifier | Internal ID of the customer activity (ActivityId) |

### CustomerMeasure

This table contains the output data of customer attribute-based measures.

| Column             | Type             | Description                 |
|--------------------|------------------|-----------------------------|
| CustomerId         | Text           | Customer profile ID        |
| Measures           | Text      | Includes a list of key value pairs for measure name and values for the given customer |
| Identifier | Text           | `Customer_Measure|CustomerId` |
| CustomerMeasureId | Unique identifier     | Customer profile ID |

### Enrichment

This table contains the output of the enrichment process.

| Column               | Type             |  Description                                          |
|----------------------|------------------|------------------------------------------------------|
| CustomerId           | Text           | Customer profile ID                                 |
| EnrichmentProvider   | Text           | Name of the provider for the enrichment                                  |
| EnrichmentType       | Text           | Type of enrichment                                      |
| Values               | Text      | List of attributes produced by the enrichment process |
| EnrichmentId | Unique identifier            | Deterministic GUID generated from `Identifier` |
| Identifier   | Text           | `EnrichmentProvider|EnrichmentType|CustomerId`         |

### Prediction

This table contains the output of the model predictions.

| Column               | Type        | Description                                          |
|----------------------|-------------|------------------------------------------------------|
| CustomerId           | Text      | Customer profile ID                                  |
| ModelProvider        | Text      | Name of the provider of the model                                      |
| Model                | Text      | Model name                                                |
| Values               | Text | List of attributes produced by the model |
| PredictionId | Unique identifier       | Deterministic GUID generated from `Identifier` |
| Identifier   | Text      |  `Model|ModelProvider|CustomerId`                      |

### Segment membership

This table contains segment membership information of the customer profiles.

| Column        | Type | Description                        |
|--------------------|--------------|-----------------------------|
| CustomerId        | Text       | Customer Profile ID        |
| SegmentProvider      | Text       | App that publishes the segments.      |
| SegmentMembershipType | Text       | Type of customer for this segment membership record. Supports multiple types such as Customer, Contact, or Account. Default: Customer  |
| Segments       | Text  | List of unique segments the customer profile is a member of      |
| Identifier  | Text   | Unique identifier of the segment membership record. `CustomerId|SegmentProvider|SegmentMembershipType|Name`  |
| SegmentMembershipId | Unique identifier      | Deterministic GUID generated from `Identifier`          |


[!INCLUDE [footer-include](includes/footer-banner.md)]
