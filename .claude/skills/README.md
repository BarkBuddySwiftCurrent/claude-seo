# Project Skills: Amazon PPC Advanced Skills

These six skills are vendored from
[nospicyplease/amazon-ppc-advanced-skills](https://github.com/nospicyplease/amazon-ppc-advanced-skills)
at commit `b1ec987` (2026-05-28). They are MIT licensed; see `LICENSE.txt` in each folder.
Claude Code loads every `.claude/skills/<name>/SKILL.md` automatically when a session
opens this repository.

| Skill | Use it for |
|---|---|
| `amazon-ads-performance-drop-diagnosis` | Sales, orders, ROAS, TACoS, BSR, CVR, or traffic dropped: find the cause before changing anything |
| `amazon-growth-opportunity-finder` | ASINs, campaigns, search terms, product targets, and placements that can scale profitably |
| `amazon-account-growth-operating-system` | One prioritized weekly or monthly plan: protect, fix, grow, monitor |
| `amazon-search-term-harvest-planner` | Classify search terms for exact harvesting, controlled tests, negatives, and watchlist |
| `rocketcart-amazon-ads-live-review` | Read-first Sponsored Products review; runs standalone from exports when Rocketcart MCP is not connected |
| `case-camouflage-skill` | Shareable optimization output with exact KPIs but masked ASINs, campaigns, and names |

Invoke a skill with `/<skill-name>`, or describe the task and let Claude pick one. The
upstream docs use Codex's `$<skill-name>` syntax, which means the same thing. None of the
skills write to Amazon Ads: every bid, budget, negative, or pause change stays a proposal
until you approve the exact row.

## Local Changes From Upstream

- `LICENSE.txt` added to each skill folder (the upstream MIT notice).
- `rocketcart-amazon-ads-live-review`: the upstream `docs/GLOSSARY.md` is bundled as
  `references/glossary.md` and the `SKILL.md` link points there, because the original
  `../docs/GLOSSARY.md` path does not exist once the skill is installed on its own.

## Updating

Run from the repository root, then update the commit hash above:

```bash
git clone --depth 1 https://github.com/nospicyplease/amazon-ppc-advanced-skills /tmp/appc
for d in amazon-account-growth-operating-system amazon-ads-performance-drop-diagnosis \
         amazon-growth-opportunity-finder amazon-search-term-harvest-planner \
         rocketcart-amazon-ads-live-review skills/case-camouflage-skill; do
  n=$(basename "$d")
  rm -rf ".claude/skills/$n" && cp -R "/tmp/appc/$d" ".claude/skills/$n"
  cp /tmp/appc/LICENSE ".claude/skills/$n/LICENSE.txt"
done
cp /tmp/appc/docs/GLOSSARY.md .claude/skills/rocketcart-amazon-ads-live-review/references/glossary.md
perl -pi -e 's#See the repo \[glossary\]\(\.\./docs/GLOSSARY\.md\)#See the [glossary](references/glossary.md)#' \
  .claude/skills/rocketcart-amazon-ads-live-review/SKILL.md
git -C /tmp/appc rev-parse --short HEAD
```
