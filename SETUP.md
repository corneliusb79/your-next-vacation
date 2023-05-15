# Installing Packages

## Chocolatey

`[ADMIN]`

Run `Get-ExecutionPolicy`. If it returns Restricted, then run `Set-ExecutionPolicy AllSigned` or `Set-ExecutionPolicy Bypass -Scope` Process.

Now run the following command:

```ps
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

## NVM (Node Version Manager)

`[ADMIN]`

```ps
choco install nvm
```

## Node

```ps
nvm install 18
nvm use 18
```

## VSCode

`[ADMIN]`

```ps
choco install vscode
```

## Git

`[ADMIN]`

```ps
choco install git
```

## GitHub CLI

`[ADMIN]`

```ps
choco install gh
```

## GitHub Desktop

`[ADMIN]`

```ps
choco install github-desktop
```
