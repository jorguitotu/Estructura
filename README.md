#include<iostream>
#include<conio.h>
#include<stdlib.h>
#include<string.h>
#include<fstream>
#include<locale> // Incluir la biblioteca para setlocale
#include <windows.h>
#include<sstream>
using namespace std;

void setColor(int color) {
    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), color);
}

struct typeEstudiante{
    string nombre;
    string apellido;
    int edad;
    float promedio;
};

void menu(bool isDirector);
int mainScreen(bool isDirector);
bool action(int opc, bool isDirector);
bool loginDirector(void);
bool loginProfesor(void);
void menu(void);
int mainScreen(void);
bool action(int opc);
void agregar(void);
void mostrar(void);
void ordenar(void);
void buscar(void);
void eliminar(void);
void editar(void);
void guardarDatos(void);
void cargarDatos(void);



typeEstudiante alumno[40];
int count = 0;
bool VC_menu = true;
bool VC_login = false;
bool isDirector = false; // Añadir esta línea al principio del archivo, junto a las demás variables globales


int main() {
    setlocale(LC_ALL, ""); 
    system("color 0A"); 
    cargarDatos();

    while (true) {
        int userType;
        cout << "\n\t\t Seleccione el tipo de usuario:" << endl;  
        cout << "\n\t\t1. Docente" ;
        cout << "\n\t\t2. Director" << endl;
        cout << "\n\t\tOpcion: ";
        cin >> userType;
        cin.ignore(); 

        if (userType == 1) {
            if (loginProfesor()) {
                isDirector = false;
                menu(isDirector);
                break; 
            }
        } else if (userType == 2) {
            if (loginDirector()) {
                isDirector = true;
                menu(isDirector);
                break; 
            }
        } else {
            cout << "Opcion no valida. Intentelo de nuevo." << endl;
        }
    }

    getch();
    guardarDatos();
    return 0;
}




bool loginDirector(void) {
    setlocale(LC_ALL, "");

    wstring user, pass;
    wstring storedUser = L"director";
    wstring storedPass = L"12345";
    bool loginSuccess = false;

    system("color 0A"); // Fondo negro (0), texto verde (A)

    for (int count_login = 0; count_login < 3; count_login++) {
        system("cls");
        setColor(14); // Amarillo
        wcout << L"\n\t\t  ===============================" << endl;
        wcout << L"\t\t |                               |" << endl;
        setColor(10);
        wcout << L"\t\t       BIENVENIDO DIRECTOR      " << endl;
        setColor(14);
        wcout << L"\t\t |                               |" << endl;
        wcout << L"\t\t  ===============================" << endl;
        wcout << endl;
        setColor(10);
        wcout << L"\tIntentos restantes: " << 3 - count_login << endl << endl;
        wcout << L"\t\tUsuario: ";
        getline(wcin, user);
        wcout << L"\t\tContraseña: ";

        wchar_t clave;
        pass = L"";
        while ((clave = _getwch()) != 13) { // 13 es Enter
            if (clave == '\b') { // Caracter de retroceso
                if (!pass.empty()) {
                    wcout << L"\b \b"; // Borrar último asterisco en pantalla
                    pass.pop_back(); // Eliminar último carácter de la contraseña
                }
            } else {
                pass.push_back(clave);
                wcout << L"*";
            }
        }

        if (user == storedUser && pass == storedPass) {
            loginSuccess = true;
        }

        if (loginSuccess) {
            wcout << L"\n\n\t\tIniciando...";
            for (int i = 0; i < 7; ++i) {
                wcout << L".";
                Sleep(300); // Espera 0.3 segundos entre cada punto
            }
            Sleep(1000); // Espera un segundo antes de continuar
            system("cls");
            wcout << L"\n\t\t¡BIENVENIDO AL PROGRAMA!\n";
            Sleep(2000); // Espera un segundo antes de continuar
            return true;
        } else {
            if (count_login == 2) {
                system("cls");
                system("color F4"); // Cambiar a fondo rojo y texto blanco para el mensaje de error
                wcout << L"\n\tERROR." << endl;
                wcout << L"\tIntentos fallidos. Intentelo mas tarde." << endl;
                return false;
            } else {
                wcout << L"\n\tUsuario o Contraseña incorrecto. Intentelo de nuevo." << endl;
                Sleep(1000);
            }
        }
    }
    return false;
}



	

