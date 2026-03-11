# Use Case: Submit Owner Verification

## Summary
Owner submits personal identification information and supporting documents for manual review by the System Admin. System records the submission and awaits administrative decision.

## Dependency
- None

## Actors
- **Primary Actor:** Owner
- **Secondary Actor(s):** Cloud Storage

## Preconditions
1. Owner is signed in.
2. Owner has not yet been verified, or has a previously rejected verification submission.

## Description of main sequence
1. Owner accesses the owner verification submission function.
2. System displays the required verification information fields and document requirements.
3. Owner enters personal information and uploads supporting identification documents.
4. System validates that all required fields are present and sends uploaded documents to Cloud Storage.
5. Owner reviews the submission and confirms it.
6. System records the verification submission with status Pending Review.
7. System informs the Owner that the submission has been received and is pending admin review.

## Description of alternative sequences
- **Step 4: Required information or documents are missing**
  - 4.1: System informs the Owner which items must be corrected or completed.
  - Returns to Step 3.
- **Step 4: Cloud Storage is unavailable**
  - 4.1: System informs the Owner that document upload failed at this time.
  - Returns to Step 3.

## Nonfunctional Requirements
- **Security:** Verification documents must be stored securely and accessible only to System Admin.
- **Performance:** Submission must be recorded reliably without data loss.

## Postcondition
Owner verification submission is recorded with status Pending Review. Owner cannot publish listings until System Admin approves the submission.

## Outstanding questions
- The final list of required verification document types will be finalized later.
