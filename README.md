# Dotfiles

Personal macOS dotfiles for development environment configuration.

## 📋 Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Synchronization](#synchronization)
- [What Gets Synced](#what-gets-synced)
- [Scripts](#scripts)
- [Customization](#customization)

## ✨ Features

- **Shell Configuration**: Bash profile, aliases, exports, and custom prompt
- **Git Configuration**: Global gitconfig, gitignore, and gitattributes
- **Cursor IDE**: Settings, keybindings, and extensions syncing
- **iTerm2**: Profile configuration
- **Package Management**: Automated installation via Homebrew
- **macOS Defaults**: Custom system preferences

## 🔧 Prerequisites

- macOS (tested on darwin 25.1.0)
- [Homebrew](https://brew.sh/) installed
- Git

## 🚀 Installation

### First Time Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/dotfiles.git ~/dvp/dotfiles
   cd ~/dvp/dotfiles
   ```

2. **Run the dotfiles installer**
   ```bash
   ./bin/dotfiles
   ```
   
   This script will:
   - Update Homebrew and install required packages
   - Install desired applications via Homebrew casks
   - Install NVM (Node Version Manager)
   - Install Cursor command in PATH
   - Create symlinks to configuration files
   - Sync Cursor settings and keybindings

## 🔄 Synchronization

### Syncing Configuration to a New Machine

When setting up a new machine with your dotfiles:

```bash
cd ~/dvp/dotfiles
git pull origin master
./bin/dotfiles
```

### Syncing Cursor Extensions

**To install extensions from the dotfiles:**
```bash
./bin/cursor-sync-extensions
```

This will:
- Install missing extensions from `.cursor-extensions.txt`
- Remove extensions not in the list (to keep your setup clean)

**To update the extension list after installing new extensions:**
```bash
./bin/cursor-export-extensions
git add cursor/.cursor-extensions.txt
git commit -m "Update Cursor extensions"
git push
```

### Updating Configuration Files

After making changes to your local configuration:

1. **Edit files in the dotfiles directory:**
   ```bash
   cd ~/dvp/dotfiles
   # Edit your files (e.g., shell/bash_aliases, cursor/settings.json, etc.)
   ```

2. **Commit and push changes:**
   ```bash
   git add .
   git commit -m "Update configuration"
   git push origin master
   ```

3. **On other machines, pull and sync:**
   ```bash
   cd ~/dvp/dotfiles
   git pull origin master
   ./bin/dotfiles  # Re-run to update symlinks
   ./bin/cursor-sync-extensions  # Sync extensions
   ```

## 📦 What Gets Synced

### Shell Configuration
- `.bashrc` → `shell/bashrc`
- `.bash_profile` → `shell/bash_profile`
- `.bash_aliases` → `shell/bash_aliases`
- `.bash_exports` → `shell/bash_exports`
- `.bash_prompt` → `shell/bash_prompt`
- `.curlrc` → `shell/curlrc`
- `.inputrc` → `shell/inputrc`

### Git Configuration
- `.gitconfig` → `git/gitconfig`
- `.gitignore` → `git/gitignore`
- `.gitattributes` → `git/gitattributes`

### Cursor IDE
- `settings.json` → `cursor/settings.json`
- `keybindings.json` → `cursor/keybindings.json`
- Extensions list → `cursor/.cursor-extensions.txt`

### Homebrew Packages

**Formulae:**
- git
- bash
- bash-completion
- tree
- wget

**Casks (Applications):**
- Cursor (IDE)
- iTerm2 (Terminal)
- Rectangle (Window manager)
- AltTab (Window switcher)
- Jumpcut (Clipboard manager)
- Gather (Video conferencing)

## 🛠 Scripts

### `bin/dotfiles`
Main installation script that sets up your entire development environment.

### `bin/cursor-sync-extensions`
Syncs Cursor extensions based on the list in `cursor/.cursor-extensions.txt`.
- Installs missing extensions
- Removes extensions not in the list

### `bin/cursor-export-extensions`
Exports your currently installed Cursor extensions to `cursor/.cursor-extensions.txt`.

### `bin/osxdefaults`
Applies custom macOS system preferences (run manually).

### `bin/aws-sso-login`
Helper script for AWS SSO authentication.

### `bin/codecopy`
Utility for copying code with formatting.

## 🎨 Customization

### Adding New Bash Aliases

Edit `shell/bash_aliases`:
```bash
alias myalias='my command'
```

### Adding Environment Variables

Edit `shell/bash_exports`:
```bash
export MY_VAR="value"
```

### Adding Homebrew Packages

Edit `bin/dotfiles` and add to the arrays:
```bash
local -a desired_formulae=(
    'git'
    'bash'
    'your-new-package'
)

local -a desired_casks=(
    'cursor'
    'your-new-app'
)
```

### Modifying Cursor Settings

Edit `cursor/settings.json` or `cursor/keybindings.json` directly in the dotfiles repo.

## 🔗 Workflow Example

**Setting up a new machine:**
```bash
# 1. Clone dotfiles
git clone https://github.com/yourusername/dotfiles.git ~/dvp/dotfiles

# 2. Install everything
cd ~/dvp/dotfiles
./bin/dotfiles

# 3. Sync Cursor extensions
./bin/cursor-sync-extensions
```

**After installing a new Cursor extension:**
```bash
# 1. Export extensions
./bin/cursor-export-extensions

# 2. Commit and push
cd ~/dvp/dotfiles
git add cursor/.cursor-extensions.txt
git commit -m "Add new Cursor extension"
git push
```

**Updating configuration on another machine:**
```bash
# Pull latest changes
cd ~/dvp/dotfiles
git pull

# Sync everything
./bin/dotfiles
./bin/cursor-sync-extensions
```

## 📝 Notes

- The dotfiles directory is expected to be at `~/dvp/dotfiles`
- Existing files are backed up with a `.backup` extension before being replaced
- Symlinks are used for most configuration files (changes are reflected immediately)
- `.gitconfig` is copied (not symlinked) to allow machine-specific overrides

## 🤝 Contributing

Feel free to fork and customize for your own use!

## 📄 License

Free to use and modify as needed.

