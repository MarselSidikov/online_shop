Подготовка к деплою:

### 01. Работа с properties, профилями и переменными окружения

* Цель - сделать отдельные настройки для локального запуска и запуска на сервере
* Не указывать нигде в коде явные данные для настройки

* Последовательность подключения пропертисов - сначала смотрит ENVIRONMENT_VARIABLES, потом смотрит application.yml, потом смотрит application-профиль.yml

* На сервере запуск всегда должен быть через переменные окружения и без профиля

## 2. Редактирование pom.xml

* Нам нужно, чтобы приложение собиралось со всеми зависимостями

## 03. Добавление Docker-файла

#### Linux 

* Linux - операционная система, которая поддерживает изолированные области для процессов
* Т.е. каждый процесс может запускаться в своей изолированной области не мешая другим процессам
* На основе этой особенности реализовали инструмент Docker

#### Docker

* Docker - система контейнеризации, нужен для того, чтобы все приложение упаковать в один "образ"
* Docker позволяет постоянно руками не настраивать сервер и не устанавливать туда какие-то зависимости, окружения, библиотеки и т.д.
* Вы можете описать инструкцию по тому, как нужно запустить ваше приложение один раз (такая инструкция называется Dockerfile)
* На основе Docker-файл создается "образ" (image)
* А на основе image можно делать изолированный контейнер
* Т.е. глобально, вы передаете заказчику образ, в котором уже все настроено. и никому не нужно возиться с сервером
* Основная задача Docker - защитить окружения друг от друга, поэтому если будут проблемы в одном приложении, они не отразятся на другом
* Также, удобно, что некоторые платформы (например, Digital Ocean) могут читать ваши Docker-файлы и запускать приложения согласно им
  * и это будет происходить в автоматическом режиме

* В нашем случае, чтобы приложение заработало, нужно:
  * Чтобы был Maven (его надо установить)
  * Чтобы было JDK (нужно установить)
  * Приложение нужно собрать
  * Чтобы было JRE (виртуальная машина Java, тоже нужно установить)
  * Приложение нужно запустить внутри этой виртуальной машины


* Внутри этого образа находятся все настройки для окружения вашего приложения
* В нашем случае Docker работает следующим образом:
  * Берет какой-то linux, в котором уже есть Maven
  * Он берет ваш код и собирает его с помощью Maven
  * Он берет Linux с JRE
  * И запускает ваш проект с этим linux

### Резюме

1. Сделать отдельный профиль для local-запуска
2. Починить все тесты, чтобы они работали
3. Редактировать pom.xml
4. Подключить Docker-файл, убедиться, что там идет вызов вашего приложения