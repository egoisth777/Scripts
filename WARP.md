# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Repository Overview

This is a collection of personal automation scripts and configurations organized as Git submodules. The repository serves as a centralized hub for managing various Windows automation tools, editor configurations, and development environment setup scripts.

## Architecture & Structure

The repository follows a modular architecture using Git submodules, where each component is maintained as a separate repository:

- **Opus-Scripts**: Directory Opus user commands (`.ouc` files) for file manager automation
- **Win-Automation**: Windows-specific automation scripts and utilities  
- **AHK-Scripts**: AutoHotkey v2 scripts for keyboard remapping and Windows automation
- **Configs**: System configuration files including PowerShell modules, Chocolatey packages, and environment setup
- **Nvim-Config**: LazyVim/Lazy.nvim configuration for Neovim

Each submodule can be developed and deployed independently while being managed collectively through the main repository.

## Common Development Commands

### Repository Management
```powershell
# Initialize and update all submodules
git submodule update --init --recursive

# Pull latest changes for all submodules
git submodule update --remote --recursive

# Commit and push changes across all submodules (Windows)
.\commitSubmodules.ps1 "Your commit message"

# Commit and push changes across all submodules (Unix-like)
./commitSubmodules.sh "Your commit message"
```

### Working with Individual Submodules
```powershell
# Navigate to a specific submodule
cd Opus-Scripts
# or cd Win-Automation, AHK-Scripts, Configs, Nvim-Config

# Work with the submodule as a normal Git repository
git add .
git commit -m "Update script"
git push
```

### Environment Setup (Windows)
```powershell
# Bootstrap new environment (requires Administrator privileges)
cd Configs
.\bootstrap.ps1

# Individual setup scripts
.\clonerepos.ps1       # Clone additional repositories
.\installsoftware.ps1  # Install software via Chocolatey
.\setglobenv.ps1       # Set environment variables
.\setsymlink.ps1       # Create symbolic links
```

## Development Workflow

### Submodule Development Pattern
1. Each submodule maintains its own development lifecycle
2. Changes are committed to individual submodule repositories first
3. The main repository tracks specific commits of each submodule
4. Use `commitSubmodules.ps1` or `commitSubmodules.sh` to batch-commit across all submodules

### Cross-Platform Compatibility
- PowerShell scripts are designed for Windows environments
- Shell scripts (`.sh`) provide Unix-like compatibility where applicable
- AHK scripts are Windows-specific automation tools

### Configuration Management
The `Configs` submodule serves as the central configuration hub:
- PowerShell profile and module management
- Chocolatey package definitions
- Environment variable setup
- Symbolic link creation for dotfiles

### Automation Scripts
- **Opus-Scripts**: Context menu commands for Directory Opus (file manager integration)
- **AHK-Scripts**: System-wide keyboard remapping and automation
- **Win-Automation**: General Windows automation utilities

## Environment Variables

The repository expects and creates several environment variables:
- `SCRIPTS`: Points to the main Scripts directory
- `GIT_LOC`: Points to Git installation directory
- `YAZI_FILE_ONE`: Points to file.exe for YAZI integration
- Obsidian and cloud drive related variables (configured in setglobenv.ps1)

## Important Notes

### Prerequisites
- PowerShell 7.x required for bootstrap scripts
- Administrator privileges needed for environment setup
- Git with SSH keys configured for submodule access
- Drive E: expected for repository storage (configurable)

### Submodule Management
- Always commit changes to submodules before updating the main repository
- The main repository tracks specific commit hashes of submodules
- Use the provided batch commit scripts to maintain consistency across submodules

### Windows-Specific Features
- AutoHotkey scripts require AHK v2.0
- Directory Opus commands integrate with the file manager
- PowerShell modules provide cross-session functionality
