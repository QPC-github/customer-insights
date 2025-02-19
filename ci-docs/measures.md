---
title: "Create and manage measures"
description: "Create and manage measures to help analyze and reflect the performance of your business."
author: v-wendysmith
ms.author: wameng
ms.reviewer: v-wendysmith
ms.topic: how-to
ms.date: 03/20/2023
ms.custom: bap-template
searchScope: 
  - ci-measures
  - ci-measure-builder
  - ci-measure-template
  - ci-enrichment-details
  - customerInsights
---

# Create and manage measures

Measures help you to better understand customer behaviors and business performance. They look at relevant values from [unified profiles](data-unification.md). For example, a business wants to see the *total spend per customer* to understand an individual customer’s purchase history or measure *total sales of the company* to understand the aggregate-level revenue in the whole business. Some [service limits](/dynamics365/customer-insights/service-limits) apply.

## Create measures

Create measures to plan business activities by querying customer data and extract insights. For example, create a measure of *total spend per customer* and *total return per customer* to help identify a group of customers with high spend yet high return. Then, [create a segment](segments.md) based on these measures to drive next best actions.

Choose how to create a measure based on your target audience.

# [Individual consumers (B-to-C)](#tab/b2c)

- From scratch with measure builder: [Build your own](measure-builder.md).
- From commonly used measures: [Use predefined templates](measure-templates.md).

# [Business accounts (B-to-B)](#tab/b2b)

From scratch with measure builder: [Build your own](measure-builder.md).

---

## Manage existing measures

Go to the **Insights** > **Measures** page to view the measures you created, their status, measure type, and the last time the data was refreshed. You can sort the list of measures by any column or use the search box to find the measure you want to manage.

Select next to a measure to view available actions. Select the measure name to preview the output and download a CSV file.

:::image type="content" source="media/measures-actions.png" alt-text="Actions to manage single measures."lightbox="media/measures-actions.png":::

> [!TIP]
> Supported bulk operations include: refresh, delete, change state (activate/deactivate), and tags.

- **Edit** the measure to change its properties.
- **Refresh** one or more measures manually to include the latest data.
- **Rename** the measure.
- **Activate** or **Deactivate** one or more measures. For multiple measures, select **Change state**. Inactive measures won't get refreshed during a [scheduled refresh](schedule-refresh.md) and have the **Status** listed as **Skipped**, indicating that a refresh wasn't even attempted.
- **Tag** to [manage tags](work-with-tags-columns.md#manage-tags) for one or more measures.
- **Delete** one or more measures.
- [**Schedule**](measures-schedule.md) to customize schedules for measures.
- **Columns** to [customize the columns](work-with-tags-columns.md#customize-columns) that display.
- **Filter** to [filter on tags](work-with-tags-columns.md#filter-on-tags).
- **Search name** to search by measure name.

## Manage the number of active measures

When you approach or exceed the number of active measures based on the [service limits](service-limits.md), you might experience the following:

- Typical system refresh time is slower
- Running or refreshing individual measures is slower
- Refresh failures indicating out of memory

The complexity of your measures can also impact performance. To help you prevent performance issues, Customer Insights provides messages or warnings when you approach, reach, or exceed the total number of active measures. These messages display on the **Measures** list page. If you encounter these messages or symptoms, see the following recommendations.

1. Delete old or no longer relevant measures even if they are static or inactive.
1. [Schedule individual measures](measures-schedule.md) to run weekly or monthly during slow business days (such as the weekend) instead of daily.


[!INCLUDE [footer-include](includes/footer-banner.md)]
