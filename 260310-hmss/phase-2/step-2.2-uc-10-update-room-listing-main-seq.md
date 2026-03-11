# Communication Diagram: UC-10 Update Room Listing — Main Sequence

## Object Layout

```
Owner --- OwnerUI --- ListingManagementCoordinator --- RoomListingLogic --- RoomListing
                                  |--- CloudStorageProxy --- Cloud Storage
```

## Participants

| Position | Object | Stereotype |
|---|---|---|
| 1 | Owner | Actor (primary) |
| 2 | OwnerUI | `<<user interaction>>` |
| 3 | ListingManagementCoordinator | `<<coordinator>>` |
| 4 | RoomListingLogic | `<<business logic>>` |
| 5 | RoomListing | `<<entity>>` |
| 6 | CloudStorageProxy | `<<proxy>>` |
| 7 | Cloud Storage | Actor (secondary) |

## Messages

| # | From → To | Message |
|---|---|---|
| 1 | Owner → OwnerUI | access listing management, select listing to update |
| 1.1 | OwnerUI → ListingManagementCoordinator | listing selected (listing id) |
| 1.2 | ListingManagementCoordinator → RoomListingLogic | get listing details |
| 1.3 | RoomListingLogic → RoomListing | fetch listing data |
| 1.4 | RoomListingLogic → ListingManagementCoordinator | current listing info |
| 1.5 | ListingManagementCoordinator → OwnerUI | current listing info (editable) |
| 1.6 | OwnerUI → Owner | display listing in editable form |
| 2 | Owner → OwnerUI | updated listing info (+ optional new images) |
| 2.1 | OwnerUI → ListingManagementCoordinator | updated info + new images (optional) |
| 2.2 | ListingManagementCoordinator → CloudStorageProxy | upload new images (if any) |
| 2.3 | CloudStorageProxy → Cloud Storage | store images |
| 2.4 | Cloud Storage → CloudStorageProxy | images stored (image refs) |
| 2.5 | CloudStorageProxy → ListingManagementCoordinator | image refs |
| 2.6 | ListingManagementCoordinator → RoomListingLogic | validate and update listing |
| 2.7 | RoomListingLogic → RoomListing | update listing data |
| 2.8 | RoomListingLogic → ListingManagementCoordinator | listing updated |
| 2.9 | ListingManagementCoordinator → OwnerUI | listing updated successfully |
| 2.10 | OwnerUI → Owner | display listing updated successfully |

Use `/drawio` to generate a visual .drawio file from this blueprint.
