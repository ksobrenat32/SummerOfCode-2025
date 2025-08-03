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

### Final evaluation

Final submission should include:

- Bullet points summarizing the key features and improvements
- What code was added or modified and what not, including links to the relevant commits or pull requests
- Whats left to do
- Work submission URL is what is linked to the GSoC archive. Put it on a permanent URL, a GitHub gist is a good option.
- Remember only you know about the project, add context where needed.

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

Currently, the infrastructure is manually created using 'clickops'. The goal of this project is to migrate all stateless components (i.e., resources that do not persist data, like compute instances) to an Infrastructure as Code (IaC) model using Terraform. Stateful components, such as databases, storage buckets, and Pub/Sub topics, will remain under manual management for now.

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

## GSoC 2025 Work Plan (REVISED - July 31st)

**REVISED PLAN:** Adjusted to account for actual progress and remaining timeline (25 days to final evaluation).

**Current Status (July 31st):**
- **GCP Resource Cleaner:** ✅ **COMPLETED** - Functional, automated, GitHub Actions integrated
- **GCP Access Control:** ✅ **LARGELY COMPLETED** - Terraform roles structure done, automated workflow implemented
- **Key Rotation:** 🟡 **IN PROGRESS** - ServiceAccountManager implemented, needs automation
- **Stateless Infrastructure:** 🟡 **PARTIALLY STARTED** - Some Terraform migration done
- **Security Monitoring:** ❌ **NOT STARTED**

**Assumptions:**
*   Current Date: July 31st, 2025
*   Final Evaluation: August 25th, 2025 (25 days remaining)
*   Time Commitment: Intensive focus on remaining deliverables

---

### REVISED Phase 2: Completion Sprint (Aug 1-25, 2025)

**Strategic Approach:** Focus on completing all promised deliverables with MVP implementations where necessary.

---

#### Week 1 (Aug 1-7): Key Rotation Completion & Documentation
**PRIORITY 1: Complete Key Rotation System**
*   **Days 1-3 (Aug 1-3):**
    *   Finalize ServiceAccountManager with all required features
    *   Create configuration system for rotation schedules
    *   Implement GitHub Actions for scheduled key rotation
    *   Add secure key distribution mechanism
*   **Days 4-5 (Aug 4-5):**
    *   Integration testing of key rotation system
    *   Documentation for key rotation
*   **Days 6-7 (Aug 6-7):**
    *   GCP Access Control final refinements
    *   Complete any remaining Gradle integration

**Milestone 1 (Aug 7):** Key Rotation fully operational with automation

---

#### Week 2 (Aug 8-14): Stateless Infrastructure & Integration
**PRIORITY 2: Stateless Infrastructure Foundation**
*   **Days 1-4 (Aug 8-11):**
    *   Complete migration of remaining stateless resources to Terraform
    *   Implement label-based auto-delete policies
    *   Integrate Resource Cleaner with IaC processes
*   **Days 5-7 (Aug 12-14):**
    *   Create basic monitoring/reporting system for infrastructure state
    *   Implement orphaned resource detection
    *   Test integration between all components

**Milestone 2 (Aug 14):** Stateless Infrastructure operational with monitoring

---

#### Week 3 (Aug 15-21): Security Monitoring & Testing
**PRIORITY 3: Security Monitoring (Simplified Implementation)**
*   **Days 1-3 (Aug 15-17):**
    *   Implement audit log ingestion using Python
    *   Create basic alert system for suspicious activities
    *   Set up GCP logging configuration via Terraform
*   **Days 4-5 (Aug 18-19):**
    *   End-to-end testing of all systems
    *   Performance and reliability testing
*   **Days 6-7 (Aug 20-21):**
    *   Bug fixes and optimization
    *   Integration testing between all components

**Milestone 3 (Aug 21):** All core systems functional and integrated

---

#### Week 4 (Aug 22-25): Final Documentation & Evaluation Prep
**PRIORITY 4: Documentation & Final Evaluation**
*   **Days 1-2 (Aug 22-23):**
    *   Complete comprehensive documentation for all components
    *   Create user guides and deployment instructions
    *   Prepare project showcase materials
*   **Day 3 (Aug 24):**
    *   Final testing and validation
    *   Prepare final GSoC presentation
    *   Submit final evaluation materials
*   **Day 4 (Aug 25):**
    *   **Final Evaluation Due**

---

### Deliverable Coverage Strategy

**1. GCP Resource Cleaner** ✅ **COMPLETED**
- Automated stale resource detection and cleanup
- GitHub Actions integration
- Configuration-based management

**2. GCP Access Control** ✅ **COMPLETED**
- Terraform-based role management
- Automated PR workflow
- Custom role hierarchy (Admin, Committer, Viewer)

**3. Key Rotation** 🎯 **COMPLETE BY AUG 7**
- ServiceAccountManager for key lifecycle
- Automated rotation scheduling
- Secure key distribution
- Configuration-driven rotation policies

**4. Stateless Infrastructure** 🎯 **COMPLETE BY AUG 14**
- Migration of stateless resources to Terraform
- Label-based auto-delete policies
- Basic monitoring and reporting
- Integration with Resource Cleaner

**5. Security Monitoring** 🎯 **MVP BY AUG 17**
- **Simplified Implementation:**
  - Basic audit log ingestion
  - Alert system for suspicious activities
  - Python-based log analysis
  - Terraform configuration for GCP logging
- **Note:** Full OpenTelemetry integration deferred to post-GSoC

---

### Risk Mitigation

**High Risk Items:**
1. **Security Monitoring complexity** → Simplified to basic audit log monitoring
2. **Integration testing time** → Parallel development and continuous testing
3. **Documentation time** → Documentation created alongside development

**Contingency Plans:**
- If behind schedule: Focus on core functionality over advanced features
- Security monitoring can be reduced to basic log alerting if needed
- Prioritize working demos over perfect implementations

**Success Criteria:**
- All 5 main deliverables functional by Aug 21st
- Comprehensive documentation by Aug 24th
- Successful final evaluation on Aug 25th

**Final Evaluation: 2025-08-25**

---

**General Tips for Success:**
*   **Communicate Regularly:** Use Apache Beam mailing lists for milestones/blockers.
*   **Break Down Tasks:** Smaller daily/bi-daily goals.
*   **Version Control:** Use Git diligently.
*   **Seek Feedback Early and Often:** Share progress with mentors/community.
*   **Documentation As You Go:** Easier than at the end.
*   **Flexibility:** Be prepared to adjust plan with mentors.
