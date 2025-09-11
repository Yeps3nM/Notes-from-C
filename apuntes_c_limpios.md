# 📘 Apuntes de Lenguaje C


## Introducción y Sintaxis Básica
```c
#include <stdio.h>
/* Comentario en C */

// C busca una función main()
// Hay que declarar variables antes de usarlas
// Cada instrucción termina con ;
```

### Notas:
1. C inicia la ejecución en la función `main()`.
2. Las variables deben declararse antes de usarse.
3. Las instrucciones finalizan con punto y coma (`;`).
4. En los strings c sabe que se terminó cuando hay un Null al final 

## Entrada con scanf
```c
int usf, euf;
printf("Ingresa c° gatos
");
scanf("%d", &usf);
euf = usf - 1;
```

- `%d` es el especificador de formato para enteros.
- `&usf` pasa la dirección de memoria de `usf`.

## Entrada múltiple con scanf
```c
int myNum;
char myChar;
printf("Type : \n");
scanf("%d %c", &myNum, &myChar);
printf("Your number is: %d", myNum);
```

- Puedes capturar múltiples entradas con `scanf`.

## Input de cadenas (strings)
```c
char name[10];
printf("Enter name\n");
scanf("%s", name);
printf("Hello %s", name);
```

- `scanf("%s", name)` no necesita `&`.
- Solo permite una palabra.

## Lectura de línea con fgets
```c
char linea[100];
printf("Enter line\n");
fgets(linea, sizeof(linea), stdin);
printf("Line: %s", linea);
```

- `fgets` permite capturar líneas completas, incluyendo espacios.

## Estructuras y Listas Enlazadas
```c
struct item {
    int p;
    int q;
    struct item *next;
};
```
- Las listas enlazadas se componen de nodos con punteros al siguiente nodo.

## Suma de arreglo de estructuras
```c
int sumArray(struct arrayItem p[], int num) {
    int sum = 0, i;
    for (i = 0; i < num; i++) {
        sum = sum + p[i].p;
    }
    return sum;
}
```

## Suma de lista enlazada
```c
int sumlist(struct item *p) {
    int sum = 0;
    while(p != NULL) {
        sum = sum + p->p;
        p = p->next;
    }
    return sum;
}
```

## Lectura de archivos
```c
FILE *hand;
char line[1000];
hand = fopen("romeo.txt", "r");
while (fgets(line, 1000, hand) != NULL) {
    printf("%s", line);
}
```

## Ciclos y Condiciones
**Bucle contado:**
```c
for (int i = 0; i < 5; i++) {
    printf("%d\n", i);
}
```

**Mínimo y máximo valor:**
```c
int val, maxval, minval, first = 1;
while (scanf("%d", &val) != EOF) {
    if (first || val > maxval) maxval = val;
    if (first || val < minval) minval = val;
    first = 0;
}
```

## Adivinar número
```c
int guess;
while (scanf("%d", &guess) != EOF) {
    if (guess == 42) {
        printf("NICE WORK\n");
        break;
    } else if (guess < 42) {
        printf("TOO LOW\n");
    } else {
        printf("TOO HIGH\n");
    }
}
```

## Funciones
```c
int mymult(a, b)
    int a, b;
{
    return a * b;
}

int main() {
    int retval = mymult(6, 7);
    printf("Answer: %d\n", retval);
}
```

## Punteros

- `&`para obtener la dirección de memoria de cualquier variable.
- `*`utilizada para declarar una variable que es un puntero.
- `->`cuando se tiene una estructura y se usa un puntero que apunta a esta no se puede acceder directamente con un `.` por ello se utiliza la flecha para acceder a sus campos

```c
int valor; // Declaramos un puntero de tipo int que se llama foo*//
int *foo = &valor; //inicializamos foo con la dirección de valor que es un int//
*foo = 10;
foo -> bar == (*foo).bar 
```

- `*foo` accede al valor.
- `&valor` da la dirección de memoria.

```c
int* p; // p es un puntero a un entero
Node* n; // n es un puntero a un struct Node
int x = 5;
int* p = &x; // p guarda la dirección de x
printf("d\n", *p) // accede al valor de x

## Punteros y funciones

```c
void reiniciar(int *numero) {
    *numero = 0;
}

