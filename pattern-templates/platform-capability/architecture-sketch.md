# Architecture Sketch: AI Analyst

> The HOW for the AI Analyst work: the technical shape the team has put forward for the AI Analyst.
> The team's architecture sketch, transcribed to markdown.
>
> This is the **generic LLM-agent reference pattern** the team has put forward (source: "General architecture of an LLM-powered agent"). 

## The sketch

```
USER INPUT
   |
   v
AGENT CORE / LLM  <-----------------------------+
   |--->  PLANNING  --->  TAKE STEPS            |
   |--->  MEMORY    --->  CONTEXT / HISTORY     |
   |--->  OUTPUT                                |
   |--->  TOOLS     --->  APIS / DB / CODE      |
   +--->  CRITIC    --->  VALIDATION  ----------+
```

## Components

| Box | Role (as drawn) |
|---|---|
| **User Input** | The consumer's plain-language question enters here. |
| **Agent Core / LLM** | The reasoning centre. Receives the input and coordinates every other component. |
| **Planning to Take Steps** | Breaks the question into a plan and executes the steps. |
| **Memory to Context / History** | Holds the conversation context and history the agent reasons over. |
| **Output** | Returns the answer to the user. |
| **Tools to APIs / DB / Code** | The agent calls out to APIs, databases and code to fetch and compute. |
| **Critic to Validation** | Checks the result, then loops back into the Agent Core before the answer is trusted. |

## Flows

- **User Input to Agent Core**: the question arrives.
- **Agent Core to Planning to Take Steps**: plan the work, take the steps.
- **Agent Core to Memory to Context / History**: read and write context.
- **Agent Core to Output**: return the answer to the user.
- **Agent Core to Tools to APIs / DB / Code**: fetch and compute against systems.
- **Critic to Validation to Agent Core**: validate the result, then loop back before responding.

