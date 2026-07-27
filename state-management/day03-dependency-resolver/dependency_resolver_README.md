# Recursive Dependency Resolution

## Engineering Pattern

Resolve hierarchical dependencies while ensuring that every dependency is processed before the object that depends on it.

```
Deploy Service
       │
       ▼
Resolve Dependencies
       │
       ▼
Resolve Dependency Dependencies
       │
       ▼
Continue Until No Dependencies Remain
       │
       ▼
Complete Services During Stack Unwind
```

---

## State

The algorithm maintains three independent pieces of state.

### Visiting

```python
visiting = set()
```

Services currently being explored.

Purpose:

- Detect circular dependencies.
- Prevent infinite recursion.

---

### Deployed

```python
deployed = set()
```

Services whose dependency trees have already been completely processed.

Purpose:

- Prevent duplicate work.
- Ensure each service is deployed exactly once.

---

### Deployment Order

```python
order = []
```

Stores the final deployment sequence.

A service is appended only after all of its dependencies have been successfully processed.

---

## Invariants

The following conditions must always remain true.

- A service is deployed exactly once.
- Every dependency is deployed before the service that depends on it.
- Circular dependency graphs are rejected.
- Services already processed are never processed again.

---

## State Transitions

```
Visit Service
      │
      ▼
Already Visiting?
      │
      ├── Yes → Circular Dependency
      │
      ▼
Already Deployed?
      │
      ├── Yes → Return
      │
      ▼
Mark Visiting
      │
      ▼
Visit Each Dependency
      │
      ▼
Remove Visiting
      │
      ▼
Mark Deployed
      │
      ▼
Append to Deployment Order
```

---

## Time Complexity

Each service is visited once.

Each dependency relationship is traversed once.

**Time Complexity:** O(V + E)

Where:

- V = number of services
- E = number of dependency relationships

Space complexity is proportional to the recursion depth and the number of tracked services.

---

## Typical Engineering Patterns

Dependency graphs appear throughout distributed systems.

Examples include:

- Package managers
- CI/CD pipelines
- Infrastructure as Code (Terraform)
- Kubernetes deployment ordering
- Docker image builds
- Workflow orchestration
- Build systems
- Database migration frameworks

---

## AI Applicability

Agentic AI systems naturally form dependency graphs.

Examples include:

- LangGraph execution graphs
- Planner / Executor architectures
- Tool dependency execution
- Multi-agent delegation
- Retrieval pipelines
- Evaluation pipelines
- Autonomous workflow execution

Cycle detection is critical whenever autonomous systems dynamically compose execution plans.

---

## Lessons Learned

- Recursive problems often describe smaller versions of themselves.
- Separate "currently processing" from "already processed" state.
- Circular dependency detection is simply recognizing that a node has been encountered twice on the same active path.
- Recursion naturally produces post-order traversal, making it ideal for dependency resolution.
- Trust recursive calls to completely solve the smaller problem before continuing.