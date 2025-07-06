# Шаблон небольшого проекта на C • Начало


## Выстраиваем систему выстраивания системы

```mermaid
flowchart LR
code(Просто код)
template(Шаблон проекта)
system(Настройка системы)

code:::b ==> |3| template:::y -.-> |10| system:::g

classDef b fill:#504945,color:#fff;
classDef y fill:#FABD2F;
classDef g fill:#B8BA46;

```

Преждевременная оптимизация — [censored]


Лень-матушка


Итерации решают

## Где запускаем?

```mermaid
flowchart LR
2025(2025)
cloud(Облако)
hard(Железо)
virtual(Виртуалка)

2025:::black ==> cloud:::green
2025 ==> hard:::green
hard -.-> virtual:::yellow
cloud -.-> virtual

classDef black fill:#504945,color:#fff;
classDef green fill:#B8BA46;
classDef yellow fill:#FABD2F;
```

- Очень, **очень** маленький проект
- Запускаем ≠ компилируем

### Облако • [Codespace](https://docs.github.com/ru/codespaces/about-codespaces)

```mermaid
flowchart LR
subgraph Ваш компьютер
browser(Браузер)
end

subgraph Ваш Github-репозиторий
code(Код)
subgraph Ваш Codespace
ide(IDE)
virtual(Виртуалка)
end
end

browser:::green ==> ide:::white
ide -.-> virtual:::yellow
ide -.-> code:::black

classDef black fill:#504945,color:#fff;
classDef white fill:#fff;
classDef green fill:#B8BA46;
classDef yellow fill:#FABD2F;
```

![image.png](attachment:a4ff1be2-8131-419a-bac1-135280ba9e94:image.png)

