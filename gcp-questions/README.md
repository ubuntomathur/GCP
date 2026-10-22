# Google Cloud Questions — Study Notes

Collected from the Google Cloud assessment questions discussed in this conversation. Answers are study notes; verify service-specific details against current Google Cloud documentation before using them in production.

## 1. Resource hierarchy

**Q: What is the root of the Google Cloud resource hierarchy?**  
**Answer:** Organization.

**Remember:** Organization → Folders (optional) → Projects → Resources. A resource has one parent in the hierarchy.

## 2. Cloud Identity and IAM

**Q: How does Cloud Identity work with IAM?**  
**Answer:** Cloud Identity manages user identities and groups. IAM controls what those identities can do on Google Cloud resources. Cloud Identity identities and groups can be granted IAM roles.

**Q: Which service centrally manages user accounts and groups across projects?**  
**Answer:** Cloud Identity.

**Q: Which principle should guide IAM role assignments to a service account?**  
**Answer:** Grant only the minimum permissions necessary for the workload (least privilege).

**Q: Which IAM role allows an administrator to generate short-lived OAuth 2.0 tokens for a service account?**  
**Answer:** Service Account Token Creator — `roles/iam.serviceAccountTokenCreator`.

**Q: Which command displays the current IAM policy for a project?**  
**Answer:** `gcloud projects get-iam-policy PROJECT_ID`.

**Q: What is a Google Cloud service account?**  
**Answer:** A non-human identity used by applications, VMs, and services to authenticate to Google Cloud APIs.

**Q: Why avoid the default Compute Engine service account for production workloads when it has broad permissions?**  
**Answer:** Create a dedicated service account with only the roles required by the workload.

**Q: What is a benefit of service account impersonation and short-lived credentials?**  
**Answer:** It reduces long-lived credential/key leakage risk. Use narrowly scoped permissions and short-lived credentials when possible.

**Q: Which roles grant SSH access through OS Login? (Choose two.)**  
**Answer:** `roles/compute.osLogin` and `roles/compute.osAdminLogin`. The latter provides administrator-level login privileges.

**Q: How does OS Login simplify SSH access?**  
**Answer:** It centralises SSH identity/access management through Google identities and IAM, reducing the need to manage SSH keys separately on each VM.

**Q: What is the recommended way to grant a Cloud Run workload access to Google Cloud services?**  
**Answer:** Use a dedicated service account with only the necessary IAM roles.

## 3. Organization Policy and Cloud Asset Inventory

**Q: What can an Organization Policy constraint enforce?**  
**Answer:** Organisational restrictions such as limiting resource creation to approved regions (for example, with the resource locations constraint).

**Q: What benefit does reviewing Cloud Asset Inventory exports over time provide during compliance audits?**  
**Answer:** It helps track changes to resources and IAM policies over time.

## 4. Billing and multi-project management

**Q: What are benefits of linking multiple projects to one Cloud Billing account? (Choose two.)**  
**Answer:** Consolidated billing/cost visibility across projects, and sharing eligible committed use discounts across linked projects when supported and configured.

**Note:** Billing-account linkage does not automatically grant IAM roles or increase project quotas.

## 5. Compute Engine

**Q: What does a Managed Instance Group (MIG) do?**  
**Answer:** Manages a group of VM instances created from an instance template and supports scaling, auto-healing, and maintaining the desired number of instances.

**Q: What is a MIG?**  
**Answer:** A collection of VM instances created from an instance template.

**Q: What does the “On host maintenance” setting control?**  
**Answer:** Whether a VM is live-migrated during host maintenance or stopped/terminated, depending on the VM configuration and supported machine type. Automatic restart is a separate setting.

**Q: For a VM expected to continue through host maintenance and recover after crashes, which settings are typically appropriate?**  
**Answer:** Set On host maintenance to “Migrate VM instance” and enable automatic restart, where supported.

**Q: How many zones store data for a zonal persistent disk?**  
**Answer:** One zone. A regional persistent disk synchronously replicates data across two zones in the same region.

**Q: What is the difference between a disk snapshot and a machine image?**  
**Answer:** A snapshot is a point-in-time backup of a disk; an image is a bootable disk template used to create VM boot disks.

