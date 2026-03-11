# Statechart: OwnerVerification

## States

| State | Type | Entry/Exit Actions |
|---|---|---|
| Submitted | Initial target | — |
| Verified | Final | entry / Enable owner publishing |
| Rejected | Normal | — |

## Transitions

| # | Source State | Event [Condition] / Action | Target State |
|---|---|---|---|
| T1 | Initial | — | Submitted |
| T2 | Submitted | Admin Approves / Mark Verified, Notify Owner | Verified |
| T3 | Submitted | Admin Rejects / Mark Rejected, Notify Owner | Rejected |
| T4 | Rejected | Owner Resubmits / Reset Verification Data | Submitted |

## Communication Diagram Synchronization

| Transition | UC | Comm Diagram Message |
|---|---|---|
| T1 | UC-13 | via `VerificationLogic → OwnerVerification: record verification` |
| T2 | UC-16 | via `VerificationLogic → OwnerVerification: approve verification` |
| T3 | UC-16 | via `VerificationLogic → OwnerVerification: reject verification` |
| T4 | UC-13 | via `VerificationLogic → OwnerVerification: update verification` |

## Notes

- T4 (resubmission after rejection) is implied by business logic but not explicitly documented in any UC. If resubmission is out of scope, remove T4 and Rejected becomes a terminal state.
- Verified is terminal — no transition back (owner cannot un-verify).

Use `/drawio` to generate a visual .drawio file from this blueprint.
