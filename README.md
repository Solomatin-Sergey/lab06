[![Build Status](https://www.travis-ci.com/Solomatin-Sergey/lab06.svg?branch=main)](https://www.travis-ci.com/Solomatin-Sergey/lab06)
# lab06
## Изучение средств пакетирования на примере CPack

>> После того, как вы настроили взаимодействие с системой непрерывной интеграции,
обеспечив автоматическую сборку и тестирование ваших изменений, стоит задуматься
о создание пакетов для измениний, которые помечаются тэгами (см. вкладку releases).
Пакет должен содержать приложение solver из предыдущего задания Таким образом, каждый новый релиз будет состоять из следующих компонентов:

* архивы с файлами исходного кода (.tar.gz, .zip)
* пакеты с бинарным файлом solver (.deb, .rpm, .msi, .dmg)

>> Для этого нужно добавить ветвление в конфигурационные файлы для CI со следующей логикой:
>> если commit помечен тэгом, то необходимо собрать пакеты (DEB, RPM, WIX, DragNDrop, ...) и разместить их на сервисе GitHub. (см. пример для Travi CI).

### Выполнение работы.

>> CMakeLists.txt был изменён под использование CPack, т.е. были добавлены следующие строки:

install(TARGETS solver DESTINATION bin)
set(CPACK_PACKAGE_NAME "solver") 
set(CPACK_PACKAGE_VENDOR "SuperCompany") 
set(CPACK_PACKAGE_CONTACT "some contact")  
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Nightmare") 
set(CPACK_PACKAGE_DESCRIPTION "What's up, guys? :-)") 
set(CPACK_GENERATOR "DEB" "RPM")  

>> в .travis.yml в соответсвие с инструкцией (примером) понадобилось добавить следующий код:

```# Эта конфигурация будет использовать «GITHUB OAUTH TOKEN» для загрузки «ФАЙЛА ДЛЯ ЗАГРУЗКИ» (относительно рабочего каталога) в сборках с тегами.
deploy: 
provider: releases
skip_cleanup: true
on:
  tags: true
```