int main() {
    int n = 15;
    reiniciar(&n); //se pasa la dirección de n//
    printf("Valor después de reiniciar: %d\n", n);
}
```

**Incorrecto:**

- En c las variables creadas dentro de una función (no de forma global), solo interactúan dentro del scope de la función. Para que si sean accedibles desde fuera se hace global o se entrega en argumentos la dirección. 

```c
void reiniciar(int numero) {
    numero = 0;
}
int main() {
        int n = 15;
        reiniciar(n); /* Pasamos el valor de n, no su dirección */
        printf("Valor de n después de reiniciar: %d\n", n); /* Imprime 15 */
        return 0;}
```

## Punteros y Arrays
- Un array es un bloque contiguo de memoria.
- El nombre del array es un puntero al primer elemento.
- El array de un array es una matriz 
- (->) este operador se usa para acceder a elementos de un struct apuntada por un puntero

#### Inicializar char 
- En c no existen string propiamente tal como en python 
```c
char hello[] = "Hello, World!";
char hello[20] = "Hello, World!";
```
#### Aritmética de punteros 
- Para acceder a un elementos de un array A[offset]. Se ejemplifica de la siguiente forma:
    - A[0] = dirección del primer elemento + 0* sizeof(tipo de dato)
    - A[1] = dirección del primer elemento + 1* sizeof(tipo de dato)
    - A[N] = dirección del primer elemento + N* sizeof(tipo de dato)
- Size of permite saber cuántos bytes ocupa un tipo de dato para acceder a la posición correcta

## Structs
- OJO no son clases como en python sino una forma de agrupar datos relacionados bajo un mismo nombre.
```c
typedef struct gatito {
    char* nombre;
    bool desordenado;
    int edad;
} Gato;

int main() {
    Gato mi_gato = {"melon", true, 2};
    printf("Nombre: %s\n", mi_gato.nombre);
    printf("Desordenado: %d\n", mi_gato.desordenado);
    printf("Edad: %d\n", mi_gato.edad);
}
```

```c
int main(){
    //ejemplo de querer pedir memoria
    Gato* ,mi_gato = calloc(1, sizeof(Gato));
    // si Gato tuviera un array con hijos gatitos 
    mi_gato -> = Calloc(5,(sizeof(Gato)));
}
```

## Memoria dinámica con malloc
- Malloc se utiliza para reservar espacio en la memoria 
- Hay que revisar si el malloc fue exitoso
```c
typedef struct nodo {
    int dato;
    struct nodo* siguiente; 
} Nodo;

Nodo* cabeza = NULL; // puntero en la cabeza de la lista//

void imprimirLista(Nodo* cabeza) {
    while (cabeza != NULL) {
        printf("%d -> ", cabeza->dato);
        cabeza = cabeza->siguiente; //pasa al siguiente nodo//
    }
    printf("NULL\n");
}

int main() {
    Nodo* nuevo_nodo = (Nodo*)malloc(sizeof(Nodo)); // reserva memoria para un nuevo nodo
    if (nuevo_nodo == NULL) {
        fprintf(stderr, "Error al reservar memoria\n");
        return 1;
    }
    nuevo_nodo->dato = 42;
    nuevo_nodo->siguiente = NULL;
    cabeza = nuevo_nodo; // asigna el nuevo nodo a la cabeza 
}
```
## Memoria 
1. Stack : Sector asignado al programa, tiene espacio limitado
    - Almacena variables locales y temporales
2. Heap : No tiene estructura de asignación de espacios. Colección de bloques de memoria solicitados por el programa.
    - Almacena estructuras dinámicas 
#### Libreria <stdlib.h>
- malloc : recibe c° de bytes a pedir al Heap y retorna un puntero. Inicializa con valores random.
- calloc : Recibe la c° de elementos y su tamaño para pedir al Heap, retorna un puntero. Inicializa con 0 los valores
- free : Para liberar los bloques utilizados del Heap.
```c
//Malloc//
int a = 4 
int* b = malloc(a*sizeof(int));

//Calloc//
int a2 = 4
int* b2 = calloc(a2, sizeof(int));

