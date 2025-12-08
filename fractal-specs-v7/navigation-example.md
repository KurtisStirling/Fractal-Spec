# Trapscan Navigation Map

Quick reference map for the Trapscan application structure.

---

## Application Components

### [Projects](./app/projects/projects.md)
End-user feature for creating and managing trap monitoring projects. Includes project creation, editing, listing, and deletion workflows.

### [Traps](./app/traps/traps.md)
Core value stream for trap device management. Handles trap registration, location tracking, status updates, and maintenance scheduling.

### [Observations](./app/observations/observations.md)
Recording and viewing trap check observations. Captures photos, counts, timestamps, and field notes from trap visits.

### [Reports](./app/reports/reports.md)
Analytics and export features. Generates summaries, charts, and CSV exports for conservation reporting.

---

## Shared Infrastructure (Horizontal)

### [Data Schema](./app/data-schema/data-schema.md)
Shared data models and validation rules. Used by projects, traps, observations, and reports.

### [Authentication](./app/auth/auth.md)
User authentication and authorization. Provides login, session management, and role-based access control.

### [Maps Integration](./app/maps/maps.md)
Geospatial functionality shared across features. Handles location selection, map rendering, and coordinate validation.

### [Photo Storage](./app/photo-storage/photo-storage.md)
Image upload, compression, and retrieval. Used by observations and trap registration.

---

## Architecture Notes

**Vertical components** (projects, traps, observations, reports) are end-user facing value streams.

**Horizontal components** (data-schema, auth, maps, photo-storage) are shared services consumed by multiple features.

See individual component specs for detailed design and dependencies.

---

**Note:** This is a navigation helper only. The source of truth for each component is its `.md` spec file.
