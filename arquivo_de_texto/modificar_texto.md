## 3. Modificar um Arquivo Existente

```csharp
// Ler, modificar e salvar
string conteudo = File.ReadAllText("arquivo.txt");
conteudo = conteudo.Replace("antigo", "novo");
File.WriteAllText("arquivo.txt", conteudo);

// Modificar linhas específicas
string[] linhas = File.ReadAllLines("arquivo.txt");
linhas[0] = "Primeira linha modificada"; // Modifica a primeira linha
File.WriteAllLines("arquivo.txt", linhas);
```
