# Microservices

## Problems
* [Monolithic backend][Example: uPortal] that you don't completely control.
  * Sometimes that can be [social][Example: Dev List] and sometimes that can be [technical][Example: Pull Request].
  * Want to avoid forking:
    * Forks get out of date, and become [productivity sinks][Example: Contribute Back to Master].
* [Multi-tenant system][Example: MyUW Apps] applies stress to the [All-Or-Nothing][Example: Build Ear] architecture.
  * One bad (or [inattentive][Example: Missing Tag]) actor can ruin it for everyone.

## What are Microservices?
* ### tl;dr: [Wikipedia][Microservices on Wikipedia]
  Processes that communicate with each other over a network

  Goals:
  * Independently Deployable
  * Modular Structure
  * Enables Continuous Delivery
  * Scalable Architecture

* ### [Martin Fowler's Microservices][Martin Fowler's Microservices]
  * All content in this section ripped from martinfowler.com and paraphrased.
  * #### Monoliths versus Microservices

    ![Monoliths and Microservices]

    * Monoliths:
      * Small changes require entire project to be rebuilt and deployed
      * Code tends to quietly become more coupled over time
    * Microservices:
      * Small changes require only containing module to be rebuilt and deployed
      * Coupling is readily apparent, and deincentivized

  * #### Componentization via Services
    * not via Libraries

  * #### Organized around Business Capabilities
    * not around Technology Layers

      ![Conways Law in Action]

    * instead:

      ![Functional Staff Organization]

  * #### Products not Projects
    * Amazon's "You build it, you run it"
    * Instead of bringing a product to "completion" and handing it off to a maintenance team
    * Shrink the feedback use between developers and users

  * #### Smart Endpoints and Dumb pipes
    * Separate the Business Logic from the Message Routing
    * Using a decoupled module for Choreography or Orchestration

  * #### Decentralized Governance
    * Favor internal open source model over formal guidance
    * Developers focus on making tools that others can use to solve similar
      problems.
    * Build out the service only to the point where it satisfies the contract

  * #### Decentralized Data Management
    * Let each Microservice manage its own data.

      ![Decentralized Data]

    * Make the separation of concerns explicit at the service level, not the database level.

  * #### Infrastructure Automation
    * Continuous Integration focuses on automating the acceptance of code being merged into the code base
    * Continuous Delivery focuses on automating the Migration of code to the production environment.
      * "Make Deployment Boring"

      ![Basic Build Pipeline]

    * Separating microservices out and formalizing their API contract allows us
      to write targeted "Unitized" Integration tests.

      ![Micro Deployment]

  * #### Design for Failure
    * By separating out components across a network, we're adding more area for things to fail
    * It's essential for development teams to constantly reflect on how service failures affect the user experience

  * #### Evolutionary Design
    * Design to maximize independent replacement and upgradeability
    * Expect services to be scrapped or replaced rather than evolved

  > The Guardian website is a good example of an application that was designed
  > and built as a monolith, but has been evolving in a microservice direction.
  > The monolith still is the core of the website, but they prefer to add new
  > features by building microservices that use the monolith's API.

## Goals of MyUW approach
* Move toward a [vanilla uPortal instance][Example: uPortal 5]
  * Componentization via Services
* Mitigate risk of one tenant [breaking things for everyone][Example: Gatekeeping]
  * Infrastructure Automation
* Easier to adopt [contributions][Example: Apereo Incubation]
  * Decentralized Governance

## Overview of Microservices by MyUW
* ### [Key Value Store][Key Value Store]
  * ##### What it does:
    > A separate service to enable key value storage for MyUW applications

  * ##### What we use it for:
    * [Find Usages][TODO]

---
* ### [Rest Proxy][Rest Proxy]
  * ##### What it does:
    > A Simple server side REST proxy service written in Groovy

    Cross-Domain calls are tricky and filled with potential security issues.
    This allows you to control the remote resources on the server side, while
    avoiding browser side security issues.

  * ##### What we use it for:
    * [Find Usages][TODO]

