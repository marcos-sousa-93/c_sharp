### 9. Programação Assíncrona
```csharp
public async Task<string> BaixarDadosAsync(string url)
{
    using (HttpClient client = new HttpClient())
    {
        return await client.GetStringAsync(url);
    }
}

// Uso
try
{
    string dados = await BaixarDadosAsync("https://api.exemplo.com/dados");
    Console.WriteLine(dados);
}
catch (Exception ex)
{
    Console.WriteLine($"Erro: {ex.Message}");
}
```
