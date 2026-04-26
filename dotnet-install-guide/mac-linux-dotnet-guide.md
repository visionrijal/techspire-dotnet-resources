# .NET 10 Installation Guide - macOS & Linux

Follow the section for your operating system. All commands run in a terminal.

---

## Table of Contents

- [macOS](#macos)
- [Debian / Ubuntu](#debian--ubuntu)
- [Fedora / RHEL](#fedora--rhel)
- [Arch Linux](#arch-linux)
- [Verify Installation](#verify-installation)

---

## macOS

### Step 1 - Open Terminal

Press **Cmd + Space**, type `Terminal` and press **Enter**.


### Step 2 - Install the .NET 10 SDK

**Option A - Homebrew** (recommended if you already have Homebrew installed)

```bash
brew install --cask dotnet-sdk
```

**Option B - Microsoft install script** (no Homebrew required)

```bash
curl -fsSL https://dot.net/v1/dotnet-install.sh | bash /dev/stdin --channel 10.0
```


The SDK includes the base runtime and ASP.NET Core runtime. No separate downloads are needed.

Note: Apple Silicon (M1/M2/M3) is fully supported. Both options above detect your architecture automatically and install the correct Arm64 build.

### Step 3 - Add dotnet to your PATH

Skip this step if you used Homebrew. Homebrew handles PATH automatically.

If you used Option B, add `dotnet` to your PATH so it is available in every terminal session.

**zsh** (default on macOS Catalina and later):

```bash
echo 'export PATH="$HOME/.dotnet:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

**bash:**

```bash
echo 'export PATH="$HOME/.dotnet:$PATH"' >> ~/.bash_profile
source ~/.bash_profile
```

### Step 4 - Install VS Code

```bash
brew install --cask visual-studio-code
```

If you do not have Homebrew, download the `.dmg` from [code.visualstudio.com](https://code.visualstudio.com).

### Step 5 - Install C# Extensions

Open a new terminal window after VS Code installs, then run:

```bash
code --install-extension ms-dotnettools.csdevkit
```

This installs C# Dev Kit. The base C# (Roslyn) extension is pulled in automatically as a dependency.


---

## Debian / Ubuntu

### Step 1 - Open Terminal

Press **Ctrl + Alt + T** or search for Terminal in your application menu.

### Step 2 - Add the Microsoft package repository

```bash
wget https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
```


### Step 3 - Install the .NET 10 SDK

```bash
sudo apt-get update
sudo apt-get install -y dotnet-sdk-10.0
```


### Step 4 - Install VS Code

```bash
sudo apt-get install -y wget gpg
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" | sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null
sudo apt-get update
sudo apt-get install -y code
```

### Step 5 - Install C# Extensions

```bash
code --install-extension ms-dotnettools.csdevkit
```

---

## Fedora / RHEL

### Step 1 - Open Terminal

Search for Terminal in your application menu or press **Ctrl + Alt + T**.

### Step 2 - Add the Microsoft package repository

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo wget -O /etc/yum.repos.d/microsoft-prod.repo https://packages.microsoft.com/config/fedora/$(rpm -E %fedora)/prod.repo
```

### Step 3 - Install the .NET 10 SDK

```bash
sudo dnf install -y dotnet-sdk-10.0
```

### Step 4 - Install VS Code

VS Code is available from the same Microsoft repository added in Step 2.

```bash
sudo dnf install -y code
```

### Step 5 - Install C# Extensions

```bash
code --install-extension ms-dotnettools.csdevkit
```

---

## Arch Linux

### Step 1 - Open Terminal

### Step 2 - Install the .NET 10 SDK

The .NET SDK is available in the official Arch repositories.

```bash
sudo pacman -Syu dotnet-sdk-10.0
```

### Step 3 - Install VS Code

VS Code (open source build) is available via the AUR. Install `yay` first if you do not have an AUR helper:

```bash
sudo pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

Then install VS Code:

```bash
yay -S visual-studio-code-bin
```

### Step 4 - Install C# Extensions

```bash
code --install-extension ms-dotnettools.csdevkit
```

---

## Verify Installation

Open a new terminal window and run:

```bash
dotnet --version
dotnet --list-runtimes
```

Expected output:

```
10.0.x
Microsoft.AspNetCore.App 10.0.x [/usr/share/dotnet/shared/...]
Microsoft.NETCore.App 10.0.x [/usr/share/dotnet/shared/...]
```

Both `AspNetCore.App` and `NETCore.App` appearing confirms the SDK and runtimes installed correctly.

---

