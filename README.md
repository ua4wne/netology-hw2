## Задача 0

Убедимся, что у нас установлено нужное ПО.
![docker compose](task0/docker_compose.png)


## Задача 1

[Создаем fork репозитория](https://github.com/ua4wne/shvirtd-example-python.git)

Создали файл с именем Dockerfile.python для сборки данного проекта и проверяем корректность сборки.
![Сборка контейнера](task1/build.png)
![Сборка контейнера](task1/build1.png)
![Сборка контейнера](task1/build2.png)
![Сборка контейнера](task1/build3.png)

Запускаем web-приложение без использования docker в venv. (Mysql БД запускаем в контейнере docker).
![venv](task1/venv.png)
![site](task1/venv_result.png)

## Задача 3
![Запуск контейнера](task3/1.png)
![Стоп контейнер](task3/2.png)