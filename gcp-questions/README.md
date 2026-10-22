# 🌈 Google Cloud Assessment — Questions, All Options & Correct Answers

> 📘 **Study guide from the assessment screenshots shared in this conversation.** Each question keeps the visible answer choices, marks the best answer, and adds a short explanation. Colours are represented with emoji and Markdown so the page renders nicely on GitHub.
>
> ⚠️ **Image-readability note:** The screenshots are photographed at an angle. I’ve transcribed all visible options where they are legible. If a phrase was clipped or hard to read, it is identified as paraphrased rather than presented as an exact quote.

---

## 🧭 Section 1 — Setting Up Google Cloud

### Q1. Google Cloud resource hierarchy
**Question:** Which node is at the root of the hierarchy and serves as the highest-level container for all resources?

**Options**
- A. Folder
- B. Project
- C. Billing account
- D. **Organization** ✅

**Correct answer: D — Organization**

**Why:** The usual resource hierarchy is **Organization → Folders (optional) → Projects → Resources**. Billing accounts are associated with projects but are not the root of the resource hierarchy.

---

### Q2. Cloud Identity and IAM
**Question:** Which statement accurately describes how Cloud Identity works with IAM policies?

**Options visible in the screenshot**
- A. Users in Cloud Identity cannot be members of groups
- B. Cloud Identity is only used for billing relationship to IAM
- C. Cloud Identity identities can be granted roles just like user accounts ✅ *(intended answer)*
- D. Cloud Identity automatically grants service-account roles

**Correct answer: C — Cloud Identity identities can be granted roles just like user accounts**

**Why:** Cloud Identity manages identities and groups. IAM roles authorise those identities to access Google Cloud resources.

---

### Q3. IAM and service-account permissions
**Question:** Which principle should guide you when assigning IAM roles to a service account?

**Options**
- A. Use custom roles exclusively for every workload, regardless of need
- B. Assign the Owner role broadly to simplify administration
- C. Always include broad basic roles such as Editor for redundancy
- D. **Grant only the minimum permissions necessary for the workload** ✅

**Correct answer: D — Least privilege**

**Why:** Give the workload only the permissions it needs. Avoid broad Owner/Editor roles as a shortcut.

---

### Q4. Owner role and project administration
**Question:** To maintain administrative control, every Google Cloud project must have at least one member with which role?

**Options**
- A. Viewer
- B. Editor
- C. **Owner** ✅
- D. Service Account Admin

**Best answer for this assessment: C — Owner**

**Note:** The Owner basic role is broad and may not be required in every modern access model or organisation policy. In practice, follow the organisation’s governance requirements and prefer granular predefined roles when suitable.

---

## 💻 Section 2 — Planning and Using Google Cloud

### Q5. Cloud Spanner
**Question:** Which Google Cloud database combines relational consistency with non-relational scalability and is ideal for globally distributed, strongly consistent transactions?

**Options**
- A. Cloud SQL
- B. **Cloud Spanner** ✅
- C. Cloud Firestore
- D. Cloud Bigtable

**Correct answer: B — Cloud Spanner**

**Why:** Spanner provides relational database semantics and strongly consistent transactions with horizontal scalability and multi-region capabilities.

---

### Q6. Cloud Run design considerations
**Question:** Cloud Run has which limitation that developers must consider?

**Options visible in the screenshot**
- A. It supports stateful workloads and GPU accelerators
- B. It requires container images to start quickly and be stateless
- C. It provides built-in support for complex microservice architectures
- D. It can only run Node.js applications

**Best answer: B — Design for quick startup and statelessness**

**Why:** Stateless, quick-starting containers work best with Cloud Run’s request-driven autoscaling. This is a design consideration, not a claim that every stateful pattern is impossible.

---

### Q7. Uploading files to Cloud Storage from the command line
**Question:** Which command-line tool is commonly used to upload files to Cloud Storage buckets?

**Options**
- A. `gcloud compute`
- B. `kubectl`
- C. **`gsutil`** ✅
- D. `bq`

**Correct answer: C — `gsutil`**

