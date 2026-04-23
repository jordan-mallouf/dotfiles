# Dotfiles for macOS

Welcome to my personal dotfiles repository!
This repo contains my curated configuration files, shell customizations, and automation scripts for a productive, beautiful, and secure macOS development environment.

## Features

- **Zsh & Oh My Zsh**: Powerlevel10k theme and syntax highlighting for a fast, informative prompt.
- **Custom Login Experience**: Personalized welcome message, Apple logo, and neofetch system info on every terminal launch.
- **Security**: Sensitive directories like `.ssh/` are never tracked. `.hushlogin` suppresses noisy login messages.
- **Copilot Agent Configs**: All my GitHub Copilot agent and instruction files are tracked for reproducibility and sharing.

## Directory Structure

```
.
├── .zshrc                  # Zsh configuration
├── .zprofile               # Zsh profile
├── .p10k.zsh               # Powerlevel10k theme config
├── .vimrc                  # Vim configuration
├── .hushlogin              # Suppress 'Last login' message
├── .oh-my-zsh/             # Oh My Zsh framework
├── .copilot/
│   ├── agents/             # Copilot agent definitions
│   └── copilot-instructions.md # Copilot instructions
└── ...                     # Other macOS user folders (ignored)
```

## Setup Instructions

1. **Clone the repo to your home directory:**
	```bash
	git clone --bare https://github.com/jordan-mallouf/dotfiles.git $HOME/.dotfiles
	alias dotfiles='/usr/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
	dotfiles checkout
	```

2. **Install dependencies:**
	- [Oh My Zsh](https://ohmyz.sh/)
	- [Powerlevel10k](https://github.com/romkatv/powerlevel10k)
	- [neofetch](https://github.com/dylanaraps/neofetch)
	- [lolcat](https://github.com/busyloop/lolcat)
	- [figlet](http://www.figlet.org/)

3. **Customize as needed:**
	- Edit `.zshrc` for zsh core tweaks and adjustments.
    - Edit `.p10k.zsh` for prompt and terminal aesthetic changes. 

## Security & Privacy

- `.ssh/`, `.Trash/`, and other sensitive or transient files are ignored by default.
- Only safe, shareable configuration is tracked.