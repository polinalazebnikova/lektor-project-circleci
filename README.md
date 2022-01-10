# lektor-project-circleci

# lektor-project

Для сборки был создан следующий файл config.yml:

Версия:
```
version: 2.1
```

Включение уже написанной конфигурации для работы с python:
```
orbs:
  python: circleci/python@1.2
```

Указание образа виртуальной машины, на которой будет происходить сборка и анализ:
```
jobs:
  build-and-test: 
    docker:
      - image: cimg/python:3.8
    steps:
      # подключение к репозиторию гитхаба с правами записи
      - add_ssh_keys:
          fingerprints:
            - e5:60:37:47:81:81:25:b5:07:6f:4f:b5:40:d8:27:cd

      - checkout
      # установка зависимостей (включая lektor)
      - run: pip install -r requirements.txt
      # сборка и деплой сайта на лекторе
      - run: lektor build && lektor deploy

```

Запуск указанных jobs: 
```
workflows:
  sample: 
    jobs:
      - build-and-test
```

Демонстрация успешной сборки:
