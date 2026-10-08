# MONI

A dashboard for Windows that shows what your PC is doing — processor, graphics cards, memory,
drives, network, frame rate and fans — on one board that you arrange yourself.

---

## Install

Download the newest `MONI-x.y.z-setup.exe` from the Releases page and run it:

**https://github.com/MONI-SystemMonitor/MONI/releases/latest**

- **Windows will warn you.** The installer is not code-signed, so Windows shows *"Windows protected
  your PC"* and names an unknown publisher. Click **More info**, then **Run anyway**. It works; it
  arrives with a warning.
- **MONI asks for administrator rights on every launch, and it needs them.** Without them Windows
  does not let any program read the processor's temperature, the motherboard's fans or the storage
  hardware — about a third of what the machine reports. Those readings are then **absent rather than
  wrong**, and MONI says so on its status bar.
- **64-bit Windows 10 version 2004 (build 19041) or newer.**

There is nothing else to install: the installer carries the whole .NET runtime MONI needs.

## Uninstall

**Settings → Apps → MONI → Uninstall**, or *Uninstall MONI* in the Start menu.

**Your boards are not deleted.** They live in `%APPDATA%\MONI3\profiles` and are left where they are.

## The sensor driver, said plainly

MONI reads the hardware through LibreHardwareMonitor, which carries the **WinRing0** kernel driver.
It is written beside the program as `MONI.sys` and registered as the kernel service **`R0MONI`** at
the first elevated run — that registration is why MONI asks for administrator rights at all.

**Windows Defender classifies that driver file as `VulnerableDriver:WinNT/Winring0`, and the
classification is correct**: it is a known-vulnerable driver, which is exactly what makes raw
hardware access possible. AIDA64 and HWiNFO carry equivalents. It is a real trade-off, and it is
named here rather than discovered later.

**The uninstaller removes it** — the service is stopped, its registration is deleted, and the file
goes. A program that leaves a known-vulnerable driver on a machine for ever after the user believes
they have removed it is not acceptable.

## Updates

**MONI does not update itself, deliberately.** *Settings → About → Check for updates* asks one small
text file for the version that is current, compares it with the build that is running, and — if there
is a newer one — opens the release page. Installing is then done by hand.

The reason is in the sentence above the last one: MONI installs a kernel driver, and a program that
replaces itself while a driver is loaded is a problem nobody needs.

## What is in this repository

**Three files, and nothing else.**

| File | What it is |
|---|---|
| `README.md` | this page |
| `CHANGELOG.txt` | the changelog. The same file the installed program shows under Settings → About, and the page the installer's wizard draws |
| `latest.txt` | **one line — the version that is current.** This is the file the update check reads |

**The program's source code is not published here.** The installer attached to each release is the
whole of what is handed out.
