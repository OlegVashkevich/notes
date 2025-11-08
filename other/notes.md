[<< На главную](../README.md)

# Разное - заметки

### Инструменты для запуска/сборки задач
- [taskfile](https://taskfile.dev/) - кроссплатформенная замена makefile

### JSON
- [./jq](https://jqlang.github.io/jq/) - потоковый преобразователь json(парсер, фильтр, преобразователь) 

### Найти и убить процесс по используемому порту одной командой
- ```sudo ss -tlp 'sport = :3000' | grep pid  | awk -F, '{print $2 }' | awk -F= '{system("kill -9 " $2) }'``` - где :3000 номер порта

### Скинуть публичный ключик из винды на сервер linux из под PowerShell одной командой

```
$USER_AT_HOST="логин@сервер_ip"
$PUBKEY_PATH="$HOME\.ssh\название_ключа.pub"

$pubKey = Get-Content "$PUBKEY_PATH"
ssh $USER_AT_HOST "mkdir -p ~/.ssh && echo '${pubKey}' >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
```