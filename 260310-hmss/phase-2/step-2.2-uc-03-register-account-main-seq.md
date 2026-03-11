# Communication Diagram: UC-03 Register Account - Main Sequence

## Object Layout

```text
Visitor --- RegistrationUI --- RegistrationCoordinator --- AccountRegistrationRules --- UserAccount
```

## Participants

| Position | Object                   | Stereotype             |
| -------- | ------------------------ | ---------------------- |
| 1        | Visitor                  | Actor (primary)        |
| 2        | RegistrationUI           | `<<user interaction>>` |
| 3        | RegistrationCoordinator  | `<<coordinator>>`      |
| 4        | AccountRegistrationRules | `<<business logic>>`   |
| 5        | UserAccount              | `<<entity>>`           |

## Messages
    
| #   | From -> To                                         | Message                  |
| --- | -------------------------------------------------- | ------------------------ |
| 1   | Visitor -> RegistrationUI                          | Registration Access      |
| 1.1 | RegistrationUI -> RegistrationCoordinator          | Registration Request     |
| 1.2 | RegistrationCoordinator -> RegistrationUI          | Registration Form        |
| 1.3 | RegistrationUI -> Visitor                          | Registration Form        |
| 2   | Visitor -> RegistrationUI                          | Registration Information |
| 2.1 | RegistrationUI -> Visitor                          | Registration Review      |
| 3   | Visitor -> RegistrationUI                          | Registration Confirmation |
| 3.1 | RegistrationUI -> RegistrationCoordinator          | Registration Request     |
| 3.2 | RegistrationCoordinator -> AccountRegistrationRules | Registration Information |
| 3.3 | AccountRegistrationRules -> RegistrationCoordinator | Registration Assessment  |
| 3.4 | RegistrationCoordinator -> UserAccount             | Account Information      |
| 3.5 | UserAccount -> RegistrationCoordinator             | Account Record           |
| 3.6 | RegistrationCoordinator -> RegistrationUI          | Registration Outcome     |
| 3.7 | RegistrationUI -> Visitor                          | Registration Confirmation |

Use `/drawio` to generate a visual `.drawio` file from this blueprint.
