# Task B – Terraform Error: `Error locking state`

This task is about a Terraform setup that uses an S3 backend and returns the error `Error locking state`.

## What is the problem?

Terraform state is a shared file that keeps track of infrastructure resources.

When Terraform wants to update the state, it first tries to lock it.  
This is done so that two people or two pipelines do not change the same infrastructure at the same time.

The error usually happens because:
- someone else is already running Terraform against the same state,
- a previous run failed and left a stale lock,
- or the backend setup is not safe enough for team usage.

The original backend looks like this:

```hcl
terraform {
  backend "s3" {
    bucket = "terraform-state-storage"
    key    = "devopsacademy/infra.tfstate"
    region = "eu-west-1"
  }
}
