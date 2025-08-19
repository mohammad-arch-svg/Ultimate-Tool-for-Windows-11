# ShrineTool v2.0

ShrineTool is a command-line utility designed to enhance Windows 11 by applying useful system tweaks, installing popular applications, and checking the Windows license status. It’s a simple tool for power users who want quick access to common tweaks and software installation.

---

## Features in v2.0

- Prompt to create a **system restore point** before making changes.
- Tweaks to:
  - Disable GPS tracking
  - Disable telemetry
  - Disable Bing search suggestions
- Install popular apps using `winget`:
  - Google Chrome, Visual Studio Code, 7-Zip, VLC, Brave, Visual Studio 2022, Notepad++, Spotify, Git, Mozilla Firefox, Python, OBS Studio, Discord
- Check Windows license status.
- About section with ASCII art and pause to keep window open.
- Prompts to ensure running as Administrator and testing on a virtual machine.

---

## How to Use

1. Compile the source code with a C++ compiler (Visual Studio recommended).
2. Run the executable as Administrator.
3. Follow on-screen instructions:
   - Choose to create a restore point.
   - Select Tweaks, Install Apps, Check License Status, or About.
   - Follow prompts for each section.

---

## Source Code

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
    cout << "        ShrineTool v2.0 — Windows 11      " << endl;
    cout << "==========================================" << endl;
    cout << endl;
    cout << "[1] Tweaks" << endl;
    cout << "[2] Install Apps" << endl;
    cout << "[3] Check License Status" << endl;
    cout << "==================" << endl;
    cout << "[4] About" << endl;
    cout << "==================" << endl;
    cout << endl;
    char restore;
    cout << "Before we get started let's make restore point do you  want to make restore point (y/n):" << endl;
    cin >> restore;

    if (restore == 'y' || restore == 'Y') {
        cout << "making restore point..." << endl;
        system("powershell -Command \"Checkpoint-Computer -Description 'ShrineTool Restore Point' -RestorePointType 'MODIFY_SETTINGS'\"");
        cout << "==================================" << endl;
        cout << "Done" << endl;
        cout << "==================================" << endl;
    }
    else if (restore == 'n' || restore == 'N') {
        cout << "Aborted. please make restore point first if something goes wrong" << endl;
    }
    cout << "Please run as Administrator. Choose from (1 to 4):" << endl;
    cin >> choose;

    switch (choose) {
    case 1:
        char w;
        cout << "=================" << endl;
        cout << "Welcome to Tweaks" << endl;
        cout << "=================" << endl;
        cout << endl;
        cout << "[1] Disable GPS tracking" << endl;
        cout << "[2] Disable telemetry" << endl;
        cout << "[3] Disable Bing from search" << endl;
        cout << endl;
        cout << "NOTICE: This will modify system settings. Make sure you have created a restore point. Do you want to continue? (y/n): ";
        cin >> w;

        if (w == 'y' || w == 'Y') {
            cout << endl;
        }
        else if (w == 'n' || w == 'N') {
            cout << "Aborted." << endl;
            system("pause");
            break;
        }
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
        cout << "[5] Brave" << endl;
        cout << "[6] Visual Studio 2022" << endl;
        cout << "[7] Notepad++" << endl;
        cout << "[8] Spotify" << endl;
        cout << "[9] Git" << endl;
        cout << "[10] Mozilla Firefox" << endl;
        cout << "[11] Python" << endl;
        cout << "[12] OBS Studio" << endl;
        cout << "[13] Discord" << endl;
        cout << endl;
        cout << "Choose an app to install (1-13): " << endl;
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
        else if (install_app == 5) {
            cout << "Installing Brave Browser..." << endl;
            system("powershell -Command \"winget install --id Brave.BraveBrowser -e --accept-package-agreements --accept-source-agreements\"");
        }
        else if (install_app == 6) {
            cout << "Installing Visual Studio 2022..." << endl;
            system("powershell -Command \"winget install --id Microsoft.VisualStudio.2022.Community -e --accept-package-agreements --accept-source-agreements\"");
        }
        else if (install_app == 7) {
            cout << "Installing Notepad++..." << endl;
            system("powershell -Command \"winget install --id Notepad++.Notepad++ -e --accept-package-agreements --accept-source-agreements\"");
        }
        else if (install_app == 8) {
            cout << "Installing Spotify..." << endl;
            system("powershell -Command \"winget install --id Spotify.Spotify -e --accept-package-agreements --accept-source-agreements\"");
        }
        else if (install_app == 9) {
            cout << "Installing Git..." << endl;
            system("powershell -Command \"winget install --id Git.Git -e --accept-package-agreements --accept-source-agreements\"");
        }
        else if (install_app == 10) {
            cout << "Installing Mozilla Firefox..." << endl;
            system("powershell -Command \"winget install --id Mozilla.Firefox -e --accept-package-agreements --accept-source-agreements\"");
        }
        else if (install_app == 11) {
            cout << "Installing Python..." << endl;
            system("powershell -Command \"winget install --id Python.Python.3 -e --accept-package-agreements --accept-source-agreements\"");
        }
        else if (install_app == 12) {
            cout << "Installing OBS Studio..." << endl;
            system("powershell -Command \"winget install --id OBSProject.OBSStudio -e --accept-package-agreements --accept-source-agreements\"");
        }
        else if (install_app == 13) {
            cout << "Installing Discord..." << endl;
            system("powershell -Command \"winget install --id Discord.Discord -e --accept-package-agreements --accept-source-agreements\"");
        }
        else {
            cout << "Invalid choice." << endl;
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
        cout << "This Tool Made by Mohammad" << endl;
        cout << "Purpose: To make Windows 11 better" << endl;
        cout << "Thanks to everyone using ShrineTool" << endl;
        cout << "Version 2.0" << endl;
        system("pause");
        cout << "Press any key to continue..." << endl;
        break;
    }

    return 0;
}
