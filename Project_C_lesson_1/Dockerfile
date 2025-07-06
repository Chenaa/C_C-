#Устанавливать так:
#docker build -t dev

#Базовый дистрибутив
FROM alpine:3.20

#Дополнительные утилиты
RUN apk --upgrade add \
	gcc \
	bash \
	make \
	alpine-sdk \
	valgrind \
	clang18-extra-tools 
#Программы для редактирования кода
RUN apk --upgrade add \
	vim \
	tmux
#Проверки и проекты утилиты
RUN apk --upgrade add \
	check-dev \
	doxygen	\
	gcovr
#Мягкая ссылка для совместимости
RUN ln -s /usr/lib/llvm18/clang-format /usr/bin/clang-format

#Приглашение командной строки
#ENV PS1 = "\033[90mdev\033[0m \033[33m->\033[0m" 
