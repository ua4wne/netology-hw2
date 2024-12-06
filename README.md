## Задача 0

Убедимся, что у нас установлено нужное ПО.
![docker compose](task0/docker_compose.png)


## Задача 1

Создаем [fork репозитория](https://github.com/ua4wne/shvirtd-example-python.git)

Создали файл с именем Dockerfile.python для сборки данного проекта и проверяем корректность сборки.
![Сборка контейнера](task1/build.png)
![Сборка контейнера](task1/build1.png)
![Сборка контейнера](task1/build2.png)
![Сборка контейнера](task1/build3.png)

Запускаем web-приложение без использования docker в venv. (Mysql БД запускаем в контейнере docker).
![venv](task1/venv.png)
![site](task1/venv_result.png)

Исправление для управления названием используемой таблицы через ENV переменную, которую добавляем в Dockerfile.python (ENV DB_TABLE="requests")
![edit_env](task1/db_table.png)

## Задача 2

Создали в yandex cloud container registry с именем "test" с помощью "yc tool" (при выполнении команды не поправил имя на test, изменил его потом через веб-интерфейс)
![yc](task2/yc_registry.png)

после загрузки образа выполняем его сканирование
![scan](task2/yc_scan.png)
![result1](task2/result1.png)
![result2](task2/result2.png)
видно, что образ содержит одну критическую уязвимость и несколько уязвимостей уровня HIGH и MEDIUM

## Задача 3

Создаем файл для запуска нескольких контейнеров для работы приложения и запускаем  его в работу при помощи команды docker compose up -d
![curl](task3/curl.png)
Теперь подключимся к БД и посмотрим, что там есть
![show](task3/mysql.png)

## Задача 4

Создаем ВМ в Yandex Cloud и устанавливаем необходимое ПО, далее при помощи скрипта deploy.sh запускаем проект на этой ВМ и проверяем работу приложения
![check](task4/check.png)

Настраиваем remote ssh context к нашему серверу
![check](task4/context.png)

Теперь подключимся к БД и посмотрим, что там есть
![show](task4/mysql.png)

## Задача 5

Настроим резервное копирование при помощи образа schnitzler/mysqldump. Чтобы не светить секреты в репозиторий, предварительно на хосте создадим необходимые переменные окружения

`export DB_HOST=172.20.0.10 
export DB_USER=app 
export DB_PASSWORD=pass
export DB_NAME=virtd`

Далее напишем скрипт для кронтаба db_backup.sh, в который поместим следующую команду
`/usr/bin/docker run --rm --entrypoint "" -v /opt/backup:/backup --network="shvirtd-example-python_backend" --link="db:db" schnitzler/mysqldump mysqldump --opt -h db -u$DB_USER -p$DB_PASSWORD "--result-file=/backup/$(date +%F--%H-%M-%S)-dumps.sql" $DB_NAME`

Сам кронтаб

![show](task5/cron.png)

Результат работы задания по архивации
![show](task5/folder.png)


