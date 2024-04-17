> We believe in a future where developers are amplified, not automated

## Introduction

In the era of [Large Language Models (LLMs)](https://www.youtube.com/watch?v=zjkBMFhNj_g), software development is becoming increasingly automated by AI copilots. Many folks are forecasting that AI will replace developers in as little as a few years, while investors declare the arrival of superhuman AI software engineers. This worries some developers and annoys others.

Our motivation with `amplified.dev` is to instead 1) empower developers and 2) raise awareness of systemic issues we’ve seen in how engineering organizations are adopting, using, and evolving AI software development systems.

Our hope is that, over time, we can find a shared vocabulary for discussing these problems. For now, we describe the [current state of the world](#where-we-are-today), [where we are heading](#where-we-are-heading), and [what amplified developers need their organizations to do today](#amplified-developers):

1. [Establish an architecture of participation](#1-establish-an-architecture-of-participation)
2. [Enable the right models for the job](#2-enable-the-right-models-for-the-job)
3. [Measure and improve system metrics](#3-measure-and-improve-system-metrics)
4. [Standardize permissions and integrations](#4-standardize-permissions-and-integrations)
5. [Adopt open-source interfaces](#5-adopt-open-source-interfaces)

## Where we are today

What we call “AI copilots” are much more than a single LLM. As the Berkeley Artificial Intelligence Research Lab points out, [“state-of-the-art AI results are increasingly obtained by compound systems with multiple components, not just monolithic models”](https://bair.berkeley.edu/blog/2024/02/18/compound-ai-systems/).

As more of software development is automated, we are seeing more human engineering time go into monitoring, maintaining, and improving the different components that make up AI software development systems. That said, most copilots to date have been black box, SaaS solutions with roughly the same components, which you often have little to no ability to understand or improve.

- [Tab model](./where-we-are-today/tab.md)
- [Chat model](./where-we-are-today/chat.md)
- [Local context engine](./where-we-are-today/local.md)
- [Server context engine](./where-we-are-today/server.md)
- [Filtering](./where-we-are-today/filtering.md)

## Where we are heading

Among the changes on the horizon are two new components (async engines and training engines) and three trends that are likely to expand the standard AI software development system (further specialized models, better toolchain integrations, and increasingly modular systems).

- [Async engines](./where-we-are-heading/async.md)
- [Training engines](./where-we-are-heading/training.md)
- [Trends](./where-we-are-heading/trends.md)

AI software development systems are evolving quickly. In order to avoid vendor lock-in, keep up as new components emerge, and customize your AI dev system to your specific needs, you need an approach that enables freedom and flexibility.

## Amplified developers

Companies at the frontier like [Google](https://blog.research.google/2023/05/large-sequence-models-for-software.html), [Meta](https://arxiv.org/abs/2402.09171), [Nvidia](https://research.nvidia.com/publication/2023-10_chipnemo-domain-adapted-llms-chip-design), [Airbnb](https://youtu.be/_kV7fUVGz9E?si=9YWu-UQGE6CuPeuM), and [Uber](https://youtu.be/zQ5e3B5I-U0?si=UNtJo3DDxhrZBoE5) have platform development teams that create their own AI software development systems. We are seeing many more organizations head down the same path.

Similar to when DevOps was known as “web operations”, we are in the early days of creating and standardizing workflows and tools. As we converge on best practices, platform development teams are establishing AI software development systems as a key aspect of their initiatives to improve developer experience.

While there’s definitely some work required to set up a good system, you can expect its value to increase over time, so start early! The organizations that find the most success will create the right set of initial conditions:

### 1. Establish an architecture of participation

Amplified developers use AI software development systems and are actively involved in improving them.

**Actions to take now**

- Commit to a future where developers are amplified and tell your team
- Ensure your AI dev system is modular and designed for user contribution
- Set up a sustainable way to configure and roll out updates to your team
- Make it easy to share prompts, context providers, slash commands, etc.

Like DevOps, this is a practice that requires the whole team. You need to make sure to design your AI software development system with an [architecture of participation](https://web.archive.org/web/20120208001626/http://www.oreillynet.com/pub/a/oreilly/tim/articles/architecture_of_participation.html) in mind. When anyone on your team gets a wrong / bad suggestion from the system, they should be able to do something about it. This is critical because these systems are so often wrong today.

But this is only possible if each developer has the opportunity to participate in the creation and maintenance of the system. If this true, then over time, the system will increasingly help construct and maintain the software you create within your organization, while the developers who previously did that work shift more time to working on the system itself.

### 2. Enable the right models for the job

Amplified developers need the freedom to use and reuse the right models and components to automate tasks.

**Actions to take now**

- Set up a proxy server to make LLMs available to developers
- Make multiple models available and compare their usage
- Provide explicit guidance on how developers can test models locally
- Ask developers to share about how they are using your AI dev system

Situations and environments vary so much that developers are going to need figure out how to balance speed, quality, cost, and other constraints when automating part of their job. To do this, they need to be able to know about the models they are using and have choice over when, where, and how to use them.

The state-of-the-art is moving so fast that even models released six months ago can be outdated, so you don’t want to be locked into any particular vendor. You want to be able to constantly swap out and try different models. Empowering developers in this way will set them up to use the specific model best suited to each task (e.g. autocomplete, chat, re-rank, embed, etc.)

### 3. Measure and improve system metrics

Amplified developers need to understand how the AI software development system works and have the information to decide whether their changes lead to better outcomes.

**Actions to take now**

- Collect [development data](https://continue.dev/docs/development-data) when developers use LLMs
- Determine what KPIs are worth tracking for your team
- Set up dashboards that show your system usage
- Identify opportunities for improvement from the data
- Make changes to the components to improve KPIs

Your system will likely not be the best when you first stand it up, but if you collect data, you will set yourself up to improve it over time. You’ll also be able to show the value / ROI / positive impact on productivity. This will set you up to get more budget and resources from your organization for future system investments.

When you use LLMs while coding, you generate development data that shows the step-by-step process taken to complete a task, the context used to decide what to do at each step, and natural language that explains the reasoning behind the steps. It’s data on how you build software—the stuff that happens in between Git commits, which is created as a by-product of using LLMs while coding.

The ability to collect this data is critical. AI models are as good at coding as they are because developers made their code publicly available on GitHub, and you being able to keep your development data is going to be critical for your ability to understand and improve your AI software development system in the future.

The reason this is necessary is because each of us has our own definition of the right way to build software. To gain mass adoption, the AI systems that we use to build software need to not only respect this but also reflect it. When suggestions we get from AI systems do not meet [our definition of the right way to build software](https://joshcollinsworth.com/blog/copilot), we need to be able to [improve them](https://blog.continue.dev/improve-code-suggestions/).

### 4. Standardize permissions and integrations

Amplified developers need clear guidance about how data should flow into and out of the AI software development system.

**Actions to take now**

- Allow data software development lifecycle data to be used as context
- Explore how you can allow “write action” integrations (e.g. creating Jira tickets)
- Centralize the management of tokens, so folks automatically follow best security practices
- Follow Principle of least privilege (PoLP) but make it easy for folks to request access

You want to give LLMs as much relevant information as possible to get the best suggestions, so allowing for integrations but putting proper permissions that enable this will be important. This is both read and write access for not only human developers but also for the AI software development system.

Already today you’ll want to deploy embeddings, a “chat” model, a configuration server, a shared index, and more, so you need permissions and integrations that enable you to index any codebase and reference it with context providers. There is also lots of data from across the software development lifecycle that you will want to pull in more and more over time (i.e. GitLab Issues, Confluence docs, etc) too.

Best practices from web apps and DevOps apply here too. Permissions and integrations can get messy quick, so having a good approach here will set you up to evolve much better.

### 5. Adopt open-source interfaces

Amplified developers need standardized interfaces (i.e. IDE extensions today), so that an open an ecosystem can emerge within and across organizations.

**Actions to take now**

- Educate developers on your team about development data
- Roll out open-source interfaces to your team
- Push for other organizations to also standardize on the same interfaces

The interface between developers and AI should be open source. This enables all of us to 1) build an open ecosystem of components decoupled from the interface and 2) ensure that data emitted by the interface, which will be used to make increasingly capable models for software development, is pooled and directed by its owners rather than being collected and monopolized by a centralized, closed-source interface.

Today, this interface is often in the form of an IDE extension that likely includes a GUI, prompts, basic retrieval systems, configuration, and abstractions that allow you to plug in other components (e.g. your own RAG system). Much like Docker, Linux, and Git, the interface between developers and AI is so critical that we believe it will ultimately be public infrastructure.

## Conclusion

When a new tool enters your workflow, it changes how you think. As software development is increasingly automated, we need to be able to shape AI software development systems, so that we can shape how we think. But AI is not going to magically do everything. When it works, developers will move toward higher levels of abstraction. When it doesn’t, we should be able to do something about it.

This is another wave like DevOps, analytics, supervised ML systems, etc. which is expanding the number of problems available to reliable automation. As a result, the principles that will lead to success will be the same as they have always been: successful teams will set a foundation, adopt best practices, look to iterate, build internal tools, and talk candidly with their team.

All in all, each of us will need to actively participate in the construction and maintenance of AI software development systems. This shouldn’t be a surprise; if you or your fellow developers use a code assistance tool every day, maybe even seeing suggestions on every keystroke, you know that each improvement has a huge effect on productivity; as much, if not more, than any other developer tool that you could spend time and resources on improving.

If we put our energy into crafting the right AI software development systems in the right way, developers will be amplified, instead of being automated. Perhaps one day all developers will do is sit around a table discussing where to point their AI software development system next. But, for now, we have a lot of work to do to head towards that!

_If you believe in a future where developers are amplified, join us by adding your name and opening a pull request [here](https://github.com/continuedev/amplified.dev/edit/main/authors.md)._
