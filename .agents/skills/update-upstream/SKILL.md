---
name: update-upstream
description: Update the Spanish PHP The Right Way fork with the latest upstream English content, then translate the newly merged content to Spanish. Use when the user invokes /update-upstream or asks to "update from upstream", "sync with upstream", "merge upstream", or "merge upstream and translate". Merges upstream into upstream-gh-pages, then into gh-pages (committing the sync), diffs the changes under _posts/, translates the new English content to Spanish (left uncommitted for review), and reports everything that changed. Never pushes.
---

# Update Upstream & Translate to Spanish

Workflow for the `wilsenhc/php-the-right-way` fork.

**Repo background**
- `gh-pages` = the **Spanish** translation site (`es.phptherightway.com`). Keep its content fully in Spanish.
- `upstream-gh-pages` = mirror of the English upstream (`codeguy/php-the-right-way`).
- Upstream has **no `main` branch**; its default branch is `gh-pages`. Treat upstream's default branch as "main".
- Site content lives in `_posts/`; site chrome in `_layouts/`, `_includes/`, `_config.yml`.

**Rules of engagement**
- Commit the **initial sync merge** (steps 1–3): the update MUST be committed and confirmed when conflict-free.
- Do **NOT** commit the translation changes (step 4): leave them uncommitted (staged or unstaged, per user preference) for the user to review and commit separately.
- NEVER push or open PRs.
- Keep the site register consistent: **informal "tú"**, never formal "usted".
- Never translate or rewrite code blocks, shell commands, URLs, or link-reference definitions (`[foo]: url`).

## Steps

### 1. Fetch upstream and sync `upstream-gh-pages`
1. `git fetch upstream`
2. Resolve upstream's default branch: `git symbolic-ref refs/remotes/upstream/HEAD` (here: `refs/remotes/upstream/gh-pages`).
3. `git switch upstream-gh-pages` then `git merge --ff-only <upstream-default-branch>`.
   - If it is not a fast-forward, stop and report.

### 2. Merge into `gh-pages` (English wins on conflict)
1. `git switch gh-pages`.
2. **Dry-run first** to preview conflicts without touching the working tree:
   `git merge-tree --write-tree --messages gh-pages <upstream-branch>` — note the CONFLICT files.
3. Run the real merge:
   `git merge -X theirs <upstream-branch>`
   - `-X theirs` = on any conflict, keep the **English/upstream** text (replaces the existing Spanish block), per requirement 2a.
   - If the merge stops with conflict markers, resolve every marker by taking the upstream side (`git checkout --theirs <file>` then `git add <file>`), verify with `grep -n '^<\{7\}\|^=\{7\}\|^>\{7\}'` returning nothing, then commit the resolution.
   - Expected outcome: conflict hunks are English, non-conflicting lines stay Spanish (files are mixed until step 4).

### 3. Commit and confirm the sync merge
- Once there are no more merge conflicts, **commit and confirm the merge** — the initial sync MUST be committed:
  `git commit --no-edit` (uses the default merge message, e.g. "Merge remote-tracking branch 'upstream/gh-pages' into gh-pages").
- Verify: `git status` clean and `git log --oneline -1`.
- If the user needs the site to keep working, this commit is the stable checkpoint; nothing beyond it is committed yet.

### 4. Diff the merged changes in `_posts/`
- The merge is now committed, so diff against its first parent:
  - `git diff HEAD^1 HEAD --name-only -- _posts/` — list changed posts.
  - `git diff HEAD^1 HEAD -- _posts/` — review the incoming English content.
- Enumerate every affected file and what changed (new sections, version bumps, rewordings, link changes).
- Also review the removed (`-`) lines for **Spanish-only content** that `-X theirs` may have silently dropped (e.g. a site-specific link like `<https://t.me/laravelVe>` in `16-03`); restore any that are still relevant.

### 5. Translate the new English content to Spanish
For each changed post, translate the **English that came in** to Spanish.
- Keep front matter, anchors (`{#...}`), code blocks, commands, URLs, and link-reference definitions untouched.
- Preserve the Spanish already in the file — translate only newly merged English text.
- Use informal "tú" and the **translation glossary** below for consistent terminology.
- Preserve the source file's line wrapping and trailing whitespace to keep diffs minimal and reviewable.
- Leave all of this **uncommitted** for the user to review.

### 6. Report what changed and what was translated
Per-file table: file → upstream change → Spanish translation applied. State clearly that the sync merge was committed and the translations are uncommitted and ready for review (`git diff` to review, then the user commits).

### 7. Report non-`_posts/` changes needing translation
The merge also touches files outside `_posts/`. Inspect and translate the English prose in them, then report separately:
- `_config.yml` — `title` / `tagline` / `description` (title stays "PHP: La Manera Correcta"; translate the rest).
- `_layouts/default.html`, `_layouts/page.html` — UI strings, e.g. "Share on X" → "Compartir en X".
- `_includes/welcome.md`, `README.md` — language-list entries, e.g. "German" → "Alemán".
- `index.html`, `LICENSE`, `Gemfile`, scripts — usually no prose; report if anything needs attention.

### 8. Jekyll sanity check (recommended, at the end)
If a local Ruby/Jekyll toolchain is available, build the site to catch things the merge can break:
- `bundle exec jekyll build` — watch for errors from `{% seo %}` (jekyll-seo-tag), missing `images/og-image.png`, or Liquid issues.
- Confirm `Gemfile` uses `github-pages` (provides jekyll-seo-tag by default) or that the plugin is listed.
- Flag pre-existing config quirks worth the user's attention, e.g. `baseurl: /php-the-right-way` vs the `es.phptherightway.com` CNAME.
- If the toolchain isn't available, say so and skip — never block the workflow on it.

## Translation glossary (keep terminology consistent across runs)

| English | Spanish (site usage) |
|---|---|
| PHP: The Right Way | PHP: La Manera Correcta (brand/title) |
| best practices | mejores prácticas |
| current stable version | versión estable actual |
| End of Life | fin de su ciclo de vida / fin de su vida útil |
| backwards compatibility | compatibilidad con versiones anteriores |
| webserver / built-in webserver | servidor web / servidor web integrado |
| Virtual Machine | Máquina Virtual |
| Windows Subsystem for Linux (WSL) | Subsistema de Windows para Linux (WSL) |
| command line / from the command line | línea de comandos / desde la línea de comandos |
| source code | código fuente |
| package manager | gestor de paquetes |
| configuration wizard | asistente de configuración |
| dependency management | gestión de dependencias |
| coding standards | estándares de codificación |
| acceptance testing | pruebas de aceptación |
| functional testing | pruebas funcionales |
| user group (PUG) | grupo de usuarios (PUG) |
| Share on X | Compartir en X |
| German (language link) | Alemán |
| repositories (official) | repositorios (oficiales) |
| script / scripts (files) | archivo(s) de script (keep "script") |

## Additional checks to include

- **Register sweep:** after translating, scan the touched files for stray formal forms (`usted`, `puede *`, `realice|actualice|asegúrese|añada|descargue|ejecute|configure|utilice|tenga`, possessive `su`) and normalize to "tú" (`puedes`, `realiza`, `asegúrate`, `añade`, `descarga`, `ejecuta`, `configura`, `utiliza`, `ten`, `tu`).
- **Anchors are mixed after `-X theirs`:** non-conflicting Spanish anchors (e.g. `use_la_version_estable_actual`) survive even when the text became English — acceptable, but mention it in the report.
- **Code samples:** user-visible strings and comments inside code samples may be translated, but never alter commands or logic.
- **Verify** no left-over conflict markers and no English prose left in the changed posts before reporting.