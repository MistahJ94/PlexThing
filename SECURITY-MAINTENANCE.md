# PlexThing security maintenance

This branch contains conservative source-level security changes. The physical Car Thing must remain disconnected during development and testing.

## Changes made
- Removed Chromium flags that disabled CORS and relaxed localhost transport protections.
- Device ADB commands in the Electron helper are blocked by default. `PLEXTHING_ENABLE_DEVICE_WRITES=1` explicitly enables them; do not set this while using an irreplaceable unmodified device.
- Save Plex connection settings only after a successful connection.
- Stop copying Plex tokens into renderer `localStorage` (existing historical localStorage values are not automatically cleared).

## Outstanding work before release
- Protect Plex credentials in OS-backed storage; current `config.json` remains plaintext.
- Review unauthenticated WebSocket listener on port 8891; any binding/auth change must preserve intended Car Thing connectivity.
- Audit and update dependencies, particularly Electron, with lockfile-aware testing.
- Verify Plex HTTP and HTTPS connection behavior, desktop packaging and regression tests.
- Review existing localStorage migration/cleanup and ADB recovery procedures.

No runtime, device, or cross-platform build verification has been performed yet. Do not merge this branch into `main` until tested.
