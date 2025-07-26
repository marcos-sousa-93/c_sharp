# Aprenda C# do Básico ao Avançado

Vou te guiar através de uma jornada de aprendizado de C#, desde os conceitos mais básicos até tópicos avançados. C# (pronunciado "C Sharp") é uma linguagem de programação moderna, orientada a objetos e de propósito geral, desenvolvida pela Microsoft.

## 📌 Nível Básico

### 1. Introdução ao C#
- **O que é C#**: Linguagem criada pela Microsoft, parte do ecossistema .NET
- **Ambiente de desenvolvimento**: Visual Studio, Visual Studio Code, ou JetBrains Rider
- **Estrutura básica de um programa**:

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello, World!");
    }
}
```

### 2. Variáveis e Tipos de Dados
```csharp
// Tipos primitivos
int idade = 25;                     // Inteiro
double altura = 1.75;                // Ponto flutuante
decimal preco = 19.99m;              // Decimal (para valores monetários)
char letra = 'A';                    // Caractere único
string nome = "João";                // Texto
bool temCarteira = true;             // Booleano (true/false)

// Tipos complexos
DateTime hoje = DateTime.Now;        // Data e hora
object obj = new object();           // Tipo base de todos os tipos
```

### 3. Operadores
```csharp
// Aritméticos
int soma = 5 + 3;        // 8
int subtracao = 5 - 3;   // 2
int multiplicacao = 5 * 3; // 15
int divisao = 15 / 3;    // 5
int resto = 5 % 3;       // 2

// Comparação
bool igual = (5 == 3);   // false
bool diferente = (5 != 3); // true
bool maior = (5 > 3);    // true
bool menor = (5 < 3);    // false

// Lógicos
bool and = (true && false);  // false
bool or = (true || false);   // true
bool not = !true;            // false
```

### 4. Estruturas de Controle
```csharp
// If-else
int numero = 10;
if (numero > 0)
{
    Console.WriteLine("Positivo");
}
else if (numero < 0)
{
    Console.WriteLine("Negativo");
}
else
{
    Console.WriteLine("Zero");
}

// Switch
string dia = "Segunda";
switch (dia)
{
    case "Segunda":
        Console.WriteLine("Início da semana");
        break;
    case "Sexta":
        Console.WriteLine("Final da semana");
        break;
    default:
        Console.WriteLine("Dia qualquer");
        break;
}

// Loops
for (int i = 0; i < 5; i++)
{
    Console.WriteLine(i);
}

int j = 0;
while (j < 5)
{
    Console.WriteLine(j);
    j++;
}

do
{
    Console.WriteLine(j);
    j--;
} while (j > 0);
```

## 📌 Nível Intermediário

### 5. Orientação a Objetos
```csharp
// Classe básica
public class Pessoa
{
    // Propriedades
    public string Nome { get; set; }
    public int Idade { get; set; }

    // Método
    public void Apresentar()
    {
        Console.WriteLine($"Olá, meu nome é {Nome} e tenho {Idade} anos.");
    }
}

// Uso
Pessoa pessoa1 = new Pessoa();
pessoa1.Nome = "Maria";
pessoa1.Idade = 30;
pessoa1.Apresentar();
```

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

### 7. Tratamento de Exceções
```csharp
try
{
    int divisor = 0;
    int resultado = 10 / divisor;
}
catch (DivideByZeroException ex)
{
    Console.WriteLine("Não é possível dividir por zero!");
    Console.WriteLine(ex.Message);
}
finally
{
    Console.WriteLine("Este bloco sempre é executado");
}
```

### 8. Delegados e Eventos
```csharp
// Delegado
public delegate void OperacaoMatematica(int x, int y);

public class Calculadora
{
    public static void Somar(int a, int b)
    {
        Console.WriteLine($"Soma: {a + b}");
    }
    
    public static void Subtrair(int a, int b)
    {
        Console.WriteLine($"Subtração: {a - b}");
    }
}

// Uso
OperacaoMatematica op = Calculadora.Somar;
op += Calculadora.Subtrair;
op(10, 5);

// Evento
public class Botao
{
    public event EventHandler? Clique;
    
    public void Clicar()
    {
        Clique?.Invoke(this, EventArgs.Empty);
    }
}
```

## 📌 Nível Avançado

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

### 10. Expressões Lambda e LINQ Avançado
```csharp
List<Produto> produtos = new List<Produto>
{
    new Produto { Id = 1, Nome = "Notebook", Preco = 3500.00m, Categoria = "Eletrônicos" },
    new Produto { Id = 2, Nome = "Smartphone", Preco = 2500.00m, Categoria = "Eletrônicos" },
    new Produto { Id = 3, Nome = "Mesa", Preco = 800.00m, Categoria = "Móveis" }
};

// Filtro com Lambda
var eletronicos = produtos.Where(p => p.Categoria == "Eletrônicos");

// Ordenação
var ordenados = produtos.OrderByDescending(p => p.Preco);

// Agregação
decimal precoTotal = produtos.Sum(p => p.Preco);
decimal precoMedio = produtos.Average(p => p.Preco);
```

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

### 12. Entity Framework (ORM)
```csharp
public class AppDbContext : DbContext
{
    public DbSet<Produto> Produtos { get; set; }
    
    protected override void OnConfiguring(DbContextOptionsBuilder options)
        => options.UseSqlServer("Server=(localdb)\\mssqllocaldb;Database=LojaDB;Trusted_Connection=True;");
}

// CRUD
using (var context = new AppDbContext())
{
    // Create
    var novoProduto = new Produto { Nome = "Teclado", Preco = 150.00m };
    context.Produtos.Add(novoProduto);
    context.SaveChanges();
    
    // Read
    var produtosBaratos = context.Produtos
        .Where(p => p.Preco < 200.00m)
        .ToList();
        
    // Update
    var produto = context.Produtos.Find(1);
    if (produto != null)
    {
        produto.Preco *= 1.1m; // Aumento de 10%
        context.SaveChanges();
    }
    
    // Delete
    var produtoParaRemover = context.Produtos.Find(2);
    if (produtoParaRemover != null)
    {
        context.Produtos.Remove(produtoParaRemover);
        context.SaveChanges();
    }
}
```

### 13. Programação Paralela
```csharp
// Parallel.For
Parallel.For(0, 10, i =>
{
    Console.WriteLine($"Executando iteração {i} na thread {Thread.CurrentThread.ManagedThreadId}");
    Thread.Sleep(100);
});

// Tasks
Task<int> tarefa1 = Task.Run(() => CalcularAlgoComplexo(5));
Task<int> tarefa2 = Task.Run(() => CalcularAlgoComplexo(10));

Task.WhenAll(tarefa1, tarefa2).ContinueWith(t =>
{
    Console.WriteLine($"Resultado 1: {tarefa1.Result}, Resultado 2: {tarefa2.Result}");
});

int CalcularAlgoComplexo(int input)
{
    Thread.Sleep(1000);
    return input * input;
}
```

## 🚀 Próximos Passos

Para se tornar um especialista em C#:

1. **Pratique muito**: Crie projetos pessoais
2. **Explore o ecossistema .NET**: ASP.NET Core, Xamarin, MAUI, Blazor
3. **Aprenda padrões de projeto**: Repository, Unit of Work, Dependency Injection
4. **Estude arquitetura**: Clean Architecture, DDD (Domain-Driven Design)
5. **Participe da comunidade**: Stack Overflow, GitHub, fóruns de discussão

Quer que eu detalhe algum tópico específico ou tenha alguma dúvida sobre algum conceito?
