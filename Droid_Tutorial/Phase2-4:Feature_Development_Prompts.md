# coding-droid-feature-prompts.md  
Feature-by-feature instructions for **Coding Droid** to implement the MVP backlog in isolated branches and PRs.  
Base repo: `github.com/guillehoyob/travelvault`  
Default branches: `main` (prod) · `development` (integration)

---

## How to Use  
1. Pick the **next unfinished feature prompt**.  
2. Create the branch exactly as specified (`feature/<slug>`).  
3. Follow “Scope & Tasks”.  
4. Ensure tests, lint, and CI pass locally.  
5. Open a PR **into `development`** with the title provided.  
6. Wait for review before starting another feature.

---

## Feature 1 – User Registration & Profile  
**Branch:** `feature/auth-onboarding`  
**PR Title:** `feat(auth): onboarding, email+SSO, biometric toggle`  

### Scope & Tasks  
- Implement email, Google, Apple sign-up / sign-in with Firebase Auth.  
- Add 2FA toggle (placeholder UI, no backend yet).  
- Biometric unlock integration (Expo LocalAuth).  
- On first login route to **ProfileSetup** screen.  
- Store basic profile in `users/{uid}` with schema: `{displayName,email,photoURL,createdAt}`.  

### Acceptance Criteria  
- New users can register via all three providers.  
- Returning users auto-login if token valid.  
- Biometric switch appears in Settings and saves prefer-ence in Firestore.  
- Unit tests cover happy & error paths (≥80 % new lines).  

---

## Feature 2 – Passport OCR Scan  
**Branch:** `feature/doc-passport-ocr`  
**PR Title:** `feat(doc): passport scan with MRZ OCR`  

### Scope & Tasks  
- Screen `PassportScanScreen` accessible via “Add Document”.  
- Use Expo Camera + ML Kit to capture image and extract MRZ fields.  
- Pre-fill `DocForm` with `number`, `name`, `nationality`, `expiryDate`.  
- Encrypt image locally, upload to Firebase Storage, metadata to `documents/{docId}`.  

### Acceptance Criteria  
- MRZ extraction ≥90 % success on sample images.  
- Fallback manual edit flow.  
- Encrypted upload verified (file not readable in Storage viewer).  
- Jest test mocks ML Kit; e2e test with sample image passes.

---

## Feature 3 – Multi-Document Upload  
**Branch:** `feature/doc-multi-upload`  
**PR Title:** `feat(doc): multi-file import & metadata tags`  

### Scope & Tasks  
- Support PDF/JPG/PNG selection via Expo DocumentPicker.  
- Batch upload up to 5 docs at once.  
- Allow user to assign type & tags; auto-suggest from filename.  
- Store in `documents` collection; update offline queue logic.  

### Acceptance Criteria  
- UI shows progress per file.  
- Tags searchable in Documents screen.  
- Works fully offline then syncs.  

---

## Feature 4 – Expiration Reminders  
**Branch:** `feature/doc-expiry-reminders`  
**PR Title:** `feat(reminder): push & .ics export for expiring docs`  

### Scope & Tasks  
- Cloud Function scheduled daily: check docs expiring 90/30/7 days → write `notifications/{id}`.  
- Client listens and shows push via Expo Notifications.  
- Add “Add to Calendar” (.ics) export.  

### Acceptance Criteria  
- Function covered by unit test with Firestore emulator.  
- Push received on device (Expo Go).  
- .ics file imports correctly in Google Calendar.

---

## Feature 5 – Traveler Card v1  
**Branch:** `feature/traveler-card-v1`  
**PR Title:** `feat(card): customizable traveler card with QR`  

### Scope & Tasks  
- Screen to select profile & doc fields to expose.  
- Generate static JSON, store `travelerCards/{cardId}`.  
- Create QR linking to deep link `travelvault://card/<id>`.  
- View card offline with Restyle theme.  

### Acceptance Criteria  
- Selection UI respects design tokens.  
- QR scan on second device opens card.  
- Unit test ensures only chosen fields are present in JSON.

---

## Feature 6 – Offline Cache & Sync  
**Branch:** `feature/offline-sync`  
**PR Title:** `feat(core): offline cache and retry queue`  

### Scope & Tasks  
- Activate Firestore persistence.  
- Implement `syncQueue` Zustand slice.  
- Banner “Syncing…” when queue length > 0.  

### Acceptance Criteria  
- Airplane-mode test: add doc → appears locally.  
- When re-online, upload completes & banner hides.  
- Conflict resolution uses last-write-wins.

---

## Feature 7 – Groups & Roles  
**Branch:** `feature/groups-core`  
**PR Title:** `feat(groups): create, invite, role management`  

### Scope & Tasks  
- Create Group screen (name, avatar).  
- Invite via link containing `groupId`.  
- Roles: owner, admin, member, viewer.  
- Firestore security enforced per rules.  

### Acceptance Criteria  
- Owner can promote/demote, remove members.  
- Viewer cannot edit docs.  
- Unit & rules tests for permissions.

---

## Feature 8 – Granular Permissions  
**Branch:** `feature/doc-permissions`  
**PR Title:** `feat(doc): per-group & per-field visibility`  

### Scope & Tasks  
- Extend `documents.visibility` map.  
- UI toggle in `DocCard` for none/metadata/full per group.  
- Traveler Card inherits doc visibility.  

### Acceptance Criteria  
- Firestore rules updated & tested.  
- UI reflects real-time permission change.

---

## Feature 9 – Trip Planner  
**Branch:** `feature/trip-planner`  
**PR Title:** `feat(trip): destinations, checklist, doc validation`  

### Scope & Tasks  
- Trip create wizard: destination, dates, companions.  
- Auto-list required docs (passport, visa).  
- Checklist items with checkbox UI.  

### Acceptance Criteria  
- Validation marks missing/expired docs red.  
- Trip detail shows status chips.  

---

## Feature 10 – Dashboard Readiness  
**Branch:** `feature/dashboard`  
**PR Title:** `feat(dashboard): alerts, quick actions, summary widgets`  

### Scope & Tasks  
- Home screen with: next expiry, active trips, pending invites.  
- Quick action buttons: “Scan Doc”, “Create Trip”, “Show Card”.  
- Use Restyle grid, animated glow on alerts.  

### Acceptance Criteria  
- Loads in < 1 s on cold start (Profiler).  
- Widgets navigate correctly.  
- Snapshot test for layout passes.

---

### After Each Merge  
- Update `CHANGELOG.md` under `## Unreleased`.  
- Increment minor version in `package.json`.  
- Tag release on merge to `main`.

---

**Happy coding, Droid!**  
