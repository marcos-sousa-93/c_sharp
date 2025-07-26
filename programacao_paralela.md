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
