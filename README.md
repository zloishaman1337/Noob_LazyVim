# Noob_LazyVim + Oh-my-posh
Делаем красивый терминал и ставим LazyVim
![photo_2025-08-19_22-10-50](https://github.com/user-attachments/assets/6f7afcb2-78ef-4d92-b435-de22c97f3df0)
![photo_2025-08-19_22-10-25](https://github.com/user-attachments/assets/0983fe11-ff47-45ee-be11-281ef8bf46fe)
Используем WindowsTerminal (в Вин11 стоит по стандарту, на Вин10 можно скачать отдельно в [майкрософт стор](https://apps.microsoft.com/detail/9n0dx20hk701?hl=ru-RU&gl=RU) или на [гитхабе](https://github.com/microsoft/terminal))
## Обновляем PowerShell
```powershell
winget install --id Microsoft.Powershell --source winget
```
## Устанавливаем Nerd Font 
Для отображения иконок, корректного отображения в LazyVim и просто красиво, ставим обязательно все шрифты, скачанные в архиве [NerdFonts](https://www.nerdfonts.com/font-downloads) (я использую Meslo)  
Далее меняем в настройках терминала на установленный шрифт
## Устанавливаем OhMyPosh (опционально)
1)
```powershell
winget install JanDeDobbeleer.OhMyPosh --source winget --scope user --force
```
2)
```powershell
oh-my-posh get shell
```
3)
```powershell
New-Item -Path $PROFILE -Type File -Force
```
4)
```powershell
notepad $PROFILE
```
5) Вставляем конфиг для запуска
```powershell
oh-my-posh init pwsh --config 'atomic' | Invoke-Expression
```
6) Сохраняем и закрываем  
7) Применяем настройки
```powershell
. $PROFILE
```
## Устанавливаем git
Скачиваем последний релиз [Git](https://git-scm.com/downloads/win)
## Устанавливаем Node.js
Скачиваем последний релиз [Node-JS](https://nodejs.org/en/download)
## Устанавливаем python3
Скачиваем последний релиз [Python](https://www.python.org/downloads/)
## Устанавливаем choco
```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```
## Устанавливаем зависимости
```powershell
choco install ripgrep luarocks lazygit fzf unzip wget gzip 7zip tree-sitter zig curl -Y
```
## Устанавливаем neovim
```powershell
winget install Neovim.Neovim
```
Проверяем установку, запустив
```powershell
nvim
```
выходим через
```powershell
:q
```
Делаем бэкапы (или удаляем) стандартные директории nvim
```powershell
Move-Item $env:LOCALAPPDATA\nvim $env:LOCALAPPDATA\nvim.bak
```
```powershell
Move-Item $env:LOCALAPPDATA\nvim-data $env:LOCALAPPDATA\nvim-data.bak
```
## Устанавливаем LazyVim
Клонируем репозиторий LazyVim
```powershell
git clone https://github.com/LazyVim/starter $env:LOCALAPPDATA\nvim
```
Удаляем папку .git

```powershell
Remove-Item $env:LOCALAPPDATA\nvim\.git -Recurse -Force
```
Запускаем снова nvim, происходит первая инициализация и установка, обязательно ждем пока все уведомления закончатся!
Заходим в командную строку через Пробел+: и вводим 
```powershell
checkhealth
```
Смотрим на ошибки, нас интересуют секции lazy, lazyvim, mason, nvim-treesitter, Snacks (все кроме image), vim.health, vim.lsp, vim.treesitter
Если все ок - идем дальше, если не ок, то доставляем недостающие или интересующие пакеты через choco или winget (смотря где они будут)
Перезапускаем 
```powershell
nvim
```
Идем в LazyExtras (через :LazyExtras или через начальное меню)
Листаем стрелочками и ставим нужные допы через клавишу x
Я поставил:
```powershell
coding.yanky
editor.dial
editor.inc-rename
until.mini-hitpatterns
```
Далее идем в Mason (через пробел+c+m)
и ставим нужные LSP, линтеры и форматтеры (через клавишу i) (Они нужны для корректной подсветки синтаксиса, форматированиия, автоподставки кода и подсказок)
