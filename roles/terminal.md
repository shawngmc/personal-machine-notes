# Terminal

## Tooling
### Terminal Emulator
[Tabby](https://) is my terminal of choice.
- GPU Acceleration
- Sixel Image support
- Global Hotkey (Ctrl-Space)

### Prompt
Liquidprompt seems just faster...
- Powerline theme
- More active development
- Just clone a git repo

### Editor
Neovim is just a better vim.

### Other Tools
- fzf: command line search tool
- gh-cli: Easier GH access, especially downloading release artifacts
- htop: Just a better top
- jq: JSON query tool; use with fzf for interactive
- libsixel-utils: Image preview on the CLI
- python3-pip: Just have a pip for the default python
- testssl: useful for debugging TLS servers
- yq: YAML query tool

## Installation
### GH-CLI
```
# Use their repo - released often
sudo dnf install -y dnf5-plugins
sudo dnf config-manager addrepo --from-repofile=https://cli.github.com/packages/rpm/gh-cli.repo
sudo dnf install -y git 
sudo dnf install -y gh --repo gh-cli
# Login (interactive)
gh auth login
```

### Tabby
```
# Download the latest RPM
gh release download -R Eugeny/tabby --pattern tabby*linux-x64.rpm
# Install
sudo dnf install -y tabby*linux-x64.rpm
# Cleanup
rm -rf tabby*linux-x64.rpm
# Install img2sixel to see images on command line
sudo dnf install -y libsixel-utils
```

### Liquidprompt
```
# Clone
git clone --branch stable https://github.com/liquidprompt/liquidprompt.git ~/liquidprompt
# Install in .bashrc.d
mkdir -pv ~/.bashrc.d/
cat << EOF > ~/.bashrc.d/liquidprompt.sh
#!/bin/bash
# Only load Liquid Prompt in interactive shells, not from a script or from scp
if [[ "$-" == *i* ]]; then
  source ~/liquidprompt/liquidprompt
  source ~/liquidprompt/themes/powerline/powerline.theme
  lp_theme powerline
fi
EOF
```

### Neovim
```
sudo dnf install -y neovim
# Set neovim as default editor
sudo alternatives --install /usr/bin/editor nvim /bin/nvim 1
# Use neovim for vi/vim
mkdir -pv ~/.bashrc.d/
cat << EOF > ~/.bashrc.d/neovim.sh
#!/bin/bash
alias vim='nvim'
alias vi='nvim'
EOF
# Ensure I have PIP, then install python support
sudo dnf install -y python3-pip
python3 -m pip install --user --upgrade pynvim
```


### Other stuff
```
sudo dnf install -y htop testssl jq yq fzf
# Add jq-repl
mkdir -pv ~/.local/bin
cat << "EOF" > ~/.local/bin/jq-repl
#!/usr/bin/env bash
if [[ -z $1 ]] || [[ $1 == "-" ]]; then
    input=$(mktemp)
    trap "rm -f $input" EXIT
    cat /dev/stdin > $input
else
    input=$1
fi

echo '' \
    | fzf --phony \
          --preview-window='up:90%' \
          --print-query \
          -q . \
          --preview "jq --color-output -r {q} $input" 
EOF
chmod +x ~/.local/bin/jq-repl

cat << "EOF" > ~/.local/bin/yq-repl
#!/usr/bin/env bash
if [[ -z $1 ]] || [[ $1 == "-" ]]; then
    input=$(mktemp)
    trap "rm -f $input" EXIT
    cat /dev/stdin > $input
else
    input=$1
fi

echo '' \
    | fzf --phony \
          --preview-window='up:90%' \
          --print-query \
          -q . \
          --preview "yq -C -r {q} $input" 
EOF
chmod +x ~/.local/bin/yq-repl
```