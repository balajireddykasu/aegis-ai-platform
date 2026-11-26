# 🛡️ Aegis AI Platform (`aegis-ai-platform`)

**Multi-Tenant AWS EKS & LLMOps Control Plane with Automated FinOps Guardrails, Java RBAC Governance, and Self-Healing AIOps Agents.**

[![AWS EKS](https://img.shields.io/badge/AWS-EKS%20%7C%20Terraform-FF9900?style=flat-square&logo=amazon-aws)](https://aws.amazon.com/eks/)
[![Java Spring Boot](https://img.shields.io/badge/Control%20Plane-Java%2021%20%7C%20Spring%20Boot-6DB33F?style=flat-square&logo=spring-boot)](https://spring.io/projects/spring-boot)
[![Frontend Portal](https://img.shields.io/badge/Portal-Next.js%20%7C%20TypeScript-000000?style=flat-square&logo=next.js)](https://nextjs.org/)
[![Observability & FinOps](https://img.shields.io/badge/Observability-OpenTelemetry%20%7C%20Grafana-F46800?style=flat-square&logo=grafana)](https://opentelemetry.io/)
[![GitOps](https://img.shields.io/badge/GitOps-GitHub%20Actions%20%7C%20ArgoCD-EF7B4D?style=flat-square&logo=argo)](https://argo-cd.readthedocs.io/)

---

## 🎯 Executive Problem Statement

Enterprise engineering teams scaling generative AI in 2026–2027 face three systemic bottlenecks once models leave prototype notebooks:
1. **Uncontrolled FinOps & Token Burn:** Lack of per-tenant token budgets, semantic caching, and dynamic model tiering leads to runaway cloud and inference spend.
2. **Governance & Compliance Gaps:** Absence of centralized RBAC, PII redaction, and immutable audit trails blocks production adoption in regulated industries (FinTech, Banking, Healthcare).
3. **Operational Fragility:** Upstream LLM rate limits, latency spikes, and Kubernetes pod OOMs require manual firefighting instead of deterministic failover and autonomous remediation.

**Aegis AI Platform** solves these problems at the infrastructure and control-plane layer—providing a production-ready internal AI factory that engineering organizations can deploy, govern, and optimize for cost and reliability.

---

## 🏗️ System Architecture

```text
+-----------------------------------------------------------------------------------+
|                        INTERNAL DEVELOPER PORTAL (Next.js / TS)                   |
|        [ Tenant Onboarding ]   [ FinOps Cost Dashboards ]   [ Model Catalog ]     |
+-----------------------------------------+-----------------------------------------+
                                          | HTTPS / OIDC
                                          v
+-----------------------------------------------------------------------------------+
|                  ENTERPRISE CONTROL PLANE (Java 21 / Spring Boot)                 |
|  [ Multi-Tenant RBAC ]   [ Token Quota Engine ]   [ PII Guardrails & Audit Log ]  |
+-----------------------------------------+-----------------------------------------+
                                          | gRPC / REST
                                          v
+-----------------------------------------------------------------------------------+
|                   AWS EKS DATA & INFERENCE PLANE (Terraform + ArgoCD)             |
|                                                                                   |
|  +-----------------------------------------------------------------------------+  |
|  |                     LLM GATEWAY & SEMANTIC CACHE LAYER                      |  |
|  |  • Dynamic Model Routing (Primary -> Fallback)   • Semantic Cache (Redis)   |  |
|  |  • Per-Team Rate Limiting & Cost Ceilings        • OpenTelemetry Tracing    |  |
|  +--------------------------------------+--------------------------------------+  |
|                                         |                                         |
|            +----------------------------+----------------------------+            |
|            v                                                         v            |
|  +-----------------------+                                 +-------------------+  |
|  |  OBSERVABILITY STACK  |                                 |   AIOPS AGENT     |  |
|  | • Prometheus/Grafana  | ------------------------------> | • Anomaly Triage  |  |
|  | • FinOps Token Ledger |   Alerts & Telemetry Stream     | • Automated PRs   |  |
|  +-----------------------+                                 +-------------------+  |
+-----------------------------------------------------------------------------------+
