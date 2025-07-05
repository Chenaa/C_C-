# Шаблон небольшого проекта на C • Начало





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
- # Для разработки модулей ядра нам нужен linux-headers-$ (uname -r)
sed "s|\$(uname -r) | $(uname -r) g" requirements.system | xargs sudo apt install -y

### Виртуалка * Docker-контейнер
 - sudo systemctl status docker // проверим статус
 - vim Dockertest -> FROM ubuntu:latest
 - docker build -t devdev -f Dockertest // создадим образ 
 - docker images // проверим наши образы докера 
 - docker run -it devdev // зайти на образ докера devdev
 - docker ps -a //список контейнеров 
 - docker run -it -v $(pwd):/prj dev // находясь в любой директори на ОС прокидываем ее в докер dev
 - docker run --rm --name run -v $(pwd):/prj dev ./prj/a.out / запуск на оснвной ОС файл из докера 
 




