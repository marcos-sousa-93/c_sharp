# Manipulação de Arquivos em Hexadecimal no C#

Vou te mostrar várias técnicas para manipular arquivos em nível hexadecimal no C#, incluindo extração de strings, leitura de diferentes tipos de dados, análise de offsets e identificação de magic numbers.

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

## 3. Leitura de Dados por Offset e Tipos Específicos

```csharp
public static void ReadDataAtOffset(string filePath, long offset, DataType type, int length = 0)
{
    using (FileStream fs = new FileStream(filePath, FileMode.Open, FileAccess.Read))
    using (BinaryReader reader = new BinaryReader(fs))
    {
        fs.Seek(offset, SeekOrigin.Begin);
        
        switch (type)
        {
            case DataType.Byte:
                byte byteValue = reader.ReadByte();
                Console.WriteLine($"Byte em 0x{offset:X}: {byteValue} (0x{byteValue:X2})");
                break;
                
            case DataType.Int16:
                short shortValue = reader.ReadInt16();
                Console.WriteLine($"Int16 em 0x{offset:X}: {shortValue} (0x{shortValue:X4})");
                break;
                
            case DataType.Int32:
                int intValue = reader.ReadInt32();
                Console.WriteLine($"Int32 em 0x{offset:X}: {intValue} (0x{intValue:X8})");
                break;
                
            case DataType.Int64:
                long longValue = reader.ReadInt64();
                Console.WriteLine($"Int64 em 0x{offset:X}: {longValue} (0x{longValue:X16})");
                break;
                
            case DataType.Float:
                float floatValue = reader.ReadSingle();
                Console.WriteLine($"Float em 0x{offset:X}: {floatValue}");
                break;
                
            case DataType.Double:
                double doubleValue = reader.ReadDouble();
                Console.WriteLine($"Double em 0x{offset:X}: {doubleValue}");
                break;
                
            case DataType.String:
                if (length <= 0) throw new ArgumentException("Length must be specified for string type");
                byte[] stringBytes = reader.ReadBytes(length);
                string stringValue = Encoding.ASCII.GetString(stringBytes);
                Console.WriteLine($"String em 0x{offset:X}: {stringValue}");
                break;
                
            case DataType.HexDump:
                if (length <= 0) throw new ArgumentException("Length must be specified for hexdump");
                byte[] hexBytes = reader.ReadBytes(length);
                Console.WriteLine($"Hex dump em 0x{offset:X} (tamanho {length}):");
                for (int i = 0; i < hexBytes.Length; i++)
                {
                    Console.Write("{0:X2} ", hexBytes[i]);
                    if ((i + 1) % 16 == 0) Console.WriteLine();
                }
                Console.WriteLine();
                break;
        }
    }
}

public enum DataType
{
    Byte, Int16, Int32, Int64, Float, Double, String, HexDump
}
```

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

## 7. Editor Hexadecimal Básico

```csharp
public static void SimpleHexEditor(string filePath)
{
    byte[] fileBytes = File.ReadAllBytes(filePath);
    bool editing = true;
    
    while (editing)
    {
        Console.Clear();
        Console.WriteLine("Editor Hexadecimal - {0}", filePath);
        Console.WriteLine("Tamanho: {0} bytes", fileBytes.Length);
        Console.WriteLine("Comandos: q-sair, g-ir para offset, e-editar byte");
        
        // Mostra uma parte do arquivo
        int start = 0;
        int length = 256;
        for (int i = start; i < Math.Min(start + length, fileBytes.Length); i++)
        {
            Console.Write("{0:X4}: {1:X2} ", i, fileBytes[i]);
            if ((i + 1) % 8 == 0) Console.WriteLine();
        }
        
        Console.Write("\n> ");
        string input = Console.ReadLine().Trim().ToLower();
        
        switch (input)
        {
            case "q":
                editing = false;
                break;
                
            case "g":
                Console.Write("Offset (hex): ");
                string offsetStr = Console.ReadLine().Trim();
                try
                {
                    start = Convert.ToInt32(offsetStr, 16);
                    start = Math.Max(0, Math.Min(start, fileBytes.Length - length));
                }
                catch
                {
                    Console.WriteLine("Offset inválido. Pressione qualquer tecla...");
                    Console.ReadKey();
                }
                break;
                
            case "e":
                Console.Write("Offset para editar (hex): ");
                string editOffsetStr = Console.ReadLine().Trim();
                Console.Write("Novo valor (hex): ");
                string newValueStr = Console.ReadLine().Trim();
                
                try
                {
                    int editOffset = Convert.ToInt32(editOffsetStr, 16);
                    byte newValue = Convert.ToByte(newValueStr, 16);
                    
                    if (editOffset >= 0 && editOffset < fileBytes.Length)
                    {
                        fileBytes[editOffset] = newValue;
                        Console.WriteLine("Byte modificado. Pressione qualquer tecla...");
                        Console.ReadKey();
                    }
                    else
                    {
                        Console.WriteLine("Offset fora do intervalo. Pressione qualquer tecla...");
                        Console.ReadKey();
                    }
                }
                catch
                {
                    Console.WriteLine("Valor inválido. Pressione qualquer tecla...");
                    Console.ReadKey();
                }
                break;
        }
    }
    
    // Pergunta se deseja salvar as alterações
    Console.Write("Deseja salvar as alterações? (s/n): ");
    if (Console.ReadLine().Trim().ToLower() == "s")
    {
        File.WriteAllBytes(filePath, fileBytes);
        Console.WriteLine("Alterações salvas.");
    }
}
```

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

## Considerações Importantes

1. **Manipulação de arquivos grandes**: Para arquivos muito grandes, carregar tudo na memória pode não ser eficiente. Considere usar FileStream para leitura em blocos.

2. **Endianness**: Ao ler valores inteiros ou de ponto flutuante, esteja atento à ordem dos bytes (little-endian vs big-endian).

3. **Codificação de texto**: Strings podem usar diferentes codificações (ASCII, UTF-8, UTF-16, etc.). O código mostrado assume ASCII para simplificação.

4. **Segurança**: Sempre valide offsets e tamanhos para evitar exceções ao acessar posições inválidas no array.

5. **Magic numbers**: A lista de magic numbers fornecida é apenas exemplificativa. Existem muitos outros tipos de arquivos com assinaturas específicas.

Esta implementação cobre desde a leitura básica até análise avançada de arquivos binários, incluindo a capacidade de identificar formatos de arquivo comuns através de seus magic numbers.
