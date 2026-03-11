# Communication Diagram: UC-02 View Room Details - Main Sequence

## Object Layout

```
Visitor --- VisitorUI --- RoomDetailCoordinator --- RoomListingLogic --- RoomListing
                                   |
                            GoogleMapsProxy --- Google Maps
```

## Participants

| Position | Object                | Stereotype             |
| -------- | --------------------- | ---------------------- |
| 1        | Visitor               | Actor (primary)        |
| 2        | VisitorUI             | `<<user interaction>>` |
| 3        | RoomDetailCoordinator | `<<coordinator>>`      |
| 4        | RoomListingLogic      | `<<business logic>>`   |
| 5        | RoomListing           | `<<entity>>`           |
| 6        | GoogleMapsProxy       | `<<proxy>>`            |
| 7        | Google Maps           | Actor (secondary)      |

## Messages

| #   | From -> To                                | Message                          |
| --- | ----------------------------------------- | -------------------------------- |
| 1   | Visitor -> VisitorUI                      | select room listing              |
| 1.1 | VisitorUI -> RoomDetailCoordinator        | listing selected (listing id)    |
| 1.2 | RoomDetailCoordinator -> RoomListingLogic | get listing details              |
| 1.3 | RoomListingLogic -> RoomListing           | fetch listing data               |
| 1.4 | RoomListingLogic -> RoomDetailCoordinator | listing details                  |
| 1.5 | RoomDetailCoordinator -> VisitorUI        | room details                     |
| 1.6 | VisitorUI -> Visitor                      | display full room details        |
| 2   | Visitor -> VisitorUI                      | request map location             |
| 2.1 | VisitorUI -> RoomDetailCoordinator        | map location requested           |
| 2.2 | RoomDetailCoordinator -> GoogleMapsProxy  | request property location        |
| 2.3 | GoogleMapsProxy -> Google Maps            | location query                   |
| 2.4 | Google Maps -> GoogleMapsProxy            | map data                         |
| 2.5 | GoogleMapsProxy -> RoomDetailCoordinator  | map data                         |
| 2.6 | RoomDetailCoordinator -> VisitorUI        | property map                     |
| 2.7 | VisitorUI -> Visitor                      | display property location on map |

Use `/drawio` to generate a visual .drawio file from this blueprint.
