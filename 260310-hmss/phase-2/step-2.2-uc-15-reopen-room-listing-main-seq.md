# Communication Diagram: UC-15 Reopen Room Listing — Main Sequence

## Object Layout

```
Owner --- OwnerUI --- RequestReviewCoordinator --- RentalRequestLogic --- RentalRequest
                                  |                                     \-- RoomListing
                                  |--- NotificationService
                                  |--- EmailProxy --- Email Provider
```

## Participants

| Position | Object | Stereotype |
|---|---|---|
| 1 | Owner | Actor (primary) |
| 2 | OwnerUI | `<<user interaction>>` |
| 3 | RequestReviewCoordinator | `<<coordinator>>` |
| 4 | RentalRequestLogic | `<<business logic>>` |
| 5 | RentalRequest | `<<entity>>` |
| 6 | RoomListing | `<<entity>>` |
| 7 | NotificationService | `<<service>>` |
| 8 | EmailProxy | `<<proxy>>` |
| 9 | Email Provider | Actor (secondary) |

## Messages

| # | From → To | Message |
|---|---|---|
| 1 | Owner → OwnerUI | access accepted arrangement management |
| 1.1 | OwnerUI → RequestReviewCoordinator | request accepted arrangements |
| 1.2 | RequestReviewCoordinator → RentalRequestLogic | get accepted arrangements |
| 1.3 | RentalRequestLogic → RentalRequest | provide accepted requests |
| 1.4 | RentalRequestLogic → RequestReviewCoordinator | accepted arrangements + room info |
| 1.5 | RequestReviewCoordinator → OwnerUI | accepted arrangements |
| 1.6 | OwnerUI → Owner | display accepted arrangements |
| 2 | Owner → OwnerUI | select arrangement to reopen |
| 2.1 | OwnerUI → RequestReviewCoordinator | arrangement selected (request id) |
| 2.2 | RequestReviewCoordinator → RentalRequestLogic | get arrangement details |
| 2.3 | RentalRequestLogic → RentalRequest | provide arrangement details |
| 2.4 | RentalRequestLogic → RequestReviewCoordinator | arrangement details + reopen consequence |
| 2.5 | RequestReviewCoordinator → OwnerUI | arrangement details + reopen action |
| 2.6 | OwnerUI → Owner | display arrangement details and business consequence |
| 3 | Owner → OwnerUI | confirm reopen (offline arrangement failed) |
| 3.1 | OwnerUI → RequestReviewCoordinator | confirm reopen |
| 3.2 | RequestReviewCoordinator → RentalRequestLogic | reopen room |
| 3.3 | RentalRequestLogic → RentalRequest | revoke rental request |
| 3.4 | RentalRequestLogic → RoomListing | reopen room |
| 3.5 | RentalRequestLogic → RequestReviewCoordinator | room reopened (tenant info) |
| 3.6 | RequestReviewCoordinator → NotificationService | compose tenant notification (revocation event, tenant info) |
| 3.7 | NotificationService → RequestReviewCoordinator | notification content |
| 3.8 | RequestReviewCoordinator → EmailProxy | send notification (content, tenant email) |
| 3.9 | EmailProxy → Email Provider | send notification |
| 3.10 | Email Provider → EmailProxy | notification sent |
| 3.11 | EmailProxy → RequestReviewCoordinator | email dispatched |
| 3.12 | RequestReviewCoordinator → OwnerUI | room reopened successfully |
| 3.13 | OwnerUI → Owner | display room listing reopened successfully |

Use `/drawio` to generate a visual .drawio file from this blueprint.
