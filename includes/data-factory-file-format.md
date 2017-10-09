## <a name="specifying-formats"></a>Especificando formatos
A fábrica de dados do Azure dá suporte a saudação tipos de formato a seguir:

* [Formato de texto](#specifying-textformat)
* [Formato JSON](#specifying-jsonformat)
* [Formato Avro](#specifying-avroformat)
* [Formato ORC](#specifying-orcformat)
* [Formato de Parquet](#specifying-parquetformat)

### <a name="specifying-textformat"></a>Especificando TextFormat
Se você quiser tooparse arquivos de texto de saudação ou gravar dados saudação em formato de texto, defina Olá `format` `type` propriedade muito**TextFormat**. Você também pode especificar o seguinte Olá **opcional** propriedades no hello `format` seção. Consulte [TextFormat exemplo](#textformat-example) seção sobre como tooconfigure.

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| columnDelimiter |caractere de saudação usado tooseparate colunas em um arquivo. Você pode considerar toouse um caractere não imprimível raro que provavelmente não existe em seus dados: por exemplo, especifique "\u0001" que representa o início do título (SOH). |Somente um caractere é permitido. Olá **padrão** valor é **vírgula (',')**. <br/><br/>toouse um caractere Unicode, consulte muito[caracteres Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello código correspondente para ele. |Não |
| rowDelimiter |caractere de saudação usado tooseparate linhas em um arquivo. |Somente um caractere é permitido. Olá **padrão** valor é qualquer um dos valores a seguir na leitura de saudação: **["\r\n", "\r", "\n"]** e **"\r\n"** na gravação. |Não |
| escapeChar |caractere especial Olá usado tooescape um delimitador de coluna no conteúdo de saudação do arquivo de entrada. <br/><br/>Não é possível especificar ambos escapeChar e quoteChar para uma tabela. |Somente um caractere é permitido. Nenhum valor padrão. <br/><br/>Exemplo: se você tem vírgula (', ') como delimitador de coluna hello, mas você deseja o caractere de vírgula Olá toohave no texto de saudação (exemplo: "Olá, mundo"), você pode definir o '$' como o caractere de escape hello e usar a cadeia de caracteres "$Oi, mundo" na fonte de saudação. |Não |
| quoteChar |caractere de saudação usado tooquote um valor de cadeia de caracteres. delimitadores de coluna e linha Hello dentro de caracteres de aspas Olá seriam tratadas como parte do valor de cadeia de caracteres de saudação. Essa propriedade é aplicável tooboth entrada e conjuntos de dados de saída.<br/><br/>Não é possível especificar ambos escapeChar e quoteChar para uma tabela. |Somente um caractere é permitido. Nenhum valor padrão. <br/><br/>Por exemplo, se você tem vírgula (', ') como delimitador de coluna hello, mas você deseja toohave caractere de vírgula no texto de saudação (exemplo: < Olá, mundo >), você pode definir "(aspas duplas) como Olá caractere de aspas e usar a cadeia de caracteres hello"Olá, mundo"na fonte de saudação. |Não |
| nullValue |Um ou mais caracteres usados toorepresent um valor nulo. |Um ou mais caracteres. Olá **padrão** os valores são **"\N" e "NULL"** na leitura e **"\N"** na gravação. |Não |
| encodingName |Especifique o nome de codificação de saudação. |Um nomes de codificação válido. Consulte [Propriedade Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx). Por exemplo: windows-1250 ou shift_jis. Olá **padrão** valor é **UTF-8**. |Não |
| firstRowAsHeader |Especifica se tooconsider Olá a primeira linha como cabeçalho. Para um conjunto de dados de entrada, o Data Factory lê a primeira linha como cabeçalho. Para um conjunto de dados de saída, o Data Factory lê a primeira linha como cabeçalho. <br/><br/>Veja [Cenários para usar o `firstRowAsHeader` e o `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para cenários de exemplo. |True <br/>**False (padrão)** |Não |
| skipLineCount |Indica o número de saudação de linhas tooskip ao ler dados de arquivos de entrada. Se skipLineCount e firstRowAsHeader forem especificados, linhas de saudação são ignoradas primeiro e, em seguida, as informações de cabeçalho de saudação é lido do arquivo de entrada hello. <br/><br/>Veja [Cenários para usar o `firstRowAsHeader` e o `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para cenários de exemplo. |Número inteiro |Não |
| treatEmptyAsNull |Especifica se a cadeia de tootreat nula ou vazia como nula valor quando ler dados de um arquivo de entrada. |**True (padrão)**<br/>Falso |Não |

#### <a name="textformat-example"></a>Exemplo de TextFormat
Olá exemplo a seguir mostra algumas das propriedades de formato de saudação para TextFormat.

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

toouse um `escapeChar` em vez de `quoteChar`, substitua a linha hello com `quoteChar` com hello escapeChar a seguir:

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>Cenários de uso de firstRowAsHeader e skipLineCount
* Você está copiando um arquivo de texto do arquivo fonte tooa e gostaria de tooadd uma linha de cabeçalho que contém metadados do esquema de saudação (por exemplo: esquema SQL). Especifique `firstRowAsHeader` como true no conjunto de dados de saída de saudação para esse cenário.
* Você está copiando um arquivo de texto que contém um coletor de arquivo do cabeçalho linha tooa e deseja toodrop de linha. Especifique `firstRowAsHeader` como true no conjunto de dados de entrada hello.
* Você está copiando um arquivo de texto e deseja tooskip algumas linhas no início de saudação que não contêm nenhuma informação de cabeçalho ou de dados. Especifique `skipLineCount` tooindicate Olá número de linhas toobe ignorados. Se o resto de saudação do arquivo hello contém uma linha de cabeçalho, você também pode especificar `firstRowAsHeader`. Se ambos os `skipLineCount` e `firstRowAsHeader` forem especificados, linhas de saudação são ignoradas pela primeira vez e, em seguida, as informações de cabeçalho de saudação é lido do arquivo de entrada hello

### <a name="specifying-jsonformat"></a>Especificando JsonFormat
muito**arquivos JSON como importação/exportação-está em de banco de dados do Azure Cosmos**, consulte [documentos JSON de importação/exportação](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) seção no conector do banco de dados do Azure Cosmos Olá com detalhes.

Se você deseja tooparse Olá JSON arquivos ou gravar dados saudação no formato JSON, defina Olá `format` `type` propriedade muito**JsonFormat**. Você também pode especificar o seguinte Olá **opcional** propriedades no hello `format` seção. Consulte [JsonFormat exemplo](#jsonformat-example) seção sobre como tooconfigure.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| filePattern |Indica padrão Olá dos dados armazenados em cada arquivo JSON. Os valores permitidos são: **setOfObjects** e **arrayOfObjects**. Olá **padrão** valor é **setOfObjects**. Veja a seção [Padrões de arquivo JSON](#json-file-patterns) para obter detalhes sobre esses padrões. |Não |
| jsonNodeReference | Se você deseja tooiterate e extrair dados de objetos hello dentro de uma matriz de campo com hello mesmo padrão, especifique o caminho do JSON Olá dessa matriz. Esta propriedade só terá suporte na cópia de dados de arquivos JSON. | Não |
| jsonPathDefinition | Especifique a expressão de caminho JSON Olá para cada mapeamento de coluna com um nome de coluna personalizada (começam com letras minúsculas). Esta propriedade só terá suporte na cópia de dados de arquivos JSON, e você pode extrair dados de objeto ou de matriz. <br/><br/> Para os campos no objeto raiz, começar com $ raiz; para campos de matriz de saudação escolhida pelo `jsonNodeReference` propriedade, início do elemento da matriz hello. Consulte [JsonFormat exemplo](#jsonformat-example) seção sobre como tooconfigure. | Não |
| encodingName |Especifique o nome de codificação de saudação. Para obter lista de saudação de nomes válidos de codificação, consulte: [encodingname](https://msdn.microsoft.com/library/system.text.encoding.aspx) propriedade. Por exemplo: windows-1250 ou shift_jis. Olá **padrão** valor é: **UTF-8**. |Não |
| nestingSeparator |Caractere usado tooseparate níveis de aninhamento. valor padrão de saudação é '.' (ponto). |Não |

#### <a name="json-file-patterns"></a>Padrões de arquivo JSON

A atividade de cópia pode analisar os padrões dos arquivos JSON abaixo:

- **Tipo I: setOfObjects**

    Cada arquivo contém um único objeto ou vários objetos concatenados/delimitados por linhas. Quando essa opção é escolhida em um conjunto de dados de saída, a atividade de cópia produz um único arquivo JSON com cada objeto por linha (delimitados por linha).

    * **Exemplo de JSON de objeto único**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * **Exemplo de JSON delimitado por linha**

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * **Exemplo de JSON concatenado**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- **Tipo II: arrayOfObjects**

    Cada arquivo contém uma matriz de objetos.

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

#### <a name="jsonformat-example"></a>Exemplo de JsonFormat

**Caso 1: copiar dados de arquivos JSON**

Veja abaixo dois tipos de amostras ao copiar dados de arquivos JSON e Olá toonote pontos genérico:

**Exemplo 1: extrair dados de objeto e de matriz**

Neste exemplo, você espera que um objeto JSON de raiz mapeia toosingle registro na tabela de resultados. Se você tiver um arquivo JSON com hello conteúdo a seguir:  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
e você deseja toocopy-lo em uma tabela do SQL Azure no seguinte Olá Formatar, extraindo dados de objetos e a matriz:

| ID | deviceType | targetResourceType | resourceManagmentProcessRunId | occurrenceTime |
| --- | --- | --- | --- | --- |
| ed0e4960-d9c5-11e6-85dc-d7996816aad3 | Computador | Microsoft.Compute/virtualMachines | 827f8aaa-ab72-437c-ba48-d8917a7336a3 | 13/01/2017 11:24:37 |

conjunto de dados de entrada de saudação com **JsonFormat** tipo é definido da seguinte maneira: (definição parcial com partes relevantes apenas Olá). Mais especificamente:

- `structure`seção define os nomes de coluna de saudação personalizada e o tipo de dados correspondente Olá ao converter dados tootabular. Esta seção é **opcional** , a menos que você precisa toodo mapeamento de coluna. Veja a seção [Especificar a definição de estrutura para conjuntos de dados retangulares](#specifying-structure-definition-for-rectangular-datasets) para obter mais detalhes.
- `jsonPathDefinition`Especifica o caminho JSON de saudação para cada coluna que indica onde tooextract Olá dados. toocopy dados da matriz, você pode usar **array [x] .property** tooextract valor Olá considerando a propriedade do objeto de x ª hello, ou você pode usar  **matriz [*] .property** toofind valor de saudação de qualquer objeto que contém essa propriedade.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

**Exemplo 2: cruzada aplicar vários objetos com o mesmo padrão da matriz de saudação**

Neste exemplo, você espera que um objeto JSON de raiz tootransform em vários registros na tabela de resultados. Se você tiver um arquivo JSON com hello conteúdo a seguir:  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
e você deseja toocopy-lo em uma tabela do SQL Azure no seguinte Olá Formatar, mesclando dados hello dentro da matriz de saudação e cross join com informações de raiz comum hello:

| ordernumber | orderdate | order_pd | order_price | city |
| --- | --- | --- | --- | --- |
| 01 | 20170122 | P1 | 23 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P2 | 13 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P3 | 231 | [{"sanmateo":"No 1"}] |

conjunto de dados de entrada de saudação com **JsonFormat** tipo é definido da seguinte maneira: (definição parcial com partes relevantes apenas Olá). Mais especificamente:

- `structure`seção define os nomes de coluna de saudação personalizada e o tipo de dados correspondente Olá ao converter dados tootabular. Esta seção é **opcional** , a menos que você precisa toodo mapeamento de coluna. Veja a seção [Especificar a definição de estrutura para conjuntos de dados retangulares](#specifying-structure-definition-for-rectangular-datasets) para obter mais detalhes.
- `jsonNodeReference`indica tooiterate e extrair dados de objetos Olá Olá mesmo padrão em **matriz** orderlines.
- `jsonPathDefinition`Especifica o caminho JSON de saudação para cada coluna que indica onde tooextract Olá dados. Neste exemplo, "ordernumber", "orderdate" e "cidade" estão no objeto raiz com o caminho JSON iniciar com"$", enquanto "order_pd" e "order_price" são definidos com caminho derivado do elemento de matriz Olá sem "$"..

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

**Observe Olá pontos a seguir:**

* Se hello `structure` e `jsonPathDefinition` não estão definidos no conjunto de dados de Data Factory hello, hello atividade de cópia detecta Olá esquema do objeto primeiro hello e mesclar objeto inteiro hello.
* Se a entrada JSON Olá tem uma matriz, por padrão hello atividade de cópia converte Olá matriz inteira valor em uma cadeia de caracteres. Você pode escolher dados tooextract usando `jsonNodeReference` e/ou `jsonPathDefinition`, ou ignorá-la não especificando na `jsonPathDefinition`.
* Se não houver duplicados Olá de nomes no mesmo nível, hello atividade de cópia selecionará Olá último.
* Os nomes de propriedade diferenciam maiúsculas de minúsculas. Duas propriedades com o mesmo nome, mas com maiúsculas e minúsculas diferentes são tratadas como duas propriedades separadas.

**Caso 2: Gravando dados tooJSON arquivo**

Se você tiver a tabela a seguir no Banco de Dados SQL:

| ID | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | Davi |
| 2 | 20170120 | 3500 | Pedro |
| 3 | 20170121 | 4000 | Jason |

e, para cada registro, você espera que o objeto JSON de tooa toowrite no abaixo formato:
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

saudação de conjunto de dados com saída **JsonFormat** tipo é definido da seguinte maneira: (definição parcial com partes relevantes apenas Olá). Mais especificamente, `structure` seção define os nomes de propriedade Olá personalizado no arquivo de destino, `nestingSeparator` (o padrão é ".") será a camada de aninhar Olá tooidentify usado do nome de saudação. Esta seção é **opcional** a menos que você deseja o nome da propriedade Olá toochange comparando com o nome da coluna de origem ou aninhar algumas das propriedades de saudação.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

### <a name="specifying-avroformat"></a>Especificando AvroFormat
Se você deseja tooparse Olá Avro arquivos ou gravar dados saudação no formato Avro, defina Olá `format` `type` propriedade muito**AvroFormat**. Não é necessário toospecify as propriedades na seção de formato de saudação na seção de typeProperties hello. Exemplo:

```json
"format":
{
    "type": "AvroFormat",
}
```

formato de Avro toouse em uma tabela de Hive, você pode consultar muito[tutorial do Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).

Observe Olá pontos a seguir:  

* Não há suporte para [Tipos de dados complexos](http://avro.apache.org/docs/current/spec.html#schema_complex) (registros, enumerações, matrizes, mapas, uniões e fixo).

### <a name="specifying-orcformat"></a>Especificando OrcFormat
Se você deseja tooparse Olá ORC arquivos ou gravar dados saudação no formato ORC, defina Olá `format` `type` propriedade muito**OrcFormat**. Não é necessário toospecify as propriedades na seção de formato de saudação na seção de typeProperties hello. Exemplo:

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> Se você não estiver copiando arquivos ORC **como-é** entre local e nuvem armazenamentos de dados, precisa tooinstall Olá 8 JRE (Java Runtime Environment) no seu computador do gateway. Um gateway de 64 bits exige JRE de 64 bits, enquanto um gateway de 32 bits exige JRE de 32 bits. Você pode encontrar as duas versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605). Escolha Olá apropriado.
>
>

Observe Olá pontos a seguir:

* Não há suporte para tipos de dados complexos (STRUCT, MAP, LIST e UNION)
* O arquivo ORC tem três [opções de compactação](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB e SNAPPY. O Data Factory dá suporte à leitura de dados de arquivo ORC em qualquer um dos formatos compactados acima. Ele usa compactação Olá codec está nos dados de Olá Olá metadados tooread. No entanto, ao gravar o arquivo ORC tooan, fábrica de dados escolhe ZLIB, que é o padrão de saudação para ORC. Atualmente, não há nenhuma opção toooverride esse comportamento.

### <a name="specifying-parquetformat"></a>Especificando ParquetFormat
Se você deseja tooparse Olá Parquet arquivos ou gravar dados saudação no formato Parquet, defina Olá `format` `type` propriedade muito**ParquetFormat**. Não é necessário toospecify as propriedades na seção de formato de saudação na seção de typeProperties hello. Exemplo:

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> Se você não estiver copiando arquivos Parquet **como-é** entre local e nuvem armazenamentos de dados, precisa tooinstall Olá 8 JRE (Java Runtime Environment) no seu computador do gateway. Um gateway de 64 bits exige JRE de 64 bits, enquanto um gateway de 32 bits exige JRE de 32 bits. Você pode encontrar as duas versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605). Escolha Olá apropriado.
>
>

Observe Olá pontos a seguir:

* Não há suporte para tipos de dados complexos (MAP, LIST)
* Arquivo parquet tem Olá opções de compactação a seguir: NONE, SNAPPY, GZIP e LZO. O Data Factory dá suporte à leitura de dados de arquivo ORC em qualquer um dos formatos compactados acima. Ele usa o codec de compactação de saudação nos dados de Olá Olá metadados tooread. No entanto, ao gravar o arquivo de Parquet tooa, fábrica de dados escolhe SNAPPY, que é saudação padrão para o formato de Parquet. Atualmente, não há nenhuma opção toooverride esse comportamento.
