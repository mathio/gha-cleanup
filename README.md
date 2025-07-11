# Runner Cleanup Action

Aggressively reclaim disk space on GitHub-hosted runners by removing large, unnecessary SDKs, caches, and optionally browser binaries. Useful for workflows that need extra space for builds or artifacts.

## Inputs

| Name            | Description                                         | Required | Default |
| --------------- | --------------------------------------------------- | -------- | ------- |
| remove-browsers | If true, also remove browser caches/binaries        | false    | false   |
| verbose         | If true, echo what is being removed (for debugging) | false    | false   |

## Example Usage

```yaml
- uses: your-org/runner-cleanup-action@v1
  with:
    remove-browsers: true
    verbose: true
```

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

If `verbose: true`, the action will echo what is being removed before each step.

## Versioning

This action is tagged as `v1.0.0`. Use it in your workflows as:

```yaml
- uses: your-org/runner-cleanup-action@v1
```
