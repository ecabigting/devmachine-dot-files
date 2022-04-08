# Config

 - Install starship from [here](http://starship.rs/guide/#-installation)
 - Create a `starship.toml` file in `~/.config`, copy the content from [here](/starship.toml)
 - Install Meslo Nerd Fonts
    > For `xterm` get it from [here](/Fonts/xterm/)
    > For `vscode` get from [here](/Fonts/vscode/)
 - Open `~/.Xresources` and change the font for **xterm** to this: `XTerm*faceName:          MesloLGS NF`
 - Open `vscode` and set the terminal font by opening _Settings ->_ **search: terminal font** and set the value to `MesloLGL Nerd Font`

# Installing `dotnet`

- Download `dotnet-install.sh` from [here](https://dot.net/v1/dotnet-install.sh)
- Run the following command:
```bash
bash ./dotnet-install.sh --install-dir /usr/share/dotnet -channel Current -version latest
```
- Add the it to the PATH of your shell, for `zsh` open `~/.zshrc` and add the following line:

```bash
export PATH="$PATH:/usr/share/dotnet"
```

# Installing `npm`

We need to install `nvm` first.

Run the following commands:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | zsh
```

## Installing `npm` using `nvm`

To install npm run the following command:

```bash
nvm install --lts
```

Check the installed version using the following 

Check `npm` version
```bash
nvm --version
```

Check `node` version
```bash
node --version
```

Check `nvm` version
```bash
nvm --version
```

