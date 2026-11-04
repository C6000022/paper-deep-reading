# Private local profile for Paper Deep Reading

Copy this file to `<USER_HOME>/.codex/paper-deep-reading.local.md` and edit the
copy. This is a model-readable Markdown profile, not executable configuration.
Do not commit the completed copy to the public repository.

## Output location and routing

- Absolute output root: `<ABSOLUTE_OUTPUT_ROOT>`
- Journal-to-directory mappings: none initially. Add exact journal names and
  their destination subdirectory names here if needed.
- Fallback directory: `Others`, relative to the output root. Use it when the
  journal is unspecified or has no configured mapping.
- Keep all destination directories inside the configured output root. Use
  journal subdirectories only after resolving the selected destination.
- The configured output root is authorized for note storage. If it is absent,
  create it after checking that the configured value is an absolute path and
  no placeholder remains. Create the selected journal or fallback subdirectory
  there as needed. A file occupying a required directory path is an error.

Replace the output-root placeholder with a real absolute path before use.
Treat placeholders or ambiguous routing rules as incomplete configuration.

## Filename and language

- Filename pattern: `{year} - {title}.md`.
- Use the paper's formal title from the PDF for `{title}`.
- Use the publication year verified in the PDF for `{year}`; if it cannot be
  verified, use `undated` and mark the year as unspecified in the note.
- Follow the skill's filename-character replacement rules. Do not shorten
  titles to fit a path limit.
- Note language: Simplified Chinese. Preserve necessary original technical
  terms, paper titles, symbols, and units.
- Write UTF-8 Markdown without YAML frontmatter, tags, or wiki links.

## Research-context sources

- Sources: none initially.
- If adding sources, specify their local paths or supported access routes and
  what research question each source informs. Treat every source as read-only.
- When no source is configured or accessible, complete the paper analysis and
  state that the relationship to the user's research cannot be fully assessed.
- Do not infer a research project or fabricate background to fill this gap.

## New-note structure

Use all 11 sections in `references/note-template.md`. No additional
domain-specific checklist is configured. Cite important evidence by physical
PDF page number and figure or table identifier where available.

## Existing-note supplements

- Preserve every original byte of an existing same-name note.
- Append only sections 9 (Limitations and potential problems), 10 (Relationship
  to the user's research), and 11 (Final assessment).
- Prefix the addition with a blank line, `---`, a blank line, and the heading
  `## Supplement — YYYY-MM-DD`, using the user's current local date.
- Put the three supplemental sections under that heading as level-3 headings.
- Do not regenerate or replace original sections. Verify that the original
  byte sequence is an exact prefix of the file after appending.
