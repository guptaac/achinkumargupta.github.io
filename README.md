## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/achinkumargupta/achinkumargupta.github.io/edit/main/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/achinkumargupta/achinkumargupta.github.io/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.



out.



Agentic AI Operational Runbook Platform

 

Reference Architecture for Regulatory Processes (FR2052a, 9Q, CCAR)

 

1. Executive Summary

 

Large enterprises operate complex ecosystems consisting of:

 

- microservices

- batch schedulers (Autosys)

- data platforms (DB, Polypaths)

- caches (Redis)

- APIs

- reconciliation engines

 

Operational issues can occur at any layer and impact critical regulatory processes such as:

 

- FR2052a liquidity reporting

- 9Q reporting

- CCAR stress testing

- Basel reporting

- treasury analytics

 

Traditional runbooks are static, hard to maintain and dependent on tribal knowledge.

 

This document proposes an Agentic AI Runbook Platform that:

 

- dynamically diagnoses incidents

- orchestrates diagnostic tools via MCP servers

- composes runbooks automatically

- enables users to create runbooks on demand

- provides explainable root cause analysis

- optionally performs automated remediation

 

 

2. Design Goals

 

Functional Goals

 

Support multiple regulatory processes

Diagnose failures across heterogeneous systems

Enable reusable runbook components

Allow users to create runbooks dynamically

Integrate with observability platforms

Provide explainable AI reasoning

Support audit traceability

 

Non Functional Goals

 

Scalable across hundreds of services

Extensible via MCP tools

Secure and auditable

Incrementally adoptable

Cloud or on-prem compatible

 

 

3. Conceptual Model

 

Layer 1 — Process Runbooks

 

Business workflows describing regulatory processes such as FR2052a, 9Q and CCAR.

 

Responsibilities:

 

define process steps

define SLA checkpoints

define dependencies on capabilities

 

 

Layer 2 — Capability Runbooks

 

Reusable operational logic shared across multiple processes.

 

Examples:

 

data ingestion

reconciliation

aggregation

file transfer

scheduler orchestration

reference data validation

 

Responsibilities:

 

diagnostic logic

root cause patterns

recommended actions

 

 

Layer 3 — Service Runbooks

 

Technical runbooks specific to infrastructure or applications.

 

Examples:

 

Autosys scheduler

Redis cache

Oracle database

microservice APIs

Polypaths file store

 

Responsibilities:

 

health checks

restart procedures

known failure patterns

 

 

4. High Level Architecture

 

Users

 

Operations teams

SRE teams

Application teams

Finance teams

 

Runbook Authoring Layer

 

UI

YAML

API

 

Knowledge Layer

 

Process Knowledge Base

Capability Knowledge Base

Service Knowledge Base

Dependency Graph

 

Agent Orchestration Layer

 

Supervisor Agent

 

Specialist Agents

 

Data Agent

Pipeline Agent

Reconciliation Agent

Infra Agent

Root Cause Agent

Action Agent

 

MCP Tool Layer

 

Observability MCP

Scheduler MCP

Data MCP

Microservice MCP

Cache MCP

File MCP

 

Enterprise Systems

 

Microservices

Autosys

Databases

Redis

Polypaths

Reporting Engines

 

 

5. Knowledge Layer Design

 

Example Process Runbook

 

PROCESS_FR2052A_INTRADAY

 

steps:

 

data_ingestion

liquidity_calculation

reconciliation

submission

 

dependencies:

 

payments_service

liquidity_engine

reconciliation_service

reporting_api

 

 

Example Capability Runbook

 

CAP_RECONCILIATION

 

diagnostics:

 

compare totals between systems

detect missing records

validate currency conversion

 

root causes:

 

mapping mismatch

missing data

late file arrival

 

actions:

 

rerun aggregation

refresh reference data

 

 

Example Service Runbook

 

SERVICE_AUTOSYS

 

diagnostics:

 

check job status

check dependency tree

