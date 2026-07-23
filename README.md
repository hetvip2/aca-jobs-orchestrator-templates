# Azure Container Apps Jobs orchestrator templates

A curated collection of templates for running orchestrated workloads on [Azure Container Apps Jobs](https://learn.microsoft.com/azure/container-apps/jobs). Choose the orchestrator your team already operates, or start with the decision guide below.

All templates use Azure Container Apps Jobs for task execution. Unless noted otherwise, the orchestrator remains customer-owned and the template deploys only the Azure target resources required to start and monitor jobs.

## Choose a template

| Use case | Recommended template | Why |
|---|---|---|
| Deploy a complete Airflow environment on Azure Container Apps | [Airflow hosted on ACA](https://github.com/hetvip2/airflow-hosted-on-aca) | Includes the Airflow control plane and ACA Jobs integration |
| Connect an existing Airflow deployment | [Airflow on ACA Jobs](https://github.com/hetvip2/airflow-on-aca-jobs) | Keeps the existing Airflow environment and adds ACA Jobs execution |
| Run Kubernetes-native workflows from AKS | [Argo Workflows](https://github.com/hetvip2/argo-workflows-on-aca-jobs) | Uses Argo workflow templates and AKS workload identity |
| Model long-running business processes with BPMN | [Camunda 8](https://github.com/hetvip2/camunda-8-on-aca-jobs) | Fits BPMN processes, service tasks, and human workflow systems |
| Use JSON-defined microservice workflows | [Conductor](https://github.com/hetvip2/conductor-on-aca-jobs) | Fits Conductor task workers and `FORK_JOIN` workflows |
| Build Python-native data and asset pipelines | [Dagster](https://github.com/hetvip2/dagster-on-aca-jobs) | Uses Dagster ops, assets, and dynamic fan-out |
| Build Python-native task and flow automation | [Prefect](https://github.com/hetvip2/prefect-on-aca-jobs) | Uses Prefect tasks, flows, and mapped execution |
| Build visual low-code automation and integrations | [n8n](https://github.com/hetvip2/n8n-on-aca-jobs) | Fits webhook, SaaS integration, and visual automation workflows |
| Use Azure-native data pipelines | [Azure Data Factory and Fabric](https://github.com/hetvip2/data-factory-on-aca-jobs) | Fits ADF pipelines and includes a Fabric pipeline definition |
| Use Azure-native integration workflows | [Logic Apps Standard](https://github.com/hetvip2/logic-apps-standard-on-aca-jobs) | Fits connectors, events, APIs, and enterprise integration |
| Build code-first durable orchestration on Azure Functions | [Durable Functions](https://github.com/hetvip2/durable-functions-on-aca-jobs) | Provides durable state, retries, and native fan-out/fan-in |
| Explore Dapr Workflow architecture | [Dapr Workflow](https://github.com/hetvip2/dapr-workflow-on-aca-jobs) | Demonstrates Dapr orchestration, with an important preview limitation |

## Template catalog

### Airflow

- **[Airflow hosted on ACA](https://github.com/hetvip2/airflow-hosted-on-aca)** deploys Apache Airflow on Azure Container Apps and uses Azure Container Apps Jobs for task execution. Choose this when you need a complete Airflow environment.
- **[Airflow on ACA Jobs](https://github.com/hetvip2/airflow-on-aca-jobs)** connects an existing Airflow deployment to Azure Container Apps Jobs. Choose this when Airflow is already installed and operated elsewhere.

### Open-source orchestrators

- **[Argo Workflows](https://github.com/hetvip2/argo-workflows-on-aca-jobs)** for teams already operating Argo on AKS.
- **[Camunda 8](https://github.com/hetvip2/camunda-8-on-aca-jobs)** for BPMN-based process orchestration.
- **[Conductor](https://github.com/hetvip2/conductor-on-aca-jobs)** for Conductor task and workflow definitions.
- **[Dagster](https://github.com/hetvip2/dagster-on-aca-jobs)** for Python data orchestration and asset-centric workflows.
- **[n8n](https://github.com/hetvip2/n8n-on-aca-jobs)** for visual automation and integration workflows.
- **[Prefect](https://github.com/hetvip2/prefect-on-aca-jobs)** for Python-native flows and task orchestration.

### Azure-native orchestrators

- **[Azure Data Factory and Fabric](https://github.com/hetvip2/data-factory-on-aca-jobs)** for data integration pipelines. The ADF path is live validated; the Fabric definition is structurally validated and still requires native execution in a Fabric workspace.
- **[Durable Functions](https://github.com/hetvip2/durable-functions-on-aca-jobs)** for code-first durable workflows on Azure Functions.
- **[Logic Apps Standard](https://github.com/hetvip2/logic-apps-standard-on-aca-jobs)** for connector-rich integration and event-driven workflows.

### Preview architecture

- **[Dapr Workflow](https://github.com/hetvip2/dapr-workflow-on-aca-jobs)** is explicitly a preview architecture. Azure Container Apps Jobs do not host Dapr sidecars, so review the documented runtime boundary before adopting it.

## Common capabilities

The existing-orchestrator templates share these design goals:

- Azure Developer CLI (`azd`) deployment for Azure target resources
- Managed identity and scoped Azure RBAC
- Single-job and native fan-out/fan-in examples
- Configurable fan-out from 1 to 50 shards, defaulting to 5
- Automated validation in GitHub Actions
- Production guidance and cleanup instructions

A supported shard count is not a throughput guarantee. Validate 25- and 50-shard configurations against your Azure quotas, workload duration, image startup time, downstream dependencies, and orchestrator concurrency settings before production rollout.

## Quick selection rules

1. Already operate an orchestrator? Use its existing-mode template.
2. Need Airflow but do not operate it yet? Use **Airflow hosted on ACA**.
3. Prefer Azure-managed visual data pipelines? Use **Data Factory and Fabric**.
4. Need connector-heavy application integration? Use **Logic Apps Standard**.
5. Need durable code-first orchestration? Use **Durable Functions**.
6. Need Python-first data assets? Use **Dagster**; for general Python flows, use **Prefect**.
7. Treat **Dapr Workflow** as preview until its documented platform limitation fits your architecture.

Each repository README is the source of truth for prerequisites, deployment, native runtime evidence, limitations, and cleanup.

## Repository status

The collection is public and its current `main` branches pass their repository validation workflows. Runtime-validation scope differs by orchestrator and is documented in each repository. No benchmark claim is made for unmeasured 25- or 50-shard workloads.
