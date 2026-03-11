# Communication Diagram: UC-13 Submit Owner Verification — Main Sequence

## Object Layout

```
Owner --- OwnerUI --- VerificationCoordinator --- VerificationLogic --- OwnerVerification
                                  |--- CloudStorageProxy --- Cloud Storage
```

## Participants

| Position | Object | Stereotype |
|---|---|---|
| 1 | Owner | Actor (primary) |
| 2 | OwnerUI | `<<user interaction>>` |
| 3 | VerificationCoordinator | `<<coordinator>>` |
| 4 | VerificationLogic | `<<business logic>>` |
| 5 | OwnerVerification | `<<entity>>` |
| 6 | CloudStorageProxy | `<<proxy>>` |
| 7 | Cloud Storage | Actor (secondary) |

## Messages

| # | From → To | Message |
|---|---|---|
| 1 | Owner → OwnerUI | access verification submission |
| 1.1 | OwnerUI → VerificationCoordinator | request verification form |
| 1.2 | VerificationCoordinator → VerificationLogic | get verification requirements |
| 1.3 | VerificationLogic → VerificationCoordinator | verification form requirements |
| 1.4 | VerificationCoordinator → OwnerUI | verification form |
| 1.5 | OwnerUI → Owner | display verification form and document requirements |
| 2 | Owner → OwnerUI | personal info + supporting documents |
| 2.1 | OwnerUI → VerificationCoordinator | personal info + documents |
| 2.2 | VerificationCoordinator → CloudStorageProxy | upload identification documents |
| 2.3 | CloudStorageProxy → Cloud Storage | store documents |
| 2.4 | Cloud Storage → CloudStorageProxy | documents stored (document refs) |
| 2.5 | CloudStorageProxy → VerificationCoordinator | document refs |
| 2.6 | VerificationCoordinator → VerificationLogic | validate and record submission (info + doc refs) |
| 2.7 | VerificationLogic → OwnerVerification | create submission (status = Pending Review) |
| 2.8 | VerificationLogic → VerificationCoordinator | submission recorded |
| 2.9 | VerificationCoordinator → OwnerUI | submission received and pending review |
| 2.10 | OwnerUI → Owner | display submission received, awaiting admin review |

Use `/drawio` to generate a visual .drawio file from this blueprint.
