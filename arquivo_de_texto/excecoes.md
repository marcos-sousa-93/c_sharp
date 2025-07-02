## 6. Tratamento de Exceções

Sempre é bom tratar erros ao trabalhar com arquivos:

```csharp
try
{
    string conteudo = File.ReadAllText("arquivo.txt");
    // Processar o conteúdo
}
catch (FileNotFoundException)
{
    Console.WriteLine("Arquivo não encontrado");
}
catch (IOException ex)
{
    Console.WriteLine($"Erro de E/S: {ex.Message}");
}
catch (UnauthorizedAccessException)
{
    Console.WriteLine("Sem permissão para acessar o arquivo");
}
catch (Exception ex)
{
    Console.WriteLine($"Erro inesperado: {ex.Message}");
}
```
