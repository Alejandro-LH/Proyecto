## Universidad de Colima
### FIME 
### ICI
### Mstro. Walter Alexander Mata Lopez
### Almn. Jahir Alejandro Lopez
### 2B

## PROYECTO FINAL

### class Registro:
```dart
  class Registro {
  int id;
  String nombre;
  String aPaterno;
  String aMaterno;
  String correo;

  Registro(this.id, this.nombre, this.aPaterno, this.aMaterno, this.correo);

  @override
  String toString() {
    return "ID: ${this.id}\nNombre: ${this.nombre}\nApellido Paterno: ${this.aPaterno}\nApellido Materno: ${this.aMaterno}\nCorreo: ${this.correo}";
  }
}
```

### class Maestro:
``` dart
import 'Registro.dart';

class Maestro extends Registro {
  Maestro(
      int id, String nombre, String aPaterno, String aMaterno, String correo)
      : super(id, nombre, aPaterno, aMaterno, correo);

  @override
  String toString() {
    return "ID: ${this.id}\nNombre: ${this.nombre}\nApellido Paterno: ${this.aPaterno}\nApellido Materno: ${this.aMaterno}\nCorreo: ${this.correo}\nTipo: Maestro";
  }
}

```

### class Alumno:
```dart
import 'Registro.dart';

class Alumno extends Registro {
  Alumno(int id, String nombre, String aPaterno, String aMaterno, String correo)
      : super(id, nombre, aPaterno, aMaterno, correo);

  @override
  String toString() {
    return "ID: ${this.id}\nNombre: ${this.nombre}\nApellido Paterno: ${this.aPaterno}\nApellido Materno: ${this.aMaterno}\nCorreo: ${this.correo}\nTipo: Alumno";
  }
}

```

