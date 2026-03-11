# Communication Diagram: UC-18 Control Listing Visibility — Main Sequence

## Object Layout

```
System Admin --- AdminUI --- AdminCoordinator --- RoomListingLogic --- RoomListing
                                  |--- NotificationService
                                  |--- EmailProxy --- Email Provider
```

## Participants

| Position | Object | Stereotype |
|---|---|---|
| 1 | System Admin | Actor (primary) |
| 2 | AdminUI | `<<user interaction>>` |
| 3 | AdminCoordinator | `<<coordinator>>` |
| 4 | RoomListingLogic | `<<business logic>>` |
| 5 | RoomListing | `<<entity>>` |
| 6 | NotificationService | `<<service>>` |
| 7 | EmailProxy | `<<proxy>>` |
| 8 | Email Provider | Actor (secondary) |

## Messages

| # | From → To | Message |
|---|---|---|
| 1 | System Admin → AdminUI | access listing administration |
| 1.1 | AdminUI → AdminCoordinator | request visible listings |
| 1.2 | AdminCoordinator → RoomListingLogic | get publicly visible listings |
| 1.3 | RoomListingLogic → RoomListing | fetch published listings |
| 1.4 | RoomListingLogic → AdminCoordinator | visible listings |
| 1.5 | AdminCoordinator → AdminUI | listings with info |
| 1.6 | AdminUI → System Admin | display publicly visible listings |
| 2 | System Admin → AdminUI | select listing to review |
| 2.1 | AdminUI → AdminCoordinator | listing selected (listing id) |
| 2.2 | AdminCoordinator → RoomListingLogic | get listing details |
| 2.3 | RoomListingLogic → RoomListing | fetch listing details |
| 2.4 | RoomListingLogic → AdminCoordinator | listing details + control actions |
| 2.5 | AdminCoordinator → AdminUI | listing details + Disable action |
| 2.6 | AdminUI → System Admin | display listing details and control options |
| 3 | System Admin → AdminUI | select Disable action |
| 3.1 | AdminUI → AdminCoordinator | disable listing (listing id) |
| 3.2 | AdminCoordinator → RoomListingLogic | disable listing |
| 3.3 | RoomListingLogic → RoomListing | update visibility to Disabled |
| 3.4 | RoomListingLogic → AdminCoordinator | listing disabled (owner info) |
| 3.5 | AdminCoordinator → NotificationService | compose owner notification (listing disabled, owner info) |
| 3.6 | NotificationService → AdminCoordinator | notification content |
| 3.7 | AdminCoordinator → EmailProxy | send notification (content, owner email) |
| 3.8 | EmailProxy → Email Provider | deliver email |
| 3.9 | Email Provider → EmailProxy | delivery acknowledged |
| 3.10 | EmailProxy → AdminCoordinator | email dispatched |
| 3.11 | AdminCoordinator → AdminUI | listing disabled successfully |
| 3.12 | AdminUI → System Admin | display listing disabled successfully |

Use `/drawio` to generate a visual .drawio file from this blueprint.
