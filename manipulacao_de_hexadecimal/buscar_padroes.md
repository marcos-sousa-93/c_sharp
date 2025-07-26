## 6. Busca por Padrões Específicos

```csharp
public static List<long> FindPattern(string filePath, byte[] pattern)
{
    List<long> positions = new List<long>();
    byte[] fileBytes = File.ReadAllBytes(filePath);
    
    for (int i = 0; i <= fileBytes.Length - pattern.Length; i++)
    {
        bool match = true;
        for (int j = 0; j < pattern.Length; j++)
        {
            if (fileBytes[i + j] != pattern[j])
            {
                match = false;
                break;
            }
        }
        
        if (match)
        {
            positions.Add(i);
        }
    }
    
    return positions;
}

// Exemplo de uso:
// byte[] pattern = new byte[] { 0x50, 0x4B, 0x03, 0x04 }; // Assinatura ZIP
// var positions = FindPattern("arquivo.exe", pattern);
```
