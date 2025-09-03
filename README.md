# Incident, Service and Change Management

## 1. Quality Assurance of Incidents
- Incidents are unplanned interruptions or degradation of a service. 

**QA in incidents means ensuring that:**
- Incidents are properly documented.
- The resolution steps are correct and reproducible.
- The root cause analysis (RCA) is complete and accurate.
- The incident process follows SLAs (Service Level Agreements).

**Example in DevOps/SRE:**
- Scenario: Kubernetes cluster goes down because of an expired TLS certificate.

**Incident QA checks:**

✅ Was the incident logged in the tracking tool (like ServiceNow, Jira, PagerDuty)?

✅ Was severity correctly assigned (Sev-1, Sev-2)?

✅ Were escalation procedures followed? (ex: escalation to on-call SRE within 15 mins)

✅ Were mitigation steps (e.g., renewing the TLS cert manually) documented clearly?

✅ Was a postmortem written with preventive measures (automated cert renewal in pipeline)?

➡️ Why QA matters: Without QA, the same TLS expiration issue could recur in production.

## 2. Quality Assurance of Service Requests

- Service requests are planned, standard, and low-risk requests (not failures) — like access provisioning, adding a user, or requesting a new environment. 
- QA ensures:
  - Requests follow standard templates/processes.
  - Access controls, compliance, and security checks are applied.
  - Execution is timely and within SLA.

**Example in DevOps/SRE:**
- Scenario: A developer requests read-only access to production logs in Splunk.
- Service Request QA checks:
  ✅ Was the request raised through the official ITSM tool (like ServiceNow)?
  ✅ Was manager approval attached?
  ✅ Were least privilege principles applied (read-only, not admin)?
  ✅ Was the access granted only for the requested duration?
  ✅ Was the request completed within SLA (e.g., 24 hrs)?

➡️ Why QA matters: Without QA, the engineer might get excessive permissions, violating compliance or security rules.

## 3. Quality Assurance of Change Requests
- Change requests are for planned changes to systems (deployments, upgrades, infrastructure modifications). QA ensures:
- Risk is properly assessed.
- Testing, rollback plans, and impact analysis are documented.
- Changes are reviewed/approved before execution.
- Post-change validation is done.

**Example in DevOps/SRE:**
- Scenario: Deploying a new version of a microservice to Kubernetes using ArgoCD.
- Change Request QA checks:
  ✅ Was the change raised in ServiceNow/Jira with details of service, impact, and timeline?
  ✅ Was the change peer-reviewed (code + infrastructure as code)?
  ✅ Was it tested in staging before production?
  ✅ Was a rollback plan defined (ArgoCD rollback, Helm rollback)?
  ✅ Was monitoring/alerting updated to track new metrics?
  ✅ Was the deployment executed within a Change Window (e.g., Sunday 2–4 AM)?
  ✅ Did post-deployment checks confirm service health?

➡️ Why QA matters: Without QA, a bad deployment could cause outages, and rollback might fail.

| Process              | QA Focus                               | SRE Link                                      | Example                                      |
| -------------------- | -------------------------------------- | --------------------------------------------- | -------------------------------------------- |
| **Incidents**        | Correct RCA, documentation, prevention | Protect SLOs, track error budget usage        | TLS cert expiry → automation prevents repeat |
| **Service Requests** | Secure, approved, least privilege      | Prevent hidden risks to reliability           | Log access → read-only to avoid misuse       |
| **Change Requests**  | Testing, rollback, controlled rollout  | Prevent SLO violations, preserve error budget | Canary deploy → rollback if latency > SLO    |

✅ Takeaway:
- Incidents QA → ensures error budget usage is tracked and minimized.
- Service Requests QA → ensures compliance & prevention of new risks.
- Change Requests QA → ensures deployments don’t violate SLOs.
Together, QA is the guardrail for reliability in SRE.

## 1. SLA, SLO, SLI Recap
- SLA (Service Level Agreement) → Contractual agreement with customers (e.g., 99.9% uptime per month).
- SLO (Service Level Objective) → Internal reliability target (e.g., 99.95% uptime per month).
- SLI (Service Level Indicator) → Metric to measure performance (e.g., % of successful HTTP requests).

🔗 Reporting ties these together: SLIs → SLOs → SLA compliance.

## 2. KPIs (Key Performance Indicators) in DevOps/SRE
- KPIs are operational metrics that help track engineering effectiveness.
- Typical DevOps/SRE KPIs include:

**Incident Management KPIs:**
- MTTR (Mean Time to Resolve)
- MTTA (Mean Time to Acknowledge)
- % of incidents resolved within SLA

**Change Management KPIs:**
- Change success rate (% of changes without incident)
- % of emergency changes vs planned changes
- Deployment frequency (DORA metric)

**Service Request KPIs:**
- Average request fulfillment time
- % fulfilled within SLA

**Reliability KPIs (SRE):**
- Error budget consumption
 % of time within latency/availability SLO
