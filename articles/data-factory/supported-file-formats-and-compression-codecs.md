---
title: Formatos de arquivo com suporte no Azure Data Factory| Microsoft Docs
description: "Este tópico descreve os formatos de arquivo e os códigos de compactação com suporte nos conectores baseados em arquivo no Azure Data Factory."
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.topic: article
ms.date: 11/21/2017
ms.author: jingwang
ms.openlocfilehash: e583c6952e02c4a93f56594f6392f1d9a260dce0
ms.sourcegitcommit: 62eaa376437687de4ef2e325ac3d7e195d158f9f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2017
---
# <a name="supported-file-formats-and-compression-codecs-in-azure-data-factory"></a>Formatos de arquivo e codecs de compactação com suporte no Azure Data Factory

*Este tópico se aplica aos seguintes conectores: [Amazon S3](connector-amazon-simple-storage-service.md), [Blob do Azure](connector-azure-blob-storage.md), [Azure Data Lake Store](connector-azure-data-lake-store.md), [Armazenamento de Arquivos do Azure](connector-azure-file-storage.md), [Sistema de Arquivos](connector-file-system.md), [FTP](connector-ftp.md), [HDFS](connector-hdfs.md), [HTTP](connector-http.md) e [SFTP](connector-sftp.md).*

Se você quiser **copiar arquivos no estado em que se encontram** entre repositórios baseados em arquivo (cópia binária), ignore a seção de formato nas duas definições de conjunto de dados de entrada e de saída. Se você quiser **analisar ou gerar arquivos com um formato específico**, o Azure Data Factory dará suporte aos seguintes tipos de formato de arquivo:

