# Config

 - Install starship from [here](http://starship.rs/guide/#-installation)
 - Create a `starship.toml` file in `~/.config`, copy the content from [here](/starship.toml)
 - Install Meslo Nerd Fonts
    > For `xterm` get it from [here](/Fonts/xterm/)
    > For `vscode` get from [here](/Fonts/vscode/)
 - Open `~/.Xresources` and change the font for **xterm** to this: `XTerm*faceName:          MesloLGS NF`
 - Open `vscode` and set the terminal font by opening _Settings ->_ **search: terminal font** and set the value to `MesloLGL Nerd Font`

# Installing `dotnet` on `linux`

- Download `dotnet-install.sh` from [here](https://dot.net/v1/dotnet-install.sh)
- Run the following command:
```bash
bash ./dotnet-install.sh --install-dir /usr/share/dotnet -channel Current -version latest
```
- Add the it to the PATH of your shell, for `zsh` open `~/.zshrc` and add the following line:

```bash
export PATH="$PATH:/usr/share/dotnet"
```

- You need to add a symbolic for dotnet, run the following command to do so:

```bash
sudo ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet
```
Where `/usr/share/dotnet/` in the command is the path and the additional `dotnet` is the `executable`


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

## Configuring Arch Linux in VMware Player

### Missing screen resolution

If you cannot find the correct screen resolution on your guest Arch Linux using VMware, run the following steps.

Install `open-vm-tools`

```bash
sudo pacman open-vm-tools
```

Lets add the missing resolution:

Run the following command to get the resolution you want
```bash
cvt 2560 1080 60
```
The command above will show the screen resolution of `2560` by `1080` on `60hz`

You should get something like this
```bash
Modeline "2560x1080_60.00"  230.00  2560 2720 2992 3424  1080 1083 1093 1120 -hsync +vsync
```

Now run the following command to add a new mode
```bash
xrandr --newmode "2560x1080_60.00"  230.00  2560 2720 2992 3424  1080 1083 1093 1120 -hsync +vsync
```

Now we need to add the new mode to `xrandr` using the following command
```bash
xrandr --addmode Virtual1 2560x1080_60.00
```
Where `Virtual1` is your monitor and `2560x1080` is the screen mode you want to use

Last step is to add the following modules to `mkinicpio.conf`

Edit `/etc/mkinitcpio.conf` and replace `MODULES=""` with
```bash
MODULES=(vsock vmw_vsock_vmci_transport vmw_balloon vmw_vmci vmgfx)
```

Restart your machine and you should get the resolution, you set, `PRO TIP: force VMware to fullscreen`

### Enabling Shared folders 

Adding shared folder from `Host` to be accessible in the `guest` machine. 

- Make sure from VMware player under __Settings -> Options -> Shared folder__. Select the folder you want to share with the guest machine.

- Create a folder in your `Guest`. For example `/home/stifmiester/Shared`

- Mount the folder from `Host` to the folder your created in your `Guest`
```bash
/usr/bin/vmhgs-fuse -o auto_unmount,allow_other .host:/ /home/stifmiester/Shared
```

- Next is to update your `/etc/fstab`
```bash
sudo nano /etc/fstab
```

Add the the following code to the end of the file
```bash
.host:/ /home/stifmiester/Shared fuse.vmhgfs-fuse defaults,allow_other 0 0
```

