Catalyst is envisioned as a platform that will serve as the core engine for any application to be built on top of it. Over time we'll add support for more themes and business domains.

# Key High-Level Objectives

- Have the system granular enough to support frequent releases eliminating the need for separate long-lived release and staging branches
- Have extensive logging to get, analyze, simulate, and restore the history of events as closely as possible.
- Have modular/in-place replaceable UI components to allow users to customize their apps as per their needs and preferences.
- Have a multifaceted caching service on the UI layer to increase performance and reduce cost & latency by making fewer API calls.
- Have extensively componentized UI to support the capability to sell UI as component libraries and prepare a no-code dev tool.
- Have extensive automated testing to support frequent releases without the fear of breaking anything.
- Have granular feature toggles to turn off a feature should things start to break without redeployment and support the gradual rollout and A/B testing.

# Tech Stack

Backend:  ASP.NET Core Minimal APIs, .NET 7, C# 11

Frontend: ASP.NET Core Blazor, MAUI, .NET 7, C# 11, Bootstrap

Azure services: App Service, Functions, Cosmos DB, Service Bus, Table Storage, Blob Storage

Testing: xUnit (For unit/integration testing), bUnit (for Blazor components), Playwright (For e2e testing)

Architecture patterns: CQRS, MVVM, Reactive Programming, Component Driven Development

# Environments

## Staging

API - [https://catalyst-api-staging.azurewebsites.net/](https://catalyst-api-staging.azurewebsites.net/)

UI - [https://catalyst-ui-staging.azurewebsites.net/](https://catalyst-ui-staging.azurewebsites.net/)

Credentials

|Email|Password|Role|
|---|---|---|
|[catalystsupportadmin@arinsyscorp.com](mailto:catalystsupportadmin@arinsyscorp.com)|Staging@123|Support Admin|