Ура, дождались, **наконец-то IDE**! Конкретно [VSCode](https://code.visualstudio.com)


- «Ваш» означает деньги 👛 (или нет)
- Не забываем **явно** останавливать 👛 👛 👛
- Можно подключаться удалённо

### Железо • Linux (Debian, Ubuntu, etc.)

```mermaid
flowchart LR
null((•))
base(База)
features(Всякие штуки)

null:::black ==> |Зачем?| base:::blue -.-> |Как?| features:::pink

classDef blue fill:#2C78BF,color:#fff;
classDef pink fill:#FF6DB5,color:#fff;
classDef black fill:#504945,color:#fff;
```

- Наверняка можно и Windows — рассказывайте?
- Вперемешку редактирование, компиляция и выполнение
- Файл `requirements.system`:
    
    ```c
    gcc
    clang-format-18
    gcovr
    make
    gdb
    valgrind
    git
    vim
    tmux
    gdb
    ```
    
- Установка всех зависимостей в систему:
    
    ```bash
    xargs -a requirements.system sudo apt install -y
    ```
    
- *Именно такой* файл может пригодиться много позже (ключевое слово — `CI`)
- Можно использовать и для настройки среды разработки
- Задача со звёздочкой — зависимость от конфигурации ОС:
    
    ```bash
    # Для разработки модулей ядра нам нужен linux-headers-$(uname -r)
    sed "s|\$(uname -r)|$(uname -r)|g" requirements.system | xargs sudo apt install -y
    ```
    
    <aside>
    <img src="/icons/clover-four-leaf_green.svg" alt="/icons/clover-four-leaf_green.svg" width="40px" />
    
    Пора складывать заклинания в `Makefile`
    
    </aside>



### Шаблон небольшого проекта на языке С


- Папки верхнего уровня:
    
    ```c
    build/ -- для компиляции
    data/  -- для работы с данными  
    demo/  -- примеры использования 
    doc/   -- документация
    inlucde/ -- это заголовочные файлы для подключения дополнительных библиотек (API) 
    lib/   -- подключения библиотек 
    log/   -- запись логов
    play/  -- проверка проекта 
    src/   -- основной код
    test/  -- для тестов
    tool/  -- инструменты для разработки 
    ```
    

    

### .gitignore

- Можно взять на Github стандартный для С, а потом доработывать:
    
    ```c
    build/* -- для компиляции
    play/*  -- проверка проекта 
    *.env
    *.log
    *.swp
    *.run
    ```


    

### Markdown-файлы с описанием проекта

- README.md
- INSTALL.md
- USAGE.md


### LICENSE
- Обычно MIT, реже GNU3, остальное совсем редкое
- Проще сразу
- Если потом - создать в web-интерфейсе файл LICENSE, остальное GITHUB предложит сам 


### Редактирование 
- Настройка IDE

### Скрипты
- Список недоделок (T0D0)
- Сессия мультиконного менеджера (tmux)

### Файл rquirements.system:

Что нужно установить 

- git
- gcc
- clang-format-18
- gcovr
- make
- alpine-sdk
- vim
- gdb
- tmux

### Установка всех зависимостей в систему:

- Bash
    - xargs -a requirements.system sudo apt install -y

### Именно такой файл может пригодиться  много позже (ключевое слово - CI)


### Можно использовать и для настройки среды разработки 


### Задача со звездочкой - зависимость от конфигурации ОС:
- #### Для разработки модулей ядра нам нужен linux-headers-$ (uname -r)
sed "s|\$(uname -r) | $(uname -r) g" requirements.system | xargs sudo apt install -y

### Виртуалка * Docker-контейнер
 - sudo systemctl status docker // проверим статус
 - vim Dockertest -> FROM ubuntu:latest
 - docker build -t devdev -f Dockertest // создадим образ 
 - docker images // проверим наши образы докера 
 - docker run -it devdev // зайти на образ докера devdev
 - docker ps -a //список контейнеров 
 - docker run -it -v $(pwd):/prj dev // находясь в любой директори на ОС прокидываем ее в докер dev
 - docker run --rm --name run -v $(pwd):/prj dev ./prj/a.out // запуск на оснвной ОС файл из докера 
 - alias ll="ls -la" //




    

### Виртуалка • [Docker](https://www.docker.com)-контейнер

```mermaid
flowchart LR
task(Задача)
tech(Технология)
file(Файл настройки)
com(Система команд)
gui(Интерфейс)

task:::black ==> tech:::blue
tech <--> file:::yellow
tech <--> com:::yellow
com <-.-> gui:::white

classDef black fill:#504945,color:#fff;
classDef blue fill:#2C78BF,color:#fff;
classDef yellow fill:#FABD2F;
classDef white fill:#fff;
```

- Уберём с железа хотя бы выполнение (а лучше и компиляцию)
- Сам [Docker](https://www.docker.com) не забываем установить. Проверка:
    
    ```bash
       sudo systemctl status docker
    ```
    
- Для начала обзаведёмся операционкой:
    
    ```docker
    FROM ubuntu:latest
    ```
    
    Создадим образ (типа диска для запуска):
    
    ```bash
    docker build -t dev .
    ...
    docker images
    ```
    
    Уже можно заходить:
    
    ```bash
    docker run -it dev
    ...
    docker ps -a
    ```
    
    <aside>
    <img src="/icons/chili-pepper_red.svg" alt="/icons/chili-pepper_red.svg" width="40px" />
    
    Есть много настроек и параметров, но начинать без них — легально
    
    </aside>
    
- Потом это просто `requirements.system` другими словами:
    
    ```docker
    # Устанавливать так:
    # docker build -t dev .
    
    # Базовый дистрибутив
    FROM alpine:3.20
    
    # Дополнительные утилиты
    RUN apk --upgrade add \
        bash \
        make \
        alpine-sdk \
        valgrind \
        clang18-extra-tools 
    
    # Программы для редактирования кода
    RUN apk --upgrade add \
        vim \
        tmux
    
    # Проверки и проектные утилиты
    RUN apk --upgrade add \
        check-dev \
        doxygen \
        gcovr
    ```
    
- Ну и немножко тюнинга, как будто мы в терминале:
    
    ```bash
    # Мягкая ссылка для совместимости
    RUN ln -s /usr/lib/llvm18/bin/clang-format /usr/bin/clang-format
    
    # Приглашение командной строки
    ENV PS1="\033[90mdev\033[0m \033[33m→\033[0m "
    ```
    
- А как передать в Docker код?
    
    ```bash
    docker run -it -v $(pwd)/../..:/prj dev
    ```
    

- Теперь можно компилировать:
    
    ```bash
    docker run --rm --name compile -v $(pwd)/../..:/prj dev make -C /src main.run
    ```
    

Ах ты ж


- И исполнять:
    
    ```bash
    docker run --rm --name run -v $(pwd)
    ```
    
- Добавить в `Makefile` не так-то просто
    
    ```bash
    PRJ_DIR := $(shell pwd)/../../
    SHELL   := /bin/bash
    ```
    

### Next steps

- Разные системы для запуска и компиляции
- Мультиконтейнерное приложение (как минимум Docker Compose)
- Контейнирование эмуляторов микроконтроллеров
- Другие виртуальные машины
- Удалённый доступ через IDE
- Публикация на [Docker Hub](https://hub.docker.com)





