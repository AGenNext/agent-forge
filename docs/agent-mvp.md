# Agent MVP

## Product Definition

An Agent MVP is the smallest useful agent-native software unit that can be defined, run, observed, and stopped.

It is not a platform, marketplace, registry, operating system, or enterprise control plane.

## One-Line Product

**A configurable local agent runner that executes one goal using one runtime and one small set of tools.**

## User Promise

A developer can define an agent in one file and run it with one command.

```bash
agent run
```

## MVP Boundary

The MVP has only five primitives:

1. **Identity** — the name and subject of the agent.
2. **Goal** — what the agent is trying to accomplish.
3. **Runtime** — the model or execution engine used by the agent.
4. **Tools** — the limited capabilities the agent may call.
5. **Memory** — the local context the agent may read or write.

## Minimal Contract

```yaml
apiVersion: agent.agennext.io/v1alpha1
kind: Agent
metadata:
  name: hello-agent
spec:
  goal: Answer simple questions using the configured runtime.
  runtime:
    provider: local
    model: default
  tools: []
  memory:
    type: local
```

## Commands

```bash
agent init
agent run
agent stop
```

## What `agent init` Creates

```text
agent.yaml
README.md
```

## What `agent run` Does

1. Reads `agent.yaml`.
2. Validates required fields.
3. Starts the configured runtime loop.
4. Executes the goal using allowed tools.
5. Writes a local run trace.

## What `agent stop` Does

Stops the running agent process.

## MVP Outputs

```text
running agent process
local trace file
basic status output
```

## Explicit Non-Goals

The MVP does not include:

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

## Product Test

The MVP is successful when this works:

```bash
agent init hello-agent
cd hello-agent
agent run
```

And the user can see:

```text
hello-agent is running
```

## Roadmap After MVP

After the MVP works, Agent Forge can package the agent:

```bash
agent-forge build
agent-forge deploy
```

But packaging and deployment are not part of the Agent MVP.
