
#nixos #nix 

The file `/etc/nixos/configuration.nix` contains the current configuration of your machine. Whenever you've changed something in that file, you should do:

```
nixos-rebuild switch --use-remote-sudo
```

to build the new configuration as your current user, and as the root user, make it the default configuration for booting. `switch` will also try to realize the configuration in the running system (e.g. by restarting system services).

You can also do

```
nixos-rebuild test --use-remote-sudo
```

to build the configuration and switch the running system to it, but without making it the boot default. So if the configuration locks up your machine, you can just reboot to get back to a working configuration.

