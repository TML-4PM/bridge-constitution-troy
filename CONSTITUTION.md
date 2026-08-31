# T4H Bridge Constitution

## 1. Authority
The Bridge is the T4H control-plane ingress and policy boundary.
`ENDPOINT_REGISTRY.yaml` is the canonical endpoint registry.

No client, worker, runner, LLM, MCP capability server, or specialist service may
create a competing public ingress for the same capability.

## 2. Canonical topology

```text
Client / Agent
      |
      v
  /bridge  <--- identity + authority + audit + routing
      |
      +--> /mcp                 MCP capability plane
      +--> /internal/runner     execution
      +--> /internal/llm        reasoning
      +--> /internal/mid        medium-risk services
      +--> /internal/low        low-risk services
      +--> /internal/special    specialist services
```

Only `/bridge`, `/mcp`, `/healthz`, and `/readyz` are public ingress surfaces.
Workers and downstream services are bridge-only.

## 3. MCP rationalisation
There is one canonical public MCP ingress: `/mcp`.
Existing MCP implementations are capability backends, not additional public
control planes. Duplicate public MCP URLs must be retired or converted to
bridge adapters.

## 4. Runner and LLM
The runner executes authorised work. The LLM reasons over authorised context.
Neither is a public endpoint. Both are invoked through the Bridge using the
same governed call envelope.

LLM routing is functional, explicit, and policy-controlled; model choice is a
routing decision, not an endpoint proliferation mechanism.

## 5. Risk tiers
- **low** — read-only, reversible, low-impact capabilities.
- **mid** — consequential operations requiring policy checks and evidence.
- **special** — specialist capabilities requiring explicit capability grants.
- **runner** — execution plane; never directly exposed.
- **llm** — reasoning plane; never directly exposed.

## 6. Required call contract
Every governed call carries:
`request_id`, `principal`, `capability`, `input`, `authority`, and
`correlation_id`.

Every successful response carries:
`request_id`, `status`, `result`, `evidence`, and `correlation_id`.

Every failure carries:
`request_id`, `status`, `error_code`, and `correlation_id`.

## 7. Security and governance
- Read-only by default.
- Writes require explicit capability and policy gates.
- Secrets never enter source, logs, responses, or evidence payloads.
- Health/readiness endpoints expose operational state only.
- Direct bridge bypasses are prohibited.
- Evidence must identify what was requested, authorised, executed, and returned.

## 8. Migration rule
Do not create another MCP, bridge, runner, or LLM public endpoint to solve a
routing problem. First register the capability, route it through the Bridge,
and retire the duplicate ingress.

## 9. Repository boundary
This repository governs the bridge contract. Runtime implementations live in
their appropriate service repositories and must conform to this registry.
