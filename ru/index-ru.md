---
layout: default-ru
lang: 🇷🇺
language: Русский
ref: idena-runner-script
title: Скрипт автоматической настройки Идена ноды — Idena Runner Script
---

## Добро пожаловать на страницу баш скрипта Idena Runner

<p align="justify"><b>Установщик ноды Идена</b> в виде bash скрипта. Позволяет устанавить множество нод <b>Idena-Go</b> на ваш сервер в виде простого и понятного мастера с друественным интерфейсом.</p>

<p align="center"><a href="https://github.com/ltraveler/idena-runner/releases/latest" target="_blank"><img src="https://img.shields.io/badge/version-v0.2.2-blue?style=for-the-badge&logo=none" alt="последняя версия скрипта idena runner" /></a>&nbsp;<a href="https://wiki.ubuntu.com/FocalFossa/ReleaseNotes" target="_blank"><img src="https://img.shields.io/badge/Ubuntu-20.04(LTS)+-00ADD8?style=for-the-badge&logo=none" alt="Ubuntu minimum version" /></a>&nbsp;<a href="https://github.com/ltraveler/idena-runner/blob/main/CHANGELOG.md" target="_blank"><img src="https://img.shields.io/badge/Build-Stable-success?style=for-the-badge&logo=none" alt="idena-go latest release" /></a>&nbsp;<a href="https://www.gnu.org/licenses/quick-guide-gplv3.html" target="_blank"><img src="https://img.shields.io/badge/license-GPL3.0-red?style=for-the-badge&logo=none" alt="license" /></a></p>

## 🚀&nbsp; Запуск `idena_install.sh` (необходимо запускать от пользователя с привелегиями root)

Пожалуйста убедитесь, что у вас установлена чистая Ubuntu 20.04.
Для установки ноды идена-гоу используя данный скрипт, пожалуйста вледуйте следующим шагам:
* `git clone https://github.com/ltraveler/idena-runner.git` склонируйте репозиторий
* `cd idena-runner` перейти в директорию скрипта
* `chmod +x idena_install.sh` сделать скрипт исполняемым
* `./idena_install.sh` запуск скрипта

## ✅&nbsp; Функции

* Возможность установки нескольких нод на одном сервере: 1 пользователь - 1 сервер
* Возможность импорта уже существующих приватных/нод ключей во время процесса установки
* Автоматическое создание crontask задачи для автоматической проверки и установки новой версии клиента ноды idena-go
* Автоматическая настройка и конфигурирование необходимых портов для Uncomplicated Firewall (UFW) во время процесса установки ноды. 

## 🙋&nbsp; Что этот скрипт делает?

1. Проверяет существует ли сервис idena.service exists;
2. Создаёт нового пользователя и пароль для запуска демона ноды идена от его имени;
3. Обновление необходимых пакетов и установка все требуемых зависимостей;
4. Скачивание последней версии клиента ноды идена или той версии, которая была введена вручную в процессе установки. Если ввод оказался пустым, скачивается самая последняя версия. История релизов идена ноды [доступна здесь](https://github.com/idena-network/idena-go/releases);
5. Скрипт использует предопределённый конфигурационный файл `config.json` который может быть изменён во время процесса установки;
6. Установка клиента ноды Idena-go и его запуск основываясь на конфигурационном файле config.json доступным из репозитория;
7. Возможность изменения на лету/во время установки API нод ключа и приватного ключа на ваши собственные есил они у вас есть;
8. Создание задания cron для регулярной проверки наличия обновления для клиента ноды. По умолчанию проверка происходит раз в день. Вы можете указать любую периодичность с помощью языка cron;
9. Создание демона Idena Daemon и его последующий запуск;
10. Установка и конфигурирования необходимых настроек фаервола для добавления туда всех необходимых портов, основываясь на выставленных номерах портов SSH и IPFS.

##  ⚙️&nbsp;  About Idena Daemon
The script is creating a service daemon called idena. Which starts on the boot.
#### You can use these commands to control it:
* `service idena_$username status`- to check the status 
* `service idena_$username restart` - to restart the service
* `service idena_$username stop` - to stop the service
* `service idena_$username start` - to start the service

*where $username is required instance username

## ✔️&nbsp; Idena-runner instance update process (requires root privileges)

1. Backup the private key (`/home/idena_instance_username/idena-go/datadir/keystore/nodekey`)
2. Backup the node api.key (`/home/idena_instance_username/idena-go/datadir/api.key`)
3. Run the latest version of the idena-runner script and put the same username that you have used to install the instance that you are trying to update.
That will overwrite all required files.
***Attention:*** **all files inside the idena-go folder will be permanently deleted**.

## 🗑️&nbsp; Idena-go instance uninstallation process (requires root privileges)

1. `service idena_username stop` _stopping idena user instance_;
2. `pkill -u username` _killing all processes related to the user_;
3. `deluser --remove-home username` _removing related to idena-go instance user and all his files and folders_;
4. `rm /etc/cron.d/idena_update_username` _removing cron idena-go update related task_;
5. `rm /etc/systemd/system/idena_username.service` _removing idena daemon service related to the instance that we are uninstalling_;
6. `systemctl daemon-reload` and `systemctl reset-failed` _updating systemctl changes that we have made in the previous step_;
7. `ufw delete allow ipfs_port_number` you have to change ipfs_port_number to the ipfs port that you have used to install the idena-go instance. By default it is `40405`;
8. `sudo visudo` you have to find and delete the line related to the deleted user.

### 🤝&nbsp; Idena Donations

* `0xf041640788910fc89a211cd5bcbf518f4f14d831` - **All donations are welcomed and appreciated**;

### ℹ️&nbsp; Other information
* If you are looking for a stable shared node service, please contact me on **Telegram**  `@ltrvlr`

### 🗣️&nbsp; Contact information
* **Email** `ltraveler@protonmail.com`
* **Telegram** `@ltrvlr`

For more detailed information about **idena-go** client please check the official [idena-go](https://github.com/idena-network/idena-go) github repository.
