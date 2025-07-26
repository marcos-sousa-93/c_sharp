## 5. Análise Completa de Arquivo Hexadecimal

```csharp
public static void FullFileAnalysis(string filePath)
{
    byte[] fileBytes = File.ReadAllBytes(filePath);
    
    Console.WriteLine($"Análise completa do arquivo: {filePath}");
    Console.WriteLine($"Tamanho: {fileBytes.Length} bytes");
    
    // Verifica magic numbers
    CheckMagicNumbers(filePath);
    Console.WriteLine();
    
    // Exibe cabeçalho hexadecimal
    Console.WriteLine("Cabeçalho hexadecimal (primeiros 64 bytes):");
    for (int i = 0; i < Math.Min(64, fileBytes.Length); i++)
    {
        Console.Write("{0:X2} ", fileBytes[i]);
        if ((i + 1) % 16 == 0) Console.WriteLine();
    }
    Console.WriteLine("\n");
    
    // Extrai strings
    Console.WriteLine("Strings encontradas no arquivo:");
    ExtractStringsFromFile(filePath);
    Console.WriteLine();
    
    // Analisa seções específicas (exemplo: procurar por cabeçalhos PE em executáveis)
    if (fileBytes.Length > 0x3C + 4)
    {
        // Offset para PE header em executáveis Windows
        int peOffset = BitConverter.ToInt32(fileBytes, 0x3C);
        if (peOffset + 4 < fileBytes.Length)
        {
            uint peSignature = BitConverter.ToUInt32(fileBytes, peOffset);
            if (peSignature == 0x00004550) // "PE\0\0"
            {
                Console.WriteLine("Este arquivo parece ser um executável PE (Windows).");
                
                // Pode-se extrair mais informações do cabeçalho PE aqui
                ushort machine = BitConverter.ToUInt16(fileBytes, peOffset + 4);
                Console.WriteLine($"Arquitetura: {(machine == 0x014C ? "x86" : machine == 0x8664 ? "x64" : "Desconhecida")}");
            }
        }
    }
}
```
