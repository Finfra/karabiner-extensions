---
name: README_en
description: "Karabiner-Elements complex_modifications rules — English entry point"
date: 2026.08.09
---
[![ko](https://img.shields.io/badge/lang-ko-red.svg)](README.md)

> 📦 **This repository is generated.** The source of truth lives in a private working
> repository; what you see here is a public copy produced by `tools/build_public.py`.
> Backticked paths in the text (e.g. `data/rule_source.yaml`) point into that private
> repository and do **not** exist here — only linked paths resolve within this tree.

# Karabiner-Elements Extensions

Five `complex_modifications` rules for [Karabiner-Elements](https://karabiner-elements.pqrs.org/), the macOS keyboard customizer. Each rule gets its own folder holding a **ready-to-install JSON** (`rule.json`) and a document explaining what it does.

These grew out of one person's setup over more than a decade, so they are uneven by design. Two are plain key remaps you can drop in. The other three assume specific hardware or an external app — **the table says which is which**, because a rule whose conditions aren't met does nothing at all, and that is indistinguishable from a broken install.

# The five rules

| Rule | What it does | Requires |
| :--- | :--- | :--- |
| [RemoteDesktop](remoteDesktop/README.md) | Swaps `alt` ↔ `command`, but only while Microsoft Remote Desktop is frontmost | **Nothing** — a plain key remap |
| [EngCharOnKor](engCharOnKor/README.md) | Types English **while `Insert` is held**, without switching away from the Korean input source | A key that emits `insert` · a Korean IME |
| [FootPedal](footPedal/README.md) | USB 3-pedal foot switch — editing / navigation / media layers across six modifier tiers | A 3-pedal USB foot switch |
| [NowageShorthand (n3sh)](n3sh/README.md) | Korean shorthand for the 3-set 390 layout — jamo chords expand into whole words and phrases | A Korean IME · the 3-set 390 layout |
| [12Key2Knob](12Key2Knob/README.md) | Turns a 12-key + 2-knob macropad into Keyboard Maestro triggers | That macropad **plus 62 macros you write yourself** ⚠️ |

## Where to start

**[RemoteDesktop](remoteDesktop/README.md)** is the shortest and has no prerequisites — a good look at how a Karabiner rule is put together.

**[EngCharOnKor](engCharOnKor/README.md)** is the one most likely to be useful if you type Korean. It covers the common case of typing a few English characters mid-sentence, and because it never switches the input source, **it does not care what your language-switch shortcut is**.

# Installing

1. Karabiner-Elements → **Complex Modifications → Add rule**
2. Or drop `rule.json` into `~/.config/karabiner/assets/complex_modifications/` and enable it in the UI
3. Restart Karabiner-Elements if the rule doesn't show up

⚠️ **Device-specific rules stay dormant until that device is attached.** They match on `vendor_id`/`product_id`, so with the hardware absent an enabled rule simply does nothing — which looks exactly like a failed install.

# What's here and what isn't

| Included | Not included |
| :--- | :--- |
| `rule.json` — the rule you actually install | The build tools that generate n3sh |
| `info.md` — description and provenance | Keyboard Maestro macros for 12Key2Knob |
| `README.md` — per-rule entry point | Live config backups and comparison snapshots |
| n3sh's rule tables (`layout/`), generated data (`core/`), notes (`_doc/`) | Anything carrying personal paths |

⚠️ **12Key2Knob will not work as shipped.** Its manipulators do nothing but hand macro *names* to Keyboard Maestro, and the macros themselves are too tied to one person's workflow to publish. Using it means writing 62 macros with matching names — [its README](12Key2Knob/README.md) lists them and flags the traps.

# Registered on pqrs.org

The official registry, [ke-complex-modifications.pqrs.org](https://ke-complex-modifications.pqrs.org/), takes **one rule per entry**. There was nowhere to show all five together, which is why this repository exists.

| Rule | Status |
| :--- | :--- |
| FootPedal | ✅ Registered — *USB Foot Pedal (3 pedals)*, PR [#1982](https://github.com/pqrs-org/KE-complex_modifications/pull/1982) |
| EngCharOnKor | 🚧 Submission ready, PR pending |
| 12Key2Knob | ⏸️ Postponed — without the macros it cannot work on another machine |
| RemoteDesktop | ⏸️ Postponed — `alt`↔`command` swaps are already well covered there |
| n3sh | ❌ Not applicable — a generated rule set doesn't fit the one-per-entry model |

# Layout

```
.
├── README.md · README_en.md   # this document
└── {rule}/
    ├── README.md              # rule entry point — overview, file map, status
    ├── info.md                # description and provenance
    ├── rule.json              # the rule you install
    └── layout/ core/ _doc/    # rule-specific assets (n3sh only)
```

Folder names are the rule code names. `12Key2Knob` starts with a digit because that is the device's name, not a sort prefix.

# About this repository

The source of truth is a private working repository; what you see here is a **generated copy**. Backticked paths in the text (e.g. `data/rule_source.yaml`) point into that private repository and are not present here — only linked paths resolve.

To judge whether a rule is worth installing, go to its folder `README.md` first. It states **what the rule assumes about your environment**, and that is usually what decides whether it will work for you.
