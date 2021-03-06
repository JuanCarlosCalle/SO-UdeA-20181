# Ejemplo multiarchivo

## Informacion general

* **Archivos**: 
  - main.c
  - funciones.c
  - funciones.h
  
## Casos de compilacion ##  
  
**Caso 1**:

```
# Generando los archivos objeto
gcc -Wall -c funciones.c
gcc -Wall -c main.c
# Generando el ejecutable
gcc -Wall funciones.o main.o -o example_multi1.out
```

**Caso 2**: Aca se usara la opcion -I

```
# Generando los archivos objeto
gcc -I. -Wall -c funciones.c
gcc -I. -Wall -c main.c
# Generando el ejecutable
gcc -Wall funciones.o main.o -o example_multi1.out
```

**Caso 3**: Usando comodines (Ya sea que se use o no la opcion -I)

```
# Generando los archivos objeto
gcc -I. -Wall *.c -c 
# Generando el ejecutable
gcc -Wall *.o -o example_multi1.out
```

* **Comando de ejecucion**:

```
./example_multi1.out
```

## Trabajando con makefiles

* **Archivo**: makefile1
```

# Regla de construccion general
all: example_multi1.out

# Regla que genera el archivo ejecutable
example_multi1.out: main.o funciones.o
        gcc main.o funciones.o -o example_multi1.out

# Reglas para generar los archivos objeto del programa
funciones.o: funciones.c funciones.h
        gcc -I. -c funciones.c
        
main.o: main.c funciones.h
        gcc -I. -c main.c

#Regla para borrar todos los archivos obtejo (.o) y copias de seguridad (~) del proyecto
clean:
	rm *.o *~

#Regla para borrar todos los archivos obtejo (.o), copias de seguridad (~) y el ejecutable generado	
clean_all:
	rm *.o *~ myexe

```

**Archivo 2**: Una version un poco mas mejorada:

```
#variables

#compilador
CC=gcc

# Regla de construccion general
all: example_multi1.out

# Regla que genera el archivo ejecutable
example_multi1.out: main.o funciones.o
	echo "Generando el archivo ejecutable..."
	$(CC) main.o funciones.o -o example_multi1.out

# Reglas para generar los archivos objeto del programa
funciones.o: funciones.c funciones.h
	$(CC) -I. -c funciones.c
	
main.o: main.c funciones.h
	$(CC) -I. -c main.c

#Regla para borrar todos los archivos obtejo (.o) y copias de seguridad (~) del proyecto
clean:
	rm *.o *~

#Regla para borrar todos los archivos obtejo (.o), copias de seguridad (~) y el ejecutable generado	
clean_all:
	rm *.o *~ *.out
```

Para mejorar los makefiles aun mas es bueno cacharrear en la pagina principal del tema hay enlaces de interes. Adicionalmente se pueden mirar los siguientes links:
1. [Quick Reference](https://www.gnu.org/software/make/manual/html_node/Quick-Reference.html)
2. [Make Cheatsheet](http://eduardolezcano.com/wp-content/uploads/2016/06/make_cheatsheet.pdf)
3. [RefCard Make](https://www.tofgarion.net/lectures/IN323/refcards/refcardMakeIN323.pdf)

El siguiente makefile tomado del siguiente [enlace](https://stackoverflow.com/questions/39699563/makefile-doesnt-find-source-files?rq=1) y adaptado al caso muestra el uso de variables como las mostradas anteriormente.

