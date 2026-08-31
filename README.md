# T4H Bridge Constitution — 001 Reference

This repository is the Tech4Humanity-001 constitutional/reference surface for Bridge architecture.

## Current canonical model

T4H has two independent authority domains:

- **MCP System** — governed tool/capability access with its own identity, authority, scopes, permissions, capabilities, credentials and lifecycle.
- **Super-Agent** — autonomous solve/fix/repair system with its own independent identity, authority, scopes, permissions, capabilities, tools/workers, credentials and lifecycle.

The Super-Agent is **not** an MCP permission gate and is **not** in the MCP routing chain. Neither system inherits authority from the other.

MCP capability paths are classified independently by:

- risk: `LOW | BAU | HIGH`
- persistence: `ONE_SHOT | SESSION | PERMANENT`
- boundary
- scope
- permission
- authority
- credential reference
- contract version
- evidence requirement

BAU means an explicit approved capability set for the job; it is not a blanket server grant.

## Source of truth

The active v2 design package is maintained in the Tech4Humanity-002 `bridge-constitution` repository. This 001 repository remains a reference surface and must not introduce a conflicting architecture.

## Migration rule

Existing MCP/Bridge repositories are reference material until proven fit. Reuse sound code and open-source components where appropriate; redesign broken parts. Do not create duplicate public gateways.
