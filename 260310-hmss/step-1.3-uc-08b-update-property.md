# Use Case: Update Property

## Summary
Owner updates information on an existing property (name, address, description, policies). The system records the changes.

## Dependency
- None

## Actors
- **Primary Actor:** Owner
- **Secondary Actor(s):** None

## Preconditions
1. Owner is signed in.
2. At least one property owned by this owner exists in the system (UC-08a has been performed).

## Description of main sequence
1. Owner accesses the property management function.
2. System displays the list of existing properties owned by this owner.
3. Owner selects a property and requests to update it.
4. System displays the current property information in an editable form.
5. Owner edits property information: name, address, map location, description, and general policies.
6. System validates that required property fields are complete.
7. Owner confirms the update.
8. System records the updated property information.
9. System informs the Owner that the property has been updated successfully.

## Description of alternative sequences
- **Step 6: Required property information is incomplete or invalid**
  - 6.1: System informs the Owner which fields must be corrected.
  - Returns to Step 5.

## Nonfunctional Requirements
- **Performance:** Updated property information must be reflected promptly after confirmation.

## Postcondition
The selected property's information is updated in the system.

## Outstanding questions
- The final list of optional property attributes may be adjusted later.
