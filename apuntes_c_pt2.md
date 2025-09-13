# 📘 Apuntes de Lenguaje C : Parte 2

## Punteros, algoritmos de búsqueda y estructuras de datos

### Punteros 
- Variable que guarda una dirección de memoria (stack or heap)

```c
int cat_force = 350
int* pointer = &cat_force // si se usara heap, el lado derecho con calloc devuelve un puntero a su dirección de memoria. 
```
- En el ejemplo, pointer es el nombre que lleva una variable de tipo puntero.
- Si se imprimiera cat_force , da 350.
- Si se imprimiera pointer o &cat_force, dan ambos la dirección de memoria.
##### Desreferenciar
- Si se imprimiera *pointer, se imprime 350, ya que da el valor en sí al que apuntaba. 

- Nota : `*` puede seer utilizado para :
    1. Crear una variable de tipo puntero
    2. Como operador para desreferenciar 

#### Arrays con punteros 
- El nombre de un array es un puntero al primer elemento del array, por lo tanto si se imprimiera solo su nombre da la dirección de memoria de este. 
- Si se accede con `*` da el valor del primer elemento. 

```c
int cats_id[3] = {20,25,35};
printf("%d", *cats_id); // printea 20 
printf("%d\n", *(cats_id + 1)); // printea 25

for (int i = 0; i < 3; i++) {
  printf("%d\n", *(cats_id + i));
  *(cats_id + i) += 2 ;
}
\\ el loop accede a cada elemento del array de ids de gato, los printea y luego a cada valor de id le suma 2.

```
#### Struct y punteros 

- Para acceder a los campos de un struct con punteros, se utiliza `->`. 
-  A las funciones se les da el puntero del struct para que efectivamente se cambien los valores.