**Q: Which `gcloud` flag specifies the service account for a new Compute Engine VM?**  
**Answer:** `--service-account`.

**Q: Which information does `gcloud compute instances list` include by default? (Choose two examples.)**  
**Answer:** Instance name/zone and machine type/status.

**Q: How do you reserve a regional static external IP address?**  
**Answer:** Create a regional address, for example:
```bash
gcloud compute addresses create my-static-ip --region=asia-south1
```
Then assign it to a compatible VM in that region.

## 6. Networking

**Q: Which connectivity option provides high-bandwidth, low-latency private connectivity from an on-premises data centre to Google Cloud?**  
**Answer:** Cloud Interconnect.

**Q: How do VPC network tags differ from secure tags?**  
**Answer:** Network tags are simple strings commonly used to target VM instances in firewall rules. Secure tags are centrally managed and IAM-controlled, and can be used in firewall policies.

**Q: How can a regional static external IP be reserved?**  
**Answer:** Create a static address with the required region using `gcloud compute addresses create`.

**Q: How should you expand a subnet when the needed larger range cannot safely be assigned to the existing subnet?**  
**Answer:** Create a new subnet with a suitable non-overlapping range and migrate workloads; delete the old subnet only after it is no longer in use. (Whether an existing range can be expanded depends on the precise subnet/IP-range constraints.)

## 7. Cloud Run and serverless

**Q: How can a Cloud Run service be triggered when a file is uploaded to Cloud Storage without custom glue code?**  
**Answer:** Use Eventarc to route Cloud Storage events to Cloud Run.

**Q: What should developers consider when using Cloud Run?**  
**Answer:** Design containers to start quickly and services to be stateless where possible, allowing rapid scaling and efficient request handling. Cloud Run supports multiple languages and containerised workloads.

**Q: How do you route 90% of traffic to an old Cloud Run revision and keep a new revision under observation?**  
**Answer:** Configure a service-level traffic split across revisions (for example, 90% old and 10% new), then increase traffic to the new revision as confidence grows.

**Q: Where is percentage-based traffic splitting configured for Cloud Run revisions?**  
**Answer:** At the Cloud Run service level, across revisions.

## 8. Storage

**Q: What are benefits of a multi-region Cloud Storage bucket?**  
**Answer:** Geographic redundancy and high availability across multiple locations, subject to the storage location’s design and service guarantees.

**Q: How can a partner be granted read-only access to objects in a specific bucket?**  
**Answer:** Grant the partner principal `roles/storage.objectViewer` on that bucket, following least privilege.

**Q: Which command-line tool is commonly used to upload files to Cloud Storage buckets?**  
**Answer:** `gsutil` is a commonly known tool; newer workflows may use `gcloud storage`. Example:
```bash
gcloud storage cp file.txt gs://BUCKET_NAME/
```

## 9. Databases and analytics

**Q: Which Google Cloud database combines relational consistency, strong transactions, horizontal scalability, and global distribution?**  
**Answer:** Cloud Spanner.

**Q: Which service is best for ad-hoc SQL analytics on structured data in a data warehouse?**  
**Answer:** BigQuery.

**Q: Which services are suitable for ACID-compliant transactional workloads?**  
**Answer:** Cloud SQL is the common choice for traditional relational OLTP. Cloud Spanner also supports strongly consistent ACID transactions at global scale. BigQuery supports transactions in specific supported scenarios, but is primarily an analytics warehouse.

**Q: Which database combines relational consistency with non-relational scalability and is suitable for globally distributed, strongly consistent transactions?**  
**Answer:** Cloud Spanner.

**Q: Why export Cloud Logging data to BigQuery?**  
**Answer:** To run advanced SQL analytics on logs and retain/query exported data according to BigQuery storage and retention settings.

**Q: What is a good way to estimate BigQuery query cost before running a query?**  
**Answer:** Use the query validator/validator or query dry run to estimate processed data. Configure appropriate budgets, quotas, and cost controls; BigQuery Reservations primarily manage capacity rather than serving as daily/monthly spend limits.

