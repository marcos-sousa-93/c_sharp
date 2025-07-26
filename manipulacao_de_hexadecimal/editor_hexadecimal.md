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
