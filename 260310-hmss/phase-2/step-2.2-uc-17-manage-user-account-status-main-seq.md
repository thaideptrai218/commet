# Communication Diagram: UC-17 Manage User Account Status — Main Sequence

## Object Layout

```
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

| # | From → To | Message |
|---|---|---|
| 1 | System Admin → AdminUI | access user account administration |
| 1.1 | AdminUI → AdminCoordinator | request user list |
| 1.2 | AdminCoordinator → UserManagementLogic | get user accounts |
| 1.3 | UserManagementLogic → User | fetch user accounts |
| 1.4 | UserManagementLogic → AdminCoordinator | user accounts list |
| 1.5 | AdminCoordinator → AdminUI | user accounts + available actions |
| 1.6 | AdminUI → System Admin | display user accounts |
| 2 | System Admin → AdminUI | select user account |
| 2.1 | AdminUI → AdminCoordinator | user selected (user id) |
| 2.2 | AdminCoordinator → UserManagementLogic | get account details |
| 2.3 | UserManagementLogic → User | fetch account info |
| 2.4 | UserManagementLogic → AdminCoordinator | account info + current status + available actions |
| 2.5 | AdminCoordinator → AdminUI | account info + status actions (Enable / Suspend / Disable) |
| 2.6 | AdminUI → System Admin | display account info and status actions |
| 3 | System Admin → AdminUI | select status action (e.g., Suspend) |
| 3.1 | AdminUI → AdminCoordinator | status action (Suspend, user id) |
| 3.2 | AdminCoordinator → UserManagementLogic | validate and apply status change |
| 3.3 | UserManagementLogic → User | check current status (action permitted?) |
| 3.4 | User → UserManagementLogic | current status (valid transition) |
| 3.5 | UserManagementLogic → User | update account status to Suspended |
| 3.6 | UserManagementLogic → AdminCoordinator | status updated (user info) |
| 3.7 | AdminCoordinator → NotificationService | compose user notification (status change event, user info) |
| 3.8 | NotificationService → AdminCoordinator | notification content |
| 3.9 | AdminCoordinator → EmailProxy | send notification (content, user email) |
| 3.10 | EmailProxy → Email Provider | deliver email |
| 3.11 | Email Provider → EmailProxy | delivery acknowledged |
| 3.12 | EmailProxy → AdminCoordinator | email dispatched |
| 3.13 | AdminCoordinator → AdminUI | account status updated successfully |
| 3.14 | AdminUI → System Admin | display account-management action applied |

## Notes
- Main sequence shows Suspend action. Enable and Disable follow the same structure with different target status.

Use `/drawio` to generate a visual .drawio file from this blueprint.
