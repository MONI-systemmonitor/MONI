# MONI

A dashboard for Windows that shows what your PC is doing — processor, graphics cards, memory,
drives, network, frame rate and fans — on one board that you arrange yourself.

---

## Install

Download `MONI-setup.exe` from the Releases page and run it — the newest release is always the one
that page opens on:

**https://github.com/MONI-SystemMonitor/MONI/releases/latest**

**The file has no version number in its name, and that is deliberate.** A release is found by its
tag (`v1.1.0`), and the version is written in three places a person actually reads: the tag, the
About card inside the program, and the entry in *Apps*. **A version typed into a file name is the one
copy that goes stale** — it happened to this project's own executable, which stayed `MONI3.exe`
through two renames. It is also what makes the automatic update possible at all: the program asks a
single unchanging address,
`https://github.com/MONI-SystemMonitor/MONI/releases/latest/download/MONI-setup.exe`, which GitHub resolves to the
newest release's file of that name.

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

**MONI looks for a newer version when it starts, and can install it for you.**

It asks one small text file for the version that is current and compares it with the build that is
running. That happens **once, after the board is up**, so nothing about the start is slower. If there
is a newer version it says so in the notification center and on the status bar; **if there is not, it
says nothing at all; and if there is no network it says nothing either** — a machine with no internet
is not a fault. The whole check can be turned off in *Settings → Starting up*.

*Settings → About* has two buttons:

- **Check for updates** asks the address and tells you the answer. It downloads nothing.
- **Download and install** fetches the new version, **checks that it arrived whole**, closes MONI,
  runs the installer without showing you a wizard, and starts MONI again.

**Nothing on your machine is replaced until that check has passed.** The download goes to a temporary
file, its size is compared with what the server said, and its SHA-256 is compared with the hash the
release page records. A download that failed, arrived truncated or does not match is refused: MONI
says so on screen and keeps working, with your installation exactly as it was. A half-replaced MONI
would be worse than an old one.

The release page is still there for anyone who would rather install by hand, and the button beside it
opens it.

## What is in this repository

**Three files, and nothing else.**

| File | What it is |
|---|---|
| `README.md` | this page |
| `CHANGELOG.txt` | the changelog. The same file the installed program shows under Settings → About, and the page the installer's wizard draws |
| `latest.txt` | **one line — the version that is current.** This is the file the update check reads |

**The program's source code is not published here.** The installer attached to each release is the
whole of what is handed out.