free(b);
free(b2);
```
#### Ejemplo con heap 
```c
typedef struct account{  // un struct llamado cuenta //
    int balance; // campo//

} Account;
/* Función que modifica el balance  - Account *account un puntero a una account  - int amount cuánto suma al balance */
void add_balance(Account *account, int amount){
    account -> balance += amount  // Accede al campo balance a través del puntero y le suma amount//
} 
int main (){
    Account* acc; // se define una variable de puntero de tipo account
    acc = malloc(sizeof(Account));
    acc -> balance = 0;
    add_balance(acc,100)
    free(acc) //liberar la memoria solicitada al Heap 

}
```
## Listas ligadas 
- Una estructura organizada en nodos
- El nodo presente solo conoce el anterior y el siguiente 
- Cada nodo es un struct 
- Agregar elementos es asignar punteros, es más fácil que en un array
- No se busca fácil los elementos como en array, porque se debe recorrer todo nodo. Se debe iterar en torno a la lista y luego actualizar el último valor.
- Tiene complejidad de búsqueda O(n) y de inserción es O(1)!
```c
#include <stdio.h>
typedef struct node {
    // dos campos : value y next//
    int value;  
    struct node *next; // puntero al sgte nodo//
} Node;
 void print_linked_list(Node* head){ // recibe un puntero al primer nodo llamado head//
    while (head != NULL){
        printf("Value in node %d\n", head->value);
    }
 }
 int main(){
    //inicializar nodos (aún sin tener memoria)//
    Node* one = NULL;
    Node* two = NULL;
    Node* three =NULL;
    // Allocar memoria (memoria pedida al HEAP// 
    one = calloc (1, sizeof(Node));
    two = calloc (1, sizeof(Node));
    three = calloc (1, sizeof(Node));

    // Asignar valores a los espacios de memoria solicitados//
    one -> value = 1;   // value es un campo int del struct Nodo/7
    two -> value = 2;
    three -> value = 3;

    //Conectamos los nodos//
    //Desde el nodo one, su campo next (puntero) apunta a la dirección de two//
    one -> next = two; 
    two -> next = three;
    three -> next = NULL;

    print_linked_list(one);

    // Liberar memoria
    free(one);
    free(two);
    free(three);
    return 0
 }
 
 ```
- "struct node *next" declara un puntero llamado next que apunta a otro nodo de la misma estructura (struct node)
- (->) permite acceder a elementos de una estructura a través de un puntero

## Matrices 
- Es un array de arrays
- Se pueden usar arrays para guardar punteros
- Como los arrays son punteros, un arreglo de arrelgos, es un arreglo de punteros

```c
#include <stdio.h>
int main(){
    //método a) inicialización de matrices
    int matrix[3][2] = {{1,1},{2,2},{3,3}};
    // método b) inicialización de matriz por iteración
    int* matrix[3]; // matrix[3] es un puntero a un entero
        for (int i; i<3; i++){
            int array[2] = {i + 1, i + 1};
            matrix[i] = array;
        };
}
```
##
int *A = malloc (3 * sizeof(int))
A[0] = 1;
....
print( A, &A, &A[0])

A = puntero
A& = es un puntero de un puntero
&A[0] = pido el puntero del primer elemento del arreglo
A[0] = 1 

## Relevante 
- Cuando se tiene un struct, y se define un campo que no es puntero se hace con un . , no una flecha.
- Las variables siempre están en stack. Pueden almacenar cualquier cosa pero siguen en stack.
    - int number, int*number : ambas son variables pero la primera almacena un número en sí en el stack y otra almacena un puntero(dirección) en el stack.
- Usar `calloc` para más claridad 


## Errores comunes : Segmentation Fault
- Referenciar un puntero con valor null
- Usar punteros sin inicializarlos 
- Recursión infinita -> Stack overflow (se utiliza más memoria de la solicitada o de la existente)
- Acceder a índices fuera del límite del array
- Acceder a espacios de memoria ya liberados
- Liberar dos veces un espacio de memoria
- Punteros a variables locales (se eliminan después de los usos) & retornar punteros a variables locales
- Liberar punteros que nunca fueron del heap
- Modificar strings de forma literal
- 

```
int *psyduck = NULL;
printf("%d", *psyduck);  


int *psyduck;          
printf("%d", *psyduck); 
```

## NOTA : Uso de valgrind como herramienta para debugging 
## NOTA : Verificar los null para evitar Segmentation Faults 