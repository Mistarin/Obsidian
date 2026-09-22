# Agent README — Tresor

This file is the operating guide for agents working in the Tresor folder. The
Obsidian-specific section describes the `Mistarin` vault and was checked on
2026-09-21. Plugin versions, settings, permissions, and documentation can
change; verify the current vault configuration before relying on a detail.

## General operating rules

1. Read the relevant note and the plugin documentation before making a
   plugin-specific change.
2. Prefer plain Markdown, YAML properties, wikilinks, and standard Obsidian
   syntax so notes remain portable. Use a plugin only when its added behavior
   is actually needed.
3. Preserve existing frontmatter, links, embeds, task markers, query blocks,
   board syntax, and plugin-generated files unless the user asks to change
   them.
4. Treat plugin-generated views as projections of source files. Before a
   destructive operation, identify the source of truth and make a backup or
   commit when appropriate.
5. Use command-palette commands and plugin settings for normal workflows.
   Edit `.obsidian/plugins/*/data.json` directly only when explicitly asked or
   when the documented UI cannot perform the required change.
6. Do not expose API keys, tokens, private note contents, or AI prompts in
   responses, commits, or documentation.
7. After editing, validate Markdown structure, YAML, internal links, query
   syntax, and any generated files affected by the change.

## Mandatory workflow for every task

Use this workflow before making a change. It is deliberately short so an
agent does not redo diagnostics or expand a narrowly scoped request.

1. **Confirm the request and scope.** Separate the current user request from
   old transcript context. If the user asks to update this README, edit
   `AGENTS.md`; do not continue editing a note mentioned in an earlier
   request unless the user asks for both. Do not change plugin settings,
   create notes, move files, or commit anything unless that is in scope.
2. **Locate the source of truth.** Use `rg --files` for filenames and `rg -n`
   for content. Search the likely folder first (for example, `Mistarin/7GALP`)
   and record the exact path before opening or editing it. Do not create a
   second note because a search result is ambiguous; inspect the candidates
   and choose the existing source file.
3. **Read before rewriting.** Read the complete relevant note, or the
   relevant sections when it is very large. Preserve frontmatter, headings
   with links, wikilinks, embeds, callouts, task markers, code/query blocks,
   inline fields, and plugin syntax. “Format nicely” means improving
   structure and readability while retaining facts; it does not authorize
   summarizing, inventing, deleting, or moving content.
4. **Make one minimal edit.** Use `apply_patch` and quote paths containing
   spaces or special characters. Keep UTF-8 and the existing line-ending
   style. Do not use shell redirection or a whole-file rewrite for a local
   Markdown cleanup, and do not touch unrelated files.
5. **Verify the actual result.** Reopen the changed file, inspect the edited
   sections, check that Markdown fences and YAML frontmatter still pair
   correctly, and search for accidental mojibake or broken link syntax. Only
   claim success after the file on disk contains the intended change.
6. **Report precisely.** Name the files actually changed and the checks that
   passed. If a command failed or a change was not applied, say so plainly;
   never describe a planned or attempted edit as completed.

### Link creation convention

For every newly created link, write one context line using this exact
template:

```text
<složka> / <existující_odkaz> / <nový_odkaz>
```

Field definitions:

- `<složka>` = containing folder of the source note;
- `<existující_odkaz>` = existing/source link;
- `<nový_odkaz>` = link just created.

Do not change the field order or omit a field. Use valid Obsidian wikilinks
or Markdown links as field values and verify that every target exists.

### `!!` link trigger and context lookup

Treat any non-empty text immediately followed by `!!` as a link-creation
request:

```text
<text>!!
```

Process the request in this order:

1. Search existing created files for a matching definition or relevant
   context.
2. If a definition exists, reuse it and create the link to that definition;
   do not create a duplicate.
3. If no definition exists, create one using the available context, then
   create the link to it.
4. Apply the link format from the preceding section and verify the target.

### `??` expansion and `?!` subpage explanation

Treat any non-empty text immediately followed by `??` as a request to expand
the text and provide a clear explanation in the current note:

```text
<text>??
```

Treat any non-empty text immediately followed by `?!` as a request to provide
the explanation in a dedicated subpage and link that subpage to the triggering
text:

```text
<text>?!
```

For `?!`, search for an existing relevant subpage first and reuse it instead
of creating a duplicate. If none exists, create the subpage in the parent
note's `Odkaz/` folder, add the explanation there, create the link from the
parent note, and follow the link creation convention above. Preserve existing
content and verify the new link target.

### Rich text formatting and styling guidelines

Actively use rich Markdown formatting in note text to enhance visual hierarchy, scannability, and clarity:

- **Bold (`**text**`)**: Highlight key terms, fundamental concepts, definitions, and main takeaways.
- *Italics (`*text*`)*: Secondary notes, Latin/English technical terms, variable explanations, and subtle remarks.
- ==Highlight (`==text==`)==: Use Obsidian highlight syntax for critical exam points, crucial definitions, core formulas, and must-remember facts.
- Citations & Callouts (`> text`): Use standard blockquotes for lecture definitions, and Obsidian callouts (`> [!NOTE] Title\n> Contents`, `> [!info]`, `> [!example]`, etc.) for key takeaways and emphasized context.
- Dividers (`---`): Use horizontal rules to cleanly separate logical topics and sections.

