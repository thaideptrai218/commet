# Step 1.1: Actor Identification — Hostel Management and Search System

## Primary Actors

| # | Actor Name | Type | Rationale |
|---|-----------|------|-----------|
| 1 | Visitor | Human | Initiates room search and views listings without authentication |
| 2 | Tenant | Human | Initiates rental requests, cancellations, and request status tracking |
| 3 | Owner | Human | Initiates property/room management, verification submission, and request review |
| 4 | System Admin | Human | Initiates owner verification review, account management, and listing control |

## Secondary Actors

| # | Actor Name | Type | Rationale |
|---|-----------|------|-----------|
| 5 | Google Maps | External System | Provides location data when system displays property/listing map view |
| 6 | Cloud Storage | External System | Stores and serves room images when listing is published or updated |
| 7 | Email Provider | External System | Delivers notification messages when system triggers status-change events |

## Actor Generalizations

- **Registered User** generalizes: Tenant, Owner, System Admin
  - Shared behavior: Sign In use case (all three share the same authentication interaction)
