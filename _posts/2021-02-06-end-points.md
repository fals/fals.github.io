---
layout: post
title: Designing APIs using Endpoints
subtitle: Creating simple and maintainable services designed around Endpoints as Components
bigimg: /img/jenga.jpg
share-img: /img/jenga.jpg
tags: [architecture, REST, dotnet, API, endpoints]
---

## 📚 That's how we used to do it

When designing services a common practice in the industry is creating a granular set of APIs at the same place, having in single file or class the whole specification of routes and methods aggregated by a reason, usually by domain capability. 

This design was historically driven by how frameworks were developed to provide such capability to web service applications, for example, ASP.NET and Spring, in which the **Controller** is the base for any API.

The **Controller** is used for multiple purpose REST methods, it gets too large overtime, it aggregates more responsibility than it should. The same piece of code that changes an entity also exposes data from that entity. API methods are located far away from contracts they use, the maintainability is low.

![Designing Around Single Controller Class](/img/end-points-single-controller.png)

## 📦 Endpoints and Component Base Design

The idea of organizing your API using endpoints got forgotten and lost with the deprecation of [SOA]([https://link](https://en.wikipedia.org/wiki/Service-oriented_architecture)), but in the end it is basically the utilization of the design patters below:

* SoC - Separation of Concerns, an endpoint is the extension of the Use Case, it exposes a specific capability, requires certain contracts, the contracts should follow the endpoint, all together represents small module in that service.

* SRP - Single-responsibility principle, the endpoint and its contracts they change for a single reason, because the Use Case which it exposes the capability changed, the contracts change because the end-point changed and vice versa.

![Designing Around Multiple Endpoints](/img/end-points-multiples.png)

At first glance you might notice that your code is going to get better, the maintainability and evolvability won't fade overtime because of the way the code fits together, your service will age well and healthy. 

## 🌏 What about Service Discovery?

If you are familiar with [Swagger]([https://link](https://swagger.io/)), a widespread tool to document and design APIs, you know that it is easy to aggregate a set of endpoints based on the HTTP Method, route and others.

Having your API with multiple endpoints classes doesn't affect discoverability, you can use the tool to do as you please.

## 👉 Conclusion

Designing your code around Endpoints is the way to go for maintainability and evolvability of services exposing APIs. Give it a try, you won't regret.

The source code is hosted on GitHub: [cqrs-clean-eventual-consistency](https://github.com/fals/cqrs-clean-eventual-consistency)

## 📖 Reference 

* <a href="https://en.wikipedia.org/wiki/Component-based_software_engineering" target="_blank">Component-based software engineering</a>

* <a href="https://en.wikipedia.org/wiki/Separation_of_concerns" target="_blank">Separation of concerns
</a>
