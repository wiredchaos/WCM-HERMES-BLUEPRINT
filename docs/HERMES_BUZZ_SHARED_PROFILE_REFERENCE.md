# Canonical Hermes + Buzz Shared Profile Reference

## Adopted upstream bridge

AGENTROPOLIS recognizes [`r0b0tlab/hermes-buzz-shared-profile`](https://github.com/r0b0tlab/hermes-buzz-shared-profile) as the current reference implementation for exposing an existing Hermes profile as a native managed agent in Buzz Desktop.

The bridge is deliberately narrow:

```text
Hermes profile state
  -> hermes -p <profile> acp
  -> buzz-acp child process
  -> Buzz managed-agent entry
  -> Buzz channel participation
```

## Shared-profile invariant

One Hermes profile directory remains the sole writable owner of:

- identity and configuration
- memory
- skills
- sessions
- `SOUL.md`
- `state.db`

Buzz stores a managed-agent reference and launch configuration. The bridge does not clone, synchronize, merge, or directly edit Hermes profile state.

## Managed-agent contract

```json
{
  "agent_command": "/resolved/path/to/hermes",
  "agent_args": ["-p", "<profile>", "acp"],
  "acp_command": "buzz-acp",
  "slug": "hermes:<profile>",
  "is_builtin": false,
  "is_active": true,
  "respond_to": "owner-only"
}
```

The implementation performs atomic updates to `managed-agents.json`, preserves existing entries, normalizes profile names, resolves the Hermes executable, and can import a bounded system prompt from `SOUL.md`.

## Installation

```bash
hermes skills inspect amanning3390/hermes-buzz-shared-profile/hermes-buzz-shared-profile
hermes skills install amanning3390/hermes-buzz-shared-profile/hermes-buzz-shared-profile

hermes profile create hermes-buzz --description "Shared profile for Buzz"
python3 ${HERMES_SKILL_DIR}/scripts/shared_profile.py buzz-add --profile hermes-buzz
```

Buzz Desktop must be installed and launched at least once. Restart it after adding or removing a profile.

## Implementation versus governance

The upstream bridge solves:

- profile discovery
- Buzz data-directory discovery
- native managed-agent registration
- ACP child-process launch configuration
- add, update, list, and remove lifecycle

It does not solve:

- capability sandboxing
- mandate and job-envelope normalization
- signed approval gates
- secrets brokering
- artifact verification
- receipt generation
- idempotent event processing
- cross-community isolation enforcement outside Buzz
- deployment, publishing, payment, or wallet policy

Those remain AGENTROPOLIS runtime responsibilities.

## Canonical combined architecture

```text
Human Mission Control
  -> signed Buzz mandate
  -> Buzz managed Hermes profile
  -> hermes -p <profile> acp
  -> runtime capability gate
  -> approved MCP, browser, terminal, or file tools
  -> artifact and receipt
  -> Buzz thread review
  -> acceptance, rejection, or approved external action
```

## Threat model note

`respond_to: owner-only` limits who can directly address the agent, but it must not be treated as sufficient authorization for host-level tools. If the authorized owner identity is compromised, ACP execution can become a path to local command execution. Runtime tool allowlists, scoped credentials, filesystem boundaries, approval binding, and revocation remain mandatory.

## Reviewed upstream status

- Skill version: `0.3.0`
- Python: 3.11+
- Platforms: macOS, Linux, Windows 10/11
- License: MIT
