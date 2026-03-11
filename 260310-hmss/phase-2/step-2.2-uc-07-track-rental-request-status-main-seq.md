# Communication Diagram: UC-07 Track Rental Request Status - Main Sequence

## Object Layout

```text
Tenant --- RentalRequestStatusUI --- RentalRequestCoordinator --- RentalRequestStatusRules --- RentalRequest
```

## Participants

| Position | Object                   | Stereotype             |
| -------- | ------------------------ | ---------------------- |
| 1        | Tenant                   | Actor (primary)        |
| 2        | RentalRequestStatusUI    | `<<user interaction>>` |
| 3        | RentalRequestCoordinator | `<<coordinator>>`      |
| 4        | RentalRequestStatusRules | `<<business logic>>`   |
| 5        | RentalRequest            | `<<entity>>`           |

## Messages

| #   | From -> To                                      | Message                           |
| --- | ----------------------------------------------- | --------------------------------- |
| 1   | Tenant -> RentalRequestStatusUI                 | Request Status Access             |
| 1.1 | RentalRequestStatusUI -> RentalRequestCoordinator | Rental Request Status Request   |
| 1.2 | RentalRequestCoordinator -> RentalRequestStatusRules | Rental Request Status Request |
| 1.3 | RentalRequestStatusRules -> RentalRequest       | Rental Request Status List Request |
| 1.4 | RentalRequest -> RentalRequestStatusRules       | Rental Request Status List        |
| 1.5 | RentalRequestStatusRules -> RentalRequestCoordinator | Rental Request Status List    |
| 1.6 | RentalRequestCoordinator -> RentalRequestStatusUI | Rental Request Status List     |
| 1.7 | RentalRequestStatusUI -> Tenant                 | Rental Request Status List        |
| 2   | Tenant -> RentalRequestStatusUI                 | Status Detail Selection           |
| 2.1 | RentalRequestStatusUI -> RentalRequestCoordinator | Status Detail Request          |
| 2.2 | RentalRequestCoordinator -> RentalRequestStatusRules | Status Detail Request         |
| 2.3 | RentalRequestStatusRules -> RentalRequest       | Status Detail Request             |
| 2.4 | RentalRequest -> RentalRequestStatusRules       | Status Detail                     |
| 2.5 | RentalRequestStatusRules -> RentalRequestCoordinator | Status Detail and Available Actions |
| 2.6 | RentalRequestCoordinator -> RentalRequestStatusUI | Status Detail and Available Actions |
| 2.7 | RentalRequestStatusUI -> Tenant                 | Status Detail and Available Actions |

Use `/drawio` to generate a visual `.drawio` file from this blueprint.
