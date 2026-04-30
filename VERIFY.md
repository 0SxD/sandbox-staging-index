# Quick verification commands

Run these locally to confirm state:

```bash
# 1. List all 0SxD private repos (expect 36+)
gh repo list 0SxD --visibility private --limit 100 | wc -l

# 2. Confirm tonight's 3 new repos
for r in trinity-dialectic 143-protocol agent-creator-handoff-v2; do
  gh repo view 0SxD/$r --json visibility,name,url
done

# 3. Confirm key existing repos
for r in archive-openbrain ce-rd-os github-curator-v01 agent-creator-handoff-v1; do
  gh repo view 0SxD/$r --json visibility,name,size
done

# 4. Inspect ce-rd-os curator pattern (already private, 1-step from public)
gh api repos/0SxD/ce-rd-os/contents/ce-rd-os --jq '[.[] | {name, type}]'
```
