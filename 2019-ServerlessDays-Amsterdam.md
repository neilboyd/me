# ServerlessDays Amsterdam 29 March 2019

[ServerlessDays](https://serverlessdays.amsterdam/)
is a small conference that is part of a series of community events.
As the name implies, it's about
[serverless](https://en.wikipedia.org/wiki/Serverless_computing)
architecture,
which is about building applications where you only concern yourself with the application,
and not with the server that it runs on.
They are typically low cost, pay-per-invocation and highly scalable.

The two main providers are
Amazon [AWS Lambda](https://aws.amazon.com/lambda/)
and
Microsoft [Azure Functions](https://azure.microsoft.com/en-us/services/functions/).
Google also has
[Cloud Functions](https://cloud.google.com/functions/),
but this was barely mentioned.

## Serverless-as-a-bank

Talk about
[Moneyou](https://www.moneyou.nl/)'s journey to serverless.
Moneyou started 12 years ago as a mortgage product of ABN Amro
with outsourced development.
In 2016 it started as a retail banking app with in-house development,
and they started with serverless because
it's easier to be secure and compliant than in their own data centre.
The idea of serverless is that they don't touch the OS and don't do capacity planning.
They use [serverless.com](https://serverless.com/)
infrastructure-as-code.
They continually scan for compliance,
eg if they find an
[S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingBucket.html)
without encryption then they notify the the team responsible so that it can be fixed.

## Testing serverless applications

The testing pyramid for serverless applications can be thicker in the middle
because it's cheap to test a function.

## Serverless machine learning

ML looks for patterns in existing data and predicts results for new data.
Because ML tends to be server-intensive,
there's limited possibilities for serverless,
but it can be used as the glue for binding together other services.
Azure Functions has bindings for i/o to many data sources.
[Durable Functions](https://docs.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-overview)
can be used to coordinate jobs.

A couple of ML terms:
- overfitting: the model fits the past data very well but not good at predicting the future
- regularizing: making the model less complex

## Where serverless falls short

Azure Functions can use smart scaling for pull events,
eg for a function with a queue trigger,
it can scale quickly when it sees that there's a long queue.
This is not possible for push events,
eg HTTP trigger,
because the function is reactive.

Coming soon: premium functions:
A shortfall of functions is that they have a coldstart warmup time when the function scales to a new instance.
With reserved instances there will always be one reserved instance,
so that the scale is already ahead of current load,
in order to avoid the coldstart.
This is still within the consumption plan,
but using one more instance than would otherwise be used.

It's a common pattern to chain functions together, eg with queues.
A fallback of this design is that it's hard to handle errors.
[Logic Apps](https://azure.microsoft.com/en-us/services/logic-apps/)
and Durable Functions coordinate the child functions.

Durable Functions invoke other functions in a way that looks similar to calling an async method.
It may look like a long, sequential, top-level method,
but it's reliable.
The Durable Function stores state and wakes up when needed.

## Serverless security

With serverless,
more of the security responsibility moves from the application developer to the cloud provider,
but there are still many security considerations:
- [Serverless security top 10](https://www.puresec.io/blog/serverless-top-10-released)

A couple of interesting points are:
- dependency poisoning - injecting vulnerabilities into third-party libraries
- use least-privilege roles to restrict the blast radius in the event of an attack

## Orchestrating functions

This talk was comparing the three main cloud providers,
specifically in the area of orchestrating functions.

Azure Durable functions:
- good for developers: has a base type, each function has a durable trigger type
- good testing framework
- very good orchestration

AWS:
- good for some things, mainly performance

GCP:
- not much good for anything, but they have the best portal

## Safe deployments

Options for deploying:
- canary: deploy a small percent. If okay, deploy everything
- linear: deploy gradually over time

Use a post-traffic function after deployment,
eg to check NFA's such as encryption being enabled.
