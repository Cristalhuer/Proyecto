# Proyecto
Proyecto
#include <stdio.h>

#define MAX_TAREAS 100
#define MAX_TITULO 100

typedef struct {
    char titulo[MAX_TITULO];
    int completada;
} TAREA;

TAREA tareas[MAX_TAREAS];
int numTareas = 0;

void agregarUnaTarea() {
    if (numTareas < MAX_TAREAS) {
        printf("Ingrese el título de la tarea: ");
        scanf(" %[^\n]", tareas[numTareas].titulo);
        tareas[numTareas].completada = 0;
        numTareas++;
        printf("Tarea agregada correctamente.\n");
    } else {
        printf("No se pueden agregar más tareas, la lista está llena.\n");
    }
}

void marcarComoCompletada() {
    char titulo[MAX_TITULO];
    int encontrado = 0;

    printf("Ingrese el titulo de la tarea que desea marcar como completada: ");
    scanf(" %[^\n]", titulo);

    for (int i = 0; i < numTareas; i++) {
        if (strcmp(titulo, tareas[i].titulo) == 0) {
            tareas[i].completada = 1;
            printf("Tarea marcada como completada.\n");
            encontrado = 1;
            break;
        }
    }

    if (!encontrado) {
        printf("No se encontró la tarea con ese título.\n");
    }
}

void listaDeTareasPendientes() {
    printf("Tareas Pendientes:\n");
    for (int i = 0; i < numTareas; i++) {
        if (!tareas[i].completada) {
            printf("- %s\n", tareas[i].titulo);
        }
    }
}

void listarTodasLasTareas() {
    printf("Todas las Tareas:\n");
    for (int i = 0; i < numTareas; i++) {
        printf("- %s (%s)\n", tareas[i].titulo, tareas[i].completada ? "Completada" : "Pendiente");
    }
}

int buscarTareaPorTitulo(char titulo[MAX_TITULO], int index) {
    if (index >= numTareas) {
        return -1; //Cuando la tarea no se encuentra.
    }
    if (strcmp(titulo, tareas[index].titulo) == 0) {
        return index; // Cuando la tarea si es encontrada.
    }
    return buscarTareaPorTitulo(titulo, index + 1); // Aqui buesca a las siguiente tarea.
}

void buscarTarea() {
    char titulo[MAX_TITULO];

    printf("Ingrese el título de la tarea que desea buscar: ");
    scanf(" %[^\n]", titulo);

    int index = buscarTareaPorTitulo(titulo, 0);

    if (index != -1) {
        printf("Tarea encontrada: %s (%s)\n", tareas[index].titulo, tareas[index].completada ? "Completada" : "Pendiente");
    } else {
        printf("No se encontró la tarea con ese título.\n");
    }
}

int main() {   //El menu.
    int opcion;

    do {
        printf("\n***_MENU_***\n");
        printf("1. Agregar una nueva tarea\n");
        printf("2. Marcar una tarea como completada\n");
        printf("3. Lista de todas las tareas pendientes\n");
        printf("4. Lista de todas las tareas\n");
        printf("5. Buscar tarea por título\n");
        printf("6. Salir del programa\n");
        printf("Ingrese cualquier opción: ");
        scanf("%d", &opcion);

        switch (opcion) {
            case 1:
                agregarUnaTarea();
                break;
            case 2:
                marcarComoCompletada();
                break;
            case 3:
                listaDeTareasPendientes();
                break;
            case 4:
                listarTodasLasTareas();
                break;
            case 5:
                buscarTarea();
                break;
            case 6:
                printf("Salió del programa con éxito...\n");
                break;
            default:
                printf("Opción inválida. Por favor, ingrese una opción válida.\n");
        }
    } while (opcion != 6);

    return 0;
}
