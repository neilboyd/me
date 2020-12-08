# .NET Conf 2020

[.NET Conf 2020](https://channel9.msdn.com/Events/dotnetConf/2020)
is an online conference, mostly about all the good new stuff in .Net 5.

There are lots of good presentations,
but I don't have time to watch them all.
These are the ones that appealed to me most.

## [KeyNote](https://channel9.msdn.com/Events/dotnetConf/2020/Keynote-Welcome-to-NET-5)

- Better Git integration in Visual Studio
- GitHub Actions in Visual Studio
- Blazor looks better and faster and debugging
- Great Swagger (Open API) support
- Project Tye to make K8s easier

## [What’s New in C#?](https://channel9.msdn.com/Events/dotnetConf/2020/Whats-New-in-C)

- top level program
- `init` setter
  - serializer still breaks "read-only-ness", ie can set `init` properties
- `record`
  - class with value but no methods
  - nice `ToString` implementation
  - value equality
  - define properties in constructor
  - can be deconstruced (tuples)
  - probably immutable
- `with` expression - create (shallow) copy and have an extra object initialiser
- better pattern matching in switch statements

## [Porting Projects to .NET 5](https://channel9.msdn.com/Events/dotnetConf/2020/Porting-Projects-to-NET-5)

- .Net 5 is not LTS - 6 will be
- Xamarin not in 5 - will be in 6
- everything they intend to bring from FF is now in .Net 5
  - AddDomains will not be ported, but can use AssemblyLoadContext instead
- .Net 5 replaces Core and Standard
  - also have platform specific versions that add stuff
  - cross platform libraries to support FF are still Standard 2.0
  - Standard 2.1 to share with Core 3.0 and Xamarin
- only reason to port is to innovate - Core 3.1 and FF will stay around for ever
- nice tools to migrate - `ApiPort` and `try-convert`

## [Developer Fun with Scott Hanselman](https://channel9.msdn.com/Events/dotnetConf/2020/Developer-Fun-with-Scott-Hanselman)

- I watched the first few minutes and it's just some fun - nothing new.

## [Accelerate .NET to Azure with GitHub Actions](https://channel9.msdn.com/Events/dotnetConf/2020/Accelerate-NET-to-Azure-with-GitHub-Actions)

- mostly just an intro with slides
- Actions is still behind Azure DevOps so no urgent need to move

## [Setting Up Feature Flags with .NET](https://channel9.msdn.com/Events/dotnetConf/2020/S236)

- using [Split](https://split.io/product/feature-flags/), not the .Net Core feature
- kill switch
- A/B testing
- subscription management
- canary release
- different differentiators: user, device, location, etc
- approval
- demo wasn't very good, but maybe she just wasn't a good presenter
- the product supports good best practises
- start simple, eg an A/A test (yes really!)

## [Azure Management Superpowers with Pulumi](https://channel9.msdn.com/Events/dotnetConf/2020/Azure-Management-Superpowers-with-Pulumi)

- [Pulumi](https://www.pulumi.com/azure/) has full coverage of Azure and Kubernetes APIs, and .Net 5 and C# 9
- multiple cloud providers
- infrastructure as code
  - ARM templates
  - yaml
  - actual code
- Pulumi is the last in that list
  - has IDE support etc, and can also write unit tests etc
- 100% Azure coverage - it's generated from the OpenApi spec
- can convert an ARM template to code

### [Developing and Deploying Microservices with 'Tye'](https://channel9.msdn.com/Events/dotnetConf/2020/Developing-and-Deploying-Microservices-with-Tye)

- it's supposed to simplify Kubernetes
- but if you don't find Kubernetes too hard, then Tye is probably not useful for you
- it's still an experiment
  - useful for development cycle
  - most people don't get as far as using it for deployment
- the second half of the video was a demo, but they'd already lost me

### [What’s New in Visual Studio 2019 and beyond](https://channel9.msdn.com/Events/dotnetConf/2020/Whats-New-in-Visual-Studio-2019-and-beyond)

- themes - download a theme extension and select it - it'll do colors, etc
- checkbox to open solution without loading projects
- configure file nesting options, eg show different file types as if they were in different folders
- intellicode suggestion - suggest what to do next when it sees you're repeating edits, and suggest to do it in other locations
- demo didn't go well - VS kept freezing

### [Improve Your Productivity with Roslyn Analyzers](https://channel9.msdn.com/Events/dotnetConf/2020/Improve-Your-Productivity-with-Roslyn-Analyzers)

- Roslyn is the C# compiler with an open API surface that let's you plugin other technologies, one of which is code analysers
- diagnostics, suggestions and code fixes
- report violations: error, warning, suggestion, hidden
- hidden is refactoring suggestions, eg extract method
- style support for XML comments, also for `inheritdoc`
- (new C# feature - default constructor when variable type is defined, eg `List<int> list = new()`)
- show parameter names when pressing alt-f - or always if configured
- Regex completion
- DateTime format suggestions
- best practises
  - they've been disabled for a long time to avoid breaking stuff, but now they're enabling more
  - project setting `AnalysisLevel` to revert to previous behavior, or use a later behavior
- second half was about how to write a Roslyn analyser, which I'm not interested in

### [Introducing the New and Improved Azure SDK for .NET](https://channel9.msdn.com/Events/dotnetConf/2020/Introducing-the-New-and-Improved-Azure-SDK-for-NET)

- New team to create consistency in all the Azure SDKs
- [idiomatic, consistent, approachable, diagnosable, dependable](https://aka.ms/azsdk/guide)
- in depth description about how the SDK works internally
  - not necessary to know for the simple use case
  - but could be interesting for extending or diagnosing
- pipeline is immutable, which means that a single client can be used by multiple threads

### [Level-up Your DevOps with GitHub Actions and Kubernetes](https://channel9.msdn.com/Events/dotnetConf/2020/Level-up-Your-DevOps-with-GitHub-Actions-and-Kubernetes)

- https://github.com/robrich/levelup-devops-github-actions-kubernetes
- demo creating a project from scratch, dockerizing it (multi-stage, including using docker to build instead of local)
- then deploy to k8s - copy-paste yaml because it's always the same
- Github Actions - build container (tag with sha), push to registry, apply to k8s (including replacing params in k8s yaml)
- flawless and complete demo
