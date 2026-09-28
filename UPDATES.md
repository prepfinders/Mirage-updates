# Update manifest (maintainer notes)

This repo hosts Mirage's public update feed. The in-app update check reads
`appcast.json`; `source.json` is an AltStore/SideStore source.

## Publish a new version
1. Ship the new build (bump `MARKETING_VERSION`).
2. Create a GitHub release tagged `vX.Y.Z` and upload `Mirage.ipa` to it.
3. Edit `appcast.json`:
   - `version` — the new version (e.g. `2.9.0`)
   - `notes` — what's new (shown in-app)
   - `url` — where users get it
4. Edit `source.json` — add a new entry at the **top** of `apps[0].versions`:
   - `version`, `date` (YYYY-MM-DD), `localizedDescription`
   - `downloadURL` — `.../releases/download/vX.Y.Z/Mirage.ipa` (must resolve —
     AltStore/SideStore will try to download it)
   - `size` — exact byte size of the uploaded IPA
   - `minOSVersion`
5. Bump the version badge in `README.md`.
6. Validate both JSON files (`python3 -m json.tool source.json`), then commit +
   push. Mirage picks it up on next check (Settings → Updates).

Only bump `version` above the shipped build when an update is actually available.
