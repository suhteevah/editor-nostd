# editor-nostd

[![Crates.io](https://img.shields.io/crates/v/editor-nostd.svg)](https://crates.io/crates/editor-nostd)
[![Documentation](https://docs.rs/editor-nostd/badge.svg)](https://docs.rs/editor-nostd)
[![License](https://img.shields.io/crates/l/editor-nostd.svg)](https://github.com/suhteevah/editor-nostd)

A minimal nano-like text editor for `#![no_std]` environments. Works on bare-metal, embedded systems, or anywhere you have an allocator but no standard library.

## Features

- **`#![no_std]` + `alloc`** -- no OS dependencies
- Insert, delete, backspace, enter (line splitting)
- Arrow key navigation, Home, End, Page Up, Page Down, Delete
- Ctrl+S save, Ctrl+Q quit, Ctrl+X cut line
- Tab inserts 4 spaces
- Line-number gutter
- Status bar with filename, modified indicator, and cursor position
- Vertical scrolling for large files
- Full ANSI escape sequence rendering
- 12 tests covering all core operations

## Usage

Add to your `Cargo.toml`:

```toml
[dependencies]
editor-nostd = "0.1"
pc-keyboard = "0.8"
```

```rust
use editor_nostd::{Editor, EditorAction};
use pc_keyboard::DecodedKey;

// Create an editor for an 80x24 terminal
let mut ed = Editor::new(80, 24);

// Load a file
ed.load("main.rs", "fn main() {\n    println!(\"hello\");\n}");

// Process keypresses in your event loop
let action = ed.handle_key(DecodedKey::Unicode('x'));
match action {
    EditorAction::Continue => {
        // Re-render the screen
        let ansi_output = ed.render();
        // Write ansi_output to your framebuffer / serial / terminal
    }
    EditorAction::Save(filename) => {
        let content = ed.content();
        // Persist content to your storage
    }
    EditorAction::Quit => {
        // Exit the editor
    }
}
```

## How It Works

The editor maintains an in-memory buffer of lines (`Vec<Vec<char>>`) and renders the visible portion as ANSI escape sequences. It does not perform any I/O itself -- the caller is responsible for:

1. Feeding keypresses via `handle_key()`
2. Writing the ANSI output from `render()` to a display
3. Persisting file contents when `EditorAction::Save` is returned

This design makes it suitable for bare-metal OS kernels, embedded displays, or any environment where you control the I/O layer.

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| Ctrl+S | Save (returns `EditorAction::Save`) |
| Ctrl+Q | Quit (returns `EditorAction::Quit`) |
| Ctrl+X | Cut current line |
| Tab | Insert 4 spaces |
| Arrow keys | Move cursor |
| Home / End | Move to start / end of line |
| Page Up / Down | Scroll by page |
| Delete | Delete character at cursor / join lines |
| Backspace | Delete character before cursor / join lines |

## License

Licensed under either of

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or <http://www.apache.org/licenses/LICENSE-2.0>)
- MIT License ([LICENSE-MIT](LICENSE-MIT) or <http://opensource.org/licenses/MIT>)

at your option.

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

## Support This Project

If you find this project useful, consider buying me a coffee! Your support helps me keep building and sharing open-source tools.

[![Donate via PayPal](https://img.shields.io/badge/Donate-PayPal-blue.svg?logo=paypal)](https://www.paypal.me/baal_hosting)

**PayPal:** [baal_hosting@live.com](https://paypal.me/baal_hosting)

Every donation, no matter how small, is greatly appreciated and motivates continued development. Thank you!
