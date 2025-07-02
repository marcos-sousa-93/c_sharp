## 1. Ler um Arquivo de Texto

```csharp
// Ler todo o conteúdo de uma vez
string conteudo = File.ReadAllText("caminho/arquivo.txt");

// Ler todas as linhas em um array
string[] linhas = File.ReadAllLines("caminho/arquivo.txt");

// Ler linha por linha (eficiente para arquivos grandes)
using (StreamReader reader = new StreamReader("caminho/arquivo.txt"))
{
    string linha;
    while ((linha = reader.ReadLine()) != null)
    {
        Console.WriteLine(linha);
    }
}
```
