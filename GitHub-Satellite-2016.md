# GitHub Satellite Conference Amsterdam 11 May 2016

[GitHub Satellite](http://githubuniverse.com/satellite/)
was a one-day conference in Amsterdam, primarily aimed at developers.

There was no focus on any specific technology since GitHub is just a platform,
but insted a focus on the workflows of software development.

There was a `Develop` track and a `Discover` track.
I had intended to attend the `Develop` track, but ended up on the `Discover` track,
which turned out to be a good choice.

## Opening keynote - Chris Wanstrath, Co-founder and CEO GitHub

GitHub was founded in the USA but is now growing much faster in Europe,
with 21% increase in traffic and 100% increase in signups every year.
They have more anonymous users than logged in users.
This growth is accredited to the growth of the open source community,
eg. some large projects such as Linux, MySQL and jQuery.

Some big companies that are traditionally closed source are now embracing open source,
and even putting others to shame in the way that they manage the open source projects,
eg Apple with Swift and Microsoft with .Net and ASP.

Open source is not just about putting source online, it's about the way you run the project.
It's a way to work with other people in a community.
It's more about the developer than the code.

He talked about the way some traditionally slow organizations are adopting open source,
for example governments, and specifically the UK government with the
[alphagov/whitehall](https://github.com/alphagov/whitehall) project
which makes it easy for the government to surface data to a website.
The people that work there are not experts at making websites,
but this project can make them experts, or make it so that they don't need to be experts.

He then continued with a few topics on the theme of GitHub catering to their own workflow,
ie [dogfooding](https://en.wikipedia.org/wiki/Eating_your_own_dog_food) :

- Emoji reactions reduce the number of issue comments
- Saved replies and issue and [PR](https://help.github.com/articles/using-pull-requests/)
templates to make it easier to reply to repeated questions and help people make PRs
- Squash your commits from the merge button - they didn't build it for a long time because it's not in their internal workflow

Finally a few announcements :
- GitHub Enterprise 2.5 release - main feature is clustering to allow it to run on multiple servers
- Electron 1.0 release - framework to build desktop apps in web technologies, used by Atom, VSCode and Slack
- [Unlimited private repositories](https://github.com/blog/2164-introducing-unlimited-private-repositories) - billing
per user for company accounts, instead of the previous per repository plan.

## Hubot - Brent Beer, GitHub

I must admit I don't yet understand the power of
[Hubot](https://hubot.github.com/docs/),
but the people at GitHub swear by it.
It allows you to perform tedious and repetitive tasks with a simple command.

## Social coding at SAP - Thomas Jansen, SAP

He is a Product Owner who was given the task two years ago to improve the developer experience at SAP.
He has given more responsibility to development teams.
Not just developing, but also maintaining deployments.

They moved to GitHub because it's perfect for collaboration and working with open source.
They met with initial management resistance,
which can be a good sign because it means you're really trying to change something.

They coined the "satellite" name,
meaning tools that are tightly integrated but lightly coupled.

They developed a logical sequence of satellites as they adopted the GitHub workflow across the company :

- [PSCHub](http://www.rachelreynard.com/pschub/) - compliance management
- Bridge - an [inner source](http://dirkriehle.com/services/inner-source/benefits/platform-development/)
internal dashboard that was kicked off with hackathons across the company
- [ReviewNinja](https://www.review.ninja/) - a more controlled code review process that appealed to the people
that otherwise prefered [Gerrit](https://www.gerritcodereview.com/)
- [CLA assistant](https://cla-assistant.io/) - when they started getting PRs for their open source projects,
they released that [CLA](https://en.wikipedia.org/wiki/Contributor_License_Agreement)'s
are not well integrated with GitHub
- GitHub insights - a layer on top of issues that provides hierarchy and ranking.
Developer doesn't need to use it but can be used for planning

Now SAP has 9000 GitHub users across multiple disciplines.
They created a bootstrap page for new users to document how to get started, create first PR, etc.
They develop some large open source projects, such as
[TwoGo](https://www.sapstore.com/solutions/60051/TwoGo)
and
[Concur platform](https://www.concur.com/).

## Inspiring innovation - Peter Klenk, IBM

- Enterprises are worried about getting "uberred" - a disruptive technology
can come out of nowhere and destroy their business
- Existing culture inhibits innovation and speed
- IBM is moving to smaller "two pizza" teams
- Microservices naturally comes out of this because small teams can't create big projects
- Moved from Scrum to Kanban
- All stakeholders are the in same channels in Slack
- It's hard to change a large enterprise.
Rather than hiring in external experts to help,
they looked for teams within IBM that were breaking out of the mold.
- Initially created private repositories within their GitHub Enterprise,
but realized it's better to inner source to share code within the organization.
- Documented their process: [www.ibm.com/devops/method](https://www.ibm.com/devops/method)
- Better to have 10 tests that can run reliably and repeatedly with CI than 1000 that are not.
- [OSS](https://en.wikipedia.org/wiki/Open-source_software) is ubiquitous, but not all OSS is the same.
Free is not always good. It should have responsible licensing and open governance.
- eg nodejs - technology was good but governance was bad, which led to the project being
[forked](http://anandmanisankar.com/posts/nodejs-iojs-why-the-fork/).
- eg [Parse](http://parse.com/) - Facebook
[pulled the plug](http://blog.parse.com/announcements/moving-on/)
and open sourced it, but there's no community so it'll die

## Optimizing for cognitive workflows - Laurent Ploix, Spotify

A vague talk about problems of scaling and matching your development workflow to human characteristics.
People are bad at context switching, so your workflow should be optimized to give quick feedback.
He was describing a build system that they're working on which will statistically calculate
which tests are most likely to fail based on who committed and what has changed,
and then run those tests first and give feedback within seconds.
You only need to know relevant information - if something breaks, only need to know the delta,
eg which lines of code are not covered by tests that were previously.

## Every company is a software company - panel

This was a group of VPs etc of big companies

https://twitter.com/vanderGoes/status/730387318473957376

Best way to increase user experience is to improve development process
Technology as a differentiator for a non-technology company

In Europe people are more focused on working on things that matter, cf career in US
Developers are a scarce resource so it's important to create a nice environment for software development

GitHub shows how important the social and collaborative aspect

Banking is regulated, so the person who developed is not allowed to deploy, and someone else should review

OSS is a given
- even if you buy software it contains open source
- more interesting question is what we can learn from open source development - culture
- makes people proud of code - better code

Product managers etc also need to work with GitHub
- prioritizing features
- technical docs

PM etc has more trust in a group than an individual
- peer review
- developer-led organization / decision-making
