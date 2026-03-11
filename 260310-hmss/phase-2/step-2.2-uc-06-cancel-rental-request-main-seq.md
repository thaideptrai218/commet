# Communication Diagram: UC-06 Cancel Rental Request - Main Sequence

## Object Layout

```text
Tenant --- RentalRequestUI --- RentalRequestCoordinator --- RentalRequestRules --- RentalRequest
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
| 5        | RentalRequest            | `<<entity>>`           |
| 6        | NotificationService      | `<<service>>`          |
| 7        | EmailProxy               | `<<proxy>>`            |
| 8        | Email Provider           | Actor (secondary)      |

## Messages

| #   | From -> To                                     | Message                        |
| --- | ---------------------------------------------- | ------------------------------ |
| 1   | Tenant -> RentalRequestUI                      | Request Management Access      |
| 1.1 | RentalRequestUI -> RentalRequestCoordinator    | Rental Request List Request    |
| 1.2 | RentalRequestCoordinator -> RentalRequestRules | Rental Request List Request    |
| 1.3 | RentalRequestRules -> RentalRequest            | Rental Request List Request    |
| 1.4 | RentalRequest -> RentalRequestRules            | Rental Request List            |
| 1.5 | RentalRequestRules -> RentalRequestCoordinator | Rental Request List            |
| 1.6 | RentalRequestCoordinator -> RentalRequestUI    | Rental Request List            |
| 1.7 | RentalRequestUI -> Tenant                      | Rental Request List            |
| 2   | Tenant -> RentalRequestUI                      | Cancellation Selection         |
| 2.1 | RentalRequestUI -> Tenant                      | Cancellation Confirmation      |
| 3   | Tenant -> RentalRequestUI                      | Cancellation Confirmation      |
| 3.1 | RentalRequestUI -> RentalRequestCoordinator    | Cancellation Request           |
| 3.2 | RentalRequestCoordinator -> RentalRequestRules | Cancellation Request           |
| 3.3 | RentalRequestRules -> RentalRequest            | Cancellation Eligibility Check |
| 3.4 | RentalRequest -> RentalRequestRules            | Cancellation Eligibility Result |
| 3.5 | RentalRequestRules -> RentalRequest            | Cancellation Record            |
| 3.6 | RentalRequest -> RentalRequestRules            | Cancellation Record            |
| 3.7 | RentalRequestRules -> RentalRequestCoordinator | Cancellation Result            |
| 3.8 | RentalRequestCoordinator -> NotificationService | Owner Notification Request    |
| 3.9 | NotificationService -> RentalRequestCoordinator | Owner Notification            |
| 3.10 | RentalRequestCoordinator -> EmailProxy        | Owner Notification             |
| 3.11 | EmailProxy -> Email Provider                  | Owner Notification             |
| 3.12 | Email Provider -> EmailProxy                  | Notification Delivery Result   |
| 3.13 | EmailProxy -> RentalRequestCoordinator        | Notification Delivery Result   |
| 3.14 | RentalRequestCoordinator -> RentalRequestUI   | Cancellation Outcome           |
| 3.15 | RentalRequestUI -> Tenant                     | Cancellation Confirmation      |

## Notes

- `NotificationService` prepares notification content only.
- `RentalRequestCoordinator` is responsible for external email dispatch through `EmailProxy`.
- Messages are kept at analysis level and avoid method-style naming.

Use `/drawio` to generate a visual `.drawio` file from this blueprint.