* [Formato de texto](#text-format)
* [Formato JSON](#json-format)
* [Formato Avro](#avro-format)
* [Formato ORC](#orc-format)
* [Formato Parquet](#parquet-format)

> [!NOTE]
> Este artigo aplica-se à versão 2 do Data Factory, que está atualmente em versão prévia. Se você usar a versão 1 do serviço do Data Factory, que está em GA (disponibilidade geral), consulte os [formatos de arquivo e compactação com suporte no Data Factory versão 1](v1//data-factory-supported-file-and-compression-formats.md).

> [!TIP]
> Saiba como a atividade de cópia mapeia seus dados de origem até o coletor da seção [Mapeamento de esquema na atividade de cópia](copy-activity-schema-and-type-mapping.md), incluindo como os metadados são determinados com base nas suas configurações de formato de arquivo e dicas sobre quando especificar o [conjunto de dados `structure`](concepts-datasets-linked-services.md#dataset-structure).

## <a name="text-format"></a>Formato de texto

Se você quiser ler um arquivo de texto ou gravar em um arquivo de texto, defina a propriedade `type` na seção `format` do conjunto de dados para **TextFormat**. Você também pode especificar as seguintes propriedades **opcionais** na seção `format`. Veja a seção [Exemplo de TextFormat](#textformat-example) sobre a configuração.

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| columnDelimiter |O caractere usado para separar as colunas em um arquivo. Você pode considerar o uso de um caractere não imprimível raro que não exista em seus dados. Por exemplo, especifique "\u0001", que representa o SOH (início do título). |Somente um caractere é permitido. O valor **padrão** é **vírgula (‘,’)**. <br/><br/>Para usar um caractere Unicode, consulte [Caracteres Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) para obter o código correspondente. |Não |
| rowDelimiter |O caractere usado para separar as linhas em um arquivo. |Somente um caractere é permitido. O valor **padrão** é um dos seguintes valores na leitura: **["\r\n", "\r" e "\n"]** e **"\r\n"** na gravação. |Não |
| escapeChar |O caractere especial usado como escape do delimitador de coluna no conteúdo do arquivo de entrada. <br/><br/>Não é possível especificar ambos escapeChar e quoteChar para uma tabela. |Somente um caractere é permitido. Nenhum valor padrão. <br/><br/>Por exemplo, se tiver a vírgula (,) como o delimitador de coluna, mas quiser ter o caractere de vírgula no texto (exemplo: "Hello, world"), você poderá definir '$' como o caractere de escape e usar a cadeia de caracteres "Hello$, world" na fonte. |Não |
| quoteChar |O caractere usado para citar um valor de cadeia de caracteres. Os delimitadores de linha e coluna dentro dos caracteres de aspas seriam tratados como parte do valor de cadeia de caracteres. Essa propriedade é aplicável a ambos os conjuntos de dados de entrada e de saída.<br/><br/>Não é possível especificar ambos escapeChar e quoteChar para uma tabela. |Somente um caractere é permitido. Nenhum valor padrão. <br/><br/>Por exemplo, se tiver a vírgula (,) como o delimitador de coluna, mas quiser ter o caractere de vírgula no texto (exemplo: <Hello, world>), você poderá definir " (aspas duplas) como o caractere de citação e usar a cadeia de caracteres "Hello, world" na origem. |Não |
| nullValue |Um ou mais caracteres usados para representar um valor nulo. |Um ou mais caracteres. Os valores **padrão** são **"\N" e "NULL"** na leitura e **"\N"** na gravação. |Não |
| encodingName |Especifique o nome de codificação. |Um nomes de codificação válido. Consulte [Propriedade Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx). Por exemplo: windows-1250 ou shift_jis. O valor **padrão** é **UTF-8**. |Não |
| firstRowAsHeader |Especifica se a primeira linha será considerada como cabeçalho. Para um conjunto de dados de entrada, o Data Factory lê a primeira linha como cabeçalho. Para um conjunto de dados de saída, o Data Factory lê a primeira linha como cabeçalho. <br/><br/>Veja [Cenários para usar o `firstRowAsHeader` e o `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para cenários de exemplo. |True <br/><b>False (padrão)</b> |Não |
| skipLineCount |Indica o número de linhas a serem ignoradas ao ler dados de arquivos de entrada. Se skipLineCount e firstRowAsHeader forem especificados, as linhas serão ignoradas pela primeira vez e, em seguida, as informações de cabeçalho serão lidas do arquivo de entrada. <br/><br/>Veja [Cenários para usar o `firstRowAsHeader` e o `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para cenários de exemplo. |Número inteiro |Não |
| treatEmptyAsNull |Especifica se uma cadeia de caracteres nula ou vazia será ou não tratada como um valor nulo ao ler dados de um arquivo de entrada. |**True (padrão)**<br/>Falso |Não |

### <a name="textformat-example"></a>Exemplo de TextFormat

Na definição de JSON a seguir para um conjunto de dados, algumas das propriedades opcionais são especificadas.

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

Para usar um `escapeChar` em vez de `quoteChar`, substitua a linha com `quoteChar` por este escapeChar:

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>Cenários de uso de firstRowAsHeader e skipLineCount

* Você está copiando de uma fonte que não é de arquivo para um arquivo de texto e deseja adicionar uma linha de cabeçalho que contém os metadados de esquema (por exemplo: esquema SQL). Especifique `firstRowAsHeader` como true no conjunto de dados de saída para esse cenário.
* Você está copiando de um arquivo de texto contendo uma linha de cabeçalho para um coletor que não é em arquivo e gostaria de remover essa linha. Especifique `firstRowAsHeader` como true no conjunto de dados de entrada.
* Você está copiando de um arquivo de texto e deseja ignorar algumas linhas no início que não são informações de dados nem de cabeçalho. Especifique `skipLineCount` para indicar o número de linhas a serem ignoradas. Se o restante do arquivo contiver uma linha de cabeçalho, você também poderá especificar `firstRowAsHeader`. Se `skipLineCount` e `firstRowAsHeader` forem especificados, as linhas serão ignoradas pela primeira vez e, em seguida, as informações de cabeçalho serão lidas do arquivo de entrada

## <a name="json-format"></a>Formato JSON

Para **importar/exportar um arquivo JSON no estado em que se encontra de/para o Azure Cosmos DB**, consulte a seção Importar/exportar documentos JSON do artigo [Move data to/from Azure Cosmos DB](connector-azure-cosmos-db.md) (Mover dados de/para o Azure Cosmos DB).

Se você quiser analisar os arquivos de JSON ou gravar os dados no formato JSON, defina a propriedade `type` na seção `format` como **JsonFormat**. Você também pode especificar as seguintes propriedades **opcionais** na seção `format`. Veja a seção [Exemplo de JsonFormat](#jsonformat-example) sobre como configurar.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| filePattern |Indique o padrão de dados armazenados em cada arquivo JSON. Os valores permitidos são: **setOfObjects** e **arrayOfObjects**. O valor **padrão** é **setOfObjects**. Veja a seção [Padrões de arquivo JSON](#json-file-patterns) para obter detalhes sobre esses padrões. |Não |
| jsonNodeReference | Se você quiser fazer uma iteração e extrair dados de objetos dentro de um campo de matriz com o mesmo padrão, especifique o caminho JSON da matriz. Esta propriedade só terá suporte na cópia de dados de arquivos JSON. | Não |
| jsonPathDefinition | Especifique a expressão de caminho JSON para cada mapeamento de coluna com um nome de coluna personalizado (iniciar com letra minúscula). Esta propriedade só terá suporte na cópia de dados de arquivos JSON, e você pode extrair dados de objeto ou de matriz. <br/><br/> Para os campos sob o objeto root, comece com root $; para os campos dentro da matriz escolhidos pela propriedade `jsonNodeReference`, comece do elemento de matriz. Veja a seção [Exemplo de JsonFormat](#jsonformat-example) sobre como configurar. | Não |
| encodingName |Especifique o nome de codificação. Para obter a lista de nomes de codificação válidos, consulte: Propriedade [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) . Por exemplo: windows-1250 ou shift_jis. O valor **padrão** é **UTF-8**. |Não |
| nestingSeparator |Caractere que é usado para separar os níveis de aninhamento. O valor padrão é '.' (ponto). |Não |

### <a name="json-file-patterns"></a>Padrões de arquivo JSON

A atividade de cópia pode analisar os padrões de arquivos JSON a seguir:

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

Consulte os exemplos a seguir ao copiar dados de arquivos JSON. Os pontos genéricos a serem observados:

**Exemplo 1: extrair dados de objeto e de matriz**

Neste exemplo, você espera que um objeto JSON de raiz seja mapeado para um único registro no resultado tabular. Se você tiver um arquivo JSON com o seguinte conteúdo:  

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

e quiser copiá-lo para uma tabela SQL do Azure no formato a seguir, ao extrair dados dos objetos e da matriz:

| ID | deviceType | targetResourceType | resourceManagmentProcessRunId | occurrenceTime |
| --- | --- | --- | --- | --- |
| ed0e4960-d9c5-11e6-85dc-d7996816aad3 | Computador | Microsoft.Compute/virtualMachines | 827f8aaa-ab72-437c-ba48-d8917a7336a3 | 13/01/2017 11:24:37 |

O conjunto de dados de entrada com o tipo **JsonFormat** é definido da seguinte maneira: (definição parcial com apenas as partes relevantes). Mais especificamente:

- A seção `structure` define os nomes de coluna personalizada e o tipo de dados correspondente ao converter em dados tabulares. Esta seção é **opcional**, a menos que você tenha de fazer o mapeamento de colunas. Para obter mais informações, consulte [Mapear colunas de conjunto de dados de origem para colunas de conjunto de dados de destino](copy-activity-schema-and-type-mapping.md).
- `jsonPathDefinition` especifica o caminho JSON para cada coluna que indica de onde extrair os dados. Para copiar dados de matriz, você pode usar `array[x].property` para extrair o valor da determinada propriedade do objeto `xth` ou usar `array[*].property` para localizar o valor de qualquer objeto que contenha essa propriedade.

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

**Exemplo 2: cruzar aplicar vários objetos com o mesmo padrão da matriz**

Neste exemplo, você espera transformar um objeto JSON de raiz em vários registros no resultado tabular. Se você tiver um arquivo JSON com o seguinte conteúdo:

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

e você deseja copiá-lo para uma tabela do Azure SQL no formato a seguir, ao nivelar os dados de dentro da matriz e fazer uma união cruzada com as informações comuns de root:

| `ordernumber` | `orderdate` | `order_pd` | `order_price` | `city` |
| --- | --- | --- | --- | --- |
| 01 | 20170122 | P1 | 23 | `[{"sanmateo":"No 1"}]` |
| 01 | 20170122 | P2 | 13 | `[{"sanmateo":"No 1"}]` |
| 01 | 20170122 | P3 | 231 | `[{"sanmateo":"No 1"}]` |


O conjunto de dados de entrada com o tipo **JsonFormat** é definido da seguinte maneira: (definição parcial com apenas as partes relevantes). Mais especificamente:

- A seção `structure` define os nomes de coluna personalizada e o tipo de dados correspondente ao converter em dados tabulares. Esta seção é **opcional**, a menos que você tenha de fazer o mapeamento de colunas. Para obter mais informações, consulte [Mapear colunas de conjunto de dados de origem para colunas de conjunto de dados de destino](copy-activity-schema-and-type-mapping.md).
- `jsonNodeReference` indica iterar e extrair dados dos objetos com o mesmo padrão da **matriz** `orderlines`.
- `jsonPathDefinition` especifica o caminho JSON para cada coluna que indica de onde extrair os dados. Neste exemplo, `ordernumber`, `orderdate` e `city` estão sob o objeto raiz com o caminho do JSON começando com `$.`, enquanto `order_pd` e `order_price` estão definidos com um caminho derivado do elemento da matriz sem `$.`.

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

**Observe os seguintes pontos:**

* Se `structure` e `jsonPathDefinition` não forem definidos no conjunto de dados do Data Factory, a atividade de cópia detectará o esquema do primeiro objeto e mesclará todo o objeto.
* Se a entrada JSON tiver uma matriz por padrão, a atividade de cópia converterá o valor da matriz inteira em uma cadeia de caracteres. Você pode optar por extrair dados dele usando o `jsonNodeReference` e/ou o `jsonPathDefinition` ou ignorá-lo ao não especificá-lo no `jsonPathDefinition`.
* Se houver nomes duplicados no mesmo nível, a atividade de cópia selecionará o último entre eles.
* Os nomes de propriedade diferenciam maiúsculas de minúsculas. Duas propriedades com o mesmo nome, mas com maiúsculas e minúsculas diferentes são tratadas como duas propriedades separadas.

**Caso 2: gravação de dados no arquivo JSON**

Se você tiver a tabela a seguir no Banco de Dados SQL:

| ID | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | Davi |
| 2 | 20170120 | 3500 | Pedro |
| 3 | 20170121 | 4000 | Jason |

e, para cada registro, você espera gravar em um objeto JSON neste formato:

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

O conjunto de dados de saída com o tipo **JsonFormat** é definido da seguinte maneira: (definição parcial com apenas as partes relevantes). Mais especificamente, a seção `structure` define os nomes de propriedade personalizada no arquivo de destino, `nestingSeparator` (o padrão é ".") que são usados para identificar a camada de aninhamento do nome. Esta seção é **opcional**, a menos que você queira alterar o nome da propriedade em comparação ao nome da coluna de origem ou aninhar algumas das propriedades.

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

Se você quiser analisar os arquivos Avro ou gravar os dados no formato Avro, defina a propriedade `format` `type` como **AvroFormat**. Não será necessário especificar nenhuma propriedade na seção Formato dentro da seção typeProperties. Exemplo:

```json
"format":
{
    "type": "AvroFormat",
}
```

Para usar o formato Avro em uma tabela de Hive, confira [Tutorial do Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).

Observe os seguintes pontos:

* Não há suporte para [tipos de dados complexos](http://avro.apache.org/docs/current/spec.html#schema_complex) (registros, enumerações, matrizes, mapas, uniões e fixo).

## <a name="orc-format"></a>Formato ORC

Se você quiser analisar os arquivos ORC ou gravar os dados no formato ORC, defina a propriedade `format` `type` como **OrcFormat**. Não será necessário especificar nenhuma propriedade na seção Formato dentro da seção typeProperties. Exemplo:

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> Se você não estiver copiando arquivos ORC **como são** entre repositórios de dados locais e na nuvem, você precisará instalar o JRE 8 (Java Runtime Environment) no computador do gateway. Um gateway de 64 bits exige JRE de 64 bits, enquanto um gateway de 32 bits exige JRE de 32 bits. Você pode encontrar as duas versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605). Escolha aquela que for apropriada.
>

Observe os seguintes pontos:

* Não há suporte para tipos de dados complexos (STRUCT, MAP, LIST e UNION)
* O arquivo ORC tem três [opções de compactação](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB e SNAPPY. O Data Factory dá suporte à leitura de dados de arquivo ORC em qualquer um dos formatos compactados acima. Ele usa o codec de compactação nos metadados para ler os dados. No entanto, ao gravar um arquivo ORC, o Data Factory escolhe ZLIB, que é o padrão para ORC. Não há nenhuma opção para substituir esse comportamento neste momento.

## <a name="parquet-format"></a>Formato Parquet

Se você quiser analisar os arquivos Parquet ou gravar os dados no formato Parquet, defina a propriedade `format` `type` como **ParquetFormat**. Não será necessário especificar nenhuma propriedade na seção Formato dentro da seção typeProperties. Exemplo:

```json
"format":
{
    "type": "ParquetFormat"
}
```

> [!IMPORTANT]
> Se você não estiver copiando arquivos Parquet **no estado em que se encontram** entre armazenamentos de dados locais e na nuvem, você precisará instalar o JRE 8 (Java Runtime Environment) no computador do gateway. Um gateway de 64 bits exige JRE de 64 bits, enquanto um gateway de 32 bits exige JRE de 32 bits. Você pode encontrar as duas versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605). Escolha aquela que for apropriada.
>

Observe os seguintes pontos:

* Não há suporte para tipos de dados complexos (MAP, LIST)
* O arquivo Parquet tem as seguintes opções relacionadas à compactação: NONE, SNAPPY, GZIP e LZO. O Data Factory dá suporte à leitura de dados de arquivo ORC em qualquer um dos formatos compactados acima. Ele usa o codec de compactação nos metadados para ler os dados. No entanto, ao gravar um arquivo Parquet, o Data Factory escolhe SNAPPY, que é o padrão para o formato Parquet. Não há nenhuma opção para substituir esse comportamento neste momento.

## <a name="compression-support"></a>Suporte à compactação

O Azure Data Factory dá suporte para compactar/descompactar dados durante a cópia. Quando você especifica a propriedade `compression` em um conjunto de dados de entrada, a atividade de cópia lê os dados compactados da origem e descompacta-os e, quando você especifica a propriedade em um conjunto de dados de saída, a atividade de cópia compacta e grava os dados no coletor. Aqui estão alguns exemplos de cenários:

* Ler dados compactados em GZIP de um blob do Azure, descompactá-los e gravar os dados resultantes em um banco de dados do SQL Azure. Você define o conjunto de dados de Blob do Azure de entrada com a propriedade `compression` `type` como GZIP.
* Ler dados de um arquivo de texto sem formatação do Sistema de arquivos local, compactá-los usando o formato GZip e gravar os dados compactados em um blob do Azure. Você define um conjunto de dados de Blob do Azure de saída com a propriedade `compression` `type` como GZip.
* Leia o arquivo .zip do servidor FTP, descompacte-o para obter os arquivos e inclua-os no Azure Data Lake Store. Você define um conjunto de dados FTP de entrada com a propriedade `compression` `type` como ZipDeflate.
* Ler dados compactados em GZIP de um blob do Azure, descompactá-los, compactá-los usando BZIP2 e gravar os dados de resultado em um blob do Azure. Você define o conjunto de dados de Blob do Azure de entrada com `compression` `type` definido como GZIP e o conjunto de dados de saída com `compression` `type` definido como BZIP2.

Para especificar a compactação de um conjunto de dados, use a propriedade **compactação** no conjunto de dados JSON, como no exemplo a seguir:   

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": {
            "referenceName": "StorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "fileName": "pagecounts.csv.gz",
            "folderPath": "compression/file/",
            "format": {
                "type": "TextFormat"
            },
            "compression": {
                "type": "GZip",
                "level": "Optimal"
            }
        }
    }
}
```

A seção **compactação** tem duas propriedades:

* **Tipo:** o codec de compactação, que pode ser **GZIP**, **Deflate**, **BZIP2** ou **ZipDeflate**.
* **Nível:** a taxa de compactação, que pode ser **Ideal** ou **Mais rápida**.

  * **Mais rápida:** a operação de compactação deve ser concluída o mais rápido possível, mesmo se o arquivo resultante não for compactado da maneira ideal.
  * **Ideal**: a operação de compactação deve ser concluída da maneira ideal, mesmo se a operação demorar mais tempo para ser concluída.

    Para saber mais, veja o tópico [Nível de compactação](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) .

> [!NOTE]
> Não há suporte para configurações de compactação de dados no **AvroFormat**, **OrcFormat** ou **ParquetFormat**. Ao ler arquivos nesses formatos, o Data Factory detecta e usa o codec de compactação nos metadados. Ao gravar em arquivos em um desses formatos, o Data Factory escolhe o codec de compactação padrão para esse formato. Por exemplo, ZLIB para OrcFormat e SNAPPY para ParquetFormat.

## <a name="next-steps"></a>Próximas etapas

Consulte os artigos a seguir para armazenamentos de dados baseados em arquivo com suporte pelo Azure Data Factory:

- [Azure Blob Storage connector](connector-azure-blob-storage.md) (Conector do Armazenamento de Blobs do Azure)
- [Azure Data Lake Store connector](connector-azure-data-lake-store.md) (Conector do Azure Data Lake Store)
- [Amazon S3 connector](connector-amazon-simple-storage-service.md) (Conector do Amazon S3)
- [File System connector](connector-file-system.md) (Conector de sistema de arquivos)
- [FTP connector](connector-ftp.md) (Conector de FTP)
- [SFTP connector](connector-sftp.md) (Conector de SFTP)
- [HDFS connector](connector-hdfs.md) (Conector de HDFS)
- [HTTP connector](connector-http.md) (Conector de HTTP)