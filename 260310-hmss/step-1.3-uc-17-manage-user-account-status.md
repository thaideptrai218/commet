# Use Case: Manage User Account Status

## Summary
System Admin controls the status of a user account (enable, suspend, or disable) when the account violates policy or requires administrative restriction.

## Dependency
- None

## Actors
- **Primary Actor:** System Admin
- **Secondary Actor(s):** Email Provider

## Preconditions
1. System Admin is signed in.
2. The target user account exists in the system.

## Description of main sequence
1. System Admin accesses the user account administration function.
2. System displays user accounts and available account-management actions.
3. System Admin selects a user account to manage.
4. System displays the current account information and status.
5. System Admin selects the desired status-management action (Enable / Suspend / Disable).
6. System validates that the selected action is permitted under current business rules.
7. System Admin confirms the action.
8. System updates the user account status.
9. System instructs Email Provider to notify the user of the status change.
10. System informs the System Admin that the account-management action has been applied successfully.

## Description of alternative sequences
- **Step 6: Selected action is not permitted under current business rules**
  - 6.1: System informs the System Admin that the action cannot be completed.
  - Use case ends unsuccessfully.
- **Step 9: Email Provider unavailable**
  - 9.1: System records the notification as failed but the account status update still succeeds.
  - Continues to Step 10.

## Nonfunctional Requirements
- **Security:** Account-management actions must be traceable and applied consistently. Disabled accounts must not retain unauthorized access.

## Postcondition
User account status is updated. A disabled or suspended account cannot access protected system functions.

## Outstanding questions
- The final list of account status values (enabled, suspended, disabled) will be confirmed later.
