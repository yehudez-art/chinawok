import java.util.Scanner;
import java.time.YearMonth;
import java.time.format.DateTimeFormatter;
import java.time.format.DateTimeParseException;
import java.util.ArrayList;
import java.time.LocalDate;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Random;

public class Chinawok {

    public static String productoNombre = "";
    public static double productoPrecio = 0.0;
    public static int cantidadLlevar = 0;

    public static String clienteNombre = "";
    public static String clienteApellido = "";
    public static String clienteDni = "";
    public static String clienteTelefono = "";
    public static String clienteCorreo = "";
    public static String Clientecontraseña = "";
    public static double totalPagar = 0.0;
    public static String tiendaSeleccionada = "";
    public static String metodoPagoSeleccionado = "";
    public static double montoPagadoCon = 0.0;
    public static double vueltoEntregar = 0.0;

    static ArrayList<String> losMasVendidos = new ArrayList<>();
    static ArrayList<Double> precioLosMasVendidos = new ArrayList<>();
    static ArrayList<String> carritoProductos = new ArrayList<>();
    static ArrayList<Integer> carritoCantidades = new ArrayList<>();
    static ArrayList<Double> carritoSubtotales = new ArrayList<>();
    static ArrayList<String> combosPersonales = new ArrayList<>();
    static ArrayList<Double> precioCombosPersonales = new ArrayList<>();
    static ArrayList<String> paraCompartir = new ArrayList<>();
    static ArrayList<Double> precioParaCompartir = new ArrayList<>();
    static ArrayList<String> festivalMostrazo = new ArrayList<>();
    static ArrayList<Double> precioFestivalMostrazo = new ArrayList<>();

    public static String ADMIN_CORREO = "admin@chinawok.com";
    public static String ADMIN_CONTRASEÑA = "Admin123";
    static boolean esadmin=false;
    static boolean esUsuario=false;

    public static String usuarioLogueado = "Invitado";

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String NARANJA = "\u001B[33m";
        String RESET = "\u001B[0m";

        System.out.println(NARANJA);