Example:
```bash
gsutil cp file.txt gs://YOUR_BUCKET/
```

**Note:** Google also provides the newer `gcloud storage` command group.

---

### Q8. Managed Instance Groups (MIGs)
**Question:** What can a Managed Instance Group do automatically?

**Options visible in the screenshot**
- A. **Create and destroy instances during scaling and auto-healing** ✅
- B. Encrypt data at rest
- C. Migrate VMs across zones without downtime
- D. Attach GPUs to instances

**Correct answer: A**

**Why:** A MIG uses an instance template and can maintain the desired number of VMs, autoscale, and recreate unhealthy instances with auto-healing.

---

### Q9. VPC network tags vs secure tags
**Question:** Network tags are simple string labels used in VPC firewall rules, whereas secure tags differ in what way?

**Options visible in the screenshot**
- A. Managed by the Compute Engine metadata server
- B. Automatically assigned to service accounts
- C. Key-value pairs managed by IAM and Resource Manager
- D. **Deprecated in favour of firewall policies**

**Important correction:** **D is not a reliable general description of secure tags.** Secure tags are centrally managed resources with IAM-controlled administration and can be used in firewall policies. Network tags are simpler strings used to target VM instances. The screenshot wording/options appear ambiguous; verify the intended answer with the course answer key before relying on this item.

---

### Q10. Serverless Google Cloud data services (choose TWO)
**Question:** Which Google Cloud data services are serverless and used for real-time or analytics workloads?

**Options**
- A. Cloud Firestore
- B. Cloud Bigtable
- C. **BigQuery** ✅
- D. **Cloud SQL** ✅ *(selected in the screenshot; see note)*

**Likely expected answers from the assessment screenshot: C — BigQuery and D — Cloud SQL.**

**Study note:** BigQuery is serverless analytics. Cloud SQL is a fully managed relational database, but it is not generally described as serverless in the same sense as BigQuery. Depending on the exact wording, Firestore may also be described as serverless. This question’s phrasing is therefore ambiguous; check the assessment’s key.

---

### Q11. Managed Instance Group definition
**Question:** What is a Managed Instance Group (MIG) in Google Cloud?

**Options**
- A. A networking construct for connecting VPCs
- B. A set of different VM instances with manual scaling
- C. **A collection of identical VM instances created from an instance template** ✅
- D. A serverless compute platform for containerised apps

**Correct answer: C**

---

### Q12. On-premises data-centre connectivity
**Question:** A financial company needs low latency and high bandwidth from its data centre to Google Cloud for critical workloads. Which connectivity option should it choose?

**Options**
- A. Cloud VPN
- B. VPC Peering
- C. Shared VPC
- D. **Cloud Interconnect** ✅

**Correct answer: D — Cloud Interconnect**

**Why:** It provides dedicated or partner-provided private connectivity. Cloud VPN uses encrypted tunnels over the internet.

---

### Q13. Compute Engine “On host maintenance”
**Question:** What does the “On host maintenance” setting determine for a Compute Engine instance?

**Options**
- A. Backed up to Cloud Storage
- B. Automatically restarted
- C. Moved to another project
- D. **Whether the VM is live-migrated or stopped during host maintenance** ✅

**Correct answer: D**

**Remember:** Host maintenance behaviour and **Automatic restart** are separate VM settings.

---

### Q14. Cloud Logging to BigQuery
**Question:** Why export Cloud Logging data to BigQuery?

**Options visible in the screenshot**
- A. **To run advanced SQL analytics and retain logs beyond default retention periods** ✅
- B. To reduce the number of Pub/Sub subscriptions
- C. Because BigQuery automatically indexes logs in real time
- D. To avoid paying storage costs for log entries

**Correct answer: A**

**Why:** BigQuery allows analytical SQL over exported logs and separate data-retention management. Exporting logs does not eliminate storage costs.

---

### Q15. BigQuery cost estimation and control (choose TWO)
**Question:** Which methods can help estimate and control BigQuery costs before running queries?

**Options visible in the screenshot**
- A. **Use the Query Validator to preview data processed** ✅ *(wording paraphrased)*
- B. Set daily and monthly cost controls through BigQuery Reservations
- C. Disable Cloud Logging for queries
- D. Only run queries in the free tier