### Do not add AI disclaimers

Do **not** add AI-generated-content disclaimers (e.g., `<small><span style="color: gray;">Tento odstavec byl vygenerován AI...</span></small>`). Keep notes clean, authentic, and free of automated AI tags or disclaimers unless explicitly requested by the user.

### Plain, human-friendly language (psát lidsky a srozumitelně)

Avoid unnecessarily complicated, rigid, or academic definitions. Write notes clearly, naturally, and with human accessibility in mind:
- **Prefer simple, everyday words over heavy jargon**: Whenever an intuitive equivalent exists, use it or provide it prominently (e.g. use *trvalý / stálý* instead of *perzistentní*, *souběžný přístup* instead of *konkurentní přístup*, etc.).
- **Explain concepts intuitively**: Pair formal definitions with practical analogies or simple real-world explanations rather than dry textbook jargon.
- **Maintain precision without academic fluff**: Keep core distinctions accurate (e.g. data vs. information), but explain them in language that is straightforward to read and study.

### Task, checklist, and context commands

Use the following command suffixes for task and note operations. A command
must contain non-empty text before its suffix and must be interpreted only
when the suffix is explicitly present.

| Command | Operation | Write behavior |
| --- | --- | --- |
| `<text> >>` | Create task(s) in the current note | Writes to the current note |
| `<text> >> checklist` | Force a multi-item checklist | Writes to the current note |
| `<text> >> todolist` | Create a standard task list | Writes to the current note |
| `<text> %%` | Format existing content as a structure or checklist | Writes only the requested formatting change |
| `<text> <<` | Find related notes and produce a linked overview | Read-only unless writing is explicitly requested |

Task and checklist items must use standard Markdown task syntax:

```markdown
- [ ] Open task
- [x] Completed task
```

Apply these rules when processing task commands:

1. Use the current note as the default destination. Do not create a central
   task note unless the user explicitly requests one.
2. For plain `<text> >>`, create one task unless the input contains a clearly
   structured list of steps; in that case, create one task per step.
3. Treat `checklist` and `todolist` as explicit multi-item modes. Preserve
   the order of the source steps and do not invent steps that are not implied
   by the source content.
4. Search the current note and its existing context before creating a task.
   Do not add an equivalent task twice. Keep the existing task as the source
   of truth when a matching task already exists.
5. Add dates, priorities, recurrence, or other Tasks metadata only when the
   user provides it explicitly. Do not infer deadlines or priority.
6. Use `%%` to improve structure or convert clearly actionable content into
   tasks. Preserve the original meaning, facts, links, and non-actionable
   context.
7. Use `<<` as a read-only lookup by default. Search exact paths and titles,
   then the current folder, then the rest of the vault; verify every linked
   target before presenting the overview.
8. Do not add AI disclaimers to generated tasks or checklists.

After a task or checklist operation, verify the destination note, checkbox
syntax, item count, duplicate handling, and preserved links. The Tasks plugin
may render or query these Markdown tasks, but the task lines in their source
notes remain the canonical data.

### Do not repeat a failed check blindly

Treat each command result as information. If a command fails, diagnose the
failure once (wrong directory, missing file, invalid repository, permissions,
or malformed input), choose the appropriate fallback, and do not rerun the
same command unchanged. If a file has not changed, rely on the already
obtained result instead of repeating identical searches, dumps, or status
checks. Re-run a check only after the relevant file or state has changed.

The presence of a directory named `.git` is not proof that Git is usable. Run
one repository probe from the intended workspace, for example:

```sh
git -C "/home/martin/Main/Cloud/Trezor" rev-parse --is-inside-work-tree
```

If that probe fails, record that the workspace is not a valid Git checkout and
stop issuing `git status`, `git diff`, `git log`, `git commit`, `git pull`, or
`git push` commands for this task. Do not run `git init`, create a fake
baseline, or remove/rebuild `.git` unless the user explicitly requests Git
setup. Use direct file inspection and a non-destructive local comparison when
Git is unavailable. This rule also applies when `.git` exists but is empty,
incomplete, or points to a missing worktree.

### GALP and Markdown-formatting tasks

For a request such as “format GALP nicely”:

1. Find the exact GALP note with `rg --files`/`rg -n`; do not assume that a
   title is a filename and do not infer that a failed previous attempt changed
   the file.
2. Read the current file bytes as text and inspect its existing structure
   before editing. Use a byte/encoding inspection only when the text appears
   corrupted; a raw `od`/hex dump is diagnostic output, not a substitute for
   reading the note.
3. Keep all substantive information and existing links. Group related prose
   under clear headings, turn genuine enumerations into lists, preserve exam
   questions as visible questions, and isolate a hardware or other tangent
   only when doing so does not lose text or links. Do not create a separate
   note unless the user explicitly asks for a split.
