# Step 1.0: Context Diagram Blueprint — Hostel Management and Search System

## [CONTEXT DIAGRAM BLUEPRINT]

### System Under Consideration

- Hostel Management and Search System (HMSS)

### External Entities

- Visitor
- Tenant
- Owner
- System Admin
- Google Maps
- Cloud Storage
- Email Provider

### Exchanges to Draw

Visitor <-> HMSS
- To system: search criteria, listing selection, registration information
- From system: search results, room details, registration outcome

Tenant <-> HMSS
- To system: sign-in credentials, rental request submission, cancellation request, status inquiry
- From system: authentication result, request status, request outcome

Owner <-> HMSS
- To system: sign-in credentials, property data, room listing data, owner verification submission, request decisions, reopen request
- From system: authentication result, publication result, request lists and request details, verification status, listing state result

System Admin <-> HMSS
- To system: sign-in credentials, verification review decision, account-status change, listing-control action
- From system: verification data, user and listing data, review result, control result

Google Maps <-> HMSS
- To system: map data, geolocation data
- From system: location lookup request

Cloud Storage <-> HMSS
- To system: stored asset reference, retrieved file data
- From system: image upload request, document upload request, asset retrieval request

Email Provider <-> HMSS
- To system: delivery status
- From system: notification dispatch request

### Drawing Notes

1. Draw HMSS as one central black-box system.
2. Place human entities on the left side of the system.
3. Place external service systems on the right side of the system.
4. Keep data-flow labels business-visible and short.
5. Do not show use cases, classes, packages, or internal subsystems in this diagram.
