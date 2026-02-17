# ⚠️ Breaking Change: raw-window-handle 0.6 Migration
This version of baseview has been migrated from raw-window-handle 0.5 to 0.6. This is a significant breaking change that affects how window handles are requested and passed.

## What has changed?
New Traits: The deprecated HasRawWindowHandle and HasRawDisplayHandle have been replaced by the modern HasWindowHandle and HasDisplayHandle.

Type Safety: Handles are no longer returned as raw enums. They now return a Result<WindowHandle, HandleError>, providing better lifecycle safety and error handling.

Platform Specifics:

Windows: HWND is now handled as a NonZero<isize>.

macOS: NSView and NSWindow now use NonNull<c_void>.

Linux (X11): Display pointers now require NonNull wrappers and Window IDs are u64.

## Why this matters
This update ensures that baseview is fully compatible with the latest ecosystem releases of wgpu, vizia, glutin, and Slint. If you are upgrading from an older version of baseview, you will need to update your window creation and rendering setup to handle the new Result-based handle API.

# baseview

A low-level windowing system geared towards making audio plugin UIs.

`baseview` abstracts the platform-specific windowing APIs (winapi, cocoa, xcb) into a platform-independent API, but otherwise gets out of your way so you can write plugin UIs.

Interested in learning more about the project? Join us on [discord](https://discord.gg/b3hjnGw), channel `#plugin-gui`.

## Roadmap

Below is a proposed list of milestones (roughly in-order) and their status. Subject to change at any time.

| Feature                                               | Windows            | Mac OS             | Linux              |
| ----------------------------------------------------- | ------------------ | ------------------ | ------------------ |
| Spawns a window, no parent                            | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| Cross-platform API for window spawning                | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| Can find DPI scale factor                             |                    | :heavy_check_mark: | :heavy_check_mark: |
| Basic event handling (mouse, keyboard)                | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| Parent window support                                 | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| OpenGL context creation (behind the `opengl` feature) | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |

## Prerequisites

### Linux

Install dependencies, e.g.:

```sh
sudo apt-get install libx11-dev libxcb1-dev libx11-xcb-dev libgl1-mesa-dev
```

## License

Licensed under either of <a href="LICENSE-APACHE">Apache License, Version
2.0</a> or <a href="LICENSE-MIT">MIT license</a> at your option.

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in Baseview by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.
