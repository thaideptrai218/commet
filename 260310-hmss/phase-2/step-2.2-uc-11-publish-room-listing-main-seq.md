# Communication Diagram: UC-11 Publish Room Listing — Main Sequence

## Object Layout

```
Owner --- OwnerUI --- ListingManagementCoordinator --- RoomListingLogic --- RoomListing
                                  |--- VerificationLogic --- OwnerVerification
```

## Participants

| Position | Object | Stereotype |
|---|---|---|
| 1 | Owner | Actor (primary) |
| 2 | OwnerUI | `<<user interaction>>` |
| 3 | ListingManagementCoordinator | `<<coordinator>>` |
| 4 | RoomListingLogic | `<<business logic>>` |
| 5 | RoomListing | `<<entity>>` |
| 6 | VerificationLogic | `<<business logic>>` |
| 7 | OwnerVerification | `<<entity>>` |

## Messages

| # | From → To | Message |
|---|---|---|
| 1 | Owner → OwnerUI | access publication function (listing selected) |
| 1.1 | OwnerUI → ListingManagementCoordinator | publication request (listing id) |
| 1.2 | ListingManagementCoordinator → RoomListingLogic | request listing for publication check |
| 1.3 | RoomListingLogic → RoomListing | provide listing data |
| 1.4 | RoomListingLogic → ListingManagementCoordinator | listing data + completeness result |
| 1.5 | ListingManagementCoordinator → VerificationLogic | check owner verification status |
| 1.6 | VerificationLogic → OwnerVerification | get owner verification status |
| 1.7 | VerificationLogic → ListingManagementCoordinator | owner is verified |
| 1.8 | ListingManagementCoordinator → OwnerUI | listing + publication checklist (verified, fields complete, image exists) |
| 1.9 | OwnerUI → Owner | display listing and publication requirements checklist |
| 2 | Owner → OwnerUI | confirm publication |
| 2.1 | OwnerUI → ListingManagementCoordinator | confirm publication |
| 2.2 | ListingManagementCoordinator → RoomListingLogic | publish listing |
| 2.3 | RoomListingLogic → RoomListing | publish listing |
| 2.4 | RoomListingLogic → ListingManagementCoordinator | listing published |
| 2.5 | ListingManagementCoordinator → OwnerUI | published successfully |
| 2.6 | OwnerUI → Owner | display listing is now publicly searchable |

## Notes
- Coordinator calls both `RoomListingLogic` and `VerificationLogic` independently — no cross-service calls.
- Image existence checked via `RoomListing.imagesRef` (set during UC-09); no Cloud Storage call needed at publish time.

Use `/drawio` to generate a visual .drawio file from this blueprint.
