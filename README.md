# Bexaverse Lore Vault

Voice note → fact-check against canon → confirm → deposit → live wiki.

Plain markdown + YAML frontmatter + `[[wikilinks]]`, versioned in git, rendered by [Quartz](https://quartz.jzhao.xyz/) into a browsable wiki with backlinks and a relationship graph. The `lore-keeper` skill (in `.claude/skills/`) enforces search-first, conflict-flagging, and confirm-before-write.

## Setup (once, ~10 minutes)

1. **Create a private GitHub repo** (e.g. `lore-vault`) and push this folder to it:
   ```bash
   cd lore-vault
   git init -b main
   git add -A
   git commit -m "lore: initial vault"
   git remote add origin git@github.com:YOURNAME/lore-vault.git
   git push -u origin main
   ```
2. **Enable the wiki**: repo → Settings → Pages → Source: **GitHub Actions**. The `deploy-quartz.yml` workflow builds and publishes on every push. Your wiki appears at `https://YOURNAME.github.io/lore-vault/`.
   - Note: GitHub Pages sites on free plans are public even if the repo is private. If your lore must stay secret, keep the workflow off (delete it) and run Quartz locally, or upgrade for private Pages.
3. **Wire up Claude**:
   - **Claude Code** (desktop or mobile app): open the repo — the skill in `.claude/skills/lore-keeper/` is picked up automatically.
   - **Claude app conversations**: save the packaged `lore-keeper.skill` file to your profile (Save skill button), and connect the GitHub connector to this repo so Claude can read/write it from any chat.

## Daily use

Dictate into Claude: *"New lore: Mia's grandmother Zeta founded the first Roster league on the old net."*

Claude will: search the vault → flag anything that contradicts canon → propose exactly which files change → wait for your **yes** → write, commit, push. A minute later the wiki has rebuilt.

## Structure

```
Characters/  Locations/  Factions/  Events/  Timeline/  Projects/
Templates/   ← file templates the skill copies
.claude/skills/lore-keeper/   ← the rules
.github/workflows/deploy-quartz.yml   ← wiki auto-deploy
```

Conventions: lowercase-kebab-case filenames, `status: canon | draft` in frontmatter, every cross-reference is a `[[wikilink]]`, retcons get logged in each file's `## Changelog`.

## Later (optional)

Add an always-on layer (OpenClaw on a VPS) pointed at this same repo for WhatsApp entry, scheduled digests, or the community welcome bot. Nothing here needs to change.
