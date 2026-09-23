---
name: tray-ai-promote-a-project-between-environments
description: >-
  Move a Tray project from a development workspace to a production workspace safely — version it,
  export it, check what the target needs, preview the import, then commit. Use this for CI/CD and
  release management of Tray integrations, and any time an agent is asked to "ship" or "promote" a
  Tray project.
api: Tray.ai Platform API
base_url: https://api.tray.io/core/v1
auth: 'Authorization: Bearer <RBAC API token>'
operations:
  - PublicApiProjectController.createProjectVersion
  - listProjectVersions
  - exportAProjectVersion
  - PublicApiProjectController.getProjectImportRequirements
  - PublicApiProjectController.previewProjectImport
  - PublicApiProjectController.importProject
generated: '2026-09-02'
method: generated
source: openapi/_original/tray-ai-platform-api-published-openapi.yaml, cli/tray-ai-cli.yml, conventions/tray-ai-conventions.yml
---

# Promote a Tray project between environments

This is one of the few Tray flows with a real pre-flight story — use it, because there is no
rollback on the other side.

## Choose your tool

- **API** — the operations below, for your own pipeline.
- **Tray Sync CLI** — `npm install -g @trayai/tray-sync-cli` (Node >= 22), then `tray init`,
  `tray pull`, `tray env add`, `tray env resolve`, `tray promote`. It wraps these same operations and
  adds local checksum drift detection (`tray status`, zero API calls). Prefer it for anything a human
  will run.

Tokens are per workspace and per region. `tray auth set -w <workspace-id> -r <region> -t <token>`.

## Step 1 — cut a version in the source workspace

`PublicApiProjectController.createProjectVersion` →
`POST /core/v1/projects/{projectId}/versions/{versionNumber}`

Version first. The export is of a *version*, not of the live project, so an uncut project promotes
whatever the last version was.

## Step 2 — confirm what exists

`listProjectVersions` → `GET /core/v1/projects/{projectId}/versions`

## Step 3 — export

`exportAProjectVersion` → `GET /core/v1/projects/{projectId}/versions/{versionNumber}/export`

**Keep this artifact.** It is the only restore path Tray publishes for a project, and it is
client-side. Nothing on the Tray side undoes a bad import.

## Step 4 — ask the target what it needs

`PublicApiProjectController.getProjectImportRequirements` →
`POST /core/v1/projects/{projectId}/imports/requirements`

This tells you which authentications and config values the target workspace must supply. Authentications
do **not** travel with the project — a prod import needs prod auths, and creating them is a separate,
often interactive, step.

## Step 5 — preview

`PublicApiProjectController.previewProjectImport` →
`POST /core/v1/projects/{projectId}/imports/previews`

This is your dry run. Read it before you commit. The Tray Sync CLI does the same thing and **refuses
the promotion outright if anything is unresolved** — replicate that behaviour in your own pipeline
rather than importing and hoping.

## Step 6 — import

`PublicApiProjectController.importProject` → `POST /core/v1/projects/{projectId}/imports`

## After the import

- The first import into a new prod environment usually has to be done by hand, so the correct prod
  authentications can be selected. Imports after that can be programmatic.
- For Embedded, a new project version does not reach end users until the Solution is released —
  see `POST /core/v1/solutions/{solutionId}/releases`, with
  `POST /core/v1/solutions/{solutionId}/releases/previews` as its dry run.

## Reversibility

There is no `demote`, no import rollback, and no version pinning on the target after the fact. Your
recovery plan is: keep the previous export, and re-import it. Verify you can actually do that before
you promote anything that matters.
