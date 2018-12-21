
# First generation Intel HD Graphics on macOS
This repo contains information regarding first generation Intel HD Graphics and macOS.

## Requirements
* Laptop with first generation Intel HD Graphics that uses an LVDS-connected display (eDP is unsupported). Desktop systems cannot be used.
* Mac OS X 10.6.4 to macOS 10.13.x.
* [The Clover bootloader](https://sourceforge.net/projects/cloverefiboot). Latest build: https://github.com/Dids/clover-builder/releases.

## Installation
Install macOS as normal. Graphics will need to be disabled during installation by injecting Intel with a fake-id of `0x12345678`.

## Post installation
Apply the patches and modifications in this repo to your config.plist as required. Ensure you are using an SMBIOS of MacBookPro6,x. The full list of patches can be found [here](https://github.com/Goldfish64/ArrandaleGraphicsHackintosh/blob/master/Patches.md).

## Credits
Patches based on the work by [verteks](https://www.insanelymac.com/forum/topic/286879-appleintelhdgraphicsfb-fixed-sl-1068) and [GhostRaider](https://www.insanelymac.com/forum/topic/286092-guide-1st-generation-intel-hd-graphics-qeci).
