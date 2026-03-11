# Communication Diagram: UC-14 Review Rental Request — Main Sequence (Accept)

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
| 1 | Owner → OwnerUI | access rental request review (room selected) |
| 1.1 | OwnerUI → RequestReviewCoordinator | request list (room id) |
| 1.2 | RequestReviewCoordinator → RentalRequestLogic | get requests for room |
| 1.3 | RentalRequestLogic → RentalRequest | provide rental requests |
| 1.4 | RentalRequestLogic → RequestReviewCoordinator | requests with visible info |
| 1.5 | RequestReviewCoordinator → OwnerUI | request list |
| 1.6 | OwnerUI → Owner | display submitted requests |
| 2 | Owner → OwnerUI | select request to handle |
| 2.1 | OwnerUI → RequestReviewCoordinator | request selected (request id) |
| 2.2 | RequestReviewCoordinator → RentalRequestLogic | get request details |
| 2.3 | RentalRequestLogic → RentalRequest | provide request details |
| 2.4 | RentalRequestLogic → RequestReviewCoordinator | request details + decision options |
| 2.5 | RequestReviewCoordinator → OwnerUI | request details + actions (Accept / Reject / Keep Pending) |
| 2.6 | OwnerUI → Owner | display request details and decision options |
| 3 | Owner → OwnerUI | select decision (Accept) |
| 3.1 | OwnerUI → RequestReviewCoordinator | decision = Accept (request id) |
| 3.2 | RequestReviewCoordinator → RentalRequestLogic | accept rental request |
| 3.3 | RentalRequestLogic → RentalRequest | mark request accepted |
| 3.4 | RentalRequestLogic → RoomListing | lock room |
| 3.5 | RentalRequestLogic → RequestReviewCoordinator | decision recorded (tenant info) |
| 3.6 | RequestReviewCoordinator → NotificationService | compose tenant notification (decision result, tenant info) |
| 3.7 | NotificationService → RequestReviewCoordinator | notification content |
| 3.8 | RequestReviewCoordinator → EmailProxy | send notification (content, tenant email) |
| 3.9 | EmailProxy → Email Provider | send notification |
| 3.10 | Email Provider → EmailProxy | notification sent |
| 3.11 | EmailProxy → RequestReviewCoordinator | email dispatched |
| 3.12 | RequestReviewCoordinator → OwnerUI | decision recorded successfully |
| 3.13 | OwnerUI → Owner | display decision recorded successfully |

## Notes
- Main sequence shows Accept decision path. Reject path follows same structure but omits room lock (step 3.4).
- Room locking (step 3.4) is a mandatory business rule enforced by `RentalRequestLogic`, not a separate UC.

Use `/drawio` to generate a visual .drawio file from this blueprint.
