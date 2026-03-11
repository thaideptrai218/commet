# Use Case: Sign In

## Summary
A registered user authenticates with credentials to establish an authenticated session and gain access rights based on account role.

## Dependency
- None

## Actors
- **Primary Actor:** Registered User (Tenant, Owner, or System Admin)
- **Secondary Actor(s):** None

## Preconditions
The user is not currently signed in.

## Description of main sequence
1. Registered User accesses the sign-in function.
2. System displays the sign-in form.
3. Registered User enters credentials (email and password) and submits.
4. System verifies the submitted credentials and the account status.
5. System establishes an authenticated session and applies access rights corresponding to the user's account role.
6. System informs the Registered User that sign-in has completed successfully.

## Description of alternative sequences
- **Step 4: Credentials are invalid**
  - 4.1: System informs the user that the credentials are incorrect.
  - Returns to Step 3.
- **Step 4: Account is disabled or suspended**
  - 4.1: System informs the user that the account cannot access the system.
  - Use case ends unsuccessfully.

## Nonfunctional Requirements
- **Security:** Credentials must be protected in transit. Authenticated sessions must be secured against hijacking.
- **Performance:** Sign-in must complete within an acceptable response time.

## Postcondition
The Registered User has an authenticated session with access rights corresponding to their account role (Tenant, Owner, or System Admin).

## Outstanding questions
- Whether multi-factor authentication is required in release 1 will be finalized later.
