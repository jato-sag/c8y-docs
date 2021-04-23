---
weight: 40
title: Microservice runtime and applications
layout: redirect
---
Custom EPL apps (individual \*.mon files), Apama Analytics Builder models and smart rules are executed in an Apama-ctrl microservice. This has a per-tenant isolation scope, that is, each subscribed tenant has its own instance of an Apama container with dedicated resources (that is, memory and CPU usage). The container is isolated from other tenants, hence high CPU load or memory issues on other containers are tracked and resourced independently.

You can use predefined rules (see [Smart rules](/users-guide/cockpit/#smart-rules)), define your own custom rules with Apama EPL Apps, or use Apama Analytics Builder to build analytic models. This requires the following microservices and/or applications:

| To do this                  | you need the following                                       |
| --------------------------- | ------------------------------------------------------------ |
| Use predefined rules        | Apama-ctrl microservice and Smartrule microservice (included in Cumulocity IoT's Standard Tenant). |
| Define custom rules         | Apama-ctrl microservice and Apama EPL Apps web application.  |
| Use Apama Analytics Builder | Apama-ctrl microservice and Apama Analytics Builder web application. |

See also the tables listing the available applications under [Managing applications](/users-guide/administration/#managing-applications) in the *User guide*.

If your tenant is subscribed to the Apama Starter microservice (instead of other Apama-ctrl microservices), then the following applies for Apama:

- Unlimited number of smart rules.
- Apama Analytics Builder is limited to at most 3 active models. Custom blocks written with the Apama Analytics Builder Block SDK cannot be used.
- Apama EPL Apps is not available in the application switcher.

Contact [product support](/about-doc/contacting-support) to discuss adding more capabilities.

> **Info:** If your tenant is subscribed to the Apama Smart Rules-only microservice (also called Apama-ctrl-smartrules), Apama EPL Apps and Apama Analytics Builder are not available.