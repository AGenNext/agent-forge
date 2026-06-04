# Composable Agent MVP

## Product Definition

The Agent MVP is the smallest composable agent-native unit.

It is not a CLI, platform, registry, marketplace, Kubernetes operator, or enterprise control plane.

## One-Line Definition

**An agent is a composable identity-bound decision-action loop.**

## MVP Principle

An agent must be assembled from explicit primitives, not hidden inside one prompt.

Each primitive must be readable, replaceable, and testable.

## MVP Primitives

The MVP has seven primitives:

1. **Identity** — who or what the agent is.
2. **Objective** — what the agent is trying to achieve.
3. **Context** — what the agent currently knows.
4. **Capabilities** — what the agent can use.
5. **Decision** — how the agent chooses the next step.
6. **Action** — what the agent does.
7. **Trace** — what happened and why.

## Minimal Contract

```yaml
apiVersion: agent.agennext.io/v1alpha1
kind: Agent
metadata:
  name: hello-agent
spec:
  identity:
    id: agent:hello-agent

  objective:
    description: Respond to one user message clearly.

  context:
    input: user-message

  capabilities:
    - name: respond
      type: builtin

  decision:
    strategy: simple

  actions:
    - name: reply
      type: message-response

  trace:
    enabled: true
    store: local
```

## Minimal Runtime Loop

```text
load agent contract
  -> read context
  -> evaluate objective
  -> select capability
  -> make decision
  -> execute action
  -> write trace
```

## MVP Output

The MVP must produce:

```text
agent response
trace record
```

## First Product Test

Given this input:

```text
Hello agent
```

The MVP should return:

```text
hello-agent responded
```

And write a trace showing:

```text
identity
objective
context
decision
action
result
```

## Explicit Non-Goals

The MVP does not include:

- CLI as product
- Kubernetes deployment
- OCI packaging
- DID or verifiable credentials
- OpenFGA
- AuthZEN
- OpenFeature
- OPA
- Harbor
- Zot
- GitOps
- multi-agent orchestration
- marketplace
- registry
- enterprise identity lifecycle
- evaluation engine
- memory graph
- distributed network

## Roadmap After MVP

After this works, Agent Forge can package the agent into deployable artifacts.

But the first milestone is only:

**one composable agent definition, one runtime loop, one response, one trace.**
