# Mint

An empty datapack template for **Minecraft 26.1** set up to **replace vanilla structures**.

## Why this works

To replace a vanilla structure you don't "edit" it — you place a file at the **same
resource location inside the `minecraft` namespace**, and your datapack wins (datapacks
override the built-in vanilla pack). Every folder below mirrors a vanilla path.

## Install

1. Drop the whole `Mint` folder into your world's `datapacks/` directory:
   `.minecraft/saves/<world>/datapacks/Mint/`
2. **Worldgen changes only apply to NEW worlds** (or freshly generated chunks).
   Create a new world, or run `/reload` for non-worldgen tweaks.
3. Verify it loaded with `/datapack list`.

## Layout

```
Mint/
├── pack.mcmeta                 # format declaration (see below)
└── data/
    └── minecraft/
        ├── structure/          # .nbt building pieces (singular "structure")
        └── worldgen/
            ├── structure/       # structure definitions (what + where rules)
            ├── structure_set/   # placement: spacing, separation, salt
            ├── template_pool/   # jigsaw pools for villages/bastions/etc.
            └── processor_list/  # block-swap rules for jigsaw pieces
```

## How to replace a specific vanilla structure

Copy the vanilla file from the version jar (`assets`/`data` in
`.minecraft/versions/<v>/<v>.jar`, or browse it on the [Minecraft Wiki](https://minecraft.wiki/w/Data_pack)),
edit it, and save it to the matching path here. Examples:

| Goal | File to create |
|------|----------------|
| Change plains village houses | `data/minecraft/worldgen/template_pool/village/plains/houses.json` |
| Swap a village building's blocks | `data/minecraft/structure/village/plains/houses/<name>.nbt` |
| Rarer / denser villages | `data/minecraft/worldgen/structure_set/villages.json` |
| Disable a structure entirely | override its `structure_set` with `"structures": []` |
| Change which biomes a structure spawns in | `data/minecraft/worldgen/structure/<name>.json` |

## pack.mcmeta / format note (26.1)

Since 25w31a the format is declared with `min_format` / `max_format` (each a
`[major, minor]` array) instead of the old single `pack_format` integer.
The **data pack format for 26.1 is `101.1`**:

```json
{
  "pack": {
    "description": "Mint — vanilla structure replacement (26.1)",
    "min_format": [101, 1],
    "max_format": [101, 1]
  }
}
```

Widen `max_format` if you want the pack to load on later versions without the
"incompatible" warning. Confirm the exact number for your build with `/version`
in-game.
