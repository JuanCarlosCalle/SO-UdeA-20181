# Ejemplo 3

## Compilacion con comandos

```
gcc -I./includes main.c -c
gcc -I./includes gerga.c -c
gcc -I./includes matematicas.c -c
gcc *.o -o main.out -lm
```

## Compilacion empleando el archivo make

```
make
```

## Ejecucion

```
./main.out
```
