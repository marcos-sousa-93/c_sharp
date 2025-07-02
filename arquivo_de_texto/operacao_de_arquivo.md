## 4. Operações com Arquivos

```csharp
// Verificar se o arquivo existe
bool existe = File.Exists("arquivo.txt");

// Copiar arquivo
File.Copy("origem.txt", "destino.txt", true); // true para sobrescrever

// Mover/Renomear arquivo
File.Move("antigo.txt", "novo.txt");

// Deletar arquivo
File.Delete("arquivo.txt");

// Obter informações do arquivo
DateTime criacao = File.GetCreationTime("arquivo.txt");
DateTime modificacao = File.GetLastWriteTime("arquivo.txt");
long tamanho = new FileInfo("arquivo.txt").Length;
```