---
* ### [Personalized Redirection][Personalized Redirection]
  * ##### What it does:
    > A service to provide a customized URL based on the identity of the user.

  * ##### What we use it for:
    * [Find Usages][TODO]

---
* ### [LTI Proxy][LTI Proxy]
  * ##### What it does:
    > A configurable service to sign LTI parameters are return form data for your application

  * ##### What we use it for:
    * [Find Usages][TODO]

---
* ### [RSS to JSON][RSS to JSON]
  [Documentation](https://uw-madison-doit.github.io/rssToJson/)
  * ##### What it does:
    > Microservice for converting RSS feeds to JSON.

  * ##### What we use it for:
    * [Find Usages][TODO]

---
* ### [Widget Creator][Widget Creator]
  * ##### What it does:
    > Web-based tool supporting developing widgets for uPortal-home.

  * ##### What we use it for:
    * [Find Usages][TODO]
---

## Issues to keep in mind when using Microservices
* #### Versions and Regressions
  * You lose ability to easily know who depends on the microservice
  * Backwards compatibility is key
  * Don't get attached to an implementation
    * often it's better to write a whole new microservice than to change the API
      of an existing microservice.
* #### How many Microservices does it take to screw in a light bulb?
  * Clean layers of abstraction are essential
  * Shouldn't need to pull down 12 microservices to work on one thing.
* #### Microservices for the sake of Microservices
  * Keep in mind the problem you're trying to solve.
  * [Insert Horror Story Here][TODO]

## Future steps
* [Docker][TODO] and [Kubernetes][TODO]
* [Strangle vine][TODO]?

## Discussion
* How do you see microservices evolving the way you work with uPortal?

<!-- MyUW Github Repositories -->
[Rest Proxy]: https://github.com/UW-Madison-DoIT/rest-proxy (Rest Proxy Github Repository)
[Key Value Store]: https://github.com/UW-Madison-DoIT/KeyValueStore (Key Value Store Github Repository)
[LTI Proxy]: https://github.com/UW-Madison-DoIT/lti-proxy (LTI Proxy Github Repository)
[Personalized Redirection]:  https://github.com/UW-Madison-DoIT/personalizedRedirection (Personalized Redirection Github Repository)
[RSS to JSON]: https://github.com/UW-Madison-DoIT/rssToJson (RSS to JSON Github Repository)
[Widget Creator]: https://github.com/UW-Madison-DoIT/widget-creator (Widget Creator Github Repository)

<!-- External Links -->
[Martin Fowler's Microservices]: https://martinfowler.com/articles/microservices.html (Martin Fowler's Microservices)
[Microservices on Wikipedia]: https://en.wikipedia.org/wiki/Microservices (Wikipedia: Microservices)

<!-- Images -->
[Monoliths and Microservices]: https://martinfowler.com/articles/microservices/images/sketch.png (Monoliths and Microservices)
[Conways Law In Action]: https://martinfowler.com/articles/microservices/images/conways-law.png (Conway's Law in Action)
[Functional Staff Organization]: https://martinfowler.com/articles/microservices/images/PreferFunctionalStaffOrganization.png (Service boundaries reinforced by team boundaries)
[Decentralized Data]: https://martinfowler.com/articles/microservices/images/decentralised-data.png (Decentralized Data Management)
[Basic Build Pipeline]: https://martinfowler.com/articles/microservices/images/basic-pipeline.png (Basic Build Pipeline)
[Micro Deployment]: https://martinfowler.com/articles/microservices/images/micro-deployment.png (Micro Deployment)

<!-- Examples -->
[Example: uPortal]: # ()
[Example: Dev List]: # ()
[Example: Pull Request]: # ()
[Example: Contribute Back to Master]: # ()
[Example: MyUW Apps]: # ()
[Example: Build Ear]: # ()
[Example: Missing Tag]: # ()
[Example: uPortal 5]: # ()
[Example: Gatekeeping]: # ()
[Example: Apereo Incubation]: # ()


<!-- TODO Marker -->
[TODO]: # (Elaborate on this!)
