# Statechart: RentalRequest

## States

| State               | Type           | Entry/Exit Actions             |
| ------------------- | -------------- | ------------------------------ |
| Submitted           | Initial target | —                              |
| Pending             | Normal         | —                              |
| Accepted            | Normal         | entry / Lock associated room   |
| Rejected            | Final          | —                              |
| Cancelled by Tenant | Final          | —                              |
| Revoked by Owner    | Final          | entry / Reopen associated room |

## Transitions

| #   | Source State | Event [Condition] / Action                                                | Target State        |
| --- | ------------ | ------------------------------------------------------------------------- | ------------------- |
| T1  | Initial      | —                                                                         | Submitted           |
| T2  | Submitted    | Owner Reviews [defers decision] / Mark Pending                            | Pending             |
| T3  | Submitted    | Owner Reviews [accepts] / Mark Accepted, Lock Room                        | Accepted            |
| T4  | Submitted    | Owner Reviews [rejects] / Mark Rejected, Notify Tenant                    | Rejected            |
| T5  | Pending      | Owner Reviews [accepts] / Mark Accepted, Lock Room                        | Accepted            |
| T6  | Pending      | Owner Reviews [rejects] / Mark Rejected, Notify Tenant                    | Rejected            |
| T7  | Submitted    | Tenant Cancels / Mark Cancelled, Notify Owner                             | Cancelled by Tenant |
| T8  | Pending      | Tenant Cancels / Mark Cancelled, Notify Owner                             | Cancelled by Tenant |
| T9  | Accepted     | Owner Revokes [offline failed] / Mark Revoked, Reopen Room, Notify Tenant | Revoked by Owner    |

## Composite States

| Composite | Contains           | Aggregated Transitions               |
| --------- | ------------------ | ------------------------------------ |
| Open      | Submitted, Pending | Tenant Cancels → Cancelled by Tenant |

Using the **Open** composite state reduces T7 + T8 into a single aggregated transition from the composite boundary.

## Communication Diagram Synchronization

| Transition | UC    | Comm Diagram Message                                                 |
| ---------- | ----- | -------------------------------------------------------------------- |
| T1         | UC-05 | msg 2.5: `RentalRequestLogic → RentalRequest: record rental request` |
| T3/T5      | UC-14 | msg 3.3: `RentalRequestLogic → RentalRequest: mark request accepted` |
| T4/T6      | UC-14 | via `RentalRequestLogic → RentalRequest: mark request rejected`      |
| T7/T8      | UC-06 | via `RentalRequestLogic → RentalRequest: cancel rental request`      |
| T9         | UC-15 | msg 3.3: `RentalRequestLogic → RentalRequest: revoke rental request` |

## Discrepancy Note

Source doc §12.2 lists "Submitted" and "Pending" as distinct statuses. UC-05 records initial status as "Pending" (not "Submitted"). This statechart follows the source doc's 6-status model. Reconciliation: "Submitted" = just submitted, awaiting owner review; "Pending" = owner has seen and explicitly deferred. UC-06 cancel precondition ("Pending status") should also allow cancellation from "Submitted."

Use `/drawio` to generate a visual .drawio file from this blueprint.
