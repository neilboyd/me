# [NDC Sydney](http://ndcsydney.com/) 1-5 August 2016

NDC started at a small developer conference in Norway in 2008, extended to London in 2013,
and I attended the first one in Sydney in 2016.
It has kept to it's roots as a small and friendly conference

I attended a two-day workshop before the conference, the three days of the conference,
and the tiny informal PubConf on the last evening. 

The recurring themes of the conference were:

- microservices
- serverless architecture
- .Net Core

The technical level of the talks and the audience was fairly high.
This is better than other conferences I've been to which have been at more of a beginner's level.


## [Workshop: Design and Implementation of Microservices](http://ndcsydney.com/workshop/design-and-implementation-of-microservices/)

This workshop was given by Sam Newman, the author of the authoratative book
[Building Microservices](http://samnewman.io/books/building_microservices/).
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
  - orchestration: tell other processes what to do and monitor status - disadvantage is that services become dumb and orhcestrator becomes god
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
- have a separate database for reporting
  - keep in sync with events - do a full sync every now and then in case any errors occured
  - need to consider data freshness
  - to prevent problems with broken relationships, never allow deleting, or never allow updating
- testing:
  - should only have a few end-to-end tests for main flows (happy path)
  - modify end-to-end tests when adding a new feature, rather than adding new tests
  - if a test fails, write a unit test for the failre so that you catch it faster next time
- service discovery by convention (eg DNS) or configuration (use a service discovery tool)

Conclusion: services should be logically separated and independant.


## [Node.js Crash Course](http://ndcsydney.com/talk/node-js-crash-course-for-net-developers/)

- JavaScript on the server
- Not just back end - automation, CLI, desktop apps (Electron)
- Simple, good performance, not much built into nodejs itself - everything is in npm
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














## Talks


Move talks details to a separate document and just keep highlights here


## [PubConf](http://pubconf.io/)

The conference ended with a series of light-hearted lightning talks in a pub.
The idea for PubConf came out of the philosophy "always do when you're sober what you say when you're drunk".
The format is 20 slides in 5 minutes.
There's one code of conduct rule: what happens in PubConf stays in PubConf.
That means no photos and no quotes.

The star of the conference, and of PubConf, was Troy Hunt.
He was the subject of many of the jokes,
and he gave a nice talk on the lighter side of security.

PubConf ended with music from Dylan Beattie who said
"two good things came out of Australia 40 years ago - Troy Hunt and AC/DC"
before playing a version of "[Have I been pwned?](https://haveibeenpwned.com/)"
to the tune of "Highway from Hell".
He also played his hilarious hit "[We're Gonna Build a Framework](http://www.dylanbeattie.net/2016/05/were-gonna-build-framework.html)".



## Notes to include somewhere in text

- Different range of tech - not just .Net
- Lots of talk about functional programming, but attendees didn't seem so impressed that they would actually use it
- Lots of talk about .Net Core, but still very much a 1.0 release
- Mention slow internet and Pokemon Go (perhaps I can mention this in keynote talk)
- Not much talk about security in microservices, although it was mentioned, which is why the talk was disappointing

Microservice seems to be more of a concept and a buzzword than an actual thing

[Videos](https://vimeo.com/ndcconferences)
