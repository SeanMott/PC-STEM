# How To Use

Place the GS plugin inside PCSX2's plugins folder. Afterwards, go to `Config > Plugin/BIOS Selector`. Ensure under the `Plugins` section that the `GS` plugin is set to the new `GSdx` plugin.

After applying the change and the plugin has been initialized, click `Configure...` to open the plugin's settings. Settings can be set to whatever you like, with the exception of `GPU Palette Conversion`. This setting must be *DISABLED* in order to enable `Manipulation Functions`.

Enabling the aforementioned option will present the choice of either dumping or replacing textures. Dumped textures for every game will be automatically placed within `textures/@DUMP/[CRC]` inside of PCSX2's root directory. The CRC will match the CRC32 of the booted game. For example, Kingdom Hearts II Final Mix textures would be placed in `textures/@DUMP/F266B00B` and Dragon Ball Budokai 3 would be placed in `textures/@DUMP/2A4B60EB`.

To replace textures, an YAML config named `[CRC].yaml` must be placed within a `txtconfig` folder in PCSX2's folder. Said YAML must follow a format in order to apply changed textures, detailed below.

NOTE: AMD Cards may require Anti-Aliasing enabled for the textures to look good.
NOTE 2: Textures must be made in DDS format in either RGBA8 or BGRA8. And it must be uncompressed.

# YAML Layout

```yaml
ProcessTEX: 
  0x0CF2C584: "@COM/field2d/zz0field.dds"
  0x1971E6D5: "@COM/field2d/zz1field.dds"
  0x0F92318E: "@COM/obj/P_EX100/texture00.dds"
  0xB901C8DB: "@COM/obj/P_EX100/texture01.dds"
```

## YAML Descriptors & Formatting Info

Commenting out lines with `#` is valid. While not necessary, the top few lines can be dedicated to credits and other info. For example, game name, texture pack creator, version details, date published, etc.

`ProcessTEX` is the only table present for replacements. All textures should be placed under this category.

Hashes for textures can be grabbed from the `@DUMP` location and must be placed in the appropriate `txtconfig`. Simply formatting the texture table as `0x[hash] = [location]` inside the `textures` folder is enough. For example, in replacing image hash 0F92318E, the directory `textures/@COM/obj/P_EX100/texture00.dds` was created and inside is a higher quality `0.dds` texture. As such, we end up with `0x23A3A104:  @COM/obj/P_EX100/texture00.dds` inside the config. 

Image hashes will always be the same between all copies of a game, provided the CRC is the same and in the event of modified games like Kingdom Hearts the exact same modifications are applied. If a texture is changed, its hash naturally changes and will not replace upon loading.

# Closing

### This much requested feature has finally been created and is pretty much as user friendly as can be at this point. There really isn't much else to say other than, happy texturing!