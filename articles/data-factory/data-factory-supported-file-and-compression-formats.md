---
title: "formatos de compactação e aaaFile na fábrica de dados do Azure | Microsoft Docs"
description: Saiba mais sobre os formatos de arquivo hello com suporte do Azure Data Factory.
keywords: "dados de blob, cópia de blobs do azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a>Formatos de arquivo aos quais o Azure Data Factory dá suporte
*Este tópico se aplica a toohello conectores a seguir: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [BLOBs do Azure](data-factory-azure-blob-connector.md), [repositório Azure Data Lake](data-factory-azure-datalake-connector.md), [sistema de arquivos](data-factory-onprem-file-system-connector.md), [ FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), e [SFTP](data-factory-sftp-connector.md).*

A fábrica de dados do Azure dá suporte a saudação tipos de arquivo de formato a seguir:

* [Formato de texto](#text-format)
* [Formato JSON](#json-format)
* [Formato Avro](#avro-format)
* [Formato ORC](#orc-format)
* [Formato Parquet](#parquet-format)

## <a name="text-format"></a>Formato de texto
Se você desejar tooread de um arquivo de texto ou gravar o arquivo de texto tooa, defina Olá `type` propriedade Olá `format` seção do conjunto de dados de saudação muito**TextFormat**. Você também pode especificar o seguinte Olá **opcional** propriedades no hello `format` seção. Consulte [TextFormat exemplo](#textformat-example) seção sobre como tooconfigure.

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| columnDelimiter |caractere de saudação usado tooseparate colunas em um arquivo. Você pode considerar toouse um caractere não imprimível raro que provavelmente não pode existe em seus dados. Por exemplo, especifique "\u0001", que representa o SOH (início do título). |Somente um caractere é permitido. Olá **padrão** valor é **vírgula (',')**. <br/><br/>toouse um caractere Unicode, consulte muito[caracteres Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello código correspondente para ele. |Não |
| rowDelimiter |caractere de saudação usado tooseparate linhas em um arquivo. |Somente um caractere é permitido. Olá **padrão** valor é qualquer um dos valores a seguir na leitura de saudação: **["\r\n", "\r", "\n"]** e **"\r\n"** na gravação. |Não |
| escapeChar |caractere especial Olá usado tooescape um delimitador de coluna no conteúdo de saudação do arquivo de entrada. <br/><br/>Não é possível especificar ambos escapeChar e quoteChar para uma tabela. |Somente um caractere é permitido. Nenhum valor padrão. <br/><br/>Exemplo: se você tem vírgula (', ') como delimitador de coluna hello, mas você deseja o caractere de vírgula Olá toohave no texto de saudação (exemplo: "Olá, mundo"), você pode definir o '$' como o caractere de escape hello e usar a cadeia de caracteres "$Oi, mundo" na fonte de saudação. |Não |
| quoteChar |caractere de saudação usado tooquote um valor de cadeia de caracteres. delimitadores de coluna e linha Hello dentro de caracteres de aspas Olá seriam tratadas como parte do valor de cadeia de caracteres de saudação. Essa propriedade é aplicável tooboth entrada e conjuntos de dados de saída.<br/><br/>Não é possível especificar ambos escapeChar e quoteChar para uma tabela. |Somente um caractere é permitido. Nenhum valor padrão. <br/><br/>Por exemplo, se você tem vírgula (', ') como delimitador de coluna hello, mas você deseja toohave caractere de vírgula no texto de saudação (exemplo: < Olá, mundo >), você pode definir "(aspas duplas) como Olá caractere de aspas e usar a cadeia de caracteres hello"Olá, mundo"na fonte de saudação. |Não |
| nullValue |Um ou mais caracteres usados toorepresent um valor nulo. |Um ou mais caracteres. Olá **padrão** os valores são **"\N" e "NULL"** na leitura e **"\N"** na gravação. |Não |
| encodingName |Especifique o nome de codificação de saudação. |Um nomes de codificação válido. Consulte [Propriedade Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx). Por exemplo: windows-1250 ou shift_jis. Olá **padrão** valor é **UTF-8**. |Não |
| firstRowAsHeader |Especifica se tooconsider Olá a primeira linha como cabeçalho. Para um conjunto de dados de entrada, o Data Factory lê a primeira linha como cabeçalho. Para um conjunto de dados de saída, o Data Factory lê a primeira linha como cabeçalho. <br/><br/>Veja [Cenários para usar o `firstRowAsHeader` e o `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para cenários de exemplo. |True <br/><b>False (padrão)</b> |Não |
| skipLineCount |Indica o número de saudação de linhas tooskip ao ler dados de arquivos de entrada. Se skipLineCount e firstRowAsHeader forem especificados, linhas de saudação são ignoradas primeiro e, em seguida, as informações de cabeçalho de saudação é lido do arquivo de entrada hello. <br/><br/>Veja [Cenários para usar o `firstRowAsHeader` e o `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para cenários de exemplo. |Número inteiro |Não |
| treatEmptyAsNull |Especifica se a cadeia de tootreat nula ou vazia como nula valor quando ler dados de um arquivo de entrada. |**True (padrão)**<br/>Falso |Não |

### <a name="textformat-example"></a>Exemplo de TextFormat
Em Olá definição JSON para um conjunto de dados a seguir, algumas das propriedades opcionais Olá são especificadas.

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

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>Cenários de uso de firstRowAsHeader e skipLineCount
* Você está copiando um arquivo de texto do arquivo fonte tooa e gostaria de tooadd uma linha de cabeçalho que contém metadados do esquema de saudação (por exemplo: esquema SQL). Especifique `firstRowAsHeader` como true no conjunto de dados de saída de saudação para esse cenário.
* Você está copiando um arquivo de texto que contém um coletor de arquivo do cabeçalho linha tooa e deseja toodrop de linha. Especifique `firstRowAsHeader` como true no conjunto de dados de entrada hello.
* Você está copiando um arquivo de texto e deseja tooskip algumas linhas no início de saudação que não contêm nenhuma informação de cabeçalho ou de dados. Especifique `skipLineCount` tooindicate Olá número de linhas toobe ignorados. Se o resto de saudação do arquivo hello contém uma linha de cabeçalho, você também pode especificar `firstRowAsHeader`. Se ambos os `skipLineCount` e `firstRowAsHeader` forem especificados, linhas de saudação são ignoradas pela primeira vez e, em seguida, as informações de cabeçalho de saudação é lido do arquivo de entrada hello

## <a name="json-format"></a>Formato JSON
muito**importação/exportação de um arquivo JSON como-está em de banco de dados do Azure Cosmos**, consulte Olá [documentos JSON de importação/exportação](data-factory-azure-documentdb-connector.md#importexport-json-documents) seção [mover dados para/de banco de dados do Azure Cosmos](data-factory-azure-documentdb-connector.md) artigo.

Se você deseja tooparse Olá JSON arquivos ou gravar dados saudação no formato JSON, defina Olá `type` propriedade Olá `format` seção muito**JsonFormat**. Você também pode especificar o seguinte Olá **opcional** propriedades no hello `format` seção. Consulte [JsonFormat exemplo](#jsonformat-example) seção sobre como tooconfigure.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| filePattern |Indica padrão Olá dos dados armazenados em cada arquivo JSON. Os valores permitidos são: **setOfObjects** e **arrayOfObjects**. Olá **padrão** valor é **setOfObjects**. Veja a seção [Padrões de arquivo JSON](#json-file-patterns) para obter detalhes sobre esses padrões. |Não |
| jsonNodeReference | Se você deseja tooiterate e extrair dados de objetos hello dentro de uma matriz de campo com hello mesmo padrão, especifique o caminho do JSON Olá dessa matriz. Esta propriedade só terá suporte na cópia de dados de arquivos JSON. | Não |
| jsonPathDefinition | Especifique a expressão de caminho JSON Olá para cada mapeamento de coluna com um nome de coluna personalizada (começam com letras minúsculas). Esta propriedade só terá suporte na cópia de dados de arquivos JSON, e você pode extrair dados de objeto ou de matriz. <br/><br/> Para os campos no objeto raiz, começar com $ raiz; para campos de matriz de saudação escolhida pelo `jsonNodeReference` propriedade, início do elemento da matriz hello. Consulte [JsonFormat exemplo](#jsonformat-example) seção sobre como tooconfigure. | Não |
| encodingName |Especifique o nome de codificação de saudação. Para obter lista de saudação de nomes válidos de codificação, consulte: [encodingname](https://msdn.microsoft.com/library/system.text.encoding.aspx) propriedade. Por exemplo: windows-1250 ou shift_jis. Olá **padrão** valor é: **UTF-8**. |Não |
| nestingSeparator |Caractere usado tooseparate níveis de aninhamento. valor padrão de saudação é '.' (ponto). |Não |

### <a name="json-file-patterns"></a>Padrões de arquivo JSON

Atividade de cópia pode analisar Olá padrões dos arquivos JSON a seguir:

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

### <a name="jsonformat-example"></a>Exemplo de JsonFormat

**Caso 1: copiar dados de arquivos JSON**

Consulte Olá dois exemplos a seguir ao copiar dados de arquivos JSON. Olá toonote pontos genérico:

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

- `structure`seção define os nomes de coluna de saudação personalizada e o tipo de dados correspondente Olá ao converter dados tootabular. Esta seção é **opcional** , a menos que você precisa toodo mapeamento de coluna. Consulte [mapear colunas de conjunto de dados fonte dataset colunas toodestination](data-factory-map-columns.md) seção para obter mais detalhes.
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

- `structure`seção define os nomes de coluna de saudação personalizada e o tipo de dados correspondente Olá ao converter dados tootabular. Esta seção é **opcional** , a menos que você precisa toodo mapeamento de coluna. Consulte [mapear colunas de conjunto de dados fonte dataset colunas toodestination](data-factory-map-columns.md) seção para obter mais detalhes.
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

Se você tiver Olá a tabela no banco de dados SQL a seguir:

| ID | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | Davi |
| 2 | 20170120 | 3500 | Pedro |
| 3 | 20170121 | 4000 | Jason |

e, para cada registro, você espera que o objeto JSON tooa toowrite em Olá formato a seguir:
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

saudação de conjunto de dados com saída **JsonFormat** tipo é definido da seguinte maneira: (definição parcial com partes relevantes apenas Olá). Mais especificamente, `structure` seção define os nomes de propriedade Olá personalizado no arquivo de destino, `nestingSeparator` (o padrão é ".") são usados tooidentify Olá aninhar camada do nome de saudação. Esta seção é **opcional** a menos que você deseja o nome da propriedade Olá toochange comparando com o nome da coluna de origem ou aninhar algumas das propriedades de saudação.

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

## <a name="avro-format"></a>Formato AVRO
Se você deseja tooparse Olá Avro arquivos ou gravar dados saudação no formato Avro, defina Olá `format` `type` propriedade muito**AvroFormat**. Não é necessário toospecify as propriedades na seção de formato de saudação na seção de typeProperties hello. Exemplo:

```json
"format":
{
    "type": "AvroFormat",
}
```

formato de Avro toouse em uma tabela de Hive, você pode consultar muito[tutorial do Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).

Observe Olá pontos a seguir:  

* Não há suporte para [tipos de dados complexos](http://avro.apache.org/docs/current/spec.html#schema_complex) (registros, enumerações, matrizes, mapas, uniões e fixo).

## <a name="orc-format"></a>Formato ORC
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

## <a name="parquet-format"></a>Formato Parquet
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

## <a name="compression-support"></a>Suporte à compactação
O processamento de grandes conjuntos de dados pode causar afunilamentos de E/S e de rede. Portanto, dados compactados em repositórios podem não apenas acelerar a transferência de dados pela rede hello e economizar espaço em disco, mas também abrir melhorias significativas de desempenho no processamento de big data. No momento, a compactação tem suporte para repositórios de dados baseados em arquivo, por exemplo, Blob do Azure ou o Sistema de Arquivos Local.  

compactação toospecify para um conjunto de dados, use Olá **compactação** propriedade do conjunto de dados do hello JSON como Olá exemplo a seguir:   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

Suponha que o conjunto de dados de exemplo hello é usado como saída de saudação de uma atividade de cópia, Olá Copiar atividade compacta Olá dados de saída com codec GZIP usando taxa ideal e, em seguida, gravar dados saudação compactado em um arquivo denominado pagecounts.csv.gz em Olá armazenamento de BLOBs do Azure.

> [!NOTE]
> Não há suporte para configurações de compactação de dados em Olá **AvroFormat**, **OrcFormat**, ou **ParquetFormat**. Ao ler os arquivos nos seguintes formatos, fábrica de dados detecta e usa o codec de compactação de saudação nos metadados de saudação. Ao escrever toofiles nesses formatos, fábrica de dados escolhe o codec de compactação saudação padrão para esse formato. Por exemplo, ZLIB para OrcFormat e SNAPPY para ParquetFormat.   

Olá **compactação** seção tem duas propriedades:  

* **Tipo:** codec de compactação hello, que pode ser **GZIP**, **Deflate**, **BZIP2**, ou **ZipDeflate**.  
* **Nível:** taxa de compactação hello, que pode ser **ideal** ou **mais rápido**.

  * **Mais rápido:** operação de compactação de saudação deve ser concluída assim que possível, mesmo se o arquivo resultante Olá ideal não é compactado.
  * **Ideal**: operação de compactação Olá deve ser ideal compactada, mesmo se a operação Olá leva um toocomplete de tempo mais longo.

    Para saber mais, veja o tópico [Nível de compactação](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) .

Quando você especifica `compression` propriedade em um conjunto de dados de entrada JSON, pipeline Olá pode ler dados compactados fonte Olá; e quando você especificar a propriedade de saudação em um conjunto de dados de saída JSON, atividade de cópia Olá pode gravar o destino de toohello dados compactados. Aqui estão alguns exemplos de cenários:

* Ler dados GZIP compactado de um blob do Azure, descompactam e gravar o banco de dados SQL do Azure tooan de dados de resultado. Definir o conjunto de dados entrado de BLOBs do Azure do hello com hello `compression` `type` propriedade JSON como GZIP.
* Ler dados de um arquivo de texto sem formatação do sistema de arquivos local, compactá-los usando o formato GZip e gravar Olá compactado dados tooan BLOBs do Azure. Definir um conjunto de dados de Blob do Azure de saída com hello `compression` `type` propriedade JSON como GZip.
* Arquivo. zip de leitura de servidor FTP, descompactam arquivos Olá tooget e levadas para esses arquivos no repositório Azure Data Lake. Definir um conjunto de dados FTP de entrada com hello `compression` `type` propriedade JSON como ZipDeflate.
* Ler dados de compactado GZIP de um blob do Azure, descompactam, compactá-los usando BZIP2 e gravar dados de resultado tooan BLOBs do Azure. Definir entrada dataset de BLOBs do Azure Olá com `compression` `type` definir tooGZIP e Olá conjunto de dados de saída com `compression` `type` definido tooBZIP2 nesse caso.   


## <a name="next-steps"></a>Próximas etapas
Consulte Olá artigos para repositórios de dados baseada em arquivo com suporte do Azure Data Factory a seguir:

- [Armazenamento de Blobs do Azure](data-factory-azure-blob-connector.md)
- [Repositório Azure Data Lake](data-factory-azure-datalake-connector.md)
- [FTP](data-factory-ftp-connector.md)
- [HDFS](data-factory-hdfs-connector.md)
- [Sistema de Arquivos](data-factory-onprem-file-system-connector.md)
- [Amazon S3](data-factory-amazon-simple-storage-service-connector.md)
