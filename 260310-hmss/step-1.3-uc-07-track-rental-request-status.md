# Use Case: Track Rental Request Status

## Summary
Tenant reviews current statuses of submitted rental requests to decide next actions.

## Dependency
- None

## Actors
- **Primary Actor:** Tenant
- **Secondary Actor(s):** None

## Preconditions
1. Tenant is signed in.

## Description of main sequence
1. Tenant accesses the rental request status function.
2. System displays the request list with current status of each request (Pending, Accepted, Rejected, Cancelled, Revoked).
3. Tenant selects a specific request for more detail.
4. System displays the selected request's full status details and available actions.
5. Tenant reviews the detailed status information.

## Description of alternative sequences
- **Step 2: Tenant has no submitted requests**
  - 2.1: System informs the Tenant that no request history is available.
  - Use case ends successfully.

## Nonfunctional Requirements
- **Performance:** Status information must be accurate and up to date at time of retrieval.

## Postcondition
Tenant has been informed of current rental request status, or informed that no submitted requests exist.

## Outstanding questions
- The exact level of request history detail visible to tenants will be finalized later.
