# 🕯️ ShrineTool v1.0 — The Ultimate Windows 11 Ritual Suite

> _“Every tweak is a ritual. Every install, a ceremony. This is not automation—it’s intention.”_  
> — Mohammad, Creator of ShrineTool

---

## ⚡ Overview

**ShrineTool v1.0** is a handcrafted C++ command-line utility designed to optimize and personalize Windows 11.  
Inspired by ChrisTitusTool, but reborn with manual control, stylized logic, and shrine-grade clarity.

---

## 🧰 Features

- 🔧 **Tweaks Menu**  
  - Disable GPS tracking  
  - Disable telemetry  
  - Remove Bing from Windows search  
  - Explorer restart prompt for full ritual effect

- 📦 **App Installer**  
  - Install Chrome, VS Code, VLC, 7-Zip via `winget`  
  - Accepts agreements and installs silently

- 🔐 **KMS Activation Ritual**  
  - Activates Windows 11 Pro using sacred PowerShell invocations  
  - Displays activation status with `slmgr /xpr`

- 🧾 **About Section**  
  - ASCII-branded homage to the creator  
  - Purpose, gratitude, and versioning

---

## 🖥️ Usage

> ⚠️ **Run as Administrator**  
> ShrineTool performs system-level rituals that require elevated permissions.

1. Compile the source code using a C++ compiler (MSVC recommended).
2. Run the executable:
   ```bash
   ./ShrineTool.exe


   🛡️ Is ShrineTool Safe?
Yes. ShrineTool is open-source, transparent, and built with care. Every tweak is visible in the source — no obfuscation, no hidden binaries.

⚠️ Why SmartScreen or Defender Might Warn You
Windows flags unsigned tools by default, especially those that:

Modify system settings (telemetry, Bing, GPS)

Use KMS activation logic

Are new and haven’t built reputation yet

These are heuristic triggers, not actual threats.

✅ How to Verify ShrineTool
🔍 Inspect the source: GitHub Repository

🧪 Scan the compiled .exe with VirusTotal

🧵 Compile it yourself using Visual Studio or g++

“If you doubt the ritual, read the scrolls. If you trust the shrine, run the ceremony.”

you can sae the source code this is the source code c++:

<pre lang="markdown">
#include <iostream>
#include <windows.h>

using namespace std;

int main() {
    int choose = 0, tweaks = 0, install_app = 0, kms = 0, About = 0;

    cout << "==========================================" << endl;
    cout << "The Ultimate Windows 11 Tool" << endl;
    cout << "==========================================" << endl;
    cout << "[1] tweaks\n[2] install app\n[3] kms activate pro edition\n[4] About" << endl;
    cout << "please run that as administrator choose from 1 to 4:" << endl;
    cin >> choose;

    switch (choose) {
    case 1:
        cout << "[1]disable GPS tracking\n[2] disable telemetry\n[3] disable Bing from search" << endl;
        cin >> tweaks;

        if (tweaks == 1) {
            system("powershell -Command \"Stop-Service -Name lfsvc -Force\"");
            system("powershell -Command \"Set-Service -Name lfsvc -StartupType Disabled\"");
        } else if (tweaks == 2) {
            system("powershell -Command \"Stop-Service -Name diagtrack -Force\"");
            system("powershell -Command \"Set-Service -Name diagtrack -StartupType Disabled\"");
        } else if (tweaks == 3) {
            system("powershell -Command \"New-Item -Path HKCU:\\Software\\Policies\\Microsoft\\Windows\\Explorer -Force\"");
            system("powershell -Command \"New-ItemProperty -Path 'HKCU:\\Software\\Policies\\Microsoft\\Windows\\Explorer' -Name 'DisableSearchBoxSuggestions' -Value 1 -PropertyType DWord -Force\"");
            char choose1;
            cout << "Restart Explorer? (y/n): "; cin >> choose1;
            if (choose1 == 'y' || choose1 == 'Y') {
                system("powershell -Command \"Stop-Process -Name explorer -Force\"");
            }
        }
        break;

    case 2:
        cout << "[1] Chrome\n[2] VS Code\n[3] 7-Zip\n[4] VLC" << endl;
        cin >> install_app;

        if (install_app == 1)
            system("powershell -Command \"winget install --id Google.Chrome -e --accept-package-agreements --accept-source-agreements\"");
        else if (install_app == 2)
            system("powershell -Command \"winget install --id Microsoft.VisualStudioCode -e --accept-package-agreements --accept-source-agreements\"");
        else if (install_app == 3)
            system("powershell -Command \"winget install --id 7zip.7zip -e --accept-package-agreements --accept-source-agreements\"");
        else if (install_app == 4)
            system("powershell -Command \"winget install --id VideoLAN.VLC -e --accept-package-agreements --accept-source-agreements\"");
        break;

    case 3:
        system("powershell -Command \"slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX\"");
        system("powershell -Command \"slmgr /skms kms8.msguides.com\"");
        system("powershell -Command \"slmgr /ato\"");
        system("powershell -Command \"slmgr /xpr\"");
        break;

    case 4:
        cout << R"(
   ____       _       _     _           
  |  _ \ ___ | |_   _| |__ (_)_ __  ___ 
  | |_) / _ \| | | | | '_ \| | '_ \/ __|
  |  __/ (_) | | |_| | |_) | | | | \__ \
  |_|   \___/|_|\__,_|_.__/|_|_| |_|___/
)" << endl;
        cout << "This Tool Made by Mohammad\nPurpose: To make Windows 11 better\nThanks to everyone using ShrineTool\nVersion 1.0" << endl;
        int i; cin >> i;
        break;
    }

    return 0;
}