4. After the patch, inspect the full result or every changed region, count
   headings/list items when useful, and check that no paragraphs disappeared.
   If the note contains Obsidian/plugin blocks, validate their delimiters and
   leave their syntax unchanged.
5. Prefer a clear information flow over wide tables: state the main idea first,
   place supporting detail in a collapsible Obsidian callout such as
   `> [!info]- Podrobnosti`, or link to an existing detailed note. Use a table
   only when a side-by-side comparison is genuinely clearer.
6. When a topic needs more than a short summary, create a dedicated child note
   in the parent note's `Odkaz/` folder, keep the parent note concise, and link
   to the child note. Keep broader explanations in the child note rather than
   expanding the parent with long blocks or wide tables.

### UVDT terminological rules: Data vs. Informace

When editing, structuring, or generating content for **7UVDT** (and general database / information systems notes):

1. **Never interchange "data" and "informace".** There is a fundamental conceptual difference between them:
   - **Data (údaje)**: Raw, uninterpreted symbols, values, characters, or measurements (e.g. numbers `120/80`, raw text, byte values). By themselves, data ==do not provide information== if they lack context, schema, units, or interpretation rules.
   - **Informace (Information)**: Data that have been processed, given meaning, and placed into context so that they can be reasonably interpreted. Crucial definition: *„Informace je sdělení, které odstraňuje v příjemci informace neurčitost, resp. neznalost.“*
2. **Respect database vs. information system terminology**:
   - A database (báze dat / databázový systém) primarily stores and organizes **data**.
   - Redundancy in database context is **redundance dat** (identical data/values stored in multiple places), never "redundance informací".
   - Do not substitute one word for the other for stylistic variation; always use the conceptually accurate term.
3. **Use human-friendly, plain language**: Avoid overly complicated textbook definitions. Wherever an accessible term exists, prefer it or state it clearly (e.g. use *trvalý / stálý (uložený na disk)* instead of *perzistentní*, *souběžný přístup* instead of *konkurentní přístup*, etc.).

## Plugin selection decision process

Before using a plugin, identify the requested outcome and apply the first
matching rule below. Use the plugin's documented workflow and keep the
underlying Markdown or other source file as the source of truth.

1. If the task only requires reading, editing, formatting, linking, or
   explaining portable Markdown and no plugin behavior is needed, use standard
   Markdown and built-in tools without a plugin.
2. If the task edits, formats, sorts, or calculates a Markdown table, use
   **Advanced Tables**.
3. If an AI agent must read, explain, search, transform, or create vault
   content, use **Copilot**.
4. If the task builds a live list, table, calendar, calculation, or task view
   from note metadata, use **Dataview**.
5. If the task creates a diagram, flowchart, visual map, or annotated visual
   note, use **Excalidraw**.
6. If the task reviews, versions, backs up, commits, or synchronizes vault
   changes, use **Git**.
7. If the task assigns decorative icons to files, folders, notes, tabs, or
   text, use **Iconize**.
8. If the task migrates content from another application or file format, use
   **Importer**.
9. If the task organizes cards by workflow state, use **Kanban**.
10. If the task performs fast ranked full-text or attachment search, use
    **Omnisearch**.
11. If the task reorders, indents, folds, or navigates nested lists, use
    **Outliner**.
12. If the task captures content or chains repeatable commands and scripts,
    use **QuickAdd**.
13. If the task only reopens or navigates recently used notes, use **Recent
    Files**.
14. If the task finds semantically related notes or concepts, use **Smart
    Connections**.
15. If the task tracks, filters, schedules, or queries actionable tasks, use
    **Tasks**.
16. If the task generates dynamic note content from a template, use
    **Templater**.

If multiple rules match, choose the plugin that owns the primary output and
source of truth; add another plugin only when its separate behavior is
required. If no rule matches, use standard Obsidian functionality and plain
Markdown, then consult the enabled-plugin list and relevant documentation
before introducing a new plugin workflow.

After choosing a plugin, read the relevant note and plugin documentation
before changing anything, request approval for sensitive or destructive
actions, and verify the resulting source files afterward.

### Plugin selection at a glance

| Need | Use first | Output/source of truth |
| --- | --- | --- |
| Edit or calculate a Markdown table | Advanced Tables | The Markdown table and optional `TBLFM` comments |
| Ask an AI agent to work inside the vault | Copilot | The notes/files changed by the approved agent action |
| Build live lists, tables, or calculations from metadata | Dataview | YAML/frontmatter, inline fields, and note content; Dataview renders a view |
| Draw a diagram or visual explanation | Excalidraw | `.excalidraw` drawing, plus exported PNG/SVG when portability is needed |
| Version, review, or back up vault changes | Git | Git commits and the configured remote; Git is not live sync |
| Add visual icons to files, folders, notes, or text | Iconize | Icon metadata/settings and the underlying note/file names |
| Migrate notes from another app or format | Importer | Imported Markdown/files after staging and review |
| Organize cards in a Markdown-backed board | Kanban | The Kanban Markdown file and linked notes/cards |
| Search the vault and indexed attachments | Omnisearch | Search results; source files remain unchanged |
| Reorder, indent, fold, and navigate nested lists | Outliner | The original Markdown list |
| Create repeatable capture and automation commands | QuickAdd | The configured choice and the files it writes |
| Reopen recently used notes | Recent Files | Navigation only; note contents remain unchanged |
| Find semantically related notes | Smart Connections | Local embedding/index data and the original notes |
| Track and query actionable tasks | Tasks | Markdown task lines in their source notes |
| Generate dynamic note content from templates | Templater | The template file and the generated note |

