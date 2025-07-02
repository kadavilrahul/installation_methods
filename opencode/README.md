Refernce: 
https://github.com/sst/opencode
https://opencode.ai/docs/

## Install Opencode 
```bash
curl -fsSL https://opencode.ai/install | bash
```

## Start commands:
List of commands:

- ``opencode --help``

- ``opencode --version``

- ``opencode run [message..]``

- ``opencode auth login``

- ``opencode auth logout``

- ``opencode auth list``

- ``opencode [project]``

- ``opencode upgrade [target]``

- ``opencode upgrade``

- ``opencode serve``

- ``opencode models``













## Commands
The opencode CLI also has the following commands.

### run
Run opencode in non-interactive mode by passing a prompt directly.
```bash
opencode run [message..]
```
This is useful for scripting, automation, or when you want a quick answer without launching the full TUI. For example.
```bash
opencode run Explain the use of context in Go
```
Flags
Flag	Short	Description
--continue	-c	Continue the last session
--session	-s	Session ID to continue
--share		Share the session
--model	-m	Mode to use in the form of provider/model

