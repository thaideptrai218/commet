# Use Case: Update Room Listing

## Summary
Owner updates information on an existing room listing. System records the changes and updates listing data.

## Dependency
- None

## Actors
- **Primary Actor:** Owner
- **Secondary Actor(s):** Cloud Storage

## Preconditions
1. Owner is signed in.
2. Owner has at least one existing room listing.

## Description of main sequence
1. Owner accesses the room listing management function and selects an existing listing to update.
2. System displays the current listing information in editable form.
3. Owner modifies the desired fields (title, description, price, capacity, amenities, available-from date) and optionally uploads new images.
4. System validates the updated fields and sends any new images to Cloud Storage.
5. Owner reviews the changes and confirms the update.
6. System records the updated listing information.
7. System informs the Owner that the listing has been updated successfully.

## Description of alternative sequences
- **Step 4: Required fields are cleared or invalid**
  - 4.1: System informs the Owner which fields must be corrected.
  - Returns to Step 3.
- **Step 4: Cloud Storage unavailable**
  - 4.1: System informs the Owner that image upload failed at this time.
  - Returns to Step 3.

## Nonfunctional Requirements
- **Performance:** Updated listing information must be persisted reliably and reflect promptly.

## Postcondition
Room listing information is updated in the system.

## Outstanding questions
- Whether updating a published listing triggers a re-verification step will be finalized later.