## Enabled Obsidian plugins in `Mistarin`

These 15 community plugins are enabled in
`.obsidian/community-plugins.json`. Versions come from each local
`.obsidian/plugins/*/manifest.json`.

| Plugin | ID | Version | Primary role |
| --- | --- | ---: | --- |
| Advanced Tables | `table-editor-obsidian` | 0.23.2 | Markdown-table editing, navigation, formatting, and formulas |
| Copilot | `copilot` | 4.0.9 | AI chat and agents inside the vault |
| Dataview | `dataview` | 0.5.68 | Metadata indexing and live queries |
| Excalidraw | `obsidian-excalidraw-plugin` | 2.27.3 | Drawings, diagrams, and visual notes |
| Git | `obsidian-git` | 2.40.0 | Git version control and remote backup workflows |
| Iconize | `obsidian-icon-folder` | 2.14.7 | Icons for files, folders, notes, tabs, and text |
| Importer | `obsidian-importer` | 3.1.7 | Migration from other apps and formats |
| Kanban | `obsidian-kanban` | 2.0.51 | Markdown-backed Kanban boards |
| Omnisearch | `omnisearch` | 1.31.0 | Fast ranked vault and attachment search |
| Outliner | `obsidian-outliner` | 4.10.2 | Structured list editing and navigation |
| QuickAdd | `quickadd` | 2.27.0 | Fast capture, templates, macros, and automation |
| Recent Files | `recent-files-obsidian` | 1.7.10 | Recently opened file navigation |
| Smart Connections | `smart-connections` | 4.7.2 | Local semantic related-note discovery |
| Tasks | `obsidian-tasks-plugin` | 8.4.0 | Task metadata, recurring tasks, and task queries |
| Templater | `templater-obsidian` | 2.25.1 | Dynamic templates and JavaScript-enabled note automation |

## Obsidian plugin workflows

### 1. Advanced Tables (`table-editor-obsidian`)

**Use it when:** editing a Markdown table, adding/removing rows or columns,
aligning columns, sorting rows, exporting CSV, or calculating table values.

**Workflow:**

1. Put the cursor in a Markdown table. To start one quickly, type `|`, enter
   the first heading, and press `Tab` to create the table structure.
2. Use `Tab` and `Shift+Tab` to move between cells and `Enter` to move to the
   next row. Use the command palette or the table controls sidebar for row,
   column, alignment, sort, and export operations.
3. For calculations, add a `TBLFM` HTML comment directly after the table and
   evaluate it from the table formula controls. Keep formulas readable and
   verify the calculated values after edits.

**Important:** formulas are stored as comments and remain in the Markdown
file. The plugin documentation warns that bugs can delete table data, so use
Git or another backup before large table transformations. On mobile, use the
toolbar/sidebar commands because keyboard `Tab`/`Enter` navigation is limited.

