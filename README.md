# Noob_LazyVim
Нубский LazyVim
Используем WindowsTerminal (в Вин11 стоит по стандарту, на Вин10 можно скачать отдельно)
Обновляем PowerShell
winget install --id Microsoft.Powershell --source winget
Устанавливаем Nerd Font
https://github.com/ryanoasis/nerd-fonts/releases (я использую Meslo)
Далее меняем в настройках терминала на установленный шрифт
Устанавливаем OhMyPosh (опционально)
winget install JanDeDobbeleer.OhMyPosh --source winget --scope user --force
oh-my-posh get shell
New-Item -Path $PROFILE -Type File -Force
notepad $PROFILE
Вставляем конфиг для запуска
oh-my-posh init pwsh --config 'atomic' | Invoke-Expression
Сохраняем и закрываем
Применяем настройки
. $PROFILE
Устанавливаем git
https://git-scm.com/downloads/win
Устанавливаем Node.js
https://nodejs.org/en/download
Устанавливаем python3
https://www.python.org/downloads/
Устанавливаем choco
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
Устанавливаем зависимости
choco install ripgrep luarocks lazygit fzf unzip wget gzip 7zip tree-sitter zig curl -Y
Устанавливаем neovim
winget install Neovim.Neovim
Проверяем установку, запустив nvim
выходим через :q 
Делаем бэкапы (или удаляем) стандартные директории nvim
Move-Item $env:LOCALAPPDATA\nvim $env:LOCALAPPDATA\nvim.bak
Move-Item $env:LOCALAPPDATA\nvim-data $env:LOCALAPPDATA\nvim-data.bak
Клонируем репозиторий LazyVim
git clone https://github.com/LazyVim/starter $env:LOCALAPPDATA\nvim
Удаляем папку .git
Remove-Item $env:LOCALAPPDATA\nvim\.git -Recurse -Force
Запускаем снова nvim, происходит первая инициализация и установка, обязательно ждем пока все уведомления закончатся!
Заходим в командную строку через Пробел+: и вводим checkhealth
Смотрим на ошибки, нас интересуют секции lazy, lazyvim, mason, nvim-treesitter, Snacks (все кроме image), vim.health, vim.lsp, vim.treesitter
Если все ок - идем дальше, если не ок, то доставляем недостающие или интересующие пакеты через choco или winget (смотря где они будут)
Перезапускаем nvim
Идем в LazyExtras (через :LazyExtras или через начальное меню)
Листаем стрелочками и ставим нужные допы через клавишу x
Я поставил:
coding.yanky
editor.dial
editor.inc-rename
until.mini-hitpatterns
Далее идем в Mason (через пробел+c+m)
и ставим нужные LSP, линтеры и форматтеры (через клавишу i)
