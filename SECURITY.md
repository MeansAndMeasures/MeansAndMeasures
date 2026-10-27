# Information Security Management System (ISMS) Scope Statement
**Target Definition:** Production Deployment Pipeline & Cloud Edge Infrastructure

## 1. Boundary & Scope
The scope of the ISMS is strictly limited to the cloud-native infrastructure, repository management layers, and automated delivery pipelines that power the production application. 

* **In-Scope Assets:**
  * GitHub Organization Configuration, Repositories, and Actions.
  * Cloudflare Edge Runtime Environments (Workers, Pages, KV, R2).
  * Production Secrets managed natively via Cloudflare Environment Variables / Wrangler secrets.
* **Explicitly Out-of-Scope:**
  * On-premises local development hardware (e.g., local workstations, local development servers). 
  * Justification: Local environments handle no live production customer data and possess zero direct access paths to production data planes without passing through multi-factor cloud authentication gates.

## 2. Technical Control Mapping (ISO/IEC 27002:2022 Framework)

### Domain 5: Organizational Controls
* **Control 5.18 (Asset Management):** Primary production assets are cloud-native and documented programmatically via Wrangler configuration architecture.
* **Control 5.30 (ICT Readiness for Business Continuity):** Public-facing applications utilize Cloudflare's globally distributed edge network. Outages or utility failures at local development facilities yield a 0-hour impact on end-user availability.

### Domain 8: Technological Controls
* **Control 8.25 (Secure Development Lifecycle):** Cryptographic non-repudiation is enforced globally. The GitHub Organization configuration mandates signed commits (GPG/SSH) at the root level; unverified code is structurally rejected by the repository.
* **Control 8.27 (Secure Coding):** Code transitions from local development to production via structured Git workflows. Technical secrets are decoupled from source repositories and injected natively at the Cloudflare Edge layer via Wrangler secrets management, preventing local disk exposure.
