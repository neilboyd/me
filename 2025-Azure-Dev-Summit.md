# [Azure Dev Summit 2025](https://azuredevsummit.com/)

This was the first Azure Dev Summit, organized by Microsoft and NDC, in Lisbon.
There were 3 days of conference talks, followed by a 1 day workshop.

Here are my main takeaways:

- Agentic AI recognizes intent and context to give multi-step, proactive guidance.
  It converts a passive IDE into an active development partner.
- [GitHub Spec Kit](https://github.blog/ai-and-ml/generative-ai/spec-driven-development-with-ai-get-started-with-a-new-open-source-toolkit/)
  helps developers to describe detailed intent and requirements, and then it will create and execute a plan.
- Microsoft is developing an [SRE](https://en.wikipedia.org/wiki/Site_reliability_engineering) agent
  that can be a first line of defense for incident detection and remediation.
  It has all the context of code changes and resource state, and so it can make informed decisions.
- [.NET Aspire](https://learn.microsoft.com/en-us/dotnet/aspire/get-started/aspire-overview) has been renamed to just
  [Aspire](https://aspire.dev) because it's not just .NET.
- Aspire is an app that runs all your apps and dependencies, without requiring any changes to your existing codebase.
  However, it provides more comprehensive telemetry if you integrate Open Telemetry into your app with a few simple steps.
- The Aspire dashboard gives a unified view of the entire system, with visibility of dependencies, logs and metrics.
- Aspire always uses managed identities - never connection strings or secrets - for better security.
- Aspire is "dev first, ops friendly". It is a development and testing tool.
  Aspire itself is not deployed to production, although it can be used to deploy your environment (to production).
- [Playwright MCP](https://playwright.dev/docs/test-agents) is an agent that writes UI tests by describing user interactions
  in the way a user sees it (eg click the button "Next").
  It writes the test specification, and then generates, runs and fixes the tests.
  This way, in case you change your UI, it can regenerate the tests with the same intent.
- [Dev Containers](https://containers.dev/) provide a development environment that is consistent, isolated, and reproducible.
- [GitHub Codespaces](https://github.com/features/codespaces) uses Dev Containers to easily create a development environment in the cloud,
  for example to quickly spin up an environment for a code review.
- "Complexity is the worst enemy of security".
  50% of security flaws are business logic bugs rather than technical vulnerabilities.
- Copilot is a learning tool. Treat it as an enthusiastic intern. Don't vibe code into production!
- AI is good at solving problems we've already solved.
  It can do the dull work, leaving you to focus on the creative and interesting tasks.

---

For more details, see the longer
[conference report](https://neil-nipo-r-and-d.l6n.org/posts/azure-dev-summit/)
and [workshop report](https://neil-nipo-r-and-d.l6n.org/posts/azure-dev-summit-workshop/).
