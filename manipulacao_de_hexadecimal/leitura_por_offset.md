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
