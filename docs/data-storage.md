# Database and Storage Plan

## Database Choice
- **Type**: Relational (PostgreSQL)
- **Rationale**: Structured relations between users, projects, recordings, and models benefit from ACID transactions, schema enforcement, and SQL joins. PostgreSQL also offers `JSONB` columns for flexible metadata.

## Tables
### users
- `id` (PK)
- `email` (unique)
- `password_hash`
- `display_name`
- `created_at`

### projects
- `id` (PK)
- `owner_id` → `users.id`
- `name`
- `language`
- `engine_type`
- `metadata` (JSONB)
- `created_at`

### recordings
- `id` (PK)
- `project_id` → `projects.id`
- `file_path`
- `transcript`
- `duration_seconds`
- `created_at`

### models
- `id` (PK)
- `project_id` → `projects.id`
- `name`
- `status` (e.g., training, ready, failed)
- `artifact_path`
- `created_at`

## File Storage
- **Local development**: Store assets under `data/` on the filesystem using the structure:
  - `projects/{project_id}/recordings/{recording_id}.wav`
  - `projects/{project_id}/models/{model_id}/`
- **Production**: Use object storage (e.g., AWS S3, GCS). Database stores object keys or URLs instead of absolute paths.

## Cleanup Routines
- On project deletion, remove related recordings and model artifacts from storage and database tables within a transaction.
- Scheduled job scans for files without corresponding database records and deletes them.
- Temporary uploads stored under `tmp/` are purged after a TTL (e.g., 24 hours).
