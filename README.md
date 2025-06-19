# Apache Beam - GSoC 2025

This repository contains my notes and plans for the GSoC 2025 project with Apache Beam.

## Documentation on how to contribute

- https://github.com/apache/beam/blob/master/CONTRIBUTING.md

## Communication channels

- Mailing list: Dev and Users mailing lists are used for discussions, questions, and announcements. It is the primary communication channel. I should write when a milestone is reached.
- Google meet chat: A chat exists on Google Meet, but it is not used much.

## Technologies

In my project I will use:

- python
- terraform
- gcp
- gradle

## Evaluation

Just some questions about how the project is going, what I have done, and what I plan to do next.

- Midterm evaluation: 2025-07-14
- Final evaluation: 2025-08-25

## Topics

### 1. GCP Resource Cleaner (Python):

Recently the Beam team has noticed that some GCP resources are not being cleaned up properly, leading to unnecessary costs.

The goal of this project is to create a tool that can automatically clean up unused GCP resources.

This tool will help the Beam team to reduce costs and improve resource management. The project will involve:

- Create a Python script that can list GCP resources
- Use GCP APIs to check the creation date and last usage of resources
- Identify stale resources based on the last usage date
- Use GCP APIs to delete stale resources
- Create a configuration file to specify which resources to check and how long to wait before considering them stale
- Use a GitHub Action to run the script on a schedule (e.g., daily or weekly)

### 2. GCP Access Control through git (Python, Terraform, and Gradle):

Right now the Beam team uses a manual process to manage access, you are supposed to ask for access on the Beam mailing list, and then a committer will grant you access. This process is not very efficient and can lead to delays in getting access to the resources you need and we do not really know who has access to what.

The goal of this project is to automate the process of managing access to GCP resources using git, Terraform, and Gradle. The idea is that if someone needs access to a GCP resource, they can create a pull request (PR) that adds their username to a file in the repository. The PR would contain the reason, the level of access and to what resources. That will be reviewed by a committer, and if approved, the access will be granted using Terraform.

This project will involve:

- Create a Python script that can parse the PR and extract the necessary information
- Use Terraform to manage the infrastructure for access control
- Use Gradle to build and deploy the Python script
- Use GCP APIs to manage access to resources
- Use git to manage the access control file
- Use a GitHub Action to trigger the Python script when a PR is created
- Use a GitHub Action to notify the committer when a PR is created
- Use a GitHub Action to notify the user when their access is granted or denied
- Use a GitHub Action to notify the user if their access is revoked and why

### 3. Key rotation for GCP services (Python):

Some GCP services require keys to access them, and these keys need to be rotated regularly for security reasons. The Beam team currently does not have a process in place for key rotation, which can lead to security vulnerabilities like key leaks or unauthorized access.

The goal of this project is to create a process for key rotation that is automated and secure. This will involve:

- Create a Python script that can generate new keys for GCP services
- Use GCP APIs to manage the keys
- Use a configuration file to specify which services require key rotation and how often the keys should be rotated
- Use a GitHub Action to run the script on a schedule (e.g., monthly or quarterly)
- Use a GitHub Action to notify the team when keys are rotated and provide the new keys securely
- Use a GitHub Action to notify the team if a key rotation fails and why

### 4. Stateless Infrastructure (Terraform):

Right now most of the Beam infrastructure is stateless and managed with things like terraform, Jenkins, and Kubernetes. However, some parts of the infrastructure are still stateful, or need manual intervention, like cleanup scripts that are fragmented throughout the codebase. We are also missing a monitoring/reporting system to track the state of the infrastructure, orphaned resources, and other leaks.

The goal of this project is to make the Beam infrastructure fully stateless and automated. This will involve:

- Enforce resource auto delete policies for all resources using labels/tags.
- Integrate the cleanup scripts into the infrastructure as code (IaC) process.
- Create a monitoring/reporting system to track the state of the infrastructure, orphaned resources, and other leaks.

### 5. Automated security monitoring and policy violation detection (Python, Terraform)

- **Ingest audit logs and create alerts:** Ingesting the audit logs and analysing them we can classify them in search of suspicious ones, triggering an alert. This can go to the audit log of GCP or even to the OpenTelemetry collector. This can be done with python.

The monitoring/logging tool follows the logic:
- An application generates logs.
- The logs are ingested to GCP. If native logs are implemented, great. Else, implement logs to GCP using Terraform, mainly for the audit logs. (This could also be done with OpenTelemetry).
- Configure automatic alerts inside GCP logging for any unusual log.

## GSoC 2025 Work Plan

This plan outlines the work for the GSoC 2025 project with Apache Beam, covering roughly 12 weeks from early June to the final evaluation on August 25th, 2025.

**Assumptions:**
*   Start Date: Approx. June 1st, 2025
*   Midterm Evaluation: July 14th, 2025
*   Final Evaluation: August 25th, 2025
*   Time Commitment: Full-time, with flexibility.

---

### Phase 1: Foundation & Core Access Control (Weeks 1-6: Approx. June 1 - July 12)

*   **Primary Focus:**
    1.  Complete the GCP Resource Cleaner.
    2.  Implement core functionality for GCP Access Control through Git.
*   **Secondary Focus:**
    *   Begin groundwork for Stateless Infrastructure, linking with the Resource Cleaner.

**Detailed Breakdown - Phase 1:**

