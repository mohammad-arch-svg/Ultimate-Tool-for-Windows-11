🕯️ ShrineTool v1.1 — The Ultimate Windows 11 Ritual Suite

“Every tweak is a ritual. Every install, a ceremony. This is not automation—it’s intention.”
— Mohammad, Creator of ShrineTool

⚡ Overview

ShrineTool v1.1 is a handcrafted C++ command-line utility designed to optimize and personalize Windows 11.
Inspired by ChrisTitusTool, but reborn with manual control, stylized logic, and shrine-grade clarity.

Unlike generic “all-in-one” scripts, ShrineTool focuses on transparency and user choice — every action is visible, intentional, and ceremonial.

🧰 Features
🔧 Tweaks Menu

Disable GPS tracking

Disable telemetry

Remove Bing from Windows search

Optional Explorer restart for full ritual effect

📦 App Installer

Install Google Chrome, Visual Studio Code, VLC Media Player, 7-Zip via winget

Automatically accepts agreements and installs silently

🔍 License Status Ritual

Check your Windows activation status (slmgr /xpr)

No piracy, no cracks — pure visibility

🧾 About Section

ASCII-branded homage to the creator

Purpose, gratitude, and versioning

🖥️ Usage

⚠️ Run as Administrator
ShrineTool performs system-level rituals that require elevated permissions.

Compile the source code using a C++ compiler (MSVC recommended).

Run the executable:

./ShrineTool.exe

🛡️ Is ShrineTool Safe?

✅ Yes. ShrineTool is open-source, transparent, and built with care. Every tweak is visible in the source — no obfuscation, no hidden binaries.

⚠️ Why SmartScreen or Defender Might Warn You
Unsigned tools that:

Modify system settings (telemetry, Bing, GPS)

Use PowerShell commands

Are new and not yet reputation-established

…will often trigger Windows security heuristics. These are false positives, not real threats.

✅ How to Verify ShrineTool

🔍 Inspect the source: GitHub Repository

🧪 Scan the compiled .exe with VirusTotal

🧵 Compile it yourself using Visual Studio or g++

✨ Closing Words

“If you doubt the ritual, read the scrolls.
If you trust the shrine, run the ceremony.”

## 📜 Source Code (C++)

```cpp
#include <iostream>
#include <windows.h>

using namespace std;

int main() {
    int choose = 0;
    int tweaks = 0;
    int install_app = 0;
    int About = 0;

    cout << "==========================================" << endl;
    cout << "        ShrineTool v1.1 — Windows 11      " << endl;
    cout << "==========================================" << endl;
    cout << endl;
    cout << "[1] Tweaks" << endl;
    cout << "[2] Install Apps" << endl;
    cout << "[3] Check License Status" << endl;
    cout << "==================" << endl;
    cout << "[4] About" << endl;
    cout << "==================" << endl;
    cout << endl;
    cout << "Please run as Administrator. Choose from 1 to 4:" << endl;
    cin >> choose;

    switch (choose) {
    case 1:
        cout << "=================" << endl;
        cout << "Welcome to Tweaks" << endl;
        cout << "=================" << endl;
        cout << endl;
        cout << "[1] Disable GPS tracking" << endl;
        cout << "[2] Disable telemetry" << endl;
        cout << "[3] Disable Bing from search" << endl;
        cout << endl;
        cout << "Choose from 1 to 3:" << endl;
        cin >> tweaks;

        if (tweaks == 1) {
            cout << "Disabling GPS tracking..." << endl;
            system("powershell -Command \"Stop-Service -Name lfsvc -Force\"");
            system("powershell -Command \"Set-Service -Name lfsvc -StartupType Disabled\"");
            cout << "Success" << endl;
        }
        else if (tweaks == 2) {
            cout << "Disabling Telemetry..." << endl;
            system("powershell -Command \"Stop-Service -Name diagtrack -Force\"");
            system("powershell -Command \"Set-Service -Name diagtrack -StartupType Disabled\"");
            cout << "Success" << endl;
        }
        else if (tweaks == 3) {
            cout << "Disabling Bing search..." << endl;
            system("powershell -Command \"New-Item -Path HKCU:\\Software\\Policies\\Microsoft\\Windows\\Explorer -Force\"");
            system("powershell -Command \"New-ItemProperty -Path 'HKCU:\\Software\\Policies\\Microsoft\\Windows\\Explorer' -Name 'DisableSearchBoxSuggestions' -Value 1 -PropertyType DWord -Force\"");
            char choose1;
            cout << "A restart of Explorer is recommended. Restart now? (y/n): ";
            cin >> choose1;

            if (choose1 == 'y' || choose1 == 'Y') {
                cout << "Restarting Explorer..." << endl;
                system("powershell -Command \"Stop-Process -Name explorer -Force\"");
            }
            else {
                cout << "Restart aborted. Please restart Explorer later for changes to take effect." << endl;
            }
        }
        break;

    case 2:
        cout << "==================" << endl;
        cout << "Install Apps" << endl;
        cout << "==================" << endl;
        cout << endl;
        cout << "[1] Google Chrome" << endl;
        cout << "[2] Visual Studio Code" << endl;
        cout << "[3] 7-Zip" << endl;
        cout << "[4] VLC Media Player" << endl;
        cout << endl;
        cout << "Choose an app to install (1-4): " << endl;
        cin >> install_app;

        if (install_app == 1) {
            cout << "Installing Google Chrome..." << endl;
            system("powershell -Command \"winget install --id Google.Chrome -e --accept-package-agreements --accept-source-agreements\"");
        }
        else if (install_app == 2) {
            cout << "Installing Visual Studio Code..." << endl;
            system("powershell -Command \"winget install --id Microsoft.VisualStudioCode -e --accept-package-agreements --accept-source-agreements\"");
        }
        else if (install_app == 3) {
            cout << "Installing 7-Zip..." << endl;
            system("powershell -Command \"winget install --id 7zip.7zip -e --accept-package-agreements --accept-source-agreements\"");
        }
        else if (install_app == 4) {
            cout << "Installing VLC Media Player..." << endl;
            system("powershell -Command \"winget install --id VideoLAN.VLC -e --accept-package-agreements --accept-source-agreements\"");
        }
        cout << "Success." << endl;
        break;

    case 3:
        cout << "Checking Windows license status..." << endl;
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
        int i;
        cout << "This Tool Made by Mohammad" << endl;
        cout << "Purpose: To make Windows 11 better" << endl;
        cout << "Thanks to everyone using ShrineTool" << endl;
        cout << "Version 1.1 (Safe Edition)" << endl;
        cin >> i;
        break;
    }

    return 0;
}


