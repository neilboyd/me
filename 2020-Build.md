# MS Build 2020

[Build 2020](https://mybuild.microsoft.com/)
was a free, online event this year because of Covid-19.
It was a 48 hour, multi-stream event,
so I only watched a small sample.
Here are some notes from some of the sessions that I watched.

- [Every developer is welcome, with Scott Hanselman and guests](https://mybuild.microsoft.com/sessions/871ef73f-f04a-405b-a0fa-01d7433067d1)  
If you only watch one video it should be this one  
-[Linux for Windows](https://aka.ms/wsl) - is GA  
-[Windows package manager](https://aka.ms/winget) - preview - something like [Chocolatey](https://chocolatey.org/)  
-[CodeSpaces](https://aka.ms/codespaces) - private preview - VsCode on a VM directly in github - green button where the clone button is - seems like there's a version for VS online and a different version for GitHub

- [Scott Guthrie keynote](https://mybuild.microsoft.com/sessions/f58eb603-46cb-4d4b-975f-338d587b3d7d)

- [C# Today & Tomorrow](https://mybuild.microsoft.com/sessions/cea64369-aed9-4497-83f1-d3cf1360a57d)  
A few highlights of C# 8 and more about what's coming up in C# 9

- [What’s new with Application Insights & Azure Monitor](https://mybuild.microsoft.com/sessions/279676e7-2c9b-4209-a070-b393812bae16)  
Improved data table querying - workspace is the core - good demo of digging through logs

- [Azure Logic Apps and API Management](https://channel9.msdn.com/Events/Build/2020/BOD127)  
Logic apps on functions runtime - can edit in VsCode

- [Azure Cosmos DB](https://mybuild.microsoft.com/sessions/d29f7dd6-0e89-4d05-a417-86e0b7513a20)  
C# notebooks. eg to generate sample data -
autoscale is GA - can enable autoscale on existing database -
coming soon : consumption / serverless plan.

- C++  
I watched a part of a session that I can't find now
where the guy was saying that they've modernized C++ and made it easy to make incremental improvements to code,
eg if it sees a pointer and a length it'll suggest to use a span.
Visual Studio will give you hints for the parts you're working on,
without enforcing huge changes everywhere.  
This sounds like it could be interesting to people taking on development of legacy apps.
