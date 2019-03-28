# jenkins-packer-tutorial

Данный репозиторий содержит в себе демонстрации, показанные на вебинаре "Автоматизация сборки образов и тестирование с помощью Jenkins на Яндекс.Облаке"
Основная цель - познакомить вас с возможностями по взаимодействию продуктов, нацеленных на непрерывную интеграцию и сборку образов с компонентами Яндекс.Облака.

## Начало работы

Для запуска тестовых инструментов

* Зарегистрируйтесь в [Яндекс.Облаке](https://cloud.yandex.ru)
* Создайте себе фолдер и подсеть в нём под демонстрацию 
* Установите и иницируйте [yc cli](https://cloud.yandex.ru/docs/cli/quickstart)
* Запишите id вашего фолдера и облака, выполнив `yc config list`
* Скачайте репозиторий с помощью git
```
git clone git@github.com:megaeee/jenkins-packer-tutorial.git
```
* Запишите id подсети в которой будете собирать образы, найдя её с помощью `yc vpc subnet list`
* Создайте сервисного пользователя и назначьте ему права на доступ к своей папке
```
yc iam service-account create --name packer-key
yc iam key create --service-account-name packer-key -o packer-key.json
SERVICE_ACCOUNT_ID=$(yc iam service-account get --name packer-key --format json | jq -r .id)
yc resource-manager folder add-access-binding packer-folder --role admin --subject serviceAccount:$SERVICE_ACCOUNT_ID
```
* Установите и иницируйте [terraform](https://www.terraform.io/downloads.html)
* (Для пользователей windows) установите [git-bash](https://gitforwindows.org) и делайте все задания из под него
* Создайте отдельный форк данного репозитория у себя в аккаунте
* Сгенерируйте [ssh ключ](https://git-scm.com/book/ru/v1/Git-на-сервере-Создание-открытого-SSH-ключа) для доступа к инстансам и добавьте его к ключам своего GitHub-аккаунта