*   **Weeks 1-2: GCP Resource Cleaner & Initial Stateless Infrastructure Steps**
    *   **Goal:** Finalize GCP Resource Cleaner tool and its automation. Start connecting this to stateless infrastructure goals.
    *   **Tasks:**
        *   **GCP Resource Cleaner (Python):**
            *   Solidify Python script: list resources, check creation/usage, identify stale, delete via GCP APIs.
            *   Create/finalize configuration file (resources to check, staleness criteria).
            *   Implement/test GitHub Action for scheduled execution.
        *   **Stateless Infrastructure (Terraform):**
            *   Research/document enforcing auto-delete policies via labels/tags.
            *   Draft initial Terraform configurations for these policies.
    *   **Milestone 1 (End of Week 2 - e.g., by June 14):**
        *   Functional and automated GCP Resource Cleaner.
        *   Documented strategy & initial Terraform for label-based auto-delete.
        *   *Consider mailing list update.*

*   **Weeks 3-6: GCP Access Control through Git (Core Implementation)**
    *   **Goal:** Get fundamental system for managing GCP access via Git PRs operational.
    *   **Tasks:**
        *   **Python Script:** Develop script to parse PRs (requester, resources, access level, justification).
        *   **Terraform:** Design modules/configs for GCP IAM, driven by structured input (e.g., TFvars, JSON).
        *   **Integration Logic:** Mechanism for Python script (on PR merge) to update Terraform input.
        *   **Git & GitHub Actions:**
            *   Repo structure for access control file.
            *   Actions: Trigger Python script on merge; notify committers on PR creation; notify user on grant/deny.
        *   **GCP APIs:** Integrate for managing access as defined by Terraform.
        *   **Gradle (Optional):** Begin setup for Python script build/deploy.
    *   **Milestone 2 (End of Week 6 - e.g., by July 12, before Midterm):**
        *   Core GCP Access Control operational: PRs -> automated Terraform updates -> GCP access changes.
        *   Basic notifications for PR creation/status.
        *   *Prepare demo/summary for midterm evaluation.*

**Midterm Evaluation: 2025-07-14**
*   Present progress: GCP Resource Cleaner, GCP Access Control.
*   Demonstrate functionalities.
*   Discuss challenges, learnings, refined plan for Phase 2.

---

### Phase 2: Enhancements, Key Rotation & Full Stateless Vision (Weeks 7-12: Approx. July 15 - August 23)

*   **Primary Focus:**
    1.  Enhance/finalize GCP Access Control.
    2.  Implement Key Rotation.
    3.  Advance Stateless Infrastructure goals, including monitoring.
*   **Secondary Focus:**
    *   Thorough documentation and testing.

**Detailed Breakdown - Phase 2:**

*   **Weeks 7-8: GCP Access Control (Refinements & Completion)**
    *   **Goal:** Robust, fully featured, well-documented Access Control system.
    *   **Tasks:**
        *   **Gradle:** Fully integrate for Python script build/deploy (if not done).
        *   **GitHub Actions:** Implement remaining notifications (e.g., access revocation).
        *   **Terraform:** Refine for different roles, complex permissions.
        *   **Testing:** Thorough testing of various requests, edge cases, failures.
        *   **Documentation:** User and maintainer docs for access control.
    *   **Milestone 3 (End of Week 8 - e.g., by July 26):**
        *   Feature-complete GCP Access Control (all notifications, Gradle build).
        *   Robustly tested and documented.

*   **Weeks 9-10: Key Rotation for GCP Services**
    *   **Goal:** Automate GCP service key rotation.
    *   **Tasks:**
        *   **Python Script:** Generate new keys (GCP APIs), secure management/distribution.
        *   **Configuration:** File for services needing rotation & frequency.
        *   **GCP APIs:** Utilize for service account key management.
        *   **GitHub Actions:** Scheduled script execution; notify team on success/failure (securely provide new keys).
    *   **Milestone 4 (End of Week 10 - e.g., by August 9):**
        *   Automated key rotation operational.
        *   Secure notification system for key events.
        *   *Consider mailing list update.*

*   **Weeks 11-12: Stateless Infrastructure (Consolidation & Monitoring) & Final Wrap-up**
    *   **Goal:** Integrate components, advance stateless vision, prepare for final evaluation.
    *   **Tasks:**
        *   **Stateless Infrastructure (Terraform):**
            *   Integrate GCP Resource Cleaner with IaC (Terraform triggering/managing cleaner).
            *   Implement/test label-based auto-delete policies.
            *   Create monitoring/reporting (scripts/basic dashboards for infrastructure state, orphaned resources, leaks).
            *   Implement automated security monitoring by ingesting audit logs, creating alerts for suspicious activity, and using Python for analysis.
        *   **Final Testing:** End-to-end testing of all deliverables.
        *   **Documentation:** Complete all project documentation.
        *   **Project Showcase:** Prepare final GSoC presentation/report.
    *   **Milestone 5 (End of Week 12 - e.g., by August 23):**
        *   All GSoC goals met.
        *   Cleaner integrated with IaC; key rotation automated; access control functional.
        *   Basic monitoring/reporting in place.
        *   Comprehensive documentation & final submission ready.

**Final Evaluation: 2025-08-25**

---

**General Tips for Success:**
*   **Communicate Regularly:** Use Apache Beam mailing lists for milestones/blockers.
*   **Break Down Tasks:** Smaller daily/bi-daily goals.
*   **Version Control:** Use Git diligently.
*   **Seek Feedback Early and Often:** Share progress with mentors/community.
*   **Documentation As You Go:** Easier than at the end.
*   **Flexibility:** Be prepared to adjust plan with mentors.
