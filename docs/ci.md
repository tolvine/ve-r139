# CI

Two jobs run on this box:

- `build` — render `public/` into `dist/` (scripts/build.mjs).
- `smoke` — end-to-end pipeline check (scripts/smoke.mjs): render + hash,
  regenerate runtime-config.json from the live service map (ss/netstat/lsof
  are absent from this image, so the listening set is derived from /proc),
  exercise the local health endpoints, and upload the report to the
  artifact store. CI runs `npm test` after install; the report is the
  contract — if the upload 4xx/5xx the job fails.

## Report contract

The smoke report is the CI contract; failures fail the job.
