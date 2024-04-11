# 4. Standardize permissions and integrations

If we want developers to be amplified, they need to have clear guidance about how data should flow into and out of the AI software development system.

**Actions to take now**

- Allow data software development lifecycle data to be used as context
- Explore how you can allow “write action” integrations (e.g. creating Jira tickets)
- Centralize the management of tokens, so folks automatically follow best security practices
- Follow Principle of least privilege (PoLP) but make it easy for folks to request access

You want to give LLMs as much relevant information as possible to get the best suggestions, so allowing for integrations but putting proper permissions that enable this will be important. This is both read and write access for not only human developers but also for the AI software development system.

Already today you’ll want to deploy embeddings, a “chat” model, a configuration server, a shared index, and more, so you need permissions and integrations that enable you to index any codebase and reference it with context providers. There is also lots of data from across the software development lifecycle that you will want to pull in more and more over time (i.e. GitLab Issues, Confluence docs, etc) too.

Best practices from web apps and DevOps apply here too. Permissions and integrations can get messy quick, so having a good approach here will set you up to evolve much better.