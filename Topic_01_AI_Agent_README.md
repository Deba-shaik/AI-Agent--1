# Topic 1 - Setting Up the n8n Advanced AI Agent Environment

## Project overview
Workflow: `Topic_01_Advanced_AI_Agent`  
Platform: Tayana Solutions self-hosted n8n (version 2.40.7 shown in earlier execution details)  
Status: **Functional test passed**  
Evidence date: 10 November 2026

## Objective
Build an n8n conversational AI workflow, securely link a model credential, configure inference settings, run a chat test, and inspect the execution output and token usage.

## Workflow architecture
`When chat message received` -> `AI Agent` -> chat response  
The `OpenAI Chat Model` sub-node is connected to the AI Agent's required Chat Model port. No memory or external tool nodes were required for this introductory exercise.

## Node configuration
| Node | Configuration |
| --- | --- |
| When chat message received | Chat Trigger; public availability OFF during setup |
| AI Agent | Prompt source: Connected Chat Trigger Node; user prompt expression: `{{ $json.chatInput }}` |
| AI Agent system message | You are a professional AI assistant. Answer user questions clearly, accurately, and concisely. Follow instructions carefully and provide helpful responses. |
| OpenAI Chat Model | Credential: `OpenAI account 20`; model: `qwen/qwen-2.5-7b-instruct` |
| Model settings | Responses API OFF; maximum tokens 500; sampling temperature 0.0 |

## Implementation steps
1. Create the workflow `Topic_01_Advanced_AI_Agent` in n8n.
2. Add the `When chat message received` trigger.
3. Connect the trigger to an `AI Agent` node.
4. Connect an `OpenAI Chat Model` sub-node to the AI Agent's Chat Model port.
5. Select the existing company-managed credential and an available model.
6. Configure the model and AI Agent instructions as shown above.
7. Open the test chat, send a prompt, and inspect the execution and JSON output.

## Verification and observed results
The final shared screenshots show all three nodes with green success checks, a successful workflow execution, and an AI Agent JSON output:

```json
{"output":"Hello! How can I assist you today?"}
```

The model output reports `finish_reason: stop`, `promptTokens: 203`, `completionTokens: 10`, and `totalTokens: 213`. The workflow canvas reports successful execution in approximately 2.043 seconds; the model node reports approximately 1.734 seconds. These metrics refer to the demonstrated successful run, not a benchmark.

## Evidence index
- E1: Complete workflow with success indicators and execution logs.
- E2: AI Agent prompt configuration and returned JSON output.
- E3: Model configuration, generation response, and token counts.

## Deviations and scope
The source hands-on guide names GPT-4o or Claude 3.5 Sonnet. Neither was available in the model list shown in the provided screenshots, so `qwen/qwen-2.5-7b-instruct` was used through the company gateway. This substitution was successful for the functional exercise; acceptance against an exact-model rubric requires assessor approval. The supplied screenshots demonstrate a local test execution, not a production deployment. No API secret values are included in this README.

## Reproduction
Open the workflow in n8n, verify that the credential is available to your account, open chat, submit a short question, and inspect the AI Agent Output and OpenAI Chat Model JSON panes. If the credential or model is unavailable, consult the administrator of the company LLM gateway.
