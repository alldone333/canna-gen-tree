# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

`canna-gen-tree` is a cannabis genetics database — a system for cataloging strains, tracking genetic lineage (parent → offspring trees), recording chemical profiles (cannabinoids, terpenes), and storing phenotypic traits. Licensed under Apache 2.0.

The project is in early development. No tech stack has been committed yet. When a stack is chosen, update this file immediately with build/run/test commands and architecture details.

## Current State

- Only file: `LICENSE` (Apache 2.0)
- Active development branch: `claude/cannabis-genetics-database-jPc4R`
- No build system, no dependencies, no tests yet

## Domain Concepts

Understanding these is essential before touching any data model:

- **Strain / Cultivar** — a named cannabis variety (e.g., "OG Kush"). The central entity.
- **Genetic lineage** — parent strains that were crossed to produce a child strain. Modeled as a directed acyclic graph (DAG), not a simple tree, because a strain can have two parents and those parents may share ancestors.
- **Chemotype / Chemical profile** — cannabinoid percentages (THC, CBD, CBG, etc.) and terpene composition. These are measured values that can vary by phenotype and grow conditions.
- **Phenotype** — a specific expression of a strain's genotype. One strain may have multiple phenotypes (e.g., "Pheno #1", "Pheno #2").
- **Breeder** — the entity that created / stabilized a strain.
- **Grow traits** — flowering time, yield, height, resistance characteristics. Distinct from chemical profile.

## Architecture Decisions (to be made)

When the stack is chosen, record decisions here:

- **Database**: The lineage structure requires a graph-capable query pattern. Options: PostgreSQL with recursive CTEs (adjacency list), or a dedicated graph DB (Neo4j, ArangoDB). PostgreSQL is preferred unless query complexity demands otherwise.
- **API layer**: REST vs GraphQL. GraphQL suits the deeply nested lineage queries well.
- **Frontend**: TBD. A force-directed graph visualization (e.g., D3.js, Cytoscape.js) is a likely UI requirement for the lineage tree.

## Conventions (establish these as the project grows)

- All database migrations must be versioned and reversible.
- Strain names are stored in their canonical form (case-preserved, trimmed). Lookups must be case-insensitive.
- Chemical profile values are stored as percentages (0–100), not decimals (0–1).
- The lineage DAG must be validated for cycles before any edge is inserted.

## Branch & Commit Workflow

- Develop on `claude/cannabis-genetics-database-jPc4R`; open PRs targeting `main`
- Commit messages: imperative mood, present tense (`Add strain lineage endpoint`, not `Added`)
