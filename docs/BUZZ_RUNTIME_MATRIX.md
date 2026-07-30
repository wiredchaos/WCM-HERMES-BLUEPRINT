# Canonical Buzz Runtime Matrix

## Upstream inputs

- `r0b0tlab/hermes-buzz-shared-profile`
- `tonbistudio/buzz-skills`
- merged `block/buzz#3225`

## Runtime matrix

| Route | Best use | State owner | Required proof |
|---|---|---|---|
| Native Hermes gateway | persistent remote Hermes, skills, memory, cron, messaging | Hermes profile and gateway host | live inbound and outbound Buzz exchange |
| Shared-profile Hermes ACP | Buzz-owned interactive session using an existing Hermes profile | Buzz session plus selected Hermes profile | successful ACP launch and linked profile state |
| Built-in ACP preset | approved coding or specialist harness | Buzz managed-agent runtime | runtime discovery, bounded job, artifact and receipt |
| Devin preset | approved BYOH coding work through `devin acp` | Buzz ACP session and scoped workspace | changed-file record, tests, artifact, human review |

## Media contract

Native Buzz media delivery must use an accepted relay result as proof. A receipt should include the accepted event ID, source and output hashes, target community and channel, transformations, requester, and approval record.

## Security invariant

```text
Runtime availability != authority
Identity != authority
A successful process start != successful delivery
A model response != a completed artifact
```

All routes require dedicated identities, owner-only defaults where appropriate, secret isolation, runtime capability enforcement, community isolation, explicit approvals for external or destructive actions, and receipt-first completion.

## Selection rule

```text
Need persistent remote Hermes behavior?
  -> native gateway

Need Buzz to host the session while retaining Hermes profile state?
  -> shared-profile ACP

Need an approved specialist coding harness?
  -> built-in ACP preset
  -> Devin when selected and available
```

## Canonical governed loop

```text
IDENTITY
  -> MANDATE
  -> RUNTIME SELECTION
  -> CAPABILITY POLICY
  -> EXECUTION
  -> ARTIFACT
  -> RECEIPT
  -> HUMAN REVIEW
  -> AUDIT
```
