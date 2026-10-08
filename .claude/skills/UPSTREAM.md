# Vendored skills

`brag/` and `brag-slim/` are copied unmodified from
https://github.com/latent-spaces/brag (MIT, see `LICENSE` in each folder),
`skills/` at commit `7079945d391573edebe48fdc0a23b39c4b4e8726`.

Repo-specific overrides (Instagram Reels defaults) live in `/CLAUDE.md`.

To re-sync:

```sh
git clone --depth 1 https://github.com/latent-spaces/brag /tmp/brag
rsync -a --delete --exclude LICENSE /tmp/brag/skills/brag/ .claude/skills/brag/
rsync -a --delete --exclude LICENSE /tmp/brag/skills/brag-slim/ .claude/skills/brag-slim/
```
