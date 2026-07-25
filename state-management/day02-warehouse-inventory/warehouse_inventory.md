# Inventory reservation system

## Engineering pattern
Maintain constant state across multiple entities while preserving system invariants

```aiignore

Reserve
    ↓
Verify available inventory
    ↓
Reduce available inventory
    ↓
Increase customer reservation

```

```
Release
    ↓
Verify customer reservation
    ↓
Increase available inventory
    ↓
Reduce customer reservation
```
```
Purchase
    ↓
Verify customer reservation
    ↓
Reduce reservation
    ↓
(Available inventory unchanged)
```

## State

The system maintains two indepdenent pieces of state

### Available inventory

```aiignore
inventory = {
    "keyboard": 5,
    "mouse": 3,
    "monitor": 2
}
```
Represents the inventory that is immediately available for reservation

### Customer reservation

```aiignore
reservations = {
    "customer_a": {
        "keyboard": 2
    }
}
```

---

## Invariants
The following conditions must always remain true
- Available inventory can never become negative
- Reserved inventory can never become negative
- A customer cannot purchase more than they have reserved
- A customer cannot release more than they have observed
- Failed ops leave system state unchanged

---

## State Transitions

| Event | Available Inventory | Reservation |
|--------|--------------------|-------------|
| Reserve | - quantity | + quantity |
| Release | + quantity | - quantity |
| Purchase | unchanged | - quantity |

- purchase will never reduce available inventory as it was previously reserved

# TIme complexity
Each event performs constant-time dictionary lookups and updates
**Time:** O(n)

where 'n' = number of events

Space complexity depends on the number of customers and active reservations

---

## Engineering patterns

This pattern appears whenever resources transition through multiple ownership states

Examples include:

- Warehouse inventory
- E-commerce reservation systems
- Airline seat reservations
- Hotel room booking
- Kubernetes resource allocation
- Cloud capacity scheduling
- Database connection pools
- Ticketing systems

## AI applicability

The same state-transition pattern appears in agentic AI systems

- Tool reservation and execution
- GPU allocation
- Agent concurrency limits
- Workflow token budgeting
- HITL task assignment
- Multi-agent work queues

## guiding principle

maintain consistent state across multiple actors while preserving invariants during every event.  

