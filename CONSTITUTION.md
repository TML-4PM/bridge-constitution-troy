# T4H Bridge Constitution v2

## 1. Constitutional separation
T4H contains two independent systems: the MCP System and the Super-Agent. They share the T4H world but do not share authority.

```text
                         T4H
                          │
              ┌───────────┴───────────┐
              │                       │
              ▼                       ▼
        MCP SYSTEM              SUPER-AGENT
              │                       │
        own authority            own authority
        own identity             own identity
        own scopes               own scopes
        own permissions          own permissions
        own capabilities         own capabilities
              │                       │
              ▼                       ▼
        MCP tools/services       agents/workers/tools
              │                       │
              └───────────┬───────────┘
                          ▼
                     T4H WORLD
```

MCP authority is not Super-Agent authority. Super-Agent authority is not MCP authority.

## 2. MCP system
MCP is the governed capability and tool-access system.

Capability paths are classified by risk:
- **low** — broad, low-impact, reversible/read-oriented access.
- **BAU** — high-value, frequent-use, pre-approved capability sets.
- **high** — specialist, consequential, privileged, or sensitive access.

Persistence is independent:
- **one-shot** — one invocation.
- **session** — current authorised session.
- **permanent** — standing access approved by policy.

Risk and persistence are independent attributes.

## 3. Super-Agent system
The Super-Agent is an independent autonomous problem-solving and repair system. It has its own identity, authority, scopes, permissions, capabilities, tools, agents/workers, execution rights, and evidence model.

It diagnoses, plans, traverses authorised boundaries, executes, verifies, repairs failures, re-plans, and completes objectives.

The Super-Agent is NOT an MCP permission gate, does NOT sit in the MCP routing path, and does NOT inherit MCP permissions.

## 4. Shared boundaries
Both systems may access GitHub, cloud, files, data, LLMs, runtime, applications, APIs, and other T4H boundaries. Each uses its own authorised path. Any cross-system interaction is an explicit integration contract, never implicit authority inheritance.

## 5. MCP capability attributes
```yaml
risk: low | bau | high
persistence: one_shot | session | permanent
boundary: github | cloud | data | files | llm | runtime | external | other
authority: read | write | execute | admin
capability: <stable identifier>
version: <contract version>
principal: <MCP identity>
```

## 6. Endpoint discipline
Keep public ingress deliberately small. Do not create duplicate public endpoints for tools, providers, models, workers, runners, or adapters. Internal services may remain independently deployed.

## 7. Evidence
Agent claims are not execution proof. Successful operations require observable evidence appropriate to the capability. High-risk operations require stronger verification and durable audit evidence.

## 8. Open-source first
Reuse mature open-source protocol implementations and infrastructure where they fit. T4H retains ownership of authority, capability taxonomy, risk/persistence policy, boundary model, and evidence contracts.

## 9. Migration
Existing Bridge/MCP repositories are reference material until proven fit. Reuse working code and sound designs; redesign broken parts. Do not delete or consolidate solely from repository names. Disposition requires implementation, caller, deployment, dependency, and capability evidence.
