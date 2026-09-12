I build and operate ingestion pipelines that move hundreds of millions of events per day into queryable storage, owning the full path from API intake to warehouse schema.

## Favian Schiller

I've designed event ingestion APIs, partitioned queue consumers, and idempotent write paths that tolerate duplicate deliveries without corrupting aggregates. I own the operational contract for these systems—latency budgets, retry backoff, dead-letter recovery—and accept the trade-off of stronger ordering guarantees for higher tail latency in exchange for simpler client semantics. My work focuses on keeping schemas evolvable, indexes warm, and traces continuous across service boundaries.

### 🛠 Tech & Infrastructure

- **Core**: `TypeScript`, `Node.js`, `PostgreSQL`, `Redis`
- **Data**: `Apache Kafka`, `ClickHouse`, `Parquet`
- **Infra**: `Docker`, `Kubernetes`, `Terraform`
- **Tooling**: `GitHub Actions`, `Grafana`, `Prometheus`

### ⚙️ Engineering Areas

- Designing idempotent ingestion APIs with explicit partition keys and schema versioning.
- Building Kafka consumers with checkpointing, retry queues, and poison-message isolation.
- Optimizing ClickHouse merges and materialized views for time-series aggregates.
- Automating blue/green deployments and rollback policies for stateless workers.

### 🔭 Current Focus

- Reducing replay amplification when a consumer lags: balancing batch size against memory pressure.
- Shrinking hot partitions in Kafka by rethinking key distribution for high-cardinality tenants.
- Moving schema migrations to expand-and-contract with dual-write periods and backfill jobs.
- Cutting p95 query latency in ClickHouse by tuning primary keys and compression codecs.

### 📌 Engineering Notes

- **Testing**: Contract-test the API boundary, property-test the idempotency logic, and integration-test against a real queue—mocks hide exactly the failures you care about.
- **Boundaries/Migrations**: Prefer additive schema changes and dual writes; delete columns only after two full release cycles of verified shadow reads.
- **Error Handling/Retries**: Retry only transient errors with exponential backoff and jitter; route permanent failures to a DLQ and alert on their age, not their count.
- **Observability/Deployments/On-call**: Every deploy ships with a runbook and a dashboard; if a metric doesn't have an alert, it's decoration. On-call should be boring.

### 🧭 How I Work

- Prefer boring, well-understood technology over novelty; the cost of a clever abstraction is paid in debugging sessions.
- Make small, reversible decisions; document the ones that are hard to undo.
- When in doubt, optimize for debuggability—logs, traces, and readable code beat premature performance.

*Latency is a feature; correctness is a contract.*