**Correction / exam note:** Query validation or a dry run can estimate bytes processed. **BigQuery Reservations primarily manage capacity and slots, not daily/monthly spending caps.** Use budgets/alerts, quotas where available, maximum bytes billed, and query dry runs to control cost. The second intended answer is unclear from the screenshot, so don’t treat option B as universally correct.

---

### Q16. `gcloud compute instances list`
**Question:** Which information does the command output include by default? (Choose TWO)

**Options visible in the screenshot**
- A. **Instance name and zone** ✅
- B. **Machine type and status** ✅
- C. VPC network firewall rules applied
- D. Password for the default user

**Correct answers: A and B**

Command:
```bash
gcloud compute instances list
```

---

### Q17. Cloud Run traffic splitting
**Question:** An HTTP service runs on Cloud Run. A new revision is released, and the team wants 90% of traffic to continue going to the old revision until the new revision is confirmed stable. How should they implement this?

**Options visible in the screenshot**
- A. Use Cloud Load Balancer health checks to adjust traffic automatically
- B. Create a new Cloud Run service and DNS weighted records
- C. **Update the service configuration to set traffic-split percentages for each revision** ✅
- D. Set maximum concurrency to 1 to limit requests per instance

**Correct answer: C**

**Why:** Set the old revision to 90% and the new revision to 10%, then increase the new revision’s share after validation.

---

### Q18. GKE node pools
**Question:** Which statement about GKE node pools is correct?

**Options visible in the screenshot**
- A. Node pools are managed exclusively by Config Connector custom resources
- B. Each cluster can have only a single node pool with one machine type
- C. Node pools cannot be configured for autoscaling once they are created
- D. **Node pools allow distinct machine types and disk sizes per pool** ✅

**Correct answer: D**

---

### Q19. ACID-compliant transactional services (choose TWO)
**Question:** Which Google Cloud services are suitable for ACID-compliant transactional queries?

**Options**
- A. Cloud Spanner
- B. **Cloud SQL** ✅
- C. BigQuery
- D. Cloud Bigtable

**Correction:** The best conventional answer is **Cloud SQL and Cloud Spanner**. The screenshot’s option list shows Cloud Spanner, Cloud SQL, BigQuery, and Cloud Bigtable. Both Cloud SQL and Spanner support ACID transactions; BigQuery supports transactions only in specified scenarios and is primarily an analytics warehouse.

---

### Q20. BigQuery analytical workloads
**Question:** Which Google Cloud service is best for ad-hoc SQL queries on terabytes of structured data stored in a data warehouse?

**Options**
- A. **BigQuery** ✅
- B. Cloud Bigtable
- C. Cloud Firestore
- D. Cloud Spanner

**Correct answer: A — BigQuery**

---

## 🛡️ Section 3 — Ensuring Security and Reliability

### Q21. Cloud SQL backup and point-in-time recovery
**Question:** Cloud SQL can perform automated daily backups and restore a database instance to a specific point in time within the retention period. True or False?

**Options**
- A. **True** ✅
- B. False

**Correct answer: True**, if automated backups and point-in-time recovery are enabled and supported for the database configuration.

---

### Q22. Expand a VPC subnet’s IP range
**Question:** Which action allows you to expand the IP range of an existing VPC subnet without downtime?

**Options visible in the screenshot**
- A. Convert the VPC network to auto mode
- B. Create a new subnet with a larger range and delete the old one
- C. Assign an external IP to the subnet
- D. Add a secondary IP range to the subnet and enable Private Service Connect

**Correction:** The screenshot is difficult to read and option wording may be inaccurate. In Google Cloud, a subnet’s **primary IPv4 range can often be expanded in place** if the new range is valid and non-overlapping; it does not require creating a new subnet in every case. Secondary ranges serve different purposes. Confirm the exact intended answer with the test key.

---

### Q23. GKE troubleshooting commands (choose TWO)
**Question:** When exploring a GKE cluster, which kubectl commands can be used to list running workloads and network endpoints?

