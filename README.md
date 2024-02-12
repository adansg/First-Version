using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    private static string usuarioActual;
    private static List<Usuario> usuariosRegistrados = new List<Usuario>();
    private static Dictionary<string, Equipo> equipos = new Dictionary<string, Equipo>();

    static void Main()
    {
        MostrarMenuInicial();
    }

    static void MostrarMenuInicial()
    {
        Console.Clear();

        Console.WriteLine("Menú Inicial:");
        Console.WriteLine("1. Iniciar sesión");
        Console.WriteLine("2. Registrar usuario");
        Console.WriteLine("3. Salir");

        string opcionSeleccionada = Console.ReadLine();

        switch (opcionSeleccionada)
        {
            case "1":
                IniciarSesion();
                break;
            case "2":
                RegistrarUsuario();
                break;
            case "3":
                Environment.Exit(0);
                break;
            default:
                Console.WriteLine("Opción no válida. Inténtalo de nuevo.");
                MostrarMenuInicial();
                break;
        }
    }

    static void IniciarSesion()
    {
        Console.Clear();

        Console.Write("Nombre de usuario: ");
        string nombreUsuario = Console.ReadLine();
        Console.Write("Contraseña: ");
        string contraseña = Console.ReadLine();

        if (ValidarCredenciales(nombreUsuario, contraseña))
        {
            Console.WriteLine($"¡Bienvenido, {nombreUsuario}!");
            usuarioActual = nombreUsuario;
            MostrarMenu();
        }
        else
        {
            Console.WriteLine("Inicio de sesión fallido. Usuario no registrado. Intente nuevamente.");
            Console.WriteLine("Presiona Enter para continuar...");
            Console.ReadLine();
            MostrarMenuInicial();
        }
    }

    static void RegistrarUsuario()
    {
        Console.Clear();

        Console.Write("Nuevo nombre de usuario: ");
        string nuevoUsuario = Console.ReadLine();
        Console.Write("Nueva contraseña: ");
        string nuevaContraseña = Console.ReadLine();

        if (usuariosRegistrados.Any(u => u.NombreUsuario == nuevoUsuario))
        {
            Console.WriteLine("Usuario ya registrado. Intente con otro nombre de usuario.");
            Console.WriteLine("Presiona Enter para continuar...");
            Console.ReadLine();
            MostrarMenuInicial();
            return;
        }

        usuariosRegistrados.Add(new Usuario { NombreUsuario = nuevoUsuario, Contraseña = nuevaContraseña });

        Console.WriteLine("Usuario registrado exitosamente.");
        Console.WriteLine("Presiona Enter para continuar...");
        Console.ReadLine();

        usuarioActual = nuevoUsuario;
        MostrarMenuInicial();
    }

    static void MostrarMenu()
    {
        Console.Clear();

        Console.WriteLine($"¡Bienvenido, {usuarioActual}!");
        Console.WriteLine("Menú:");
        Console.WriteLine("1. Registrar Equipo (HostName)");
        Console.WriteLine("2. Fecha de última actualización");
        Console.WriteLine("3. Versión actual instalada");
        Console.WriteLine("4. Usuario asignado al equipo");
        Console.WriteLine("5. Fecha de registro del equipo");
        Console.WriteLine("6. Salir");

        string opcionSeleccionada = Console.ReadLine();

        switch (opcionSeleccionada)
        {
            case "1":
                Console.WriteLine("Registrar equipo");
                Console.WriteLine("Presiona Enter para continuar...");
                Console.ReadLine();
                PedirYRegistrarHostName();
                break;
            case "2":
                Console.WriteLine("Fecha de última actualización");
                Console.WriteLine("Presiona Enter para continuar...");
                Console.ReadLine();
                // Lógica para obtener la fecha de última actualización
                MostrarMenu();
                break;
            case "3":
                Console.WriteLine("Versión actual instalada");
                Console.WriteLine("Presiona Enter para continuar...");
                Console.ReadLine();
                // Lógica para obtener la versión actual instalada
                MostrarMenu();
                break;
            case "4":
                Console.WriteLine("Usuario asignado al equipo");
                Console.WriteLine("Presiona Enter para continuar...");
                Console.ReadLine();
                // Lógica para obtener el usuario asignado al equipo
                MostrarMenu();
                break;
            case "5":
                Console.WriteLine("Fecha de registro del equipo");
                Console.WriteLine("Presiona Enter para continuar...");
                Console.ReadLine();
                // Lógica para obtener la fecha de registro del equipo
                MostrarMenu();
                break;
            case "6":
                Environment.Exit(0);
                break;
            default:
                Console.WriteLine("Opción no válida. Inténtalo de nuevo.");
                MostrarMenu();
                break;
        }
    }

    static bool ValidarCredenciales(string nombreUsuario, string contraseña)
    {
        return usuariosRegistrados.Any(u => u.NombreUsuario == nombreUsuario && u.Contraseña == contraseña);
    }

    static void PedirYRegistrarHostName()
    {
        Console.Clear();
        Console.WriteLine("Introduzca el HostName:");
        string hostName = Console.ReadLine();

        // Lógica para registrar el equipo con el HostName
        equipos.Add(hostName, new Equipo { HostName = hostName, FechaRegistro = DateTime.Now });

        Console.WriteLine($"Equipo registrado exitosamente con HostName: {hostName}.");
        Console.WriteLine("Presiona Enter para continuar...");
        Console.ReadLine();

        MostrarMenu();
    }
}

class Usuario
{
    public string NombreUsuario { get; set; }
    public string Contraseña { get; set; }
}

class Equipo
{
    public string HostName { get; set; }
    public DateTime UltimaActualizacion { get; set; }
    public string VersionActual { get; set; }
    public string UsuarioAsignado { get; set; }
    public DateTime FechaRegistro { get; set; }
}
