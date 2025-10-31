# AutoZone Getting Started with Claude Code

Welcome to AutoZone! This comprehensive guide walks you through setting up Claude Code with Google Vertex AI integration. You'll learn how to install all required tools, configure your Google Cloud environment, and get Claude Code running on Windows (WSL2), Linux, or macOS.

**What you'll accomplish:**
- ✅ Install Claude Code CLI on your system
- ✅ Configure Google Vertex AI for Claude model access
- ✅ Set up authentication and environment variables
- ✅ Run your first AI-powered coding session
- ✅ Learn common workflows and troubleshooting

**Time to complete:** 30-45 minutes (including Google Cloud setup)

---

## ✅ Quick Start Checklist

Track your progress through the setup process:

### Prerequisites
- [ ] **Google Cloud Account** with billing enabled
- [ ] **Platform requirements** met (WSL2/Linux/macOS)
- [ ] **Terminal access** available

### Installation
- [ ] **Node.js 20 LTS** installed and verified (`node --version`)
- [ ] **Google Cloud SDK** installed (`gcloud --version`)
- [ ] **Claude Code CLI** installed (`claude --version`)
- [ ] PATH configured correctly for all tools

### Google Vertex AI Configuration
- [ ] **Authenticated** with Google Cloud (`gcloud auth login`)
- [ ] **Project ID** configured (`gcloud config set project`)
- [ ] **Vertex AI API** enabled in your project
- [ ] _(Claude model access and IAM permissions managed by AutoZone)_

### Environment Setup
- [ ] **Environment variables** configured in `~/.bashrc` or `~/.zshrc`
- [ ] **CLAUDE_CODE_USE_VERTEX=1** set
- [ ] **CLOUD_ML_REGION=us-east5** configured
- [ ] **ANTHROPIC_VERTEX_PROJECT_ID** configured
- [ ] Shell reloaded to apply changes

### Verification
- [ ] **First Claude Code session** started successfully
- [ ] **Connection to Vertex AI** confirmed
- [ ] **Basic commands** tested (/help, /status)

**All checked? You're ready to build with Claude Code and Vertex AI!** 🚀

