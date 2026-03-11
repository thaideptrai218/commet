# Communication Diagram: UC-08a Create Property - Main Sequence

## Object Layout

```text
Owner --- PropertyCreationUI --- PropertyCoordinator --- Property
```

## Participants

| Position | Object             | Stereotype             |
| -------- | ------------------ | ---------------------- |
| 1        | Owner              | Actor (primary)        |
| 2        | PropertyCreationUI | `<<user interaction>>` |
| 3        | PropertyCoordinator | `<<coordinator>>`     |
| 4        | Property           | `<<entity>>`           |

## Messages

| #   | From -> To                               | Message                       |
| --- | ---------------------------------------- | ----------------------------- |
| 1   | Owner -> PropertyCreationUI              | Property Creation Access      |
| 1.1 | PropertyCreationUI -> PropertyCoordinator | Property Creation Request    |
| 1.2 | PropertyCoordinator -> PropertyCreationUI | Property Creation Form       |
| 1.3 | PropertyCreationUI -> Owner              | Property Creation Form        |
| 2   | Owner -> PropertyCreationUI              | Property Information          |
| 2.1 | PropertyCreationUI -> Owner              | Property Review               |
| 3   | Owner -> PropertyCreationUI              | Property Creation Confirmation |
| 3.1 | PropertyCreationUI -> PropertyCoordinator | Property Creation Request    |
| 3.2 | PropertyCoordinator -> Property          | Property Information          |
| 3.3 | Property -> PropertyCoordinator          | Property Record               |
| 3.4 | PropertyCoordinator -> PropertyCreationUI | Property Creation Outcome    |
| 3.5 | PropertyCreationUI -> Owner              | Property Creation Confirmation |

## Notes

- No separate application-logic object is required here because the use case mainly coordinates entry and recording of property information.
- Messages are kept at analysis level and avoid method-style naming.

Use `/drawio` to generate a visual `.drawio` file from this blueprint.
