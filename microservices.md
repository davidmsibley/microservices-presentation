# Microservices

## Problems
* [Monolithic backend][Example: uPortal] that you don't completely control.
  * Sometimes that can be [social][Example: Dev List] and sometimes that can be [technical][Example: Pull Request].
  * Want to avoid [forking][Example: MyUW uPortal]:
    * Forks get out of date, and become [productivity sinks][Example: Contribute Back to Master].
* [Multi-tenant system][Example: MyUW Apps] applies stress to the [All-Or-Nothing][Example: Build Ear] architecture.
  * One bad (or inattentive) actor can ruin it for everyone.

## What are Microservices?
* ### tl;dr: [Wikipedia][Microservices on Wikipedia]
  Processes that communicate with each other over a network

  Goals:
  * Independently Deployable
  * Modular Structure
  * Enables Continuous Delivery
  * Scalable Architecture

* ### [Martin Fowler's Microservices][Martin Fowler's Microservices]
  * All content in this section is taken from martinfowler.com and paraphrased.
  * #### Monoliths versus Microservices

    ![Monoliths and Microservices]

    * Monoliths:
      * Small changes require entire project to be rebuilt and deployed
      * Code tends to quietly become more coupled over time
    * Microservices:
      * Small changes require only containing module to be rebuilt and deployed
      * Coupling is readily apparent, and deincentivized

  ### Characteristics of a Microservices Architecture
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

    > The Guardian website is a good example of an application that was designed and built as a monolith, but has been evolving in a microservice direction. The monolith still is the core of the website, but they prefer to add new features by building microservices that use the monolith's API.

## Goals of MyUW approach
* Move toward a [vanilla uPortal instance][Example: uPortal 5]
  * Componentization via Services
  * Evolutionary Design
* Mitigate risk of one tenant [breaking things for everyone][Example: Gatekeeping]
  * Organized around Business Capabilities
  * Infrastructure Automation
  * Design for Failure
* Easier to adopt [contributions][Example: Apereo Incubation]
  * Decentralized Governance

## Overview of Microservices by MyUW
### [Key Value Store][Key Value Store]
> A separate service to enable key value storage for MyUW applications

* ##### What it does:
  * It provides a user-scoped server-side storage location for valid JSON objects and arrays.

* ##### What we use it for:
  * [Features][Usage: KV Features]
  * [Notifications][Usage: KV Notifications]
  * [Announcements][Usage: KV Announcements]
  * [Widget User Preferences][Usage: KV Widget User Prefs]

---
### [Rest Proxy][Rest Proxy]
> A Simple server side REST proxy service written in Groovy

* ##### What it does:
  Cross-Domain calls are tricky and filled with potential security issues.
  This allows you to control the remote resources on the server side, while
  avoiding browser side security issues.
  This also passes through user details, allowing for personalized proxying.

* ##### What we use it for:
  * Wiscard
    * [Wiscard API Call][Usage: Proxy Wiscard]
    * [Wiscard Widget][Usage: Proxy Wiscard Example]
  * Directory
    * [Directory API Call][Usage: Proxy Directory Search]
    * [MyUW Search][Usage: Proxy Directory Example]

---
### [Personalized Redirection][Personalized Redirection]
> A service to provide a customized URL based on the identity of the user.

* ##### What it does:
  This will provide a personalized redirect url for a user specified in a CSV file on the classpath.

* ##### What we use it for:
  * [National Survey of Student Engagement][Usage: Redirect NSSE]

---
### [LTI Proxy][LTI Proxy]
> A configurable service to sign LTI parameters are return form data for your application

* ##### What it does:
  Configures a form post url for authenicating to a remote LTI service. The configured URL can be returned to the user, or the user can be redirected by the microservice.

* ##### What we use it for:
  * [Blackboard Ultra][Usage: LTI Blackboard Ultra]

