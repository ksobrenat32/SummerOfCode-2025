# Journal

## Useful scripts

```bash
cd infra && terraform init
terraform plan -out=plan.out
terraform apply plan.out
```

## Useful links

- https://spacelift.io/blog/terraform-tfvars
- https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/google_organization_iam_custom_role
- https://dev.to/ttsakai/terraform-tips-gcp-project-iam-32i9
- https://registry.terraform.io/providers/hashicorp/google/6.32.0/docs/resources/google_project_iam.html#google_project_iam_member-1
- https://betterstack.com/community/guides/logging/gcp-logging/
- https://registry.terraform.io/modules/terraform-google-modules/log-export/google/latest/submodules/logbucket

## Weeks 1-2: GCP Resource Cleaner & Initial Stateless Infrastructure Steps

### PR permissions : 2025-05-29

- Source yml from terraform, avoid python
- commiter, admin, and viewer roles

### PR permissions : 2025-05-30

- The commiter role is a role obtained from modifying the editor role, deleting every permission that contains the word "delete" in it.

## Stale Cleaner : 2025-06-02

- Implemented a stale cleaner runner on my personal server to test it.

## Stale Cleaner : 2025-06-03

- Found the prefixes of the stale Pubsub topics, added them to the cleaner to focus on those topics. [branch](https://github.com/ksobrenat32/beam/tree/stale_claner_implement)

### PR permissions : 2025-06-06

- Mapped the users and roles that exist in the GCP project to their roles in the terraform code.

### PR permissions : 2025-06-09

- Created custom roles.

### PR permissions : 2025-06-11

- Created admin custom role.

### PR permissions : 2025-06-12

- Fixed roles just using supported permissions.
- Separated the roles to be in layers to avoid duplication.

### PR permissions : 2025-06-16

- Sort the permissions in the roles.
- Made the admin role include secret manager permissions.
- Migrate users to the new roles.

### PR permissions : 2025-06-18

- Fix some roles assignments.
- Added the license to the files that required it.

## PR permissions : 2025-06-23

- Fix headers of auto-generated files.
- Add testing to the roles generation.
- Add historic of the roles.

## PR permissions : 2025-06-24

- Make the export users sciript more robust.
- Add a general README to the stale cleaner.
- Move terraform state to a bucket.

## Stale Cleaner : 2025-06-25

Setup a github action to run the stale cleaner on a schedule. The action will run every 6 hours and will delete stale resources that are older than 1 day.

## Stale Cleaner : 2025-06-26

- Moved the github action to an existing gradle script.

## Key Rotation : 2025-06-30

- Initial key rotation implementation.

## Stale Cleaner : 2025-07-01

- Noticed that the stale cleaner was not deleting the resources, it was only marking them as stale. Fixed the issue by disabling the dry run mode in the cleaner. Waiting for approval to run the cleaner on the production environment.

## Stale Cleaner : 2025-07-02

- Quick fix, the deleting function had a problem in the logic. Solved and PR created.


## Key Rotation : 2025-07-03

- Add the disable keys function to the key rotation script.
- Implement a filter to keep n keys enabled.
- Add tests to the key rotation script.

## Key Rotation : 2025-07-04

- Add requirements and license to the key rotation script.

## Key Rotation : 2025-07-07

- Talk with the mentor about the key rotation script, he suggested to control everything inside the script, including the key rotation schedule. This will be done in the next phase. Add logs to the key rotation script. Authentication for the key rotation script will be done through each service.

## Stale Cleaner : 2025-07-09

- Add new prefixes to the stale cleaner.
- Implement a cleaner for stale pubsub subscriptions that do not have a topic.

## GCP Access Terraform : 2025-07-25

- Add Terraform configuration and IAM management scripts for GCP project. The idea is to setup the users and permissions for the GCP project using Terraform, allowing for easier management and automation of the infrastructure.
- Created infrastructure files including main.tf, users.tf, and configuration variables.
- Added Python script to generate user configurations based on current users.

## GCP Access Terraform : 2025-07-26

- Add GitHub Actions workflow to manage GCP User Roles with Terraform automatically.

## Key Rotation / Secret Service : 2025-07-25

- Add ServiceAccountManager class for managing Google Cloud service accounts and keys.

## Key Rotation / Secret Service : 2025-07-27

- Add unit tests for ServiceAccountManager.

## Key Rotation / Secret Service : 2025-07-28

- Add methods to retrieve and delete oldest service account keys in ServiceAccountManager.

## GCP Access Terraform : 2025-07-29

- Move files to infra/iam directory for better organization.

## Key Rotation / Secret Service : 2025-07-29

- Enhance ServiceAccountManager with improved error handling and key management features.
- Added detailed exception handling for key deletion operations.
- Implemented a method to delete the oldest service account keys, allowing for better key management.
- Updated unit tests to include integration tests for full service account lifecycle.
- Added retry logic for key validation to handle propagation delays.

## Key Rotation / Secret Service : 2025-07-30

- Move to other directory name for better organization.
- Refactor ServiceAccountManager to use injected logger for improved logging consistency and add unit tests for ServiceAccountManager functionality.
- Add logging to secret service, save the log file on the gcp bucket.
- Improved typing in the codebase.
- Remove one time only configuration from class.

## GCP Access Terraform : 2025-07-30

- Update project variables and migrate infrastructure.
- Discourage the use of generate.py script in favor of more automated approaches.
- Update readme after migration to reflect new structure and processes.

## Project Planning : 2025-07-31

- **MAJOR PLAN REVISION:** Updated the project plan to realistically cover all promised deliverables in the remaining 25 days.
- **Status Assessment:** 
  - ✅ GCP Resource Cleaner: COMPLETED (automated, GitHub Actions integrated)
  - ✅ GCP Access Control: LARGELY COMPLETED (Terraform roles, automated workflow)
  - 🟡 Key Rotation: IN PROGRESS (ServiceAccountManager done, needs automation)
  - 🟡 Stateless Infrastructure: PARTIALLY STARTED (some Terraform migration)
  - ❌ Security Monitoring: NOT STARTED
- **Strategic Focus:** Intensive 4-week sprint to complete all deliverables with MVP implementations where necessary.
- **Risk Mitigation:** Simplified security monitoring to basic audit log alerting to ensure all 5 main topics are covered.
- **New Timeline:**
  - Week 1 (Aug 1-7): Complete Key Rotation automation
  - Week 2 (Aug 8-14): Finish Stateless Infrastructure with monitoring
  - Week 3 (Aug 15-21): Implement basic Security Monitoring
  - Week 4 (Aug 22-25): Documentation and final evaluation prep
