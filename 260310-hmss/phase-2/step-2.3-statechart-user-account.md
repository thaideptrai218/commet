# Statechart: User (accountStatus)

## States

| State | Type | Entry/Exit Actions |
|---|---|---|
| Active | Initial target | entry / Grant role-based access |
| Suspended | Normal | entry / Restrict protected functions |
| Disabled | Final | entry / Revoke all access |

## Transitions

| # | Source State | Event [Condition] / Action | Target State |
|---|---|---|---|
| T1 | Initial | — | Active |
| T2 | Active | Admin Suspends / Restrict Access, Notify User | Suspended |
| T3 | Suspended | Admin Enables / Restore Access, Notify User | Active |
| T4 | Suspended | Admin Disables / Revoke Access, Notify User | Disabled |

## Communication Diagram Synchronization

| Transition | UC | Comm Diagram Message |
|---|---|---|
| T1 | UC-03 | via `AuthenticationLogic → User: create account` |
| T2/T3/T4 | UC-17 | via `UserManagementLogic → User: update account status` |

## Notes

- Pattern: Active ↔ Suspended → Disabled (matches static model `UserManagementLogic` policy).
- Direct Active → Disabled is NOT permitted — admin must suspend first.
- Disabled is terminal — no recovery path in current scope.

Use `/drawio` to generate a visual .drawio file from this blueprint.