### main:
``` dart
import 'dart:io';
import 'Registro.dart';
import 'Maestro.dart';
import 'Alumno.dart';

String g = "-"; //Guiones para separar los menús.
int n = 90; //Número de guiones.

void main() {
  Directorio directorio = Directorio();
  while (true) { //Ciclo infinito para que el menú se repita.
    print("");
    print("\"Bienvenido a la base de datos de la Universidad de Colima\"");
    print("");
    print("\"Ingrese una opción que desea realizar\"");
    print("");
    print("1. Crear nuevo registro");
    print("2. Leer y presentar los registros");
    print("3. Actualizar los datos");
    print("4. Eliminar registros");
    print("5. Salir del programa");

    stdout.write('\nIngrese una opción:\n ');  //Solicita una opción al usuario y la guarda en la variable opcion.
    print("");
    String? opcion = stdin.readLineSync(); //Lee la opción ingresada por el usuario.

    switch (opcion) {
      case '1': //Si la opción es 1, manda a llamar a la función crearRegistro.
        directorio.crearRegistro();
        break; 
      case '2': //Si la opción es 2, manda a llamar a la función leerRegistros.
        directorio.leerRegistros();
        break; 
      case '3': //Si la opción es 3, manda a llamar a la función actualizarRegistro.
        directorio.actualizarRegistro();
        break;
      case '4': //Si la opción es 4, manda a llamar a la función eliminarRegistro.
        directorio.eliminarRegistro();
        break;
      case '5': //Si la opción es 5, termina el programa.
        return; //Termina el programa.
      default: //Si la opción no es ninguna de las anteriores, muestra un mensaje de error.
        print('\nOpción inválida. Inténtelo nuevamente.');
        break; //Termina el case.
    }
    print(''); 
  }
}

class Directorio {
  List<Registro> registros = []; //Lista de registros.
  int contadorMaestros = 0; //Contador de maestros para asignar ID.
  int contadorAlumnos = 0; //Contador de alumnos para asignar ID.

  void crearRegistro() {
    print(g * n); //Imprime guiones.
    print("\n\"Menú de Creación\"\n");
    stdout.write("Ingrese el nombre: "); //Solicita el nombre al usuario.
    String? nombre = stdin.readLineSync(); //Lee el nombre ingresado por el usuario.
    stdout.write("Ingrese el apellido paterno: "); //Solicita el apellido paterno al usuario.
    String? apellidoPaterno = stdin.readLineSync(); //Lee el apellido paterno ingresado por el usuario.
    stdout.write("Ingrese el apellido materno: "); //Solicita el apellido materno al usuario.
    String? apellidoMaterno = stdin.readLineSync(); //Lee el apellido materno ingresado por el usuario.
    stdout.write("Ingrese el correo: "); //Solicita el correo al usuario.
    String? correo = stdin.readLineSync(); //Lee el correo ingresado por el usuario.
    print("");
    int id; //Variable para guardar el ID del registro.
    String tipo = seleccionarTipo(); //Llama a la función seleccionarTipo y guarda el valor de retorno en la variable tipo.

    if (tipo == 'Maestro') {
      contadorMaestros++; //Incrementa el contador de maestros.
      id = contadorMaestros; //Asigna el valor del contador de maestros a la variable id.
      Maestro maestro =
          Maestro(id, nombre!, apellidoPaterno!, apellidoMaterno!, correo!); //Crea un objeto de la clase Maestro con los datos ingresados por el usuario.
      registros.add(maestro); //Agrega el objeto maestro a la lista de registros.
    } else { //Si el tipo es alumno, se ejecuta el siguiente bloque.
      contadorAlumnos++; //Incrementa el contador de alumnos.
      id = contadorAlumnos; //Asigna el valor del contador de alumnos a la variable id.
      Alumno alumno = 
          Alumno(id, nombre!, apellidoPaterno!, apellidoMaterno!, correo!); //Crea un objeto de la clase Alumno con los datos ingresados por el usuario.
      registros.add(alumno); //Agrega el objeto alumno a la lista de registros.
    }

    print("");
    print('\"Registro creado exitosamente\"');
    print("");    
    print(g * n);
    print("");

    //Imprimir detalles del último registro
    Registro registro = registros.last; //Guarda el último registro en la variable registro.
    print(registro); //Imprime los datos del registro.
  }

  String seleccionarTipo() {
     print(g * n);
    while (true) {
      print("\n\"Seleccione el tipo de usuario que es\":\n");
      print("1. Maestro");
      print("2. Alumno\n");
      stdout.write(""); //Solicita una opción al usuario y la guarda en la variable opcion.
    
      String? opcion = stdin.readLineSync(); //Lee la opción ingresada por el usuario y la guarda en la variable opcion.
      if (opcion == '1') { //Si la opción es 1, retorna el valor 'Maestro'.
        return 'Maestro';
      } else if (opcion == '2') { //Si la opción es 2, retorna el valor 'Alumno'.
        return 'Alumno'; 
      } else { //Si la opción no es ninguna de las anteriores, muestra un mensaje de error.
        print('Opción inválida. Inténtelo nuevamente.');
      }
    }
  }

  void leerRegistros() {
    if (registros.isEmpty) { //Si la lista de registros está vacía, muestra un mensaje de error.
      print("\nEl directorio está vacío.");
    } else { //Si la lista de registros no está vacía, muestra el menú de lectura.
      print(g * n);
      print("\n\"Menú de Lectura\"\n");
      print("1. Leer todos los registros");
      print("2. Leer registros de Maestros");
      print("3. Leer registros de alumnos\n");
      stdout.write("Ingrese una opción: "); //Solicita una opción al usuario y la guarda en la variable opcion.
      String? opcion = stdin.readLineSync(); //Lee la opción ingresada por el usuario y la guarda en la variable opcion.

      switch (opcion) { 
        case '1': //Si la opción es 1, muestra todos los registros.
        print(g * n);
          print("\n\"Todos los registros\"\n");
          mostrarRegistros(registros); //Llama a la función mostrarRegistros y le pasa como parámetro la lista de registros.
          break;
        case '2': //Si la opción es 2, muestra los registros de maestros.
        print(g * n);
          print("\n\"Registros de Maestros\"\n");
          List<Registro> profesores =
              registros.where((registro) => registro is Maestro).toList(); //Guarda los registros de maestros en la variable profesores.
          mostrarRegistros(profesores); //Llama a la función mostrarRegistros y le pasa como parámetro la lista de profesores.
          break;
        case '3':  //Si la opción es 3, muestra los registros de alumnos.
        print(g * n);
          print("\n\"Registros de alumnos\"\n");
          List<Registro> alumnos =
              registros.where((registro) => registro is Alumno).toList(); //Guarda los registros de alumnos en la variable alumnos.
          mostrarRegistros(alumnos);
          break;
        default:
          print("Opción inválida. Inténtelo nuevamente.\n");
          break; //Termina el case.
      }
    }
  }

  void mostrarRegistros(List<Registro> registros) {
    print(g * n);
      if (registros.isEmpty) { //Si la lista de registros está vacía, muestra un mensaje de error.
      print('No se encontraron registros.\n');
      } else { //Si la lista de registros no está vacía, muestra los registros.
      for (Registro registro in registros) {
        print(registro);
        print(g * n);
      }
    }
  }

  void actualizarRegistro() {
     print(g * n);
      if (registros.isEmpty) { //Si la lista de registros está vacía, muestra un mensaje de error.
      print("\nEl directorio está vacío.");
    } else {  //Si la lista de registros no está vacía, muestra el menú de actualización.
      print("\n\"Bienvenido al menú de actualización\'\n");
      print("Ingrese el ID del registro a actualizar: ");
      stdout.write("");
      String? id = stdin.readLineSync(); //Lee el ID ingresado por el usuario y lo guarda en la variable id.
      // ignore: null_check_always_fails 
      Registro? registro =
          registros.firstWhere((registro) => registro.id.toString() == id, //Busca el registro con el ID ingresado por el usuario y lo guarda en la variable registro.
              // ignore: null_check_always_fails
              orElse: () => null!);

        // ignore: unnecessary_null_comparison
        if (registro != null) { //Si el registro es diferente de nulo, muestra los datos del registro.
        stdout.write("Ingrese el nuevo nombre: ");
        String? nombre = stdin.readLineSync(); //Lee el nuevo nombre ingresado por el usuario y lo guarda en la variable nombre.
        registro.nombre = nombre!;
        stdout.write("Ingrese el nuevo apellido paterno: ");
        String? aPaterno = stdin.readLineSync(); //Lee el nuevo apellido paterno ingresado por el usuario y lo guarda en la variable aPaterno.
        registro.aPaterno = aPaterno!;
        stdout.write("Ingrese el nuevo apellido materno: ");
        String? aMaterno = stdin.readLineSync(); //Lee el nuevo apellido materno ingresado por el usuario y lo guarda en la variable aMaterno.
        registro.aMaterno = aMaterno!;
        stdout.write("Ingrese el nuevo correo electrónico: ");
        String? correo = stdin.readLineSync(); //Lee el nuevo correo ingresado por el usuario y lo guarda en la variable correo.
        registro.correo = correo!;
        print("Registro actualizado exitosamente.\n");
      } else { //Si el registro es nulo, muestra un mensaje de error.
        print("No se encontró ningún registro con ese ID.\n");
      }
    }
  }

  void eliminarRegistro() {
      print(g * n);
      if (registros.isEmpty) { //Si la lista de registros está vacía, muestra un mensaje de error.
      print("\nEl directorio está vacío.\n");
    } else { //Si la lista de registros no está vacía, muestra el menú de eliminación.
      print("\n\"Bienvenido al menú de eliminación\"\n");
      print("\nIngrese el ID del registro a eliminar: \n");
      stdout.write("");
      String? id = stdin.readLineSync(); //Lee el ID ingresado por el usuario y lo guarda en la variable id.
      registros.removeWhere((registro) => registro.id.toString() == id); //Elimina el registro con el ID ingresado por el usuario.
      print("Registro eliminado exitosamente.");
    }
  }
}
```

### Crear:

![crear](https://github.com/Alejandro-LH/Proyecto/assets/113395327/3cb12fdc-7562-4a0b-86e0-d1e74ff84dfd)

### Leer:

![leer](https://github.com/Alejandro-LH/Proyecto/assets/113395327/8530aa91-6aaa-44d2-8195-abbd4f7a111d)

### Actualizar:

![actualizar](https://github.com/Alejandro-LH/Proyecto/assets/113395327/3377cb45-32b0-435b-b308-d1c69f974414)

### Borrar:

![eliminar](https://github.com/Alejandro-LH/Proyecto/assets/113395327/96de4983-69bd-48ec-ab9b-358bdc430e55)

