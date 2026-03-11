# Use Case: Submit Rental Request

## Summary
Tenant submits a rental request for a visible and requestable room listing by providing rental details and contact preferences. The system records the request and notifies the owner.

## Dependency
- None

## Actors
- **Primary Actor:** Tenant
- **Secondary Actor(s):** Email Provider

## Preconditions
1. Tenant has a registered account and is signed in.
2. The selected room listing is publicly visible and in Published Available status.

## Description of main sequence
1. Tenant accesses the rental request function from a selected room listing.
2. System displays the room summary and the rental request form.
3. Tenant enters the request information: move-in date, expected rental duration, number of occupants, occupation category, budget expectation, contact phone, preferred contact method, and any special notes.
4. System validates that all required fields are complete and that the room is still requestable.
5. Tenant reviews the entered request information and confirms the submission.
6. System records the rental request with status Pending.
7. System sends a notification that a new rental request has been received to the Owner.
8. System informs the Tenant that the request has been submitted successfully.

## Description of alternative sequences
- **Step 4: The room is no longer requestable (locked or hidden)**
  - 4.1: System informs the Tenant that the request cannot be submitted for this room.
  - Use case ends unsuccessfully.
- **Step 4: Required request fields are incomplete or invalid**
  - 4.1: System informs the Tenant which fields must be corrected.
  - Returns to Step 3.
- **Step 7: Email Provider is unavailable**
  - 7.1: System records the notification as failed but the request submission succeeds.
  - Continues to Step 8.

## Nonfunctional Requirements
- **Security:** Request information must be stored securely and accessible only to the relevant Owner and System Admin.
- **Performance:** Request submission must complete within an acceptable response time.

## Postcondition
A rental request with status Pending is recorded for the selected room, visible to the Owner for review.

## Outstanding questions
- The exact set of optional request fields in release 1 may be adjusted later.
