---
title: "Issues and FAQs about pay-as-you-go plans | MicrosoftDocs"
description: This topic addresses known issues about pay-as-you-go plans and provides answers to frequently asked questions.
author: Kavishi
ms.component: pa-admin
ms.topic: conceptual
ms.date: 03/08/2022
ms.subservice: admin
ms.author: kaagar 
ms.reviewer: jimholtz
contributors:
  - ShawnNandiMSFT
search.audienceType: 
  - admin
search.app:
  - D365CE
  - PowerApps
  - Powerplatform
  - Flow
---

# Known issues and frequently asked questions 

## Known issues 
- Pay-as-you-go billing and reporting is not available in Norway and Korea (South).
- Deleting a billing policy in the Power Platform admin center will not automatically delete corresponding Power Platform account resource in the Azure portal. This resource can be deleted manually in the Azure portal, if needed.
- The Power Platform requests meter is planned to be in preview by the end of March 2022. During this preview we will report on usage of Power Platform requests, however, we will not bill for this usage until we reach general availability (GA) for this meter. If you link an environment to an Azure subscription, users and flows in the environment can consume more than their entitled usage without being throttled or paying for overages.
- The report for the Power Platform request meter does not currently show correct entitlements for users licensed via the Power Apps Per App license or Power Apps Per App pay-as-you-go meter. Entitlements for such users will shown as 0 when in fact they should be shown as 6000 (requests per 24h period) as outlined in https://aka.ms/platformlimits.
- Multi-factor authentication: if you have multi-factor authentication enabled for the Azure portal, you may see an error when you try to link an Azure subscription from the Power Platform admin center. This issue is planned for resolution by the end for March 2022. 

## Frequently asked questions 

### When should I consider pay-as-you-go billing over existing Power Apps subscription plans?
The addition of pay-as-you-go provides the flexibility to pay based on the number of unique apps or portals a user runs each month. Some common scenarios where it might be useful:

- When you have a team of professional developers who already have access to an Azure subscription. Using their existing subscription to use Power Apps may help reduce procurement processes while maintaining consistency with other services the team is consuming from Microsoft.
- When you're exploring premium capabilities but you're unsure how many licenses to procure in advance. Enabling pay-as-you-go delivers the flexibility to establish usage patterns, which could then be transitioned into subscription licenses, if needed.
- When an app needs to be shared with a large user base, though usage and frequency may significantly fluctuate. In this case, pay-as-you-go would enable you to pay only for users who ran an app during the monthly billing period.

### Is pay-as-you-go available for both canvas apps and model-driven apps?
Yes.

