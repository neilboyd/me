# [.NET Conf 2020](https://channel9.msdn.com/Events/dotnetConf/2020)

TODO

- [ ] intro
- [ ] update L6n site

## [KeyNote](https://channel9.msdn.com/Events/dotnetConf/2020/Keynote-Welcome-to-NET-5)

- Better Git integration in Visual Studio
- GitHub Actions in Visual Studio
- Blazor looks better and faster and debugging
- Great Swagger (Open API) support
- Project Tye to make K8s easier

## [Day One](https://channel9.msdn.com/Events/dotnetConf/2020?sort=status&direction=desc&d=1)

### [What’s New in C#?](https://channel9.msdn.com/Events/dotnetConf/2020/Whats-New-in-C)

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

### https://channel9.msdn.com/Events/dotnetConf/2020/A-talk-for-trailblazers-Blazor-in-NET-5

### [Porting Projects to .NET 5](https://channel9.msdn.com/Events/dotnetConf/2020/Porting-Projects-to-NET-5)

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

### https://channel9.msdn.com/Events/dotnetConf/2020/Modern-Web-Development-with-Blazor--NET-5

### https://channel9.msdn.com/Events/dotnetConf/2020/Developing-and-Deploying-Microservices-with-Tye

### https://channel9.msdn.com/Events/dotnetConf/2020/MLNET-in-the-Real-World

### [Developer Fun with Scott Hanselman](https://channel9.msdn.com/Events/dotnetConf/2020/Developer-Fun-with-Scott-Hanselman)

- I watched the first few minutes and it's just some fun - nothing new.

## [Day Two](https://channel9.msdn.com/Events/dotnetConf/2020?sort=status&direction=desc&d=2)

### https://channel9.msdn.com/Events/dotnetConf/2020/GitHub--Visual-Studio--NET

### https://channel9.msdn.com/Events/dotnetConf/2020/Whats-New-in-Visual-Studio-2019-and-beyond

### https://channel9.msdn.com/Events/dotnetConf/2020/Improve-Your-Productivity-with-Roslyn-Analyzers

### [Accelerate .NET to Azure with GitHub Actions](https://channel9.msdn.com/Events/dotnetConf/2020/Accelerate-NET-to-Azure-with-GitHub-Actions)

- mostly just an intro with slides
- Actions is still behind Azure DevOps so no urgent need to move

### https://channel9.msdn.com/Events/dotnetConf/2020/Introducing-the-New-and-Improved-Azure-SDK-for-NET

### [Setting Up Feature Flags with .NET](https://channel9.msdn.com/Events/dotnetConf/2020/S236)

- using [Split](https://split.io/product/feature-flags/), not the .Net Core feature
- kill switch
- A/B testing
- subscription management
- canary release
- different differentiators: user, device, location, etc
- approval
- demo wasn't very good, but maybe she just wasn't a good presenter
- the product supports good best practises

### https://channel9.msdn.com/Events/dotnetConf/2020/Level-up-Your-DevOps-with-GitHub-Actions-and-Kubernetes

### https://channel9.msdn.com/Events/dotnetConf/2020/Blazor-Client-Side-vs-Server-Side-Hands-on-Development-and-Deployment

### https://channel9.msdn.com/Events/dotnetConf/2020/Architecting-Cloud-Native-Application-in-Azure-using-NET-Core

## [Day Three](https://channel9.msdn.com/Events/dotnetConf/2020?sort=status&direction=desc&d=3)

### https://channel9.msdn.com/Events/dotnetConf/2020/Azure-Management-Superpowers-with-Pulumi
