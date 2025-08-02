## We believe in a future where developers are amplified, not automated

In the era of [Large Language Models (LLMs)](https://www.youtube.com/watch?v=zjkBMFhNj_g), software development is becoming increasingly automated by AI copilots. Many folks are forecasting that AI will replace developers in as little as a few years, while investors declare the arrival of superhuman AI software engineers. This worries some developers and annoys others.

Our motivation with `amplified.dev` is to **(1) empower developers and (2) raise awareness of systemic issues** we’ve seen in how engineering organizations are adopting, using, and evolving AI software development systems.

Our hope is that, over time, we can find a shared vocabulary for discussing these problems. For now, we describe the [current state of the world](#where-we-are-today), [where we are heading](#where-we-are-heading), and [what amplified developers need to do at their organizations today](#amplified-developers):

1. [Establish an architecture of participation](#1-establish-an-architecture-of-participation)
2. [Enable the right models for the job](#2-enable-the-right-models-for-the-job)
3. [Measure and improve system metrics](#3-measure-and-improve-system-metrics)
4. [Standardize permissions and integrations](#4-standardize-permissions-and-integrations)
5. [Adopt open-source interfaces](#5-adopt-open-source-interfaces)

## Where we are today

What we call “AI copilots” are much more than a single LLM. As the Berkeley Artificial Intelligence Research Lab points out, [“state-of-the-art AI results are increasingly obtained by compound systems with multiple components, not just monolithic models”](https://bair.berkeley.edu/blog/2024/02/18/compound-ai-systems/).

As more of software development is automated, we are seeing more human engineering time go into monitoring, maintaining, and improving the different components that make up AI software development systems. That said, most copilots to date have been black box, SaaS solutions with roughly the same components, which you often have little to no ability to understand or improve.

<details>
<summary>Autocomplete model</summary>
<br>
<p>The "autocomplete" model component is used to power code completion suggestions and is typically a 1-15B parameter model. The models are run on your laptop or on a remote server and have generally been trained with special templates like fill-in-the-middle (FIM) for code infilling. Because developers need a suggestion within 500ms, you generally need to use a smaller model in order to meet the latency requirements. However, the quality of suggestions you get from models that are too small is bad. Thus, the tab-autocomplete model is optimized primarily with these two constraints in mind. Examples of models used for code completion include <a href="https://arxiv.org/pdf/2107.03374.pdf">Codex</a>, <a href="https://developers.googleblog.com/2024/04/gemma-family-expands.html">CodeGemma</a>, <a href="https://arxiv.org/pdf/2308.12950.pdf">Code Llama</a>, <a href="https://deepseekcoder.github.io/">DeepSeek Coder Base</a>, and <a href="https://arxiv.org/pdf/2402.19173.pdf">StarCoder 2</a>.</p>
</details>

<details>
<summary>Chat model</summary>
<br>
<p>The “chat” model component is used to power question-answer experiences and is typically a 30B+ parameter model. Latency is not as important as it is for the “autocomplete” model, so most people choose the one that gives them the best possible responses, oftentimes opting for SaaS API endpoints. When SaaS isn’t possible or preferred, open-source models are self-hosted on a server for the entire team to use. Examples of models used for chat experiences include GPT-4, DeepSeek Coder 33B, Claude 3, Code Llama 70B, Llama 3 70B, etc.</p>
</details>

<details>
<summary>Local context engine</summary>
<br>
<p>The local context engine component is used to automatically gather relevant context from your current codebase or other parts of your software development lifecycle (e.g. Jira tickets). It is most commonly leveraged for the tab-autocomplete use case, where it handles timing, context, and filtering. The local context engine frequently leverages embeddings, full-text search, and the Language Server Protocol to provide fast responses for smaller-scale data.</p>
</details>

<details>
<summary>Remote context engine</summary>
<br>
<p>The remote context engine component is used to automatically gather relevant context from all of your codebases and your entire software development lifecycle. Like the local context engine, it uses embeddings to build an index of your codebase. It is critical when you have many and large codebases, so that you can create a single, shared index for all developers in your organization to use. It is also beginning to grow beyond codebases, incorporating software development lifecycle data like GitLab issues, Confluence docs, etc.</p>
</details>

<details>
<summary>Filtering</summary>
<br>
<p>The filtering component filters for suggestions that are low quality, insecure, or raise licensing concerns. It sometimes even asks for a new suggestion automatically. While the most common use case is to block suggestions matching public code, developers are also exploring filtering to make sure that suggestions can compile, pass a linter, pass tests, only use certain libraries, etc. before being shown to the user.</p>
</details>

## Where we are heading

Among the changes on the horizon are two new components (async engines and training engines) and three trends that are likely to expand the standard AI software development system (further specialized models, better toolchain integrations, and increasingly modular systems).

<details>
<summary>Async engines</summary>
<br>
<p>The async engine component or set of components would enable your AI software development system to accomplish tasks that require many steps. Often referred to as “agents” by some developers, it likely requires reasoning, planning, and proactive capabilities.</p>
<h3>Reasoning</h3>
<p>To get help on tasks that include many steps, this likely requires some sort of reasoning engine. It could also be a model, depending on how LLM capabilities improve. <a href="https://swe-agent.com/">SWE-Agent</a> and <a href="https://www.cognition-labs.com/introducing-devin">Devin</a> are early projects that excite people about the possibilities of reasoning, and there are indications that OpenAI and other research labs are working in this direction. There are still many open research questions here though.</p>
<h3>Planning</h3>
<p>For slower, asynchronous tasks (e.g. multi-file refactoring), planning in a task environment is needed to run workflows. The task environment should contain common developer tools, including a shell, code editor, and browser within a sandboxed compute environment—everything a human would need to do their work. Examples heading in this direction include <a href="https://platform.openai.com/docs/assistants/tools/code-interpreter">Code Interpreter</a> and <a href="https://www.openinterpreter.com/">OpenInterpreter</a> as well as sandboxes like <a href="https://e2b.dev/">e2b.dev</a>. This is also an important area of exploration for research labs that frequently goes hand-in-hand with reasoning.</p>
<h3>Proactive</h3>
<p>In addition to reasoning and planning capabilities, you are likely to want an “agent” to be able to 1) ask for help from developers when it gets stuck or needs feedback and 2) offer support before the developer asks for help. This makes reasoning and planning even more complex and challenging, since you don’t want to overwhelm or annoy developers with notifications.
</p>
</details>
<details>
<summary>Training engine</summary>
<br>
<p>The training engine component or set of components would enable you to use your <a href="https://continue.dev/docs/development-data">development data</a> to improve the LLMs you use. This could involve fine-tuning, domain adaptive continued pre-training, and/or pre-training models from scratch.</p>
<h3>Fine-tuning</h3>
<p>This approach is the most accessible to organizations in the near-term. A good rule of thumb is that this requires domain-specific instruction data and hundreds of GPU hours. The benefit of this approach is that it can shape the style and format of the suggestions for your organization and maybe even for particular teams or individual developers. This likely happens on a remote server using development data, though it could happen locally eventually. It could also become a continuous process that runs periodically like <a href="https://smol.ai/">smol.ai</a> and <a href="https://www.arcee.ai/">Arcee</a> are aiming to do.</p>
<h3>Domain adaptive continued pre-training</h3>
<p>This approach is likely to become more accessible to organizations in the medium-term. A good rule of thumb today is that this requires an open-source base model, billions of tokens of relevant company data, and thousands of GPU hours. Due to these requirements, this will almost certainly take place on a server. The benefit of this approach is that you can have a lot more control over model capabilities than what fine-tuning offers. This is how <a href="https://research.nvidia.com/publication/2023-10_chipnemo-domain-adapted-llms-chip-design">ChipNeMo was created by Nvidia</a> and how <a href="https://arxiv.org/pdf/2308.12950.pdf">Code Llama was created by Meta</a>, which both used Llama 2 as their base model.</p>
<h3>Pre-training models from scratch</h3>
<p>This approach is likely to become more accessible to organizations in the long term. A good rule of thumb today is that this requires trillions of tokens of Internet data, billions of tokens of relevant company data, and millions of GPU hours. The benefit of this approach is that you get complete control over model capabilities by determining what data is used for training. It could also be the case that you use vendors to help with this. For example, today OpenAI <a href="https://openai.com/form/custom-models">will create custom GPT-4 models for you</a> with prices starting at $2-3M, MosaicML has trained models for organizations like <a href="https://blog.replit.com/llm-training">Replit</a>, and Together will <a href="https://www.together.ai/products#custom-models">help you build models from scratch</a> too.</p>
</details>
<details>
<summary>Trends</summary>
<br>
<p>There are even more AI software development system components that are likely to emerge from trends that are just beginning: further specialized models, better toolchain integrations, and increasingly modular systems.</p>
<h3>Further specialized models</h3>
<p>We are seeing a number of vendors beginning to train models for specialized use cases:</p>
<ul>
    <li>Cursor has a model aimed at <a href="https://cursor.sh/cpp">predicting your next edit</a></li>
    <li>Phind has a model aimed at <a href="https://www.phind.com/blog/introducing-phind-70b">being just as good as GPT-4 but faster</a></li>
    <li>Replit has a model aimed at <a href="https://twitter.com/pirroh/status/1775327316157358564?s=20">mimicking the behavior of LSP Code Actions</a></li>
    <li>Magic has a model aimed at <a href="https://x.com/magicailabs/status/1666116935904292869?s=20">being able to use entire codebases as context</a></li>
    <li>Poolside has a model aimed at <a href="https://www.poolside.ai/">better helping with real-world use cases</a></li>
</ul>
<p>We expect more and more specialized models to be created and dispersed over time.</p>
<h3>Better toolchain integrations</h3>
<p>We are seeing folks creating deeper, more custom integrations with their infrastructure:</p>
<ul>
    <li>Being able to use <a href="https://continue.dev/docs/customization/context-providers#jira">Jira tickets</a> as context</li>
    <li>Being able to use <a href="https://continue.dev/docs/customization/context-providers#docs">documentation sites</a> as context</li>
    <li>Being able to use <a href="https://continue.dev/docs/customization/context-providers#database">database tables</a> as context</li>
</ul>

<p>We expect to increasingly see more of the software development lifecycle integrated. Eventually, we believe that “write action” integrations will emerge too (e.g. create a GitHub Issue).</p>
<h3>Increasingly modular systems</h3>
<p>Because model capabilities are improving so rapidly and developers are constantly figuring out new ways to leverage LLMs while coding, folks are designing their AI software development systems to be modular. This is because it ensures you minimize vendor lock-in, enables you to better keep up as AI progress occurs, and allows you to meet your specific requirements.</p>
<p>When new components become available or are shown to be valuable, your modular system gives you the flexibility and extensibility necessary to either buy them from vendors or build them yourself. At this point, betting on any particular model, provider, or tool completely is premature optimization. To create these systems, we each have our own needs, so we will need to create and tune our own reusable components.</p>
</details>

## Amplified developers

AI software development systems are evolving quickly. In order to avoid vendor lock-in, keep up as new components emerge, and customize your AI dev system to your specific needs, you need an approach that enables freedom and flexibility.

Companies at the frontier like [Google](https://blog.research.google/2023/05/large-sequence-models-for-software.html), [Meta](https://arxiv.org/abs/2402.09171), [Nvidia](https://research.nvidia.com/publication/2023-10_chipnemo-domain-adapted-llms-chip-design), [Airbnb](https://youtu.be/_kV7fUVGz9E?si=9YWu-UQGE6CuPeuM), [Salesforce](https://engineering.salesforce.com/codegenie-how-salesforce-leveraged-generative-ai-to-enhance-internal-developer-productivity/), and [Uber](https://youtu.be/zQ5e3B5I-U0?si=UNtJo3DDxhrZBoE5) have platform development teams that create their own AI software development systems. We are seeing many more organizations head down the same path.

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

But this is only possible if each developer has the opportunity to participate in the creation and maintenance of the system. If this is true, then over time, the system will increasingly help construct and maintain the software you create within your organization, while the developers who previously did that work shift more time to working on the system itself.

### 2. Enable the right models for the job

Amplified developers need the freedom to use and reuse the right models and components to automate tasks.

**Actions to take now**

- Set up a proxy server to make LLMs available to developers
- Make multiple models available and compare their usage
- Provide explicit guidance on how developers can test models locally
- Ask developers to share how they are using your AI dev system

Situations and environments vary so much that developers are going to need to figure out how to balance speed, quality, cost, and other constraints when automating part of their job. To do this, they need to be able to know about the models they are using and have choice over when, where, and how to use them.

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

- Allow data from your software development lifecycle to be used as context
- Explore how you can allow “write action” integrations (e.g. creating Jira tickets)
- Centralize the management of tokens, so folks automatically follow best security practices
- Follow Principle of Least Privilege (PoLP) but make it easy for folks to request access

You want to give LLMs as much relevant information as possible to get the best suggestions, so allowing for integrations but putting proper permissions that enable this will be important. This is both read and write access for not only human developers but also for the AI software development system.

Already today you’ll want to deploy embeddings, a “chat” model, a remote configuration server, a shared index, and more, so you need permissions and integrations that enable you to index any codebase and reference it with context providers. There is also lots of data from across the software development lifecycle that you will want to pull in more and more over time (e.g. GitLab issues, Confluence docs, etc.).

Best practices from web apps and DevOps apply here too. Permissions and integrations can get messy quicky, so having a good approach here will set you up to evolve much better.

### 5. Adopt open-source interfaces

Amplified developers need standardized interfaces (i.e. IDE extensions today), so that an open ecosystem can emerge within and across organizations.

**Actions to take now**

- Educate developers on your team about development data
- Roll out open-source interfaces to your team
- Push for other organizations to also standardize on the same interfaces

The interface between developers and AI should be open source. This enables all of us to 1) build an open ecosystem of components decoupled from the interface and 2) ensure that data emitted by the interface, which will be used to make increasingly capable models for software development, is pooled and directed by its owners rather than being collected and monopolized by a centralized, closed-source interface.

Today, this interface is often in the form of an IDE extension that likely includes a GUI, prompts, basic retrieval systems, configuration, and abstractions that allow you to plug in other components (e.g. your own RAG system). Much like Docker, Linux, and Git, the interface between developers and AI is so critical that we believe it will ultimately be public infrastructure.

## Conclusion

When a new tool enters your workflow, it changes how you think. As software development is increasingly automated, we need to be able to shape AI software development systems, so that we can shape how we think. But AI is not going to magically do everything. When it works, developers will move toward higher levels of abstraction. When it doesn’t, we should be able to do something about it.

At a minimum, this is another wave like DevOps, analytics, supervised ML systems, etc. which is expanding the number of problems available to reliable automation. As a result, the principles that will lead to success will be the same as they have always been: successful teams will set a foundation, adopt best practices, look to iterate, build internal tools, and talk candidly with their team.

All in all, each of us will need to actively participate in the construction and maintenance of AI software development systems. This shouldn’t be a surprise; if you or your fellow developers use a code assistance tool every day, maybe even seeing suggestions on every keystroke, you know that each improvement has a huge effect on productivity; as much, if not more, than any other developer tool that you could spend time and resources on improving.

If we put our energy into crafting the right AI software development systems in the right way, developers will be amplified, instead of being automated. Perhaps one day all developers will do is sit around a table discussing where to point their AI software development system next. But, for now, we have a lot of work to do to head towards that!

_If you believe in a future where developers are amplified, join us by adding your name and opening a pull request [here](https://github.com/continuedev/amplified.dev/edit/main/supporters.md)._
