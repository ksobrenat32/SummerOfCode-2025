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