### How is the Power Apps per-app meter unit counted?
The count is the number of unique users who opened an app or a portal in the course of a month. Repeat access to the same app or portal is counted only once. Read [Power Apps per-app meter](pay-as-you-go-meters.md#power-apps-per-app-meter) for more details.

### Can I set up pay-as-you-go for my environment without an Azure subscription?
No. You need an Azure subscription to set up pay-as-you-go.

### Which environments are available for pay-as-you-go?
Currently, production and sandbox environments are available.

### Can pay-as-you-go be set up for individual apps?
No. Pay-as-you-go is set up for an environment and all apps within that environment are billed against the associated Azure subscription. However, you can exclude an app from using the Azure subscription, in which case a user will need a per-user license to use the app. Per-app licenses cannot be used in a pay-as-you-go environment.

### What if I already have a user license and I use an app in a pay-as-you-go-enabled environment? Will I be billed against the Azure subscription?
Users with per-user licenses aren't counted towards the Power Apps per-app meter, and therefore won't incur charges. However, note that when an environment is linked to an Azure subscription, Dataverse capacity overages will be billed to the Azure subscription. Any Dataverse capacity granted for the per-user license will still be pooled at a tenant level but won't apply to a pay-as-you-go-enabled environment. Pay-as-you-go environments grant 1 GB of Dataverse database storage and 1 GB file capacity.

### What happens if I have an Office license and use an app with standard connectors in a pay-as-you-go-enabled environment?
Those who are using an app with standard connectors and have Office licenses are not counted towards the Power Apps per-app meter, and therefore won't incur charges.

### Can guest users use apps in a pay-as-you-go environment without licenses?
Yes.

### What if a user runs the same app multiple times in a month? How will that user be charged?
Pay-as-you-go billing only counts unique monthly active users of an app. Repeat access of the same app by a user in a single month results in only one charge for that user that month.

### If a user runs multiple apps in a single environment, how will that user be charged?
You'll be charged for the number of apps that a unique user accesses in a month. If a user runs three different apps in a month, you'll be charged for three active users.

### What if my app is already using app passes that are available in the environment? Can I still use pay-as-you-go billing for my app?
Yes, you can set up pay-as-you-go for your app's environment. Doing so will disregard the app passes and you can pay for your app via Azure subscription.

### Can I use pay-as-you-go billing for some apps and use per-app passes for the others in the same environment?
No. As soon as you enable pay-as-you-go for your environment, all apps will be billed against it.

### I don't have admin permissions for the environment I'm working with. Can I set up pay-as-you-go for the environment?
No. You need admin permissions for the environment to be able to link the environment to a billing policy. Check out [Who can set it up](pay-as-you-go-set-up.md#who-can-set-it-up) for details on permissions.

### Can I enable/disable specific meters?
No. Once you enable pay-as-you-go, both the Power Apps per app-meter and Dataverse meter will be enabled, and both app access and storage will be charged.

### How is Dataverse capacity calculated when one environment is enabled for pay-as-you-go and the other is not within my tenant?
Environments draw from a tenant-wide pool of Dataverse storage. However, when an environment is linked to an Azure subscription, it stops drawing from the tenant-wide pool. All pay-as-you-go environments will get an initial entitlement of 1 GB of Dataverse database and 1 GB of Dataverse file storage capacities to cover the typical initial storage footprint consumed by Dataverse. Any usage above the initial entitlement is billed to Azure via the Dataverse pay-as-you-go meter. 

### Is there throttling if I exceed Power Platform requests entitlements in a pay-as-you-go environment?
In the context of Power Platform Request entitlement limits, any high usage throttling will be removed when an environment has pay-as-you-go enabled.  When Power Platform Request metering is active in the Public Preview, if you exceed a daily entitlement limit, you will automatically be charged for the overages via Azure subscription without experiencing high usage throttling. 

> [!NOTE]
> This does not supersede [Service Protection Limit](/powerapps/developer/data-platform/api-limits) browser errors that are separate from high usage throttling.  If service protection limits are exceeded, the user could still experience issues on client applications described on the service protection limits page.

### Can I stop using pay-as-you-go billing at any time?
Yes, you can disable pay-as-you-go at any point by either deleting the billing policy or removing the environment from the billing policy. Doing so will stop any further charges on the Azure subscription. For more information, go to [Turning off pay-as-you-go](pay-as-you-go-set-up.md#turning-off-pay-as-you-go).

### What admin guardrails are available to prevent accidental costs?
You can leverage Azure Cost Management and alerting capabilities to manage spending within your organization. Go to [How to manage costs](pay-as-you-go-usage-costs.md#how-to-manage-costs) for more details.

### Can I use the Power Platform request or Dataverse capacity add-ons in a pay-as-you-go environment?
No, you can't use add-ons in a pay-as-you-go environment. Overages for both Dataverse and Power Platform requests will be charged via Azure subscription in a pay-as-you-go environment. 

### What storage model does the Dataverse capacity meter use?
All environments enabled for pay-as-you-go will use the [new Dataverse storage model](capacity-storage.md)  that has three separate categories of storage usage. If a tenant is still on the [legacy storage model](legacy-capacity-storage.md), the tenant’s storage model status will not change when an environment is enabled for pay-as-you-go.





[!INCLUDE[footer-include](../includes/footer-banner.md)]
