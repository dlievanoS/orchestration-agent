# Mona's Project Pulse agent team

I am using GitHub Copilot CLI in a Codespace to orchestrate the work on Mona's Project Pulse dashboard.

| Agent | Target model | Responsibility | Definition file |
| --- | --- | --- | --- |
| Orchestrator | Claude Sonnet 5.5 (`claude-sonnet-5.5`) | Coordinates the specialist agents and integrates their work. | [`.github/agents/orchestrator.agent.md`](../.github/agents/orchestrator.agent.md) |
| Planner | Claude Sonnet 5.5 (`claude-sonnet-5.5`) | Creates implementation phases, dependencies, and validation expectations. | [`.github/agents/planner.agent.md`](../.github/agents/planner.agent.md) |
| Designer | Gemini 3.8 Flash (`gemini-3.8-flash`) | Defines the dashboard's visual structure, usability, accessibility, and responsive design. | [`.github/agents/designer.agent.md`](../.github/agents/designer.agent.md) |
| Coder | GPT-5.4 (`gpt-5.4`) | Implements and validates the dashboard files. | [`.github/agents/coder.agent.md`](../.github/agents/coder.agent.md) |
