# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01

#### - Ciclo feetch-decode-execute

``` asm
@1
D=A
@2
D=D+A
@16
M=D
@END
(END)
0;JMP
```
##### Notas:
A (addres-direcciones) y D son 'variables', @1 guarda el valor en A, M es la memoria y guarda el dato en la memoria RAM, el apartado de PC me dice que instrucción esta leyendo y va a ejecutar, incrementa de uno en uno; (0;JMP) es una dirección en la ROM, JMP es jump (salto) y lo realiza a la posición guardada en A, 0 es una operación; (END) es una etiqueta y da la posición en la que está, es decir, el @END me pondrá un @7 en la posición 6.ROM guarda la receta/instrucciones, RAM hoja en blanco

##### Experimento
``` asm
@5
D=A
@10
D=D+A
@20
M=D
@END
(END)
0;JMP
```
##### Pregunta
- ¿Qué diferencia hay entre la memoria ROM y RAM?
