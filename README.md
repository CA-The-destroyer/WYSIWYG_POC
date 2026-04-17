# Local WYSIWYG

A local-first desktop writing app built with Tauri 2, React, TypeScript, Vite, Tiptap, Tailwind CSS, and a Rust backend for native filesystem and desktop integration.

## Stack

- Tauri 2
- React 19
- TypeScript
- Vite
- Tiptap
- Tailwind CSS
- Rust

## Features

### Editor

- Bold, italic, underline, strikethrough
- Headings, bullet lists, ordered lists
- Blockquotes and code blocks
- Links, images, and tables
- Undo/redo and clear formatting
- Placeholder text
- Read-only mode
- Top toolbar and bubble menu
- Optional syntax highlighting for code blocks

### Content APIs

The editor surface exposes methods equivalent to:

- `getText()`
- `getHTML()`
- `getContent()`
- `loadContent(json)`
- `loadHTMLContent(html)`
- `insertImage(url)`

### Documents

- New document
- Open document
- Save and Save As
- Autosave
- Recent documents
- Dirty state indicator
- Crash recovery snapshots

### Desktop UX

- Light and dark mode
- Sidebar for recent documents and recovery snapshots
- Tabs for open documents
- Keyboard shortcuts
- Command palette
- Toast notifications
- Settings dialog

### Import / Export

- Import from Markdown
- Export to HTML
- Export to Markdown
- Export to PDF

## Project Structure

```text
.
├── README.md
├── docs
│   ├── architecture.md
│   ├── bom.md
│   └── security-review.md
├── src
│   └── frontend
│       ├── components
│       ├── features
│       │   ├── documents
│       │   ├── editor
│       │   └── settings
│       ├── hooks
│       ├── lib
│       ├── styles
│       └── types
├── src-tauri
│   ├── capabilities
│   ├── icons
│   ├── src
│   │   ├── commands
│   │   ├── errors
│   │   ├── models
│   │   └── services
│   ├── Cargo.toml
│   └── tauri.conf.json
└── tests
```

## Setup

### Prerequisites

- Node.js 22+
- pnpm
- Rust toolchain with `cargo`
- Windows WebView2 runtime on Windows

### Install

```powershell
pnpm install
```

### Run the frontend only

```powershell
pnpm dev
```

### Run the Tauri desktop app

If Cargo is not already on your `PATH`, prepend it for the shell session:

```powershell
$env:PATH = 'C:\Users\<you>\.cargo\bin;' + $env:PATH
pnpm tauri dev
```

### Build the desktop app

```powershell
$env:PATH = 'C:\Users\<you>\.cargo\bin;' + $env:PATH
pnpm tauri build --debug
```

The debug executable is emitted at:

```text
src-tauri/target/debug/wysiwyg_editor.exe
```

## Validation Commands

```powershell
pnpm build
pnpm audit --prod
pnpm list --depth 0
& 'C:\Users\<you>\.cargo\bin\cargo.exe' check
& 'C:\Users\<you>\.cargo\bin\cargo.exe' tree -d
```

## Notes

- Document files are stored as local JSON files with a versioned schema.
- `settings.json`, `recents.json`, and recovery snapshots live in the local app data directory.
- File dialogs, save flows, recovery, and exports are handled in Rust.
- Editor behavior remains in React and Tiptap.
