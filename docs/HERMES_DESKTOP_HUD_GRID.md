# HERMES Desktop HUD Grid

## Role

HERMES Desktop HUD is the governed floating operator surface for AGENTROPOLIS. It may observe approved screen context, ground answers in governed knowledge, and request scoped actions without receiving blanket authority over the desktop.

## Canonical Flow

```text
Foreground application / approved screen region
  -> HUD Context Capture
  -> App + Window Context Resolver
  -> AGENTROPOLIS Ingest Membrane
  -> 54-T containment + capability check
  -> WikiVault provenance lookup / approved knowledge retrieval
  -> HERMES reasoning surface
  -> advisory answer OR scoped action proposal
  -> Policy/Risk gate
  -> human approval when required
  -> app adapter / computer-use worker
  -> validation
  -> permanent action receipt
```

## Core Behaviors

### 1. Floating Composer
- one global shortcut toggles compact HUD mode
- HUD remains movable and dismissible
- HUD never implies background authority merely because it is visible
- each interaction carries the active app/window identity and capture timestamp

### 2. Screen Context
Supported capture classes:
- foreground application identity
- active window title
- approved screen region or screenshot
- accessibility-tree text where available
- user-selected text or object
- optional OCR fallback only where platform access requires it

Raw screen context is treated as untrusted sensor data. It must not write directly to sovereign memory.

### 3. App-Switch Detection
The HUD must not rely on the operator manually stating every app transition.

Required signals:
- foreground-process change
- active-window handle/title change
- capture timestamp
- display/monitor identity
- context epoch ID

When an app/window switch is detected, HERMES invalidates stale interaction assumptions and begins a new context epoch.

### 4. Knowledge Grounding
HUD answers may consult:
- WikiVault evidence records
- governed Obsidian materialization
- gBRAIN derived indexes
- approved local project docs
- repository context
- district-specific knowledge adapters

Rules:
- retrieved knowledge must preserve provenance
- gBRAIN is never treated as source of truth
- Quantization Torque may compact context but may not determine truth
- screen-derived claims remain explicitly separated from retrieved evidence

### 5. Action Modes
Per application, capability scopes are distinct:

1. `observe` — inspect approved screen/app context
2. `analyze` — summarize, classify, compare, explain
3. `draft` — prepare commands, text, edits, or proposed actions
4. `execute` — perform an approved action through a scoped adapter or computer-use worker

Execution is never inherited from Observe/Analyze/Draft.

## Example App Profiles

### GitHub
- observe repository, issue, PR, diff, workflow state
- analyze code/review context
- draft issue comments, review notes, branch/PR actions
- execute only through scoped GitHub capability handles

### X
- observe visible posts and approved account context
- analyze post/thread/signals
- draft replies/posts
- execute only through Social Transit Grid permissions and receipts

### Trading / Charting
- observe visible chart, timeframe, annotations, labels
- analyze price structure and visible indicators
- no trade execution from visual context alone
- financial execution requires a separately governed broker/wallet capability path

### Video Editor
- observe timeline/editor state
- propose edits and transport commands
- execute only through an editor-specific adapter or scoped computer-use worker

### Spotify
- observe now-playing/library context where authorized
- analyze artists, playlists, playback state
- execute playback controls only through approved media capability

### Steam
- observe visible library/game metadata
- aggregate visible statistics where permitted
- no credential exposure or purchase execution from HUD context

### SSH / Terminal
- observe only the approved terminal region/session metadata
- redact or block secret-like material before model context where possible
- commands are proposed first unless explicit execution permission exists
- high-impact shell, network, credential, package, or destructive operations require 54-T gating and human approval

## 54-T HUD Security Contract

The HUD is a high-risk sensor/actuator boundary and must pass 54-T containment checks.

Required controls:
- default-deny application execution
- per-app capability handles
- no raw passwords, cookies, API keys, tokens, seed phrases, private keys, or signing secrets in model context
- secret-pattern detection/redaction before model ingestion
- screenshot/context TTLs
- active-window provenance
- explicit capture indicators
- egress restrictions
- computer-use sandboxing
- Effective Capability Graph evaluation for transitive permissions
- app adapter attestation
- immutable read/action receipts
- kill switch and per-app revoke
- dual control for irreversible/high-impact actions

## Context Epoch Schema

```json
{
  "epoch_id": "uuid",
  "captured_at": "timestamp",
  "app_id": "string",
  "process_id": "string",
  "window_id": "string",
  "window_title": "string",
  "display_id": "string",
  "capture_mode": "region|window|accessibility|selection",
  "permissions": ["observe", "analyze"],
  "provenance": {},
  "risk_score": 0,
  "ttl_ms": 0
}
```

## HUD Decision Contract

Every HERMES HUD response should resolve into one of:
- `answer`
- `ask_for_selection`
- `draft_action`
- `request_approval`
- `execute_scoped_action`
- `deny`
- `quarantine_context`

No hidden transition from analysis to execution is permitted.

## Agent Wikis / External Knowledge

Agent Wikis or similar curated external knowledge products may be used only as external knowledge sources behind the Ingest Membrane. They are not sovereign memory and they do not bypass WikiVault provenance rules.

Recommended pattern:

```text
External wiki/API/content
  -> Ingest Membrane
  -> provenance + licensing + trust classification
  -> ephemeral retrieval or reviewed WikiVault evidence record
  -> HERMES HUD answer
```

Never ingest an entire third-party knowledge service directly into durable memory without evidence records, provenance, scope, and review.

## Beta Acceptance Tests

HUD beta is not production-ready until these pass:

1. foreground app switch creates a new context epoch
2. stale app assumptions are invalidated after switch
3. hidden/background windows are not captured unless explicitly allowed
4. secret-like text is blocked/redacted before model context
5. Observe permission cannot trigger execution
6. Draft permission cannot publish/click/send
7. high-risk terminal action requires approval
8. X execution routes through governed social permissions
9. GitHub write routes through scoped GitHub capabilities
10. all execution returns permanent receipts
11. kill switch revokes active HUD execution immediately
12. offline/local mode can answer from approved local knowledge without cloud secrets
13. capture TTL expiry removes stale context
14. provenance distinguishes screen evidence from WikiVault evidence
15. external wiki retrieval remains non-authoritative until reviewed

## Integration Targets

- HERMES Desktop — operator surface
- Intelligence Grid — dispatch/runtime substrate
- Ingest Membrane — screen/external-context validation
- WikiVault — provenance/evidence authority
- Obsidian — durable human-readable knowledge
- gBRAIN — rebuildable derived index
- Quantization Torque — context budgeting/compaction
- 54-T — containment/capability verification
- HERMES Social Surface — governed social execution
- app-specific adapters / computer-use workers — bounded actuators

## Governing Principle

**The HUD may see only what the operator has allowed, reason only over governed context, and do only what its current capability handle permits.**
