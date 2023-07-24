# windows
7steps by manually install

1. install `windows terminal` at microsoft store in GUI

2. install font `Cica`
https://github.com/miiton/Cica

3. install `Gow`
https://github.com/bmatzelle/gow/releases/tag/v0.8.0

4. install `chocolately`
run below command in PowerShell used by admin
```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

5. install `deno`
run below command in PowerShell used by admin
```
choco install deno
```

6. install `Rust` tool chain
https://www.rust-lang.org/ja/tools/install
:::tips
automatically installed `Visual Studio`
:::

7. install `MinGW`
ref:
    https://dianxnao.com/windows%E3%81%ABc%E8%A8%80%E8%AA%9E%E9%96%8B%E7%99%BA%E7%92%B0%E5%A2%83-mingw-w64%EF%BC%88gcc%E3%82%B3%E3%83%B3%E3%83%91%E3%82%A4%E3%83%A9%EF%BC%89%E3%82%92%E5%B0%8E%E5%85%A5%E3%81%99%E3%82%8B/
downloads:
    https://www.mingw-w64.org/downloads/
    access to `SourceForge`

8. install `neovim`

9. setup GitHub settings
* add `~/.gitconfig` below lines
```
[user]
	name = nikekukuri
	email = nikekukuri0327@gmail.com
[core]
	editor = nvim
[init]
	defaultBranch = main
```
* generate and add SSH key

10. install scoop
```
iwr -useb get.scoop.sh | iex
```

11. install PowerShell v7
```
winget search Microsoft.PowerShell
winget install --id Microsoft.Powershell --source winget
winget install --id Microsoft.Powershell.Preview --source winget
```
When you run new terminal on Windows Terminal, always run PowerShell7
`C:\Program Files\PowerShell\7-preview\pwsh.exe`

12. oh-my-posh install
```
winget install JanDeDobbeleer.OhMyPosh -s winget
```

12. install utilities
```
scoop install zoxide fzf ripgrep fd gzip less tar gawk sed nodejs unzip gcc
scoop install uutils-coreutils
scoop install sudo
scoop install nvs
scoop bucket add github-gh https://github.com/cli/scoop-gh.git
scoop install gh
cargo install --git https://github.com/skyline75489/exa --branch chesterliu/dev/win-support
Install-Module -Scope CurrentUser PSFzf
Install-Module posh-git -Scope CurrentUser
```

# mac / linux
1. install zsh
2. install neovim
3. install ...
