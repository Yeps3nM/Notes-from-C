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
1. Stack : Sector asignado al programa, tiene espacio limitado.
2. Heap : No tiene estructura de asignación de espacios. Colección de bloques de memoria solicitados por el programa.
#### Libreria <stdlib.h>
- malloc : recibe c° de bytes a pedir al Heap y retorna un puntero. Inicializa con valores random.
- calloc : Recibe la c° de elementos y su tamaño para pedir al Heap, retorna un puntero. Inicializa con 0 los valores
- free : Para liberar los bloques utilizados del Heap.

```c
typedef struct account{  // un struct llamado cuenta //
    int balance; // campo//

} Account;
/* Función que modifica el balance 
- Account *account un puntero a una account  
- int amount cuánto suma al balance */
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