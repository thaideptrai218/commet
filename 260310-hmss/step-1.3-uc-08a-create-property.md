# Use Case: Create Property

## Summary
Owner creates a new property record with name, address, description, and policies. The system records the property under the owner's account.

## Dependency
- None

## Actors
- **Primary Actor:** Owner
- **Secondary Actor(s):** None

## Preconditions
1. Owner is signed in.

## Description of main sequence
1. Owner accesses the create property function.
2. System displays the property creation form.
3. Owner enters property information: name, address, map location, description, and general policies.
4. System validates that required property fields are complete.
5. Owner confirms the creation.
6. System records the new property.
7. System informs the Owner that the property has been created successfully.

## Description of alternative sequences
- **Step 4: Required property information is incomplete or invalid**
  - 4.1: System informs the Owner which fields must be corrected.
  - Returns to Step 3.

## Nonfunctional Requirements
- **Performance:** Property creation must be reflected promptly after confirmation.

## Postcondition
A new property record exists under the owner's account.

## Outstanding questions
- The final list of optional property attributes may be adjusted later.
