# Vault Conventions for Claude Code

## Frontmatter (required on every note)
---
title: 
created: YYYY-MM-DD
tags: []
type: core | project | area | resource | daily
status: active | done | archived   # only on type: project or area
---
## Tagging (controlled vocabulary)
- Before tagging any note, read 2-Context/Resources/tag-index.md.
- Only use tags that already exist in that index.
- If no existing tag fits the note's content, STOP and ask the user whether to 
  create a new tag — do not add one unilaterally.
- If a new tag is approved, add it to tag-index.md under "Active tags" in the 
  same operation as tagging the note, so the index never drifts out of sync 
  with what's actually in use.
- Never use a tag that's a near-duplicate of an existing one 
  (e.g. don't add "ai-tools" if "ai" already exists and would cover it) — 
  flag the overlap to the user instead

## Linking rules
- Use [[wikilinks]] for all internal references — never markdown links ([text](path)) for notes within this vault.
- Before creating a new note, search 1-Core/ and 2-Context/ for existing related notes.
- If a related note exists, link to it.
- If no related note exists, leave the new note unlinked. Do NOT create placeholder/stub links to nonexistent notes.
- Never silently create a new note just to satisfy a link — if a concept seems 
  to deserve its own note, flag it to the user instead of creating it unprompted.
- Unlinked notes are expected and acceptable, especially early on. They are not 
  an error to fix automatically.

## Note types — what goes where

### 1-Core/
Distilled, durable knowledge — your own conclusions AND important facts/frameworks 
you've internalized as foundational, regardless of original source.
- One idea per note. If a note contains multiple distinct ideas, split it.
- Title states the idea as a claim, not a topic 
  (e.g. "Compound interest rewards patience over timing" not "Compound Interest").
- A note belongs here only after it has been refined — never write directly 
  into 1-Core/ from raw capture. It must pass through 2-Context first.
- Rarely restructured once here. If you're editing a Core note's *meaning* 
  often, it probably wasn't ready to be here yet.

### 2-Context/Inbox/
Raw, unprocessed capture. Anything new lands here first — voice notes, 
half-formed thoughts, article highlights, screenshots-as-text. No frontmatter 
required at point of capture; frontmatter gets added during processing.

### 2-Context/Projects/
Has a defined outcome and an end state. Must include a "Done when:" line 
near the top stating what finished looks like.

### 2-Context/Areas/
Ongoing responsibility with no finish line (health, a role, a relationship, 
a skill you maintain). No "Done when" — areas don't complete, they're maintained.

### 2-Context/Resources/
Reference material and source notes that support Core or Projects but haven't 
been distilled into a standalone Core idea yet. This is where most "facts/frameworks 
you learned from elsewhere" live until they're refined enough to graduate to 1-Core.

### Daily/
Append-only log, one file per day (YYYY-MM-DD.md). Raw timestamped entries. 
Never deleted or restructured — it's a record, not a working document.

## Inbox processing procedure
When the user runs the inbox-processing workflow, for each file in 2-Context/Inbox/:

1. Read the raw note in full.
2. Check if it contains more than one distinct idea. If so, split it into 
   separate notes — one idea per note (see Note types: 1-Core/).
3. Classify each resulting note as one of: resource, project, area, daily-log-item.
   - DEFAULT TO "resource" if uncertain whether something is polished enough 
     for Core. Never place a freshly processed note directly into 1-Core/ — 
     that only happens as a separate, deliberate promotion step, never as 
     part of inbox processing.
4. Add required frontmatter (title, created, tags, type, status if applicable).
5. Tag using ONLY the controlled vocabulary in 2-Context/Resources/tag-index.md.
   If no existing tag fits, stop and ask the user — do not invent tags.
6. Search 1-Core/ and 2-Context/ for related existing notes. Link with 
   [[wikilinks]] if a genuine match exists. If none exists, leave unlinked — 
   do not create stub/placeholder links.
7. Move the processed note to its destination folder (2-Context/Resources/, 
   2-Context/Projects/, or 2-Context/Areas/).
8. Delete the original file from 2-Context/Inbox/ only after the processed 
   version is successfully written elsewhere. Never delete content — only 
   relocate and restructure it.
9. After processing all files, report a summary: how many notes created, 
   where each landed, any new tags proposed, any notes flagged as ambiguous.

## Promoting a note to 1-Core/
This is always a separate, explicit action — never automatic, never bundled 
into inbox processing. The user decides when something has earned a permanent 
place. Claude Code can suggest candidates (e.g. a Resource note referenced 
repeatedly, or a note the user explicitly says "this is now core to how I think") 
but does not move files into 1-Core/ without the user confirming.

## Scope boundaries
- Never modify, move, or delete files inside .obsidian/ or .git/.
- Only operate within 1-Core/, 2-Context/, Daily/, and Templates/ unless 
  explicitly told otherwise.
- Before any operation that touches more than 5 files, remind the user to 
  confirm a recent git commit exists. Do not proceed with bulk changes if 
  the working tree is dirty (uncommitted changes) — ask the user to commit 
  or stash first.
- Never run git commands that rewrite history (rebase, force-push, reset --hard) 
  without explicit user confirmation for that specific operation.