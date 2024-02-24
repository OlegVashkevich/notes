[<< На главную](../README.md)

# Разное - WSL в windows (Debian)
## Установка среды
1. включаем WSL `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`
2. включаем виртуализацию `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`
3. устанавливаем wsl2 версию по умолчанию `wsl --set-default-version 2`
4. проверим доступные дестрибутивы `wsl --list --online`
5. устанавливаем debian `wsl --install -d Debian` 
6. прописываем пользователя и пороль
7. доступ к debian через команду `wsl -d Debian`
8. проверяем и устанавливаем пакеты `sudo apt update && sudo apt upgrade -y`
9. проверяем версию `cat /etc/os-release`

## Установка окружения
1. ставим wget `sudo apt install wget`
2. качаем новую версию go название пакета и путь смотрим тут https://go.dev/dl/ `wget путь_к_архиву`
3. (опционально) если go стоял - сносим `rm -rf /usr/local/go`
4. распаковываем в /usr/local - `tar -C /usr/local -xzf название_архива`
5. открываем файл `sudo nano /etc/profile` в конец добавляем строку `export PATH=$PATH:/usr/local/go/bin` выходим с сохранением
6. что бы устанавливаемые бинарные пакеты для го работали как баш-команды - открываем файл `sudo nano ~/.profile` прописываем строку В конце `export PATH=$PATH:$HOME/go/bin`
7. перезапускаем профиль `source $HOME/.profile`
8. проверяем `go version`
9. ставим git `sudo apt install git`
10. прописываем данные для гита `git config --global user.email "you@example.com"` и `git config --global user.name "Your Name"`
11. ставим taskfile `go install github.com/go-task/task/v3/cmd/task@latest`, после перезагружаем профиль `source $HOME/.profile`
12. ставим temple `go install github.com/a-h/templ/cmd/templ@latest`, после перезагружаем профиль `source $HOME/.profile`