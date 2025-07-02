Refernce: 
https://github.com/sst/opencode
https://opencode.ai/docs/

Install Opencode 
Command to install on Linux:
curl -fsSL https://opencode.ai/install | bash

Start commands:
opencode --help
opencode --version 
opencode run [message..]   run opencode with a message
opencode auth login   log in to a provider
opencode auth logout  log out from a configured provider
opencode auth list    list providers   
opencode [project]         start opencode tui [default]
opencode upgrade [target]  upgrade opencode to the latest or a specific version
opencode upgrade           upgrade opencode to the latest
opencode serve             starts a headless opencode server
opencode models            list all available models

Run commands
Running the opencode CLI starts it for the current directory.
opencode
Or you can start it for a specific working directory.
opencode /path/to/project
Commands
The opencode CLI also has the following commands.

run
Run opencode in non-interactive mode by passing a prompt directly.
opencode run [message..]
This is useful for scripting, automation, or when you want a quick answer without launching the full TUI. For example.
opencode run Explain the use of context in Go
Flags
Flag	Short	Description
--continue	-c	Continue the last session
--session	-s	Session ID to continue
--share		Share the session
--model	-m	Mode to use in the form of provider/model

