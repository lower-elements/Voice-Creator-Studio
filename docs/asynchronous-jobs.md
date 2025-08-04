# Asynchronous Job Handling and Progress Feedback

Voice Creator Studio offloads long-running tasks such as audio cleanup, transcription, and model training to background workers.

## Architecture
- **Task Queue**: [Celery](https://docs.celeryq.dev/) orchestrates jobs using Redis as both broker and results backend.
- **Job IDs**: Each request that launches a background task returns a unique ID so clients can query progress.

## Job Scheduling and Resource Management
- Celery routes work to CPU-only or GPU-enabled queues based on task requirements.
- Worker concurrency is capped to match available hardware, preventing oversubscription and balancing throughput.

## Progress Updates
- Workers periodically update task state in Redis with percentage complete and status messages.
- The FastAPI backend exposes a `/progress/{job_id}` endpoint and a WebSocket channel that stream these updates to the frontend.
- The React UI shows a progress bar and log snippets based on the streamed data.

## Failure Handling
- Failed tasks report error details through the same progress endpoint.
- Users can retry or cancel jobs from the interface if a task fails or stalls.

## Monitoring, Pausing, and Resuming
- The `/progress/{job_id}` endpoint and WebSocket stream provide live updates so users can monitor jobs.
- Canceling a job stops execution but retains intermediate checkpoints on disk.
- Resuming queues a new task that loads those checkpoints and continues training from the last saved state.
