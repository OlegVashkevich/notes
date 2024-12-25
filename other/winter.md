[<< На главную](../README.md)

# WinterCMS
##  Общее
- до установки надо знать что вызов ```php artisan winter:mirror public --relative``` в windows требует административных прав, вариантов несколько, но один из - поменять политику создания символических ссылок для пользователя ```secpol.msc``` -> ```Security Settings → Local Policies → User Rights Assignment``` и добавить своего пользователя к ```Create symbolic links```
- установка ```composer create-project wintercms/winter .```
- сброс пароля ```php artisan winter:passwd admin new_pasword``` (просто пошаговый вызов через php artisan winter:passwd почему то не срабатывает)
- плагин для кастомизации админки ```cyd293-backendskin``` - ломает ее, аналогов пока не нашел
## ide-helper
плагин генерирует вспомогательные файлы, которые позволяют вашей IDE обеспечить точное автодополнение

установка 
```bash
composer require --dev flynsarmy/wn-idehelper-plugin "dev-master"
```
генерация файла 
```bash
php artisan ide-helper:generate
```
## builder
```bash 
composer require --dev winter/wn-builder-plugin
```
```bash
php artisan migrate
```
```bash
php artisan winter:mirror public --relative
```
