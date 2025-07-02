Refernce: 
https://github.com/sst/opencode
https://opencode.ai/docs/

## Install Opencode 
```bash
curl -fsSL https://opencode.ai/install | bash
```

## Start commands:
List of commands:

<details>
<summary>opencode --help</summary>

```bash
opencode --help
```
</details>

<details>
<summary>opencode --version</summary>

```bash
opencode --version
```
</details>

<details>
<summary>opencode run [message..]</summary>

```bash
opencode run [message..]
```
</details>

<details>
<summary>opencode auth login</summary>

```bash
opencode auth login
```
</details>

<details>
<summary>opencode auth logout</summary>

```bash
opencode auth logout
```
</details>

<details>
<summary>opencode auth list</summary>

```bash
opencode auth list
```
</details>

<details>
<summary>opencode [project]</summary>

```bash
opencode [project]
```
</details>

<details>
<summary>opencode upgrade [target]</summary>

```bash
opencode upgrade [target]
```
</details>

<details>
<summary>opencode upgrade</summary>

```bash
opencode upgrade
```
</details>

<details>
<summary>opencode serve</summary>

```bash
opencode serve
```
</details>

<details>
<summary>opencode models</summary>

```bash
opencode models
```
</details>












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

