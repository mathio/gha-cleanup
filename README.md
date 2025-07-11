# 🚀🧹💾 Runner Cleanup Action

Aggressively reclaim disk space on GitHub-hosted runners by removing large, unnecessary SDKs, caches, and optionally browser binaries. Useful for workflows that need extra space for builds or artifacts.

Read more at DEV.to: [Squeezing Disk Space from GitHub Actions Runners: An Engineer's Guide](https://dev.to/mathio/squeezing-disk-space-from-github-actions-runners-an-engineers-guide-3pjg)

## Inputs

| Name            | Description                                         | Required | Default |
| --------------- | --------------------------------------------------- | -------- | ------- |
| remove-browsers | If true, also remove browser caches/binaries        | false    | false   |
| verbose         | If true, echo what is being removed (for debugging) | false    | false   |

## Example Usage

```yaml
- uses: mathio/gha-cleanup@v1
  with:
    remove-browsers: true
    verbose: true
```

## Results

📊 Disk space **before** cleanup:

```
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        72G   44G   28G  62% /
```

📊 Disk space **after** cleanup (with `remove-browsers: true`):

```
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        72G   16G   57G  22% /
```

The action reclaims almost 30 GB of disk space.

## What gets removed?

- Always:
  - `/usr/lib/jvm`
  - `/usr/share/dotnet`
  - `/usr/share/swift`
  - `/usr/local/.ghcup`
  - `/usr/local/julia*`
  - `/usr/local/lib/android`
  - `/opt/az`
  - `/usr/local/share/powershell`
  - `/opt/hostedtoolcache`
- If `remove-browsers: true`:
  - `/usr/local/share/chromium`
  - `/opt/microsoft`
  - `/opt/google`
  - `/usr/lib/firefox`
- Docker system and builder cache is always pruned.

## Logging

If `verbose: true`, the action will echo what is being removed before each step.

## Versioning

This action is tagged as `v1.0.0`. Use it in your workflows as:

```yaml
- uses: mathio/gha-cleanup@v1
```
