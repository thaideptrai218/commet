# Communication Diagram: UC-01 Search Hostel Room — Main Sequence

## Object Layout

```
Visitor --- VisitorUI --- SearchCoordinator --- SearchMatchingLogic --- RoomListing
                                  |
                           GoogleMapsProxy --- Google Maps
```

## Participants

| Position | Object              | Stereotype             |
| -------- | ------------------- | ---------------------- |
| 1        | Visitor             | Actor (primary)        |
| 2        | VisitorUI           | `<<user interaction>>` |
| 3        | SearchCoordinator   | `<<coordinator>>`      |
| 4        | SearchMatchingLogic | `<<business logic>>`          |
| 5        | RoomListing         | `<<entity>>`           |
| 6        | GoogleMapsProxy     | `<<proxy>>`            |
| 7        | Google Maps         | Actor (secondary)      |

## Messages

| #    | From → To                               | Message                                                                        |
| ---- | --------------------------------------- | ------------------------------------------------------------------------------ |
| 1    | Visitor → VisitorUI                     | open search                                                                    |
| 1.1  | VisitorUI → SearchCoordinator           | request search page                                                            |
| 1.2  | SearchCoordinator → SearchMatchingLogic | request initial published listings                                             |
| 1.3  | SearchMatchingLogic → RoomListing       | provide published listings                                                     |
| 1.4  | SearchMatchingLogic → SearchCoordinator | listings data                                                                  |
| 1.5  | SearchCoordinator → GoogleMapsProxy     | request location data for listings                                             |
| 1.6  | GoogleMapsProxy → Google Maps           | location data request                                                                 |
| 1.7  | Google Maps → GoogleMapsProxy           | location data                                                                  |
| 1.8  | GoogleMapsProxy → SearchCoordinator     | location data                                                                  |
| 1.9  | SearchCoordinator → VisitorUI           | search form + initial listings with location data                              |
| 1.10 | VisitorUI → Visitor                     | display search form with listings                                              |
| 2    | Visitor → VisitorUI                     | search criteria (location, price range, amenities, availability, move-in date) |
| 2.1  | VisitorUI → SearchCoordinator           | search criteria                                                                |
| 2.2  | SearchCoordinator → SearchMatchingLogic | filter listings by criteria                                                    |
| 2.3  | SearchMatchingLogic → RoomListing       | provide matching listings                                                      |
| 2.4  | SearchMatchingLogic → SearchCoordinator | matching listings                                                              |
| 2.5  | SearchCoordinator → GoogleMapsProxy     | request location data for results                                              |
| 2.6  | GoogleMapsProxy → Google Maps           | location data request                                                                 |
| 2.7  | Google Maps → GoogleMapsProxy           | location data                                                                  |
| 2.8  | GoogleMapsProxy → SearchCoordinator     | location data                                                                  |
| 2.9  | SearchCoordinator → VisitorUI           | search results with location data                                              |
| 2.10 | VisitorUI → Visitor                     | display matching room listings                                                 |
| 3    | Visitor → VisitorUI                     | select listing                                                                 |
| 3.1  | VisitorUI → SearchCoordinator           | listing selected                                                               |
| 3.2  | SearchCoordinator → VisitorUI           | listing detail entry point                                                     |
| 3.3  | VisitorUI → Visitor                     | navigate to listing detail                                                     |

## Notes

- Google Maps is a secondary actor — responds to queries from GoogleMapsProxy; does not initiate.
- Coordinator calls GoogleMapsProxy (boundary), not SearchMatchingLogic — COMET rule: Business Logic/Service never calls Proxy.

Use `/drawio` to generate a visual .drawio file from this blueprint.
