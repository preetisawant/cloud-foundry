---

copyright:
  years: 2015, 2017, 2018
lastupdated: "2018-02-26"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# What makes a good Cloud Foundry application?
{: #goodapp}

<!-- This file is reused in the CF Public subcollection. -->

A modern cloud application, and thusly a Cloud Foundry application, are about some key development facets: Cloud platforms, agile methodology, DevOps, microservices, and continuous delivery.

Due to these pieces, you really want to have a Platform-as-a-Service (PaaS) model. Although not absolutely required, a PaaS makes things a lot easier. Most cloud customers are using or start out with infrastructure-as-a-service (IaaS), which helps abstract their apps from the underlying hardware. But PaaS adds an extra layer to abstract the underlying OS, so you can focus entirely on the business logic of your app and not worry about repetative and consumable services that you could easily be engaging instead.

As part of this, there are two major concepts that come into play: "Cloud-native" applications and "12 Factor Apps".


## Cloud-Native
{: #cloudnative}

A "cloud-native" app has been defined by the Cloud Native Computing Foundation as

> “Cloud-native technologies empower organizations to build and run scalable applications in modern, dynamic environments such as public, private, and hybrid clouds. Containers, service meshes, microservices, immutable infrastructure, and declarative APIs exemplify this approach.

> These techniques enable loosely coupled systems that are resilient, manageable, and observable. Combined with robust automation, they allow engineers to make high-impact changes frequently and predictably, with minimal toil.”

So a "cloud native" application isn't just an "application". It's a set of processes and best practices that also go along with it. It's a transformation of development processes that is critical - the "development ecosystem" are learning at a fast pace the very best ways to deliver software, and that is an important part of the latest application creation process.

So let's overview the important points about cloud-native apps:

* Applications are highly connected with a variety of technologies and architectures, such as containers, container orchestration, microservices, and declarative APIs.
* Applications are built to run on modern infrastructures, typicaly "clouds". Those can be an external cloud vendor, or your own internal cloud environment.
* Building cloud-native apps is critically a practice and philosophy, not just a technology choice - it's about changing the way software is delivered in a DevOps and automation culture.
* They represent the dynamic and distributed nature of computing today, and needs for increased deployment speed, flexibility, agility, scalability, reliability, and security.


## 12 Factor App
{: #12factor}

As explained by the original concept creator, 

> "Twelve Factor apps are built for agility and rapid deployment, enabling continuous delivery and reducing the time and cost for new developers to join a project. At the same time, they are architected to exploit the principles of modern cloud platforms while permitting maximum portability between them. Finally, they can scale up without significant changes to tooling, architecture or development practices"

So that means that the the 12 factor apps check-list is really just a set of guidelines that dictate how an application should be built to properly support the concept of independently managed and iterated services. 

The [12 factors web site](https://12factor.net) describes the 12 factors as:

1. One codebase tracked in revision control, many deploys
2. Explicitly declare and isolate dependencies
3. Store config in the environment
4. Treat backing services as attached resources
5. Strictly separate build and run stages
6. Execute the app as one or more stateless processes
7. Export services via port binding
8. Scale out via the process model
9. Maximize robustness with fast startup and graceful shutdown
10. Keep development, staging and production as similar as possible
11. Treat logs as event streams
12. Run admin/management asks as one-off processes

These steps allow a maturing development organization to start adopting the range of cloud-native capabilties and create highly capable and flexible cloud applications.



