# Phase I journal

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
