# Use Case: Control Listing Visibility

## Summary
System Admin disables a suspicious or policy-violating listing from public search to protect platform integrity.

## Dependency
- None

## Actors
- **Primary Actor:** System Admin
- **Secondary Actor(s):** Email Provider

## Preconditions
1. System Admin is signed in.
2. The target listing is currently publicly visible.

## Description of main sequence
1. System Admin accesses the listing administration function.
2. System displays publicly visible listings with their associated information.
3. System Admin selects a listing to review.
4. System displays the listing details and available control actions.
5. System Admin selects the Disable action for the listing.
6. System Admin confirms the disable action.
7. System removes the listing from public search results.
8. System instructs Email Provider to notify the Owner that the listing has been disabled.
9. System informs the System Admin that the listing has been disabled successfully.

## Description of alternative sequences
- **Step 8: Email Provider unavailable**
  - 8.1: System records the notification as failed but the listing is still disabled.
  - Continues to Step 9.

## Nonfunctional Requirements
- **Security:** Admin listing control must be traceable and applied immediately to protect platform users.

## Postcondition
The listing is removed from public search and no longer visible to visitors or tenants.

## Outstanding questions
- Whether a disabled listing can be re-enabled by admin or owner, and under what conditions, will be finalized later.
