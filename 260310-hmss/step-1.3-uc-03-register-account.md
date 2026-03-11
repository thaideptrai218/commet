# Use Case: Register Account

## Summary
Visitor creates a new Tenant or Owner account by providing required registration information. The system validates the input, creates the account with the selected role, and confirms the result.

## Dependency
- None

## Actors
- **Primary Actor:** Visitor
- **Secondary Actor(s):** None

## Preconditions
The visitor is not currently signed in.

## Description of main sequence
1. Visitor accesses the account registration function.
2. System displays the registration form with available account role options (Tenant or Owner).
3. Visitor selects the desired account role and enters required registration information (name, email, phone, password).
4. System validates that all required fields are complete, the email is not already registered, and the password meets requirements.
5. Visitor reviews the entered information and confirms the registration request.
6. System creates the new account with the selected role and assigns initial account status.
7. System informs the visitor that the account has been created successfully.

## Description of alternative sequences
- **Step 4: Required information is incomplete or invalid**
  - 4.1: System informs the visitor which fields must be corrected.
  - Returns to Step 3.
- **Step 4: Email address is already associated with an existing account**
  - 4.1: System informs the visitor that an account with this email already exists.
  - Returns to Step 3.

## Nonfunctional Requirements
- **Security:** Registration credentials must be protected in transit, and passwords must be stored in a non-recoverable protected form according to the system's security standards.
- **Performance:** Registration validation must complete within an acceptable response time.

## Postcondition
A new account exists in the system with the selected role and initial account status.

## Outstanding questions
- Whether email verification is required immediately after registration will be finalized later.
