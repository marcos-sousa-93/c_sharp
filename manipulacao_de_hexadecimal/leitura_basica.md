## 1. Leitura Básica de Arquivos em Hexadecimal

```csharp
using System;
using System.IO;
using System.Text;

public class HexFileReader
{
    public static void ReadFileAsHex(string filePath)
    {
        byte[] fileBytes = File.ReadAllBytes(filePath);
        
        Console.WriteLine("Tamanho do arquivo: {0} bytes", fileBytes.Length);
        Console.WriteLine("Conteúdo em hexadecimal:");
        
        for (int i = 0; i < fileBytes.Length; i++)
        {
            Console.Write("{0:X2} ", fileBytes[i]);
            if ((i + 1) % 16 == 0) Console.WriteLine(); // Quebra a cada 16 bytes
        }
    }
}
```