---
### [RSS to JSON][RSS to JSON]
> Microservice for converting RSS feeds to JSON.

  [Documentation](https://uw-madison-doit.github.io/rssToJson/)

* ##### What it does:
  This takes an external xml RSS feed url, and returns the contents of that url formatted in JSON. Only works on valid RSS feeds.

* ##### What we use it for:
  * [RSS Feed Widget Type][Usage: RSS Feed Widget Type]

---
### [Widget Creator][Widget Creator]
> Web-based tool supporting developing widgets for uPortal-home.

* ##### What it does:
  This full uPortal app helps users mock out the look and functionality of uPortal-home widgets in the browser.

* ##### What we use it for:
  * [Creating Widgets!][Usage: Widget Creator]
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
  * [Insert Horror Story Here][Example: AQCU]

## Related
* #### [Docker][Docker]

* #### [Kubernetes][Kubernetes]
  > Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications.

* #### [Strangle Vine][Strangler Vine]?

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
[Docker]: https://www.docker.com/ (Docker)
[Kubernetes]: https://kubernetes.io/ (Kubernetes homepage)
[Strangler Vine]: https://www.martinfowler.com/bliki/StranglerApplication.html (Martin Fowler's StranglerApplication)

<!-- Images -->
[Monoliths and Microservices]: https://martinfowler.com/articles/microservices/images/sketch.png (Monoliths and Microservices)
[Conways Law In Action]: https://martinfowler.com/articles/microservices/images/conways-law.png (Conway's Law in Action)
[Functional Staff Organization]: https://martinfowler.com/articles/microservices/images/PreferFunctionalStaffOrganization.png (Service boundaries reinforced by team boundaries)
[Decentralized Data]: https://martinfowler.com/articles/microservices/images/decentralised-data.png (Decentralized Data Management)
[Basic Build Pipeline]: https://martinfowler.com/articles/microservices/images/basic-pipeline.png (Basic Build Pipeline)
[Micro Deployment]: https://martinfowler.com/articles/microservices/images/micro-deployment.png (Micro Deployment)

<!-- Examples -->
[Example: uPortal]: https://github.com/Jasig/uPortal (uPortal Github Page)
[Example: MyUW uPortal]: https://git.doit.wisc.edu/myuw/uPortal (MyUW uPortal GitLab Page)
[Example: Dev List]: https://groups.google.com/a/apereo.org/forum/#!forum/uportal-dev (uPortal Developers Email List)
[Example: Pull Request]: https://github.com/Jasig/uPortal/pull/883#issuecomment-301067785 (Default Behavior Breaking Pull Request)
[Example: Contribute Back to Master]: https://jira.doit.wisc.edu/jira/browse/MUMUP-2929 (Take something that works and put it over there)
[Example: MyUW Apps]: https://my.wisc.edu/web/apps (There's a lot of them)
[Example: Build Ear]: https://tools.my.wisc.edu/jenkins/job/docker-activate-test/lastFailedBuild/ (whoops.)
[Example: uPortal 5]: https://jasig.github.io/uPortal/ (uPortal Documentation)
[Example: Gatekeeping]: https://git.doit.wisc.edu/myuw-overlay/CampusCourseGuidePortlet/merge_requests/20 (But who watches the Watchmen?)
[Example: Apereo Incubation]: https://www.apereo.org/incubation (The Warm and Fuzzies)
[Example: AQCU]: # (AQCU)

<!-- Usages -->
[Usage: KV Features]: https://github.com/UW-Madison-DoIT/uw-frame/tree/master/uw-frame-components/portal/features (Features Module Github)
[Usage: KV Notifications]: https://my.wisc.edu/web/notifications (MyUW Notifications)
[Usage: KV Announcements]: https://github.com/UW-Madison-DoIT/uw-frame/blob/master/uw-frame-components/portal/features/services.js#L83 (Announcements Usage Source Code)
[Usage: KV Widget User Prefs]: https://github.com/UW-Madison-DoIT/uw-frame/blob/master/uw-frame-components/portal/widgets/controllers.js#L408 (Weather Widget User Preferences)
[Usage: Proxy Wiscard]: https://my.wisc.edu/web/api/proxy/wiscard (Wiscard API Call)
[Usage: Proxy Wiscard Example]: https://my.wisc.edu/web/apps/details/wiscard-balance (Wiscard Widget)
[Usage: Proxy Directory Search]: https://my.wisc.edu/web/api/proxy/wiscdirectory/?name=sibley (Oh hey, that's me!)
[Usage: Proxy Directory Example]: https://my.wisc.edu/web/apps/search/sibley (I've never met those other people)
[Usage: Redirect NSSE]: https://my.wisc.edu/web/apps/details/nsse (Personalized Link Survey Widget)
[Usage: LTI Blackboard Ultra]: https://test.my.wisc.edu/web/apps/details/blackboard-ultra-launcher (Blackboard Launcher Widget)
[Usage: RSS Feed Widget Type]: https://my.wisc.edu/web/apps/details/doit-scheduled-outages (DoIT Scheduled Outages)
[Usage: Widget Creator]: https://test.my.wisc.edu/widget-creator/ (MyUW Widget Creator)
