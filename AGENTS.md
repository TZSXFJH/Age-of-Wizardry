# AGENTS.md - Age of Wizardry (Victoria 3 Mod)

## Overview
Victoria 3 mod adding magical elements (pops, buildings, goods, techs). Uses Paradox Script (.txt), Localization (.yml), and GUI (.gui).

## Project Structure
```
Age of Wizardry/
├── common/              # Game definitions (Paradox script .txt)
│   ├── buildings/       # Building & PM definitions
│   ├── pop_types/       # Pop definitions (mages, archmages)
│   ├── technology/      # Tech tree (use _9981 suffix)
│   ├── scripted_triggers/ # Reusable logic
│   └── ...              # Other game systems
├── localization/        # Translations (UTF-8 BOM REQUIRED)
│   ├── english/         # AoW_<name>_l_english.yml
│   └── simp_chinese/    # AoW_<name>_l_simp_chinese.yml
├── gui/                 # UI definitions (.gui)
├── skills/              # Specialized agent guides (READ THESE)
└── gfx/                 # Graphics assets
```

## Validation & Testing
**No traditional build/test.** Mod is validated by the game engine at runtime.
1. **Launch**: Launch Victoria 3 with `-debug_mode` and the mod enabled.
2. **Logs**: Check `Documents/Paradox Interactive/Victoria 3/logs/error.log` for parse/scope errors.
3. **Console**: Use `^` in-game for console. Key commands: `event <id>`, `script_docs`, `DumpDataTypes`.
4. **Hotloading**: Most `.txt` files reload on change in debug mode. Localization and GUI may require restart or `reload` command.

## Code Style Guidelines

### File Naming
- Prefix mod-added files with `AoW_` (e.g., `AoW_industry.txt`).
- Use lowercase with underscores.
- Localization files MUST end in `_l_english.yml` or `_l_simp_chinese.yml`.

### Paradox Script (.txt)
- **Encoding**: UTF-8 with BOM (Byte Order Mark).
- **Indentation**: Use 1 **tab** (not spaces).
- **Spacing**: `key = value` (spaces around `=`).
- **Keywords**:
  - `REPLACE_OR_CREATE:name = { ... }`: Default for new/modified entities.
  - `INJECT:name = { ... }`: Add fields to existing vanilla definitions.
- **Tech Naming**: Append `_9981` to new technologies (e.g., `magic_theory_9981`) to avoid conflicts.

### Localization (.yml)
- **CRITICAL**: Files MUST use **UTF-8 with BOM**.
- **Indentation**: 1 space before keys (standard Paradox style).
- **Format**: `key: "Text"`
- **Icons**: Use `@icon_name!` (e.g., `@mana!`, `@mages!`).
- **Sync**: Every key in `english` must have a corresponding entry in `simp_chinese`.

### GUI (.gui)
- Follow Paradox nesting patterns. Use `AoW_texticons.gui` for icon definitions.

## Content Specifics (Skills)
For detailed implementation patterns, refer to the following in `skills/`:
- `modding-basics.md`: General workflow and keywords.
- `building-creation.md`: Building groups, PMs, and modifiers.
- `localization.md`: Color codes, dynamic text, and text icons.
- `goods-creation.md`: Defining new trade goods.

## Best Practices
1. **Atomic Changes**: Add one building or tech at a time and check `error.log`.
2. **Naming**: Use descriptive internal keys; prefix with `AoW_`.
3. **Commenting**: Use `#` for headers and explaining complex scope logic.
4. **Scope Safety**: Always verify scope (ROOT, PREV, THIS, owner) when writing triggers/effects.
5. **No WIP Deletion**: Preserve commented-out code blocks as they often represent planned features.