---

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Google Vertex AI Setup](#google-vertex-ai-setup)
- [First-Time Configuration](#first-time-configuration)
- [Getting Started with Claude Code](#getting-started-with-claude-code)
- [Common Workflows](#common-workflows)
- [Troubleshooting](#troubleshooting)
- [Additional Resources](#additional-resources)

---

## Prerequisites

### All Platforms
- **Google Cloud Account** with billing enabled
- **Project access** to Vertex AI with Claude models (managed by AutoZone)
- **Terminal/Command Line** access
- **Internet connection** for downloading installers

### Platform-Specific Requirements

#### Windows (WSL2)
- Windows 10 version 2004+ or Windows 11
- WSL2 installed and configured
- Ubuntu 20.04 or 22.04 recommended

**Install WSL2 (if not installed):**
```powershell
# Run in PowerShell as Administrator
wsl --install
```

#### Linux
- Ubuntu 20.04+, Debian 11+, Fedora 35+, or equivalent
- curl or wget installed
- bash shell

#### macOS
- macOS 11 (Big Sur) or later
- Terminal access (Terminal.app or iTerm2)

---

## Installation

### Step 1: Install Node.js and npm

#### Windows (WSL2)

**Recommended: Using NodeSource repository**
```bash
# Add NodeSource repository (Node.js 20 LTS)
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs

# Verify installation
node --version  # Should show v20.x.x
npm --version
```

**Alternative: Using nvm (Node Version Manager)**
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc
nvm install 20
nvm use 20
```

#### Linux (Ubuntu/Debian)

**Recommended: Using NodeSource repository**
```bash
# Add NodeSource repository (Node.js 20 LTS)
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs

# Verify installation
node --version  # Should show v20.x.x
npm --version
```

#### macOS

**Recommended: Using Homebrew**
```bash
# Install Homebrew if not already installed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Node.js 20 LTS
brew install node@20

# Verify installation
node --version  # Should show v20.x.x
npm --version
```

**Alternative: Official Installer**
1. Download from [nodejs.org](https://nodejs.org/) (LTS version 20.x)
2. Run the `.pkg` installer
3. Verify: `node --version && npm --version`

**Node.js is now ready - proceed to Step 2!**

### Step 2: Install Google Cloud SDK

#### Windows (WSL2) & Linux
```bash
# Add Cloud SDK distribution URI
echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list

# Import Google Cloud public key
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -

# Update and install
sudo apt-get update && sudo apt-get install google-cloud-cli

# Verify installation
gcloud --version
```

#### macOS
```bash
# Download and install Google Cloud SDK
curl https://sdk.cloud.google.com | bash

# Restart shell to apply changes
exec -l $SHELL

# Or restart terminal, then verify
gcloud --version

# Initialize gcloud
gcloud init
```

**Alternative**: Download the [interactive installer](https://cloud.google.com/sdk/docs/install) from Google Cloud.

### Step 3: Install Claude Code

#### Windows (WSL2)

**Recommended: NPM Installation**
```bash
# Inside WSL2 terminal
npm install -g @anthropic-ai/claude-code

# Verify installation
claude --version
```

#### Linux

**Recommended: Native Installer**
```bash
# Official installer - automatically configures PATH
curl -fsSL https://claude.ai/install.sh | bash

# Verify installation
claude --version
```

**Alternative: NPM Installation**
```bash
# If you prefer npm or have PATH issues with native installer
npm install -g @anthropic-ai/claude-code
claude --version
```

#### macOS

**Recommended: Native Installer**
```bash
# Official installer - automatically configures PATH
curl -fsSL https://claude.ai/install.sh | bash

# Verify installation
claude --version
```

**Alternative: NPM Installation**
```bash
# If you prefer npm or have PATH issues with native installer
npm install -g @anthropic-ai/claude-code
claude --version
```

---

### Installation Notes

**Native Installer Benefits:**
- ✅ Automatic PATH configuration
- ✅ Native binary optimized for your platform
- ✅ Fastest installation (30 seconds)
- ✅ Recommended by Anthropic for macOS/Linux

**NPM Installation Benefits:**
- ✅ Works on all platforms
- ✅ Consistent with npm-based workflow
- ✅ Easy updates: `npm update -g @anthropic-ai/claude-code`
- ✅ Recommended by Anthropic for Windows

**AutoZone Recommendation:** While native installers are generally recommended for macOS/Linux, you may prefer NPM for consistency across your entire development environment since Node.js 20 is already installed.

---

### Troubleshooting Claude Code Installation

#### PATH Issues with NPM Installation

If `claude` command is not found after npm installation:

**Linux/WSL2:**
```bash
# Add npm global bin to PATH
echo 'export PATH="$(npm config get prefix)/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

**macOS:**
```bash
# Add npm global bin to PATH
echo 'export PATH="$(npm config get prefix)/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

Verify npm global bin location:
```bash
npm config get prefix
# Should show something like /usr/local or /Users/username/.npm-global
```

#### Updating Claude Code

**If installed via native installer:**
```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**If installed via npm:**
```bash
npm update -g @anthropic-ai/claude-code
```

---

## Google Vertex AI Setup

### Step 1: Authenticate with Google Cloud

```bash
# Login to Google Cloud
gcloud auth login

# Set up application default credentials
gcloud auth application-default login

# Set your project ID
gcloud config set project YOUR-PROJECT-ID
```

### Step 2: Enable Required APIs

```bash
# Enable Vertex AI API
gcloud services enable aiplatform.googleapis.com

# Verify API is enabled
gcloud services list --enabled | grep aiplatform
```

**Note:** Claude model access, quotas, and IAM permissions are managed by AutoZone. You don't need to request access or configure permissions - your account is already set up.

---

## First-Time Configuration

### Step 1: Set Environment Variables

Create or edit `~/.bashrc` (Linux/WSL2) or `~/.zshrc` (macOS):

```bash
# Open config file
nano ~/.bashrc  # Linux/WSL2
# or
nano ~/.zshrc   # macOS

# Add these environment variables
set CLAUDE_CODE_USE_VERTEX=1
set CLOUD_ML_REGION=us-east5
set ANTHROPIC_VERTEX_PROJECT_ID=your-az-vertex-project-id

source ~/.bashrc  # or source ~/.zshrc
```

### Step 2: Verify Configuration

```bash
# Check environment variables
echo $CLAUDE_CODE_USE_VERTEX
echo $ANTHROPIC_VERTEX_PROJECT_ID

# Test gcloud authentication
gcloud auth list

## Getting Started with Claude Code

# Navigate to your project directory
cd ~/projects/my-project

# Start Claude Code (makes sure your in Node 18+)
claude
```

You'll see an interactive prompt. Since you're using Vertex AI, you won't need to login with Anthropic credentials.

```

### Built-in Slash Commands

Inside Claude Code, try these commands:

```
/help          - Show all available commands
/status        - Check configuration and model status
/model         - Switch between available models
/settings      - View current settings
/context       - Show current context size
/cost          - View estimated costs
/clear         - Clear conversation history
/exit          - Exit Claude Code
```

---
```
## Additional Resources

### Official Documentation
- **Claude Code Docs**: https://docs.claude.com/en/docs/claude-code
- **Vertex AI Docs**: https://cloud.google.com/vertex-ai/docs
- **Model Garden**: https://console.cloud.google.com/vertex-ai/model-garden

### Useful Commands Cheat Sheet
```bash
# Start Claude Code
claude                                    # Interactive mode

# Google Cloud
gcloud auth login                        # Authenticate
gcloud config set project PROJECT-ID    # Set project
gcloud services list --enabled          # Check enabled APIs

# Environment
set CLAUDE_CODE_USE_VERTEX=1
set CLOUD_ML_REGION=us-east5
set ANTHROPIC_VERTEX_PROJECT_ID=your-az-vertex-project-id
source ~/.bashrc  # or ~/.zshrc

# Updates
claude update                            # Update Claude Code
gcloud components update                 # Update Google Cloud SDK
npm update -g                            # Update all global npm packages
npm install -g npm@latest               # Update npm itself
```
### Getting Help

**Claude Code Issues:**
- GitHub Issues: https://github.com/anthropics/claude-code/issues
- Documentation: https://docs.claude.com/en/docs/claude-code

**Vertex AI Issues:**
- Google Cloud Support: https://cloud.google.com/support
- Community: https://www.googlecloudcommunity.com/

**In-Session Help:**
```bash
# Inside Claude Code
/help          # Show all commands
/doctor        # Run diagnostics
/status        # Check configuration
```

---


---

*Last Updated: October 31, 2025*
*For AutoZone - Claude Code with Google Vertex AI*
