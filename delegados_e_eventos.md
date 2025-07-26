### 8. Delegados e Eventos
```csharp
// Delegado
public delegate void OperacaoMatematica(int x, int y);

public class Calculadora
{
    public static void Somar(int a, int b)
    {
        Console.WriteLine($"Soma: {a + b}");
    }
    
    public static void Subtrair(int a, int b)
    {
        Console.WriteLine($"Subtração: {a - b}");
    }
}

// Uso
OperacaoMatematica op = Calculadora.Somar;
op += Calculadora.Subtrair;
op(10, 5);

// Evento
public class Botao
{
    public event EventHandler? Clique;
    
    public void Clicar()
    {
        Clique?.Invoke(this, EventArgs.Empty);
    }
}
```
