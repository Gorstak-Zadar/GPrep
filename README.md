<!-- description: GPrep: GPrep.ps1 bulk winget + tweaks; manifest.json + GPrepHelper.ps1 selective OS-aware installs (Win10+ vs legacy). -->

# GPrep

This repo contains **two related approaches** to “prep” a Windows machine:

### 1. `GPrep.ps1` (monolithic)

Runs **elevated** (self-relaunches if needed). In order, it roughly:

- **`winget install`** a long **fixed list** of package IDs (browsers, Steam, dev tools, games, etc.).
- Sets **DNS** on all **up** adapters to **Cloudflare** **1.1.1.1** / **1.0.0.1** (IPv4 and IPv6).
- **`Disable-MMAgent -MemoryCompression`**, creates a **restore point**, prunes **phantom PnP** devices, disables **USB power management** via WMI, applies **BCD** tweaks (including **VM**-related options), **NTFS** `fsutil` behavior, **RAM** memory-management registry values, sets many services to **Manual**, **mouse curve** tweaks, **SSD**-oriented disk settings, adds a **desktop “Restart to BIOS”** context menu, downloads **PowerToys** and **FxSound** installers, then **Chocolatey** + extra packages, then more **winget** IDs.

**Warning:** Opinionated, **heavy**, and **hard to undo** as a whole—review the script before use.

### 2. `manifest.json` + `GPrepHelper.ps1` (selective)

**`GPrepHelper.ps1`** reads **`manifest.json`**: each app has **`modern`** (e.g. **winget** / **choco** IDs) and **`legacy`** (direct **URLs** for older Windows). **Pre–Windows 10** uses **legacy** paths; **Windows 10 and later** uses **modern** where available. It is invoked with **`-AppIds`** (list of manifest **`id`** strings). Comments in the script reference **GPrep.cpl** / **GPrepUI.hta** as a possible UI front-end.

---

## Usage

```powershell
# Monolithic prep (after reading the script)
.\GPrep.ps1

# Selective installs (example IDs from manifest.json)
.\GPrepHelper.ps1 -AppIds firefox,7zip,vlc
```

---

## Disclaimer

**NO WARRANTY.** THERE IS NO WARRANTY FOR THE PROGRAM, TO THE EXTENT PERMITTED BY APPLICABLE LAW. EXCEPT WHEN OTHERWISE STATED IN WRITING THE COPYRIGHT HOLDERS AND/OR OTHER PARTIES PROVIDE THE PROGRAM "AS IS" WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE. THE ENTIRE RISK AS TO THE QUALITY AND PERFORMANCE OF THE PROGRAM IS WITH YOU. SHOULD THE PROGRAM PROVE DEFECTIVE, YOU ASSUME THE COST OF ALL NECESSARY SERVICING, REPAIR OR CORRECTION.

**Limitation of Liability.** IN NO EVENT UNLESS REQUIRED BY APPLICABLE LAW OR AGREED TO IN WRITING WILL ANY COPYRIGHT HOLDER, OR ANY OTHER PARTY WHO MODIFIES AND/OR CONVEYS THE PROGRAM AS PERMITTED ABOVE, BE LIABLE TO YOU FOR DAMAGES, INCLUDING ANY GENERAL, SPECIAL, INCIDENTAL OR CONSEQUENTIAL DAMAGES ARISING OUT OF THE USE OR INABILITY TO USE THE PROGRAM (INCLUDING BUT NOT LIMITED TO LOSS OF DATA OR DATA BEING RENDERED INACCURATE OR LOSSES SUSTAINED BY YOU OR THIRD PARTIES OR A FAILURE OF THE PROGRAM TO OPERATE WITH ANY OTHER PROGRAMS), EVEN IF SUCH HOLDER OR OTHER PARTY HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGES.

---

## Explained like you're five (the honest kind)

Your PC is a **busy kitchen**. This repo is at best a **sticky note on the fridge**: it might remind you where the knives are, but it does not make you a Michelin chef, and it definitely does not stop someone from sneaking in through the window. We use simple words on purpose so nobody confuses scripts with superpowers.

---

## Disclaimer (read this; it matters)

This software and documentation are provided **“as is”**, without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. **Use at your own risk.**

- Nothing here is professional security, legal, medical, or financial advice.
- The authors and contributors are **not liable** for any direct, indirect, incidental, special, exemplary, or consequential damages (including loss of data, profits, goodwill, or business interruption) arising from use or inability to use this material, **even if advised of the possibility** of such damages.
- You are solely responsible for compliance with laws and policies that apply to you. Do not use these tools to violate privacy, computer misuse laws, or terms of service.
- “Detection,” “monitoring,” and “hardening” features can be wrong (false positives), miss real threats (false negatives), and change system behavior. **Test in a safe environment** before relying on anything important.

If you do not agree, **do not use** this repository.
