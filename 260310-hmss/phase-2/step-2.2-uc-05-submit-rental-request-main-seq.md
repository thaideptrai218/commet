# Communication Diagram: UC-05 Submit Rental Request - Main Sequence

## Object Layout

```text
Tenant --- RentalRequestUI --- RentalRequestCoordinator --- RentalRequestRules --- RoomListing
                                      |                         |
                                      |                         --- RentalRequest
                                      |
                                      --- NotificationService
                                      --- EmailProxy --- Email Provider
```

## Participants

| Position | Object                   | Stereotype             |
| -------- | ------------------------ | ---------------------- |
| 1        | Tenant                   | Actor (primary)        |
| 2        | RentalRequestUI          | `<<user interaction>>` |
| 3        | RentalRequestCoordinator | `<<coordinator>>`      |
| 4        | RentalRequestRules       | `<<business logic>>`   |
| 5        | RoomListing              | `<<entity>>`           |
| 6        | RentalRequest            | `<<entity>>`           |
| 7        | NotificationService      | `<<service>>`          |
| 8        | EmailProxy               | `<<proxy>>`            |
| 9        | Email Provider           | Actor (secondary)      |

## Messages

| #   | From -> To                                     | Message                    |
| --- | ---------------------------------------------- | -------------------------- |
| 1   | Tenant -> RentalRequestUI                      | Rental Request Access      |
| 1.1 | RentalRequestUI -> RentalRequestCoordinator    | Rental Request Form Request |
| 1.2 | RentalRequestCoordinator -> RentalRequestRules | Listing Information Request |
| 1.3 | RentalRequestRules -> RoomListing              | Listing Information Request |
| 1.4 | RoomListing -> RentalRequestRules              | Listing Information        |
| 1.5 | RentalRequestRules -> RentalRequestCoordinator | Listing Information        |
| 1.6 | RentalRequestCoordinator -> RentalRequestUI    | Rental Request Form        |
| 1.7 | RentalRequestUI -> Tenant                      | Rental Request Form        |
| 2   | Tenant -> RentalRequestUI                      | Rental Request Information |
| 2.1 | RentalRequestUI -> Tenant                      | Rental Request Review      |
| 3   | Tenant -> RentalRequestUI                      | Rental Request Confirmation |
| 3.1 | RentalRequestUI -> RentalRequestCoordinator    | Rental Request Submission  |
| 3.2 | RentalRequestCoordinator -> RentalRequestRules | Rental Request Information |
| 3.3 | RentalRequestRules -> RoomListing              | Requestability Check       |
| 3.4 | RoomListing -> RentalRequestRules              | Requestability Result      |
| 3.5 | RentalRequestRules -> RentalRequest            | Rental Request Record      |
| 3.6 | RentalRequest -> RentalRequestRules            | Rental Request Record      |
| 3.7 | RentalRequestRules -> RentalRequestCoordinator | Submission Result          |
| 3.8 | RentalRequestCoordinator -> NotificationService | Owner Notification Request |
| 3.9 | NotificationService -> RentalRequestCoordinator | Owner Notification        |
| 3.10 | RentalRequestCoordinator -> EmailProxy        | Owner Notification         |
| 3.11 | EmailProxy -> Email Provider                  | Owner Notification         |
| 3.12 | Email Provider -> EmailProxy                  | Notification Delivery Result |
| 3.13 | EmailProxy -> RentalRequestCoordinator        | Notification Delivery Result |
| 3.14 | RentalRequestCoordinator -> RentalRequestUI   | Rental Request Outcome     |
| 3.15 | RentalRequestUI -> Tenant                     | Rental Request Confirmation |

## Notes

- `NotificationService` prepares notification content only.
- `RentalRequestCoordinator` remains responsible for the external email dispatch through `EmailProxy`.
- Messages are kept at analysis level and avoid method-style naming.

Use `/drawio` to generate a visual `.drawio` file from this blueprint.