## 10. GKE and Kubernetes workloads

**Q: What is a correct statement about GKE node pools?**  
**Answer:** Node pools allow distinct machine types and disk sizes per pool within a cluster.

**Q: Which kubectl commands help list GKE workloads and services? (Choose two.)**  
**Answer:** `kubectl get pods` and `kubectl get services` (often shortened to `kubectl get svc`).

**Q: How can a GKE workload access Google Cloud services using Workload Identity Federation for GKE?**  
**Answer:** Associate a Kubernetes ServiceAccount (KSA) with a Google service account (GSA), annotate the KSA with the GSA email when using the KSA-to-GSA linking approach, and grant the KSA the `roles/iam.workloadIdentityUser` role on the GSA. Newer direct principal-based configurations may not require a GSA.

**Q: How do you associate a Kubernetes service account with a Google service account using the KSA-to-GSA method?**  
**Answer:** Add an annotation to the KSA referencing the GSA email and grant the KSA the appropriate Workload Identity User permission on the GSA. Avoid storing GSA private keys in Kubernetes Secrets.

## 11. Google Cloud Functions and Cloud Run revisions

**Q: At what level is traffic splitting by percentage applied across Cloud Run revisions (including second-generation functions deployed on Cloud Run)?**  
**Answer:** At the service level across revisions.

## 12. Logging and backup permissions

**Q: Which roles should a service account use to write logs and create backup objects in Cloud Storage?**  
**Answer:** `roles/logging.logWriter` and `roles/storage.objectCreator`, assuming it only needs to create objects and does not need to read or delete them.

## 13. Cloud SQL backup and recovery

**Q: Can Cloud SQL perform automated daily backups and restore an instance to a point in time within the retention period?**  
**Answer:** True, when automated backups and point-in-time recovery are enabled and the relevant engine/configuration supports them.

## 14. IAM policy best practices

**Q: Which principle should guide service account role assignments?**  
**Answer:** Least privilege—grant only the minimum permissions required for the workload.

**Q: What should you do if a default service account has unnecessarily broad permissions?**  
**Answer:** Create a dedicated service account, assign the minimum required roles, and attach it to the workload.

**Q: What is the purpose of the Owner role?**  
**Answer:** The Owner basic role grants broad project-level control, including IAM management. Do not treat an Owner as technically required for every project under all modern access models; follow your organisation’s governance standards and prefer granular predefined roles.

## Quick revision table

| Requirement | Google Cloud service/concept |
|---|---|
| Root of resource hierarchy | Organization |
| Central user/group identity management | Cloud Identity |
| Access to resources and permissions | Cloud IAM |
| Resource policy change history / audit review | Cloud Asset Inventory |
| Globally distributed relational transactions | Cloud Spanner |
| Managed traditional relational database | Cloud SQL |
| Serverless analytics warehouse | BigQuery |
| Event-driven Cloud Run trigger | Eventarc |
| Serverless containers | Cloud Run |
| Kubernetes orchestration | GKE |
| Dedicated private on-premises connectivity | Cloud Interconnect |
| VM group with scaling and auto-healing | Managed Instance Group |
| Centrally managed VM SSH access | OS Login |
| Object storage | Cloud Storage |
| Service-account short-lived token generation | Service Account Token Creator |
| Logs writer role | `roles/logging.logWriter` |
| Cloud Storage object creation role | `roles/storage.objectCreator` |
| KSA-to-GSA access for GKE | Workload Identity Federation for GKE |
| VM list command | `gcloud compute instances list` |
| Read a project IAM policy | `gcloud projects get-iam-policy PROJECT_ID` |

## Important accuracy notes

- Cloud Run supports a range of containerised workloads; “stateless and quick-starting” is a design recommendation, not an absolute platform restriction.
- BigQuery supports transactions only for supported operations and scenarios; it is primarily designed for analytics.
- Do not use basic Owner/Editor roles as a shortcut where narrower predefined roles are appropriate.
- Cloud SQL point-in-time recovery depends on configuration, database engine, and retention settings.
- For production workloads, prefer short-lived credentials and Workload Identity over long-lived service-account key files.
