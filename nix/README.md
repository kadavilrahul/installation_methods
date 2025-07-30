# Nix Package Manager Guide

## Installation

### Multi-user Installation (Recommended)
```bash
curl -L https://nixos.org/nix/install | sh -s -- --daemon
```

**What this does:**
- Creates 32 build users (nixbld1-nixbld32) with UIDs 30001-30032
- Creates nixbld group (GID 30000)
- Installs Nix in `/nix` directory
- Sets up systemd daemon service
- Configures shell profiles for all users

### Post-Installation
After installation, restart your shell or source the profile:
```bash
source /nix/var/nix/profiles/default/etc/profile.d/nix-daemon.sh
```

## Basic Commands

### Package Management

#### Search for packages
```bash
nix search nixpkgs firefox
nix search nixpkgs python
```

#### Install packages temporarily (development shell)
```bash
nix-shell -p firefox git vim
nix-shell -p python3 nodejs
```

#### Install packages permanently (legacy method)
```bash
nix-env -iA nixpkgs.firefox
nix-env -iA nixpkgs.git
```

#### Install packages permanently (modern flakes method)
```bash
nix profile install nixpkgs#firefox
nix profile install nixpkgs#git
```

#### List installed packages
```bash
nix-env -q --installed
nix profile list
```

#### Remove packages
```bash
nix-env -e firefox
nix profile remove firefox
```

#### Update packages
```bash
nix-env -u
nix profile upgrade
```

### System Management

#### Update channel
```bash
nix-channel --update
```

#### Garbage collection
```bash
nix-collect-garbage
nix-collect-garbage -d  # Delete old generations
```

#### List generations
```bash
nix-env --list-generations
```

#### Rollback to previous generation
```bash
nix-env --rollback
```

## Configuration Files

### Main config: `/etc/nix/nix.conf`
```
build-users-group = nixbld
experimental-features = nix-command flakes
```

### User channels: `~/.nix-channels`
```
https://nixos.org/channels/nixpkgs-unstable nixpkgs
```

### User config: `~/.config/nixpkgs/config.nix`
```nix
{
  allowUnfree = true;
}
```

## Flakes (Modern Approach)

### Enable flakes
Add to `/etc/nix/nix.conf`:
```
experimental-features = nix-command flakes
```

### Create a flake.nix
```nix
{
  description = "My development environment";
  
  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-unstable";
  };
  
  outputs = { self, nixpkgs }: {
    devShells.x86_64-linux.default = nixpkgs.legacyPackages.x86_64-linux.mkShell {
      buildInputs = with nixpkgs.legacyPackages.x86_64-linux; [
        nodejs
        python3
        git
      ];
    };
  };
}
```

### Use flake
```bash
nix develop  # Enter development shell
nix build    # Build the flake
```

## Migration from Other Systems

### Export current packages (for migration)
```bash
nix-env -q --installed > packages.txt
```

### Restore packages on new system
```bash
# Install Nix first, then:
while read package; do
  nix-env -iA nixpkgs.$package
done < packages.txt
```

### Copy Nix store (optional, saves bandwidth)
```bash
rsync -av /nix/ newserver:/nix/
```

## Useful Directories

- `/nix/store/` - Immutable package store
- `/nix/var/nix/profiles/` - User profiles and generations
- `/etc/nix/` - System configuration
- `~/.nix-profile/` - User profile symlink

## Troubleshooting

### Test installation
```bash
nix-shell -p nix-info --run "nix-info -m"
```

### Check daemon status
```bash
systemctl status nix-daemon
```

### Restart daemon
```bash
sudo systemctl restart nix-daemon
```

### Fix permissions
```bash
sudo chown -R root:nixbld /nix
sudo chmod 1775 /nix/store
```

## Benefits

1. **Reproducible builds** - Same package works identically everywhere
2. **Atomic upgrades/rollbacks** - Easy to revert changes
3. **No dependency conflicts** - Multiple versions coexist
4. **Declarative configuration** - Define system state in files
5. **Isolated environments** - Clean development shells

## Best Practices

1. Use flakes for new projects
2. Pin package versions for reproducibility
3. Regular garbage collection to save space
4. Use development shells instead of global installs
5. Keep configuration in version control

## Uninstallation

If you need to remove Nix:
```bash
sudo systemctl stop nix-daemon.socket
sudo systemctl stop nix-daemon.service
sudo systemctl disable nix-daemon.socket
sudo systemctl disable nix-daemon.service
sudo systemctl daemon-reload

# Remove users and group
for i in {1..32}; do
  sudo userdel nixbld$i
done
sudo groupdel nixbld

# Remove directories
sudo rm -rf /nix
sudo rm -rf /etc/nix
sudo rm /etc/profile.d/nix.sh
sudo rm /etc/systemd/system/nix-daemon.service
sudo rm /etc/systemd/system/nix-daemon.socket

# Restore shell configs
sudo mv /etc/bash.bashrc.backup-before-nix /etc/bash.bashrc
```