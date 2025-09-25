# Unidad 2
## Fase: Set-Seek 🔎💡
### Actividad 1
#### Dibujando un punto en la pantalla
  Al cargar la instrucción 0: A toma un valor de 16384.  \
  Al cargar la instrucción 1: A tiene el valor 16384, en la RAM posición 16384 se escribe un 1, se pinta un píxel o punto en la pantalla.  \
    \
  *Notas = En la dirección 16384 (SCREEN) se almacena la primer línea de pixeles de la pantalla, sinedo 16 en total. 1= negro y 0=blanco. En binario, la instrucción M=1 va a quedar 0000000000000001 pintando sólo un punto.*
```asm
@SCREEN
M=1
```
```c++
screen=1;
//Se fuerza la compilador para que asigne la variable screen a la dirección:16384
```

### Actividad 2
#### Dibujando una línea horizontal
  Al cargar la instrucción 0: A toma un valor de 16384.  \
  Al cargar la instrucción 1: A tiene el valor 16384, en la RAM posición 16384 se escribe un -1, se pinta un píxel o punto en la pantalla.  \
    \
  *Notas = En binario, la instrucción M=-1 va a quedar 1111111111111111 pintando una línea.*
```asm
@SCREEN
M=-1
```
```c++
screen=-1;
//Se fuerza la compilador para que asigne la variable screen a la dirección:16384
```

### Actividad 3
#### Entrada salida interactiva
  *Notas = Primero realizamos el mover hacia la derecha, lo probamos y realizamos modificaciones. Luego realizamos el mover hacia la izquierda, lo probamos y realizamos modificaciones necesarias para poder ver si funciona o no. Por ultimo realizamos la lectura de las teclas, para completar el ciclo, el funcionamiento y la interactividad del programa. Recordar que @KBD lee las teclas del teclado, JEQ es saltar si es igual a, con 0;JMP se genera el loop.*
```asm
@SCREEN
M=-1
@CONTADOR
M=0

(LEER)
@KBD
D=M
// d=100 i=105
@100
D=D-A
@DERECHA
D;JEQ

@KBD
D=M
// d=100 i=105
@105
D=D-A
@IZQUIERDA
D;JEQ

@LEER
0;JMP

(DERECHA)
//DIRECCIÓN SCREEN + N

//BORRAR DIRECCIÓN ACTUAL
@CONTADOR
D=M
@SCREEN
A=D+A
M=0


//PINTAR PROX. DIRECCIÓN
@CONTADOR
M=M+1
D=M
@SCREEN
A=D+A
M=-1


@LEER
0;JMP

(IZQUIERDA)
//DIRECCIÓN SCREEN - N

//BORRAR DIRECCIÓN ACTUAL
@CONTADOR
D=M
@SCREEN
A=D+A
M=0

//PINTAR PROX. DIRECCIÓN
@CONTADOR
M=M-1
D=M
@SCREEN
A=D+A
M=-1

@LEER
0;JMP
```
Una idea de cómo sería en c++, aunque no lo sea
```c++
//No es c++

Memoria[screen]=-1;
contador=0;

//Leer

int temp;

while (1)
{
  temp = KBD;	
  if (temp == 100)
   {
     //Derecha
     memoria[contador+screen]=0;
     contador = contador + 1;
     memoria[contador+screen]=-1;
   }
  else if (temp == 150)
   {
     //Izquierda
     memoria[contador+screen]=0;
     contador = contador - 1;
     memoria[contador+screen]=-1;
   }
}
```

### Actividad 4
#### Paso de lenguaje c++ a lenguaje ensamblador:
```c++
int i =1;
int sum=0;
```
En lenguaje ensamblador es: 
```asm
@i
M=1
@sum
M=0
```
```c++
while (i<=100)
```
Esa condicion en lenguaje ensamblador es:
```asm
@i
D=M // D=i
@100
D=D-A // D=i-100
@END
D;JGT
```
```c++
sum+=i;
i++;
```
En lenguaje ensamblador es: 
```asm
@i
D=M // D=i
@sum
M=D+M // sum=sum+i
@i
M=M+1 // i=i+1
```
#### Por que el while y el for son equivalentes?
  Son equivalentes porque el for es una forma mas compacta del ciclo while, al final obtendremos lo mismo y en lenguaje ensamblador son iguales.
```asm
// Adds1+...+100.
 @i //i se refiere a una ubicacion en la memoria.
 M=1 //i=1
 @sum //sum se refiere a una ubicacion en la memoria.
 M=0 //sum=0
 (LOOP)
 @i
 D=M //D=i
 @100
 D=D-A //D=i-100
 @END
 D;JGT //If(i-100)>0 gotoEND
 @i
 D=M //D=i
 @sum
 M=D+M //sum=sum+i
 @i
 M=M+1 //i=i+1
 @LOOP
 0;JMP //Va al LOOP
 (END)
 @END
 0;JMP //Loop infinito
```
### Actividad 5
#### Punteros
  Es una variable donde se pueden guardar direcciones.
```c++
//Variable que guarda un valor (entero en este caso).
int i;

//Declarar un puntero de nombre ptr, es una variable que guarda direcciones de otras variables.
int* ptr;

int i + 5;
int* ptr = &i;
//Error int* ptr = i; el & ayuda a definir su variable.

//Leer con el puntero.
int j = *ptr;

//Escribir con el puntero.
*ptr = 25;
```
#### Convierte estos programas a ensamblador y realiza la simulación paso a paso. 
1.
```c++
int a=10;
int* p;
p=&a;
*p=20;
```
En lenguaje ensamblador:
```asm
@10
D=A
@a //16
M=D

@a
D=A
@p //17
M=D

@20
D=A
@p
A=M
M=D
```

2. 
```c++
int a = 10;
int b = 5;
int *p;
p = &a;
b = *p;
```
En lenguaje emsamblador:
```asm
@10
D=A
@a //16
M=D

@5
D=A
@b //17
M=D

@a
D=M
@p //18
M=D


@p
D=M
@b
M=D
```
## Fase: Apply 🛠️
### Actividad 6
- Experimenta con arreglos
```c#
int arr[] = {1,2,3,4,5,6,7,8,9,10};
int sum = 0;

for (int j = 0; j < 10; j++)
{
    sum = sum + arr[j];
}
```
```asm
// Inicializacion del arreglo

@1
D=A
@a
M=D

@2
D=A
@b
M=D

@3
D=A
@c
M=D

@4
D=A
@d
M=D

@5
D=A
@e
M=D

@6
D=A
@f
M=D

@7
D=A
@g
M=D

@8
D=A
@h
M=D

@9
D=A
@i
M=D

@10
D=A
@j
M=D

// Inicializaciones

@12
M=0   // sum = 0

@a
D=A
@13
M=D   // puntero = 16

@10
D=A
@14
M=D   // cuenta = 10

(FOR)
@13
A=M
D=M       

@12
M=D+M    

@13
M=M+1    

@14
M=M-1     

@14
D=M
@FOR
D;JGT
```

## 🤔 Fase: Reflect
