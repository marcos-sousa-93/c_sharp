## 4. Identificação de Magic Numbers

```csharp
public static void CheckMagicNumbers(string filePath)
{
    // Dicionário de magic numbers conhecidos (assinaturas de arquivo)
    var magicNumbers = new Dictionary<string, string>
    {
        { "FFD8FF", "JPEG image" },
        { "89504E47", "PNG image" },
        { "47494638", "GIF image" },
        { "25504446", "PDF document" },
        { "504B0304", "ZIP archive or Office Open XML document" },
        { "52617221", "RAR archive" },
        { "7F454C46", "ELF executable" },
        { "4D5A", "DOS/Windows executable" },
        { "494433", "MP3 audio file" },
        { "424D", "BMP image" },
        { "00000100", "ICO icon" },
        { "1F8B08", "GZIP archive" }
    };

    byte[] headerBytes = new byte[8]; // Lemos os primeiros 8 bytes para verificação
    using (FileStream fs = new FileStream(filePath, FileMode.Open, FileAccess.Read))
    {
        fs.Read(headerBytes, 0, headerBytes.Length);
    }

    string hexHeader = BitConverter.ToString(headerBytes).Replace("-", "");
    
    Console.WriteLine("Assinatura do arquivo (hex): " + hexHeader);
    Console.WriteLine("Possíveis tipos:");

    bool found = false;
    foreach (var magic in magicNumbers)
    {
        if (hexHeader.StartsWith(magic.Key))
        {
            Console.WriteLine($"- {magic.Value} (assinatura: {magic.Key})");
            found = true;
        }
    }

    if (!found)
    {
        Console.WriteLine("Nenhum magic number conhecido encontrado.");
    }
}
```
