### 6. Coleções
```csharp
// Array
int[] numerosArray = new int[] { 1, 2, 3 };

// List
List<string> nomes = new List<string>();
nomes.Add("Alice");
nomes.Add("Bob");
nomes.Add("Charlie");

// Dictionary
Dictionary<int, string> pessoas = new Dictionary<int, string>();
pessoas.Add(1, "João");
pessoas.Add(2, "Maria");

// LINQ (Language Integrated Query)
var numerosPares = numerosArray.Where(n => n % 2 == 0).ToList();
```
