# FC0456TareaProgramacionBasica

using System;
using System.Collections.Generic;

class Estudiante
{
    public string Nombre { get; set; }
    public double Nota1 { get; set; }
    public double Nota2 { get; set; }
    public double Nota3 { get; set; }
    public double Nota4 { get; set; }

    public double Promedio()
    {
        return (Nota1 + Nota2 + Nota3 + Nota4) / 4;
    }

    public string Estatus()
    {
        return Promedio() >= 70 ? "Aprobado" : "Reprobado";
    }
}

class Program
{
    static void Main()
    {
        Console.Title = "Sistema de Calificaciones";

        Console.Write("¿Cuántos estudiantes desea ingresar?: ");
        int cantidad = int.Parse(Console.ReadLine());

        List<Estudiante> lista = new List<Estudiante>();

        for (int i = 1; i <= cantidad; i++)
        {
            Console.WriteLine($"\n--- Estudiante #{i} ---");

            Estudiante e = new Estudiante();

            Console.Write("Nombre completo: ");
            e.Nombre = Console.ReadLine();

            e.Nota1 = LeerNota("Nota 1");
            e.Nota2 = LeerNota("Nota 2");
            e.Nota3 = LeerNota("Nota 3");
            e.Nota4 = LeerNota("Nota 4");

            lista.Add(e);
        }

        MostrarTabla(lista);

        Console.WriteLine("\nPresione cualquier tecla para salir...");
        Console.ReadKey();
    }

    static double LeerNota(string mensaje)
    {
        double nota;
        do
        {
            Console.Write($"{mensaje} (0 - 100): ");
        } while (!double.TryParse(Console.ReadLine(), out nota) || nota < 0 || nota > 100);

        return nota;
    }

    static void MostrarTabla(List<Estudiante> lista)
    {
        Console.WriteLine("\n==============================================================================================");
        Console.WriteLine("{0,-20} {1,8} {2,8} {3,8} {4,8} {5,10} {6,12}",
            "Estudiante", "Nota1", "Nota2", "Nota3", "Nota4", "Promedio", "Estatus");
        Console.WriteLine("==============================================================================================");

        foreach (var e in lista)
        {
            Console.WriteLine("{0,-20} {1,8:F0} {2,8:F0} {3,8:F0} {4,8:F0} {5,10:F2} {6,12}",
                e.Nombre,
                e.Nota1,
                e.Nota2,
                e.Nota3,
                e.Nota4,
                e.Promedio(),
                e.Estatus());
        }

        Console.WriteLine("==============================================================================================");
    }
}
