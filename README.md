# Agent Forge

**Agent Forge is a cloud-native composition and distribution forge for agent-native software.**

It exists to decompose software into governed building blocks, recombine them into usable agent artifacts, and keep those artifacts portable across Git, OCI, Kubernetes, and enterprise control planes.

## Why Agent Forge

Traditional software delivery assumes humans write code, package it, deploy it, and operate it through separate tools. Agent-native delivery changes the center of gravity:

- agents need identity, policy, memory, tools, runtime, traces, and approval boundaries;
- enterprises need provenance, reproducibility, auditability, and rollback;
- developers need reusable building blocks instead of weak generated software;
- platform teams need GitOps, OCI compatibility, Kubernetes compatibility, and supply-chain control.

Agent Forge is the bridge between **developer intent** and **operationally governed agent software**.

## Core idea

Agent Forge treats software as a composition graph.

A forgeable artifact is not just source code. It may include:

- source code
- buildpack or build recipe
- OCI image metadata
- Kubernetes manifests
- policy rules
- identity requirements
- secrets requirements
- tools and MCP contracts
- agent skills
- memory schema
- evaluation rules
- runtime configuration
- traces and provenance
- publishing metadata

The forge decomposes these into primitives, validates them, and recomposes them into deployable artifacts.

## Positioning

Agent Forge is not only a CI/CD tool.

It is a higher-level agent software supply-chain layer that can integrate with:

- Git providers such as GitHub, Forgejo, and Gitea
- build systems such as Cloud Native Buildpacks
- OCI registries
- Kubernetes and K3s
- GitOps controllers such as Flux or Argo CD
- policy engines such as OPA
- identity systems using DID, VC, SSO, SCIM, and RBAC
- observability, tracing, and evaluation platforms

## Operating model

```text
Intent
  -> Decompose
  -> Validate
  -> Compose
  -> Build
  -> Sign
  -> Publish
  -> Deploy
  -> Observe
  -> Evaluate
  -> Improve
```

Every step should be explainable, replayable, governed, and versioned.

## Initial architecture

```text
agent-forge/
  README.md
  forge.yaml
  schemas/
    forge.schema.json
  examples/
    basic-agent/forge.yaml
```

## Forge contract

A forge contract describes what is being built, how it is composed, and what controls must be satisfied before it can be published or deployed.

```yaml
apiVersion: forge.agennext.io/v1alpha1
kind: ForgeArtifact
metadata:
  name: example-agent
  owner: AGenNext
spec:
  type: agent
  source:
    provider: git
    repository: https://github.com/AGenNext/example-agent
  build:
    strategy: buildpack
    output: oci
  runtime:
    target: kubernetes
  governance:
    requirePolicy: true
    requireProvenance: true
    requireSignature: true
  evaluation:
    required: true
```

## Artifact types

Agent Forge should support these artifact classes first:

| Artifact | Purpose |
|---|---|
| `agent` | Deployable agent runtime unit |
| `skill` | Reusable tool or capability package |
| `workflow` | Agent execution graph or operating flow |
| `policy` | Guardrail, approval, access, or risk rule |
| `runtime` | Execution environment or runner profile |
| `connector` | External system integration |
| `bundle` | Composed deployable package |

## Non-goals

Agent Forge is not trying to replace Git, OCI, Kubernetes, buildpacks, or GitOps.

It composes them into an agent-native software lifecycle.

## Design principles

1. **Agent-native first** — agents are first-class software units.
2. **Git-compatible** — all contracts must live cleanly in Git.
3. **OCI-compatible** — artifacts should be packageable and distributable through registries.
4. **Kubernetes-compatible** — deployment targets should remain cloud-native.
5. **Policy-first** — publish and deploy only after controls pass.
6. **Identity-bound** — every artifact should know who created, approved, signed, and deployed it.
7. **Composable** — primitives must recombine without losing capability.
8. **Observable** — build, deploy, runtime, and evaluation events must be traceable.
9. **Reproducible** — artifacts must be rebuildable from source, contract, and pinned dependencies.
10. **Portable** — no single vendor or runtime should own the artifact.

## Roadmap

### Phase 1 — Contract

- define `forge.yaml`
- define JSON Schema
- define artifact taxonomy
- add basic examples
- add validation command

### Phase 2 — Composer

- implement decomposition model
- implement composition graph
- support buildpack-based builds
- emit OCI metadata

### Phase 3 — Control plane integration

- GitOps handoff
- policy validation
- provenance and signing
- Kubernetes deployment templates

### Phase 4 — Agent-native capabilities

- skill registry integration
- MCP contract validation
- identity and credential binding
- evaluation gates
- runtime trace hooks

## Status

This repository is in foundation stage.

The first goal is to define the canonical contract for forgeable agent artifacts.
