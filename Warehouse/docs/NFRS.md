# Non-Functional Requirements (NFRs)

These NFRs apply across the entire Warehouse System, ensuring it meets the quality standards required for daily warehouse operations.

## 1. Performance & Scalability
- **NFR-PERF-01**: API response times for standard CRUD operations (e.g., adding an item, updating a customer) MUST be under 500ms under normal load.
- **NFR-PERF-02**: The system MUST support up to 50 concurrent warehouse workers scanning items simultaneously without degradation in performance.
- **NFR-PERF-03**: Barcode scans on the picking/receiving screens MUST process and return a visual feedback (success/error) within 200ms.

## 2. Availability & Reliability
- **NFR-AVAIL-01**: The system MUST have an uptime of 99.9% during business hours (defined as 6:00 AM to 10:00 PM local time).
- **NFR-AVAIL-02**: Inventory updates (put-away, picking, adjusting) MUST be transactional. If a movement fails halfway through, no partial inventory changes should be saved.
- **NFR-AVAIL-03**: The mobile/web interface for truck drivers (Delivery) SHOULD support an offline mode to view assigned routes, syncing data back to the server once connectivity is restored.

## 3. Security
- **NFR-SEC-01**: All web traffic MUST be encrypted using TLS 1.3 (HTTPS).
- **NFR-SEC-02**: Passwords MUST be hashed using bcrypt (or Argon2) with a minimum work factor of 12.
- **NFR-SEC-03**: The system MUST enforce Role-Based Access Control (RBAC) at the API level, ensuring that a user cannot execute actions outside their assigned role (e.g., a driver cannot delete an item).
- **NFR-SEC-04**: Sessions MUST automatically timeout after 15 minutes of inactivity on office computers, but remain active for up to 8 hours on warehouse scanners to prevent workflow interruption.

## 4. Usability & Accessibility
- **NFR-USE-01**: Warehouse screens (Picking, Receiving, Put-Away) MUST be optimized for mobile devices and tablets, with touch targets (buttons) being at least 44x44 pixels.
- **NFR-USE-02**: The UI MUST provide clear visual and auditory feedback when a barcode is scanned (Green/Success beep vs. Red/Error buzz).
- **NFR-USE-03**: The system MUST display user-friendly error messages that guide the user on how to fix the issue (e.g., "Scan failed: Wrong item. Please scan SKU 12345").

## 5. Maintainability & Data Integrity
- **NFR-MAINT-01**: The codebase MUST include automated tests for all business-critical logic (inventory movement calculations, order total sums).
- **NFR-MAINT-02**: Database backups MUST be performed daily, retaining data for 30 days.
- **NFR-MAINT-03**: Historical records (receiving history, shipment history) MUST be immutable (append-only) and retained indefinitely for auditing purposes.

## 6. Interoperability & Hardware Integration
- **NFR-INT-01**: The frontend MUST support standard USB and Bluetooth barcode scanners configured as "Keyboard Emulation" devices without requiring custom driver installations.
- **NFR-INT-02**: The system SHOULD generate standard PDF formats for Bills of Lading to ensure they can be easily printed or emailed to external partners.
- **NFR-INT-03**: The API design must allow for future integration with external shipping APIs (e.g., FedEx, UPS) for automated tracking number generation.