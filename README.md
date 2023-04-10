# CleanCode
Corrección de un ejercicio de examen sobre arrays de la segunda evaluación.
En este ejercicio nos piden el dis y mes para poder reservar un asiento.

```
public static void main(String[] args) {
        /*
        Pedir un día y un mes, y comprobar que es correcto. Consideramos que febrero tiene siempre 28 días.
         */
        Scanner sc = new Scanner(System.in);
        int dia = 0;
        int mes = 0;

        // Creamos un Array con los días del mes
        int[] diaMes ={31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

        boolean fechaCorrecta = false;
        do {
            System.out.println("Dia: ");
            dia = sc.nextInt();
            sc.nextLine();

            System.out.println("Mes: ");
            mes = sc.nextInt();
            sc.nextLine();

            // Comprobamos si la fecha es correcta
            if (mes >= 1 && mes <=12 && dia >= 1 && dia <= diaMes[mes - 1]){
                System.out.println("La fecha está correcta");
                // Cambiamos la fecha a correcta para salir del bucle
                fechaCorrecta = true;
            } else {
                System.out.println("La fecha es incorrecta. Vuelva a introducir la fecha");
                fechaCorrecta = false;
            }
        } while (!fechaCorrecta);

        /*
        A continuación, se muestra un mensaje como el siguiente, en el que se indica el mes con letras:
         */

        String [] mesLetra = {"Enero" , "Febrero" ,  "Marzo" ,  "Abril" ,  "Mayo" ,  "Junio" ,  "Julio" ,  "Agosto" ,  "Septiembre" ,  "Octubre" ,  "Noviembre" ,  "Diciembre"};
        System.out.println("Los asientos disponibles para el día " + dia + " de " + mesLetra[mes - 1] + " son: ");
        System.out.println("--------------------------------------------------------------------");

        /*
        Los asientos están representados por un array bidimensional de caracteres, de tamaño 4x4, donde una L indica que el asiento está libre, y una X indica que está ocupado. Inicialmente, algunos asientos están libres y otros ocupados:
         */

        char [][]asientos = new char[4][4];
        for (int i = 0; i < asientos.length; i++) {
            for (int j = 0; j < asientos[i].length; j++) {
                asientos[i][j] = 'L';
            }
        }

        // Ponemos algunos ocupados
        asientos[0][1] = 'X';
        asientos[1][1] = 'X';
        asientos[1][2] = 'X';

        // Imprimimos los asientos.
        for (int i = 0; i < asientos.length; i++) {
            for (int j = 0; j < asientos[i].length; j++) {
                System.out.print(asientos[i][j] + "\t");
            }
            System.out.println();
        }
        System.out.println("--------------------------------------------------------------------");

        /*
        Se pide al usuario que indique fila y asiento, controlando que la respuesta esté dentro del rango:
         */

        // Escogemos la fila
        int fila = 0;
        do{
            System.out.println("Elige fila (0 - 4)");
            fila = sc.nextInt();
            if (fila < 0 || fila > 4) {
                System.out.println("Fuera de rango. Por favor, introduce un valor válido entre 0 y 4");
            }
        } while (fila < 0 || fila > 4);

        // Ahora escogemos el asiento
        int asiento = 0;
        do{
            System.out.println("Elige asiento (0 - 4)");
            asiento = sc.nextInt();
            if (asiento < 0 || asiento > 4){
                System.out.println("Fuera de rango. Por favor, introduce un valor válido entre 0 y 4");
            }
        } while (asiento < 0 || asiento > 4);

        /*
        Una vez seleccionados fila y asiento, se comprueba si en esa posición el asiento está ocupado.
         */
        if (asientos[fila][asiento] == 'L'){
            asientos[fila][asiento] = 'X';
            System.out.println("Se te ha asignado el asiento solicitado :)");
            for (int i = 0; i < asientos.length; i++) {
                for (int j = 0; j < asientos[i].length; j++) {
                    System.out.print(asientos[i][j] + "\t");
                }
                System.out.println();
            }
        } else {
            System.out.println("El asiento está ocupado. Tendrás que empezar de nuevo");
        }
    }
```

Lo que vamos a corregir en este código es:
#### 1. Nombres:
Los nombres deben ser legibles, significativos y que explique por si mismos la función que hace el código

#### 2. Bloques y sangrado: 
Los bloques en instrucciones if, else, while y similares deben tener una línea.
 - El if se puede reducir con el operador ternario, sintaxis: resultado = condición ? valor_si_se_cumple : valor_si_no_se_cumple
 - Los for se pueden poner como foreach.

#### 3. Comentarios:
Es mejor usar un código autoexplicativo, dando nombres descriptivos donde se entienda el código.

#### 4. Constantes:
Usamos las variables dia y mes como final porque sabemos que no van a variar.

#### 3. Evitar repeticiones:
Intentar evitar las repeticiones de código utilizando métodos
```
public class EjercicioExamen {
    public static final int[] diaPorMes ={31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
    public static final String [] mesLetra = {"Enero" , "Febrero" ,  "Marzo" ,  "Abril" ,  "Mayo" ,  "Junio" ,  "Julio" ,  "Agosto" ,  "Septiembre" ,  "Octubre" ,  "Noviembre" ,  "Diciembre"};
    static Scanner sc = new Scanner(System.in);
    public static void main(String[] args) {
        int dia, mes;

        boolean fechaCorrecta;
        do {
            System.out.println("Introduce el día: ");
            dia = sc.nextInt();

            System.out.println("Introduce el mes: ");
            mes = sc.nextInt();

            fechaCorrecta = mes >= 1 && mes <= 12 && dia >= 1 && dia <= diaPorMes[mes - 1];
            System.out.println(fechaCorrecta ? "La fecha está correcta" : "La fecha es incorrecta. Vuelva a introducir la fecha");
        } while (!fechaCorrecta);

        char [][]asientos = new char[4][4];
        for (char[] fila : asientos) {
            java.util.Arrays.fill(fila, 'L');
        }

        // Ponemos algunos asientos como ocupados
        asientos[0][1] = 'X';
        asientos[1][1] = 'X';
        asientos[1][2] = 'X';

        // Se muestran los asientos disponibles
        System.out.println("Los asientos disponibles para el día " + dia + " de " + mesLetra[mes - 1] + " son: ");
        mostrarAsientos(asientos);

        // Reservar asiento
        int fila;
        do{
            System.out.println("Elige fila (0 - 3)");
            fila = sc.nextInt();
            System.out.println(fila < 0 || fila > 3 ? "Fuera de rango. Por favor, introduce un valor válido entre 0 y 4" : "");
        } while (fila < 0 || fila > 3);
        
        int asiento;
        do{
            System.out.println("Elige asiento (0 - 3)");
            asiento = sc.nextInt();
            System.out.println(fila < 0 || fila > 3 ? "Fuera de rango. Por favor, introduce un valor válido entre 0 y 4" : "");
        } while (asiento < 0 || asiento > 3);

        if (asientos[fila][asiento] == 'L'){
            asientos[fila][asiento] = 'X';
            System.out.println("Se te ha asignado el asiento solicitado.");
            mostrarAsientos(asientos);
        } else {
            System.out.println("El asiento está ocupado. Tendrás que empezar de nuevo");
        }
    }
    private static void mostrarAsientos(char[][] asientos) {
        for (char[] fila : asientos) {
            for (char asiento : fila) {
                System.out.print(asiento + "\t");
            }
            System.out.println();
        }
    }
}
```