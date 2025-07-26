## 2. Extração de Strings do Arquivo

```csharp
public static void ExtractStringsFromFile(string filePath, int minLength = 4)
{
    byte[] fileBytes = File.ReadAllBytes(filePath);
    StringBuilder currentString = new StringBuilder();
    List<string> foundStrings = new List<string>();

    foreach (byte b in fileBytes)
    {
        // ASCII imprimível está entre 32 e 126
        if (b >= 32 && b <= 126)
        {
            currentString.Append((char)b);
        }
        else
        {
            if (currentString.Length >= minLength)
            {
                foundStrings.Add(currentString.ToString());
            }
            currentString.Clear();
        }
    }

    // Verifica a última string
    if (currentString.Length >= minLength)
    {
        foundStrings.Add(currentString.ToString());
    }

    Console.WriteLine("Strings encontradas:");
    foreach (string s in foundStrings)
    {
        Console.WriteLine(s);
    }
}
```
