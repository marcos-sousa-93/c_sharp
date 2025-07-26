## Como Usar Estas Funções

```csharp
class Program
{
    static void Main(string[] args)
    {
        string filePath = "arquivo.bin"; // Substitua pelo seu arquivo
        
        // Exemplos de uso:
        HexFileReader.ReadFileAsHex(filePath);
        ExtractStringsFromFile(filePath);
        ReadDataAtOffset(filePath, 0x100, DataType.Int32);
        CheckMagicNumbers(filePath);
        FullFileAnalysis(filePath);
        
        // Para buscar um padrão específico:
        byte[] zipSignature = new byte[] { 0x50, 0x4B, 0x03, 0x04 };
        var zipPositions = FindPattern(filePath, zipSignature);
        Console.WriteLine($"Assinatura ZIP encontrada em {zipPositions.Count} posições:");
        foreach (var pos in zipPositions)
        {
            Console.WriteLine($"0x{pos:X}");
        }
        
        // Editor hexadecimal interativo
        SimpleHexEditor(filePath);
    }
}
```
