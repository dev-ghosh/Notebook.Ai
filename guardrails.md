# Guardrails (in AI)

## Answer first
**Guardrails** are the rules and checks placed around an AI system so it behaves safely, stays on task and doesn't cause harm. The model generates; guardrails decide what is allowed in, what is allowed out, and what actions it may take. They are needed because LLMs are probabilistic: instructions alone can't guarantee behavior.

## 1. Types (by where they sit)
| Layer | What it checks | Example | 
|---|---|---|
| **Input** | The user's prompt before the model sees it | Block prompt injection, strip PII, reject off-topic requests |
| **Model-level** | The model's own training and system prompt | Safety training, refusal behavior, system prompt rules |
| **Output** | The response before the user sees it | Filter toxic content, check for leaked secrets, validate JSON format |
| **Tool / action** | What an agent is allowed to do | Read-only database access, human approval before sending email or spending money |
| **Monitoring** | What happens after deployment | Logging, audits, rate limits, alerts |

## 2. What they protect against
- Harmful or toxic content
- Prompt injection and jailbreaks
- Leaking private data (PII, API keys)
- Hallucinated or wrong answers presented as fact
- Agents taking irreversible or unauthorized actions
- Off-topic use and brand risk

## 3. How they're implemented
- **Rule-based:** regex, allow/deny lists, schema validation. Fast and predictable, but rigid.
- **Model-based:** a classifier or second LLM judges the input or output. Flexible, but can be wrong and adds cost and latency.
- **Permissions:** least privilege, sandboxing, approval gates. The strongest guardrail for agents.
- **Human-in-the-loop:** a person confirms risky steps.
- Common tools: NVIDIA NeMo Guardrails, Guardrails AI, provider moderation APIs, and in Claude Code its permission settings and hooks.

## 4. Example for an AI hiring agent
- Input: reject resumes containing hidden instructions aimed at the model
- Output: never produce a decision based on protected attributes; require a reason tied to job criteria
- Action: the agent can rank candidates but a human must approve any rejection or email

## 5. Limits and trade-offs
- No guardrail is perfect; stack several layers (defense in depth).
- Too strict → blocks legitimate use; too loose → misses harm.
- Instructions in a prompt are the weakest guardrail; enforce critical rules in code and permissions.
- Test them regularly with adversarial inputs (red teaming).

## 6. One-line takeaway
Don't trust the model to police itself on high-stakes actions: validate inputs, verify outputs, limit permissions, and keep a human in the loop.
