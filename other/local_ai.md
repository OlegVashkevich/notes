[<< На главную](../README.md)

# Локальный ИИ

## Ollama
Ollama - позволяет запустит сервер с языковыми моделями и управлять ими.

- скачать https://ollama.com/download/OllamaSetup.exe
- установить
- запуск сервера `ollama serve`
- подключить модель для чата `ollama run llama3.1:8b`
- подключить модель для автокомплита `ollama run qwen2.5-coder:1.5b`

полезные команды
- ollama list
- ollama ps
- ollama stop <model_name>

для запуска сервера под определенным IP - нужно прописать переменную окружения `OLLAMA_HOST` с адресом компа в сети, например `192.168.100.34` 

скорее всего потребуется создать правило в фаерволе на порт `11434`

## Сontinue
Сontinue - плагин для `VS Сode` или `JetBrains` IDE

сайт https://continue.dev/

кусок из настроек

```json
{
  "models": [
    {
        "title": "Llama3.1 8B",
        "provider": "ollama",
        "model": "llama3.1:8b",
        "apiBase": "http://192.168.100.34:11434"
    }
  
  ],
  "tabAutocompleteModel": {
    "title": "Qwen2.5-Coder 1.5B",
    "provider": "ollama",
    "model": "qwen2.5-coder:1.5b",
    "apiBase": "http://192.168.100.34:11434"
  },
  "contextProviders": [
    {
        "name": "url"
    },

    ----

  ]

  ---

}

```
