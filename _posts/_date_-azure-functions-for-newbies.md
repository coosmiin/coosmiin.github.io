---
title: "Azure Functions for newbies"
date: _date_ +0200
categories: azurefunctions routing keyvault applicationinsights
---

Last update on: _date_

Intro

## Checking environment at runtime

There are several options:

1. Using `AZURE_FUNCTIONS_ENVIRONMENT`

As specified in this [issue](https://github.com/Azure/azure-functions-host/issues/4491), the `AZURE_FUNCTIONS_ENVIRONMENT` is used internally by the Functions host builder. To check if your function is running locally (in developoment) you can simply do this:
```csharp
bool isDevelopment = Environment.GetEnvironmentVariable("AZURE_FUNCTIONS_ENVIRONMENT") == "Development";
```

2. Using `APPSETTING_WEBSITE_SLOT_NAME` or `WEBSITE_SLOT_NAME`

If you check your function app settings on production (for example by using the Advanced tool (Kudu) from the Platform Features settings) you'll see that the two mentioned environment variables are set to `Production`.

AppInsights

KeyVault