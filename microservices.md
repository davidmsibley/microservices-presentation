# Microservices

## Problems
* Monolithic backend that you don't completely control.
  * Sometimes that can be social and sometimes that can be technical.
* Multi-tenant system applies stress to the All-Or-Nothing approach.
  * One bad (or inattentive) actor can ruin it for everyone.

## Goals of MyUW approach
* Need to patch functionality without forking the backend.
* Need to add server side functionality that isn't applicable to all users of backend.

Our microservices approach has typically been to add functionality that allows us
to use the backend uPortal in different ways than traditional uPortal users.

## Microservice Principles
* [Martin Fowler's Microservices]
* [Microservices on Wikipedia]

## Overview of Microservices by MyUW
### [Key Value Store]
##### What it does:
##### What we use it for:

### [Rest Proxy]
##### What it does:
##### What we use it for:

### [Personalized Redirector]
##### What it does:
##### What we use it for:

### [LTI Proxy]
##### What it does:
##### What we use it for:

### [RSS to JSON]
##### What it does:
##### What we use it for:

### [Widget Creator]
##### What it does:
##### What we use it for:

## Demo

## MyUW problems solved with Microservices
* Move toward a vanilla uPortal instance
* Mitigate risk of one tenant breaking things for everyone
* Easier to adopt contributions

## Issues to keep in mind when using Microservices
* Versions and Regressions
  * Don't get attached to an implementation
* Microservices for the sake of Microservices
  * Keep in mind the problem you're trying to solve.

## Future steps


<!-- MyUW Github Repositories -->
[Rest Proxy]: https://github.com/UW-Madison-DoIT/rest-proxy "Rest Proxy Github Repository"
[Key Value Store]: https://github.com/UW-Madison-DoIT/KeyValueStore "Key Value Store Github Repository"
[LTI Proxy]: https://github.com/UW-Madison-DoIT/lti-proxy "LTI Proxy Github Repository"
[Personalized Redirector]:  https://github.com/UW-Madison-DoIT/personalizedRedirection "Personalized Redirector Github Repository"
[RSS to JSON]: https://github.com/UW-Madison-DoIT/rssToJson "RSS to JSON Github Repository"
[Widget Creator]: https://github.com/UW-Madison-DoIT/widget-creator "Widget Creator Github Repository"

<!-- External Links -->
[Martin Fowler's Microservices]: https://martinfowler.com/articles/microservices.html "Martin Fowler's Microservices"
[Microservices on Wikipedia]: https://en.wikipedia.org/wiki/Microservices "Wikipedia: Microservices"
