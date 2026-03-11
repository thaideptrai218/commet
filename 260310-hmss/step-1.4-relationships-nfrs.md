# Step 1.4: Relationships & NFRs — Hostel Management and Search System

## <<include>> Relationships

After analyzing all 19 use cases, no <<include>> relationships are identified at Phase 1.

| Candidate | Reason Not Extracted |
|-----------|---------------------|
| Authentication (Sign In) | Precondition for protected UCs — Sign In runs before UC initiates, not inside it |
| Cloud Storage upload | Technical step embedded in UC sequences, not a full standalone actor↔system interaction sequence |
| Email notification | Each UC has specific notification content — no identical shared sequence to extract |

## <<extend>> Relationships

After analyzing all 19 use cases, no <<extend>> relationships are identified at Phase 1.

| Candidate | Base UC | Reason Not Extracted |
|-----------|---------|---------------------|
| Submit Rental Request from detail page | UC-02 View Room Details | UC-05 is also accessible independently — not purely conditional on UC-02 |
| Lock Room after Accept | UC-14 Review Rental Request | Locking is mandatory business rule of UC-14, not optional |
| Reopen after failed arrangement | UC-14 Review Rental Request | UC-15 is initiated at a separate point in time, not within UC-14's session |

Note: <<include>>/<<extend>> relationships may emerge in Phase 2 Analysis when interaction diagrams reveal shared object collaborations.

## Updated Use Cases
No base UCs require rewriting. All dependency fields correctly set to None.

## Nonfunctional Requirements

### Performance
- Search results (UC-01) must return within 3 seconds under normal load.
- Room detail page (UC-02) must load within 3 seconds under normal conditions.
- All write operations (request submission, listing publication, account updates) must complete within an acceptable response time.

### Security
- All credentials and authenticated sessions must be protected against unauthorized access and hijacking.
- Owner verification documents must be stored securely and accessible only to System Admin.
- Rental request information must be accessible only to the relevant Owner and System Admin.
- Publication rules must be enforced consistently — unverified owners must never bypass the verification gate.
- Account-management actions must be traceable and take effect immediately upon confirmation.

### Availability
- Public search and listing viewing must be available during normal operating hours with minimal interruption.
- Protected functions (request submission, listing management, admin review) must be consistently accessible to authenticated users.

### Scalability
- The system must accommodate growth in listings, users, and concurrent requests without fundamental business-model changes.
- Cloud Storage and Email Provider integrations must support increased volume as the platform scales.