**Options visible in the screenshot**
- A. **`kubectl get pods`** ✅
- B. **`kubectl get services`** ✅
- C. `kubectl auth can-i list`
- D. `kubectl cordon`

**Correct answers: A and B**

**Why:** Pods show workloads; Services show service objects and their exposed ports/addresses. Use `kubectl get endpoints` or `kubectl get endpointslices` to inspect back-end endpoints specifically.

---

### Q24. Regional static external IP
**Question:** How do you reserve a regional static external IP address for a Compute Engine instance?

**Options visible in the screenshot (approximate)**
- A. Use `gcloud compute addresses create` with the required region and a name ✅
- B. Assign the IP address in instance metadata
- C. Reserve it by creating a firewall rule
- D. Use a custom-mode VPC

**Correct answer: A**

Example:
```bash
gcloud compute addresses create my-static-ip \\
  --region=asia-south1
```

---

### Q25. Cloud SQL automated backups
**Question:** Can Cloud SQL perform automated daily backups and point-in-time recovery?

**Options**
- A. **True** ✅
- B. False

**Correct answer: True, if configured and supported.**

---

### Q26. GKE service-account permissions
**Question:** Which IAM roles grant administrator SSH access through OS Login? (Choose TWO)

**Options shown**
- A. `roles/compute.osLogin` ✅
- B. `roles/compute.osAdminLogin` ✅
- C. `roles/iam.serviceAccountUser`
- D. `roles/viewer`

**Correct answers: A and B**

**Remember:** `osAdminLogin` includes administrator login privileges. Additional IAM permissions may be required to use a VM’s attached service account.

---

## 🔐 Section 4 — Configuring Google Cloud Access

### Q27. Short-lived OAuth 2.0 tokens
**Question:** Which IAM role grants permission to generate short-lived OAuth 2.0 tokens for a service account?

**Options visible in the screenshot**
- A. **Service Account Token Creator** ✅
- B. Service Account User
- C. Owner
- D. Project Editor

**Correct answer: A — `roles/iam.serviceAccountTokenCreator`**

---

### Q28. Default Compute Engine service account
**Question:** Why should you avoid using the default Compute Engine service account for workloads?

**Options visible in the screenshot**
- A. **It can have broad Editor privileges, violating least privilege** ✅
- B. It cannot be used with Cloud Run or Cloud Functions
- C. It expires after 30 days and must be renewed manually
- D. It is unsupported in GKE clusters with Workload Identity enabled

**Correct answer: A**

**Why:** Create a dedicated identity and grant only the required predefined roles. The default service account’s permissions depend on project and organisation settings.

---

### Q29. Service-account impersonation
**Question:** What is a benefit of service-account impersonation instead of distributing long-lived service-account keys?

**Options visible in the screenshot**
- A. **Reduces credential leakage risk because tokens are short-lived and scoped** ✅
- B. Allows unlimited token lifetime and safe storage in source-code repositories
- C. Eliminates the need to grant any IAM roles to the calling principal
- D. Automatically promotes the caller to the Owner role

**Correct answer: A**

---

### Q30. Specify a service account when creating a VM
**Question:** When creating a Compute Engine VM with `gcloud`, which flag specifies the service account the VM should use?

**Options**
- A. **`--service-account`** ✅
- B. `--machine-type`
- C. `--image-family`
- D. `--zone`

**Correct answer: A**

---

### Q31. What is a Google Cloud service account?
**Question:** A Google Cloud service account is best described as which of the following?

**Options visible in the screenshot**
- A. A GCP billing account created for each project
- B. A Google Workspace user account managed by an end user
- C. A Kubernetes namespace used for isolating workloads
- D. **A special identity used by applications or services to access Google APIs** ✅

**Correct answer: D**

---

### Q32. Review a project’s current IAM policy
**Question:** Which gcloud command should be used to review the current IAM policy for a project?

**Options visible in the screenshot**
- A. **`gcloud projects get-iam-policy PROJECT_ID`** ✅
- B. `gcloud projects set-iam-policy PROJECT_ID`
- C. `gcloud iam roles describe ROLE_NAME`
- D. `gcloud iam service-accounts list`