bool loginProfesor(void) {
    setlocale(LC_ALL, "");

    wstring user, pass;
    wstring storedUser = L"docente";
    wstring storedPass = L"12345";
    bool loginSuccess = false;

    system("color 0A"); // Fondo negro (0), texto verde (A)

    for (int count_login = 0; count_login < 3; count_login++) {
        system("cls");
        setColor(14); // Amarillo
        wcout << L"\n\t\t  ===============================" << endl;
        wcout << L"\t\t |                               |" << endl;
        setColor(10);
        wcout << L"\t\t       BIENVENIDO DOCENTE      " << endl;
        setColor(14);
        wcout << L"\t\t |                               |" << endl;
        wcout << L"\t\t  ===============================" << endl;
        wcout << endl;
        setColor(10);
        wcout << L"\tIntentos restantes: " << 3 - count_login << endl << endl;
        wcout << L"\t\tUsuario: ";
        getline(wcin, user);
        wcout << L"\t\tContraseña: ";

        wchar_t clave;
        pass = L"";
        while ((clave = _getwch()) != 13) { // 13 es Enter
            if (clave == '\b') { // Caracter de retroceso
                if (!pass.empty()) {
                    wcout << L"\b \b"; // Borrar último asterisco en pantalla
                    pass.pop_back(); // Eliminar último carácter de la contraseña
                }
            } else {
                pass.push_back(clave);
                wcout << L"*";
            }
        }

        if (user == storedUser && pass == storedPass) {
            loginSuccess = true;
        }

        if (loginSuccess) {
            wcout << L"\n\n\t\tIniciando...";
            for (int i = 0; i < 7; ++i) {
                wcout << L".";
                Sleep(300); // Espera 0.3 segundos entre cada punto
            }
            Sleep(1000); // Espera un segundo antes de continuar
            system("cls");
            wcout << L"\n\t\t¡BIENVENIDO AL PROGRAMA!\n";
            Sleep(2000); // Espera un segundo antes de continuar
            return true;
        } else {
            if (count_login == 2) {
                system("cls");
                system("color F4"); // Cambiar a fondo rojo y texto blanco para el mensaje de error
                wcout << L"\n\tERROR." << endl;
                wcout << L"\tIntentos fallidos. Intentelo mas tarde." << endl;
                return false;
            } else {
                wcout << L"\n\tUsuario o password incorrecto. Intentelo de nuevo." << endl;
                Sleep(1000);
            }
        }
    }
    return false;
}



void menu(bool isDirector) {
    int opcion;
    do {    
        opcion = mainScreen(isDirector);
        VC_menu = action(opcion, isDirector);
        cout << endl;
    } while (VC_menu);
}

int mainScreen() {
    int opc;
    bool repetir;
    do {
        system("cls");
        system("color 0A");
        repetir = true;
        cout << "\n\t********** GESTOR DE ESTUDIANTES **********" << endl;
        cout << endl;
        cout << "\t\t(1) Agregar" << endl;
        cout << "\t\t(2) Mostrar" << endl;
        cout << "\t\t(3) Ordenar" << endl;
        cout << "\t\t(4) Buscar" << endl;
        cout << "\t\t(5) Eliminar" << endl;
        cout << "\t\t(6) Editar" << endl;
        cout << "\t\t(7) Guardar" << endl;
        cout << "\t\t(8) Salir" << endl;
        cout << "\n\t----- Seleccione una opcion: ";
        cin >> opc;
        cin.ignore();
        if (opc >= 1 && opc <= 8) {
            repetir = false;
        } else {
            cout << "Opcion no valida. Intentelo de nuevo." << endl;
            Sleep(1000);
        }
    } while (repetir);
    return opc;
}



int mainScreen(bool isDirector) {
    int opc;
    bool repetir;
    do {
        system("cls");
        system("color 0A");
        repetir = true;
        cout << "\n\t********** GESTOR DE ESTUDIANTES **********" << endl;
        cout << endl;

        if (isDirector) {
            cout << "\t\t(1) Mostrar" << endl;
            cout << "\t\t(2) Ordenar" << endl;
            cout << "\t\t(3) Guardar" << endl;
            cout << "\t\t(4) Salir" << endl;
        } else {
            cout << "\t\t(1) Agregar" << endl;
            cout << "\t\t(2) Mostrar" << endl;
            cout << "\t\t(3) Ordenar" << endl;
            cout << "\t\t(4) Buscar" << endl;
            cout << "\t\t(5) Eliminar" << endl;
            cout << "\t\t(6) Editar" << endl;
            cout << "\t\t(7) Guardar" << endl;
            cout << "\t\t(8) Salir" << endl;
        }

        cout << "\n\t----- Seleccione una opcion: ";
        cin >> opc;
        cin.ignore();

        if ((isDirector && opc >= 1 && opc <= 4) || (!isDirector && opc >= 1 && opc <= 8)) {
            repetir = false;
        } else {
            cout << "Opcion no valida. Intentelo de nuevo." << endl;
            Sleep(1000);
        }
    } while (repetir);

    return opc;
}



