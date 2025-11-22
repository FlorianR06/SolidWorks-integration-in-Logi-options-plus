# SolidWorks integration in Logi Options+

Goal: Make Logitech MX Master 4 give a small haptic pulse when the mouse hovers
(over preselection) on a line/edge in SolidWorks.

## Architecture

This repo contains two C# projects:

1. **SolidWorksHoverAddin**
   - A SolidWorks C# add-in.
   - Listens for preselection / hover events via the SolidWorks API.
   - When the hovered entity is an edge/line, it sends a small message to
     a local endpoint on `localhost`.

2. **LogiHoverHapticsPlugin**
   - A Logitech Actions SDK plugin for Logi Options+.
   - Listens on `localhost` for hover messages from the SolidWorks add-in.
   - When a hover message arrives, triggers a short haptic effect on an
     MX Master 4 mouse.

## Rough data flow

SolidWorks (C# add-in) → hover detected → HTTP/UDP ping to localhost →  
Logi plugin receives ping → calls Haptics API → mouse vibrates.

## Status

- [ ] SolidWorks add-in skeleton
- [ ] Preselection (hover) detection
- [ ] Local IPC between add-in and plugin
- [ ] Logi plugin skeleton
- [ ] Haptic trigger on incoming hover event
