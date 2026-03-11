# Communication Diagram: UC-17 Manage User Account Status - Main Sequence

## Object Layout

```text
System Admin --- AdminUI --- AdminCoordinator --- UserManagementLogic --- User
                                  |--- NotificationService
                                  |--- EmailProxy --- Email Provider
```

## Participants

| Position | Object | Stereotype |
|---|---|---|
| 1 | System Admin | Actor (primary) |
| 2 | AdminUI | `<<user interaction>>` |
| 3 | AdminCoordinator | `<<coordinator>>` |
| 4 | UserManagementLogic | `<<business logic>>` |
| 5 | User | `<<entity>>` |
| 6 | NotificationService | `<<service>>` |
| 7 | EmailProxy | `<<proxy>>` |
| 8 | Email Provider | Actor (secondary) |

## Messages

| # | From -> To | Message |
|---|---|---|
| 1 | System Admin -> AdminUI | Account Management Access |
| 1.1 | AdminUI -> AdminCoordinator | User Account List Request |
| 1.2 | AdminCoordinator -> UserManagementLogic | User Account List Request |
| 1.3 | UserManagementLogic -> User | User Account List Request |
| 1.4 | User -> UserManagementLogic | User Account List |
| 1.5 | UserManagementLogic -> AdminCoordinator | User Account List |
| 1.6 | AdminCoordinator -> AdminUI | User Account List |
| 1.7 | AdminUI -> System Admin | User Account List |
| 2 | System Admin -> AdminUI | User Account Selection |
| 2.1 | AdminUI -> AdminCoordinator | User Account Detail Request |
| 2.2 | AdminCoordinator -> UserManagementLogic | User Account Detail Request |
| 2.3 | UserManagementLogic -> User | User Account Detail Request |
| 2.4 | User -> UserManagementLogic | User Account Detail and Available Status Actions |
| 2.5 | UserManagementLogic -> AdminCoordinator | User Account Detail and Available Status Actions |
| 2.6 | AdminCoordinator -> AdminUI | User Account Detail and Available Status Actions |
| 2.7 | AdminUI -> System Admin | User Account Detail and Available Status Actions |
| 3 | System Admin -> AdminUI | Account Status Change Decision |
| 3.1 | AdminUI -> AdminCoordinator | Account Status Change Request |
| 3.2 | AdminCoordinator -> UserManagementLogic | Account Status Change Request |
| 3.3 | UserManagementLogic -> User | Account Status Transition |
| 3.4 | User -> UserManagementLogic | Account Status Record |
| 3.5 | UserManagementLogic -> AdminCoordinator | Account Status Change Result |
| 3.6 | AdminCoordinator -> NotificationService | User Notification Request |
| 3.7 | NotificationService -> AdminCoordinator | User Notification |
| 3.8 | AdminCoordinator -> EmailProxy | User Notification |
| 3.9 | EmailProxy -> Email Provider | User Notification |
| 3.10 | Email Provider -> EmailProxy | Notification Delivery Result |
| 3.11 | EmailProxy -> AdminCoordinator | Notification Delivery Result |
| 3.12 | AdminCoordinator -> AdminUI | Account Status Change Outcome |
| 3.13 | AdminUI -> System Admin | Account Status Change Confirmation |

## Notes
- Main sequence shows one permitted status change path. The same structure applies to Enable, Suspend, or Disable when the selected account status allows that transition.
- Disabled accounts have no outgoing transition in the current scope, so the system presents no further status-management action for them.
- Messages are kept at analysis level and avoid method-style naming.