**Correct answer: A**

---

### Q33. KSA-to-GSA association with GKE Workload Identity
**Question:** In GKE Workload Identity, how do you associate a Kubernetes ServiceAccount (KSA) with a Google Cloud service account (GSA)?

**Options visible in the screenshot**
- A. Store the GSA’s private key in a Kubernetes Secret and mount it into the pod
- B. **Add an annotation to the KSA referencing the GSA email and grant the KSA permission to act as the GSA** ✅
- C. Configure the GSA as a node label and select it with a pod affinity
- D. Create a network policy mapping the KSA to the GSA

**Correct answer: B**

Example annotation:
```bash
kubectl annotate serviceaccount KSA_NAME \\
  iam.gke.io/gcp-service-account=GSA_NAME@PROJECT_ID.iam.gserviceaccount.com
```

Grant the KSA the `roles/iam.workloadIdentityUser` role on the GSA. Do not put long-lived service-account keys in Kubernetes Secrets.

---

### Q34. Service-account permissions for application logs and backups
**Question:** An application writes logs to Cloud Logging and creates backup objects in Cloud Storage. Which roles should it receive?

**Options visible in the screenshot**
- A. `roles/owner`
- B. `roles/editor` and `roles/storage.admin`
- C. **`roles/logging.logWriter` and `roles/storage.objectCreator`** ✅
- D. `roles/logging.viewer` and `roles/storage.objectViewer`

**Correct answer: C**

**Why:** These roles allow writing logs and creating objects. If the application must overwrite or delete existing objects, additional permissions may be needed.

---

### Q35. Least privilege for a service account
**Question:** Which principle should guide you when assigning IAM roles to a service account?

**Options visible in the screenshot**
- A. Use custom roles exclusively for every workload regardless of need
- B. Assign the Owner role broadly to simplify ongoing administration
- C. Always include broad basic roles such as Editor for redundancy
- D. **Grant only the minimum permissions necessary for the workload** ✅

**Correct answer: D — Least privilege**

---

### Q36. Cloud Run uses the default Compute Engine service account
**Question:** A Cloud Run service was deployed using the default Compute Engine service account, and a security review found broad permissions. What is the best remediation?

**Options visible in the screenshot**
- A. Use the default service account but rotate its key every 90 days
- B. Assign the Owner role to the default service account to ensure stability
- C. **Create a dedicated service account with only necessary roles and assign it to Cloud Run** ✅
- D. Disable Cloud Run and migrate to App Engine

**Correct answer: C**

**Why:** The dedicated service account limits the workload’s permissions. Grant the minimum roles it actually needs.

---

### Q37. Generate short-lived credentials: best practices (choose TWO)
**Question:** Which choices are recommended best practices for generating and using short-lived service-account credentials?

**Options visible in the screenshot**
- A. **Request only the specific OAuth scopes needed for the task** ✅
- B. Use long-lived keys whenever possible to avoid API calls
- C. Grant Service Account Token Creator broadly to any principal that might need access
- D. **Configure short expiry times and rotate/reissue credentials frequently** ✅ *(closest available option wording)*

**Correct answers: A and D**

**Why:** Limit access and prefer short-lived credentials. Avoid widely granting token-generation permissions and avoid long-lived service-account keys.

---

## 🧰 Extra questions visible in earlier screenshots

### Q38. Cloud Asset Inventory exports
**Question:** What benefit does reviewing Cloud Asset Inventory exports over time provide during compliance audits?

**Options were not visible in the screenshot.**

**Correct concept:** It helps identify and track changes to resources and IAM policies over time.

---

### Q39. Multi-project billing (choose TWO)
**Question:** When linking multiple projects to a single billing account, what are two potential advantages?

**Options visible in the screenshot**
- A. **Consolidated billing and cost visibility across projects** ✅
- B. Automatic IAM role propagation from the billing account to projects
- C. **Ability to share eligible committed-use discounts across projects** ✅ *(subject to applicable terms and configuration)*
- D. Increased quotas for all projects automatically

