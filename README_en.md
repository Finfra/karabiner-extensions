---
name: Extensions_en
description: English entry point for the published Karabiner-Elements complex_modifications rules
date: 2026.08.09
---
[![ko](https://img.shields.io/badge/lang-ko-red.svg)](README.md)

> 📦 **This repository is generated.** The source of truth lives in a private working
> repository; what you see here is a public copy produced by `tools/build_public.py`.
> Backticked paths in the text (e.g. `data/rule_source.yaml`) point into that private
> repository and do **not** exist here — only linked paths resolve within this tree.

# Karabiner-Elements Extensions

Five [Karabiner-Elements](https://karabiner-elements.pqrs.org/) `complex_modifications` rules, each in its own folder with the deployable JSON and a document explaining what it does and why it is built that way.

Two of them are ordinary key remaps you can drop in and use. The other three depend on specific hardware or on an external app, and say so plainly — a rule that silently does nothing is worse than one that tells you what it needs.

# Rules

| Rule | What it does | Needs |
| :--- | :--- | :--- |
| [FootPedal](footPedal/README.md) | USB 3-pedal foot switch — editing / navigation / media layers, six modifier tiers | A 3-pedal USB foot switch |
| [12Key2Knob](12Key2Knob/README.md) | 12-key + 2-knob macropad → Keyboard Maestro macro triggers | The macropad **and** 62 macros you create yourself (see below) |
| [RemoteDesktop](remoteDesktop/README.md) | Swaps `alt` ↔ `command` while Microsoft Remote Desktop is frontmost | Nothing — pure key remap |
| [NowageShorthand (n3sh)](n3sh/README.md) | Korean shorthand for the 3-set 390 layout — jamo chords expand into whole words and phrases | A Korean IME and the 3-set 390 layout |
| [EngCharOnKor](engCharOnKor/README.md) | Type English while holding `Insert`, without leaving the Korean input source | A key that emits `insert`; Korean IME |

## Where the deployable file is

Each folder holds `rule.json`, which is what goes into `~/.config/karabiner/karabiner.json`. Four of them are the rule itself; **n3sh is generated** — its JSON is built from the tables under `n3sh/layout/` by a tool that lives in the private working repository.

# What is and is not here

| Included | Not included |
| :--- | :--- |
| `rule.json` — the deployable rule | The build tools (`tools/`) that generate n3sh |
| `info.md` — description and provenance | Keyboard Maestro macros for 12Key2Knob |
| `README.md` — per-rule entry point | Live config backups and oracle snapshots |
| n3sh source tables (`layout/`), generated data (`core/`), notes (`_doc/`) | Anything holding personal paths |

⚠️ **12Key2Knob will not work out of the box.** Its manipulators do nothing but pass macro *names* to Keyboard Maestro over `shell_command`; the macros themselves are tied to one person's workflow and are not published. You would have to create 62 macros with matching names — [its README](12Key2Knob/README.md) lists them and warns about the traps (a misspelled name fails silently, and the knob macros use *three* underscores).

# Installing a rule

1. Open **Karabiner-Elements → Complex Modifications → Add rule**
2. Or copy the rule into `~/.config/karabiner/assets/complex_modifications/` and enable it in the UI
3. Restart Karabiner-Elements if a rule does not appear

Check the **Needs** column above first. A device-specific rule matches on `vendor_id`/`product_id`, so it stays dormant until that exact device is connected — which looks identical to the rule being broken.

# Published elsewhere

| Rule | pqrs.org registry |
| :--- | :--- |
| FootPedal | ✅ [Registered](https://ke-complex-modifications.pqrs.org/?q=foot%20pedal) — *USB Foot Pedal (3 pedals)*, PR [#1982](https://github.com/pqrs-org/KE-complex_modifications/pull/1982) |
| EngCharOnKor | 🚧 Submission prepared, PR pending |
| 12Key2Knob | ⏸️ Postponed — without the macros it cannot work on someone else's machine |
| RemoteDesktop | ⏸️ Postponed — `alt`↔`command` swaps are already well covered there |
| n3sh | ❌ Not a target — the registry takes one rule at a time, and this one is a generated set |

The registry ([ke-complex-modifications.pqrs.org](https://ke-complex-modifications.pqrs.org/)) accepts **one rule per entry**, which is why this repository exists: it is the place where all five can be seen together.

# Layout

```
.
├── README.md · README_en.md   # this index
└── {rule}/
    ├── README.md              # entry point: overview, file map, status
    ├── info.md                # description and provenance
    ├── rule.json              # the deployable rule
    └── layout/ core/ _doc/    # rule-specific assets (n3sh only)
```

Folder names match the rule code names. `12Key2Knob` starts with a digit because that is the device's name — it is not a sort prefix.

# License and provenance

These rules are published as-is, as a reference for anyone building similar ones. The Korean index ([README.md](README.md)) carries the fuller history — folder conventions, path migrations, and the reasoning behind each design decision — and is the more complete document of the two.

If a rule here is useful to you, the per-rule `README.md` is the place to start: it states what the rule assumes about your environment, which is usually the part that decides whether it will work for you.
