# Recursive Folder Aggregation

## Engineering Pattern

Traverse a hierarchical structure while aggregating information from every branch.

```
Folder
   │
   ├── File
   │
   ├── Folder
   │      │
   │      ├── File
   │      └── File
   │
   └── Folder
          │
          └── File
```

Each recursive call computes the result for one subtree and returns that value to its parent.

---

## State

The algorithm maintains a local accumulator.

```python
byte_size = 0
```

Each recursive invocation owns its own accumulator.

The parent combines the returned values from each child.

---

## Recursive Pattern

```
Current Folder
       │
       ▼
Iterate Children
       │
       ├── File
       │      │
       │      ▼
       │   Add File Size
       │
       └── Folder
              │
              ▼
      Recursively Calculate Size
              │
              ▼
      Add Returned Value
```

---

## Base Case

A file is represented by an integer.

```python
isinstance(contents, int)
```

Files contain no additional work.

The integer itself is the contribution to the total.

---

## Recursive Case

A folder contains another dictionary.

The recursive call returns the total size of that folder.

```python
byte_size += file_size(contents)
```

---

## Invariants

- Every file contributes exactly once.
- Every folder contributes the sum of its children.
- Parent folders never inspect grandchildren directly.
- Recursive calls completely solve subfolders before returning.

---

## Time Complexity

Each file and folder is visited exactly once.

**Time Complexity:** O(n)

Where:

- n = total number of files and folders

---

## Typical Engineering Patterns

Recursive aggregation appears throughout software engineering.

Examples include:

- Disk usage utilities
- Cloud storage accounting
- Cost aggregation
- Organizational hierarchies
- Nested JSON processing
- XML parsing
- Abstract Syntax Trees
- Configuration hierarchies

---

## AI Applicability

Modern AI systems frequently operate on recursive structures.

Examples include:

- Conversation trees
- Agent execution traces
- Nested reasoning chains
- Retrieval hierarchies
- Knowledge graphs
- Multi-agent task decomposition
- Behavioral observability pipelines

Recursive aggregation allows metrics, costs, confidence scores, or token usage to be rolled up through an entire execution graph.

---

## Lessons Learned

- Recursive functions can return information, not just perform actions.
- Parent nodes should trust child nodes to completely solve their own subproblems.
- Aggregation naturally occurs while the recursion stack unwinds.
- The recursive return value is often more important than the recursive call itself.
- Recursive algorithms frequently model hierarchical business structures more naturally than iterative solutions.