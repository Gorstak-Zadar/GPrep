# GPrep

**System Software Installer** — A Ninite/PatchMyPC-style app that installs 70+ programs from a single Control Panel applet. Supports **Windows 7 through 11**.

[![Windows](https://img.shields.io/badge/Windows-7%20%7C%208%20%7C%2010%20%7C%2011-0078D6?logo=windows)](https://www.microsoft.com/windows)

## Features

| Feature | Description |
|---------|-------------|
| **Control Panel applet** | Runs as a classic .cpl; double-click in Control Panel or run directly |
| **Modern / Legacy tabs** | Choose apps for Win10/11 or Win7/8 |
| **OS detection** | On Windows 7, Legacy tab opens automatically with compatible apps |
| **70+ applications** | Browsers, dev tools, gaming, media, utilities, and more |
| **Flexible installers** | Modern: winget, Chocolatey. Legacy: direct download URLs |

## Quick Start

1. **Download** or clone this repo
2. **Copy** `GPrep.cpl`, `GPrepUI.hta`, `GPrepHelper.ps1`, and `manifest.json` into one folder
3. **Run**  
   `control.exe "C:\path\to\GPrep.cpl"`  
   or double-click the .cpl file

## Installation

### Option A: Run from any folder

No install. Keep the four files together and run:

```batch
control.exe "D:\GPrep\GPrep.cpl"
```

### Option B: Register in Control Panel

1. Copy the four files to e.g. `C:\Program Files\GPrep\`
2. Edit `install-cpl.reg` and set the path to match
3. Double-click the .reg file (requires admin)
4. Open Control Panel → GPrep appears in the list

### Files

| File | Purpose |
|------|---------|
| `GPrep.cpl` | Control Panel applet (launches the UI) |
| `GPrepUI.hta` | Ninite-style checkbox interface |
| `GPrepHelper.ps1` | Installer engine (winget / Chocolatey / direct) |
| `manifest.json` | App catalog (70+ entries) |

## Usage

1. Open GPrep (via Control Panel or `control.exe GPrep.cpl`)
2. Switch between **Modern (Win10/11)** and **Legacy (Win7/8)**
3. Check the apps you want
4. Click **Install Selected** (admin rights may be requested)

## Included Apps (sample)

**Browsers:** Firefox, Chrome, Vivaldi, Opera, Brave, Edge, Arc, Tor, LibreWolf, Mypal (Win7)  
**Utilities:** 7-Zip, WinRAR, Notepad++, Everything, ShareX, PuTTY, WinSCP, KeePassXC, WinMerge  
**Media:** VLC, foobar2000, Audacity, GIMP, Krita, OBS Studio, HandBrake, K-Lite Codec  
**Development:** VS Code, Git, Node.js, Python, DBeaver, HeidiSQL, Postman  
**Gaming:** Steam, Discord, Epic, GOG Galaxy, Minecraft, Playnite, Prism Launcher  
**Security:** VeraCrypt, Bitwarden, BleachBit, Malwarebytes  
**Office:** LibreOffice, Sumatra PDF, Zoom, Telegram  
**System:** HWiNFO64, CPU-Z, GPU-Z, CrystalDiskInfo, PowerToys, Rainmeter  

See `manifest.json` for the full list.

## Windows 7 / 8 (Legacy)

On older Windows:

- Legacy mode opens by default
- Only apps with known Win7/8-compatible versions are shown
- Uses direct downloads and Chocolatey (winget is not available)
- Firefox ESR, Vivaldi 5.6, Opera 95, and Mypal are supported browsers

## Customization

Edit `manifest.json` to add or change apps:

```json
{
  "id": "myapp",
  "name": "My App",
  "category": "Utilities",
  "modern": { "winget": "Publisher.AppName" },
  "legacy": {
    "url": "https://example.com/setup.exe",
    "filename": "setup.exe"
  }
}
```

| Field | Description |
|-------|-------------|
| `modern.winget` | Winget package ID |
| `modern.choco` | Chocolatey package name |
| `modern.url` | Direct download URL |
| `legacy` | Use `null` if no Windows 7 support |
| `legacy.isZip` | Set to `true` for zip archives |

## Building the CPL

Pre-built `GPrep.cpl` is included. To rebuild:

```batch
cd CPL
build-mingw.bat    # Requires MinGW or LLVM-MinGW
# or
build.bat          # Requires Visual Studio Developer Command Prompt
```

Manual build with gcc:
```batch
gcc -shared -o GPrep.cpl GPrep.c -lshell32 -s -Os
```

## License

MIT (or specify your preferred license)

---

## Disclaimer

**NO WARRANTY.** THERE IS NO WARRANTY FOR THE PROGRAM, TO THE EXTENT PERMITTED BY APPLICABLE LAW. EXCEPT WHEN OTHERWISE STATED IN WRITING THE COPYRIGHT HOLDERS AND/OR OTHER PARTIES PROVIDE THE PROGRAM "AS IS" WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE. THE ENTIRE RISK AS TO THE QUALITY AND PERFORMANCE OF THE PROGRAM IS WITH YOU. SHOULD THE PROGRAM PROVE DEFECTIVE, YOU ASSUME THE COST OF ALL NECESSARY SERVICING, REPAIR OR CORRECTION.

**Limitation of Liability.** IN NO EVENT UNLESS REQUIRED BY APPLICABLE LAW OR AGREED TO IN WRITING WILL ANY COPYRIGHT HOLDER, OR ANY OTHER PARTY WHO MODIFIES AND/OR CONVEYS THE PROGRAM AS PERMITTED ABOVE, BE LIABLE TO YOU FOR DAMAGES, INCLUDING ANY GENERAL, SPECIAL, INCIDENTAL OR CONSEQUENTIAL DAMAGES ARISING OUT OF THE USE OR INABILITY TO USE THE PROGRAM (INCLUDING BUT NOT LIMITED TO LOSS OF DATA OR DATA BEING RENDERED INACCURATE OR LOSSES SUSTAINED BY YOU OR THIRD PARTIES OR A FAILURE OF THE PROGRAM TO OPERATE WITH ANY OTHER PROGRAMS), EVEN IF SUCH HOLDER OR OTHER PARTY HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGES.
