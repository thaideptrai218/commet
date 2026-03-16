# Step 2.1: Class Diagram Blueprint - Hostel Management and Search System

## Classes

### Boundary Classes

| Class Name | Stereotype | Description |
|---|---|---|
| `VisitorUI` | `<<user interaction>>` | Interfaces with Visitor; search form, listing browse, registration entry |
| `TenantUI` | `<<user interaction>>` | Interfaces with Tenant; rental request submission, cancellation, tracking |
| `OwnerUI` | `<<user interaction>>` | Interfaces with Owner; property management, listing management, verification submission, request review |
| `AdminUI` | `<<user interaction>>` | Interfaces with System Admin; verification review, account management, listing control |
| `AuthUI` | `<<user interaction>>` | Shared sign-in interface; interfaces with all Registered User subtypes |
| `GoogleMapsProxy` | `<<proxy>>` | Interfaces with Google Maps; location data and map display |
| `CloudStorageProxy` | `<<proxy>>` | Interfaces with Cloud Storage; image upload and retrieval |
| `EmailProxy` | `<<proxy>>` | Interfaces with Email Provider; notification dispatch |

### Entity Classes

| Class Name | Stereotype | Attributes |
|---|---|---|
| `User` | `<<entity>>` | email, passwordHash, role, accountStatus, createdAt |
| `Property` | `<<entity>>` | name, address, description, policies, createdAt |
| `RoomListing` | `<<entity>>` | title, description, price, capacity, amenities, availableFrom, furnished, privateWC, imagesRef, status, visibility, publishedAt, createdAt |
| `RentalRequest` | `<<entity>>` | moveInDate, rentalDuration, occupantCount, occupationCategory, budgetExpectation, contactPhone, preferredContactMethod, specialNotes, status, submittedAt |
| `OwnerVerification` | `<<entity>>` | fullName, idDocumentRef, supportingDocsRef, status, submittedAt, reviewedAt, reviewNote |

> All entities have 2+ attributes. Single-attribute rule: satisfied.

### Control Classes

| Class Name | Stereotype | Covers |
|---|---|---|
| `SearchCoordinator` | `<<coordinator>>` | UC-01 Search Hostel Room |
| `RoomDetailCoordinator` | `<<coordinator>>` | UC-02 View Room Details |
| `AuthCoordinator` | `<<coordinator>>` | UC-03 Register Account, UC-04 Sign In |
| `RentalRequestCoordinator` | `<<coordinator>>` | UC-05 Submit, UC-06 Cancel, UC-07 Track |
| `PropertyCoordinator` | `<<coordinator>>` | UC-08a Create Property, UC-08b Update Property |
| `ListingManagementCoordinator` | `<<coordinator>>` | UC-09 Create, UC-10 Update, UC-11 Publish, UC-12 Change Visibility |
| `VerificationCoordinator` | `<<coordinator>>` | UC-13 Submit Owner Verification, UC-16 Review Owner Verification |
| `RequestReviewCoordinator` | `<<coordinator>>` | UC-14 Review Rental Request, UC-15 Reopen Room Listing |
| `AdminCoordinator` | `<<coordinator>>` | UC-17 Manage Account, UC-18 Control Listing |

> All coordinators are stateless `<<coordinator>>`. State machines live in entities (`RoomListing.status`, `RentalRequest.status`, `OwnerVerification.status`, `User.accountStatus`). State-dependent control evaluation is deferred to Step 2.3.

### Business Logic Classes

Objects that own and execute domain rules; exist independently from entity data; may read/update multiple entities.

| Class Name | Stereotype | Owned Rules |
|---|---|---|
| `SearchMatchingLogic` | `<<business logic>>` | Multi-criteria filter matching; relevance scoring for published listings |
| `RoomListingLogic` | `<<business logic>>` | Publication gate (owner must be verified); status and visibility transitions (`Draft -> Published -> Locked / Hidden / Archived`) |
| `AuthenticationLogic` | `<<business logic>>` | Credential validation; `accountStatus = Active` required; role-based access policy |
| `RentalRequestLogic` | `<<business logic>>` | Room requestability check; request lifecycle (`Pending -> Accepted / Rejected / Cancelled`); lock room on accept; release on reopen |
| `VerificationLogic` | `<<business logic>>` | Approve or reject verification decisions; owner publishing eligibility |
| `UserManagementLogic` | `<<business logic>>` | Account status transition policy (`Active <-> Suspended -> Disabled`) |

### Service Classes

