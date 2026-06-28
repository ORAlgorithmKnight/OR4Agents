# Agent Optimization Problem (AOP)

## Definition

OR4Agents formulates AI Agent optimization as a constrained black-box combinatorial optimization problem.

### Mathematical Formulation

$$
\begin{aligned}
S^*
=
\arg\max_{S\in\mathcal{F}}
\Big(
f(S)-P(S)
\Big)
\end{aligned}
$$

where

- **S** : A complete Agent configuration.
- **S*** : The optimal Agent configuration.
- **𝓕** : The feasible solution space defined by all hard constraints.
- **f(S)** : The utility (reward) of Agent **S**.
- **P(S)** : The penalty induced by soft constraints.

---

## Agent Configuration

An Agent configuration is represented as

```text
S = (
    Foundation Model,
    Prompt,
    Tool Set,
    Memory Strategy,
    Workflow,
    Planner,
    Reflection,
    Reasoning Strategy,
    Temperature,
    ...
)
```

Every component can be viewed as one decision variable.

---

## Objective Function

The objective function evaluates the overall quality of an Agent.

Typical reward components include

```text
+ Task Success Rate

+ Answer Quality

+ Robustness

+ Generalization
```

One possible formulation is

```text
f(S)
=
Accuracy
+
Task Success
+
Robustness
```

---

## Penalty Function

Soft constraints are incorporated into the optimization objective through a penalty function.

Typical penalties include

```text
P(S)
=
λ₁ · Token Cost
+
λ₂ · API Cost
+
λ₃ · Latency
+
λ₄ · Tool Calls
+
λ₅ · Memory Usage
+
...
```

Different applications may define different penalty terms.

---

## Hard Constraints

The feasible solution space **𝓕** is defined by hard constraints.

Typical constraints include

```text
Context Window ≤ Maximum Context

API Calls ≤ Budget

Execution Time ≤ Time Limit

Workflow Dependency Satisfied

Tool Compatibility Satisfied

Memory Capacity Satisfied

User-defined Constraints
```

Only feasible solutions belong to **𝓕**.

---

## Solution Space

The search space consists of all feasible Agent configurations.

```text
Current Solution

↓

Generate Neighborhood

↓

Feasibility Test

↓

Evaluate

↓

Accept / Reject

↓

Update Solution
```

Unlike gradient-based optimization,

OR4Agents searches this solution space through local search or other combinatorial optimization algorithms.

---

## Interpretation

This formulation unifies a wide range of Agent optimization problems.

Examples include

| Agent Problem | Decision Variables |
|---------------|-------------------|
| Tool Selection | Tool Set |
| Memory Retrieval | Memory Strategy |
| Workflow Optimization | Workflow |
| Model Selection | Foundation Model |
| Prompt Optimization | Prompt |
| Reflection | Reflection Strategy |
| Planning | Planner |
| Multi-Agent Coordination | Workflow + Task Assignment |

All of these are treated as optimizing the same objective over different Agent configurations.

---

## Vision

Instead of optimizing prompts, tools, or memory independently,

OR4Agents optimizes the entire Agent as one solution.

> **LLMs generate candidate solutions.**
>
> **Operations Research searches for the optimal one.**