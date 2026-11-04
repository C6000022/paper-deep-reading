# Local Private Profile

Keep personalized paths, routing rules, project names, research sources, and domain-specific checklists outside the public Skill repository.

The Skill reads the following local file after resolving the current user's home directory through the operating system:

`<USER_HOME>/.codex/paper-deep-reading.local.md`

## First use through conversation

If the profile is missing, use an absolute note output root already specified by the user. Otherwise resolve the current user's Documents directory through the operating system, propose its `PaperNotes` child as the root, and state the exact final default note directory ending in `PaperNotes/General`. Ask once for an optional alternative, preferably without blocking read-only paper analysis. After giving the user a reasonable opportunity to reply, use the announced default if no alternative is supplied before saving. If the question tool returns no answer, use that same default. Do not infer the root from the paper location or a fixed example drive. If Documents cannot be resolved reliably, ask for a usable root rather than guessing.

Create the profile from [profile.example.md](profile.example.md), replacing `<ABSOLUTE_OUTPUT_ROOT>` and recording whether the selected root was supplied by the user or came from the announced default. Use `General` as the fallback subdirectory, leave journal mappings and research-context sources empty, and keep the template's note language, filename pattern, and supplement rules unless the user requests changes.

Resolve the current user's home directory through the operating system, create the profile's parent directory when needed, and write the profile as UTF-8. Verify the saved values before continuing. Do not overwrite a profile created in the meantime. If the profile cannot be saved, explain the actual error rather than reporting successful setup.

Reuse an existing valid profile. For incomplete profiles or requested changes, update only the necessary values while preserving unrelated preferences. Treat the paper path and the note output root as separate inputs; do not infer one from the other. The user need not manually copy or edit a file for the ordinary first-use flow.

## Optional manual setup

Advanced users can copy [profile.example.md](profile.example.md) to the private profile location and edit the copy. It is model-readable Markdown, not a parsed configuration format. Replace every required placeholder before use. Keep the installed skill folder and the private profile separate.

## Profile contents

The profile should define:

- the absolute output root;
- journal-to-directory mappings and a fallback directory;
- the final filename pattern;
- research-context sources and whether each source is read-only;
- any domain-specific section headings, material fields, methods, result order, and evaluation criteria;
- which sections may be appended when a same-name note exists and the exact append heading format.

An empty research-context source list is valid. In that case the paper can still be read, but its relationship to the user's research must be marked as insufficiently contextualized. Empty journal mappings are valid when an explicit fallback directory is configured.

Do not place the real profile, sample research data, private local paths, private account identifiers, or exported library records in the public repository. Public examples use placeholders. If the profile is missing or contains unresolved required placeholders, the skill must ask for configuration rather than guess.

