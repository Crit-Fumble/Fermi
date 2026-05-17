# Modifications

Forked from [MathMan05/Fermi](https://github.com/MathMan05/Fermi) by Crit-Fumble.

Per AGPL-3.0 §5, this file is the canonical index of changes the fork
carries on top of upstream. Detailed history is in git.

## Categories

- **CFG packaging (`Dockerfile.cfg`, `ops/nginx.conf`)** — separate
  multi-stage Dockerfile producing an nginx-alpine runtime serving the
  prebuilt SPA. Upstream's `Dockerfile` (Node-based, runs `npm start`)
  is preserved untouched.
- **Sub-path-aware build (transitional)** — `Dockerfile.cfg`'s build
  stage runs a `sed` rewrite to prefix root-absolute paths with
  `FERMI_BASE_PATH` so the bundle can co-host under any sub-path on
  the Crit-Fumble platform (`/apps/fermi/`). This is transitional;
  future work will move the rewrite into source via real relative
  paths + a `BASE_PATH` constant, at which point the sed step becomes
  a no-op and the Dockerfile drops it.

## Upstream sync

Quarterly manual rebase. Procedure:

```bash
git remote add upstream https://github.com/MathMan05/Fermi.git   # one-time
git fetch upstream
git rebase upstream/main
# Resolve conflicts in Dockerfile.cfg / MODIFICATIONS.md (rare — those
# files don't exist upstream). Source files generally rebase cleanly
# until source-level relative-path patches land.
git push --force-with-lease origin main
git tag v0.1.X && git push origin v0.1.X
```

## License

AGPL-3.0, same as upstream. See `LICENSE`.
