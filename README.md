# Asus X99 A-II ReBAR
[**English**](/README.md) | [**Русский**](./docs/ru/README.ru.md)

A proven way to activate ReBAR (Resizable BAR) on the ASUS X99 A-II.

# Prequel
A simplified and secure way through the `ASUS Flashback`, gave me the following reaction **(hold for 3 seconds, release, three blinks, constant blue glow)**, which means that it rejects the firmware file and refuses to flash it because of the signature.

In this guide, I will consider a less secure method through the `FreeDOS` shell, which bypasses this method of protection, and successfully flashes the firmware even with a modified security signature.

# Sources
This guide is a simplified (to a single method) and structured version of this guide:
- https://github.com/Mak3rde/AsusX99A-II-RezisableBar (by @Mak3rde)

xCuri0 / ReBarUEFI
- https://github.com/xCuri0/ReBarUEFI

terminatorul / NvStrapsReBar
- https://github.com/terminatorul/NvStrapsReBar

# Firmware
> [!CAUTION]
>  Only if you don't have your own BIOS modifications (otherwise, what are you doing here?)
## 1. Preparation
- Download the file `X99-A-II-ASUS-2101_ROM_STOCKROM` from [main guide](https://github.com/Mak3rde/AsusX99A-II-RezisableBar ) from the `ready to use efi Downloads` section.
- Download [AFUDOS](https://disk.yandex.ru/d/lW3H05ggRWaGiA), may be deleted due to complaints from copyright holders (search in the Internet).
- Prepare the flash drive and format it using [Rufus](https://rufus.ie/en/) in the form of `FreeDOS` FAT 32 MBR format.
- After dictation, transfer all files from the `AFUDOS` archive to the flash drive in the root folder.
- Transfer the firmware file from the archive `X99-A-II-ASUS-2101_ROM_STOCKROM` to the flash drive in the root folder.
- Rename it to `bios.rom` to simplify working with it in a `DOS` environment.
- Turn off the computer, (optional: turn on CSM in the BIOS settings) boot from a USB flash drive with FreeDOS.
## 2. FreeDOS
- Select **English keyboard layout** after launching FreeDOS
![FreeDOS Language](http://xeonlive.ru/images/materials/instructions/afudos/3.jpg )
- Make a backup of the current firmware (just in case):
```
afudos backup.rom /o
```
- Wait for the process to complete, at the end you will have the file `backup.rom`
- Now we flash our new bios with the command:
```
afudos bios.rom /gan
``` 
- Waiting for the completion of the firmware process.
- At the end of the firmware, reboot into the BIOS and remove the USB flash drive.
## 3. BIOS
All settings have been reset to standard, as they should be.
- Go to the `Boot` section and turn on `Above 4G Decoding` (set the `Enabled` position) for ReBAR work.
- Go to the `CSM` section and set the value to `Disabled` for ReBAR work.
- If you need to restore any more settings, then restore them.
- Save the changes and boot into Windows.
## 4. Windows
NVIDIA graphics cards will still display that ReBAR is not enabled in the BIOS, for this:
#### If you have NVIDIA RTX 30X and higher, use the program `ReBarState.exe`
- Download `ReBarState.exe` from [ReBabUEFI](https://github.com/xCuri0/ReBarUEFI/releases) releases.
- Launch the program (as admin) and enter the value 32 (unlimited Bar size) and press `Enter`.
- If there are no errors, restart the computer.
#### If you have an NVIDIA Turing GPU (20 or 16 series) and lower, we use `NvStrapsReBar.exe`
- Download `NvStrapsReBar.exe` from [NvStrapsReBar](https://github.com/terminatorul/NvStrapsReBar/releases) releases.
- Launch the program `NvStrapsReBar.exe` and wait.
- Find the number opposite the model of your GPU and **enter it** and press `Enter`.
- If everything is successful and there were no errors, restart the computer.

In both cases, ReBAR should now work for all GPUs (AMD/NVIDIA) that support it.
- You can check this using `GPU-Z` by launching and clicking on the **Resizable BAR** element.
- Using NVIDIA Control Panel (for NVIDIA) by clicking on `System Information` - **Resizable BAR**.

![GPU-Z Nvidia ReBAR](https://github.com/DenisSolicen/Asus-X99-A-II-ReBAR/blob/main/img/gpuz.png?raw=true)
![Nvidia Control Panel](https://github.com/DenisSolicen/Asus-X99-A-II-ReBAR/blob/main/img/nvidiacontrol.png?raw=true)

*Congratulations, now ReBAR (Resizable BAR) is working stably on the board that originally did not have its support!*
- If the guide was useful, I ask you to put *a star in the repository (click at `Star` on the top right)*.
- Do the same with in the [original guide](https://github.com/Mak3rde/AsusX99A-II-RezisableBar), without **him**, this guide would not exist, thank you!
