# 🥬 spinach

> Practical spinner for Rust 

<p align="center">
	<img src="assets/screenshot.png" width="399px">
</p>

## Install

Add as a dependency to your `Cargo.toml`.

```toml
[dependencies]
spinach = "1.0"
```

## Usage

Basic example.

```rust
use std::thread::sleep;
use std::time::Duration;

use spinach::Spinach;

fn main() {
    let s = Spinach::new("Running task 1");
    sleep(Duration::from_secs(1));
    s.text("Running task 2");
    sleep(Duration::from_secs(1));
    s.succeed(Some("Ran tasks successfully"));
}
```

### Creating

```rust
use spinach::{Color, Spinach, Spinner};

// Using defaults + custom text
let s = Spinach::new("custom text");

// Using custom spinner
let spinner = Spinner::new(vec!["▮","▯"], 80);
let s = Spinach::new_with(Some(spinner), Some("custom text"), Some(Color::Red));

// Also with partial config (fallback to defaults)
let s = Spinach::new_with(None, Some("custom text"), Some(Color::Green));
```

### Updating

```rust
use spinach::{Color, Spinach};

let s = Spinach::new("custom text");

// Updating text
s.text("new text");

// Updating color
s.color(Color::White);

// Updating multiple
s.update_with(Some("new text"), Some(Color::Red));

// Also with partial update (keep current)
s.update_with(None, Some(Color::Red));
```

### Stopping

```rust
use spinach::{Color, Spinach};

let s = Spinach::new("custom text");

// Stop with final `✔` frame, green color and optional text change.
s.success(Some("gg"));

// Stop with final `✖` frame, red color and optional text change.
s.fail(Some(":("));

// Stop with final `⚠` frame, yellow color and optional text change.
s.warn(None);

// Stop with final `ℹ` frame, blue color and optional text change.
s.info("notice");

// Stop current spinner (freeze the frame)
s.stop();

// Stopping with custom final frame, text and color
s.stop_with(Some("🥬"), Some("spinach'd"), Some(Color::Ignore));

// Also with partial update (keep current)
s.stop_with(None, None, Some(Color::Blue));
```
