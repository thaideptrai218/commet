# Communication Diagram: UC-08b Update Property - Main Sequence

## Object Layout

```text
Owner --- PropertyManagementUI --- PropertyCoordinator --- Property
```

## Participants

| Position | Object               | Stereotype             |
| -------- | -------------------- | ---------------------- |
| 1        | Owner                | Actor (primary)        |
| 2        | PropertyManagementUI | `<<user interaction>>` |
| 3        | PropertyCoordinator  | `<<coordinator>>`      |
| 4        | Property             | `<<entity>>`           |

## Messages

| #   | From -> To                                 | Message                        |
| --- | ------------------------------------------ | ------------------------------ |
| 1   | Owner -> PropertyManagementUI              | Property Management Access     |
| 1.1 | PropertyManagementUI -> PropertyCoordinator | Property List Request         |
| 1.2 | PropertyCoordinator -> Property            | Property List Request          |
| 1.3 | Property -> PropertyCoordinator            | Property List                  |
| 1.4 | PropertyCoordinator -> PropertyManagementUI | Property List                |
| 1.5 | PropertyManagementUI -> Owner              | Property List                  |
| 2   | Owner -> PropertyManagementUI              | Property Update Selection      |
| 2.1 | PropertyManagementUI -> PropertyCoordinator | Property Detail Request       |
| 2.2 | PropertyCoordinator -> Property            | Property Detail Request        |
| 2.3 | Property -> PropertyCoordinator            | Property Detail                |
| 2.4 | PropertyCoordinator -> PropertyManagementUI | Property Update Form         |
| 2.5 | PropertyManagementUI -> Owner              | Property Update Form           |
| 3   | Owner -> PropertyManagementUI              | Updated Property Information   |
| 3.1 | PropertyManagementUI -> Owner              | Property Review                |
| 4   | Owner -> PropertyManagementUI              | Property Update Confirmation   |
| 4.1 | PropertyManagementUI -> PropertyCoordinator | Property Update Request       |
| 4.2 | PropertyCoordinator -> Property            | Updated Property Information   |
| 4.3 | Property -> PropertyCoordinator            | Property Record                |
| 4.4 | PropertyCoordinator -> PropertyManagementUI | Property Update Outcome       |
| 4.5 | PropertyManagementUI -> Owner              | Property Update Confirmation   |

## Notes

- No separate application-logic object is required here because the use case mainly coordinates selection, editing, and recording of property information.
- Messages are kept at analysis level and avoid method-style naming.

Use `/drawio` to generate a visual `.drawio` file from this blueprint.