bool action(int opc) {
    switch (opc) {
        case 1: agregar(); break;
        case 2: mostrar(); break;
        case 3: ordenar(); break;
        case 4: buscar(); break;
        case 5: eliminar(); break;
        case 6: editar(); break;
        case 7:cout << "Datos guardados exitosamente." << endl;
        guardarDatos();  // Modificado
        Sleep(2000);
        break;
        case 8: cout << "\n\n\t\tSaliendo";
        for(int i = 0; i < 7; ++i) {
            cout << ".";
            Sleep(300); 
        }
        Sleep(1000); 
        exit(0);
        default: cout << "ERROR, algo salio mal." << endl;
    }
    return true;
}


bool action(int opc, bool isDirector) {
    if (isDirector) {
        switch (opc) {
            case 1: mostrar(); break;
            case 2: ordenar(); break;
            case 3: cout << "Datos guardados exitosamente." << endl;
			guardarDatos();  // Modificado
            
            Sleep(2000);
            break;
            case 4: cout << "\n\n\t\tSaliendo";
            for(int i = 0; i < 7; ++i) {
                cout << ".";
                Sleep(300); 
            }
            Sleep(1000); 
            exit(0);
            default: cout << "ERROR, algo salio mal." << endl;
        }
    } else {
        switch (opc) {
            case 1: agregar(); break;
            case 2: mostrar(); break;
            case 3: ordenar(); break;
            case 4: buscar(); break;
            case 5: eliminar(); break;
            case 6: editar(); break;
            case 7:cout << "Datos guardados exitosamente." << endl;
			guardarDatos();  // Modificado
            
            Sleep(2000);
            break;
            case 8: cout << "\n\n\t\tSaliendo";
            for(int i = 0; i < 7; ++i) {
                cout << ".";
                Sleep(300); 
            }
            Sleep(1000); 
            exit(0);
            default: 
            cout<<"ERROR,algo salio mal"<<endl;
        }
    }
    return true;
}


void agregar(void){
	
	for(int i = 0; i < 7; ++i) {
		
        cout << ".";
        Sleep(200); // Espera 1 segundo entre cada punto
    }
	
    system("cls");
    cout<<"\n\t# OPCION 1: AGREGAR"<<endl<<endl;
    if(count >= 40){
        cout<<"\t\t(Tope alcanzado)."<<endl;
        getch();
        return;
    }
    typeEstudiante aux;
    cin.ignore(); 
    cout<<"\t\tEstudiante: ";        getline(cin, aux.nombre);
    cout<<"\t\tApellido: ";        getline(cin, aux.apellido);
    
    do {
        cout<<"\t\tEdad : ";
        cin>>aux.edad;
        if(aux.edad < 15 || aux.edad >= 100) {
            cout<<"\t\tError: Edad fuera del rango permitido. Intentelo de nuevo.\n"<<endl
			;	
		}
    } while(aux.edad < 15 || aux.edad >= 100);
    
    do {
        cout<<"\t\tPromedio (no mayor a 20): ";
        cin>>aux.promedio;
        if(aux.promedio < 0 || aux.promedio > 20) {
            cout<<"\t\tError: Promedio fuera del rango permitido. Intentelo de nuevo.\n";
        }
    } while(aux.promedio < 0 || aux.promedio > 20);
    
    cout<<endl;
    for(int i = 0; i < 7; ++i) {
        cout << ".";
        Sleep(200); // Espera 1 segundo entre cada punto
    }
    cout<<"Agregando Estudiante....";
    for(int i = 0; i < 7; ++i) {
        cout << ".";
        Sleep(200); // Espera 1 segundo entre cada punto
    }
    cout<<endl;
    cout<<"\n\t\t>>>>>>>> Guardado >>>>>>>>"<<endl;
    
        Sleep(1000); // Espera 1 segundo entre cada punto
    
    
    alumno[count] = aux;
    count++;
    
    Sleep(1000);
    
}

