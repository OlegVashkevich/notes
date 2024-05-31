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
5. что бы устанавливаемые бинарные пакеты для го работали как баш-команды - открываем файл `~/.profile` в конец добавляем:
```bash
# set PATH and environment for go if it exists
if [ -d "/usr/local/go" ] ; then
    export GOPATH=$HOME/go
    export GOBIN=$GOPATH/bin
    PATH="$GOBIN:/usr/local/go/bin:$PATH"
    #export GOPROXY=https://proxy.golang.org,direct
fi
```
6. обходим баг vscode (https://github.com/microsoft/vscode-remote-release/issues/6096#issuecomment-1774153528), он не запускает .profile для теминалов, изза чего очень часто отваливаются бинарные файлы go или его тузлов, и не только, для этого:
    1. в `~/.bashrc` добавляем: 
    ```bash
    if [ -f ~/.profile ]; then
        source ~/.profile
    fi
    ```
    2. в `~/.profile` находим и комментируем кусок(что бы не было зацикливания):
    ```bash
    # if running bash
    #if [ -n "$BASH_VERSION" ]; then
    #    # include .bashrc if it exists
    #    if [ -f "$HOME/.bashrc" ]; then
    #	. "$HOME/.bashrc"
    #    fi
    #fi
    ```
7. перезапускаем профиль `source $HOME/.profile`
8. проверяем `go version`
9. ставим git `sudo apt install git`
10. прописываем данные для гита `git config --global user.email "you@example.com"` и `git config --global user.name "Your Name"`
11. ставим taskfile `go install github.com/go-task/task/v3/cmd/task@latest`, после перезагружаем профиль `source $HOME/.profile`
12. ставим temple `go install github.com/a-h/templ/cmd/templ@latest`, после перезагружаем профиль `source $HOME/.profile`
### Фишки
- открыть рабочий раздел wsl-vscode в  windows -  `explorer.exe .`
- (не рекомендуется) создание контекстного меню для открытия папки windows в `vscode` как будто это подсистема linux(wsl):
> 1. открываем `regedit`
> 2. находим `HKEY_CLASSES_ROOT\directory\shell`
> 3. создаем там раздел "VSCodeWSL"
> 4. ключу по умолчанию даем значение "Открыть с помощью Code WSL"
> 5. создаем раздел `command`, должен получится путь `HKEY_CLASSES_ROOT\directory\shell\VSCodeWSL\command`
> 6. создаем ключ по умолчанию и даем ему значение `wsl.exe --distribution <Destrib_name> --user <user_name> --cd "%V" code .`, где меняем `<Destrib_name>` и `<user_name>` на свои 
> 7. все, при клике правой кнопкой по папке в контекстном меню появится пункт  Открыть с помощью Code WSL, который будет открывать WSL версию VScode