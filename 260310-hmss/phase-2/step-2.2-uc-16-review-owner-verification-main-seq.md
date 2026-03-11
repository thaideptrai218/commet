# Communication Diagram: UC-16 Review Owner Verification — Main Sequence (Approve)

## Object Layout

```
System Admin --- AdminUI --- AdminCoordinator --- VerificationLogic --- OwnerVerification
                                  |--- CloudStorageProxy --- Cloud Storage
                                  |--- NotificationService
                                  |--- EmailProxy --- Email Provider
```

## Participants

| Position | Object | Stereotype |
|---|---|---|
| 1 | System Admin | Actor (primary) |
| 2 | AdminUI | `<<user interaction>>` |
| 3 | AdminCoordinator | `<<coordinator>>` |
| 4 | VerificationLogic | `<<business logic>>` |
| 5 | OwnerVerification | `<<entity>>` |
| 6 | CloudStorageProxy | `<<proxy>>` |
| 7 | Cloud Storage | Actor (secondary) |
| 8 | NotificationService | `<<service>>` |
| 9 | EmailProxy | `<<proxy>>` |
| 10 | Email Provider | Actor (secondary) |

## Messages

| # | From → To | Message |
|---|---|---|
| 1 | System Admin → AdminUI | access verification review |
| 1.1 | AdminUI → AdminCoordinator | request pending verifications |
| 1.2 | AdminCoordinator → VerificationLogic | get pending submissions |
| 1.3 | VerificationLogic → OwnerVerification | provide pending submissions |
| 1.4 | VerificationLogic → AdminCoordinator | pending submissions list |
| 1.5 | AdminCoordinator → AdminUI | pending submissions |
| 1.6 | AdminUI → System Admin | display pending verification submissions |
| 2 | System Admin → AdminUI | select submission to review |
| 2.1 | AdminUI → AdminCoordinator | submission selected (submission id) |
| 2.2 | AdminCoordinator → VerificationLogic | get submission details |
| 2.3 | VerificationLogic → OwnerVerification | provide submission + document refs |
| 2.4 | VerificationLogic → AdminCoordinator | submission details + document refs |
| 2.5 | AdminCoordinator → CloudStorageProxy | retrieve supporting documents |
| 2.6 | CloudStorageProxy → Cloud Storage | request documents |
| 2.7 | Cloud Storage → CloudStorageProxy | documents |
| 2.8 | CloudStorageProxy → AdminCoordinator | documents ready |
| 2.9 | AdminCoordinator → AdminUI | submission details + documents |
| 2.10 | AdminUI → System Admin | display owner info and supporting documents |
| 3 | System Admin → AdminUI | select decision (Approve) |
| 3.1 | AdminUI → AdminCoordinator | decision = Approve (submission id) |
| 3.2 | AdminCoordinator → VerificationLogic | record decision (Approve) |
| 3.3 | VerificationLogic → OwnerVerification | mark owner verified |
| 3.4 | VerificationLogic → AdminCoordinator | decision recorded (owner info) |
| 3.5 | AdminCoordinator → NotificationService | compose owner notification (verification result, owner info) |
| 3.6 | NotificationService → AdminCoordinator | notification content |
| 3.7 | AdminCoordinator → EmailProxy | send notification (content, owner email) |
| 3.8 | EmailProxy → Email Provider | send notification |
| 3.9 | Email Provider → EmailProxy | notification sent |
| 3.10 | EmailProxy → AdminCoordinator | email dispatched |
| 3.11 | AdminCoordinator → AdminUI | review completed |
| 3.12 | AdminUI → System Admin | display review completed successfully |

## Notes
- Main sequence shows Approve path. Reject path follows same structure; OwnerVerification status set to Rejected instead.

Use `/drawio` to generate a visual .drawio file from this blueprint.
