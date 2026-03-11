# Step 1.5: Use Case Diagram Blueprint — Hostel Management and Search System

## [USE CASE DIAGRAM BLUEPRINT]

### System Boundary Box: Hostel Management and Search System

---

### Outside the Boundary (Actors)

**Primary Actors (Left Side):**
- Visitor
- Registered User (generalized: Tenant, Owner, System Admin)
  - Tenant
  - Owner
  - System Admin

**Secondary Actors (Right Side):**
- Google Maps
- Cloud Storage
- Email Provider

---

### Inside the Boundary (Use Cases)

- [UC-01: Search Hostel Room]
- [UC-02: View Room Details]
- [UC-03: Register Account]
- [UC-04: Sign In]
- [UC-05: Submit Rental Request]
- [UC-06: Cancel Rental Request]
- [UC-07: Track Rental Request Status]
- [UC-08a: Create Property]
- Owner --- [UC-08b: Update Property]
- [UC-09: Create Room Listing]
- [UC-10: Update Room Listing]
- [UC-11: Publish Room Listing]
- [UC-12: Change Listing Visibility]
- [UC-13: Submit Owner Verification]
- [UC-14: Review Rental Request]
- [UC-15: Reopen Room Listing]
- [UC-16: Review Owner Verification]
- [UC-17: Manage User Account Status]
- [UC-18: Control Listing Visibility]

---

### Connections to Draw

**Solid Lines (Actor ↔ Use Case):**

Visitor:
- Visitor --- [UC-01: Search Hostel Room]
- Visitor --- [UC-02: View Room Details]
- Visitor --- [UC-03: Register Account]

Registered User (via generalization arrow from Tenant, Owner, System Admin):
- Registered User --- [UC-04: Sign In]

Tenant:
- Tenant --- [UC-05: Submit Rental Request]
- Tenant --- [UC-06: Cancel Rental Request]
- Tenant --- [UC-07: Track Rental Request Status]

Owner:
- Owner --- [UC-08a: Create Property]
- Owner --- [UC-08b: Update Property]
- Owner --- [UC-09: Create Room Listing]
- Owner --- [UC-10: Update Room Listing]
- Owner --- [UC-11: Publish Room Listing]
- Owner --- [UC-12: Change Listing Visibility]
- Owner --- [UC-13: Submit Owner Verification]
- Owner --- [UC-14: Review Rental Request]
- Owner --- [UC-15: Reopen Room Listing]

System Admin:
- System Admin --- [UC-16: Review Owner Verification]
- System Admin --- [UC-17: Manage User Account Status]
- System Admin --- [UC-18: Control Listing Visibility]

Secondary Actors (right side, participating in UCs):
- Google Maps --- [UC-01: Search Hostel Room]
- Google Maps --- [UC-02: View Room Details]
- Cloud Storage --- [UC-09: Create Room Listing]
- Cloud Storage --- [UC-10: Update Room Listing]
- Cloud Storage --- [UC-13: Submit Owner Verification]
- Email Provider --- [UC-05: Submit Rental Request]
- Email Provider --- [UC-06: Cancel Rental Request]
- Email Provider --- [UC-14: Review Rental Request]
- Email Provider --- [UC-15: Reopen Room Listing]
- Cloud Storage --- [UC-16: Review Owner Verification]
- Email Provider --- [UC-16: Review Owner Verification]
- Email Provider --- [UC-17: Manage User Account Status]
- Email Provider --- [UC-18: Control Listing Visibility]

---

### Dashed Arrows (Dependencies)
- None. No <<include>> or <<extend>> relationships identified at Phase 1.

---

### Actor Generalizations
- Registered User ◁— Tenant
- Registered User ◁— Owner
- Registered User ◁— System Admin
  (Generalization arrow: hollow triangle from sub-actor pointing to super-actor)

---

### Drawing Notes
1. Place Visitor, Tenant, Owner, System Admin on the LEFT side outside the boundary.
2. Place Google Maps, Cloud Storage, Email Provider on the RIGHT side outside the boundary.
3. Place Registered User above Tenant/Owner/System Admin with generalization (hollow triangle) arrows.
4. All UC ellipses are inside the rectangular system boundary.
5. Connect actors to UCs with solid lines only.
6. No dashed arrows needed (no include/extend relationships).
7. Actor-to-actor connections are NEVER drawn.
