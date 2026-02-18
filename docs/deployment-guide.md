# Paradox AI Deployment Guide

## 1. Environments
- `dev`: local Docker compose
- `staging`: managed cloud services + preview apps
- `prod`: multi-region deployment with blue/green rollout

## 2. Baseline Stack
- Frontend: Vercel (Next.js)
- API + workers: Kubernetes or Render/Fly
- Postgres: Neon/Supabase/RDS
- Redis: Upstash/Elasticache
- Object storage: S3/R2
- Vector store: Qdrant Cloud or pgvector
- Observability: OpenTelemetry + Grafana + Sentry

## 3. CI/CD Pipeline
1. Lint + typecheck + tests
2. Build frontend + backend images
3. Run Prisma migrate in release phase
4. Deploy API and workers
5. Deploy frontend
6. Smoke tests for chat, generation, billing webhook

## 4. Secrets and Security
- Store secrets in cloud secret manager
- Rotate keys every 90 days
- Separate API keys by environment and provider
- Enforce signed webhooks for Stripe + integrations

## 5. Scaling Roadmap

### Phase 1 (0-10k MAU)
- Single region
- Shared worker queue
- Basic autoscaling

### Phase 2 (10k-100k MAU)
- Read replicas
- Dedicated queue clusters
- Model routing by cost/performance
- Edge cache strategy per geography

### Phase 3 (100k+ MAU)
- Multi-region active/active for chat + APIs
- Tenant-aware workload placement
- Dedicated enterprise clusters
- Cost-aware inference broker
