# Canonical Hermes Agent + Buzz Integration

## Operating law

**Buzz coordinates. Hermes executes. Mission Control governs. The workspace preserves artifacts. Receipts prove the work.**

## System flow

```text
IDENTITY
  -> MANDATE
  -> BUZZ THREAD
  -> HERMES DISPATCH
  -> POLICY GATE
  -> PLAN
  -> EXECUTE
  -> ARTIFACT
  -> RECEIPT
  -> HUMAN REVIEW
  -> AUDIT
```

## Responsibilities

| Layer | Responsibility |
|---|---|
| Buzz | Signed communities, channels, threads, mentions, workflows, approvals, and search |
| HERMES Dispatch | Converts signed events into bounded job envelopes and routes agents |
| Hermes Agent | Plans and executes with approved browser, terminal, file, MCP, and workflow tools |
| Mission Control | Defines mandates, grants sensitive authority, reviews results, and revokes access |
| Shared workspace | Stores durable research, plans, guides, deliverables, and manifests |
| AEGIS | Enforces identity, capability, policy, isolation, and risk controls |
| Audit ledger | Records requester, approvals, tools, files, hashes, side effects, and disposition |

## Standard agent classes

- `hermes-researcher`: read-only external research and workspace writing
- `hermes-builder`: artifact and branch production without direct merge
- `hermes-reviewer`: evidence, diff, policy, risk, and receipt review
- `hermes-operator`: approved deployment and external side effects

Every agent has an independent key, channel membership, tool policy, credential set, workspace root, and audit trail.

## Standard job envelope

```json
{
  "community": "derived-from-relay-url",
  "channel_id": "channel-event-id",
  "thread_root": "root-event-id",
  "request_event": "signed-request-event-id",
  "agent": "hermes-researcher",
  "mandate": "Complete the bounded task",
  "allowed_capabilities": ["read_files", "web_research", "write_workspace"],
  "denied_capabilities": ["write_production", "publish_external", "spend_funds"],
  "output_path": "OUTBOX/task-name/",
  "approval_required": false
}
```

The envelope is enforced by runtime policy, not treated as prompt guidance.

## Standard workspace

```text
RESEARCH/   evidence and source notes
PLANS/      execution plans and checklists
GUIDES/     reusable operating procedures
OUTBOX/     review-ready deliverables
RECEIPTS/   manifests, hashes, approvals, logs, and side effects
```

## Standard receipt

```json
{
  "status": "review_ready",
  "artifact": "OUTBOX/task-name/result.md",
  "receipt": "RECEIPTS/task-name.json",
  "sha256": "artifact-hash",
  "request_event": "signed-request-event-id",
  "agent": "hermes-researcher",
  "tools_used": ["browser", "filesystem"],
  "files_changed": [],
  "external_side_effects": [],
  "approval_events": [],
  "open_questions": []
}
```

## Non-negotiable controls

- identity is not authority
- community state is isolated by Buzz relay URL
- capability limits are enforced outside the model
- websites, messages, files, and repositories are untrusted inputs
- duplicate events are handled idempotently
- destructive and external actions require explicit approval
- credentials are scoped and short-lived where possible
- every meaningful execution leaves a receipt
- humans retain final accountability

## Adapter boundary

The integration should remain a separate adapter process rather than coupling Hermes-specific code into the Buzz relay.

```text
integrations/hermes-buzz/
  README.md
  config.example.yaml
  schemas/
    job-envelope.schema.json
    receipt.schema.json
  src/
    intake
    policy
    dispatcher
    publisher
  tests/
    community-isolation
    capability-denial
    duplicate-event-idempotency
    approval-gates
    artifact-verification
```

## Delivery sequence

1. Read-only researcher in one test channel.
2. Repository builder using isolated branches and human merge.
3. Guarded operator using signed approvals and short-lived credentials.
4. Multi-agent routing with stable thread roots and Mission Control visibility.

This file is the cross-repository integration contract for AGENTROPOLIS Hermes systems.