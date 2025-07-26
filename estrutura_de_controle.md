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
