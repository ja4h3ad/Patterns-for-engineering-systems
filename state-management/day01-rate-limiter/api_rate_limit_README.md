
# Maintain State Incrementally
```
text
Request arrives
        ↓
Expire old requests
        ↓
Check limit
        ↓
Accept or reject
        ↓
Update state
```
Each customer's deque contains only accepted requests from the last 10 seconds.

## Time Efficiency

**O(n)**

Every timestamp is:

- Appended exactly once
- Removed exactly once

## Typical Engineering Patterns

This approach appears in systems that use sliding windows, rolling buffers, event streams, or recent-history tracking.

Examples include:

- API gateways
- LLM conversation memory
- Token window management
- Session tracking
- Inventory systems
- Network packet buffers
- Streaming analytics
- Sliding-window anomaly detection
- Fraud detection
- Observability pipelines

## AI Applicability

Agentic behavioral observability pipelines can maintain a double-ended queue of tool invocation timestamps per agent.

Example question:

- Has an agent made more than `n` tool calls in the last minute?
```

