# Use Case: Create Room Listing

## Summary
Owner creates a new room listing under an existing property, entering room details and uploading images. The system saves the listing as a draft.

## Dependency
- None

## Actors
- **Primary Actor:** Owner
- **Secondary Actor(s):** Cloud Storage

## Preconditions
Owner is signed in and has at least one existing property.

## Description of main sequence
1. Owner accesses the room listing creation function under a selected property.
2. System displays the room listing form with required and optional fields.
3. Owner enters room information: title, description, price, capacity, amenities, available-from date, furnished status, private WC status, and uploads room images.
4. System validates that required fields are present and stores the uploaded images.
5. Owner reviews the entered listing information and confirms saving.
6. System records the new room listing with status Draft.
7. System informs the Owner that the room listing has been saved as draft successfully.

## Description of alternative sequences
- **Step 4: Required fields are incomplete**
  - 4.1: System informs the Owner which fields must be corrected.
  - Returns to Step 3.
- **Step 4: Cloud Storage is unavailable**
  - 4.1: System informs the Owner that images could not be uploaded at this time.
  - Returns to Step 3.

## Nonfunctional Requirements
- **Performance:** Listing draft must be saved reliably. Image upload must complete within an acceptable time.

## Postcondition
A new room listing with status Draft exists under the selected property.

## Outstanding questions
- The final set of required versus optional room fields for draft saving will be finalized later.
