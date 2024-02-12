[<< На главную](../README.md)

# Разное - WSL в windows (Debian)

1. включаем WSL `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`
2. включаем виртуализацию `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`
3. устанавливаем wsl2 версию по умолчанию `wsl --set-default-version 2`
4. проверим доступные дестрибутивы `wsl --list --online`
5. установливаем debian `wsl --install -d Debian` 
6. прописываем пользователя и пороль
7. доступ к debian через команду `wsl -d Debian`
8. проверяем и устанавливаем пакеты `sudo apt update && sudo apt upgrade -y`
9. проверяем версию `cat /etc/os-release`