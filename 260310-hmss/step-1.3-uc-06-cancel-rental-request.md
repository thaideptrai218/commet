# Use Case: Cancel Rental Request

## Summary
Tenant cancels an eligible submitted rental request. The system updates the request status and notifies the owner.

## Dependency
- None

## Actors
- **Primary Actor:** Tenant
- **Secondary Actor(s):** Email Provider

## Preconditions
1. Tenant is signed in.
2. Tenant has at least one submitted rental request in Pending status.

## Description of main sequence
1. Tenant accesses the request management function.
2. System displays the Tenant's submitted requests and their current statuses.
3. Tenant selects a request to cancel.
4. System checks that the selected request is still in Pending status and eligible for cancellation.
5. Tenant confirms the cancellation.
6. System updates the request status to Cancelled by Tenant.
7. System sends a notification of the cancellation to the Owner.
8. System informs the Tenant that the cancellation has completed successfully.

## Description of alternative sequences
- **Step 4: Request is no longer eligible for cancellation (already accepted or rejected)**
  - 4.1: System informs the Tenant the request cannot be cancelled.
  - Use case ends unsuccessfully.
- **Step 7: Email Provider unavailable**
  - 7.1: System records the notification as failed but the cancellation still succeeds.
  - Continues to Step 8.

## Nonfunctional Requirements
- **Performance:** Cancellation result must be reflected promptly in the request status.

## Postcondition
Selected request status is Cancelled by Tenant.

## Outstanding questions
- The detailed cancellation rule for requests already in Accepted status will be finalized later.
