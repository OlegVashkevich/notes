[<< На главную](../README.md)

# Скрипт для нормализации грмкости музыки

```
#!/bin/bash

# Проверка аргументов
if [ $# -eq 0 ]; then
    echo "Использование: $0 <путь_к_музыкальной_директории>"
    echo "Пример: $0 /opt/navidrome/music"
    exit 1
fi

MUSIC_DIR="$1"

# Проверка существования директории
if [ ! -d "$MUSIC_DIR" ]; then
    echo "Ошибка: Директория '$MUSIC_DIR' не существует!"
    exit 1
fi

echo "Обработка ReplayGain для директории: $MUSIC_DIR"

process_format() {
    local ext="$1"
    local total=$(find "$MUSIC_DIR" -name "*.$ext" | wc -l)
    local count=0
    
    if [ "$total" -eq 0 ]; then
        echo "Файлов .$ext не найдено"
        return
    fi
    
    echo "Обработка $ext файлов ($total всего)..."
    
    find "$MUSIC_DIR" -name "*.$ext" -print0 | while IFS= read -r -d '' file; do
        ((count++))
        
        # Проверка через правильное имя тега (без пробелов!)
        if ! exiftool -replaygaintrackgain "$file" >/dev/null 2>&1; then
            echo "[$count/$total] Обработка: $(basename "$file")"
            loudgain -s e "$file"
        else
            echo "[$count/$total] Пропускаем (есть ReplayGain): $(basename "$file")"
        fi
    done
    
    echo "Завершена обработка $ext файлов"
    echo
}

# Обработка форматов
process_format "mp3"
process_format "flac" 
process_format "m4a"

echo "Готово! Обработка ReplayGain завершена для $MUSIC_DIR"
```

## Создание и использование
1. Создайть файл скрипта:
```
sudo nano /usr/local/bin/replaygain_fix.sh
```

2. Вставить содержимое скрипта и сохраните

3. Сделать скрипт исполняемым:
```
sudo chmod +x /usr/local/bin/replaygain_fix.sh
```

4. Запустить скрипт с указанием пути:
```
sudo /usr/local/bin/replaygain_fix.sh "/opt/navidrome/music"
```