check last successful run

 

actions:

 

restart job

release dependency hold

 

 

6. MCP Tool Layer

 

Data MCP

 

run_sql

compare_tables

detect_duplicates

 

Scheduler MCP

 

job_status

restart_job

dependency_tree

 

Observability MCP

 

search_logs

detect_error_spike

retrieve_metrics

 

Microservice MCP

 

health_check

call_endpoint

retrieve_logs

 

Cache MCP

 

check_key

flush_cache

ttl_check

 

File MCP

 

verify_file_arrival

validate_format

checksum

 

 

7. Agent Architecture

 

Supervisor Agent

 

entry point for incidents

identifies relevant process

selects runbooks

coordinates specialist agents

produces final output

 

 

Specialist Agents

 

Data Agent

 

validates data completeness

runs SQL diagnostics

 

 

Pipeline Agent

 

checks Autosys jobs

checks workflow dependencies

 

 

Reconciliation Agent

 

compares aggregated balances

detects mismatches

 

 

Infrastructure Agent

 

checks Redis

checks DB connectivity

checks microservice health

 

 

Root Cause Agent

 

correlates outputs from other agents

generates explanation

computes confidence score

 

 

Action Agent

 

recommends remediation steps

optionally executes approved automation

 

 

8. End to End Execution Flow

 

Step 1 Alert Triggered

 

alerts generated from Splunk, Autosys, API monitoring or manual trigger

 

 

Step 2 Supervisor Agent Context Selection

 

process = FR2052a

capability = reconciliation

 

dependent services:

 

database

Autosys

liquidity microservice

Redis

 

 

Step 3 Dynamic Runbook Composition

 

process runbook

capability runbook

service runbooks

 

 

Step 4 Parallel Diagnostics via MCP

 

Data MCP executes SQL checks

Scheduler MCP checks Autosys

Observability MCP retrieves logs

Microservice MCP checks endpoints

Cache MCP validates Redis

 

 

Step 5 Root Cause Analysis

 

Root cause agent correlates findings

 

example root cause:

 

FX rate file missing before reconciliation

 

confidence score:

 

0.84

 

 

Step 6 Recommended Actions

 

rerun FX ingestion job

rerun reconciliation

clear Redis cache

notify payments team

 

 

Step 7 Optional Auto Remediation

 

execute approved actions via MCP tools

 

 

Step 8 Knowledge Capture

 

store incident context

store diagnostics

store resolution steps

improve future recommendations

 

 

9. Runbook Authoring Model

 

Users can create runbooks dynamically via UI or YAML

 

fields:

 

process name

capability

services

diagnostics

actions

severity

ownership

 

 

10. Repository Structure

 

runbook-platform

 

agents

 

supervisor_agent.py

data_agent.py

pipeline_agent.py

rootcause_agent.py

action_agent.py

 

runbooks

 

process

fr2052a.yaml

9q.yaml

ccar.yaml

 

capability

reconciliation.yaml

ingestion.yaml

aggregation.yaml

 

services

autosys.yaml

redis.yaml

db.yaml

microservice.yaml

 

mcps

 

data_mcp

scheduler_mcp

observability_mcp

cache_mcp

microservice_mcp

file_mcp

 

knowledge_graph

 

dependencies.json

 

ui

 

runbook_editor

incident_dashboard

 

 

11. Implementation Roadmap

 

Phase 1

 

define runbook schema

create initial capability runbooks

build supervisor agent

connect Splunk

connect database

 

 

Phase 2

 

add MCP servers

integrate Autosys

integrate Redis

add knowledge graph

 

 

Phase 3

 

multi agent reasoning

confidence scoring

auto remediation workflows

user runbook creation UI

 

 

12. Benefits

 

reduced regulatory risk

faster incident resolution

reusable operational knowledge

reduced dependency on individuals

consistent diagnosis approach

scalable across regulatory domains

compatible with existing observability tools

supports enterprise AI strategy






