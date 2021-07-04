
# First generation Intel HD Graphics on macOS
This repo contains information regarding first generation Intel HD Graphics and macOS.  

**Update:** [WhateverGreen](https://github.com/acidanthera/WhateverGreen) now can be used instead of
manual kext patches, please use it. For historical purposes, the old instructions are archived [here](README-oldway.md) for reference.  

## Requirements
* Laptop with first generation Intel HD Graphics that uses an LVDS-connected display (eDP is unsupported). Desktop systems cannot be used.  
* Mac OS X 10.6.4 to macOS 10.13.x.
* [OpenCore](https://github.com/acidanthera/OpenCorePkg) (0.6.0 or higher)
* [Lilu](https://github.com/acidanthera/Lilu)
* [WhateverGreen](https://github.com/acidanthera/WhateverGreen) (1.5.1 or higher)
* SMBIOS set to MacBookPro6,1 or MacBookPro6,2

## Configuration
Refer to [this](https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md#intel-hd-graphics-first-generation--ironlake-arrandale-processors) section
in the WhateverGreen manual for full details.  

To enable patching, add `framebuffer-patch-enable` under your iGPU device in the config.plist. For displays that are
1366x768, or as needed, you may need to enable single link mode and set the link width with `framebuffer-singlelink` and/or `framebuffer-linkwidth`.
`framebuffer-linkwidth` defaults to a link width of `1`.

All properties should be in proper 32-bit data `<XXXXXXXX>` format.

## Installation
Install macOS as normal.

## Credits
Patches based on the work by [verteks](https://www.insanelymac.com/forum/topic/286879-appleintelhdgraphicsfb-fixed-sl-1068)
and [GhostRaider](https://www.insanelymac.com/forum/topic/286092-guide-1st-generation-intel-hd-graphics-qeci). Patches used in this repo can be found [here](Patches.md).
