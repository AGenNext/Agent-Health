# Agent-Health

Agent-Health owns health checks, readiness checks, liveness checks, and health signal contracts for AGenNext agents, runtimes, and infrastructure.

## Scope

Agent-Health owns:

- health check definitions
- readiness contracts
- liveness contracts
- dependency checks
- runtime health signals
- infrastructure health signals
- health report schemas
- health-to-alert mappings

Agent-Health does not own:

- Kubernetes SDK implementation
- runtime execution
- deployment automation
- analytics aggregation
- dashboard UI

## Boundary

| Component | Responsibility |
|---|---|
| Agent-Health | Health check definitions and health report contracts |
| AgentKube | Kubernetes SDK operations used by checks |
| Agent-Runtime | Emits runtime health and consumes health decisions |
| Agent-Dashboard | Displays health status |
| Agent-Analytics | Aggregates health trends |
| Agent-Traces | Records health check events |

## Cloud agent health checks

Initial checks:

```txt
node.ssh_reachable
node.disk_available
node.memory_available
k3s.api_ready
kubernetes.nodes_ready
kubernetes.core_pods_ready
surrealdb.http_ready
surrealdb.query_ready
agent_runtime.worker_ready
agentkube.permissions_ready
```

## Flow

```txt
Agent-Health defines checks
  ↓
Agent-Runtime or Agent-deploy invokes checks
  ↓
AgentKube/SSH/SurrealDB clients perform checks
  ↓
Agent-Traces records health events
  ↓
Agent-Dashboard and Agent-Analytics consume health reports
```
