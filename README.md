package com.mycompany.egresos;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Scanner;


public class Egresos {

   public static void main(String[] args) {
        // Creo un objeto Scanner para leer la entrada del usuario
        Scanner scanner = new Scanner(System.in);
        int opcion;

        // Uso un bucle do-while para mostrar el menú hasta que el usuario elija salir
        do {
            // Muestro el menú de opciones
            System.out.println("\nMenú de Registro de Egresos");
            System.out.println("1. Registrar Egreso");
            System.out.println("2. Ver Registros de Egresos");
            System.out.println("3. Salir");
            System.out.print("Seleccione una opción: ");

            // Leo la opción seleccionada por el usuario
            opcion = scanner.nextInt();
            scanner.nextLine(); // Consumo el salto de línea después de leer el entero

            // Uso un switch para manejar la opción seleccionada
            switch (opcion) {
                case 1:
                    registrarEgreso(scanner); // Llamo al método para registrar un egreso
                    break;
                case 2:
                    verRegistrosEgresos(); // Llamo al método para ver los registros
                    break;
                case 3:
                    System.out.println("Saliendo del programa..."); // Muestro mensaje de salida
                    break;
                default:
                    System.out.println("Opción no válida. Intente de nuevo."); // Muestro mensaje para opción no válida
            }
        } while (opcion != 3); // Continúo hasta que el usuario elija salir

        // Cierro el objeto Scanner
        scanner.close();
    }

    // Método para registrar un nuevo egreso
    private static void registrarEgreso(Scanner scanner) {
        System.out.println("\nRegistro de Egresos");
        System.out.println("Por favor, ingrese los datos del egreso:");

        // Pido al usuario que ingrese los datos del egreso
        System.out.print("Correlativo del egreso: ");
        String correlativo = scanner.nextLine();

        System.out.print("ID de la cuenta bancaria: ");
        String idCuenta = scanner.nextLine();

        System.out.print("Monto del egreso: ");
        String monto = scanner.nextLine();

        System.out.print("Descripción del egreso: ");
        String descripcion = scanner.nextLine();

        System.out.print("Fecha de registro del egreso (dd/mm/yyyy): ");
        String fecha = scanner.nextLine();

        // Formateo los datos del egreso en una línea de texto
        String registro = String.format("%s,%s,%s,%s,%s", correlativo, idCuenta, monto, descripcion, fecha);

        // Escribo el registro en el archivo "Egresos.txt"
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("Egresos.txt", true))) {
            writer.write(registro);
            writer.newLine(); // Añado una nueva línea para el siguiente registro
            System.out.println("Egreso registrado exitosamente.");
        } catch (IOException e) {
            // Manejo errores al escribir en el archivo
            System.err.println("Error al escribir en el archivo: " + e.getMessage());
        }
    }

    // Método para ver los registros existentes
    private static void verRegistrosEgresos() {
        System.out.println("\nRegistros de Egresos:");

        // Leo y muestro los registros del archivo "Egresos.txt"
        try (BufferedReader reader = new BufferedReader(new FileReader("Egresos.txt"))) {
            String linea;
            while ((linea = reader.readLine()) != null) {
                System.out.println(linea);
            }
        } catch (IOException e) {
            // Manejo errores al leer el archivo
            System.err.println("Error al leer el archivo: " + e.getMessage());
        }
    }
}
