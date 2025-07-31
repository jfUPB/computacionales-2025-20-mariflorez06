# Unidad 2

## 🔎 Fase: Set + Seek

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
