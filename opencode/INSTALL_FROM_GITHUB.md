# OpenCode Installation Guide

## Prerequisites
- Git
- curl
- unzip

## Installation Steps

1. Clone the repository:
```bash
git clone https://github.com/sst/opencode.git
cd opencode
```

2. Run the install script:
```bash
./install
```

3. Verify the installation:
```bash
~/.opencode/bin/opencode --version
```

4. Add to PATH (for current session):
```bash
source ~/.bashrc
```

5. Verify global availability:
```bash
opencode --version
```

## Permanent PATH Configuration

To make opencode permanently available, add this to your ~/.bashrc:
```bash
export PATH=$PATH:~/.opencode/bin
```

Then reload:
```bash
source ~/.bashrc
```

## Troubleshooting

If `opencode` command is not found:
- Check binary exists: `ls ~/.opencode/bin/opencode`
- Verify PATH: `echo $PATH`
- Ensure ~/.bashrc contains the PATH export