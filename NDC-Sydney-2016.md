# [NDC Sydney](http://ndcsydney.com/) 1-5 August 2016

NDC started as a small developer conference in Norway in 2008, extended to London in 2013,
and I attended the first one in Sydney in 2016.
It has kept to its roots as a small and friendly conference.

I attended a two-day workshop before the conference, the three days of the conference,
and the tiny informal [PubConf](#pubconf) on the last evening. 

The technical level of the talks and the audience was fairly high.
This is better than other conferences I've been to which have been at more of a beginner's level.

The recurring themes of the conference were:

- microservices
- serverless architecture
- functional programming
- .Net Core

Watch this space for the [videos](https://vimeo.com/channels/1120652) to become available.


## [Workshop: Design and Implementation of Microservices](http://ndcsydney.com/workshop/design-and-implementation-of-microservices/)

This workshop was given by Sam Newman, the author of the authoratative book
"[Building Microservices](http://samnewman.io/books/building_microservices/)".
It was about the theory and best practices of Microservices, not about any specific implementations.
The slides for the workshop are available [here](http://bit.ly/ms-workshop).

My main takeaways are:

- microservices should be
  - independantly deployable and scalable
  - named after the business capabilities they expose
- organization of architecture mimics organization of company (Conway's law)
- teams can have ownership of services when code organization reflects company organization
- deploy small changes often - this doesn't reduce the risk, but it makes it easier to know what broke
- separate security for each part of the app limits the scope for attack
- hard to say how big a microservice should be:
  - smaller means more of them (harder to manage)
  - larger means more complex
  - start larger and and split up afterwards
- service boundary should be split on responsibilities, not data
- it's a bad idea to make services share a database (can't change the schema, can only add to it)
- better to duplicate code than use a shared library, but that's a bad idea when all copies need to change in sync
- sometimes a shared library can be made into a service
- building on REST can have some advantages such as caching, but this relies on correct implementation, eg only caching 200 responses, and not returning errors with 200 (like SOAP does)
- building on REST tends to leave some things unknown, such as when there's an error, where's the message
- orchestration vs choreography:
  - orchestration: tell other processes what to do and monitor status - disadvantage is that services become dumb and orchestrator becomes god
  - choreography: services run by themselves, eg listening on a queue - disadvantage is how to know when something failed
- moving to a microservice architecture:
  - do it slowly because it takes time to learn how to manage the services
  - start by extracting modules with few dependencies (stateless)
  - start on something that will change soon (not much point refactoring something that hasn't changed for 5 years and isn't likely to change for the next 5 years)
  - can start by organizing code into namespaces - easy and safe
  - give each module it's own database connnection (separate transactions)
    - see if there are problems with integrity or performance
    - may actually be faster because database isn't doing referential integrity
    - need to handle transactional integrity ourselves
    - surfaces new failure modes - maybe it was already a problem but we didn't know about it
- have a separate database for reporting:
  - keep in sync with events - do a full sync every now and then in case any errors occured
  - need to consider data freshness
  - to prevent problems with broken relationships, never allow deleting, or never allow updating
- testing:
  - should only have a few end-to-end tests for main flows (happy path)
  - modify end-to-end tests when adding a new feature, rather than adding new tests
  - if a test fails, write a unit test for the failre so that you catch it faster next time
- service discovery by convention (eg DNS) or configuration (use a service discovery tool)

Conclusion: services should be logically separated and independant.


## [Node.js crash course](http://ndcsydney.com/talk/node-js-crash-course-for-net-developers/)

- JavaScript on the server
- Not just back end - automation, CLI, desktop apps (Electron)
- Simple, good performance
- Not much built into nodejs itself - everything is in npm
- Single threaded event loop - handles concurrency very well

## [Node.js microservices in the cloud for (almost) free](http://ndcsydney.com/talk/undo-accept-awesome-node-js-microservices-in-the-cloud-for-almost-free/)

This was the first talk I went to on cloud functions, but it set the scene for several of the following talks.
He was the first of many to use the buzzword *serverless* that kept recurring throughout the conference.
It means that you only need to think about the code and not the servers -
it scales automatically, no need to worry about failover, no need to have backup machines etc.

There are three main cloud function providers which are basically interchangeable, in order of popularity:
- [AWS lambda](https://aws.amazon.com/lambda/)
- [Azure functions](https://azure.microsoft.com/en-us/services/functions/)
- [Google functions](https://cloud.google.com/functions/)

The premise of the talk was that AWS is free for the first million requests,
and then $2 per million after that.
He used AWS and Node.js for his example, but the principal is the same for any other technology choice.

Functions can be triggered by anything -
eg file saved, message queue, record added to database, schedule, web request, or some complex condition -
which means you don't need to write the code that triggers the function.

VMs are incentivized to keep the machine busy,
whereas functions are incentivized to write small, isolated, loosely coupled modules -
which is exactly the definition of a microservice.

## [Akka.Net and the Actor Model](http://ndcsydney.com/talk/workshop-introduction-to-akka-net-and-the-actor-model/)

- [Akka.Net](http://getakka.net/) is an implementation of the actor model
- all communication is via immutable messages
- sender and recipient are decoupled and async
- actors process one message at a time
- actor state is thread safe
- at-most-once message delivery
  - ie. it could be lost
  - cf. at-least-once (could get duplicate) and exactly-once

I got the impression that Akka.Net is a low level design of microservices.
It doesn't describe the deployment scenario.
For a more managed implementation you could use [Azure Service Fabric](https://azure.microsoft.com/en-us/services/service-fabric/).

## [NBench: Automated Performance Testing for .NET](http://ndcsydney.com/talk/nbench-automated-performance-testing-for-net/)

- performance is a feature
- create a culture of measuring performance
- it tends to improve over time once you start measuring it
- NBench tests are like unit tests
- failed assertion can fail CI build
- two run modes: number of runs in a fixed time, or run a certain number of times

## [Start taking advantage of functional programming](http://ndcsydney.com/talk/functional-programming-for-the-everyman/)

How to gradually start using functional programming features in the languages you already use.

C# Linq names functions using SQL terms rather than normal FP terms, eg select instead of map, but the concepts are the same.

In JavaScript use [lodash](https://lodash.com/) to get similar functional constructs:
```JavaScript
var _ = require('lodash')
_.first(...).skip()....etc
```

The slides and examples are available [here](http://bit.ly/fp-for-everyman).

## [Azure Machine Learning for the Developer](http://ndcsydney.com/talk/azure-machine-learning-for-the-developer/)

Machine learning was previously the domain of data scientists,
but these are in short supply and very expensive,
so [Azure Machine Learning](https://azure.microsoft.com/en-us/services/machine-learning/)
makes it accessible for developers. 

- learn from data rather than following instruction
- consider collecting *good* data in advance so that it makes it possible to do ML later
- don't provide defaults, eg first item in dropdown (Afghan accountants)

Steps:
- define objective
- collect data
- prepare data
- train models
- evaluate models
- publish
- manage

Use drag'n'drop to design experiments.
There are lots of modules to choose from, eg select columns, clean missing values, etc.
It's an experiment! If in doubt, just try something, then try something else.

Once you have a trained model, deploy it as a web service to use for prediction.

**If prediction accuracy is better than random then it's worthwhile**,
eg when predicting one of four categories, better than 25% accuracy is good.

## [Functional Architecture](http://ndcsydney.com/talk/functional-architecture-the-pits-of-success/)

Very good talk about coding best practices that need to be enforced in object-oriented programming
but come naturally in functional programming.

FP defines a *pure function* as a function that has the same output for the same input, and no side effects.
You can't call an impure function from a pure function
(in Haskell it won't even compile),
which means that functions that perform I/O (impure) will be on the outside
and business logic will be in the center.
Pure functions can be easily tested.
A function can take another function as input, eg getting a value from a database -
so the function is testable without having to, for example, mock a repository.

## [Power BI for the Developer](http://ndcsydney.com/talk/power-bi-for-the-developer/)

[Power BI](https://powerbi.microsoft.com/en-us/blog/power-bi-azure-ml/)
makes a nice dashboard with nice data visualizations out of any data sets.

- updated in real time
- many pre-defined sources
- API to push data from any data source
- stream analytics - eg take in a stream of data and report on average temperature from last 5 minutes
- can publish dashboard publicly to web

## [.Net Core](http://ndcsydney.com/talk/what-does-an-open-source-microsoft-web-platform-look-like/)

The aim of
[.Net Core](https://www.microsoft.com/net/core)
is to make .Net as easy to run as JavaScript etc:
```
dotnet init
dotnet new
dotnet restore
```

PCL seemed like a good idea at the time, but it's the lowest common denominator.

.Net Core is not a replacement for .Net 4.6 etc.
Things like **W**PF, **Win**Forms, etc will never be in Core.

.Net Core got a bad press because of the re-organizations leading up to the 1.0 release,
but that was due to re-organizations within Microsoft.

## [Practical microservice security](http://ndcsydney.com/talk/practical-microservice-security/)

The talk included "microservice" in the title but I think that was just to be buzzword-friendly.
It was about security in general.

- Security is about Confidentiality, Integrity, Availability (CIA!)
- Microsoft defines the [STRIDE](https://msdn.microsoft.com/en-us/library/ee823878(v=cs.20).aspx) threat model,
comparable to [OWASP](https://www.owasp.org/)
- Auth vs auth - why acronyms make you insecure
- Do input validation between components
- Security problem: make lots of services and then forget about them
- Log everything:
  - store securely, away from production
  - immutable (don't let hackers delete logs)
  - look at the logs

Good resources:
- [NIST](http://www.nist.gov/) - security standards and list of company's security record
- [VSAQ](https://github.com/google/vsaq) - security questionnaire to send to vendors to assess third parties


## [PubConf](https://pubconf.io/)

The conference ended with a series of light-hearted lightning talks in a pub.
The idea for PubConf came out of the philosophy "always do when you're sober what you say when you're drunk".
The format is 20 slides in 5 minutes.
There's one code of conduct rule: what happens in PubConf stays in PubConf.
That means no photos and no quotes.

The star of NDC, and of PubConf, was Troy Hunt.
He was the subject of many of the jokes, and he gave a nice talk on the lighter side of security.

PubConf ended with music from Dylan Beattie who said
"two good things came out of Australia 40 years ago - Troy Hunt and AC/DC"
before playing a version of "[Have I been pwned?](https://haveibeenpwned.com/)"
to the tune of "Highway from Hell".
He also played his hilarious hit "[We're Gonna Build a Framework](http://www.dylanbeattie.net/2016/05/were-gonna-build-framework.html)".

