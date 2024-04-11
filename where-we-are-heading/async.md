# Async engine

The async engine component or set of components would enable your AI software development system to accomplish tasks that require many steps. Often referred to as “agents” by some developers, it likely requires reasoning, planning, and proactive capabilities.

## Reasoning

To get help on tasks that include many steps, this likely requires some sort of reasoning engine. It could also be a model, depending on how LLM capabilities improve. [SWE-Agent](https://swe-agent.com/) and [Devin](https://www.cognition-labs.com/introducing-devin) are early projects that excite people about the possibilities of reasoning, and there are indications that OpenAI and other research labs are working in this direction. There are still many open research questions here though.

## Planning

For slower, asynchronous tasks (e.g. multi-file refactoring), planning in a task environment is needed to run workflows. The task environment should contain common developer tools, including a shell, code editor, and browser within a sandboxed compute environment—everything a human would need to do their work. Examples heading in this direction include [Code Interpreter](https://platform.openai.com/docs/assistants/tools/code-interpreter) and [OpenInterpreter](https://www.openinterpreter.com/) as well as sandboxes like [e2b.dev](http://e2b.devhttps://e2b.dev/). This is also an important area of exploration for research labs that frequently goes hand-in-hand with reasoning.

## Proactive

In addition to reasoning and planning capabilities, you are likely to want an “agent” to be able to 1) ask for help from developers when it gets stuck or needs feedback and 2) offer support before the developer asks for help. This makes reasoning and planning even more complex and challenging, since you don’t want to overwhelm or annoy developers with notifications.