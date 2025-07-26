### 11. Reflection e Atributos
```csharp
[Serializable]
[Author("João", Version = 1.1)]
public class MinhaClasse
{
    [Obsolete("Este método será removido na próxima versão")]
    public void MetodoAntigo() { }
    
    public void MetodoNovo() { }
}

// Uso de Reflection
Type tipo = typeof(MinhaClasse);
var atributos = tipo.GetCustomAttributes(false);

foreach (var atributo in atributos)
{
    if (atributo is AuthorAttribute author)
    {
        Console.WriteLine($"Autor: {author.Name}, Versão: {author.Version}");
    }
}
```
