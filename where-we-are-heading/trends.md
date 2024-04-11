# Trends

There are even more AI software development system components that are likely to emerge from trends that are just beginning: further specialized models, better toolchain integrations, and increasingly modular systems.

## Further specialized models

We are seeing a number of vendors beginning to train models for specialized use cases: 

- Cursor has a model aimed at [predicting your next edit](https://cursor.sh/cpp)
- Phind has a model aimed at [being just as good as GPT-4 but faster](https://www.phind.com/blog/introducing-phind-70b)
- Replit has a model aimed at [mimicking the behavior of LSP Code Actions](https://twitter.com/pirroh/status/1775327316157358564?s=20)
- Magic has a model aimed at [being able to use entire codebases as context](https://x.com/magicailabs/status/1666116935904292869?s=20)
- Poolside has a model aimed at [better helping with real world use cases](https://www.poolside.ai/)

We expect more and more specialized to be created and dispersed over time.

## Better toolchain integrations

We are seeing folks creating deeper, more custom integrations with their infrastructure:

- Being able to use [Jira tickets](https://continue.dev/docs/customization/context-providers#jira-issues) as context
- Being able to use [documentation sites](https://continue.dev/docs/customization/context-providers#documentation) as context
- Being able to use [database tables](https://continue.dev/docs/customization/context-providers#database-tables) as context

We expect to increasingly see more of the software development lifecycle integrated. Eventually, we believe that “write action” integrations will emerge too (e.g. create a GitHub Issue).

## Increasingly modular systems

Because model capabilities are improving so rapidly and developers are constantly figuring out new ways to leverage LLMs while coding, folks are designing their AI software development systems to be modular. This is because it ensures you minimize vendor lock-in, enables you to better keep up as AI progress occurs, and allows you to meet your specific requirements.

When new components become available or are shown to be valuable, your modular system gives you the flexibility and extensibility necessary to either buy them from vendors or build them yourself. At this point, betting on any particular model, provider, or tool completely is premature optimization. To create these systems, we each have our own needs, so we will need to create and tune our own reusable components.