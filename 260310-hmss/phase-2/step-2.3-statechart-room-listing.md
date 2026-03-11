# Statechart: RoomListing

## States

| State | Type | Entry/Exit Actions |
|---|---|---|
| Draft | Initial target | — |
| Published Available | Normal | entry / Add to search index |
| Locked | Normal | entry / Block new requests |
| Hidden | Normal | entry / Remove from search index |
| Archived | Final | entry / Remove from search index |

## Transitions

| # | Source State | Event [Condition] / Action | Target State |
|---|---|---|---|
| T1 | Initial | — | Draft |
| T2 | Draft | Publish Requested [owner verified, fields complete, images exist] / Mark Published | Published Available |
| T3 | Published Available | Rental Request Accepted / Lock Room | Locked |
| T4 | Published Available | Owner Hides / Remove From Search | Hidden |
| T5 | Published Available | Owner Archives / Remove From Search | Archived |
| T6 | Locked | Owner Reopens [offline arrangement failed] / Restore Availability | Published Available |
| T7 | Published Available | Admin Disables [policy violation] / Remove From Search | Hidden |
| T8 | Hidden | Owner Shows / Restore To Search | Published Available |

## Communication Diagram Synchronization

| Transition | UC | Comm Diagram Message |
|---|---|---|
| T2 | UC-11 | msg 2.3: `RoomListingLogic → RoomListing: publish listing` |
| T3 | UC-14 | msg 3.4: `RentalRequestLogic → RoomListing: lock room` |
| T4 | UC-12 | via `RoomListingLogic → RoomListing: update visibility` |
| T5 | UC-12 | via `RoomListingLogic → RoomListing: update visibility` |
| T6 | UC-15 | msg 3.4: `RentalRequestLogic → RoomListing: reopen room` |
| T7 | UC-18 | via `RoomListingLogic → RoomListing: disable listing` |
| T8 | UC-12 | via `RoomListingLogic → RoomListing: update visibility` |

## Notes

- Locked cannot transition to Hidden/Archived directly — must reopen first (UC-12 precondition requires Published status).
- T4 and T7 share the same target (Hidden) but differ in triggering actor (Owner vs Admin).
- Archived is terminal per current scope — restoration policy TBD.

Use `/drawio` to generate a visual .drawio file from this blueprint.
