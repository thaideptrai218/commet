# Communication Diagram: UC-04 Sign In - Main Sequence

## Object Layout

```text
Registered User --- SignInUI --- SignInCoordinator --- AuthenticationService --- UserAccount
```

## Participants

| Position | Object                | Stereotype             |
| -------- | --------------------- | ---------------------- |
| 1        | Registered User       | Actor (primary)        |
| 2        | SignInUI              | `<<user interaction>>` |
| 3        | SignInCoordinator     | `<<coordinator>>`      |
| 4        | AuthenticationService | `<<service>>`          |
| 5        | UserAccount           | `<<entity>>`           |

## Messages

| #   | From -> To                                  | Message                     |
| --- | ------------------------------------------- | --------------------------- |
| 1   | Registered User -> SignInUI                 | Sign-In Access              |
| 1.1 | SignInUI -> SignInCoordinator               | Sign-In Request             |
| 1.2 | SignInCoordinator -> SignInUI               | Sign-In Form                |
| 1.3 | SignInUI -> Registered User                 | Sign-In Form                |
| 2   | Registered User -> SignInUI                 | Sign-In Credentials         |
| 2.1 | SignInUI -> SignInCoordinator               | Sign-In Request             |
| 2.2 | SignInCoordinator -> AuthenticationService  | Sign-In Credentials         |
| 2.3 | AuthenticationService -> UserAccount        | Account Information Request |
| 2.4 | UserAccount -> AuthenticationService        | Account Information         |
| 2.5 | AuthenticationService -> SignInCoordinator  | Authentication Result       |
| 2.6 | SignInCoordinator -> SignInUI               | Sign-In Outcome             |
| 2.7 | SignInUI -> Registered User                 | Sign-In Confirmation        |

Use `/drawio` to generate a visual `.drawio` file from this blueprint.
