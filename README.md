# App Versions

A tiny public version manifest polled by Trozovka's shipped desktop apps
to check for updates.

`simple-pdf-editor` and `simple-photo-video-resizer` are private,
closed-source repos, so a shipped `.exe` can't safely query GitHub's API
for their latest release directly (private-repo endpoints need auth, and
embedding a token in a distributed binary would let anyone extract and
misuse it). This repo exists only to be public, so those apps can fetch
`versions.json` anonymously instead.

## Updating a version

Whenever a new version of one of those apps ships:

1. Bump `APP_VERSION` in that app's `app/version.py`.
2. Update this file's matching entry (`version` and, if it changed, `url`)
   to match.
3. Commit and push both.

No CI automation wires these together yet — this is a manual step done
alongside each release.

## Format

```json
{
  "<repo-name>": {
    "version": "<semver as X.Y.Z>",
    "url": "<where a user should go to download the new version>"
  }
}
```

Contains no source code and no secrets — just a version string and a
public download link per app.
