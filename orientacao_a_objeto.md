### 5. Orientação a Objetos
```csharp
// Classe básica
public class Pessoa
{
    // Propriedades
    public string Nome { get; set; }
    public int Idade { get; set; }

    // Método
    public void Apresentar()
    {
        Console.WriteLine($"Olá, meu nome é {Nome} e tenho {Idade} anos.");
    }
}

// Uso
Pessoa pessoa1 = new Pessoa();
pessoa1.Nome = "Maria";
pessoa1.Idade = 30;
pessoa1.Apresentar();
```
