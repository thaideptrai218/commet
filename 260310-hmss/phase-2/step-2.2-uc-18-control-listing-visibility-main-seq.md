# Communication Diagram: UC-18 Control Listing Visibility - Main Sequence

## Object Layout

```text
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

| # | From -> To | Message |
|---|---|---|
| 1 | System Admin -> AdminUI | Listing Administration Access |
| 1.1 | AdminUI -> AdminCoordinator | Visible Listing List Request |
| 1.2 | AdminCoordinator -> RoomListingLogic | Visible Listing List Request |
| 1.3 | RoomListingLogic -> RoomListing | Visible Listing List Request |
| 1.4 | RoomListing -> RoomListingLogic | Visible Listing List |
| 1.5 | RoomListingLogic -> AdminCoordinator | Visible Listing List |
| 1.6 | AdminCoordinator -> AdminUI | Visible Listing List |
| 1.7 | AdminUI -> System Admin | Visible Listing List |
| 2 | System Admin -> AdminUI | Listing Selection |
| 2.1 | AdminUI -> AdminCoordinator | Listing Detail Request |
| 2.2 | AdminCoordinator -> RoomListingLogic | Listing Detail Request |
| 2.3 | RoomListingLogic -> RoomListing | Listing Detail Request |
| 2.4 | RoomListing -> RoomListingLogic | Listing Detail and Disable Action |
| 2.5 | RoomListingLogic -> AdminCoordinator | Listing Detail and Disable Action |
| 2.6 | AdminCoordinator -> AdminUI | Listing Detail and Disable Action |
| 2.7 | AdminUI -> System Admin | Listing Detail and Disable Action |
| 3 | System Admin -> AdminUI | Listing Disable Decision |
| 3.1 | AdminUI -> AdminCoordinator | Listing Disable Request |
| 3.2 | AdminCoordinator -> RoomListingLogic | Listing Disable Request |
| 3.3 | RoomListingLogic -> RoomListing | Listing Visibility Change |
| 3.4 | RoomListing -> RoomListingLogic | Listing Visibility Record |
| 3.5 | RoomListingLogic -> AdminCoordinator | Listing Disable Result |
| 3.6 | AdminCoordinator -> NotificationService | Owner Notification Request |
| 3.7 | NotificationService -> AdminCoordinator | Owner Notification |
| 3.8 | AdminCoordinator -> EmailProxy | Owner Notification |
| 3.9 | EmailProxy -> Email Provider | Owner Notification |
| 3.10 | Email Provider -> EmailProxy | Notification Delivery Result |
| 3.11 | EmailProxy -> AdminCoordinator | Notification Delivery Result |
| 3.12 | AdminCoordinator -> AdminUI | Listing Disable Outcome |
| 3.13 | AdminUI -> System Admin | Listing Disable Confirmation |

## Notes
- Main sequence shows the admin disable path for a publicly visible listing.
- The result of the action is that the listing is no longer publicly visible in search.
- Messages are kept at analysis level and avoid method-style naming.
