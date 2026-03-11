# Communication Diagram: UC-09 Create Room Listing - Main Sequence

## Object Layout

```text
Owner --- RoomListingCreationUI --- ListingManagementCoordinator --- RoomListingRules --- Property
                                           |                                |
                                           |                                --- RoomListing
                                           |
                                           --- CloudStorageProxy --- Cloud Storage
```

## Participants

| Position | Object                       | Stereotype             |
| -------- | ---------------------------- | ---------------------- |
| 1        | Owner                        | Actor (primary)        |
| 2        | RoomListingCreationUI        | `<<user interaction>>` |
| 3        | ListingManagementCoordinator | `<<coordinator>>`      |
| 4        | RoomListingRules             | `<<business logic>>`   |
| 5        | Property                     | `<<entity>>`           |
| 6        | RoomListing                  | `<<entity>>`           |
| 7        | CloudStorageProxy            | `<<proxy>>`            |
| 8        | Cloud Storage                | Actor (secondary)      |

## Messages

| #   | From -> To                                        | Message                      |
| --- | ------------------------------------------------- | ---------------------------- |
| 1   | Owner -> RoomListingCreationUI                    | Room Listing Creation Access |
| 1.1 | RoomListingCreationUI -> ListingManagementCoordinator | Listing Creation Request  |
| 1.2 | ListingManagementCoordinator -> RoomListingRules  | Property Context Request     |
| 1.3 | RoomListingRules -> Property                      | Property Context Request     |
| 1.4 | Property -> RoomListingRules                      | Property Context             |
| 1.5 | RoomListingRules -> ListingManagementCoordinator  | Property Context             |
| 1.6 | ListingManagementCoordinator -> RoomListingCreationUI | Listing Creation Form     |
| 1.7 | RoomListingCreationUI -> Owner                    | Listing Creation Form        |
| 2   | Owner -> RoomListingCreationUI                    | Listing Information and Images |
| 2.1 | RoomListingCreationUI -> ListingManagementCoordinator | Listing Information and Images |
| 2.2 | ListingManagementCoordinator -> CloudStorageProxy | Listing Images               |
| 2.3 | CloudStorageProxy -> Cloud Storage                | Listing Images               |
| 2.4 | Cloud Storage -> CloudStorageProxy                | Image References             |
| 2.5 | CloudStorageProxy -> ListingManagementCoordinator | Image References             |
| 2.6 | ListingManagementCoordinator -> RoomListingCreationUI | Listing Review            |
| 2.7 | RoomListingCreationUI -> Owner                    | Listing Review               |
| 3   | Owner -> RoomListingCreationUI                    | Listing Save Confirmation    |
| 3.1 | RoomListingCreationUI -> ListingManagementCoordinator | Listing Creation Request  |
| 3.2 | ListingManagementCoordinator -> RoomListingRules  | Listing Draft Information    |
| 3.3 | RoomListingRules -> RoomListing                   | Room Listing Record          |
| 3.4 | RoomListing -> RoomListingRules                   | Room Listing Record          |
| 3.5 | RoomListingRules -> ListingManagementCoordinator  | Listing Creation Result      |
| 3.6 | ListingManagementCoordinator -> RoomListingCreationUI | Listing Draft Outcome    |
| 3.7 | RoomListingCreationUI -> Owner                    | Listing Draft Confirmation   |

## Notes

- `ListingManagementCoordinator` handles the external storage interaction through `CloudStorageProxy`.
- `RoomListingRules` encapsulates draft-creation rules and listing formation logic.
- Messages are kept at analysis level and avoid method-style naming.

Use `/drawio` to generate a visual `.drawio` file from this blueprint.
