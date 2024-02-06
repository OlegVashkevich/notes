[<< На главную](../README.md)

# GO заметки

### Err snippet - Упрошение написания обработки ошибок с помощью vscode
ставим плагин https://marketplace.visualstudio.com/items?itemName=yokoe.vscode-postfix-go

в настройках vscode прописываем 
```json
  "postfixGo.customTemplates": [
    {
      "name": "err",
      "body": "if {{expr}}!=nil {\n\treturn {{expr}} \n}",
      "description": "return err",
      "when": []
    }
  ]
```
использование:
в коде пишем, например `err.err`, и этот кусок подменяется на:
```go
if err!=nil {	
	return err 
}
```

можно расширить до 
```json
    {
      "name": "errLog",
      "body": "if {{expr}}!=nil {\n\tlog.Fatal(\"Error: \", {{expr}}) \n}",
      "description": "log err",
      "when": []
    },
    {
      "name": "errPrint",
      "body": "if {{expr}}!=nil {\n\tfmt.Println({{expr}}) \n}",
      "description": "print err",
      "when": []
    },
    {
      "name": "errPanic",
      "body": "if {{expr}}!=nil {\n\tpanic({{expr}}) \n}",
      "description": "panic err",
      "when": []
    }
```
не халтурим с ошибками, но при этом облегчаем рутину