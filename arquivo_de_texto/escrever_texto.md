## 2. Escrever em um Arquivo de Texto

```csharp
// Escrever todo o conteúdo de uma vez (sobrescreve)
File.WriteAllText("caminho/arquivo.txt", "Conteúdo do arquivo");

// Escrever um array de linhas (sobrescreve)
File.WriteAllLines("caminho/arquivo.txt", new string[] {"Linha 1", "Linha 2"});

// Adicionar conteúdo ao final do arquivo (append)
File.AppendAllText("caminho/arquivo.txt", "Texto adicional");

// Escrever usando StreamWriter (mais controle)
using (StreamWriter writer = new StreamWriter("caminho/arquivo.txt"))
{
    writer.WriteLine("Linha 1");
    writer.WriteLine("Linha 2");
}

// Append usando StreamWriter
using (StreamWriter writer = new StreamWriter("caminho/arquivo.txt", true))
{
    writer.WriteLine("Nova linha adicionada");
}
```
