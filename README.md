# Alvarez Armenta Steve Jovanni - 21211909
### Practica Cafeteria - Código corregido con Singleton

```csharp
using System;
using System.Collections.Generic;

namespace CafeteriaSingleton
{
    public class Pedido
    {
        public string Cliente { get; set; }
        public string Bebida { get; set; }

        public Pedido(string cliente, string bebida)
        {
            Cliente = cliente;
            Bebida = bebida;
        }
    }

    // ✅ Clase Singleton
    public class RegistroPedidos
    {
        private List<Pedido> pedidos = new List<Pedido>();

        // Aquí declaramos el constructor privado
        private RegistroPedidos() { }

        // Posteriormente la instancia estática privada
        private static RegistroPedidos _instancia;

        // Se agregó el candado para acceso seguro en multihilo
        private static readonly object _candado = new object();

        // Creamos el método de acceso a la instancia única
        public static RegistroPedidos ObtenerInstancia()
        {
            lock (_candado)
            {
                if (_instancia == null)
                {
                    _instancia = new RegistroPedidos();
                }
                return _instancia;
            }
        }

        public void AgregarPedido(Pedido pedido)
        {
            pedidos.Add(pedido);
            Console.WriteLine($"📝 Pedido agregado: {pedido.Cliente} - {pedido.Bebida}");
        }

        public void MostrarPedidos()
        {
            Console.WriteLine("📋 Pedidos registrados:");
            foreach (var pedido in pedidos)
            {
                Console.WriteLine($"- {pedido.Cliente}: {pedido.Bebida}");
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var registroBarista1 = RegistroPedidos.ObtenerInstancia();
            registroBarista1.AgregarPedido(new Pedido("Ana", "Latte"));

            var registroBarista2 = RegistroPedidos.ObtenerInstancia();
            registroBarista2.AgregarPedido(new Pedido("Luis", "Café Americano"));

            Console.WriteLine("\nRegistro del barista 1:");
            registroBarista1.MostrarPedidos();

            Console.WriteLine("\nRegistro del barista 2:");
            registroBarista2.MostrarPedidos();

            Console.WriteLine("\nAhora todos comparten el mismo registro.");
        }
    }
}


<img width="1352" height="406" alt="image" src="https://github.com/user-attachments/assets/43dd5e0b-6320-4ce6-8ad5-cf012f41bd21" />

