# interface-verduras

import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

// Definición de la interfaz Producto
interface Producto {
    double getPrecio();
}

// Clase para representar una verdura
class Verdura implements Producto {
    private String nombre;
    private double precio;

    public Verdura(String nombre, double precio) {
        this.nombre = nombre;
        this.precio = precio;
    }

    public double getPrecio() {
        return precio;
    }

    @Override
    public String toString() {
        return nombre + " - $" + precio;
    }
}

// Clase principal de la aplicación
public class VentaVerdurasApp {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Map<String, Producto> inventario = new HashMap<>();

        // Agregar algunas verduras al inventario
        inventario.put("Tomate", new Verdura("Tomate", 1.5));
        inventario.put("Zanahoria", new Verdura("Zanahoria", 0.75));
        inventario.put("Espinaca", new Verdura("Espinaca", 2.0));

        while (true) {
            System.out.println("Inventario de Verduras:");
            for (Producto producto : inventario.values()) {
                System.out.println(producto);
            }

            System.out.print("¿Qué verdura quieres comprar? (Escribe 'salir' para terminar): ");
            String opcion = scanner.nextLine();

            if (opcion.equalsIgnoreCase("salir")) {
                break;
            }

            Producto seleccion = inventario.get(opcion);
            if (seleccion != null) {
                System.out.println("Has seleccionado: " + seleccion);
                System.out.print("¿Cuántas unidades deseas comprar? ");
                int cantidad = scanner.nextInt();
                scanner.nextLine();  // Limpiar el buffer

                double total = cantidad * seleccion.getPrecio();
                System.out.println("Total a pagar: $" + total);
            } else {
                System.out.println("Verdura no encontrada en el inventario.");
            }
        }

        System.out.println("Gracias por tu compra. ¡Vuelve pronto!");
        scanner.close();
    }
}
