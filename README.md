# journal-adapt-docx

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![Claude Code](https://img.shields.io/badge/Claude_Code-compatible-blueviolet)
![Codex](https://img.shields.io/badge/Codex-compatible-green)
![Version](https://img.shields.io/badge/version-1.2--wps--tracked-brightgreen)

## Personal Note

This is my personal copy of [WantongC/journal-adapt-writing-skill](https://github.com/WantongC/journal-adapt-writing-skill).

The original idea and main framework come from that repository. I keep this copy under my own GitHub account only so I can adjust the skill for my own manuscript-writing needs and sync the same version across my devices.

My main personal change is: when a manuscript is a Word/DOCX file with EndNote, Cite While You Write, Word field codes, automatic numbering, cross-references, captions, or a generated bibliography, the skill should not convert the DOCX to Markdown for revision. It should work on a duplicate DOCX in WPS Writer tracked-changes mode, so I can review and accept/reject edits manually.

This repository is not meant to replace the original project or claim credit for it.

---

## What I Use This For

I want one skill that can keep improving with my own needs, especially for medical manuscript writing.

Examples of things I may keep adding later:

- CONSORT / STROBE / PRISMA awareness
- medical journal writing preferences
- EndNote and Cite While You Write safety
- WPS tracked-changes workflow
- my own preferred revision rules

The goal is simple: adjust the skill once, upload it to GitHub, and reuse the same version on different computers.

---

## My Sync Workflow

### 1. Adjust the skill on one computer

When I notice a new need, I can edit this skill once.

For example, if I want it to pay more attention to CONSORT, STROBE, PRISMA, EndNote, or WPS tracked changes, I can ask Codex to update the skill files in this local repository:

```bash
cd /Users/shirc/Documents/投稿/journal-adapt-writing-skill
```

### 2. Upload the updated skill to GitHub

After the skill is changed, commit and push:

```bash
git add .
git commit -m "Update journal-adapt skill"
git push
```

Then the GitHub copy is updated:

```text
https://github.com/NancyShiRC/journal-adapt-docx
```

### 3. Install on another computer for the first time

On a new computer:

```bash
git clone git@github.com:NancyShiRC/journal-adapt-docx.git
mkdir -p ~/.codex/skills/journal-adapt-writing-skill
cp -R journal-adapt-docx/skill/* ~/.codex/skills/journal-adapt-writing-skill/
```

Then restart Codex.

### 4. Update another computer later

If the repository already exists on that computer:

```bash
cd journal-adapt-docx
git pull
cp -R skill/* ~/.codex/skills/journal-adapt-writing-skill/
```

Then restart Codex.

This way, I do not need to teach or modify the skill again on every computer. I only keep GitHub as the shared copy.

