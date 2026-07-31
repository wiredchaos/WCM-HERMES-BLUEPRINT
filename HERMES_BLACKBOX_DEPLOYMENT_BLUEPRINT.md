# Hermes Blackbox Deployment Blueprint

**Upstream:** `asimons81/hermes-blackbox`  
**Pilot version:** `0.1.0`  
**Runtime:** Python 3.11+  
**Mode:** local-first, standalone, controlled pilot

## Install

```bash
git clone https://github.com/asimons81/hermes-blackbox.git
cd hermes-blackbox
python -m pip install -e ".[dev]"
pytest -q
```

## Pilot smoke test

```bash
hermes-blackbox capture --fixture fixtures/demo_session.json -o /tmp/demo.blackbox.json
hermes-blackbox verify --record /tmp/demo.blackbox.json
hermes-blackbox report --record /tmp/demo.blackbox.json -o /tmp/demo.blackbox.md
```

## Live capture

```bash
hermes-blackbox capture --latest -o /tmp/latest.blackbox.json
hermes-blackbox verify --record /tmp/latest.blackbox.json
```

Redaction must remain enabled. Do not use `--no-redact` for exported or shared records.

## Governance boundary

The `prove` command in v0.1 is a heuristic evidence finder. Its output is advisory and must not automatically close tasks, promote deployments, authorize payment, change permissions, or update verified reputation.

Route draft receipts through:

```text
Hermes Blackbox
  -> AGENTROPOLIS-AGENT-MCP
  -> AGENTROPOLIS-AEGIS-ASSURANCE
  -> Human Mission Control
  -> AGENTROPOLIS-OPS retention
```

## Production checklist

- Pin a reviewed upstream commit.
- Verify Hermes `state.db` schema compatibility.
- Add deterministic tool-result verification.
- Correlate tool calls and results.
- Require exit codes and artifact hashes.
- Remove absolute paths from shareable records.
- Sign receipt envelopes.
- Pass AEGIS adversarial tests.
- Configure OPS retention and incident alerts.
- Test disable and rollback procedures.
