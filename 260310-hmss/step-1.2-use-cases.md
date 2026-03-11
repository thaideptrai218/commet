# Step 1.2: Use Case Identification — Hostel Management and Search System

## Use Cases by Actor

### Visitor (Primary)
| # | Use Case Name | Summary | Primary Actor | Secondary Actor(s) |
|---|--------------|---------|---------------|-------------------|
| UC-01 | Search Hostel Room | Visitor searches published room listings using filters (location, price, amenities, availability, move-in date). Returns matching results. | Visitor | Google Maps |
| UC-02 | View Room Details | Visitor selects a listing and receives full room, property, pricing, and owner information. | Visitor | Google Maps |
| UC-03 | Register Account | Visitor creates a Tenant or Owner account with required registration information. | Visitor | — |

### Registered User (Primary — generalized: Tenant, Owner, System Admin)
| # | Use Case Name | Summary | Primary Actor | Secondary Actor(s) |
|---|--------------|---------|---------------|-------------------|
| UC-04 | Sign In | Registered user authenticates and gains role-based access to protected functions. | Registered User | — |

### Tenant (Primary)
| # | Use Case Name | Summary | Primary Actor | Secondary Actor(s) |
|---|--------------|---------|---------------|-------------------|
| UC-05 | Submit Rental Request | Tenant submits a rental request for a visible, requestable room listing. | Tenant | Email Provider |
| UC-06 | Cancel Rental Request | Tenant cancels an eligible submitted request. | Tenant | Email Provider |
| UC-07 | Track Rental Request Status | Tenant views current statuses of all submitted requests. | Tenant | — |

### Owner (Primary)
| # | Use Case Name | Summary | Primary Actor | Secondary Actor(s) |
|---|--------------|---------|---------------|-------------------|
| UC-08a | Create Property | Owner creates a new property record with name, address, description, and policies. | Owner | — |
| UC-08b | Update Property | Owner updates information on an existing property. | Owner | — |
| UC-09 | Create Room Listing | Owner creates a new room listing under an existing property and saves it as draft. | Owner | Cloud Storage |
| UC-10 | Update Room Listing | Owner updates information on an existing room listing. | Owner | Cloud Storage |
| UC-11 | Publish Room Listing | Verified owner publishes a prepared listing to make it publicly searchable. | Owner | — |
| UC-12 | Change Listing Visibility | Owner hides or archives a published listing. | Owner | — |
| UC-13 | Submit Owner Verification | Owner submits personal information and supporting documents for admin review. | Owner | Cloud Storage |
| UC-14 | Review Rental Request | Owner reviews submitted requests and decides to accept, reject, or keep pending. Accepting locks the room. | Owner | Email Provider |
| UC-15 | Reopen Room Listing | Owner revokes an accepted request and reopens a locked room after offline arrangement fails. | Owner | Email Provider |

### System Admin (Primary)
| # | Use Case Name | Summary | Primary Actor | Secondary Actor(s) |
|---|--------------|---------|---------------|-------------------|
| UC-16 | Review Owner Verification | Admin approves or rejects a pending owner verification submission. | System Admin | Cloud Storage, Email Provider |
| UC-17 | Manage User Account Status | Admin enables, suspends, or disables a user account. | System Admin | Email Provider |
| UC-18 | Control Listing Visibility | Admin disables a suspicious or policy-violating listing from public search. | System Admin | Email Provider |

## Use Case Summary
Total: 19 use cases across 5 primary actors (Visitor, Registered User, Tenant, Owner, System Admin)

## Changes from Original Report
- UC-03 Register Account: moved to Visitor group (was incorrectly under Registered User)
- UC-06 "Maintain Room Listing" split into UC-09 Create, UC-10 Update, UC-11 Publish, UC-12 Change Visibility (distinct useful results)
- UC-18 "Control Listing Visibility" added (was missing — covers FE-12 from project idea)
- UC-05/UC-06 secondary corrected to Email Provider (Owner doesn't directly participate in submission)
- UC-13 secondary corrected to Cloud Storage (Admin participates in UC-16 review, not submission)
- External systems appear as secondary actors in relevant UCs
