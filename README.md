#include <iostream>
#include <string> // Esto es para declarar la funcion de stoi

using namespace std;
//Estructura de la cola
struct Cola {
    int dato;
    Cola* siguiente;
};

bool esDigito(string num) {
    for (char c : num) {
        if (!isdigit(c)) {
            return false;
        }
    }
    return true;
}

void Agregar(Cola*& frente, Cola*& final, int nuevoDato) {
    Cola* nuevoNodo = new Cola();
    nuevoNodo->dato = nuevoDato;
    nuevoNodo->siguiente = nullptr;

    if (frente == nullptr) {
        frente = final = nuevoNodo;
    }
    else {
        final->siguiente = nuevoNodo;
        final = nuevoNodo;
    }

    cout << "El elemento " << nuevoDato << " ha sido añadido a la cola." << endl;
}

void EliminarUno(Cola*& frente, Cola*& final) {
    if (frente != nullptr) {
        int elementoEliminado = frente->dato;
        Cola* temp = frente;
        frente = frente->siguiente;
        delete temp;
        cout << "El elemento " << elementoEliminado << " ha sido eliminado de la cola." << endl;
    }
    else {
        cout << "La cola está vacía." << endl;
    }
}

void vaciarCola(Cola*& frente, Cola*& final) {
    if (frente != nullptr) {
        while (frente != nullptr) {
            Cola* temp = frente;
            frente = frente->siguiente;
            delete temp;
        }
        cout << "Todos los elementos han sido eliminados de la cola." << endl;
    }
    else {
        cout << "La cola está vacía." << endl;
    }
}

int main() {
    Cola* frenteCola = nullptr;
    Cola* finalCola = nullptr;

    while (true) {
        cout << "Opciones:" << endl;
        cout << "1. Agregar un elemento" << endl;
        cout << "2. Eliminar un elemento" << endl;
        cout << "3. Vaciar la cola" << endl;
        cout << "4. Salir" << endl;
        cout << "Selecciona una opción: ";

        int opcion;
        cin >> opcion;

        switch (opcion) {
        case 1: {
            cout << "Ingresa el elemento a agregar: ";
            string entrada;
            cin >> entrada;
            if (esDigito(entrada)) {
                int elemento = stoi(entrada);
                Agregar(frenteCola, finalCola, elemento);
            }
            else {
                cout << "Por favor, ingresa un dato numérico válido." << endl;
            }
            break;
        }
        case 2:
            EliminarUno(frenteCola, finalCola);
            break;
        case 3:
            vaciarCola(frenteCola, finalCola);
            break;
        case 4:
            cout << "Saliendo del programa." << endl;
            return 0;
        default:
            cout << "Opción inválida. Por favor, selecciona una opción válida." << endl;
        }
    }

    return 0;
}
