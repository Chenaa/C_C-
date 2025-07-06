%.o:
	gcc -c $(subst _,/,$(basename $@)).c -o $@
	#@gcc -c $^ -o $@
	
	#Без проверки .c-файла
	#gcc -c $*.c -o $@

	#То же самое, но сложней
	#gcc -c $(basename $@).c -o $@
	#@echo $*.c
	#echo $(basename $@)

%.run: b.o bla.o
	gcc $^ -o $@
