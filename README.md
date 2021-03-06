# wgpu_glyph
[![Build Status](https://travis-ci.org/hecrj/wgpu_glyph.svg?branch=master)](https://travis-ci.org/hecrj/wgpu_glyph)
[![crates.io](https://img.shields.io/crates/v/wgpu_glyph.svg)](https://crates.io/crates/wgpu_glyph)
[![Documentation](https://docs.rs/wgpu_glyph/badge.svg)](https://docs.rs/wgpu_glyph)
[![License](https://img.shields.io/crates/l/wgpu_glyph.svg)](https://github.com/hecrj/wgpu_glyph/blob/master/LICENSE)

A fast text renderer for [wgpu](https://github.com/gfx-rs/wgpu), powered by
[glyph_brush](https://github.com/alexheretic/glyph-brush/tree/master/glyph-brush)

```rust
use wgpu_glyph::{Section, GlyphBrushBuilder};

let font: &[u8] = include_bytes!("SomeFont.ttf");
let mut glyph_brush = GlyphBrushBuilder::using_font_bytes(font)
    .build(&mut device, render_format);

let section = Section {
    text: "Hello wgpu_glyph",
    ..Section::default() // color, position, etc
};

glyph_brush.queue(section);
glyph_brush.queue(some_other_section);

glyph_brush.draw_queued(
    &mut device,
    &mut encoder,
    &frame.view,
    frame.width.round() as u32,
    frame.height.round() as u32,
);

device.get_queue().submit(&[encoder.finish()]);
```

## Examples

Have a look at
  * `cargo run --example hello --features wgpu/<backend>`
  * [Coffee](https://github.com/hecrj/coffee), which uses `wgpu_glyph` to
    provide font rendering on the [`wgpu` graphics backend].

[`wgpu` graphics backend]: https://github.com/hecrj/coffee/tree/master/src/graphics/backend_wgpu