        System.out.println("====================================================================");
        System.out.println("██████╗ ██╗███████╗███╗   ██╗██╗   ██╗███████╗███╗   ██╗██╗██████╗  ██████╗ ███████╗");
        System.out.println("██╔══██╗██║██╔════╝████╗  ██║██║   ██║██╔════╝████╗  ██║██║██╔══██╗██╔═══██╗██╔════╝");
        System.out.println("██████╔╝██║█████╗  ██╔██╗ ██║██║   ██║█████╗  ██╔██╗ ██║██║██║  ██║██║   ██║███████╗");
        System.out.println("██╔══██╗██║██╔══╝  ██║╚██╗██║╚██╗ ██╔╝██╔══╝  ██║╚██╗██║██║██║  ██║██║   ██║╚════██║");
        System.out.println("██████╔╝██║███████╗██║ ╚████║ ╚████╔╝ ███████╗██║ ╚████║██║██████╔╝╚██████╔╝███████║");
        System.out.println("╚═════╝ ╚═╝╚══════╝╚═╝  ╚═══╝  ╚═══╝  ╚══════╝╚═╝  ╚═══╝╚═╝╚═════╝  ╚═════╝ ╚══════╝");
        System.out.println(" ");
        System.out.println(" █████╗     ██████╗██╗  ██╗██╗███╗   ██╗ █████╗ ██╗    ██╗ ██████╗ ██╗  ██╗");
        System.out.println("██╔══██╗   ██╔════╝██║  ██║██║████╗  ██║██╔══██╗██║    ██║██╔═══██╗██║ ██╔╝");
        System.out.println("███████║   ██║     ███████║██║██╔██╗ ██║███████║██║ █╗ ██║██║   ██║█████╔╝ ");
        System.out.println("██╔══██║   ██║     ██╔══██║██║██║╚██╗██║██╔══██║██║███╗██║██║   ██║██╔═██╗ ");
        System.out.println("██║  ██║   ╚██████╗██║  ██║██║██║ ╚████║██║  ██║╚███╔███╔╝╚██████╔╝██║  ██╗");
        System.out.println("╚═╝  ╚═╝    ╚═════╝╚═╝  ╚═╝╚═╝╚═╝  ╚═══╝╚═╝  ╚═╝ ╚══╝╚══╝  ╚═════╝ ╚═╝  ╚═╝");
        System.out.println("====================================================================");
        System.out.println(RESET);
        menuDePlatos();
        menuDeInicio(sc);

    }

    public static void menuDePlatos() {
        cargarLosMasVendidos();
        cargarCombosPersonales();
        cargarParaCompartir();
        cargarFestivalMostrazo();
    }

    public static void menuDeInicio(Scanner sc) {
        boolean salir = false;
        while (!salir) {
            System.out.println("_-CHINAWOK_-");
            System.out.println("Usuario actual: " + usuarioLogueado);
            System.out.println("1.- Iniciar Sesion");
            System.out.println("2.- Registrarse");
            System.out.println("3.- Entrar como invitado");
            System.out.println("4.- salir");
            if (esadmin){
                System.out.println("5.- Entrar como Administrador");
            }
            System.out.print("Seleccione una opcion: ");

            if (sc.hasNextInt()) {
                int opcion = sc.nextInt();
                sc.nextLine();

                switch (opcion) {
                    case 1:
                        boolean exitoLogin = inicioSesion(sc);
                        if (exitoLogin&&esUsuario) {
                            mostrarCategoriasChinaWok(sc);
                        }
                        break;
                    case 2:
                        registrarse(sc);
                        break;
                    case 3:
                        System.out.println("Entraste como invitado");
                        usuarioLogueado = "Invitado";
                        mostrarCategoriasChinaWok(sc);
                        break;
                    case 4:
                        System.out.println("Saliendo del sistema de ChinaWok... ¡Hasta luego!");
                        salir = true;
                        break;
                    case 5:
                        if(esadmin)
                            menuAdministrador(sc);
                        else {
                            System.out.println("usted no tiene acceso al panel de administrador");
                        }
                        break;
                    default:
                        System.out.println("Opcion invalida");
                        break;
                }
            } else {
                System.out.println("Error: Ingrese un número entero valido.");
                sc.nextLine();
            }
        }
    }

    public static boolean inicioSesion(Scanner sc) {
        boolean inicioSesionExitoso = false;

        do {
            System.out.println("_-INICIAR SESION_-");

            System.out.println("Ingrese correo:");
            String correo = sc.nextLine();

            System.out.println("Ingrese su contraseña:");
            String contraseña = sc.nextLine();
            String terminos=sc.nextLine();
            do {
                System.out.println("¿Acepta los términos y condiciones? (si/no)");
                terminos = sc.nextLine();

                if (terminos.equalsIgnoreCase("no")) {
                    System.out.println("Debe aceptar los términos para continuar.");
                }

            } while (!terminos.equalsIgnoreCase("si"));
            boolean condicionesCorreoU = correo.contains("@") && correo.endsWith(".com");

            boolean condicionesContraseñaU = contraseña.length() >= 8;

            if (!condicionesCorreoU || !condicionesContraseñaU) {
                System.out.println("No ha sido posible iniciar sesión, vuelva a intentarlo.");
                if (!condicionesCorreoU) {
                    System.out.println("El correo debe contener @ y terminar en .com");
                }
                if (!condicionesContraseñaU) {
                    System.out.println("La contraseña debe tener mínimo 8 caracteres");
                }
                System.out.println("¿Desea cancelar? (si/no)");
                String cancelar = sc.nextLine();

                if (cancelar.equalsIgnoreCase("si")) {
                    break;
                }
            }
            else if((correo.equals(ADMIN_CORREO) && contraseña.equals(ADMIN_CONTRASEÑA))){
                esadmin=true;
                inicioSesionExitoso = true;

            }
            else if (correo.equals(clienteCorreo) && contraseña.equals(Clientecontraseña)) {

                System.out.println("Inicio de sesión exitoso✔️");

                usuarioLogueado = clienteNombre;
                esUsuario=true;
                inicioSesionExitoso = true;
            }
            else {
                System.out.println("Correo o contraseña incorrectos.");

                System.out.println("¿Desea intentar nuevamente? (si/no)");
                String respuesta = sc.nextLine();

                if (respuesta.equalsIgnoreCase("no")) {
                    break;
                }
            }

        } while (!inicioSesionExitoso);

        return inicioSesionExitoso;
    }

    public static boolean registrarse(Scanner sc) {
        boolean registrado = false;
        do {
            System.out.println("_-REGISTRARSE_-");
            System.out.println("Ingrese sus nombres:");
            String nombre = sc.nextLine();

            System.out.println("Ingrese sus apellidos:");
            String apellidos = sc.nextLine();

            System.out.println("Ingrese su DNI:");
            String dni = sc.nextLine();

            System.out.println("Ingrese su numero de celular:");
            String celular = sc.nextLine();

            System.out.println("Ingrese correo:");
            clienteCorreo = sc.nextLine();

            System.out.println("Ingrese su contraseña:");
            Clientecontraseña = sc.nextLine();

            boolean verificacionDniU = dni.length() == 8;
            boolean verificacionCelularU = celular.length() == 9;
            boolean verificacionCorreoU = clienteCorreo.contains("@") && clienteCorreo.endsWith(".com");
            boolean verificacionContraseñaU = Clientecontraseña.length() >= 8;

            if (!verificacionDniU || !verificacionCelularU || !verificacionCorreoU || !verificacionContraseñaU) {
                System.out.println("No ha sido posible registrarse, vuelve a intentarlo");
                if (!verificacionDniU) {
                    System.out.println("DNI debe tener 8 caracteres");
                }
                if (!verificacionCelularU) {
                    System.out.println("Celular debe tener 9 caracteres");
                }
                if (!verificacionCorreoU) {
                    System.out.println("Correo debe contener @ y terminar en .com");
                }
                if (!verificacionContraseñaU) {
                    System.out.println("Contraseña debe tener +8 caracteres");
                }

                System.out.println("¿Desea cancelar? (si/no)");
                String cancelar = sc.nextLine();
                if (cancelar.equalsIgnoreCase("si")) {
                    break;
                }
                continue;
            }

            clienteNombre = nombre;
            clienteApellido = apellidos;
            clienteDni = dni;
            clienteTelefono = celular;
            clienteCorreo = clienteCorreo;
            usuarioLogueado = "Cliente Registrado (" + clienteCorreo + ")";
            System.out.println("Has sido registrado exitosamente");

            registrado = true;

        } while (!registrado);

        return registrado;
    }
    public static void menuAdministrador(Scanner sc) {

        int opcion;

        do {

            System.out.println("==================================");
            System.out.println("      PANEL ADMINISTRADOR");
            System.out.println("==================================");
            System.out.println("1. Ver los productos actuales");
            System.out.println("2. Agregar producto");
            System.out.println("3. Modificar precio");
            System.out.println("4. Eliminar producto");
            System.out.println("5.-Buscar productos");
            System.out.println("6.- Salir");
            System.out.print("Seleccione una opcion: ");

            opcion = sc.nextInt();
            sc.nextLine();

            switch (opcion) {

                case 1:
                    verProductosAdministrador(sc);
                    break;

                case 2:
                    agregarProductoAdministrador(sc);
                    break;

                case 3:
                    modificarPrecioAdministrador(sc);
                    break;

                case 4:
                    eliminarProductoAdministrador(sc);
                    break;

                case 5:
                    buscarProductosAdministrador(sc);
                    break;
                case 6:
                    System.out.println("Saliendo del panel admin...");
                    break;
                default:
                    System.out.println("Opción invalida.");
            }

        } while (opcion !=6);
    }

    public static void buscarProductosAdministrador(Scanner sc) {

        System.out.println("===== BUSCADOR DE PRODUCTOS =====");
        System.out.println("1. Buscar por la letra que comienza");
        System.out.println("2. Buscar por rango de precio");

        int opcion = sc.nextInt();
        sc.nextLine();
        switch(opcion){

            case 1:
                System.out.print("Ingrese una letra (B, D, M o C): ");
                char letra = Character.toUpperCase(sc.nextLine().charAt(0));
                if(letra == 'B' || letra == 'D' || letra == 'M' || letra == 'C'){
                    buscarPorLetra(letra);
                } else {
                    System.out.println("❌ Error: Solo puede buscar con las letras B, D, M o C.");
                }
                break;

            case 2:
                System.out.println("Seleccione un rango:");
                System.out.println("1. Menores de S/25");
                System.out.println("2. Entre S/45 y S/64");
                System.out.println("3. Mayores o iguales a S/65");
                System.out.println("Porfavor solo coloque números 1 ; 2 y 3 ❗");

                int rango = sc.nextInt();
                sc.nextLine();

                if(rango >= 1 && rango <= 3){
                    buscarPorPrecio(rango);
                } else {
                    System.out.println("❌ Error: No tenemos esa opción de búsqueda.");
                }
                break;

            default:
                System.out.println("Opción inválida❗");
        }
    }
    public static String PromocionRandom() {

        String[] promociones = {

                "10% de descuento en tu próxima compra✔️✔️✔️🎉🎉",
                "Lleva 2 Wantanes y paga solo 1 para la proxima compra🎊🎊🎊🎊",
                "Por el dia del padre ganaste una gaseosa gratis✔️✔️✔️🎉🎉",
                "Gaseosa para tu proxima visita🎊🎊✔️✔️✔️",
                "Postre gratis en tu próxima visita ✔️✔️✔️✔️🍭🍡🍰"
        };

        Random random = new Random();
        int indice = random.nextInt(promociones.length);

        return promociones[indice];
    }
    public static void buscarPorLetra(char letra){

        int encontrados = 0;

        encontrados += mostrarProductosLetra(losMasVendidos, precioLosMasVendidos, letra);
        encontrados += mostrarProductosLetra(combosPersonales, precioCombosPersonales, letra);
        encontrados += mostrarProductosLetra(paraCompartir, precioParaCompartir, letra);
        encontrados += mostrarProductosLetra(festivalMostrazo, precioFestivalMostrazo, letra);

        if(encontrados == 0){
            System.out.println("❌ No tenemos productos que empiecen con la letra '" + letra + "'.");
        }
    }
    public static int mostrarProductosLetra(ArrayList<String> nombres, ArrayList<Double> precios, char letra){
        int contador = 0;

        for(int i=0; i<nombres.size(); i++){

            if(Character.toUpperCase(nombres.get(i).charAt(0)) == letra){

                System.out.println(
                        nombres.get(i)
                                + " - S/"
                                + precios.get(i));

                contador++;
            }
        }

        return contador;
    }
    public static void buscarPorPrecio(int rango){

        int encontrados = 0;

        encontrados += mostrarProductosPrecio(losMasVendidos, precioLosMasVendidos, rango);
        encontrados += mostrarProductosPrecio(combosPersonales, precioCombosPersonales, rango);
        encontrados += mostrarProductosPrecio(paraCompartir, precioParaCompartir, rango);
        encontrados += mostrarProductosPrecio(festivalMostrazo, precioFestivalMostrazo, rango);

        if(encontrados == 0){
            System.out.println("❌ No tenemos productos en ese rango de precio.");
        }
    }
    public static int mostrarProductosPrecio(ArrayList<String> nombres, ArrayList<Double> precios, int rango){
        int contador = 0;
        for(int i=0; i<nombres.size(); i++){

            double precio = precios.get(i);

            boolean mostrar = false;

            switch(rango){

                case 1:
                    mostrar = precio < 25;
                    break;

                case 2:
                    mostrar = precio >= 45 && precio <= 64;
                    break;

                case 3:
                    mostrar = precio >= 65;
                    break;
            }

            if(mostrar){

                System.out.println(
                        nombres.get(i)
                                + " - S/"
                                + precio);

                contador++;
            }
        }
        return contador;
    }
    public static void verProductosAdministrador(Scanner sc) {

        System.out.println("--VER PRODUCTOS--");
        System.out.println("1.-Ver Los Mas Vendidos");
        System.out.println("2.-Ver Combos Personales");
        System.out.println("3.-Ver Para Compartir");
        System.out.println("4.-Ver Festival Mostrazo");

        int tipo = sc.nextInt();
        sc.nextLine();

        switch (tipo) {

            case 1:
                imprimirListaLosMasVendidos();
                break;

            case 2:
                imprimirListaCombosPersonales();
                break;

            case 3:
                imprimirListaParaCompartir();
                break;

            case 4:
                imprimirListaFestivalMostrazo();
                break;

            default:
                System.out.println("Opcion invalida");
                break;
        }
    }

    public static void imprimirListaLosMasVendidos() {

        for (int i = 0; i < losMasVendidos.size(); i++) {

            System.out.println(i + " " +
                    losMasVendidos.get(i) +
                    " S/" + precioLosMasVendidos.get(i));
        }
    }

    public static void imprimirListaCombosPersonales() {

        for (int i = 0; i < combosPersonales.size(); i++) {

            System.out.println(i + " " +
                    combosPersonales.get(i) +
                    " S/" + precioCombosPersonales.get(i));
        }
    }
    public static void imprimirListaParaCompartir() {

        for (int i = 0; i < paraCompartir.size(); i++) {

            System.out.println(i + " " +
                    paraCompartir.get(i) +
                    " S/" + precioParaCompartir.get(i));
        }
    }
    public static void imprimirListaFestivalMostrazo() {

        for (int i = 0; i < festivalMostrazo.size(); i++) {

            System.out.println(i + " " +
                    festivalMostrazo.get(i) +
                    " S/" + precioFestivalMostrazo.get(i));
        }
    }

    public static void agregarProductoAdministrador(Scanner sc) {

        System.out.println("--REGISTRAR NUEVO PRODUCTO--");
        System.out.println("1.-Añadir Los Mas Vendidos");
        System.out.println("2.-Añadir Combos Personales");
        System.out.println("3.-Añadir Para Compartir");
        System.out.println("4.-Añadir Festival Mostrazo");

        int tipo = sc.nextInt();
        sc.nextLine();

        switch (tipo) {

            case 1:
                System.out.println("Ingrese el nombre del producto");
                losMasVendidos.add(sc.nextLine());

                System.out.println("Ingrese el precio");
                precioLosMasVendidos.add(sc.nextDouble());
                sc.nextLine();
                System.out.println("Producto agregado correctamente✔️");
                break;

            case 2:
                System.out.println("Ingrese el nombre del producto");
                combosPersonales.add(sc.nextLine());

                System.out.println("Ingrese el precio");
                precioCombosPersonales.add(sc.nextDouble());
                sc.nextLine();
                System.out.println("Producto agregado correctamente✔️");
                break;

            case 3:
                System.out.println("Ingrese el nombre del producto");
                paraCompartir.add(sc.nextLine());

                System.out.println("Ingrese el precio");
                precioParaCompartir.add(sc.nextDouble());
                sc.nextLine();
                System.out.println("Producto agregado correctamente✔️");
                break;

            case 4:
                System.out.println("Ingrese el nombre del producto");
                festivalMostrazo.add(sc.nextLine());

                System.out.println("Ingrese el precio");
                precioFestivalMostrazo.add(sc.nextDouble());
                sc.nextLine();
                System.out.println("Producto agregado correctamente✔️");
                break;

            default:
                System.out.println("Opcion invalida");
                break;
        }
    }

    public static void modificarPrecioAdministrador(Scanner sc) {

        System.out.println("--MODIFICAR PRECIO DEL PRODUCTO--");
        System.out.println("1.-Modificar Los Mas Vendidos");
        System.out.println("2.-Modificar Combos Personales");
        System.out.println("3.-Modificar Para Compartir");
        System.out.println("4.-Modificar Festival Mostrazo");

        int tipo = sc.nextInt();
        sc.nextLine();

        int pos;

        switch (tipo) {

            case 1:

                imprimirListaLosMasVendidos();

                System.out.println("Ingrese la posicion a modificar:");
                pos = sc.nextInt();
                sc.nextLine();

                if (pos >= 0 && pos < losMasVendidos.size()) {

                    System.out.println("Ingrese el nuevo precio");
                    precioLosMasVendidos.set(pos, sc.nextDouble());
                    sc.nextLine();

                    System.out.println("Precio actualizado✔️");

                } else {
                    System.out.println("Posicion no valida✖️");
                }

                break;

            case 2:

                imprimirListaCombosPersonales();

                System.out.println("Ingrese la posicion a modificar:");
                pos = sc.nextInt();
                sc.nextLine();

                if (pos >= 0 && pos < combosPersonales.size()) {

                    System.out.println("Ingrese el nuevo precio");
                    precioCombosPersonales.set(pos, sc.nextDouble());
                    sc.nextLine();

                    System.out.println("Precio actualizado✔️");

                } else {
                    System.out.println("Posicion no valida✖️");
                }

                break;

            case 3:

                imprimirListaParaCompartir();

                System.out.println("Ingrese la posicion a modificar:");
                pos = sc.nextInt();
                sc.nextLine();

                if (pos >= 0 && pos < paraCompartir.size()) {

                    System.out.println("Ingrese el nuevo precio");
                    precioParaCompartir.set(pos, sc.nextDouble());
                    sc.nextLine();

                    System.out.println("Precio actualizado✔️");

                } else {
                    System.out.println("Posicion no valida✖️");
                }

                break;

            case 4:

                imprimirListaFestivalMostrazo();

                System.out.println("Ingrese la posicion a modificar:");
                pos = sc.nextInt();
                sc.nextLine();

                if (pos >= 0 && pos < festivalMostrazo.size()) {

                    System.out.println("Ingrese el nuevo precio");
                    precioFestivalMostrazo.set(pos, sc.nextDouble());
                    sc.nextLine();

                    System.out.println("Precio actualizado✔️");

                } else {
                    System.out.println("Posicion no valida✖️");
                }

                break;

            default:
                System.out.println("Opcion invalida");
                break;
        }
    }

    public static void eliminarProductoAdministrador(Scanner sc) {

        System.out.println("--ELIMINAR PRODUCTO--");
        System.out.println("1.-Eliminar Los Mas Vendidos");
        System.out.println("2.-Eliminar Combos Personales");
        System.out.println("3.-Eliminar Para Compartir");
        System.out.println("4.-Eliminar Festival Mostrazo");

        int tipo = sc.nextInt();
        sc.nextLine();

        int pos;

        switch (tipo) {

            case 1:

                imprimirListaLosMasVendidos();

                System.out.println("Ingrese la posicion a eliminar");
                pos = sc.nextInt();
                sc.nextLine();

                if (pos >= 0 && pos < losMasVendidos.size()) {

                    losMasVendidos.remove(pos);
                    precioLosMasVendidos.remove(pos);

                    System.out.println("Producto eliminado correctamente✔️");

                } else {
                    System.out.println("Posicion no valida✖️");
                }

                break;

            case 2:

                imprimirListaCombosPersonales();

                System.out.println("Ingrese la posicion a eliminar");
                pos = sc.nextInt();
                sc.nextLine();

                if (pos >= 0 && pos < combosPersonales.size()) {

                    combosPersonales.remove(pos);
                    precioCombosPersonales.remove(pos);

                    System.out.println("Producto eliminado correctamente✔️");

                } else {
                    System.out.println("Posicion no valida✖️");
                }

                break;

            case 3:

                imprimirListaParaCompartir();

                System.out.println("Ingrese la posicion a eliminar");
                pos = sc.nextInt();
                sc.nextLine();

                if (pos >= 0 && pos < paraCompartir.size()) {

                    paraCompartir.remove(pos);
                    precioParaCompartir.remove(pos);

                    System.out.println("Producto eliminado correctamente✔️");

                } else {
                    System.out.println("Posicion no valida✖️");
                }

                break;

            case 4:

                imprimirListaFestivalMostrazo();

                System.out.println("Ingrese la posicion a eliminar");
                pos = sc.nextInt();
                sc.nextLine();

                if (pos >= 0 && pos < festivalMostrazo.size()) {

                    festivalMostrazo.remove(pos);
                    precioFestivalMostrazo.remove(pos);

                    System.out.println("Producto eliminado correctamente✔️");

                } else {
                    System.out.println("Posicion no valida✖️");
                }

                break;

            default:
                System.out.println("Opcion invalida");
                break;
        }
    }

    public static void mostrarCategoriasChinaWok(Scanner sc) {
        int opcionCategoria = 0;
        do {
            System.out.println("==================================================");
            System.out.println("              MENU DE OPCIONES CHINAWOK            ");
            System.out.println("==================================================");
            System.out.println("1. Ver Seccion: Los Mas Vendidos");
            System.out.println("2. Ver Seccion: Combos Personales");
            System.out.println("3. Ver Seccion: Para Compartir");
            System.out.println("4. Ver Seccion: Festival Mostrazo (Promociones)");
            System.out.println("5. ver libro de reclamaciones");
            System.out.println("6. Regresar al Menu Principal / Cerrar Sesion");
            System.out.print("Seleccione una opcion para desplegar los productos: ");

            if (sc.hasNextInt()) {
                opcionCategoria = sc.nextInt();
                sc.nextLine();

                switch (opcionCategoria) {
                    case 1:
                        menuLosMasVendidos(sc);
                        break;
                    case 2:
                        menuCombosPersonales(sc);
                        break;
                    case 3:
                        menuParaCompartir(sc);
                        break;
                    case 4:
                        menuFestivalMostrazo(sc);
                        break;
                    case 5:
                        LibrodeReclamaciones(sc);
                        break;
                    case 6:
                        System.out.println("Cerrando sesion y regresando...");
                        break;
                    default:
                        System.out.println("Opcion invalida. Intente de nuevo.");
                        break;
                }
            } else {
                System.out.println("Por favor, ingrese un numero valido.");
                sc.nextLine();
            }
        } while (opcionCategoria != 6);
    }
    public static void LibrodeReclamaciones(Scanner sc){
        String departamento,provincia,distrito,direccion;
        boolean credencialescorrectos=false;
        System.out.println("parte 1:IDENTIFICACION DEL CONSUMIDOR RECLAMANTE");
do {
    System.out.println("--------------------------------------------------");
    System.out.println("        INGRESANDO AL LIBRO DE RECLAMACIONES      ");
    System.out.println("--------------------------------------------------");

    if (clienteNombre.equals("") || clienteDni.equals("")) {
        System.out.println("Ingrese Correo Electronico: ");
        clienteCorreo = sc.nextLine();
        System.out.println("Ingrese Primer y Segundo Nombre: ");
        clienteNombre = sc.nextLine();
        System.out.println("Ingrese Apellidos Completos: ");
        clienteApellido = sc.nextLine();
        System.out.println("Ingrese Numero de DNI (8 digitos): ");
        clienteDni = sc.nextLine();
        System.out.println("Ingrese Numero de Telefono Movil: ");
        clienteTelefono = sc.nextLine();
        System.out.println("ingrese su departamento ");
        departamento= sc.nextLine();
        System.out.println("ingrese su provincia ");
        provincia=sc.nextLine();
        System.out.println("ingrese su distrito");
        distrito= sc.nextLine();
        System.out.println("ingrese su direccion");
        direccion= sc.nextLine();
        credencialescorrectos=true;
    }
    else {
        System.out.println("[SISTEMA] Autocompletando datos desde su cuenta activa...");
        System.out.println("Cliente: " + clienteNombre + " " + clienteApellido);
        System.out.println("DNI    : " + clienteDni);
        System.out.println("Correo : " + clienteCorreo);
        System.out.println("telefono:" + clienteTelefono);
        System.out.println("ingrese su departamento ");
        departamento= sc.nextLine();
        System.out.println("ingrese su provincia ");
        provincia=sc.nextLine();
        System.out.println("ingrese su distrito");
        distrito= sc.nextLine();
        System.out.println("ingrese su direccion");
        direccion= sc.nextLine();
        credencialescorrectos=true;
    }
}
while (!credencialescorrectos);

        System.out.println("paso 2: IDENTIFICACION DEL BIEN CONTRATADO");
        System.out.println("ingrese que inconvenientes tiene con PRODUCTO o nuestros SERVICIOS");
        System.out.println("1: producto");
        System.out.println("2: servicio");
        int tipo=sc.nextInt();
        String inconveniente="";
        sc.nextLine();
        switch (tipo){
            case 1:
                System.out.println("ingrese el nombre del producto adquirido ");
                String producto=sc.nextLine();
                inconveniente="producto:"+producto;
                break;
            case 2:
                System.out.println("ingrese el servicio adquirido ");
                String servicio=sc.nextLine();
                inconveniente="servicio:"+servicio;
                break;
            default:
                System.out.println("error del sistema");
                LibrodeReclamaciones(sc);
                return;
        }
            System.out.println("paso 3: DETALLES DE RECLAMACION Y PEDIDO DEL CONSUMIDOR");
            System.out.println("1: RECLAMO");
            System.out.println("2: QUEJA");
            int Nreclamacion= sc.nextInt();
            String reclamacion;
            switch (Nreclamacion){
                case 1:
                    reclamacion="reclamo";
                    break;
                case 2:
                    reclamacion="queja";
                    break;
                default:
                    System.out.println("error del sistema");
                    LibrodeReclamaciones(sc);
                    return;
            }

            String tienda="";
        boolean tiendaqueja=false;
        do {
            System.out.println("seleccione el lugar donde ocurrio el percanse");
            System.out.println("1. ChinaWok - Sede Principal Juliaca");
            System.out.println("2. ChinaWok - Mall Arequipa Center (Cerro Colorado)");
            System.out.println("3. ChinaWok - Real Plaza Arequipa");
            System.out.println("4. ChinaWok - Mallplaza Bellavista");
            System.out.println("5. ChinaWok - Plaza Norte Lima");
            System.out.print("Seleccione la sucursal de preferencia (1-5): ");
            int opciontienda=sc.nextInt();
            switch (opciontienda){
                case 1:
                    tienda="ChinaWok - Sede Principal Juliaca";tiendaqueja=true;
                    break;
                case 2:
                    tienda="ChinaWok - Mall Arequipa Center (Cerro Colorado)";tiendaqueja=true;
                    break;
                case 3:
                    tienda="ChinaWok - Real Plaza Arequipa";tiendaqueja=true;
                    break;
                case 4:
                    tienda="ChinaWok - Mallplaza Bellavista";tiendaqueja=true;
                    break;
                case 5:
                    tienda="ChinaWok - Plaza Norte Lima";tiendaqueja=true;
                    break;
            }
        } while (!tiendaqueja);
            sc.nextLine();
            System.out.println("ingrese el motivo (breve)");
            String motivo=sc.nextLine();
            System.out.println("detallenos su mala experiencia en nuestra sede");
            String detalles=sc.nextLine();
            System.out.println("diganos una manera en la que podamos mejorar su experiencia en nuestra sede");
            String mejoras=sc.nextLine();
            System.out.println("GRACIAS POR AYUDARNOS A MEJORAR SU EXPERIENCIA");

        System.out.println(" RESUMEN DE SU RECLAMACION");
        System.out.println("inconveniente "+inconveniente);
        System.out.println("tienda "+tienda);
        System.out.println("motivo"+motivo);
        System.out.println(reclamacion);
        System.out.println("mejoras para la sede "+mejoras);
        menuDeInicio(sc);

    }
    public static void menuLosMasVendidos(Scanner sc) {

        System.out.println("=========== LOS MAS VENDIDOS ===========");

        for (int i = 0; i < losMasVendidos.size(); i++) {
            System.out.println((i + 1) + ". "
                    + losMasVendidos.get(i)
                    + " - S/" + precioLosMasVendidos.get(i));
        }

        System.out.print("Seleccione un producto: ");
        int opcion = sc.nextInt();
        sc.nextLine();

        if(opcion >= 1 && opcion <= losMasVendidos.size()) {
            productoNombre = losMasVendidos.get(opcion - 1);
            productoPrecio = precioLosMasVendidos.get(opcion - 1);

            solicitarCantidadYProcesar(sc);
        } else {
            System.out.println("Opcion invalida.");
        }

    }

    public static void cargarLosMasVendidos() {

        losMasVendidos.add("Arroz Chaufa de Pollo Clasico");
        precioLosMasVendidos.add(14.90);

        losMasVendidos.add("Combinado Tallarin Saltado con Chaufa");
        precioLosMasVendidos.add(16.90);

        losMasVendidos.add("Aeropuerto ChinaWok Especial");
        precioLosMasVendidos.add(19.90);

        losMasVendidos.add("Pollo Chijaukay con Chaufa Personal");
        precioLosMasVendidos.add(18.90);

        losMasVendidos.add("Pollo Tipakay Agridulce con Chaufa");
        precioLosMasVendidos.add(18.90);

        losMasVendidos.add("Wantan Frito Especial x12");
        precioLosMasVendidos.add(12.00);

        losMasVendidos.add("Tallarin Saltado de Pollo");
        precioLosMasVendidos.add(15.90);

        losMasVendidos.add("Sopa Wantan Especial Gigante");
        precioLosMasVendidos.add(16.50);

        losMasVendidos.add("Lomo Saltado al Wok con Arroz");
        precioLosMasVendidos.add(23.90);

        losMasVendidos.add("Banquetazo Mostrazo Simple");
        precioLosMasVendidos.add(21.50);
    }
    public static void menuCombosPersonales(Scanner sc) {

        System.out.println("=========== COMBOS PERSONALES ===========");

        for (int i = 0; i < combosPersonales.size(); i++) {
            System.out.println((i + 1) + ". " +
                    combosPersonales.get(i) +
                    " - S/" + precioCombosPersonales.get(i));
        }

        System.out.print("Seleccione un producto: ");
        int opcion = sc.nextInt();
        sc.nextLine();

        if(opcion >= 1 && opcion <= losMasVendidos.size()) {
            productoNombre = losMasVendidos.get(opcion - 1);
            productoPrecio = precioLosMasVendidos.get(opcion - 1);

            solicitarCantidadYProcesar(sc);
        } else {
            System.out.println("Opcion invalida.");
        }
    }
    public static void cargarCombosPersonales() {

        combosPersonales.add("Combo Personal Chaufa + Wantanes + Gaseosa");
        precioCombosPersonales.add(17.90);

        combosPersonales.add("Combo Tipakay Express Individual");
        precioCombosPersonales.add(20.90);

        combosPersonales.add("Combo Chijaukay Express Individual");
        precioCombosPersonales.add(20.90);

        combosPersonales.add("Combo Aeropuerto + Gaseosa 500ml");
        precioCombosPersonales.add(22.50);

        combosPersonales.add("Duo Wok Personal");
        precioCombosPersonales.add(19.00);

        combosPersonales.add("Combo Kaplu Individual Especial");
        precioCombosPersonales.add(24.90);

        combosPersonales.add("Wok Express de Carne Saltada");
        precioCombosPersonales.add(25.50);

        combosPersonales.add("Combo Mini Wok");
        precioCombosPersonales.add(13.90);

        combosPersonales.add("Tallarin Saltado Express + Bebida");
        precioCombosPersonales.add(18.50);

        combosPersonales.add("Combo Enrollado Express");
        precioCombosPersonales.add(21.00);
    }
    public static void menuParaCompartir(Scanner sc) {

        System.out.println("=========== PARA COMPARTIR ===========");

        for (int i = 0; i < paraCompartir.size(); i++) {
            System.out.println((i + 1) + ". " +
                    paraCompartir.get(i) +
                    " - S/" + precioParaCompartir.get(i));
        }

        System.out.print("Seleccione un producto: ");
        int opcion = sc.nextInt();
        sc.nextLine();

        if(opcion >= 1 && opcion <= losMasVendidos.size()) {
            productoNombre = losMasVendidos.get(opcion - 1);
            productoPrecio = precioLosMasVendidos.get(opcion - 1);

            solicitarCantidadYProcesar(sc);
        } else {
            System.out.println("Opcion invalida.");
        }

    }
    public static void cargarParaCompartir() {

        paraCompartir.add("Banquetazo Familiar ChinaWok");
        precioParaCompartir.add(45.90);

        paraCompartir.add("Mega Combo ChinaWok Dueto");
        precioParaCompartir.add(59.90);

        paraCompartir.add("Chifa Party Familiar");
        precioParaCompartir.add(69.90);

        paraCompartir.add("Combo Kamlu Familiar Real");
        precioParaCompartir.add(74.50);

        paraCompartir.add("Super Banquete de la Casa Imperial");
        precioParaCompartir.add(89.90);

        paraCompartir.add("Banquete Familiar Wok Especial Grande");
        precioParaCompartir.add(64.90);

        paraCompartir.add("Combo Al Gusto Familiar");
        precioParaCompartir.add(78.00);

        paraCompartir.add("Banquete Imperial Mandarin");
        precioParaCompartir.add(115.00);

        paraCompartir.add("Banquete Gran Muralla Wok");
        precioParaCompartir.add(139.90);

        paraCompartir.add("Banquete Dinastia China");
        precioParaCompartir.add(155.00);
    }
    public static void menuFestivalMostrazo(Scanner sc) {

        System.out.println("=========== FESTIVAL MOSTRAZO ===========");

        for (int i = 0; i < festivalMostrazo.size(); i++) {
            System.out.println((i + 1) + ". " +
                    festivalMostrazo.get(i) +
                    " - S/" + precioFestivalMostrazo.get(i));
        }

        System.out.print("Seleccione un producto: ");
        int opcion = sc.nextInt();
        sc.nextLine();

        if(opcion >= 1 && opcion <= losMasVendidos.size()) {
            productoNombre = losMasVendidos.get(opcion - 1);
            productoPrecio = precioLosMasVendidos.get(opcion - 1);

            solicitarCantidadYProcesar(sc);
        } else {
            System.out.println("Opcion invalida.");
        }

    }
    public static void cargarFestivalMostrazo() {

        festivalMostrazo.add("Mostrazo Ultra Especial");
        precioFestivalMostrazo.add(22.90);

        festivalMostrazo.add("Lunes de Wantan Extremo");
        precioFestivalMostrazo.add(9.90);

        festivalMostrazo.add("Locura Chaufera Promocional");
        precioFestivalMostrazo.add(22.00);

        festivalMostrazo.add("Chijaukay Imperial de Oferta");
        precioFestivalMostrazo.add(24.90);

        festivalMostrazo.add("Cyber Wok Nocturno Especial");
        precioFestivalMostrazo.add(17.90);

        festivalMostrazo.add("Mega Promocion Fin de Semana");
        precioFestivalMostrazo.add(30.00);

        festivalMostrazo.add("Promo Parejas Wok Completa");
        precioFestivalMostrazo.add(34.90);

        festivalMostrazo.add("Cuponera Digital Mostrazo Aeropuerto");
        precioFestivalMostrazo.add(25.00);

        festivalMostrazo.add("Mostrazo Tipakay Fest");
        precioFestivalMostrazo.add(22.90);

        festivalMostrazo.add("Gran Banquete Mostrazo de la Web");
        precioFestivalMostrazo.add(49.90);
    }
    public static void solicitarCantidadYProcesar(Scanner sc) {
        boolean cantidadCorrecta = false;

        do {
            System.out.print("¿Cuantas unidades de este producto desea llevar?: ");
            if (sc.hasNextInt()) {
                cantidadLlevar = sc.nextInt();
                sc.nextLine();

                if (cantidadLlevar <= 0) {
                    System.out.println("Error: No se permiten cantidades menores o iguales a cero. Reintente.");
                } else if (cantidadLlevar > 25) {
                    System.out.println("Aviso: Por politicas de la tienda, el limite maximo por orden es de 25 unidades.");
                    System.out.println("¿Desea reajustar su pedido? (si/no)");
                    String respuesta = sc.nextLine();
                    if (respuesta.equalsIgnoreCase("no")) {
                        System.out.println("Pedido cancelado de forma correcta.");
                        break;
                    }
                } else {
                    System.out.println("Cantidad registrada de forma exitosa: " + cantidadLlevar + " unidades.");
                    cantidadCorrecta = true;

                    totalPagar = productoPrecio * cantidadLlevar;
                    double subtotal = productoPrecio * cantidadLlevar;

                    carritoProductos.add(productoNombre);
                    carritoCantidades.add(cantidadLlevar);
                    carritoSubtotales.add(subtotal);
                    System.out.println("====================================");
                    System.out.println("         CARRITO DE COMPRAS         ");
                    System.out.println("====================================");

                    double totalCarrito = 0;

                    for(int i = 0; i < carritoProductos.size(); i++){
                        System.out.println(
                                (i + 1) + ". "
                                        + carritoProductos.get(i)
                                        + " x" + carritoCantidades.get(i)
                                        + " - S/" + carritoSubtotales.get(i));

                        totalCarrito += carritoSubtotales.get(i);
                    }

                    System.out.println("------------------------------------");
                    System.out.println("Total acumulado: S/" + totalCarrito);
                    System.out.println("====================================");
                    System.out.println("¿Desea agregar otro producto?");
                    System.out.println("1. Sí");
                    System.out.println("2. No");
                    System.out.print("Seleccione una opción: ");

                    int opcionCarrito = sc.nextInt();
                    sc.nextLine();

                    if(opcionCarrito == 1){
                        mostrarCategoriasChinaWok(sc);
                        return;
                    }
                    System.out.println("--------------------------------------------------");
                    System.out.println("              CALCULO DE PRECIOS WOK              ");
                    System.out.println("--------------------------------------------------");
                    double totalCalculado = 0;
                    for(int i = 0; i < carritoProductos.size(); i++){
                        System.out.println("Producto          : " + carritoProductos.get(i));
                        System.out.println("Precio Unitario   : S/ " + (carritoSubtotales.get(i) / carritoCantidades.get(i)));
                        System.out.println("Cantidad Pedida   : " + carritoCantidades.get(i));
                        System.out.println("Subtotal          : S/ " + carritoSubtotales.get(i));
                        System.out.println("--------------------------------------------------");

                        totalCalculado += carritoSubtotales.get(i);
                    }
                    System.out.println("TOTAL BRUTO COMPRA: S/ " + totalCalculado);
                    System.out.println("--------------------------------------------------");
                    System.out.print("¿Desea confirmar el monto y proceder a la facturacion? (si/no): ");
                    String confirmar = sc.nextLine();

                    if (!confirmar.equalsIgnoreCase("si")) {
                        System.out.println("Monto rechazado. Cancelando transaccion...");
                        return;
                    }

                    System.out.println("--------------------------------------------------");
                    System.out.println("        INGRESE DATOS PARA LA VALIDACION          ");
                    System.out.println("--------------------------------------------------");

                    if (clienteNombre.equals("") || clienteDni.equals("")) {
                        System.out.print("Ingrese Correo Electronico: ");
                        clienteCorreo = sc.nextLine();
                        System.out.print("Ingrese Primer y Segundo Nombre: ");
                        clienteNombre = sc.nextLine();
                        System.out.print("Ingrese Apellidos Completos: ");
                        clienteApellido = sc.nextLine();
                        System.out.print("Ingrese Numero de DNI (8 digitos): ");
                        clienteDni = sc.nextLine();
                        System.out.print("Ingrese Numero de Telefono Movil: ");
                        clienteTelefono = sc.nextLine();
                    } else {
                        System.out.println("[SISTEMA] Autocompletando datos desde su cuenta activa...");
                        System.out.println("Cliente: " + clienteNombre + " " + clienteApellido);
                        System.out.println("DNI    : " + clienteDni);
                        System.out.println("Correo : " + clienteCorreo);
                    }
                    int opcionTienda = 0;
                    boolean tiendaValida = false;
                    do {
                        System.out.println("--------------------------------------------------");
                        System.out.println("         SELECCIONE LA TIENDA DE RECOJO           ");
                        System.out.println("--------------------------------------------------");
                        System.out.println("1. ChinaWok - Sede Principal Juliaca");
                        System.out.println("2. ChinaWok - Mall Arequipa Center (Cerro Colorado)");
                        System.out.println("3. ChinaWok - Real Plaza Arequipa");
                        System.out.println("4. ChinaWok - Mallplaza Bellavista");
                        System.out.println("5. ChinaWok - Plaza Norte Lima");
                        System.out.print("Seleccione la sucursal de preferencia (1-5): ");

                        if (sc.hasNextInt()) {
                            opcionTienda = sc.nextInt();
                            sc.nextLine();

                            switch (opcionTienda) {
                                case 1:
                                    tiendaSeleccionada = "ChinaWok - Sede Principal Juliaca"; tiendaValida = true;
                                    break;
                                case 2:
                                    tiendaSeleccionada = "ChinaWok - Mall Arequipa Center (Cerro Colorado)"; tiendaValida = true;
                                    break;
                                case 3:
                                    tiendaSeleccionada = "ChinaWok - Real Plaza Arequipa"; tiendaValida = true;
                                    break;
                                case 4:
                                    tiendaSeleccionada = "ChinaWok - Mallplaza Bellavista"; tiendaValida = true;
                                    break;
                                case 5:
                                    tiendaSeleccionada = "ChinaWok - Plaza Norte Lima"; tiendaValida = true;
                                    break;
                                default: System.out.println("Error: Opcion de tienda no habilitada.");
                                    break;
                            }
                        } else {
                            System.out.println("Formato incorrecto. Ingrese un digito del 1 al 5.");
                            sc.nextLine();
                        }
                    } while (!tiendaValida);

                    int opcionPago = 0;
                    boolean pagoValido = false;
                    totalPagar = 0;

                    for(int i = 0; i < carritoSubtotales.size(); i++){
                        totalPagar += carritoSubtotales.get(i);
                    }
                    do {
                        System.out.println("--------------------------------------------------");
                        System.out.println("              SELECCIONE METODO DE PAGO           ");
                        System.out.println("--------------------------------------------------");
                        System.out.println("1. Efectivo (Pago en caja)");
                        System.out.println("2. Tarjeta de Credito / Debito");
                        System.out.println("3. Yape / Plin (Billetera Digital)");
                        System.out.print("Seleccione una opción: ");

                        if (sc.hasNextInt()) {
                            opcionPago = sc.nextInt();
                            sc.nextLine();

                            switch (opcionPago) {
                                case 1:
                                    metodoPagoSeleccionado = "Efectivo"; pagoValido = true;
                                    break;
                                case 2:
                                    metodoPagoSeleccionado = "Tarjeta"; pagoValido = true;
                                    break;
                                case 3:
                                    metodoPagoSeleccionado = "Yape/Plin"; pagoValido = true;
                                    break;
                                default: System.out.println("Opcion no valida.");
                                    break;
                            }
                        } else {
                            System.out.println("Entrada invalida.");
                            sc.nextLine();
                        }
                    } while (!pagoValido);

                    if (metodoPagoSeleccionado.equals("Tarjeta")) {

                        validapago_tarjeta(sc, totalPagar);
                        montoPagadoCon = totalPagar;
                        vueltoEntregar = 0;

                    } else {

                        boolean pagoCompletado = false;

                        do {
                            System.out.println("-----------------------------------------------------------------------------");
                            System.out.println("Total a pagar: S/ " + totalPagar + ". Ingrese el monto con el que pagará: S/ ");
                            System.out.println("-----------------------------------------------------------------------------");

                            if (sc.hasNextDouble()) {
                                montoPagadoCon = sc.nextDouble();
                                sc.nextLine();

                                if (montoPagadoCon < totalPagar) {
                                    System.out.println("Error: El monto ingresado es insuficiente. Faltan S/ " + (totalPagar - montoPagadoCon));
                                } else {
                                    vueltoEntregar = montoPagadoCon - totalPagar;
                                    pagoCompletado = true;
                                }
                            } else {
                                System.out.println("Error: Ingrese un monto numérico válido.");
                                sc.nextLine();
                            }

                        } while (!pagoCompletado);
                    }

                    LocalDate fechaCompra = LocalDate.now();
                    LocalDate fechaRecojo = fechaCompra.plusDays(1);

                    DateTimeFormatter formato = DateTimeFormatter.ofPattern("dd/MM/yyyy");

                    String fechaCompraTexto = fechaCompra.format(formato);
                    String fechaRecojoTexto = fechaRecojo.format(formato);

                    System.out.println("==================================================");
                    System.out.println("             RESUMEN DE SU PEDIDO                 ");
                    System.out.println("==================================================");
                    System.out.println("--------------------------------------------------");

                    System.out.println("PUNTO DE RECOJO");
                    System.out.println("Tu pedido estará listo para ser recogido en:");
                    System.out.println(tiendaSeleccionada);
                    System.out.println("--------------------------------------------------");

                    System.out.println("Fecha de compra: Hoy (" + fechaCompraTexto + ")");
                    System.out.println("Fecha estimada de recojo: Mañana (" + fechaRecojoTexto + ")");

                    System.out.println("Cliente: " + clienteNombre + " " + clienteApellido);
                    System.out.println();
                    System.out.println("Tus productos escogidos:");

                    double totalGeneral = 0;

                    for(int i = 0; i < carritoProductos.size(); i++){

                        System.out.println(
                                (i + 1) + ". "
                                        + carritoProductos.get(i)
                                        + " x" + carritoCantidades.get(i)
                                        + "  S/" + carritoSubtotales.get(i));

                        totalGeneral += carritoSubtotales.get(i);
                    }

                    System.out.println("--------------------------------------------------");
                    System.out.println("TOTAL A PAGAR: S/" + totalGeneral);
                    System.out.println("Tienda de recojo: " + tiendaSeleccionada);
                    System.out.println("Metodo de pago: " + metodoPagoSeleccionado);
                    System.out.println("Vuelto del pedido: S/" + vueltoEntregar);
                    System.out.println("--------------------------------------------------");
                    System.out.println("PROMOCION ESPECIAL PARA USTED:");
                    System.out.println(PromocionRandom());

                    System.out.println("==================================================");
                    System.out.println("¡Muchas gracias por su compra en ChinaWok!");
                    exportarBoleta(totalGeneral);
                    carritoProductos.clear();
                    carritoCantidades.clear();
                    carritoSubtotales.clear();
                    System.exit(0);

                }
            } else {
                System.out.println("Error: Ingrese un numero entero para la cantidad.");
                sc.nextLine();
            }
        } while (!cantidadCorrecta);
    }
    public static void exportarBoleta(double total) {
        String rutaArchivo = "D:\\BoletaChinaWok.txt";

        LocalDate fechaCompra = LocalDate.now();
        LocalDate fechaRecojo = fechaCompra.plusDays(1);

        DateTimeFormatter formato = DateTimeFormatter.ofPattern("dd/MM/yyyy");

        String fechaCompraTexto = fechaCompra.format(formato);
        String fechaRecojoTexto = fechaRecojo.format(formato);

        try (FileWriter escritor = new FileWriter(rutaArchivo)) {
            escritor.write("==================================================\n");
            escritor.write("             RESUMEN DE SU PEDIDO                 \n");
            escritor.write("==================================================\n");
            escritor.write("--------------------------------------------------\n");
            escritor.write("PUNTO DE RECOJO\n");
            escritor.write("Tu pedido estará listo para ser recogido en:\n");
            escritor.write(tiendaSeleccionada + "\n");
            escritor.write("--------------------------------------------------\n");
            escritor.write("Fecha de compra: Hoy (" + fechaCompraTexto + ")\n");
            escritor.write("Fecha estimada de recojo: Mañana (" + fechaRecojoTexto + ")\n");
            escritor.write("Cliente: " + clienteNombre + " " + clienteApellido + "\n\n");
            escritor.write("Tus productos escogidos:\n");

            for(int i = 0; i < carritoProductos.size(); i++){
                escritor.write((i + 1) + ". "
                        + carritoProductos.get(i)
                        + " x" + carritoCantidades.get(i)
                        + "  S/" + carritoSubtotales.get(i) + "\n");
            }

            escritor.write("--------------------------------------------------\n");
            escritor.write("TOTAL A PAGAR: S/" + total + "\n");
            escritor.write("Tienda de recojo: " + tiendaSeleccionada + "\n");
            escritor.write("Metodo de pago: " + metodoPagoSeleccionado + "\n");
            escritor.write("Vuelto del pedido: S/" + vueltoEntregar + "\n");
            escritor.write("==================================================\n");
            escritor.write("¡Muchas gracias por su compra en ChinaWok!\n");

            System.out.println("✅ Boleta exportada correctamente a " + rutaArchivo);

        } catch (IOException e) {
            System.out.println("❌ Error al exportar la boleta: " + e.getMessage());
        }
    }
    public static void validapago_tarjeta(Scanner escaner ,double total){
        String number_Tar, fecha_ven, cvv;
        boolean pa_Aprovado = false;

        System.out.println("El monto total del pago con tarjeta es :" + total);

        do{
            System.out.println("Ingrese los numeros de la tarjeta");
            number_Tar = escaner.nextLine();

            System.out.println("Ingrese la fecha de caducidad(MM/AA)");
            fecha_ven = escaner.nextLine();

            System.out.println("Ingrese el codigo de seguridad CVV ");
            cvv = escaner.nextLine();

            boolean tarOK = (number_Tar.length() == 16);
            boolean cvvOK = (cvv.length() == 3);
            boolean fechaestructuraOK = (fecha_ven.length() == 5 && fecha_ven.contains("/"));

            boolean fechaNO_ven = false;

            if(fechaestructuraOK) {
                try {
                    DateTimeFormatter formateador = DateTimeFormatter.ofPattern("MM/yy");
                    YearMonth fechaTarjeta = YearMonth.parse(fecha_ven, formateador);
                    YearMonth fecha_ac = YearMonth.now();

                    if (fechaTarjeta.isAfter(fecha_ac) || fechaTarjeta.equals(fecha_ac)) {
                        fechaNO_ven = true;
                    }

                } catch (DateTimeParseException e) {
                    fechaestructuraOK = false;
                }
            }

            if (tarOK && cvvOK && fechaestructuraOK && fechaNO_ven) {
                System.out.println("Autorizando fondos...transaccion exitosa");
                pa_Aprovado = true;
            } else {
                System.out.println("Datos incorrectos, intente nuevamente");
            }

            if (!fechaestructuraOK) {
                System.out.println("Formato de fecha incorrecto");
            }

            if (fechaestructuraOK && !fechaNO_ven) {
                System.out.println("Tarjeta caducada");
            }

            if (!cvvOK) {
                System.out.println("CVV incorrecto");
            }

            if (!tarOK) {
                System.out.println("Numero de tarjeta incorrecto");
            }

        } while(!pa_Aprovado);
    }
}
