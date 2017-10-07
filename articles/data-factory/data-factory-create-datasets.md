---
title: "conjuntos de dados de aaaCreate na fábrica de dados do Azure | Microsoft Docs"
description: "Saiba como conjuntos de dados toocreate na fábrica de dados do Azure, com exemplos que usam propriedades, como deslocamento e anchorDateTime."
keywords: criar conjunto de dados, exemplo de conjunto de dados, exemplo de deslocamento
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a>Conjuntos de dados no Azure Data Factory
Este artigo descreve o que são conjuntos de dados, como eles são definidos no formato JSON e como são usados em pipelines do Azure Data Factory. Ele fornece detalhes sobre cada seção (por exemplo, estrutura, disponibilidade e política) na definição de JSON de conjunto de dados de saudação. Olá artigo também fornece exemplos de uso Olá **deslocamento**, **anchorDateTime**, e **estilo** propriedades em uma definição de conjunto de dados JSON.

> [!NOTE]
> Se você for novo tooData fábrica, consulte [tooAzure Introdução Data Factory](data-factory-introduction.md) para obter uma visão geral. Se você não tiver experiência prática com a criação de fábricas de dados, você pode obter um melhor entendimento por leitura Olá [tutorial de transformação de dados](data-factory-build-your-first-pipeline.md) e hello [tutorial de movimentação de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="overview"></a>Visão geral
Uma fábrica de dados pode ter um ou mais pipelines. Um **pipeline** é um agrupamento lógico de **atividades** que juntas executam uma tarefa. atividades de saudação em um pipeline definem ações tooperform em seus dados. Por exemplo, você pode usar uma cópia de dados de toocopy de atividade de um tooAzure do SQL Server local armazenamento de Blob. Em seguida, você pode usar uma atividade de Hive que executa um script de Hive em um dado de tooprocess do cluster HDInsight do Azure de dados de saída de tooproduce de armazenamento de Blob. Por fim, você pode usar uma segunda cópia atividade toocopy Olá saída dados tooAzure SQL Data Warehouse, na parte superior que inteligência comercial (BI) reporting soluções são criadas. Para obter mais informações sobre pipelines e atividades, consulte [Pipelines e atividades no Azure Data Factory](data-factory-create-pipelines.md).

Uma atividade pode usar zero ou mais **conjuntos de dados** de entrada e gerar um ou mais conjuntos de dados de saída. Um conjunto de dados de entrada representa a entrada de saudação para uma atividade no pipeline hello e um conjunto de dados de saída representa a saída de hello atividade hello. Conjuntos de dados identificam dados em armazenamentos de dados diferentes, como tabelas, arquivos, pastas e documentos. Por exemplo, um conjunto de dados de Blob do Azure Especifica Olá contêiner de blob e a pasta no armazenamento de Blob do qual Olá pipeline deve ler dados de saudação. 

Antes de criar um conjunto de dados, criar um **serviço vinculado** toolink toohello fábrica de dados de repositório de dados. Serviços vinculados são bem semelhantes às cadeias de caracteres de conexão, que definem informações de conexão de Olá necessárias para os recursos do Data Factory tooconnect tooexternal. Conjuntos de dados identificam os dados Olá vinculado armazenamentos de dados, como tabelas SQL, arquivos, pastas e documentos. Por exemplo, um armazenamento do Azure vinculada links de serviço com uma fábrica de dados de toohello de conta de armazenamento. Um conjunto de dados de Blob do Azure representa o contêiner de blob hello e a pasta de Olá que contém a saudação blobs entrada toobe processado. 

Veja abaixo um cenário de exemplo. toocopy dados do banco de dados SQL tooa de armazenamento de Blob, criar dois serviços vinculados: o armazenamento do Azure e banco de dados do SQL Azure. Em seguida, crie dois conjuntos de dados: conjunto de dados de Blob do Azure (que refere-se o serviço de armazenamento do Azure vinculada toohello) e o conjunto de dados de tabela do SQL Azure (que refere-se o serviço de banco de dados do SQL Azure vinculado toohello). Olá armazenamento do Azure e banco de dados do SQL Azure serviços vinculados contêm cadeias de caracteres de conexão que usa fábrica de dados em tempo de execução tooconnect tooyour armazenamento do Azure e banco de dados SQL Azure, respectivamente. conjunto de dados de Blob do Azure Olá Especifica o contêiner de blob hello e a pasta de blob que contém blobs de entrada hello em seu armazenamento de Blob. conjunto de dados de tabela do SQL Azure Olá Especifica a tabela SQL de saudação em seus dados de saudação do toowhich de banco de dados SQL é toobe copiado.

Olá diagrama a seguir mostra Olá relações entre pipeline, atividade, conjunto de dados e serviços vinculados na fábrica de dados: 

![Relação entre pipeline, atividade e conjunto de dados, serviços vinculados](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a>Conjunto de dados do JSON
Um conjunto de dados no Data Factory é definido no formato JSON da seguinte maneira:

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

Olá, a tabela a seguir descreve as propriedades no hello acima JSON:   

| Propriedade | Descrição | Obrigatório | Padrão |
| --- | --- | --- | --- |
| name |Nome do conjunto de dados de saudação. Confira [Azure Data Factory - Regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura. |Sim |ND |
| type |Tipo de conjunto de dados de saudação. Especifique um dos tipos de saudação com suporte pela fábrica de dados (por exemplo: AzureBlob, AzureSqlTable). <br/><br/>Para obter detalhes, consulte [Tipo de conjunto de dados](#Type). |Sim |ND |
| estrutura |Esquema de conjunto de dados de saudação.<br/><br/>Para obter detalhes, consulte [Estrutura de conjunto de dados](#Structure). |Não |ND |
| typeProperties | Propriedades do tipo Hello são diferentes para cada tipo (por exemplo: Blob do Azure, tabela do SQL Azure). Para obter detalhes sobre os tipos de saudação com suporte e suas propriedades, consulte [tipo de conjunto de dados](#Type). |Sim |ND |
| externo | Booliano sinalizador toospecify se um conjunto de dados explicitamente produzido por um pipeline da fábrica de dados ou não. Se o conjunto de dados de entrada de saudação para uma atividade não é produzido pelo pipeline atual Olá, defina esse sinalizador tootrue. Defina tootrue este sinalizador de conjunto de dados entrada da atividade primeiro Olá Olá no pipeline de saudação.  |Não |false |
| disponibilidade | Define Olá janela de processamento (por exemplo, por hora ou diariamente) ou hello dividindo o modelo para conjunto de dados de produção de hello. Cada unidade de dados consumida e produzida por uma execução de atividade é chamada de uma fatia de dados. Se a disponibilidade de saudação de um conjunto de dados de saída for conjunto toodaily (frequência - dia, o intervalo de-1), uma fatia é produzida diariamente. <br/><br/>Para obter detalhes, consulte [Disponibilidade do conjunto de dados](#Availability). <br/><br/>Para obter detalhes sobre o conjunto de dados Olá dividindo o modelo, consulte Olá [de agendamento e execução](data-factory-scheduling-and-execution.md) artigo. |Sim |ND |
| policy |Define os critérios de saudação ou condição Olá que devem ser atendidos por fatias de conjunto de dados de saudação. <br/><br/>Para obter detalhes, consulte Olá [política de conjunto de dados](#Policy) seção. |Não |ND |

## <a name="dataset-example"></a>Exemplo de conjunto de dados
Olá exemplo a seguir, Olá dataset representa uma tabela chamada **MyTable** em um banco de dados SQL.

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

Observe Olá pontos a seguir:

* **tipo** é definido tooAzureSqlTable.
* **tableName** propriedade type (tipo de específico tooAzureSqlTable) é definida tooMyTable.
* **linkedServiceName** refere-se o serviço de tooa vinculado do tipo AzureSqlDatabase, que é definido no seguinte trecho JSON a saudação. 
* **frequência de disponibilidade** é definido como tooDay, e **intervalo** é definido too1. Isso significa que essa fatia do conjunto de dados de saudação é produzida diariamente.  

**AzureSqlLinkedService** é definido da seguinte maneira:

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

Em Olá precede o trecho JSON:

* **tipo** é definido tooAzureSqlDatabase.
* **connectionString** propriedade de tipo Especifica o banco de dados SQL tooa de tooconnect de informações.  

Como você pode ver, hello serviço vinculado define como banco de dados do SQL tooconnect tooa. saudação de conjunto de dados define qual tabela é usada como uma entrada e saída para a atividade de saudação em um pipeline.   

> [!IMPORTANT]
> A menos que um conjunto de dados é produzido pelo pipeline hello, ele deve ser marcado como **externo**. Essa configuração geralmente se aplica a tooinputs da primeira atividade em um pipeline.   


## <a name="Type"></a> Tipo de conjunto de dados
tipo de saudação do conjunto de dados Olá depende de repositório de dados Olá que você usar. Consulte Olá para obter uma lista de repositórios de dados com suporte pela fábrica de dados a tabela a seguir. Clique em um toolearn de repositório de dados como toocreate um serviço vinculado e um conjunto de dados para os dados armazenam.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Armazenamentos de dados com * podem ser locais ou IaaS (infraestrutura como serviço) do Azure. Esses armazenamentos de dados exigem tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).

No exemplo hello na seção anterior hello, tipo de saudação do conjunto de dados de saudação é definido muito**AzureSqlTable**. Da mesma forma, para um conjunto de dados de Blob do Azure, Olá tipo do conjunto de dados de saudação é definido muito**AzureBlob**, conforme mostrado no hello JSON a seguir:

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

## <a name="Structure"></a>Estrutura do conjunto de dados
Olá **estrutura** seção é opcional. Ele define o esquema de Olá do conjunto de dados Olá, que contém uma coleção de nomes e tipos de dados das colunas. Você usar Olá estrutura seção tooprovide informações de tipo é usado tooconvert tipos e mapear colunas de destino de toohello Olá fonte. Olá exemplo a seguir, Olá dataset tem três colunas: `slicetimestamp`, `projectname`, e `pageviews`. Elas são do tipo String, String e Decimal, respectivamente.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Cada coluna na estrutura de saudação contém Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| name |Nome da coluna de saudação. |Sim |
| type |Tipo de dados da coluna de saudação.  |Não |
| culture |. Toobe cultura baseada em rede usada quando a saudação é um tipo .NET: `Datetime` ou `Datetimeoffset`. saudação padrão é `en-us`. |Não |
| formato |Formatar toobe de cadeia de caracteres usada quando Olá é um tipo .NET: `Datetime` ou `Datetimeoffset`. |Não |

Olá diretrizes a seguir ajudarão a determinar quando tooinclude estrutura informações e quais tooinclude em Olá **estrutura** seção.

* **Para fontes de dados estruturados**, especifique a seção de estrutura de saudação somente se você deseja mapear colunas de toosink de colunas de origem e seus nomes não são Olá mesmo. Esse tipo de fonte de dados estruturados armazena informações de esquema e o tipo de dados junto com dados de saudação em si. Exemplos de fontes de dados estruturadas incluem SQL Server, Oracle e tabela do Azure. 
  
    Como informações de tipo já estão disponíveis para fontes de dados estruturados, você não deve incluir informações de tipo quando você inclui uma seção de estrutura de saudação.
* **Para o esquema de fontes de dados de leitura (especificamente o armazenamento de Blob)**, você pode escolher dados toostore sem armazenar qualquer informação de tipo ou esquema com dados saudação. Para esses tipos de fontes de dados, inclua estrutura quando você desejar toomap fonte colunas toosink colunas. Também incluem estrutura quando Olá conjunto de dados é uma entrada para uma atividade de cópia e tipos de dados do conjunto de dados de origem devem ser tipos toonative convertido para o coletor de saudação. 
    
    Fábrica de dados oferece suporte a saudação valores para fornecer informações de tipo na estrutura a seguir: **Int16, Int32, Int64, único, Double, Decimal, Byte [], booliano, cadeia de caracteres, Guid, Datetime, Datetimeoffset e Timespan**. Esses valores são valores de tipo baseados em NET e em conformidade com CLS (Common Language Specification).

Fábrica de dados executa automaticamente conversões de tipo ao mover o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados. 
  

## <a name="dataset-availability"></a>Disponibilidade do conjunto de dados
Olá **disponibilidade** seção em um conjunto de dados define Olá janela de processamento (por exemplo, por hora, diariamente ou semanalmente) para o conjunto de dados de saudação. Para obter mais informações sobre janelas de atividades, consulte [Agendamento e execução](data-factory-scheduling-and-execution.md).

Olá seção de disponibilidade a seguir especifica que hello conjunto de dados de saída ou produzido por hora, ou conjunto de dados de entrada hello está disponível por hora:

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Se pipeline Olá Olá horas inicial e final a seguir:  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

Olá conjunto de dados de saída é produzido por hora no pipeline de saudação início e término. Portanto, cinco fatias de conjunto de dados são geradas por esse pipeline, uma para cada janela de atividades (00h à 1h, 1h às 2h, 2h às 3h, 3h às 4h e 4h às 5h). 

Olá tabela a seguir descreve propriedades que você pode usar na seção de disponibilidade hello:

| Propriedade | Descrição | Obrigatório | Padrão |
| --- | --- | --- | --- |
| frequência |Especifica a unidade de tempo de saudação de produção de fatia do conjunto de dados.<br/><br/><b>Frequência com suporte</b>: Minuto, Hora, Dia, Semana, Mês |Sim |ND |
| intervalo |Especifica um multiplicador para a frequência.<br/><br/>"Intervalo de frequência x" determina com que frequência hello fatia é produzida. Por exemplo, se você precisar hello toobe de conjunto de dados dividido por hora, definir <b>frequência</b> muito<b>hora</b>, e <b>intervalo</b> muito<b>1</b>.<br/><br/>Observe que, se você especificar **frequência** como **minuto**, você deve definir Olá intervalo toono menos de 15. |Sim |ND |
| estilo |Especifica se a fatia Olá deve ser produzida no início de saudação ou no final do intervalo de saudação.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul>Se **frequência** está definido muito**mês**, e **estilo** está definido muito**EndOfInterval**, Olá fatia é produzida no último dia do mês de saudação. Se **estilo** está definido muito**StartOfInterval**, fatia de saudação é produzida no hello primeiro dia do mês.<br/><br/>Se **frequência** está definido muito**dia**, e **estilo** está definido muito**EndOfInterval**, Olá fatia é produzida no hello última hora do dia de saudação.<br/><br/>Se **frequência** está definido muito**hora**, e **estilo** está definido muito**EndOfInterval**, Olá fatia é produzida no final de saudação de hora hello. Por exemplo, para uma fatia para Olá PM 1-2 PM período, a fatia de saudação é produzida às 14: 00. |Não |EndOfInterval |
| anchorDateTime |Define a posição absoluta Olá no tempo usado pelos limites de fatia Olá Agendador toocompute conjunto de dados. <br/><br/>Observe que se este propoerty tem partes de data mais granulares de saudação especificado frequência, Olá partes mais granulares são ignoradas. Por exemplo, se hello **intervalo** é **por hora** (frequência: hora e intervalo: 1) e hello **anchorDateTime** contém **minutos e segundos**, Olá, em seguida, partes de minutos e segundos **anchorDateTime** são ignorados. |Não |01/01/0001 |
| deslocamento |O intervalo de tempo pelo qual saudação inicial e final de todas as fatias de conjunto de dados são transferidos. <br/><br/>Observe que, se ambos os **anchorDateTime** e **deslocamento** forem especificados, resultado de saudação é shift Olá combinado. |Não |ND |

### <a name="offset-example"></a>exemplo de deslocamento
Por padrão, as fatias diárias (`"frequency": "Day", "interval": 1`) começam às 00h (meia-noite) em UTC (Tempo Universal Coordenado). Se deseja saudação inicial tempo toobe 6 horas UTC em vez disso, defina Olá deslocamento conforme Olá trecho de código a seguir: 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>Exemplo de anchorDateTime
No hello exemplo a seguir, Olá dataset é produzido cada 23 horas. Hello primeira fatia começa no tempo de saudação especificado por **anchorDateTime**, que está definido muito`2017-04-19T08:00:00` (UTC).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>exemplo de deslocamento/estilo
Olá seguinte conjunto de dados é mensal e é gerada em Olá 3º de cada mês às 8:00 (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <a name="Policy"></a>Política de conjunto de dados
Olá **política** seção na definição de conjunto de dados de saudação define os critérios de saudação ou condição Olá Olá fatias de conjunto de dados deve ser atendidos.

### <a name="validation-policies"></a>Políticas de validação
| Nome da política | Descrição | Aplicado muito| Obrigatório | Padrão |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Valida que dados Olá em **armazenamento de BLOBs do Azure** Olá de atende aos requisitos de tamanho mínimo (em megabytes). |Armazenamento do Blob do Azure |Não |ND |
| minimumRows |Valida que dados Olá em um **banco de dados do SQL Azure** ou um **tabela do Azure** contém o número mínimo de saudação de linhas. |<ul><li>Banco de Dados SQL Azure</li><li>Tabela do Azure</li></ul> |Não |ND |

#### <a name="examples"></a>Exemplos
**minimumSizeMB:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

**minimumRows:**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a>Conjuntos de dados externos
Conjuntos de dados externos são Olá aqueles que não são produzidos por um pipeline em execução na fábrica de dados hello. Se Olá conjunto de dados está marcado como **externo**, Olá **ExternalData** política pode ser definido tooinfluence Olá comportamento de disponibilidade de fatia do conjunto de dados de saudação.

A menos que um conjunto de dados seja gerado pelo Data Factory, ele deverá ser marcado como **externo**. Essa configuração geralmente se aplica a entradas toohello da primeira atividade em um pipeline, a menos que a atividade ou o encadeamento de pipeline está sendo usado.

| Nome | Descrição | Obrigatório | Valor padrão |
| --- | --- | --- | --- |
| dataDelay |tempo de Olá Olá toodelay Verificar disponibilidade de saudação de dados externa Olá Olá fornecido fatia. Por exemplo, é possível atrasar uma verificação por hora usando essa configuração.<br/><br/>Olá configuração se aplica somente toohello a hora atual.  Por exemplo, se for 1:00 PM agora e esse valor é 10 minutos, validação Olá inicia às 13:10.<br/><br/>Observe que essa configuração não afeta fatias Olá anterior. Fatias com **Hora de Término da Fatia** + **dataDelay** < **Agora** são processadas sem atrasos.<br/><br/>Vezes maior que 23:59 horas devem ser especificadas usando Olá `day.hours:minutes:seconds` formato. Por exemplo, toospecify 24 horas, não use 24:00:00. Em vez disso, use 1.00:00:00. Se você usar 24:00:00, isso será tratado como 24 dias (24.00:00:00). Para 1 dia e 4 horas, especifique 1:04:00:00. |Não |0 |
| retryInterval |tempo de espera de saudação entre uma próxima tentativa falha e hello. Essa configuração se aplica a toopresent tempo. Se a tentativa anterior de saudação falha, próxima tentativa de saudação é após Olá **retryInterval** período. <br/><br/>Se for 1:00 PM agora, começamos Olá primeira tentativa. Se Olá duração toocomplete Olá primeira verificação de validação é 1 minuto e Falha na operação de hello, Olá próxima tentativa é às 1:00 + 1 min (duração) + 1min (intervalo de repetição) = 1:02 PM. <br/><br/>Para fatias Olá anterior, não há nenhum atraso. repetição de saudação ocorre imediatamente. |Não |00:01:00 (1 minuto) |
| retryTimeout |Olá tempo limite para cada tentativa de repetição.<br/><br/>Se essa propriedade for definida too10 minutos, validação Olá deve ser concluída em 10 minutos. Se demorar mais de validação de saudação do tooperform de 10 minutos, Olá novamente o tempo limite.<br/><br/>Se todas as tentativas de saudação validação tempo limite, Olá fatia é marcada como **TimedOut**. |Não |00:10:00 (10 minutos) |
| maximumRetry |Olá número de vezes toocheck para disponibilidade de saudação de dados externos de saudação. Olá valor máximo permitido é 10. |Não |3 |


## <a name="create-datasets"></a>Criar conjuntos de dados
Você pode criar conjuntos de dados usando uma destas ferramentas ou SDKs: 

- Assistente de Cópia 
- Portal do Azure
- Visual Studio
- PowerShell
- Modelo do Azure Resource Manager
- API REST
- API do .NET

Consulte Olá tutoriais para obter instruções passo a passo para criar pipelines e conjuntos de dados usando uma dessas ferramentas ou SDKs a seguir:
 
- [Crie um pipeline com uma atividade de transformação de dados](data-factory-build-your-first-pipeline.md)
- [Crie um pipeline com uma atividade de movimentação de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Depois de um pipeline é criado e implantado, você pode gerenciar e monitorar seus pipelines usando Olá folhas portais do Azure ou um aplicativo de monitoramento e gerenciamento hello. Consulte Olá seguintes tópicos para obter instruções passo a passo: 

- [Monitorar e gerenciar pipelines usando as folhas do portal do Azure](data-factory-monitor-manage-pipelines.md)
- [Monitorar e gerenciar pipelines usando o aplicativo de monitoramento e gerenciamento de saudação](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a>Conjuntos de dados com escopo
Você pode criar conjuntos de dados que estão no escopo tooa pipeline usando Olá **conjuntos de dados** propriedade. Esses conjuntos de dados só podem ser usados por atividades dentro deste pipeline, não por atividades em outros pipelines. saudação de exemplo a seguir define um pipeline com dois conjuntos de dados (rdc InputDataset e OutputDataset rdc) toobe usado no pipeline de saudação.  

> [!IMPORTANT]
> Conjuntos de dados no escopo são suportados apenas com pipelines única (onde **pipelineMode** está definido muito**OneTime**). Confira [Pipeline avulso](data-factory-create-pipelines.md#onetime-pipeline) para obter detalhes.
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a>Próximas etapas
- Para obter mais informações sobre pipelines, consulte [Criar pipelines](data-factory-create-pipelines.md). 
- Para obter mais informações sobre como os pipelines são agendados e executados, consulte [Agendamento e execução no Azure Data Factory](data-factory-scheduling-and-execution.md). 