void mostrar(void) {
    for (int i = 0; i < 7; ++i) {
        cout << ".";
        Sleep(200); // Espera 0.2 segundos entre cada punto
    }

    system("cls");
    cout << "\n\t# OPCION 2: MOSTRAR" << endl << endl;

    ifstream file("estudiantes.csv");
    if (!file.is_open()) {
        cout << "\t(No se pudo abrir el archivo)." << endl;
        getch();
        return;
    }

    string nombre, apellido;
    int edad;
    float promedio;
    bool hay_estudiantes = false;

    while (getline(file, nombre) && getline(file, apellido) && file >> edad && file >> promedio) {
        file.ignore(); // Ignorar el salto de línea después de leer el promedio
        hay_estudiantes = true;
        cout << "\t\tEstudiante: " << nombre << " " << apellido << endl;
        cout << "\t\tEdad: " << edad << endl;
        cout << "\t\tPromedio: " << promedio << endl;
        cout << endl;
    }

    if (!hay_estudiantes) {
        cout << "\t(Vacio)." << endl;
    }

    file.close();

    while (true) {
        cout << "\n\tPresione 1 para volver a la gestion de estudiantes: ";
        char opcion = getch(); // Obtener entrada del usuario sin necesidad de presionar Enter

        if (opcion == '1') {
            // Mostrar el número 1 y luego pedir que presione Enter
            cout << "\n\t1";
            cout << "\n\tPresione Enter para continuar...";
            while (getch() != '\r'); // Esperar a que se presione Enter

            // Animación de salida
            cout << "\n\tSaliendo...";
            for (int i = 0; i < 7; ++i) {
                cout << ".";
                Sleep(300); // Espera 0.3 segundos entre cada punto
            }
            cout << endl;

            // Limpieza y regreso al menú principal
            system("cls");
            cout << "\n\tRegresando al menu................." << endl;
            Sleep(2000); // Espera 2 segundos antes de limpiar la pantalla y regresar

            // Llamar a la función del menú principal aquí si es necesario
            // Por ejemplo, si tienes una función `mainScreen()`, la puedes llamar aquí.
            // mainScreen();
            return;
        }
    }
}

void ordenar() {
    // Simula una carga
    for(int i = 0; i < 7; ++i) {
        cout << ".";
        Sleep(200); // Espera 200 ms entre cada punto
    }

    system("cls");
    cout << "\n\t# OPCION 2: ORDENAR" << endl << endl;
    if(count == 0) {
        cout << "\t\t(Vacio)." << endl;
        getch();
        return;
    }
    cout << "\t\t>> Ordenando..." << endl;
    typeEstudiante mayor;
    int k;
    for(int i = 0; i < count - 1; i++) {
        mayor = alumno[i];
        k = i;
        for(int j = i + 1; j < count; j++) {
            if(mayor.promedio < alumno[j].promedio) {
                mayor = alumno[j];
                k = j;
            }
        }
        alumno[k] = alumno[i];
        alumno[i] = mayor;
    }
    cout << "\t\t>> Ordenado correctamente!" << endl;
    getch();
}

void buscar(void){
	
	for(int i = 0; i < 7; ++i) {
        cout << ".";
        Sleep(200); // Espera 1 segundo entre cada punto
    }
	
    system("cls");
    cout<<"\n\t# OPCION 4: BUSCAR"<<endl<<endl;
    if(count == 0){
        cout<<"\n\t\t(Vacio)."<<endl;
        getch();
        return;
    }
    string nombre, apellido;
    cin.ignore(); 
    cout<<"\t\tDigitar nombre: ";        getline(cin, nombre);
    cout<<"\t\tDigitar apellido: ";    getline(cin, apellido);
    bool found = false;
    for(int i = 0; i < count; i++){
        if ((alumno[i].nombre == nombre) && (alumno[i].apellido == apellido)){
            cout<<"\n\t\tEstudiante: "<<alumno[i].nombre<<" "<<alumno[i].apellido<<endl;
            cout<<"\t\tEdad: "<<alumno[i].edad<<endl;
            cout<<"\t\tPromedio: "<<alumno[i].promedio<<endl;
            found = true;
            break;
        }
    }
    if (!found) cout<<"\n\t\tEstudiante no encontrado."<<endl<<endl;
    getch();
}

void eliminar(void){
    for(int i = 0; i < 7; ++i) {
        cout << ".";
        Sleep(200); // Espera 1 segundo entre cada punto
    }

    system("cls");
    cout << "\n\t# OPCION 5: ELIMINAR" << endl << endl;
    if(count == 0){
        cout << "\t\t(Vacio)." << endl;
        getch();
        return;
    }

    int opcion;
    cout << "\t\tSeleccione una opcion:" << endl;
    cout << "\t\t(1) Eliminar todo el registro" << endl;
    cout << "\t\t(2) Eliminar un estudiante especifico" << endl;
    cout << "\t\t(3) Volver al menu principal" << endl;
    cout << "\t\tOpcion: ";
    cin >> opcion;
    cin.ignore(); // Ignorar el salto de línea después de la opción

    if (opcion == 1) {
        count = 0;
        cout << "\n\t\tTodos los registros han sido eliminados." << endl;
    } else if (opcion == 2) {
        string nombre, apellido;
        bool listo = false;
        cout << "\t\tDigitar nombre: ";        getline(cin, nombre);
        cout << "\t\tDigitar apellido: ";    getline(cin, apellido);
        for(int i = 0; i < count; i++){
            if((alumno[i].nombre == nombre) && (alumno[i].apellido == apellido)){
                for(int j = i; j < count - 1; j++)
                    alumno[j] = alumno[j + 1];
                count--;
                cout << "\n\t\t>> Eliminando..." << endl;
                listo = true;
                break;
            }
        }
        if(!listo) cout << "\n\t\tEstudiante no encontrado." << endl << endl;
    } else if (opcion == 3) {
        
        cout << "\n\n\t\tCargando..."; /*ANIMACIÓN IMPORTANTE */
        for(int i = 0; i < 7; ++i) {
                    cout << ".";
                    Sleep(300); 
                }
                Sleep(1000); 
                return ;       /* HASTA AQUI */
    }else{
        cout << "\n\t\tOpcion invalida." << endl;
    }
    getch();
}

void editar(void){
	
	for(int i = 0; i < 7; ++i) {
        cout << ".";
        Sleep(200); // Espera 1 segundo entre cada punto
    }
	
    system("cls");
    cout<<"\n\t# OPCION 6: EDITAR"<<endl<<endl;
    if(count == 0){
        cout<<"\t(Vacio)."<<endl;
        getch();
        return;
    }
    string nombre, apellido;
    cin.ignore();
    cout<<"\t\tDigitar nombre: ";        getline(cin, nombre);
    cout<<"\t\tDigitar apellido: ";    getline(cin, apellido);
    for(int i = 0; i < count; i++){
        if ((alumno[i].nombre == nombre) && (alumno[i].apellido == apellido)){
            cout<<"\t\tNuevo Nombre: ";        getline(cin, alumno[i].nombre);
            cout<<"\t\tNuevo Apellido: ";      getline(cin, alumno[i].apellido);
            do{
                cout<<"\t\tNueva Edad: ";        cin>>alumno[i].edad;
            } while(alumno[i].edad < 15 || alumno[i].edad >= 100);
            do{
                cout<<"\t\tNuevo Promedio: ";    cin>>alumno[i].promedio;
            } while(alumno[i].promedio < 0 || alumno[i].promedio > 20);
            
            cout << "\n\n\t\tEditando..."; /*ANIMACIÓN IMPORTANTE */
        for(int i = 0; i < 7; ++i) {
                    cout << ".";
                    Sleep(300); 
                }
                Sleep(1000); 
                return ;
        }
    }
    cout<<"\n\t\tEstudiante no encontrado."<<endl<<endl;
    getch();
}

void guardarDatos(void) {
    ofstream file("estudiantes.csv");
    if (file.is_open()) {
        for (int i = 0; i < count; i++) {
       
            file << alumno[i].nombre << "\n";
            cout<<endl;
            file << alumno[i].apellido << "\n";
            cout<<endl;
            file <<alumno[i].edad << "\n";
            cout<<endl;
            file <<alumno[i].promedio << "\n";
        }
        file.close();
    } else {
        cout << "No se pudo abrir el archivo para guardar los datos." << endl;
    }
}


void cargarDatos(void){
    ifstream file("estudiantes.csv");
    if(!file.is_open()) return;
    
    count = 0; 
    while(count < 40 && !file.eof()){
        typeEstudiante aux;
        getline(file, aux.nombre);
        if(aux.nombre.empty()) break; 
        getline(file, aux.apellido);
        file >> aux.edad;
        file >> aux.promedio;
        file.ignore();
        alumno[count++] = aux;
        
        
    }
    file.close();
}
