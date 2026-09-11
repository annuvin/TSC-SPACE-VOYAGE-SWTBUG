## TSC Space Voyage: 6809-to-6800 SWTBUG Port

This project reverse-engineers and adapts the TSC *Space Voyage* game for a real SWTPC 6800 running the SWTBUG ROM monitor.

The publicly available material included a precompiled 6800 S-record and a later 6809-oriented assembly listing, but no editable 6800 source. The 6809 listing was converted into maintainable Motorola 6800 assembly and tested on real hardware.

Key work completed:

- Replaced 6809-only instructions and addressing modes with 6800-compatible sequences, including `LDD/STD`, `TFR`, `LEAX`, condition-code operations, stack auto-indexing, and accumulator-indexed addressing.
- Retargeted monitor I/O to SWTBUG’s documented routines for character input, character output, strings, hexadecimal output, and return to the monitor.
- Corrected SWTBUG string handling: `PDATA1` requires `$04` end-of-text markers, including the internal CR/LF string.
- Prevented double keyboard echo by disabling SWTBUG’s automatic echo while the game runs; the game retains its own intentional input echo.
- Added a startup seed based on the timing of the initial `S`/`L` response, so each game begins with a different galaxy rather than a fixed deterministic state.
- Found and fixed a porting bug in indexed addressing where `1,X` was accidentally translated as `10,X`. This corrected movement vectors, false “Galaxy limit” messages, and corrupted quadrant coordinates.
- Built a SWTBUG-loadable Motorola S-record image and verified its assembly output and record checksums.

The result is an editable 6800/SWTBUG source base suitable for modifying game mechanics while preserving the original game’s console-oriented behavior.
