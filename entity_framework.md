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