**Docs:** [plugin help](https://github.com/tgrosinger/advanced-tables-obsidian/blob/main/docs/help.md), [formula reference](https://github.com/tgrosinger/md-advanced-tables/blob/main/docs/formulas.md), [community listing](https://community.obsidian.md/plugins/table-editor-obsidian).

### 2. Copilot (`copilot`)

**Use it when:** an AI agent needs to read, explain, search, transform, or
create vault content, or when a short rewrite/explanation is useful without
leaving Obsidian.

**Workflow:**

1. For desktop multi-step work, open **Agent Chat** from the ribbon or command
   palette. For short editor tasks, use Quick Ask, Quick Chat, or Copilot
   Commands.
2. Configure the required agent under **Settings → Copilot → Basic → Agents**.
   For Codex, use the managed `codex-acp` adapter when possible, sign in, and
   choose a model. A custom adapter must be compatible with the documented
   minimum version.
3. Use a Copilot Project for a focused topic or client, and enable only the
   skills needed for that agent. Use explicit note/file context rather than
   asking an agent to inspect the entire vault unnecessarily.
4. Choose a conservative permission setting. Ask for approval before writes,
   moves, deletions, external requests, or other sensitive actions.
5. Review the agent's proposed changes and verify the resulting files before
   considering the task complete.

**Important:** Agent Chat is desktop-only; Quick Chat, Copilot Commands, and
Quick Ask remain available for shorter tasks and mobile. AI output is not a
source of truth: preserve citations, check calculations, and inspect every
file changed by an agent. Do not put API keys in notes; use the documented
provider/BYOK or managed-agent settings.

**Docs:** [Copilot getting started](https://docs.obsidiancopilot.com/getting-started/), [Agent Chat](https://docs.obsidiancopilot.com/agent-chat/), [context and mentions](https://docs.obsidiancopilot.com/context-and-mentions/), [skills](https://docs.obsidiancopilot.com/skills/).

### 3. Dataview (`dataview`)

**Use it when:** notes contain structured metadata and you need live lists,
tables, calendars, grouping, sorting, calculations, or task views.

**Workflow:**

1. Decide on a stable metadata schema. Use YAML frontmatter for file-level
   data or inline fields such as `[status:: active]` for content-local data.
2. Start with a `dataview` query block and DQL. Use `FROM` to scope to a
   folder/tag, then `WHERE`, `SORT`, `GROUP BY`, and a display type such as
   `LIST`, `TABLE`, or `TASK`.
3. Use `dataviewjs` only when DQL or an inline query cannot express the view.
   Keep JavaScript small, deterministic, and readable.
4. After changing metadata, allow the index to refresh and check the rendered
   view in Reading mode and Live Preview.

Example:

```dataview
TABLE status, due
FROM "Projects"
WHERE status != "done"
SORT due ASC
```

**Important:** Dataview is primarily for displaying and calculating; it does
not edit note metadata. Query only indexed metadata, not arbitrary prose. A
Dataview task checkbox can update its source task, so review before clicking
interactive task results. Scope queries to folders/tags to keep large vaults
fast.

**Docs:** [Dataview documentation](https://blacksmithgu.github.io/obsidian-dataview/), [metadata](https://blacksmithgu.github.io/obsidian-dataview/annotation/metadata-pages/), [query language](https://blacksmithgu.github.io/obsidian-dataview/query/queries/), [JavaScript queries](https://blacksmithgu.github.io/obsidian-dataview/api/intro/).

### 4. Excalidraw (`obsidian-excalidraw-plugin`)

**Use it when:** a concept is clearer as a diagram, flowchart, sketch, visual
map, annotated image, or hand-drawn explanation than as prose.

**Workflow:**

1. Create a drawing from the ribbon, file explorer, or command palette. Keep
   editable drawings in a deliberate folder, such as `Attachments/Drawings`.
2. Add links to notes or other drawings from inside the canvas. Keep diagrams
   focused and link supporting explanations back to Markdown notes.
3. Embed an editable drawing when the viewer has the plugin:
   `![[diagram.excalidraw|800]]`.
4. For Publish, external viewers, or portability, enable auto-export to PNG or
   SVG and embed the exported image instead. Use the `excalidraw-autoexport`
   frontmatter key when a single file needs an override (`none`, `png`, `svg`,
   or `both`).
5. Before moving or renaming drawings, check linked embeds and exported files.

**Important:** Excalidraw source files are not rendered by Obsidian Publish;
exported PNG/SVG files are needed there. Scripts, OCR, external images, PDF
export, and other advanced features may access files or network resources;
enable only what the task needs. Keep the editable source alongside exports
and let Git track both when they are part of the vault.

**Docs:** [official README](https://github.com/zsviczian/obsidian-excalidraw-plugin/blob/master/README.md), [community listing](https://community.obsidian.md/plugins/obsidian-excalidraw-plugin), [community wiki](https://community.sketch-your-mind.com/Wiki).

### 5. Git (`obsidian-git`)

**Use it when:** reviewing changes, creating recoverable history, committing
vault work, or pushing/pulling an asynchronous backup to a configured remote.

**Workflow:**

1. Confirm the vault is a valid Git repository with one `git rev-parse`
   probe, and confirm that `.gitignore` excludes secrets, caches, transient
   files, and any files the user does not want versioned. A `.git` directory
   by itself is not sufficient. If the probe fails, skip Git commands and use
   the local verification procedure in **Do not repeat a failed check
   blindly**.
2. Configure authentication and the remote in the plugin settings. Never put
   passwords or tokens in notes or commit messages.
3. Before a large edit, inspect the source-control view and make a baseline
   commit if appropriate and authorized. After editing, review the diff, stage
   only intended files, write a meaningful commit message, and commit.
4. Pull before pushing when collaborating asynchronously. Resolve conflicts
   deliberately; do not overwrite a remote or local version just to make the
   working tree clean.
5. Use the history and diff views to recover or compare note versions. Enable
   automatic commit-and-sync only after confirming its pull/push behavior and
   interval.

**Important:** Git is version control, not live synchronization. It is not
appropriate for simultaneous editing of the same note. Mobile support is
experimental and has authentication, memory, merge, and submodule limits.
Never run a destructive repository operation without explicit authorization
and a verified target.

**Docs:** [Git plugin documentation](https://publish.obsidian.md/git-doc), [plugin README](https://github.com/Vinzent03/obsidian-git/blob/master/README.md), [authentication guide](https://publish.obsidian.md/git-doc/Authentication).

### 6. Iconize (`obsidian-icon-folder`)

**Use it when:** visual scanning of the file explorer, folders, tabs, note
titles, or selected text benefits from consistent icons and colors.

**Workflow:**

1. Install or select an icon pack in the plugin settings.
2. Assign icons to high-level folders and important note types first. Use
   custom rules or frontmatter integration only when the convention is stable.
3. Use SVG icons or supported icon-pack entries for custom icons, and check
   both dark and light themes if the vault theme changes.
4. Keep the icon scheme decorative and documented; the note title, path, tags,
   and properties remain the semantic source of truth.

**Important:** The plugin's community listing indicates project deprecation/end
of maintenance. Do not make critical workflows depend on icon metadata, and
expect visual settings to need maintenance after theme or Obsidian changes.
Avoid assigning hundreds of one-off icons that make the vault harder to scan.

**Docs:** [Iconize documentation](https://florianwoelki.github.io/obsidian-iconize/), [files and folders](https://florianwoelki.github.io/obsidian-iconize/files-and-folders/), [community listing](https://community.obsidian.md/plugins/obsidian-icon-folder).

### 7. Importer (`obsidian-importer`)

**Use it when:** migrating notes or data from Airtable, Notion, Evernote,
Apple Notes/Journal, OneNote, Google Keep, Bear, Roam, Logseq, Tomboy,
Textbundle, CSV, or HTML into Obsidian.

**Workflow:**

1. Make a backup or Git commit and create a temporary staging folder for the
   import. Do not merge directly into the main knowledge structure.
2. Open **Settings → Community plugins → Importer**, choose the source format,
   and follow its export/import instructions.
3. Use an Importer template when titles, properties, or content need a
   repeatable transformation. Test the template on a small sample first.
4. Inspect filenames, YAML, links, attachments, dates, and duplicate notes.
   Fix mapping issues in the source/template and repeat rather than manually
   patching thousands of files.
5. Move the reviewed result into its final folders, then commit the migration
   separately so it can be reverted as one unit.

**Important:** Import is a migration workflow, not a live sync. Preserve the
original export until the imported notes and attachments have been checked.
Treat imported HTML/CSV fields as untrusted text and validate generated YAML.

**Docs:** [official Importer help](https://obsidian.md/help/plugins/importer), [Import notes](https://obsidian.md/help/import), [Importer source](https://github.com/obsidianmd/obsidian-importer).

### 8. Kanban (`obsidian-kanban`)

**Use it when:** a project, study plan, or workflow is naturally represented
as cards moving through columns.

**Workflow:**

1. Create a new board from the ribbon or command palette and save it in a
   deliberate project folder.
2. Define a small set of columns that represent real workflow states, such as
   `Backlog`, `Next`, `Doing`, `Waiting`, and `Done`.
3. Use short card titles; put detailed content in linked notes and use
   `[[wikilinks]]` from cards to those notes.
4. Drag cards to change state, edit cards as Markdown, and archive completed
   cards according to the board's configured workflow.
5. If a board also contains actionable tasks, decide whether the board or the
   Tasks plugin is the source of truth. Do not maintain two independent due
   dates or statuses without a documented sync workflow.

**Important:** Kanban boards are Markdown-backed, so edits affect a vault file.
Keep board syntax intact and commit before bulk rearranging cards. The original
plugin documentation is hosted through the community/archive listing; verify
compatibility before depending on an unmaintained board feature.

**Docs:** [community listing](https://community.obsidian.md/plugins/obsidian-kanban), [source repository](https://github.com/mgmeyers/obsidian-kanban).

### 9. Omnisearch (`omnisearch`)

**Use it when:** the normal file switcher or search is too narrow and you need
fast ranked results across note text, filenames, headings, PDFs, office files,
or images.

**Workflow:**

1. Open Omnisearch from its command, ribbon, or configured hotkey and search
   with the most distinctive terms first.
2. Use quoted phrases for exact expressions, `-term` for exclusions, and file
   extensions such as `.md` or `.pdf` to narrow results.
3. Switch between vault search and in-file search when skimming a long note.
   Insert a `[[wikilink]]` directly from a result when that is the intended
   action.
4. Treat the result as navigation assistance; open and verify the source note
   before quoting or changing it.

**Important:** PDF, office-document, and image indexing may require the
Text Extractor add-on, which is not among this vault's enabled plugins. The
optional local HTTP server should remain disabled unless an external tool
explicitly needs it.

**Docs:** [Omnisearch README](https://github.com/scambier/obsidian-omnisearch), [Omnisearch documentation](https://publish.obsidian.md/omnisearch/Index).

### 10. Outliner (`obsidian-outliner`)

**Use it when:** writing hierarchical notes, meeting outlines, study plans, or
nested action lists where moving whole subtrees should preserve indentation.

**Workflow:**

1. Keep one logical item per list bullet and nest supporting details below it.
2. Use `Tab`/`Shift+Tab` to indent or outdent a list and
   `Ctrl/Cmd+Shift+Up/Down` to move a list item with its children.
3. Use fold/unfold commands to navigate long outlines. Use enhanced Enter and
   selection behavior only after testing it with the current note format.
4. Keep semantic state in Markdown text, tags, properties, or Tasks syntax;
   Outliner changes structure but is not a project database.

**Important:** list styling and vertical indentation lines are documented as
most compatible with Obsidian's built-in theme. This vault uses a Minimal
theme, so disable those visual options if they conflict with the theme.
Check nested list structure after drag-and-drop or bulk moves.

**Docs:** [Outliner README and hotkeys](https://github.com/vslinko/obsidian-outliner), [community listing](https://community.obsidian.md/plugins/obsidian-outliner).

### 11. QuickAdd (`quickadd`)

**Use it when:** a repeated capture, note creation, multi-step command, or
script should become one command or hotkey.

**Choose the correct choice type:**

| Goal | QuickAdd choice |
| --- | --- |
| Create a new note from a reusable file | Template |
| Append text to a journal, log, task list, or existing note | Capture |
| Chain commands, scripts, or other choices | Macro |
| Group choices into a menu | Multi |

**Workflow:**

1. Create a named choice in **Settings → QuickAdd** and test it from **QuickAdd:
   Run** in the command palette.
2. For captures, set an explicit destination and format. For example,
   `Journal/{{DATE}}.md` with `- {{DATE:HH:mm}} {{VALUE}}` appends a timestamped
   line to the day's journal.
3. Add a hotkey only after the choice works. Use a Macro when it must call
   Templater, Dataview, Tasks, Obsidian commands, or a user script.
4. Store user scripts in the configured script folder, keep them small, and
   test them on a disposable note before allowing writes across the vault.
5. Use Obsidian URI or the QuickAdd CLI only for deliberate external
   automation; verify the target vault and choice name first.

**Important:** QuickAdd placeholders such as `{{DATE}}` and `{{VALUE}}` are
not the same syntax as Templater's `<% ... %>` commands. A script can read and
write vault content and call other plugins, so review it like code. Do not run
untrusted scripts or packages.

**Docs:** [QuickAdd getting started](https://quickadd.obsidian.guide/docs/), [choices](https://quickadd.obsidian.guide/docs/Choices/), [user scripts](https://quickadd.obsidian.guide/docs/UserScripts/), [CLI](https://quickadd.obsidian.guide/docs/Advanced/CLI/).

### 12. Recent Files (`recent-files-obsidian`)

**Use it when:** returning to notes opened recently, navigating a current
working set, or dragging a recent note into an editor/folder to create a link
or move it.

**Workflow:**

1. Open the Recent Files sidebar view and click a file to reopen it; use
   `Ctrl/Cmd`-click for a new pane.
2. Configure exclusions for noisy folders, frontmatter tags, or bookmarks so
   the list represents the actual working set.
3. Use hover previews and drag-and-drop for navigation, linking, or moving;
   verify the destination when moving a file.

**Important:** Recent Files is a navigation aid and does not create a second
   index or change note content by itself. Do not infer importance, status, or
   chronology solely from the order of the list.

**Docs:** [community listing and usage](https://community.obsidian.md/plugins/recent-files-obsidian).

### 13. Smart Connections (`smart-connections`)

**Use it when:** looking for semantically related notes, rediscovering
background context, or finding connections that exact-text search misses.

**Workflow:**

1. Enable the plugin and let its local embedding model index the vault. No API
   key or external model is needed for the core workflow.
2. Open the Connections view from the current note and inspect the ranked
   related notes. Use Lookup for a deliberate semantic search.
3. Open the source notes and verify the context before using a suggested link
   or claiming a relationship. Add links manually when the connection is
   meaningful.
4. Keep semantic metadata and exclusions intentional. If using a third-party
   sync tool, ignore `.smart-env/` to prevent index conflicts; do not blindly
   delete the directory while indexing is active.

**Important:** Connections are similarity suggestions, not citations or
 factual answers. Core features are local-first; inline connections, some
 ranking controls, and Bases integrations may require the Pro tier. Smart Chat
 is a separate plugin in the current ecosystem, not part of this core plugin.

**Docs:** [Smart Connections documentation](https://smartconnections.app/docs/connections/), [official README/community listing](https://community.obsidian.md/plugins/smart-connections).

### 14. Tasks (`obsidian-tasks-plugin`)

**Use it when:** tasks need due/scheduled/start dates, recurrence, priorities,
completion dates, filtering, grouping, or cross-note dashboards.

**Workflow:**

1. Keep actionable items as standard Markdown tasks, for example:

   ```markdown
   - [ ] Review the lecture notes 📅 2026-09-25 ⏫
   ```

2. Add a Tasks query block where a dashboard is useful. Start narrow and add
   filters gradually:

   ````markdown
   ```tasks
   not done
   due before tomorrow
   sort by due
   limit 50
   ```
   ````

3. Use filters such as `path includes`, `tags include`, `due`, `scheduled`,
   `done`, `group by`, and `sort by` according to the documented query syntax.
4. Toggle a task from a Tasks view only when updating the source Markdown task
   is intended. Keep one canonical task line rather than duplicating the task
   in multiple notes.
5. Use `limit` on broad queries. Large, unbounded task queries can slow Obsidian
   significantly.

**Important:** Tasks edits source files when a task is toggled or changed from
   a query. Validate dates and recurrence syntax after editing. Coordinate with
   Kanban and Dataview so each task has one source of truth and status is not
   maintained independently in three systems.

**Docs:** [Tasks user guide](https://publish.obsidian.md/tasks/), [query examples](https://publish.obsidian.md/tasks/Queries/Examples), [quick reference](https://github.com/obsidian-tasks-group/obsidian-tasks/blob/main/docs/Quick%20Reference.md).

### 15. Templater (`templater-obsidian`)

**Use it when:** a note needs reusable structure plus dynamic dates, titles,
frontmatter, file operations, prompts, or controlled JavaScript automation.

**Workflow:**

1. Create a dedicated template folder and set it in **Settings → Templater**.
   Keep templates distinguishable from ordinary notes.
2. Start with dynamic variables and internal functions, for example:

   ```markdown
   ---
   created: <% tp.file.creation_date("YYYY-MM-DD HH:mm") %>
   ---
   # <% tp.file.title %>
   ```

3. Insert or trigger the template from a new note. Use folder templates or
   QuickAdd Template choices for repeatable note creation.
4. Add user scripts only when built-in `tp.*` functions are insufficient. Keep
   scripts versioned, document inputs/outputs, and test with a copy of a note.
5. After execution, inspect generated YAML and wikilinks. A template should
   leave the note in a valid state even if a prompt is cancelled or a value is
   missing.

**Important:** Templater's `<% ... %>` syntax is different from QuickAdd's
`{{...}}` placeholders. JavaScript and web requests can modify the vault or
send data externally; do not execute untrusted templates. Preserve generated
values as ordinary Markdown after execution unless the template is explicitly
intended to be re-run.

**Docs:** [Templater introduction](https://silentvoid13.github.io/Templater/introduction.html), [syntax](https://silentvoid13.github.io/Templater/commands/), [internal functions](https://silentvoid13.github.io/Templater/internal-functions/), [GitHub repository](https://github.com/SilentVoid13/Templater).

## How agents should combine the plugins

Use the smallest reliable chain for the task:

1. **Capture:** QuickAdd → Templater for dynamic note creation → Tasks for
   actionable items.
2. **Review:** Tasks for task state → Dataview for a structured dashboard →
   Outliner for editing the source list.
3. **Research:** Omnisearch for exact text and files → Smart Connections for
   semantic discovery → open and verify the source notes before writing.
4. **Projects:** Kanban for visual flow → linked Markdown notes for detail →
   Tasks for due dates and recurring work.
5. **Visual notes:** Excalidraw for the drawing → wikilinks to explanatory
   notes → PNG/SVG export when the result must work outside Obsidian.
6. **Safety:** Git before broad changes → make the smallest edit → inspect the
   diff → commit intentionally.

Avoid overlapping systems without a clear source of truth. In particular,
decide whether a status belongs to a Kanban column, a Tasks field, or a note
property before building dashboards around it.

## Codex plugin packages

These are Codex-level packages detected in the local plugin cache; they are
separate from the Obsidian community plugins above.

### Plugin Management (`0.1.0`)

Use it when the user asks to discover, suggest, inspect, configure, connect, or
remove a plugin, or when an external service would materially improve a task.
Prefer built-in capabilities and already connected integrations first. Search
with a concise provider/capability query, suggest only the smallest useful set,
verify a connection before use, inspect permissions only for a named plugin,
and change permissions or uninstall only after explicit user authorization.

### Default templates (`openai-templates`, `0.1.1`)

The local package contains 20 templates for documents, presentations, and
spreadsheets. Use it only when its template surface is available in the
current session and the user wants a polished Office-style artifact. Keep the
retained reference unchanged, clone/import it, preserve its layout and
formatting, use only supplied facts, render and verify the result, and do not
recreate or install a replacement if the capability is unavailable.

Available templates:

- Documents: Design Report, Experiment Analysis, Investment Committee Memo,
  Legal Memorandum, Minimal Letterhead, Strategy Memorandum, System Design.
- Presentations: Business Review, Market Trends Report, Operating Review,
  Project Kickoff, Simple Dark Mode, Simple Light Mode, Team Alignment.
- Spreadsheets: Analytics Dashboard, Financial Budget, Operating Calendar,
  Project Tracker, Sales Pipeline, Three-Statement Forecast.

The package is present locally, but its last runtime permission check reported
`not installed`; do not claim that its app is connected based only on cached
files.

## Updating this README

When the vault changes, compare `.obsidian/community-plugins.json` with the
plugin directories and manifests. Update the inventory, versions, workflows,
and documentation links after checking the relevant official docs. Keep the
distinction between an enabled local plugin, a connected external service, and
a cached-but-unavailable package.
