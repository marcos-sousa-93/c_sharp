## 5. Trabalhando com Diretórios

```csharp
// Criar diretório
Directory.CreateDirectory("caminho/novo_diretorio");

// Verificar se diretório existe
bool dirExiste = Directory.Exists("caminho/diretorio");

// Listar arquivos em um diretório
string[] arquivos = Directory.GetFiles("caminho/diretorio");

// Mover diretório
Directory.Move("origem", "destino");

// Deletar diretório
Directory.Delete("caminho/diretorio", true); // true para deletar recursivamente
```
