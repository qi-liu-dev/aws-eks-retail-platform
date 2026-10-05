# 0001: Separate application and platform repositories

Status: Accepted
Date: 2026-10-05

## Context

This project has two kinds of code. The application comes from AWS's
open-source Retail Store Sample App: five services that I did not write
and will change only slightly. The platform around it (Terraform, Helm
values, Argo CD configuration, monitoring and docs) is my own work and
will change often.

I need to keep these clearly separated so anyone can tell which parts
came from AWS and which I wrote. I also want to pull in upstream changes
later, and Argo CD needs a Git repository that holds the deployment
configuration as the source of truth.

## Options

1. **One repository, application copied in.** Copy the upstream source
   into the platform repository.
2. **One repository, platform inside the fork.** Add Terraform and
   deployment config to my fork of the application.
3. **No fork.** Use AWS's published images and keep only deployment
   config in the platform repository.
4. **Two repositories.** A fork of the application for source changes
   and application CI, plus a separate platform repository for
   infrastructure, deployment config and docs.

## Decision

Option 4.

- The fork stays close to upstream. `git diff v1.6.3` shows exactly what
  I changed, and syncing with upstream stays simple.
- Argo CD's best practices recommend keeping deployment config separate
  from application source
  (https://argo-cd.readthedocs.io/en/stable/user-guide/best_practices/).
  Config-only changes, such as replica counts, don't trigger an
  application build, and deployment history isn't mixed with code changes.
- Every deployment is a commit in the platform repository, so its Git
  history is also the deployment history.
- It matches a common team split: product teams own application
  repositories, and a platform team owns the platform repository.

Option 3 is simpler, but I want to build and push my own images to
practise CI. Options 1 and 2 mix my work with upstream code, which makes
attribution and upstream syncs harder.

## Consequences

- Clear ownership: everything in this repository is my work unless a
  file says otherwise.
- Rolling back a deployment means reverting a commit in this repository.
- CI runs in the fork but has to update image tags in this repository.
  That needs cross-repository write access, so there is one more
  credential to manage (a fine-grained token or a GitHub App).
- Work spans two repositories, so the upstream version has to be
  recorded explicitly. It is pinned at `v1.6.3` in the README.
- How CI updates the image tag (a pull request from CI, or Argo CD Image
  Updater) needs its own decision record.