Objects that provide reusable capability on request; do not own domain rules; do not initiate interactions.

| Class Name | Stereotype | Capability |
|---|---|---|
| `PropertyService` | `<<service>>` | Property CRUD (create, update, retrieve); required field validation |
| `NotificationService` | `<<service>>` | Notification content composition per event type; pure `(event, data) -> content` transformation |

## Relationships

| From | To | Type | Multiplicity | Description |
|---|---|---|---|---|
| `User` | `Property` | Association | (1) - (0..*) | Owner creates and owns properties |
| `Property` | `RoomListing` | Composition | (1) *- (1..*) | Property contains room listings; listing cannot exist without property |
| `User` | `RentalRequest` | Association | (1) - (0..*) | Tenant submits rental requests |
| `RoomListing` | `RentalRequest` | Association | (1) - (0..*) | Room receives rental requests from multiple tenants |
| `User` | `OwnerVerification` | Association | (1) - (0..1) | Owner has at most one verification record |

## Interaction Patterns Detected

All 19 UCs follow **Pattern A: Client/Server** - standard for this information system web application.

| Use Case | Pattern | Sequence |
|---|---|---|
| UC-01 Search Hostel Room | A | `VisitorUI -> SearchCoordinator -> SearchMatchingLogic -> RoomListing (+GoogleMapsProxy)` |
| UC-02 View Room Details | A | `VisitorUI -> RoomDetailCoordinator -> RoomListingLogic -> RoomListing (+GoogleMapsProxy)` |
| UC-03 Register Account | A | `VisitorUI -> AuthCoordinator -> AuthenticationLogic -> User` |
| UC-04 Sign In | A | `AuthUI -> AuthCoordinator -> AuthenticationLogic -> User` |
| UC-05 Submit Rental Request | A | `TenantUI -> RentalRequestCoordinator -> RentalRequestLogic -> RentalRequest (+EmailProxy via NotificationService)` |
| UC-06 Cancel Rental Request | A | `TenantUI -> RentalRequestCoordinator -> RentalRequestLogic -> RentalRequest (+EmailProxy via NotificationService)` |
| UC-07 Track Request Status | A | `TenantUI -> RentalRequestCoordinator -> RentalRequestLogic -> RentalRequest` |
| UC-08a Create Property | A | `OwnerUI -> PropertyCoordinator -> PropertyService -> Property` |
| UC-08b Update Property | A | `OwnerUI -> PropertyCoordinator -> PropertyService -> Property` |
| UC-09 Create Room Listing | A | `OwnerUI -> ListingManagementCoordinator -> RoomListingLogic -> RoomListing (+CloudStorageProxy)` |
| UC-10 Update Room Listing | A | `OwnerUI -> ListingManagementCoordinator -> RoomListingLogic -> RoomListing (+CloudStorageProxy)` |
| UC-11 Publish Room Listing | A | `OwnerUI -> ListingManagementCoordinator -> RoomListingLogic -> RoomListing (+VerificationLogic)` |
| UC-12 Change Listing Visibility | A | `OwnerUI -> ListingManagementCoordinator -> RoomListingLogic -> RoomListing` |
| UC-13 Submit Owner Verification | A | `OwnerUI -> VerificationCoordinator -> VerificationLogic -> OwnerVerification (+CloudStorageProxy)` |
| UC-14 Review Rental Request | A | `OwnerUI -> RequestReviewCoordinator -> RentalRequestLogic -> RentalRequest (+EmailProxy via NotificationService)` |
| UC-15 Reopen Room Listing | A | `OwnerUI -> RequestReviewCoordinator -> RentalRequestLogic -> RentalRequest, RoomListing (+EmailProxy via NotificationService)` |
| UC-16 Review Owner Verification | A | `AdminUI -> VerificationCoordinator -> VerificationLogic -> OwnerVerification (+EmailProxy via NotificationService)` |
| UC-17 Manage User Account | A | `AdminUI -> AdminCoordinator -> UserManagementLogic -> User (+EmailProxy via NotificationService)` |
| UC-18 Control Listing Visibility | A | `AdminUI -> AdminCoordinator -> RoomListingLogic -> RoomListing (+EmailProxy via NotificationService)` |

## Candidate Subsystem Grouping

See [step-2.1b-subsystem-grouping.md](./step-2.1b-subsystem-grouping.md) for the Phase 2 grouping of related use cases into candidate subsystems.

Use `/drawio` to generate a visual `.drawio` file from this blueprint.
