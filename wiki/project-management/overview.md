# Project Management Overview

> Derived from [`docs/project-management/PRD-VWO-com.md`](../../docs/project-management/PRD-VWO-com.md).  
> Do not edit directly — update the source doc and re-run ingest.

---

## Product at a Glance

**VWO (Visual Website Optimizer)** is an enterprise-grade Digital Experience Optimization (DXO) and Conversion Rate Optimization (CRO) platform. It serves product, marketing, UX, and analytics teams who need to test, personalize, and measure digital experiences.

- **Product URL:** https://app.vwo.com/
- **PRD Date:** January 7, 2026

---

## Business Objectives

| Goal | Detail |
|------|--------|
| Improve conversions | Optimize key funnels — sign-ups, purchases, lead forms |
| Data-driven decisions | Replace assumptions with empirical test results |
| Reduce engineering dependency | Self-serve experimentation for non-engineers |
| Unified insights | Single platform for testing, personalization, analytics |

---

## Stakeholders

| Role | Type |
|------|------|
| Digital Product Managers | Primary |
| UX / UI Designers | Primary |
| Growth & Marketing Teams | Primary |
| Data Analysts / CRO Specialists | Primary |
| Engineering / DevOps Teams | Primary |
| Business Executives | Secondary (strategic insights) |

---

## Functional Requirements Summary

| ID  | Feature | Priority |
|-----|---------|----------|
| FR1 | A/B, Split & Multivariate Testing | Must |
| FR2 | SmartStats (Bayesian engine) | Must |
| FR3 | Visual & Code Editor | Must |
| FR4 | Heatmaps & Session Recordings | Must |
| FR5 | Audience Targeting | High |
| FR6 | Real-time Reporting & Dashboards | Must |
| FR7 | Personalization Engine | High |
| FR8 | Integration Connectors | High |
| FR9 | Collaboration & Workflow Management | Medium |

Full descriptions → [`docs/project-management/PRD-VWO-com.md §6`](../../docs/project-management/PRD-VWO-com.md#6-functional-requirements)

---

## Non-Functional Requirements

| Category | Requirement |
|----------|-------------|
| Performance | ≤ 2s response for editing workflows |
| Security | 2FA, RBAC, activity logs |
| Scalability | Handle high visitor volumes without degradation |
| Data Privacy | GDPR, CCPA compliant |
| Reliability | 99.9% uptime SLA (enterprise) |

---

## Success Metrics (KPIs)

- Conversion rate increase (%) across prioritized pages
- Experiment velocity — tests launched per quarter
- Engineering time reduction for experimentation
- Personalized campaign engagement rate
- Platform NPS / customer satisfaction

---

## Risks & Mitigations

| Risk | Mitigation |
|------|-----------|
| Technical complexity | Robust SDKs, docs, pre-built templates |
| Data accuracy | SmartStats + cross-tool validation |
| User adoption | Guided tours, in-app support, analyst assistance |

---

## Pricing Model

Growth / Pro / Enterprise tiers. Free tier available for small usage. Scales by monthly tested users and feature set.

---

## Future Roadmap

- AI-driven test idea and personalization suggestion engine
- Native mobile SDK enhancements for app experimentation
- Predictive analytics and ROI forecasting

---

## Related Wiki Pages

- [Glossary](../glossary.md) — CRO, A/B Test, SmartStats definitions
- [Decisions](../decisions.md) — architectural and product tradeoffs
- [Wiki Index](../index.md)
