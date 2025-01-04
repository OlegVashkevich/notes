[<< На главную](../README.md)

# Composer+private github repo

Допустим у нас есть приватный репозиторий `https://github.com/{vendor}/{package-name}.git`

Необходимо использовать его в проекте через `composer require {vendor}/{package-name}`



### В репозитории создаем composer.json
```json
{
    "name": "{vendor}/{package-name}",
    "description": "",
} 
```
## Используя Tag

### Создаем Tag
```bash
git tag -a v0.0.1 -m "version 0.0.1 alfa"
```
```bash
git push --tags
```
на github у пакета тег должен появится тут `https://github.com/{vendor}/{package-name}/tags`

### В проект где требуется пакет
добавляем приватный репозиторий к проекту
```bash
composer config repositories.{vendor}-{package-name} git https://github.com/{vendor}/{package-name}.git
```

все, можем использовать 
```bash
composer require {vendor}/{package-name}
```

## Без Tag

можно не создавать тег, но тогда надо знать ветку разработки пакета например master или main

добавляем приватный репозиторий к проекту
```bash
composer config repositories.{vendor}-{package-name} git https://github.com/{vendor}/{package-name}.git
```

вызываем с указанем ветки
```bash
composer require {vendor}/{package-name}:dev-{branch}
```