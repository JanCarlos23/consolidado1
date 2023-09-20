# consolidado1
//Medina Arteaga Jan Carlos
//Palomino Chavez Rodrigo
//Delgadillo Pantoja José Samuel
//Tema: Bono de Colegios Zarate
#include <iostream>
#include <string>

using namespace std;

// Estructura para representar a los padres
struct Padre {
    string nombre;
    char nivelEducacion;
    char estadoPago;
    int numeroHijos;
    float promedio;
};

int main() {
    cout << "Colegio Zarate" << endl;
    const int numPadres = 10;
    
    // Arreglo para almacenar a los padres
    Padre padres[numPadres];

    // Captura de datos de los padres
    for (int i = 0; i < numPadres; i++) {
        cout << "\nIngrese el nombre del padre #" << (i + 1) << ": ";
        getline(cin, padres[i].nombre);

        // Captura del nivel de educación
        cout << "¿Nivel de educación del hijo (P para Primario, S para Secundario)?: ";
        cin >> padres[i].nivelEducacion;

        if (padres[i].nivelEducacion == 'P') {
            // Captura del promedio para nivel primario
            do {
                cout << "Ingrese el promedio del estudiante (0-20): ";
                cin >> padres[i].promedio;
            } while (padres[i].promedio < 0 || padres[i].promedio > 20);

            padres[i].estadoPago = ' ';
            padres[i].numeroHijos = 0; // No se utiliza para nivel primario
        } else if (padres[i].nivelEducacion == 'S') {
            // Captura del estado de pago para nivel secundario
            cout << "¿Estado de pago de pensiones (P para Puntual, A para Adelantado, R para Retrasado)?: ";
            cin >> padres[i].estadoPago;

            // Estructura condicional para preguntas adicionales según el estado de pago
            if (padres[i].estadoPago == 'R') {
                cout << "Bono denegado para " << padres[i].nombre << endl;
            } else {
                // Captura del número de hijos para nivel secundario
                cout << "¿Número de hijos?: ";
                cin >> padres[i].numeroHijos;
            }
        } else {
            cout << "Opción de nivel no válida. Ingrese 'P' o 'S'." << endl;
            i--; // Para volver a preguntar por este padre
        }

        // Consumir el salto de línea dejado por cin para evitar problemas con getline
        cin.ignore();
    }

    // Ordenar a los padres por promedio (descendente)
    for (int i = 0; i < numPadres - 1; i++) {
        for (int j = 0; j < numPadres - i - 1; j++) {
            if (padres[j].promedio < padres[j + 1].promedio) {
                swap(padres[j], padres[j + 1]);
            }
        }
    }

    // Otorgar media beca a los 3 mejores promedios en nivel primario
    cout << "\nMedias becas otorgadas a los 3 mejores promedios en nivel primario:\n";
    for (int i = 0; i < 3; i++) {
        if (padres[i].nivelEducacion == 'P') {
            cout << "Padre: " << padres[i].nombre << ", Promedio: " << padres[i].promedio << ", Media beca otorgada" << endl;
        }
    }

    // Otorgar bonos y descuentos a los padres en nivel secundario
    cout << "\nBonos y descuentos otorgados a los padres en nivel secundario:\n";
    for (int i = 0; i < numPadres; i++) {
        if (padres[i].nivelEducacion == 'S') {
            if ((padres[i].estadoPago == 'P' || padres[i].estadoPago == 'A') && padres[i].numeroHijos >= 1) {
                cout << "Bono de descuento del 50% otorgado a " << padres[i].nombre << endl;
            } else if (padres[i].estadoPago == 'R' && padres[i].numeroHijos > 1) {
                cout << "Descuento del 20% otorgado a " << padres[i].nombre << ")" << endl;
            }
        }
    }
  
    return 0;
}
