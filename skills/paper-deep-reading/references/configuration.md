# Local Private Profile

Keep personalized paths, routing rules, project names, research sources, and domain-specific checklists outside the public Skill repository.

The Skill reads the following local file after resolving the current user's home directory through the operating system:

`<USER_HOME>/.codex/paper-deep-reading.local.md`

Copy [profile.example.md](profile.example.md) to that location and edit the copy. It is model-readable Markdown, not a parsed configuration format. Replace every required placeholder before use. Keep the installed skill folder and the private profile separate.

The profile should define:

- the absolute output root;
- journal-to-directory mappings and a fallback directory;
- the final filename pattern;
- research-context sources and whether each source is read-only;
- any domain-specific section headings, material fields, methods, result order, and evaluation criteria;
- which sections may be appended when a same-name note exists and the exact append heading format.

An empty research-context source list is valid. In that case the paper can still be read, but its relationship to the user's research must be marked as insufficiently contextualized. Empty journal mappings are valid when an explicit fallback directory is configured.

Do not place the real profile, sample research data, private local paths, private account identifiers, or exported library records in the public repository. Public examples use placeholders. If the profile is missing or contains unresolved required placeholders, the skill must ask for configuration rather than guess.