**Likely answers: A and C**

---

### Q40. Cloud SQL transactional workloads
**Question:** Which service is suitable for ACID-compliant relational transactions?

**Options visible in the screenshot**
- A. Cloud Spanner
- B. **Cloud SQL** ✅
- C. BigQuery
- D. Cloud Bigtable

**Study note:** Cloud SQL is a standard answer for traditional relational transactions; Cloud Spanner also supports ACID transactions at scale.

---

### Q41. Cloud Functions/Cloud Run traffic splitting
**Question:** In Cloud Functions (2nd gen) and Cloud Run, traffic splitting by percentage is applied at what level?

**Options visible in the screenshot**
- A. **Service level across revisions** ✅
- B. Project level across all services
- C. Region level across multiple projects
- D. Container-image level across registries

**Correct answer: A**

---

### Q42. Read-only partner access to a Cloud Storage bucket
**Question:** A partner needs read access to objects in a specific bucket. The bucket currently uses uniform bucket-level access. What should you do?

**Options visible in the screenshot**
- A. **Assign the Storage Object Viewer role to the partner’s principal on the bucket** ✅
- B. Switch to fine-grained ACLs and set object ACLs
- C. Grant Storage Admin on the project
- D. Disable uniform bucket-level access and use signed URLs

**Correct answer: A — `roles/storage.objectViewer`**

---

## 🧾 Quick Answer Sheet

| Q# | Correct answer |
|---:|---|
| 1 | Organization |
| 2 | Cloud Identity identities/groups can be granted IAM roles |
| 3 | Least privilege |
| 4 | Owner *(assessment’s expected answer; governance caveat noted)* |
| 5 | Cloud Spanner |
| 6 | Design Cloud Run services to start quickly and be stateless |
| 7 | `gsutil` |
| 8 | Create/destroy instances through scaling and auto-healing |
| 9 | Secure tags are centrally managed and IAM-controlled; option wording ambiguous |
| 10 | Likely BigQuery + Cloud SQL per the screenshot, but ambiguous |
| 11 | Identical VMs created from an instance template |
| 12 | Cloud Interconnect |
| 13 | Migrate or stop VM during host maintenance |
| 14 | Advanced SQL analytics and longer retention |
| 15 | Dry-run/query validation; second screenshot option unclear |
| 16 | Instance name/zone + machine type/status |
| 17 | Configure Cloud Run traffic split across revisions |
| 18 | Different machine types and disk sizes per GKE node pool |
| 19 | Cloud SQL + Cloud Spanner |
| 20 | BigQuery |
| 21 | True, if PITR/backups enabled |
| 22 | Check subnet-range constraints; may be expanded in place |
| 23 | `kubectl get pods` + `kubectl get services` |
| 24 | `gcloud compute addresses create` with `--region` |
| 25 | True, if supported and configured |
| 26 | `roles/compute.osLogin` + `roles/compute.osAdminLogin` |
| 27 | Service Account Token Creator |
| 28 | Broad permissions risk; use dedicated service account |
| 29 | Short-lived tokens reduce key leakage risk |
| 30 | `--service-account` |
| 31 | Non-human identity for applications/services |
| 32 | `gcloud projects get-iam-policy PROJECT_ID` |
| 33 | KSA annotation + Workload Identity User binding |
| 34 | `roles/logging.logWriter` + `roles/storage.objectCreator` |
| 35 | Least privilege |
| 36 | Dedicated service account with minimal roles |
| 37 | Narrow scopes + short-lived credentials |
| 38 | Track resource and IAM changes over time |
| 39 | Consolidated billing + eligible committed-use discounts |
| 40 | Cloud SQL *(Spanner also supports ACID transactions)* |
| 41 | Service level across revisions |
| 42 | `roles/storage.objectViewer` on bucket |

---

### 🎨 Legend
- ✅ **Correct / best answer**
- ⚠️ **Ambiguous or screenshot wording unclear**
- 💡 **Exam tip / explanation**

This guide prioritises the questions and options legible in the submitted photographs. If an option’s text was clipped or blurred, the note says so instead of pretending the transcription is exact.
