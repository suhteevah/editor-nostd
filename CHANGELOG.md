# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2026-04-02

### Added

- Initial release extracted from [ClaudioOS](https://github.com/suhteevah/claudio-os)
- `Editor` struct with in-memory line buffer (`Vec<Vec<char>>`)
- `EditorAction` enum: `Continue`, `Save(String)`, `Quit`
- Character insertion, deletion (backspace + delete), line splitting (enter)
- Arrow key navigation, Home, End, Page Up, Page Down
- Ctrl+S save, Ctrl+Q quit, Ctrl+X cut line
- Tab inserts 4 spaces
- Line-number gutter with ANSI coloring
- Status bar with filename, modified indicator, cursor position
- Help bar with keyboard shortcut hints
- Vertical scrolling for files larger than the viewport
- Full ANSI escape sequence rendering via `render()`
- `load()` and `content()` for file I/O integration
- `resize()` for dynamic terminal size changes
- 12 unit tests covering all core operations
