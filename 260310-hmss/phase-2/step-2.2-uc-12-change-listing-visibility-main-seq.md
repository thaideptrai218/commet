# Communication Diagram: UC-12 Change Listing Visibility — Main Sequence

## Object Layout

```
Owner --- OwnerUI --- ListingManagementCoordinator --- RoomListingLogic --- RoomListing
```

## Participants

| Position | Object | Stereotype |
|---|---|---|
| 1 | Owner | Actor (primary) |
| 2 | OwnerUI | `<<user interaction>>` |
| 3 | ListingManagementCoordinator | `<<coordinator>>` |
| 4 | RoomListingLogic | `<<business logic>>` |
| 5 | RoomListing | `<<entity>>` |

## Messages

| # | From → To | Message |
|---|---|---|
| 1 | Owner → OwnerUI | access listing management, select published listing |
| 1.1 | OwnerUI → ListingManagementCoordinator | listing selected (listing id) |
| 1.2 | ListingManagementCoordinator → RoomListingLogic | get listing status + available visibility actions |
| 1.3 | RoomListingLogic → RoomListing | fetch listing data |
| 1.4 | RoomListingLogic → ListingManagementCoordinator | listing status + available actions |
| 1.5 | ListingManagementCoordinator → OwnerUI | listing status + visibility actions (Hide / Archive) |
| 1.6 | OwnerUI → Owner | display listing status and visibility options |
| 2 | Owner → OwnerUI | select visibility action (Hide or Archive) |
| 2.1 | OwnerUI → ListingManagementCoordinator | visibility action (Hide / Archive) |
| 2.2 | ListingManagementCoordinator → RoomListingLogic | validate and apply visibility change |
| 2.3 | RoomListingLogic → RoomListing | check current status (action valid?) |
| 2.4 | RoomListing → RoomListingLogic | current status = Published Available (valid) |
| 2.5 | RoomListingLogic → RoomListing | update status to Hidden or Archived |
| 2.6 | RoomListingLogic → ListingManagementCoordinator | visibility changed |
| 2.7 | ListingManagementCoordinator → OwnerUI | visibility changed successfully |
| 2.8 | OwnerUI → Owner | display listing visibility changed successfully |

Use `/drawio` to generate a visual .drawio file from this blueprint.
