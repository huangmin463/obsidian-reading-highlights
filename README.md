# 【标注】阅读高亮
Reading Highlights is an Obsidian plugin for non-destructive reading highlights and margin notes.

## What It Does

- Highlight selected Markdown text without changing the source note.
- Use yellow, red, or blue highlights from a floating selection toolbar.
- Attach notes to highlights.
- Open a right sidebar for highlight search, note editing, deletion, and jump-back navigation.
- Export highlights and notes into a new Markdown file.
- Keep all annotation data in the plugin's own `data.json` instead of writing highlight syntax into source Markdown files.

## Current Scope

The first implementation focuses on Markdown notes in Live Preview / editor mode. PDF annotation storage is represented in the data model, but visual PDF highlighting is not implemented because Obsidian's built-in PDF viewer does not expose the same stable text-position API as Markdown editor views.

## Plugin Isolation

Reading Highlights must not modify Obsidian's default settings. The plugin only writes its own plugin data at:

```text
<vault>/.obsidian/plugins/reading-highlights/data.json
```

It does not write to Obsidian core configuration files such as:

```text
<vault>/.obsidian/app.json
<vault>/.obsidian/appearance.json
<vault>/.obsidian/workspace.json
```

The plugin may read Obsidian's current language through the public `getLanguage()` API when its own language setting is set to `Auto`, but it must not change Obsidian's language or locale.

## Obsidian Language Troubleshooting

If Obsidian itself cannot switch interface languages after enabling this plugin:

- Confirm the language choice is saved in Obsidian's own settings.
- Inspect `.obsidian/app.json` for unexpected `language` or `locale` fields.
- Disable third-party plugins and restart Obsidian to check whether the issue still reproduces.
- Temporarily move `.obsidian/workspace.json` aside to test whether layout state is involved.
- Re-enable Reading Highlights only after confirming Obsidian's own language setting works independently.

## Development

```bash
npm install
npm run build
```

For local testing, copy or symlink `manifest.json`, `main.js`, and `styles.css` into:

```text
<vault>/.obsidian/plugins/reading-highlights/
```

Then enable `Reading Highlights` from Obsidian's Community plugins settings.
