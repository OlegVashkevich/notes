[<< На главную](../README.md)

# PHP заметки

### Установка на Debian
1. проверяем и устанавливаем пакеты `sudo apt update -y && sudo apt upgrade -y`
2. установливаем необходимые пакеты зависимостей для HTTPS-транспорта и управления сертификатами. `sudo  apt  -y  install  lsb-release  apt-transport-https  ca-certificates`
3. загружаем ключ SURY GPG `sudo wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg`
4. добавляем информацию о репозитории SURY PPA в наши источники APT `echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/php.list`
5. обновляем индекс информации о пакетах сервера, чтобы применить изменения репозитория `sudo apt update -y`
6. смотрим все доступные версии PHP в исходниках репозитория APT `sudo apt policy php`
7. установливаем последнюю версию PHP `sudo apt install -y php`
8. проверяем версию PHP`php -v`
9. устанавливаем расширения php(пачкой)`sudo apt install -y php-mysql php-curl php-json php-xml php-mbstring`
10. или по одному `sudo apt install -y php8.3-sqlite3`
11. смотрим установленные расширения `php -m`

