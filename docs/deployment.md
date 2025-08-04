# Deployment Targets and Scaling

Voice Creator Studio packages all services into Docker containers and targets cloud environments that support container orchestration.

## Deployment Targets
- **Containers**: Each service (FastAPI backend, React frontend, Celery workers, Redis) runs in a dedicated Docker image.
- **Cloud Services**: Production deployments run on Kubernetes (e.g., Amazon EKS or Google GKE). Object storage uses services like Amazon S3; PostgreSQL or Aurora host persistent data; Redis is provided by a managed service such as AWS ElastiCache.
- **Local Development**: Docker Compose starts the full stack on a single host for developers.

## Scaling Strategy
### Web Requests
- FastAPI instances are replicated behind a load balancer (NGINX or a cloud load balancer).
- Horizontal Pod Autoscalers adjust replica counts based on CPU and memory utilization.
- Static assets from the React build are served via a CDN to offload traffic from the backend.

### Background Jobs
- Celery workers run in separate deployments that can scale independently from the web layer.
- Queue depth and processing time drive autoscaling decisions; GPU jobs use dedicated nodes with limited concurrency.
- Workers are labeled by capability (CPU vs. GPU) so tasks are routed to matching queues.

## Hardware Requirements
### Training
- **GPU**: NVIDIA GPU with at least 16 GB VRAM (e.g., Tesla V100/A100). Multi-GPU setups improve throughput for large voices.
- **CPU/RAM**: 8+ vCPUs and 32 GB RAM minimum to feed the GPU and handle preprocessing.
- **Storage**: 500 GB SSD for datasets, checkpoints, and intermediate artifacts.

### Inference
- **GPU (optional)**: 8 GB VRAM (e.g., T4) accelerates real-time synthesis, but CPU-only inference is possible for smaller models.
- **CPU/RAM**: 4 vCPUs and 8–16 GB RAM support typical interactive workloads.
- **Storage**: 50 GB SSD accommodates models and cached assets.

