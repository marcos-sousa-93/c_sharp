## 7. Trabalhando com FileInfo (OOP)

```csharp
FileInfo arquivoInfo = new FileInfo("arquivo.txt");

if (arquivoInfo.Exists)
{
    Console.WriteLine($"Nome: {arquivoInfo.Name}");
    Console.WriteLine($"Extensão: {arquivoInfo.Extension}");
    Console.WriteLine($"Tamanho: {arquivoInfo.Length} bytes");
    Console.WriteLine($"Criado em: {arquivoInfo.CreationTime}");
    
    // Abrir para leitura
    using (StreamReader reader = arquivoInfo.OpenText())
    {
        // Ler conteúdo
    }
    
    // Abrir para escrita
    using (StreamWriter writer = arquivoInfo.CreateText())
    {
        // Escrever conteúdo
    }
}
```
