---
title: "aaaAzure Data Factory - referência de script JSON | Microsoft Docs"
description: Oferece esquemas JSON para entidades do Data Factory.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a>Azure Data Factory - Referência de Script do JSON
Este artigo fornece esquemas JSON e exemplos para definir entidades do Azure Data Factory (pipeline, atividade, conjunto de dados e serviço vinculado).  

## <a name="pipeline"></a>Pipeline 
estrutura de alto nível Olá para uma definição de pipeline é o seguinte: 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Tabela a seguir descreve as propriedades de saudação no pipeline de saudação definição JSON:

| Propriedade | Descrição | Obrigatório
-------- | ----------- | --------
| name | Nome do pipeline de saudação. Especifique um nome que representa a ação Olá Olá atividade ou pipeline é toodo configurado<br/><ul><li>Número máximo de caracteres: 260</li><li>Deve começar com uma letra, um número ou um sublinhado (_)</li><li>Os seguintes caracteres não são permitidos: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</li></ul> |Sim |
| description |Texto que descreve quais atividade hello ou pipeline é usado para | Não |
| atividades | Contém uma lista de atividades. | Sim |
| iniciar |Data-hora de início para o pipeline de saudação. Deve estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por exemplo: 2014-10-14T16:32:41. <br/><br/>É possível toospecify a hora local, por exemplo um tempo estimado. Aqui está um exemplo: `2016-02-27T06:00:00**-05:00`, que é 6 AM EST.<br/><br/>Hello propriedades de início e término juntas especificam o período ativo para o pipeline de saudação. Fatias de saída são produzidas somente nesse período ativo. |Não<br/><br/>Se você especificar um valor para a propriedade end hello, você deve especificar o valor para a propriedade de início de saudação.<br/><br/>Olá horários de início e término podem ser vazio toocreate um pipeline. Você deve especificar os dois valores tooset um período ativo para Olá toorun de pipeline. Se você não especificar horários de início e término durante a criação de um pipeline, você pode defini-las usando o cmdlet Olá AzureRmDataFactoryPipelineActivePeriod conjunto mais tarde. |
| end |Data-hora de término para o pipeline de saudação. Se especificado, deve estar no formato ISO. Por exemplo: 2014-10-14T17:32:41. <br/><br/>É possível toospecify a hora local, por exemplo um tempo estimado. Aqui está um exemplo: `2016-02-27T06:00:00**-05:00`, que é 6 AM EST.<br/><br/>pipeline de saudação toorun indefinidamente, especificar 9999-09-09 como valor de saudação para a propriedade end hello. |Não <br/><br/>Se você especificar um valor para a propriedade de início Olá, você deve especificar o valor para a propriedade end hello.<br/><br/>Consulte as observações para Olá **iniciar** propriedade. |
| isPaused |Se o conjunto tootrue Olá pipeline não é executado. Valor padrão = falso. Você pode usar essa propriedade tooenable ou desabilitar. |Não |
| pipelineMode |método Hello para o agendamento é executado para o pipeline de saudação. Os valores permitidos são: scheduled (padrão), onetime.<br/><br/>'Agendado' indica que esse pipeline Olá é executado em um intervalo de tempo especificado de acordo com o período ativo de tooits (hora de início e de término). 'Única' indica que esse pipeline Olá é executado apenas uma vez. Pipelines Onetime não podem ser modificados e atualizados depois de criados atualmente. Confira [Pipeline avulso](data-factory-create-pipelines.md#onetime-pipeline) para obter detalhes sobre a configuração única. |Não |
| expirationTime |Duração de tempo após a criação para o qual Olá pipeline é válido e deve permanecer provisionado. Se ele não tem qualquer ativo, falha, ou pendente é executado, o pipeline de saudação será excluído automaticamente depois que ele atinge o tempo de expiração de saudação. |Não |


## <a name="activity"></a>Atividade 
estrutura de alto nível Olá para uma atividade dentro de uma definição de pipeline (elemento de atividades) é o seguinte:

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

Tabela a seguir descrevem as propriedades de hello atividade Olá definição JSON:

| Marca | Descrição | Obrigatório |
| --- | --- | --- |
| name |Nome da atividade de saudação. Especifique um nome que representa a ação de hello atividade Olá configurado toodo<br/><ul><li>Número máximo de caracteres: 260</li><li>Deve começar com uma letra, um número ou um sublinhado (_)</li><li>Os seguintes caracteres não são permitidos: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</li></ul> |Sim |
| description |Texto que descreve quais hello atividade é usada. |Sim |
| type |Especifica o tipo de saudação da atividade de saudação. Consulte Olá [REPOSITÓRIOS de dados](#data-stores) e [atividades de TRANSFORMAÇÃO de dados](#data-transformation-activities) seções para diferentes tipos de atividades. |Sim |
| inputs |Tabelas de entrada usadas pela atividade Olá<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Sim |
| outputs |Tabelas de saída usadas pela atividade de saudação.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |Sim |
| linkedServiceName |Nome do serviço de saudação vinculado usado pela atividade de saudação. <br/><br/>Uma atividade pode exigir que você especifique que o serviço Olá vinculado que vincula o ambiente de computação necessária toohello. |Sim para atividades de HDInsight, atividades de Azure Machine Learning e Atividade de Procedimento Armazenado. <br/><br/>Não para todas as outros |
| typeProperties |Propriedades na seção de typeProperties Olá dependem do tipo de atividade de saudação. |Não |
| policy |Diretivas que afetam o comportamento de tempo de execução de saudação da atividade de saudação. Se não for especificado, as políticas padrão serão utilizadas. |Não |
| agendador |propriedade "Agendador" é usado toodefine desejado de agendamento para a atividade de saudação. Seus subpropriedades são Olá mesmo Olá na Olá [propriedade de disponibilidade em um conjunto de dados](data-factory-create-datasets.md#dataset-availability). |Não |

### <a name="policies"></a>Políticas
Políticas afetam o comportamento de tempo de execução de saudação de uma atividade, especialmente quando Olá fatia de uma tabela é processada. Olá, a tabela a seguir fornece detalhes de saudação.

| Propriedade | Valores permitidos | Valor Padrão | Descrição |
| --- | --- | --- | --- |
| simultaneidade |Inteiro  <br/><br/>Valor máximo: 10 |1 |Número de execuções concorrentes da atividade de saudação.<br/><br/>Ele determina o número de saudação de execuções de atividade paralela que pode ocorrer em intervalos diferentes. Por exemplo, se precisar de uma atividade toogo por meio de um grande conjunto de dados disponíveis, ter um valor maior da simultaneidade acelera o processamento de dados de saudação. |
| executionPriorityOrder |NewestFirst<br/><br/>OldestFirst |OldestFirst |Determina a saudação ordenação de fatias de dados que estão sendo processadas.<br/><br/>Por exemplo, se houver duas fatias (uma ocorre às 16h e a outra às 17h),e ambas estiverem com a execução pendente. Se você definir Olá executionPriorityOrder toobe NewestFirst, a fatia Olá às 17H é processada primeiro. Da mesma forma se você definir Olá executionPriorityORder toobe OldestFIrst, em seguida, Olá fatia às 16: 00 é processada. |
| tentar novamente |Número inteiro<br/><br/>O valor máximo pode ser 10 |0 |Número de tentativas antes do processamento de dados de saudação de fatia Olá é marcado como falha. A execução da atividade para uma fatia de dados é repetida backup toohello especificado contagem de repetição. repetição de saudação é feita logo após a falha de saudação. |
| Tempo limite |TimeSpan |00:00:00 |Tempo limite para a atividade de saudação. Exemplo: 00:10:00 (implica o tempo limite de 10 minutos)<br/><br/>Se um valor não for especificado ou for 0, o tempo limite de saudação é infinito.<br/><br/>Se o tempo de processamento de dados de saudação em uma fatia exceder o valor de tempo limite de Olá, é cancelada e sistema Olá tentativas de processamento de saudação tooretry. o número de tentativas Olá depende da propriedade de repetição de saudação. Quando o tempo limite ocorre, o status de saudação é definido tooTimedOut. |
| atrasar |TimeSpan |00:00:00 |Especifique o intervalo de saudação antes do processamento de dados de saudação fatia começar.<br/><br/>execução de saudação da atividade de uma fatia de dados é iniciada depois Olá atraso é passado Olá esperado tempo de execução.<br/><br/>Exemplo: 00:10:00 (implica um atraso de 10 minutos) |
| longRetry |Inteiro <br/><br/>Valor máximo: 10 |1 |número de saudação de repetição longa tentativas antes da execução da fatia Olá falhou.<br/><br/>Tentativas de longRetry são espaçadas por longRetryInterval. Portanto, se você precisar toospecify um tempo entre tentativas de repetição, use longRetry. Se Retry e longRetry forem especificados, cada tentativa de longRetry inclui novas tentativas e Olá o número máximo de tentativas é repetir * longRetry.<br/><br/>Por exemplo, se tivermos Olá configurações na política de atividade Olá a seguir:<br/>Retry: 3<br/>longRetry: 2<br/>longRetryInterval: 01:00:00<br/><br/>Pressupomos que haja apenas um tooexecute de fatia (status está esperando) e a execução da atividade Olá falha sempre. Inicialmente haveria três tentativas consecutivas de execução. Após cada tentativa, o status da fatia Olá deve ser Retry. Depois de tentativas primeiro 3 estão acima, o status da fatia Olá deve ser LongRetry.<br/><br/>Depois de uma hora (ou seja, valor de longRetryInteval), deve haver outro conjunto de três tentativas consecutivas de execução. Depois disso, o status da fatia Olá deve ser Failed e nenhuma outra tentativa será feita. Portanto, em geral, foram feitas seis tentativas.<br/><br/>Se qualquer execução for bem-sucedida, o status da fatia Olá seria pronto e não tentativa de nenhuma outra tentativa.<br/><br/>longRetry pode ser usado em situações em que dados dependentes chegam em momentos não determinística ou hello ambiente geral é instável em ocorre o processamento de dados. Nesses casos, não pode ajudar a fazer tentativas após o outro e fazer isso após um intervalo de resultados de tempo de saudação desejado de saída.<br/><br/>Advertência: não defina valores altos para longRetry ou longRetryInterval. Normalmente, os valores mais altos implicam outros problemas sistêmicos. |
| longRetryInterval |TimeSpan |00:00:00 |atraso de saudação entre as tentativas de repetição longa |

### <a name="typeproperties-section"></a>Seção typeProperties
seção de typeProperties Olá é diferente para cada atividade. Atividades de transformação tem apenas as propriedades de tipo hello. Consulte [ATIVIDADES DE TRANSFORMAÇÃO DE DADOS](#data-transformation-activities) neste artigo para obter exemplos de JSON que definem atividades de transformação em um pipeline. 

**Atividade de cópia** tem duas subseções na seção de typeProperties Olá: **fonte** e **coletor**. Consulte [REPOSITÓRIOS de dados](#data-stores) seção neste artigo para JSON exemplos que mostram como toouse um dados armazenados como uma origem e/ou o coletor. 

### <a name="sample-copy-pipeline"></a>Pipeline de cópia de exemplo
Olá pipeline de exemplo a seguir, há uma atividade do tipo **cópia** em Olá **atividades** seção. Neste exemplo, Olá [atividade de cópia](data-factory-data-movement-activities.md) copia dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure. 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Observe Olá pontos a seguir:

* Na seção de atividades hello, há apenas uma atividade cuja **tipo** está definido muito**cópia**.
* Entrada para atividade de saudação é definida muito**InputDataset** e de saída para o conjunto de hello atividade é muito**OutputDataset**.
* Em Olá **typeProperties** seção, **BlobSource** é especificado como tipo de fonte hello e **SqlSink** é especificado como tipo de coletor de saudação.

Consulte [REPOSITÓRIOS de dados](#data-stores) seção neste artigo para JSON exemplos que mostram como toouse um dados armazenados como uma origem e/ou o coletor.    

Para obter uma explicação completa de criar esse pipeline, consulte [Tutorial: copiar dados de armazenamento de Blob tooSQL banco de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="sample-transformation-pipeline"></a>Pipeline de transformação de exemplo
Olá pipeline de exemplo a seguir, há uma atividade do tipo **HDInsightHive** em Olá **atividades** seção. Neste exemplo, Olá [atividade Hive do HDInsight](data-factory-hive-activity.md) transforma os dados de um armazenamento de BLOBs do Azure executando um arquivo de script do Hive em um cluster de Hadoop de HDInsight do Azure. 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

Observe Olá pontos a seguir: 

* Na seção de atividades hello, há apenas uma atividade cuja **tipo** está definido muito**HDInsightHive**.
* arquivo de script do Hive Hello, **partitionweblogs.hql**, é armazenado no hello conta de armazenamento do Azure (especificado por scriptLinkedService hello, chamado **AzureStorageLinkedService**) e em  **script** pasta no contêiner Olá **adfgetstarted**.
* Olá **define** seção é toospecify usadas configurações de tempo de execução de saudação que são passadas script do hive toohello como valores de configuração do Hive (por exemplo `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Consulte [ATIVIDADES DE TRANSFORMAÇÃO DE DADOS](#data-transformation-activities) neste artigo para obter exemplos de JSON que definem atividades de transformação em um pipeline.

Para obter uma explicação completa de criar esse pipeline, consulte [Tutorial: Crie sua primeira pipeline tooprocess de dados usando o cluster Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="linked-service"></a>Serviço vinculado
estrutura de alto nível Olá para uma definição de serviço vinculado é o seguinte:

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

Tabela a seguir descrevem as propriedades de hello atividade Olá definição JSON:

| Propriedade | Descrição | Obrigatório |
| -------- | ----------- | -------- | 
| name | Nome do serviço de saudação vinculado. | Sim | 
| properties - type | Serviço vinculado do tipo de saudação. Por exemplo: Armazenamento do Azure, Banco de Dados SQL do Azure. |
| typeProperties | seção de typeProperties Olá tem elementos que são diferentes para cada repositório de dados ou ambiente de computação. Consulte [repositórios de dados](#datastores) seção de todos os dados de saudação serviços vinculados da loja e [ambientes de computação](#compute-environments) para Olá todos os serviços vinculados de computação |   

## <a name="dataset"></a>Conjunto de dados 
Um conjunto de dados no Azure Data Factory é definido da seguinte maneira:

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
| name | Nome do conjunto de dados de saudação. Confira [Azure Data Factory - Regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura. |Sim |ND |
| type | Tipo de conjunto de dados de saudação. Especifique um dos tipos de saudação com suporte pela fábrica de dados do Azure (por exemplo: AzureBlob, AzureSqlTable). Consulte [REPOSITÓRIOS de dados](#data-stores) seção Olá a todos os repositórios de dados e tipos de conjunto de dados com suporte pela fábrica de dados. | 
| estrutura | Esquema de conjunto de dados de saudação. Ela contém colunas, seus tipos, etc. | Não |ND |
| typeProperties | Propriedades correspondentes toohello tipo selecionado. Consulte a seção [ARMAZENAMENTOS DE DADOS](#data-stores) para saber quais são os tipos com suporte e suas propriedades. |Sim |ND |
| externo | Booliano sinalizador toospecify se um conjunto de dados explicitamente produzido por um pipeline da fábrica de dados ou não. |Não |false |
| disponibilidade | Define Olá processamento Olá dividindo o modelo para conjunto de dados de produção de hello ou janela. Para obter detalhes sobre o dataset Olá dividindo o modelo, consulte [de agendamento e execução](data-factory-scheduling-and-execution.md) artigo. |Sim |ND |
| policy |Define os critérios de saudação ou condição Olá que devem ser atendidos por fatias de conjunto de dados de saudação. <br/><br/>Para obter detalhes, consulte a seção [Política do Conjunto de Dados](#Policy) . |Não |ND |

Cada coluna no hello **estrutura** seção contém Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| name |Nome da coluna de saudação. |Sim |
| type |Tipo de dados da coluna de saudação.  |Não |
| culture |.NET com base em cultura toobe usado quando o tipo é especificado e é o tipo .NET `Datetime` ou `Datetimeoffset`. O padrão é `en-us`. |Não |
| formato |Formatar toobe de cadeia de caracteres usada quando o tipo é especificado e é o tipo .NET `Datetime` ou `Datetimeoffset`. |Não |

Olá exemplo a seguir, Olá dataset tem três colunas `slicetimestamp`, `projectname`, e `pageviews` e eles são do tipo: cadeia de caracteres, cadeia de caracteres e decimais respectivamente.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Olá tabela a seguir descreve as propriedades você pode usar em Olá **disponibilidade** seção:

| Propriedade | Descrição | Obrigatório | Padrão |
| --- | --- | --- | --- |
| frequência |Especifica a unidade de tempo de saudação de produção de fatia do conjunto de dados.<br/><br/><b>Frequência com suporte</b>: Minuto, Hora, Dia, Semana, Mês |Sim |ND |
| intervalo |Especifica um multiplicador para frequência<br/><br/>"Intervalo de frequência x" determina com que frequência hello fatia é produzida.<br/><br/>Se você precisar hello toobe de conjunto de dados dividido por hora, defina <b>frequência</b> muito<b>hora</b>, e <b>intervalo</b> muito<b>1</b>.<br/><br/><b>Observação</b>: se você especificar a frequência como minuto, recomendamos que você defina Olá intervalo toono menor que 15 |Sim |ND |
| estilo |Especifica se a fatia Olá deve ser produzida no hello início/término do intervalo de saudação.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Quando frequência é definida tooMonth e o estilo definido tooEndOfInterval, fatia de saudação é produzida no último dia do mês de saudação. Se o estilo de saudação é definido tooStartOfInterval, Olá fatia é produzida no hello primeiro dia do mês.<br/><br/>Quando frequência é definida tooDay e o estilo definido tooEndOfInterval, fatia de Olá é produzida no hello última hora do dia de saudação.<br/><br/>Quando frequência é definida tooHour e o estilo definido tooEndOfInterval, fatia de Olá é produzida no final de saudação de hora hello. Por exemplo, para uma fatia de período de 1 PM – 14: 00, a fatia de saudação é produzida às 14: 00. |Não |EndOfInterval |
| anchorDateTime |Define a posição absoluta Olá no tempo usado pelos limites de fatia do Agendador toocompute conjunto de dados. <br/><br/><b>Observação</b>: se Olá AnchorDateTime tem partes de data mais granulares do que a frequência de hello, hello partes mais granulares são ignoradas. <br/><br/>Por exemplo, se hello <b>intervalo</b> é <b>por hora</b> (frequência: hora e intervalo: 1) e hello <b>AnchorDateTime</b> contém <b>minutos e segundos</b>, em seguida, Olá <b>minutos e segundos</b> partes da saudação AnchorDateTime são ignoradas. |Não |01/01/0001 |
| deslocamento |O intervalo de tempo pelo qual saudação inicial e final de todas as fatias de conjunto de dados são transferidos. <br/><br/><b>Observação</b>: se anchorDateTime e o deslocamento forem especificados, o resultado de saudação é shift Olá combinado. |Não |ND |

Olá seção de disponibilidade a seguir especifica esse conjunto de dados de saída de saudação é produzido por hora (ou) entrada conjunto de dados está disponível por hora:

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Olá **política** seção na definição de conjunto de dados define os critérios de saudação ou condição Olá Olá fatias de conjunto de dados deve ser atendidos.

| Nome da política | Descrição | Aplicado muito| Obrigatório | Padrão |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Valida que dados Olá em um **BLOBs do Azure** Olá de atende aos requisitos de tamanho mínimo (em megabytes). |Blob do Azure |Não |ND |
| minimumRows |Valida que dados Olá em um **banco de dados do SQL Azure** ou um **tabela do Azure** contém o número mínimo de saudação de linhas. |<ul><li>Banco de Dados SQL do Azure</li><li>tabela do Azure</li></ul> |Não |ND |

**Exemplo:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

A menos que um conjunto de dados seja produzido pela Azure Data Factory, ele deverá ser marcado como **externo**. Essa configuração geralmente se aplica a toohello entradas da primeira atividade em um pipeline, a menos que uma atividade ou o encadeamento de pipeline está sendo usado.

| Nome | Descrição | Obrigatório | Valor Padrão |
| --- | --- | --- | --- |
| dataDelay |Seleção de saudação toodelay tempo na disponibilidade de saudação de dados externa Olá Olá considerando a fatia. Por exemplo, se dados saudação estão disponíveis por hora, dados externos do Olá Olá seleção toosee estão disponíveis e fatia correspondente hello está pronto pode ser atrasado usando dataDelay.<br/><br/>Aplica-se somente toohello a hora atual.  Por exemplo, se for 1:00 PM agora e esse valor é 10 minutos, validação Olá inicia às 13:10.<br/><br/>Essa configuração não afeta fatias Olá passado (fatias com hora de término da fatia + dataDelay < agora) são processados sem atraso.<br/><br/>Tempo maior que 23:59 horas necessário toospecified usando Olá `day.hours:minutes:seconds` formato. Por exemplo, toospecify 24 horas, não use 24:00:00; em vez disso, use 1.00:00:00. Se você usar 24:00:00, isso será tratado como 24 dias (24.00:00:00). Para 1 dia e 4 horas, especifique 1:04:00:00. |Não |0 |
| retryInterval |tempo de espera de saudação entre uma falha e hello próxima tentativa. Se uma tentativa falhar, a próxima tentativa de saudação é após retryInterval. <br/><br/>Se for 1:00 PM agora, começamos Olá primeira tentativa. Se Olá duração toocomplete Olá primeira verificação de validação é 1 minuto e Falha na operação de hello, Olá próxima tentativa é às 1:00 + 1 min (duração) + 1min (intervalo de repetição) = 1:02 PM. <br/><br/>Para fatias Olá anterior, não há nenhum atraso. repetição de saudação ocorre imediatamente. |Não |00:01:00 (1 minuto) |
| retryTimeout |Olá tempo limite para cada tentativa de repetição.<br/><br/>Se essa propriedade for definida too10 minutos, Olá toobe de necessidades de validação concluída em 10 minutos. Se demorar mais de validação de saudação do tooperform de 10 minutos, Olá novamente o tempo limite.<br/><br/>Se todas as tentativas de validação de saudação expira, fatia hello está marcada como TimedOut. |Não |00:10:00 (10 minutos) |
| maximumRetry |Número de vezes toocheck para disponibilidade de saudação de dados externos de saudação. Olá permitido valor máximo é 10. |Não |3 |


## <a name="data-stores"></a>ARMAZENAMENTOS DE DADOS
Olá [serviço vinculado](#linked-service) descrições de seção fornecida para elementos JSON que são tipos comuns de tooall de serviços vinculados. Esta seção fornece detalhes sobre os elementos JSON que são específicos tooeach repositório de dados.

Olá [Dataset](#dataset) descrições de seção fornecida para elementos JSON que são tipos comuns de tooall de conjuntos de dados. Esta seção fornece detalhes sobre os elementos JSON que são específicos tooeach repositório de dados.

Olá [atividade](#activity) descrições de seção fornecida para elementos JSON que são tipos de tooall comuns de atividades. Esta seção fornece detalhes sobre os elementos JSON que são específicos tooeach repositório de dados quando ele é usado como um fonte/coletor em uma atividade de cópia.  

Clique Olá link armazenamento Olá você está interessado em esquemas JSON toosee Olá para o serviço vinculado, o conjunto de dados e Olá fonte/coletor de atividade de cópia de saudação.

| Categoria | Armazenamento de dados 
|:--- |:--- |
| **As tabelas** |[Armazenamento de Blobs do Azure](#azure-blob-storage) |
| &nbsp; |[Repositório Azure Data Lake](#azure-datalake-store) |
| &nbsp; |[Azure Cosmos DB](#azure-cosmos-db) |
| &nbsp; |[Banco de Dados SQL do Azure](#azure-sql-database) |
| &nbsp; |[SQL Data Warehouse do Azure](#azure-sql-data-warehouse) |
| &nbsp; |[Pesquisa do Azure](#azure-search) |
| &nbsp; |[Armazenamento de Tabelas do Azure](#azure-table-storage) |
| **Bancos de dados** |[Amazon Redshift](#amazon-redshift) |
| &nbsp; |[IBM DB2](#ibm-db2) |
| &nbsp; |[MySQL](#mysql) |
| &nbsp; |[Oracle](#oracle) |
| &nbsp; |[PostgreSQL](#postgresql) |
| &nbsp; |[SAP Business Warehouse](#sap-business-warehouse) |
| &nbsp; |[SAP HANA](#sap-hana) |
| &nbsp; |[SQL Server](#sql-server) |
| &nbsp; |[Sybase](#sybase) |
| &nbsp; |[Teradata](#teradata) |
| **NoSQL** |[Cassandra](#cassandra) |
| &nbsp; |[MongoDB](#mongodb) |
| **Arquivo** |[Amazon S3](#amazon-s3) |
| &nbsp; |[Sistema de Arquivos](#file-system) |
| &nbsp; |[FTP](#ftp) |
| &nbsp; |[HDFS](#hdfs) |
| &nbsp; |[SFTP](#sftp) |
| **Outros** |[HTTP](#http) |
| &nbsp; |[OData](#odata) |
| &nbsp; |[ODBC](#odbc) |
| &nbsp; |[Salesforce](#salesforce) |
| &nbsp; |[Tabela da Web](#web-table) |

## <a name="azure-blob-storage"></a>Armazenamento do Blobs do Azure

### <a name="linked-service"></a>Serviço vinculado
Há dois tipos de serviços vinculados: serviço vinculado do Armazenamento do Azure e serviço vinculado do Armazenamento do Azure SAS.

#### <a name="azure-storage-linked-service"></a>Serviço vinculado de armazenamento do Azure
toolink sua fábrica de dados de tooa da conta de armazenamento do Azure usando Olá **chave de conta**, crie um serviço vinculado do armazenamento do Azure. toodefine um armazenamento do Azure vinculada serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AzureStorage**. Em seguida, você pode especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| connectionString |Especifique informações necessárias tooconnect tooAzure armazenamento para a propriedade connectionString de saudação. |Sim |

##### <a name="example"></a>Exemplo  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a>Serviço vinculado de SAS de Armazenamento do Azure
Olá SAS de armazenamento do Azure vinculada serviço permite que você toolink uma conta de armazenamento do Azure tooan data factory do Azure usando uma assinatura de acesso compartilhado (SAS). Ele fornece fábrica de dados Olá com acesso restrito/limite de tempo específicos/tooall recursos (blob/contêiner) no armazenamento de saudação. toolink sua fábrica de dados de tooa da conta de armazenamento do Azure usando a assinatura de acesso compartilhado, crie um serviço de SAS do armazenamento do Azure vinculado. toodefine um SAS de armazenamento do Azure vinculada serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**o AzureStorageSas**. Em seguida, você pode especificar propriedades no Olá a seguir **typeProperties** seção:   

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| sasUri |Especifica os recursos de armazenamento do Azure do URI de assinatura de acesso compartilhado toohello como blob, contêiner ou tabela. |Sim |

##### <a name="example"></a>Exemplo

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Para obter mais informações sobre esses serviços vinculados, consulte o artigo [Conector de Armazenamento de Blobs do Azure](data-factory-azure-blob-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados de Blob do Azure, Olá conjunto **tipo** do conjunto de dados de saudação muito**AzureBlob**. Em seguida, especifique Olá seguintes propriedades específicas de BLOBs do Azure no hello **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| folderPath |Contêiner de toohello do caminho e a pasta no armazenamento de blob hello. Exemplo: myblobcontainer\myblobfolder\ |Sim |
| fileName |Nome do blob hello. fileName é opcional e diferencia maiúsculas de minúsculas.<br/><br/>Se você especificar um nome de arquivo, hello atividade (incluindo cópia) funciona em Olá Blob específico.<br/><br/>Quando o nome de arquivo não for especificado, cópia inclui todos os Blobs no folderPath Olá para o conjunto de dados de entrada.<br/><br/>Quando o nome de arquivo não for especificado para um conjunto de dados de saída, nome de saudação do arquivo hello gerado seria em Olá seguindo este formato: dados. <Guid>. txt (por exemplo:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Não |
| partitionedBy |partitionedBy é uma propriedade opcional. Você pode usar-ele toospecify um dinâmico folderPath e filename para dados de série temporal. Por exemplo, folderPath pode ser parametrizado para cada hora dos dados. |Não |
| formato | Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Saudação de conjunto **tipo** propriedade em formato tooone desses valores. Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída. |Não |
| compactação | Especifica tipo de saudação e nível de compactação de dados de saudação. Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. Os níveis com suporte são **Ideal** e **O mais rápido**. Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory). |Não |

#### <a name="example"></a>Exemplo

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


Para obter mais informações, consulte o artigo [Conector de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties).

### <a name="blobsource-in-copy-activity"></a>BlobSource na Atividade de Cópia
Se você estiver copiando dados de um armazenamento de BLOBs do Azure, defina Olá **tipo de fonte** de hello atividade de cópia muito**BlobSource**e especificar propriedades no Olá a seguir * * fonte * * seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| recursiva |Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello. |True (valor padrão), False |Não |

#### <a name="example-blobsource"></a>Exemplo: BlobSource**
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a>BlobSink na Atividade de Cópia
Se você estiver copiando dados tooan armazenamento de BLOBs do Azure, defina Olá **tipo de coletor** de hello atividade de cópia muito**BlobSink**e especificar propriedades no Olá a seguir **coletor** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| copyBehavior |Define o comportamento de cópia de saudação quando origem Olá é BlobSource ou sistema de arquivos. |<b>PreserveHierarchy</b>: preserva Olá hierarquia de arquivos na pasta de destino de saudação. caminho relativo do Hello arquivo toosource da pasta de origem é idêntico toohello o caminho relativo da pasta de tootarget do arquivo de destino.<br/><br/><b>FlattenHierarchy</b>: todos os arquivos da pasta de origem Olá estão em Olá primeiro níveis da pasta de destino. os arquivos de destino de saudação têm nome gerado automaticamente. <br/><br/><b>MergeFiles (padrão):</b> mescla todos os arquivos Olá pasta tooone do arquivo de origem. Se Olá nome de arquivo/Blob for especificado, o nome de arquivo mesclado de Olá seria nome especificado do hello. Caso contrário, seriam nome de arquivo gerado automaticamente. |Não |

#### <a name="example-blobsink"></a>Exemplo: BlobSink

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para obter mais informações, consulte o artigo [Conector de Blob do Azure](data-factory-azure-blob-connector.md#copy-activity-properties). 

## <a name="azure-data-lake-store"></a>Repositório Azure Data Lake

### <a name="linked-service"></a>Serviço vinculado
toodefine um serviço de repositório Azure Data Lake vinculado, tipo de saudação do conjunto de saudação serviço vinculado muito**AzureDataLakeStore**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| type | propriedade de tipo Hello deve ser definida como: **AzureDataLakeStore** | Sim |
| dataLakeStoreUri | Especifique informações sobre Olá conta do repositório Azure Data Lake. É no hello formato a seguir: `https://[accountname].azuredatalakestore.net/webhdfs/v1` ou `adl://[accountname].azuredatalakestore.net/`. | Sim |
| subscriptionId | Assinatura do Azure Id toowhich repositório Data Lake pertence. | Obrigatório para coletor |
| resourceGroupName | Toowhich de nome de grupo de recursos do Azure repositório Data Lake pertence. | Obrigatório para coletor |
| servicePrincipalId | Especifique a ID do cliente. do aplicativo hello | Sim (para autenticação de entidade de serviço) |
| servicePrincipalKey | Especifique a chave de aplicativo hello. | Sim (para autenticação de entidade de serviço) |
| locatário | Especifique as informações de locatário hello (ID de locatário ou de nome de domínio) em que o aplicativo reside. Você pode recuperá-la por focalização mouse Olá no canto superior direito Olá Olá portal do Azure. | Sim (para autenticação de entidade de serviço) |
| autorização | Clique em **autorizar** botão Olá **Editor da fábrica de dados** e insira suas credenciais que atribui a propriedade de toothis de URL Olá autorização gerado automaticamente. | Sim (para autenticação de credenciais de usuário)|
| sessionId | Id de sessão do OAuth da sessão de autorização de OAuth hello. Cada ID da sessão é exclusiva e pode ser usado somente uma vez. Essa configuração é gerada automaticamente quando você usa o Editor do Data Factory. | Sim (para autenticação de credenciais de usuário) |

#### <a name="example-using-service-principal-authentication"></a>Exemplo: usando a autenticação da entidade de serviço
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a>Exemplo: usando a autenticação de credenciais de usuário
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

Para saber mais, consulte o artigo [Conector do Azure Data Lake Store](data-factory-azure-datalake-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados do repositório Azure Data Lake conjunto Olá **tipo** do conjunto de dados de saudação muito**AzureDataLakeStore**e especifique Olá seguintes propriedades em Olá **typeProperties**seção: 

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| folderPath |Contêiner de toohello do caminho e a pasta em hello Azure Data Lake armazenam. |Sim |
| fileName |Nome do arquivo hello no armazenamento do Azure Data Lake hello. fileName é opcional e diferencia maiúsculas de minúsculas. <br/><br/>Se você especificar um nome de arquivo, atividade de saudação (incluindo cópia) funciona em arquivos específicos da saudação.<br/><br/>Quando o nome de arquivo não for especificado, a cópia inclui todos os arquivos no folderPath Olá para o conjunto de dados de entrada.<br/><br/>Quando o nome de arquivo não for especificado para um conjunto de dados de saída, nome de saudação do arquivo hello gerado seria em Olá seguindo este formato: dados. <Guid>. txt (por exemplo:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Não |
| partitionedBy |partitionedBy é uma propriedade opcional. Você pode usar-ele toospecify um dinâmico folderPath e filename para dados de série temporal. Por exemplo, folderPath pode ser parametrizado para cada hora dos dados. |Não |
| formato | Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Saudação de conjunto **tipo** propriedade em formato tooone desses valores. Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída. |Não |
| compactação | Especifica tipo de saudação e nível de compactação de dados de saudação. Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. Os níveis com suporte são **Ideal** e **O mais rápido**. Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory). |Não |

#### <a name="example"></a>Exemplo
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Para saber mais, consulte o artigo [Conector do Azure Data Lake Store](data-factory-azure-datalake-connector.md#dataset-properties). 

### <a name="azure-data-lake-store-source-in-copy-activity"></a>Fonte do Azure Data Lake Store na Atividade de Cópia
Se você estiver copiando dados de um repositório Azure Data Lake, defina Olá **tipo de fonte** de hello atividade de cópia muito**AzureDataLakeStoreSource**e especificar propriedades no Olá a seguir **fonte**  seção:

**AzureDataLakeStoreSource** dá suporte a saudação seguintes propriedades **typeProperties** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| recursiva |Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello. |True (valor padrão), False |Não |

#### <a name="example-azuredatalakestoresource"></a>Exemplo: AzureDataLakeStoreSource

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para saber mais, consulte o artigo [Conector do Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).

### <a name="azure-data-lake-store-sink-in-copy-activity"></a>Coletor do Azure Data Lake Store na Atividade de Cópia
Se você estiver copiando o repositório de dados tooan Azure Data Lake, defina Olá **tipo de coletor** de hello atividade de cópia muito**AzureDataLakeStoreSink**e especificar propriedades no Olá a seguir **coletor**seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| copyBehavior |Especifica o comportamento de cópia de saudação. |<b>PreserveHierarchy</b>: preserva Olá hierarquia de arquivos na pasta de destino de saudação. caminho relativo do Hello arquivo toosource da pasta de origem é idêntico toohello o caminho relativo da pasta de tootarget do arquivo de destino.<br/><br/><b>FlattenHierarchy</b>: todos os arquivos da pasta de origem Olá são criados no primeiro nível saudação da pasta de destino. arquivos de destino de saudação são criados com o nome gerado automaticamente.<br/><br/><b>MergeFiles</b>: mescla todos os arquivos Olá pasta tooone do arquivo de origem. Se Olá nome de arquivo/Blob for especificado, o nome de arquivo mesclado de Olá seria nome especificado do hello. Caso contrário, seriam nome de arquivo gerado automaticamente. |Não |

#### <a name="example-azuredatalakestoresink"></a>Exemplo: AzureDataLakeStoreSink
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para saber mais, consulte o artigo [Conector do Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties). 

## <a name="azure-cosmos-db"></a>Azure Cosmos DB  

### <a name="linked-service"></a>Serviço vinculado
toodefine um banco de dados do Azure Cosmos o serviço saudação do conjunto vinculado **tipo** de saudação serviço vinculado muito**DocumentDb**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| **Propriedade** | **Descrição** | **Obrigatório** |
| --- | --- | --- |
| connectionString |Especifique o banco de dados do banco de dados do Cosmos tooconnect tooAzure as informações necessárias. |Sim |

#### <a name="example"></a>Exemplo

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
Para obter mais informações, consulte o artigo [Conector do Azure Cosmos DB](data-factory-azure-documentdb-connector.md#linked-service-properties).

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados do banco de dados do Azure Cosmos conjunto Olá **tipo** do conjunto de dados de saudação muito**DocumentDbCollection**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| **Propriedade** | **Descrição** | **Obrigatório** |
| --- | --- | --- |
| collectionName |Nome do hello Azure Cosmos DB coleção. |Sim |

#### <a name="example"></a>Exemplo

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
Para obter mais informações, consulte o artigo [Conector do Azure Cosmos DB](data-factory-azure-documentdb-connector.md#dataset-properties).

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a>Fonte de coleta do Azure Cosmos DB na Atividade de Cópia
Se você estiver copiando dados de um banco de dados do Azure Cosmos, defina Olá **tipo de fonte** de hello atividade de cópia muito**DocumentDbCollectionSource**e especificar propriedades no Olá a seguir **fonte** seção:


| **Propriedade** | **Descrição** | **Valores permitidos** | **Obrigatório** |
| --- | --- | --- | --- |
| query |Especifica Olá consulta tooread dados. |Cadeia de consulta com suporte no Azure Cosmos DB. <br/><br/>Exemplo: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |Não <br/><br/>Se não for especificado, Olá instrução SQL executada:`select <columns defined in structure> from mycollection` |
| nestingSeparator |Caractere especial tooindicate que Olá documento está aninhado |Qualquer caractere. <br/><br/>O Azure Cosmos DB é um repositório NoSQL para documentos JSON, em que estruturas aninhadas são permitidas. A fábrica de dados do Azure permite que a hierarquia de toodenote de usuário por meio de nestingSeparator, que é "." em hello acima exemplos. Separador hello, atividade de cópia Olá irá gerar objeto de "Nome" hello com elementos de três filhos too"Name.First primeiro, intermediária e último, acordo", "Name.Middle" e ". Sobrenome" hello definição da tabela. |Não |

#### <a name="example"></a>Exemplo

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a>Coletor para coleta do Azure Cosmos DB na Atividade de Cópia
Se você estiver copiando dados tooAzure Cosmos banco de dados, definir Olá **tipo de coletor** de hello atividade de cópia muito**DocumentDbCollectionSink**e especificar propriedades no Olá a seguir **coletor**seção:

| **Propriedade** | **Descrição** | **Valores permitidos** | **Obrigatório** |
| --- | --- | --- | --- |
| nestingSeparator |Um caractere especial em Olá fonte coluna Nome tooindicate que aninhada documento é necessário. <br/><br/>Por exemplo acima: `Name.First` na saída de hello tabela produz Olá estrutura JSON no documento de banco de dados do Cosmos Olá a seguir:<br/><br/>"Name": {<br/>    "First": "John"<br/>}, |Caractere usado tooseparate níveis de aninhamento.<br/><br/>O valor padrão é `.` (ponto). |Caractere usado tooseparate níveis de aninhamento. <br/><br/>O valor padrão é `.` (ponto). |
| writeBatchSize |Número de paralelo solicitações tooAzure documentos de toocreate do serviço de banco de dados do Cosmos.<br/><br/>Você pode ajustar o desempenho de saudação ao copiar dados de banco de dados do Azure Cosmos usando essa propriedade. Você pode esperar um desempenho melhor quando você aumenta writeBatchSize porque mais solicitações paralelas tooAzure Cosmos banco de dados são enviados. No entanto, você precisará tooavoid limitação que pode gerar a mensagem de saudação do erro: "Solicitação de taxa for grande".<br/><br/>A limitação é decida por uma série de fatores, incluindo o tamanho dos documentos, o número de termos incluídos, a política de indexação da coleção de destino, etc. Para operações de cópia, você pode usar uma saudação de toohave de coleção (por exemplo, S3) melhor taxa de transferência mais disponível (2.500 solicitação unidades/segundo). |Número inteiro |Não (padrão: 5) |
| writeBatchTimeout |Tempo de espera para Olá operação toocomplete antes de expirar. |timespan<br/><br/> Exemplo: "00:30:00" (30 minutos). |Não |

#### <a name="example"></a>Exemplo

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Azure Cosmos DB](data-factory-azure-documentdb-connector.md#copy-activity-properties).

## <a name="azure-sql-database"></a>Banco de Dados SQL do Azure

### <a name="linked-service"></a>Serviço vinculado
toodefine um banco de dados do SQL Azure vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AzureSqlDatabase**e especificar propriedades no Olá a seguir **typeProperties**seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| connectionString |Especifique informações necessárias a instância de banco de dados do Azure SQL toohello tooconnect para a propriedade connectionString de saudação. |Sim |

#### <a name="example"></a>Exemplo
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector de SQL do Azure](data-factory-azure-sql-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados do banco de dados SQL, Olá conjunto **tipo** do conjunto de dados de saudação muito**AzureSqlTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação ou exibição na instância de banco de dados do Azure SQL Olá que serviço vinculado refere-se a. |Sim |

#### <a name="example"></a>Exemplo

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Para obter mais informações, consulte o artigo [Conector de SQL do Azure](data-factory-azure-sql-connector.md#dataset-properties). 

### <a name="sql-source-in-copy-activity"></a>Origem do SQL na atividade de cópia
Se você estiver copiando dados de um banco de dados do SQL Azure, defina Olá **tipo de fonte** de hello atividade de cópia muito**SqlSource**e especificar propriedades no Olá a seguir **fonte** seção:


| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| SqlReaderQuery |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Exemplo: `select * from MyTable`. |Não |
| sqlReaderStoredProcedureName |Nome da saudação procedimento armazenado que lê dados da tabela de origem hello. |Nome da saudação de procedimento armazenado. |Não |
| storedProcedureParameters |Parâmetros de saudação de procedimento armazenado. |Pares de nome/valor. Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação. |Não |

#### <a name="example"></a>Exemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Para obter mais informações, consulte o artigo [Conector de SQL do Azure](data-factory-azure-sql-connector.md#copy-activity-properties). 

### <a name="sql-sink-in-copy-activity"></a>Coletor do SQL na Atividade de Cópia
Se você estiver copiando dados tooAzure banco de dados SQL, definir Olá **tipo de coletor** de hello atividade de cópia muito**SqlSink**e especificar propriedades no Olá a seguir **coletor** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| writeBatchTimeout |Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar. |timespan<br/><br/> Exemplo: "00:30:00" (30 minutos). |Não |
| writeBatchSize |Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize. |Inteiro (número de linhas) |Não (padrão: 10000) |
| sqlWriterCleanupScript |Especifique uma consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa. |Uma instrução de consulta. |Não |
| sliceIdentifierColumnName |Especifique um nome de coluna para a atividade de cópia toofill com identificador de fatia gerado automaticamente, que é usado tooclean os dados de uma fatia específica quando executada novamente. |Nome de uma coluna com tipo de dados de binário (32). |Não |
| sqlWriterStoredProcedureName |Nome do hello procedimento armazenado dados upserts (atualizações/inserções) na tabela de destino de saudação. |Nome da saudação de procedimento armazenado. |Não |
| storedProcedureParameters |Parâmetros de saudação de procedimento armazenado. |Pares de nome/valor. Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação. |Não |
| sqlWriterTableType |Especifique um toobe de nome de tipo de tabela usado no procedimento armazenado de saudação. Atividade de cópia disponibiliza dados Olá movidos em uma tabela temporária com esse tipo de tabela. Código do procedimento armazenado, em seguida, pode mesclar dados de saudação sejam copiados com os dados existentes. |Um nome de tipo de tabela. |Não |

#### <a name="example"></a>Exemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para obter mais informações, consulte o artigo [Conector de SQL do Azure](data-factory-azure-sql-connector.md#copy-activity-properties). 

## <a name="azure-sql-data-warehouse"></a>SQL Data Warehouse do Azure

### <a name="linked-service"></a>Serviço vinculado
toodefine um Azure SQL Data Warehouse vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AzureSqlDW**e especificar propriedades no Olá a seguir **typeProperties**seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| connectionString |Especifique informações necessárias a instância do tooconnect toohello Azure SQL Data Warehouse para a propriedade connectionString de saudação. |Sim |



#### <a name="example"></a>Exemplo

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados do Azure SQL Data Warehouse, Olá conjunto **tipo** do conjunto de dados de saudação muito**AzureSqlDWTable**e especifique Olá seguintes propriedades em Olá **typeProperties**seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação ou exibição no banco de dados de Data warehouse do SQL Azure de saudação que Olá serviço vinculado refere-se a. |Sim |

#### <a name="example"></a>Exemplo

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties). 

### <a name="sql-dw-source-in-copy-activity"></a>Origem do SQL DW na Atividade de Cópia
Se você estiver copiando dados de Data warehouse do SQL Azure, defina Olá **tipo de fonte** de hello atividade de cópia muito**SqlDWSource**e especificar propriedades no Olá a seguir **fonte**seção:


| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| SqlReaderQuery |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: `select * from MyTable`. |Não |
| sqlReaderStoredProcedureName |Nome da saudação procedimento armazenado que lê dados da tabela de origem hello. |Nome da saudação de procedimento armazenado. |Não |
| storedProcedureParameters |Parâmetros de saudação de procedimento armazenado. |Pares de nome/valor. Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação. |Não |

#### <a name="example"></a>Exemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para obter mais informações, consulte o artigo [Conector do SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties). 

### <a name="sql-dw-sink-in-copy-activity"></a>Coletor do SQL DW na Atividade de Cópia
Se você estiver copiando dados tooAzure SQL Data Warehouse, defina Olá **tipo de coletor** de hello atividade de cópia muito**SqlDWSink**e especificar propriedades no Olá a seguir **coletor** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Especifique uma consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa. |Uma instrução de consulta. |Não |
| allowPolyBase |Indica se toouse PolyBase (quando aplicável) em vez de mecanismo BULKINSERT. <br/><br/> **Usar o PolyBase é hello recomendado a maneira como os dados tooload no SQL Data Warehouse.** |Verdadeiro <br/>False (padrão) |Não |
| polyBaseSettings |Um grupo de propriedades que podem ser especificadas ao hello **allowPolybase** propriedade for definida muito**true**. |&nbsp; |Não |
| rejectValue |Especifica o número de saudação ou a porcentagem de linhas que pode ser rejeitada antes Olá consulta falhe. <br/><br/>Saiba mais sobre do PolyBase Olá rejeitar opções Olá **argumentos** seção [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) tópico. |0 (padrão), 1, 2, … |Não |
| rejectType |Especifica se a opção de rejectValue de saudação é especificada como um valor literal ou uma porcentagem. |Valor (padrão), Percentual |Não |
| rejectSampleValue |Determina o número de saudação de linhas tooretrieve antes Olá PolyBase recalcula a porcentagem de saudação de linhas rejeitadas. |1, 2, … |Sim, se **rejectType** for **percentual** |
| useTypeDefault |Especifica como toohandle faltando valores delimitados por arquivos de texto quando PolyBase recupera dados do arquivo de texto de saudação.<br/><br/>Saiba mais sobre essa propriedade da seção argumentos Olá [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |True, False (padrão) |Não |
| writeBatchSize |Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize |Inteiro (número de linhas) |Não (padrão: 10000) |
| writeBatchTimeout |Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar. |timespan<br/><br/> Exemplo: "00:30:00" (30 minutos). |Não |

#### <a name="example"></a>Exemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para obter mais informações, consulte o artigo [Conector do SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties). 

## <a name="azure-search"></a>Pesquisa do Azure

### <a name="linked-service"></a>Serviço vinculado
toodefine uma pesquisa do Azure vinculada serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AzureSearch**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
| -------- | ----------- | -------- |
| url | URL de saudação serviço de pesquisa do Azure. | Sim |
| chave | Chave de administração de saudação serviço de pesquisa do Azure. | Sim |

#### <a name="example"></a>Exemplo

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Azure Search](data-factory-azure-search-connector.md#linked-service-properties).

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados de pesquisa do Azure, Olá conjunto **tipo** do conjunto de dados de saudação muito**AzureSearchIndex**e especifique Olá seguintes propriedades em Olá **typeProperties** seção : 

| Propriedade | Descrição | Obrigatório |
| -------- | ----------- | -------- |
| type | propriedade do tipo Hello deve ser definida muito**AzureSearchIndex**.| Sim |
| indexName | Nome do índice de pesquisa do Azure hello. Fábrica de dados não cria o índice de saudação. Olá índice deve existir na pesquisa do Azure. | Sim |

#### <a name="example"></a>Exemplo

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Azure Search](data-factory-azure-search-connector.md#dataset-properties).

### <a name="azure-search-index-sink-in-copy-activity"></a>Coletor do Índice do Azure Search na Atividade de Cópia
Se você estiver copiando o índice de pesquisa do Azure tooan dados, definir Olá **tipo de coletor** de hello atividade de cópia muito**AzureSearchIndexSink**e especificar propriedades no Olá a seguir **coletor**seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Especifica se toomerge ou substituição quando um documento já existe no índice de saudação. | Merge (padrão)<br/>Carregar| Não |
| WriteBatchSize | Carrega dados no índice de pesquisa do Azure hello quando o tamanho do buffer de saudação atingir writeBatchSize. | 1 too1, 000. O valor padrão é 1000. | Não |

#### <a name="example"></a>Exemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Azure Search](data-factory-azure-search-connector.md#copy-activity-properties).

## <a name="azure-table-storage"></a>Armazenamento de Tabelas do Azure

### <a name="linked-service"></a>Serviço vinculado
Há dois tipos de serviços vinculados: serviço vinculado do Armazenamento do Azure e serviço vinculado do Armazenamento do Azure SAS.

#### <a name="azure-storage-linked-service"></a>Serviço vinculado de armazenamento do Azure
toolink sua fábrica de dados de tooa da conta de armazenamento do Azure usando Olá **chave de conta**, crie um serviço vinculado do armazenamento do Azure. toodefine um armazenamento do Azure vinculada serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AzureStorage**. Em seguida, você pode especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| type |propriedade de tipo Hello deve ser definida como: **AzureStorage** |Sim |
| connectionString |Especifique informações necessárias tooconnect tooAzure armazenamento para a propriedade connectionString de saudação. |Sim |

**Exemplo:**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a>Serviço vinculado de SAS de Armazenamento do Azure
Olá SAS de armazenamento do Azure vinculada serviço permite que você toolink uma conta de armazenamento do Azure tooan data factory do Azure usando uma assinatura de acesso compartilhado (SAS). Ele fornece fábrica de dados Olá com acesso restrito/limite de tempo específicos/tooall recursos (blob/contêiner) no armazenamento de saudação. toolink sua fábrica de dados de tooa da conta de armazenamento do Azure usando a assinatura de acesso compartilhado, crie um serviço de SAS do armazenamento do Azure vinculado. toodefine um SAS de armazenamento do Azure vinculada serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**o AzureStorageSas**. Em seguida, você pode especificar propriedades no Olá a seguir **typeProperties** seção:   

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| type |propriedade de tipo Hello deve ser definida como: **o AzureStorageSas** |Sim |
| sasUri |Especifica os recursos de armazenamento do Azure do URI de assinatura de acesso compartilhado toohello como blob, contêiner ou tabela. |Sim |

**Exemplo:**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Para obter mais informações sobre esses serviços vinculados, consulte o artigo [Conector de Armazenamento de Tabelas do Azure](data-factory-azure-table-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados de tabela do Azure, Olá conjunto **tipo** do conjunto de dados de saudação muito**AzureTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação na instância de banco de dados de tabela do Azure Olá que serviço vinculado refere-se a. |Sim. Quando um nome de tabela é especificado sem um azureTableSourceQuery, todos os registros da tabela de saudação são copiados toohello destino. Se um azureTableSourceQuery também for especificado, registros da tabela de saudação que atenda a consulta de saudação são copiados toohello destino. |

#### <a name="example"></a>Exemplo

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Para obter mais informações sobre esses serviços vinculados, consulte o artigo [Conector de Armazenamento de Tabelas do Azure](data-factory-azure-table-connector.md#dataset-properties). 

### <a name="azure-table-source-in-copy-activity"></a>Origem da Tabela do Azure na Atividade de Cópia
Se você estiver copiando dados de armazenamento de tabela do Azure, defina Olá **tipo de fonte** de hello atividade de cópia muito**AzureTableSource**e especificar propriedades no Olá a seguir **fonte**seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| AzureTableSourceQuery |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta de tabela do Azure. Consulte os exemplos na próxima seção, Olá. |Não. Quando um nome de tabela é especificado sem um azureTableSourceQuery, todos os registros da tabela de saudação são copiados toohello destino. Se um azureTableSourceQuery também for especificado, registros da tabela de saudação que atenda a consulta de saudação são copiados toohello destino. |
| azureTableSourceIgnoreTableNotFound |Indique se a exceção de Olá de assimilação da tabela não existe. |TRUE<br/>FALSE |Não |

#### <a name="example"></a>Exemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para obter mais informações sobre esses serviços vinculados, consulte o artigo [Conector de Armazenamento de Tabelas do Azure](data-factory-azure-table-connector.md#copy-activity-properties). 

### <a name="azure-table-sink-in-copy-activity"></a>Coletor da Tabela do Azure na Atividade de Cópia
Se você estiver copiando dados tooAzure armazenamento de tabela, definir Olá **tipo de coletor** de hello atividade de cópia muito**AzureTableSink**e especificar propriedades no Olá a seguir **coletor** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Partição chave valor padrão que pode ser usado pelo coletor de saudação. |Um valor de cadeia de caracteres. |Não |
| azureTablePartitionKeyName |Especifique o nome da coluna Olá cujos valores são usados como chaves de partição. Se não especificado, AzureTableDefaultPartitionKeyValue será usado como chave de partição hello. |Um nome de coluna. |Não |
| azureTableRowKeyName |Especifique o nome da coluna Olá cujos valores de coluna são usados como chave de linha. Se não especificado, um GUID é usado para cada linha. |Um nome de coluna. |Não |
| azureTableInsertType |dados de tooinsert de modo de saudação na tabela do Azure.<br/><br/>Essa propriedade controla se as linhas existentes na tabela de saída de hello com correspondência de chaves de partição e de linha têm seus valores substituídos ou mesclados. <br/><br/>toolearn sobre como essas configurações (mesclagem e substituir) funcionam, consulte [inserir ou mesclar entidade](https://msdn.microsoft.com/library/azure/hh452241.aspx) e [inserir ou substituir entidade](https://msdn.microsoft.com/library/azure/hh452242.aspx) tópicos. <br/><br> Essa configuração se aplica no nível de linha hello, não os nível de tabela Olá, e nenhuma opção exclui linhas na tabela de saída de saudação que não existem na entrada hello. |mesclar (padrão)<br/>substituir |Não |
| writeBatchSize |Insere dados em Olá tabela do Azure quando Olá writeBatchSize ou writeBatchTimeout é atingido. |Inteiro (número de linhas) |Não (padrão: 10000) |
| writeBatchTimeout |Insere dados na Olá tabela do Azure quando Olá writeBatchSize ou writeBatchTimeout é atingido |timespan<br/><br/>Exemplo: "00:20:00" (20 minutos) |Não (valor de tempo limite padrão de cliente de toostorage padrão 90 segundos) |

#### <a name="example"></a>Exemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Para obter mais informações sobre esses serviços vinculados, consulte o artigo [Conector de Armazenamento de Tabelas do Azure](data-factory-azure-table-connector.md#copy-activity-properties). 

## <a name="amazon-redshift"></a>Amazon RedShift

### <a name="linked-service"></a>Serviço vinculado
toodefine um Amazon Redshift o serviço saudação do conjunto vinculado **tipo** de saudação serviço vinculado muito**AmazonRedshift**e especificar propriedades no Olá a seguir **typeProperties**seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| server |IP endereço ou nome de host do servidor do Amazon Redshift hello. |Sim |
| porta |número de saudação de porta TCP Olá Olá Amazon Redshift server usa toolisten para conexões de cliente. |Não, valor padrão: 5439 |
| database |Nome do banco de dados do Amazon Redshift hello. |Sim |
| Nome de Usuário |Nome de usuário que tem o banco de dados do access toohello. |Sim |
| Senha |Senha da conta de usuário de saudação. |Sim |

#### <a name="example"></a>Exemplo

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Amazon Redshift](#data-factory-amazon-redshift-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados do Amazon Redshift conjunto Olá **tipo** do conjunto de dados de saudação muito**RelationalTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome de tabela Olá Olá Amazon Redshift banco de dados do qual o serviço vinculado se refere. |Não (se **query** de **RelationalSource** for especificado) |


#### <a name="example"></a>Exemplo

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Para obter mais informações, consulte o artigo [Conector do Amazon Redshift](#data-factory-amazon-redshift-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Origem Relacional na Atividade de Cópia 
Se você estiver copiando dados do Amazon Redshift, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: `select * from MyTable`. |Não (se **tableName** de **dataset** for especificado) |

#### <a name="example"></a>Exemplo

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Para obter mais informações, consulte o artigo [Conector do Amazon Redshift](#data-factory-amazon-redshift-connector.md#copy-activity-properties).

## <a name="ibm-db2"></a>IBM DB2

### <a name="linked-service"></a>Serviço vinculado
toodefine um IBM DB2 vinculada serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesDB2**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| server |Nome do servidor de saudação DB2. |Sim |
| database |Nome do banco de dados de saudação DB2. |Sim |
| schema |Nome do esquema de saudação no banco de dados de saudação. nome do esquema Olá diferencia maiusculas de minúsculas. |Não |
| authenticationType |Tipo de autenticação usado o banco de dados do DB2 tooconnect toohello. Os valores possíveis são: Anonymous, Basic e Windows. |Sim |
| Nome de Usuário |Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows. |Não |
| Senha |Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação. |Não |
| gatewayName |Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello local DB2. |Sim |

#### <a name="example"></a>Exemplo
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
Para obter mais informações, consulte o artigo [Conector do IBM DB2](#data-factory-onprem-db2-connector.md#linked-service-properties).

### <a name="dataset"></a>Conjunto de dados
conjunto de dados toodefine um DB2, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**e especifique Olá Olá propriedades a seguir **typeProperties** seção:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação na instância de banco de dados DB2 Olá que serviço vinculado refere-se a. Olá tableName diferencia maiusculas de minúsculas. |Não (se **query** de **RelationalSource** for especificado) 

#### <a name="example"></a>Exemplo
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do IBM DB2](#data-factory-onprem-db2-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Origem Relacional na Atividade de Cópia
Se você estiver copiando dados do IBM DB2, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte** seção:


| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: `"query": "select * from "MySchema"."MyTable""`. |Não (se **tableName** de **dataset** for especificado) |

#### <a name="example"></a>Exemplo
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Para obter mais informações, consulte o artigo [Conector do IBM DB2](#data-factory-onprem-db2-connector.md#copy-activity-properties).

## <a name="mysql"></a>MySQL

### <a name="linked-service"></a>Serviço vinculado
toodefine um MySQL vinculados serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesMySql**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| server |Nome do servidor MySQL de saudação. |Sim |
| database |Nome do banco de dados do hello MySQL. |Sim |
| schema |Nome do esquema de saudação no banco de dados de saudação. |Não |
| authenticationType |Tipo de autenticação usado o banco de dados do tooconnect toohello MySQL. Os valores possíveis são: `Basic`. |Sim |
| Nome de Usuário |Especifique o banco de dados do usuário nome tooconnect toohello MySQL. |Sim |
| Senha |Especifique a senha da conta de usuário de saudação especificado. |Sim |
| gatewayName |Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello local MySQL. |Sim |

#### <a name="example"></a>Exemplo

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do MySQL](data-factory-onprem-mysql-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados MySQL, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação em Olá instância de banco de dados MySQL serviço vinculado refere-se a. |Não (se **query** de **RelationalSource** for especificado) |

#### <a name="example"></a>Exemplo

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Para obter mais informações, consulte o artigo [Conector do MySQL](data-factory-onprem-mysql-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origem Relacional na Atividade de Cópia
Se você estiver copiando dados de um banco de dados MySQL, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte** seção:


| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: `select * from MyTable`. |Não (se **tableName** de **dataset** for especificado) |


#### <a name="example"></a>Exemplo
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Para obter mais informações, consulte o artigo [Conector do MySQL](data-factory-onprem-mysql-connector.md#copy-activity-properties). 

## <a name="oracle"></a>Oracle 

### <a name="linked-service"></a>Serviço vinculado
toodefine um Oracle o serviço saudação do conjunto vinculado **tipo** de saudação serviço vinculado muito**OnPremisesOracle**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| driverType | Especifique quais dados do driver toouse toocopy de / tooOracle banco de dados. Valores permitidos são **Microsoft** ou **ODP** (padrão). Consulte [suporte para instalação e da versão](#supported-versions-and-installation) seção detalhes do driver. | Não |
| connectionString | Especifique informações necessárias a instância de banco de dados Oracle toohello tooconnect para a propriedade connectionString de saudação. | Sim |
| gatewayName | Nome do gateway de saudação que é usado tooconnect toohello servidor Oracle local |Sim |

#### <a name="example"></a>Exemplo
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Oracle](data-factory-onprem-oracle-connector.md#linked-service-properties).

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados Oracle, Olá conjunto **tipo** do conjunto de dados de saudação muito**OracleTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação na Olá banco de dados Oracle que Olá serviço vinculado refere-se a. |Não (se **oracleReaderQuery** de **OracleSource** for especificado) |

#### <a name="example"></a>Exemplo

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Para obter mais informações, consulte o artigo [Conector do Oracle](data-factory-onprem-oracle-connector.md#dataset-properties).

### <a name="oracle-source-in-copy-activity"></a>Origem do Oracle na Atividade de Cópia
Se você estiver copiando dados de um banco de dados Oracle, defina Olá **tipo de fonte** de hello atividade de cópia muito**OracleSource**e especificar propriedades no Olá a seguir **fonte** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| oracleReaderQuery |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: `select * from MyTable` <br/><br/>Se não for especificado, Olá instrução SQL executada:`select * from MyTable` |Não (se **tableName** de **dataset** for especificado) |

#### <a name="example"></a>Exemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).

### <a name="oracle-sink-in-copy-activity"></a>Coletor do Oracle na Atividade de Cópia
Se você estiver copiando o banco de dados do Oracle data tooam, defina Olá **tipo de coletor** de hello atividade de cópia muito**OracleSink**e especificar propriedades no Olá a seguir **coletor** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| writeBatchTimeout |Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar. |timespan<br/><br/> Exemplo: "00:30:00" (30 minutos). |Não |
| writeBatchSize |Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize. |Inteiro (número de linhas) |Não (padrão: 100) |
| sqlWriterCleanupScript |Especifique uma consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa. |Uma instrução de consulta. |Não |
| sliceIdentifierColumnName |Especifique o nome de coluna para a atividade de cópia toofill com identificador de fatia gerado automaticamente, que é usado tooclean os dados de uma fatia específica quando executada novamente. |Nome de uma coluna com tipo de dados de binário (32). |Não |

#### <a name="example"></a>Exemplo
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Para obter mais informações, consulte o artigo [Conector do Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).

## <a name="postgresql"></a>PostgreSQL

### <a name="linked-service"></a>Serviço vinculado
toodefine um PostgreSQL vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesPostgreSql**e especificar propriedades no Olá a seguir **typeProperties**seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| server |Nome do servidor do hello PostgreSQL. |Sim |
| database |Nome do banco de dados PostgreSQL hello. |Sim |
| schema |Nome do esquema de saudação no banco de dados de saudação. nome do esquema Olá diferencia maiusculas de minúsculas. |Não |
| authenticationType |Tipo de autenticação usado o banco de dados PostgreSQL toohello tooconnect. Os valores possíveis são: Anonymous, Basic e Windows. |Sim |
| Nome de Usuário |Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows. |Não |
| Senha |Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação. |Não |
| gatewayName |Nome do gateway Olá Olá serviço da fábrica de dados deve usar tooconnect toohello local banco de dados PostgreSQL. |Sim |

#### <a name="example"></a>Exemplo

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
Para obter mais informações, consulte o artigo [Conector do PostgreSQL](data-factory-onprem-postgresql-connector.md#linked-service-properties).

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados PostgreSQL, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação em Olá instância de banco de dados PostgreSQL serviço vinculado refere-se a. Olá tableName diferencia maiusculas de minúsculas. |Não (se **query** de **RelationalSource** for especificado) |

#### <a name="example"></a>Exemplo
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Para obter mais informações, consulte o artigo [Conector do PostgreSQL](data-factory-onprem-postgresql-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Origem Relacional na Atividade de Cópia
Se você estiver copiando dados de um banco de dados PostgreSQL, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte**seção:


| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: "query": "select * from \"MySchema\".\"MyTable\"". |Não (se **tableName** de **dataset** for especificado) |

#### <a name="example"></a>Exemplo

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Para obter mais informações, consulte o artigo [Conector do PostgreSQL](data-factory-onprem-postgresql-connector.md#copy-activity-properties).

## <a name="sap-business-warehouse"></a>SAP Business Warehouse


### <a name="linked-service"></a>Serviço vinculado
toodefine um SAP Business Warehouse (BW) o serviço saudação do conjunto vinculado **tipo** de saudação serviço vinculado muito**SapBw**e especificar propriedades no Olá a seguir **typeProperties**seção:  

Propriedade | Descrição | Valores permitidos | Obrigatório
-------- | ----------- | -------------- | --------
server | Nome do servidor de saudação no qual Olá SAP BW instância reside. | string | Sim
systemNumber | Número de sistema de saudação sistema SAP BW. | Número decimal de dois dígitos representado como uma cadeia de caracteres. | Sim
clientId | ID do cliente do cliente Olá Olá sistema SAP W. | Número decimal de três dígitos representado como uma cadeia de caracteres. | Sim
Nome de Usuário | Nome de usuário de saudação que tem acesso toohello SAP server | string | Sim
Senha | Senha do usuário hello. | string | Sim
gatewayName | Nome do gateway Olá Olá serviço da fábrica de dados deve usar a instância de SAP BW tooconnect toohello local. | string | Sim
encryptedCredential | cadeia de caracteres de credencial Olá criptografado. | string | Não

#### <a name="example"></a>Exemplo

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados do SAP BW, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**. Não existem propriedades específicas do tipo de suporte para o conjunto de dados de SAP BW de saudação do tipo **RelationalTable**.  

#### <a name="example"></a>Exemplo

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Para obter mais informações, consulte o artigo [Conector do SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origem Relacional na Atividade de Cópia
Se você estiver copiando dados do SAP Business Warehouse, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte**seção:


| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query | Especifica Olá MDX consulta tooread dados da instância do SAP BW hello. | Consulta MDX. | Sim |

#### <a name="example"></a>Exemplo

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Para obter mais informações, consulte o artigo [Conector do SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#copy-activity-properties). 

## <a name="sap-hana"></a>SAP HANA

### <a name="linked-service"></a>Serviço vinculado
toodefine um SAP HANA vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**SapHana**e especificar propriedades no Olá a seguir **typeProperties** seção:  

Propriedade | Descrição | Valores permitidos | Obrigatório
-------- | ----------- | -------------- | --------
server | Nome do servidor de saudação no qual Olá SAP HANA instância reside. Se o servidor estiver usando uma porta personalizada, especifique `server:port`. | string | Sim
authenticationType | Tipo de autenticação. | cadeia de caracteres. "Básico" ou "Windows" | Sim 
Nome de Usuário | Nome de usuário de saudação que tem acesso toohello SAP server | string | Sim
Senha | Senha do usuário hello. | string | Sim
gatewayName | Nome do gateway Olá Olá serviço da fábrica de dados deve usar a instância de SAP HANA tooconnect toohello local. | string | Sim
encryptedCredential | cadeia de caracteres de credencial Olá criptografado. | string | Não

#### <a name="example"></a>Exemplo

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
Para obter mais informações, consulte o artigo [Conector do SAP HANA](data-factory-sap-hana-connector.md#linked-service-properties).
 
### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados do SAP HANA, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**. Não existem propriedades específicas do tipo de suporte para o dataset do SAP HANA saudação do tipo **RelationalTable**. 

#### <a name="example"></a>Exemplo

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Para obter mais informações, consulte o artigo [Conector do SAP HANA](data-factory-sap-hana-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origem Relacional na Atividade de Cópia
Se você estiver copiando dados de um repositório de dados do SAP HANA, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte**seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query | Especifica Olá SQL consulta tooread dados da instância do SAP HANA hello. | Consulta SQL. | Sim |


#### <a name="example"></a>Exemplo


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Para obter mais informações, consulte o artigo [Conector do SAP HANA](data-factory-sap-hana-connector.md#copy-activity-properties).


## <a name="sql-server"></a>SQL Server

### <a name="linked-service"></a>Serviço vinculado
Criar um serviço vinculado do tipo **OnPremisesSqlServer** toolink uma fábrica de dados tooa de banco de dados do local do SQL Server. Olá a tabela a seguir fornece uma descrição para o serviço vinculado do SQL Server do JSON elementos tooon local específico.

Olá, a tabela a seguir fornece uma descrição para o JSON de elementos específico tooSQL serviço do servidor vinculado.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **OnPremisesSqlServer**. |Sim |
| connectionString |Especifica informações de connectionString necessárias tooconnect toohello no SQL Server banco de dados local usando a autenticação do Windows ou autenticação do SQL. |Sim |
| gatewayName |Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello no local do SQL Server. |Sim |
| Nome de Usuário |Especifique o nome de usuário se você estiver usando a Autenticação do Windows. Exemplo: **domainname\\username**. |Não |
| Senha |Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação. |Não |

Você pode criptografar credenciais usando Olá **New-AzureRmDataFactoryEncryptValue** cmdlet e usá-los na cadeia de caracteres de conexão hello, conforme mostrado no exemplo a seguir de saudação (**EncryptedCredential** propriedade):  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Exemplo: JSON para usar Autenticação SQL

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Exemplo: JSON para usar Autenticação Windows

Se o nome de usuário e senha forem especificados, gateway usa tooimpersonate Olá dados do usuário especificado conta tooconnect toohello local do SQL Server. Caso contrário, o gateway conecta toohello do SQL Server diretamente com o contexto de segurança de saudação do Gateway (sua conta de inicialização).

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector de SQL Server](data-factory-sqlserver-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados do SQL Server, Olá conjunto **tipo** do conjunto de dados de saudação muito**SqlServerTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação ou exibição na instância de banco de dados do SQL Server Olá que serviço vinculado refere-se a. |Sim |

#### <a name="example"></a>Exemplo
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector de SQL Server](data-factory-sqlserver-connector.md#dataset-properties). 

### <a name="sql-source-in-copy-activity"></a>Origem do SQL na Atividade de Cópia
Se você estiver copiando dados de um banco de dados do SQL Server, defina Olá **tipo de fonte** de hello atividade de cópia muito**SqlSource**e especificar propriedades no Olá a seguir **fonte** seção:


| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| SqlReaderQuery |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: `select * from MyTable`. Pode fazer referência a várias tabelas de banco de dados de saudação referenciado pelo conjunto de dados de entrada hello. Se não for especificado, Olá instrução SQL executada: selecione MyTable. |Não |
| sqlReaderStoredProcedureName |Nome da saudação procedimento armazenado que lê dados da tabela de origem hello. |Nome da saudação de procedimento armazenado. |Não |
| storedProcedureParameters |Parâmetros de saudação de procedimento armazenado. |Pares de nome/valor. Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação. |Não |

Se hello **sqlReaderQuery** é especificada para Olá SqlSource, hello atividade de cópia executa esta consulta em relação aos dados de Olá Olá banco de dados do SQL Server fonte tooget.

Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros).

Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de Olá definidas na seção de estrutura hello são usada toobuild toorun uma consulta select contra Olá banco de dados do SQL Server. Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.

> [!NOTE]
> Quando você usa **sqlReaderStoredProcedureName**, você ainda precisa toospecify um valor para Olá **tableName** propriedade no conjunto de dados Olá JSON. Contudo, não há nenhuma validação executada nessa tabela.


#### <a name="example"></a>Exemplo
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Neste exemplo, **sqlReaderQuery** é especificado para Olá SqlSource. Hello atividade de cópia executa esta consulta Olá dados do banco de dados do SQL Server origem tooget hello. Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros). Olá sqlReaderQuery pode fazer referência a várias tabelas no banco de dados de saudação referenciado pelo conjunto de dados de entrada hello. Ele não é limitado tooonly Olá definido como Olá typeProperty de tableName do conjunto de dados.

Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de Olá definidas na seção de estrutura hello são usada toobuild toorun uma consulta select contra Olá banco de dados do SQL Server. Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.

Para obter mais informações, consulte o artigo [Conector de SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). 

### <a name="sql-sink-in-copy-activity"></a>Coletor do Sql na Atividade de Cópia
Se você estiver copiando o banco de dados do SQL Server data tooa, defina Olá **tipo de coletor** de hello atividade de cópia muito**SqlSink**e especificar propriedades no Olá a seguir **coletor** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| writeBatchTimeout |Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar. |timespan<br/><br/> Exemplo: "00:30:00" (30 minutos). |Não |
| writeBatchSize |Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize. |Inteiro (número de linhas) |Não (padrão: 10000) |
| sqlWriterCleanupScript |Especifique a consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa. Para saber mais, confira a seção de [repetição](#repeatability-during-copy) . |Uma instrução de consulta. |Não |
| sliceIdentifierColumnName |Especifique o nome de coluna para a atividade de cópia toofill com identificador de fatia gerado automaticamente, que é usado tooclean os dados de uma fatia específica quando executada novamente. Para saber mais, confira a seção de [repetição](#repeatability-during-copy) . |Nome de uma coluna com tipo de dados de binário (32). |Não |
| sqlWriterStoredProcedureName |Nome do hello procedimento armazenado dados upserts (atualizações/inserções) na tabela de destino de saudação. |Nome da saudação de procedimento armazenado. |Não |
| storedProcedureParameters |Parâmetros de saudação de procedimento armazenado. |Pares de nome/valor. Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação. |Não |
| sqlWriterTableType |Especifique toobe de nome de tipo de tabela usado no procedimento armazenado de saudação. Atividade de cópia disponibiliza dados Olá movidos em uma tabela temporária com esse tipo de tabela. Código do procedimento armazenado, em seguida, pode mesclar dados de saudação sejam copiados com os dados existentes. |Um nome de tipo de tabela. |Não |

#### <a name="example"></a>Exemplo
pipeline de saudação contém uma atividade de cópia que esteja configurado toouse esses conjuntos de dados de entrada e saídos e toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**BlobSource** e **coletor** tipo está definido muito**SqlSink**.

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para obter mais informações, consulte o artigo [Conector de SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). 

## <a name="sybase"></a>Sybase

### <a name="linked-service"></a>Serviço vinculado
toodefine um Sybase vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesSybase**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| server |Nome do servidor do Sybase hello. |Sim |
| database |Nome do banco de dados do Sybase hello. |Sim |
| schema |Nome do esquema de saudação no banco de dados de saudação. |Não |
| authenticationType |Tipo de autenticação usado o banco de dados do Sybase tooconnect toohello. Os valores possíveis são: Anonymous, Basic e Windows. |Sim |
| Nome de Usuário |Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows. |Não |
| Senha |Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação. |Não |
| gatewayName |Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados Sybase local de toohello de tooconnect. |Sim |

#### <a name="example"></a>Exemplo
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Sybase](data-factory-onprem-sybase-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados Sybase, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação em Olá instância de banco de dados Sybase serviço vinculado refere-se a. |Não (se **query** de **RelationalSource** for especificado) |

#### <a name="example"></a>Exemplo

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Sybase](data-factory-onprem-sybase-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origem Relacional na Atividade de Cópia
Se você estiver copiando dados de um banco de dados Sybase, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte** seção:


| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: `select * from MyTable`. |Não (se **tableName** de **dataset** for especificado) |

#### <a name="example"></a>Exemplo

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Sybase](data-factory-onprem-sybase-connector.md#copy-activity-properties).

## <a name="teradata"></a>Teradata

### <a name="linked-service"></a>Serviço vinculado
toodefine um Teradata vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesTeradata**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| server |Nome do servidor de Teradata hello. |Sim |
| authenticationType |Tipo de autenticação usado o banco de dados do tooconnect toohello Teradata. Os valores possíveis são: Anonymous, Basic e Windows. |Sim |
| Nome de Usuário |Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows. |Não |
| Senha |Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação. |Não |
| gatewayName |Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello local Teradata. |Sim |

#### <a name="example"></a>Exemplo
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Teradata](data-factory-onprem-teradata-connector.md#linked-service-properties).

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados de Teradata Blob, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**. No momento, não há nenhuma propriedade de tipo com suporte para o conjunto de dados de Teradata hello. 

#### <a name="example"></a>Exemplo
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Teradata](data-factory-onprem-teradata-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Origem Relacional na Atividade de Cópia
Se você estiver copiando dados de um banco de dados Teradata, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte**seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: `select * from MyTable`. |Sim |

#### <a name="example"></a>Exemplo

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Teradata](data-factory-onprem-teradata-connector.md#copy-activity-properties).

## <a name="cassandra"></a>Cassandra


### <a name="linked-service"></a>Serviço vinculado
toodefine um Cassandra vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesCassandra**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| host |Um ou mais endereços IP ou nomes de host dos servidores Cassandra.<br/><br/>Especifique uma lista separada por vírgulas de endereços IP ou host nomes tooconnect tooall servidores simultaneamente. |Sim |
| porta |Olá porta TCP que Olá servidor Cassandra usa toolisten para conexões de cliente. |Não, valor padrão: 9042 |
| authenticationType |Básica, ou Anônima |Sim |
| Nome de Usuário |Especifique o nome de usuário para a conta de usuário de saudação. |Sim, se authenticationType é definido tooBasic. |
| Senha |Especifique a senha da conta de usuário de saudação. |Sim, se authenticationType é definido tooBasic. |
| gatewayName |nome de saudação do gateway de saudação que é usado tooconnect toohello Cassandra banco de dados no local. |Sim |
| encryptedCredential |Credencial criptografada pelo gateway hello. |Não |

#### <a name="example"></a>Exemplo

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Cassandra](data-factory-onprem-cassandra-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados Cassandra, Olá conjunto **tipo** do conjunto de dados de saudação muito**CassandraTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| keyspace |Nome da saudação keyspace ou esquema Cassandra banco de dados. |Sim (se a **consulta** para **CassandraSource** não estiver definida). |
| tableName |Nome da tabela de saudação no banco de dados Cassandra. |Sim (se a **consulta** para **CassandraSource** não estiver definida). |

#### <a name="example"></a>Exemplo

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Cassandra](data-factory-onprem-cassandra-connector.md#dataset-properties). 

### <a name="cassandra-source-in-copy-activity"></a>Origem do Cassandra na Atividade de Cópia
Se você estiver copiando dados de Cassandra, defina Olá **tipo de fonte** de hello atividade de cópia muito**CassandraSource**e especificar propriedades no Olá a seguir **fonte** seção :

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Consulta SQL-92 ou consulta CQL. Veja [Referência ao CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html). <br/><br/>Ao usar a consulta SQL, especifique **keyspace name.table nome** toorepresent Olá tabela tooquery. |Não (se tableName e keyspace no conjunto de dados estiverem definidos). |
| consistencyLevel |nível de consistência de saudação especifica quantas réplicas deve responder a solicitação de leitura de tooa antes de retornar o aplicativo de cliente de toohello de dados. Verificações de Cassandra Olá número especificado de réplicas para a solicitação de leitura de saudação do toosatisfy de dados. |ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE. Confira [Configuring data consistency (Configurando a consistência de dados)](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) para obter detalhes. |Não. O valor padrão é ONE. |

#### <a name="example"></a>Exemplo
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Cassandra](data-factory-onprem-cassandra-connector.md#copy-activity-properties).

## <a name="mongodb"></a>MongoDB

### <a name="linked-service"></a>Serviço vinculado
toodefine um MongoDB vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesMongoDB**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| server |IP endereço ou nome de host do servidor do MongoDB hello. |Sim |
| porta |Porta TCP que Olá MongoDB server usa toolisten para conexões de cliente. |Opcional, valor padrão: 27017 |
| authenticationType |Básica ou Anônima. |Sim |
| Nome de Usuário |Conta de usuário tooaccess MongoDB. |Sim (se a autenticação básica for usada). |
| Senha |Senha do usuário hello. |Sim (se a autenticação básica for usada). |
| authSource |Nome do banco de dados do MongoDB Olá que você deseja toouse toocheck suas credenciais para autenticação. |Opcional (se a autenticação básica for usada). padrão: usa a conta de administrador hello e banco de dados de saudação especificado usando a propriedade databaseName. |
| databaseName |Nome do banco de dados do MongoDB Olá que você deseja tooaccess. |Sim |
| gatewayName |Nome do gateway de saudação que acessa o repositório de dados de saudação. |Sim |
| encryptedCredential |Credencial criptografada pelo gateway. |Opcional |

#### <a name="example"></a>Exemplo

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do MongoDB](data-factory-on-premises-mongodb-connector.md#linked-service-properties).

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados do MongoDB, Olá conjunto **tipo** do conjunto de dados de saudação muito**MongoDbCollection**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| collectionName |Nome da coleção de saudação no banco de dados do MongoDB. |Sim |

#### <a name="example"></a>Exemplo

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

Para obter mais informações, consulte o artigo [Conector do MongoDB](data-factory-on-premises-mongodb-connector.md#dataset-properties).

#### <a name="mongodb-source-in-copy-activity"></a>Origem do MongoDB na Atividade de Cópia
Se você estiver copiando dados do MongoDB, defina Olá **tipo de fonte** de hello atividade de cópia muito**MongoDbSource**e especificar propriedades no Olá a seguir **fonte** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Cadeia de consulta SQL-92. Por exemplo: `select * from MyTable`. |Não (se **collectionName** de **dataset** for especificado) |

#### <a name="example"></a>Exemplo

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Para obter mais informações, consulte o artigo [Conector do MongoDB](data-factory-on-premises-mongodb-connector.md#copy-activity-properties).

## <a name="amazon-s3"></a>Amazon S3


### <a name="linked-service"></a>Serviço vinculado
toodefine um S3 Amazon vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AwsAccessKey**e especificar propriedades no Olá a seguir **typeProperties** seção :  

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| accessKeyID |ID da chave de acesso ao segredo hello. |string |Sim |
| secretAccessKey |chave de acesso ao segredo Olá em si. |Cadeia de caracteres secreta criptografada |Sim |

#### <a name="example"></a>Exemplo
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Amazon S3](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).

### <a name="dataset"></a>Conjunto de dados
toodefine um S3 Amazon o conjunto de dados, conjunto Olá **tipo** do conjunto de dados de saudação muito**AmazonS3**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| bucketName |nome de bucket Olá S3. |Cadeia de caracteres |Sim |
| chave |chave do objeto Olá S3. |Cadeia de caracteres |Não |
| prefixo |Prefixo da chave do objeto Olá S3. Objetos cujas chaves começam com esse prefixo serão selecionados. Aplica-se apenas quando a chave está vazia. |string |Não |
| version |versão de saudação do objeto de S3 se o controle de versão S3 estiver habilitado. |Cadeia de caracteres |Não |
| formato | Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Saudação de conjunto **tipo** propriedade em formato tooone desses valores. Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída. |Não | |
| compactação | Especifica tipo de saudação e nível de compactação de dados de saudação. Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. níveis de saudação com suporte são: **ideal** e **mais rápido**. Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory). |Não | |


> [!NOTE]
> bucketName + chave especifica o local de saudação do objeto Olá S3 onde bucket é recipiente raiz Olá S3 objetos e a chave é Olá caminho completo tooS3 objeto.

#### <a name="example-sample-dataset-with-prefix"></a>Exemplo: Conjunto de dados de exemplo com o prefixo

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a>Exemplo: Conjunto de dados de exemplo (com a versão)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a>Exemplo: Caminhos dinâmicos para S3
Exemplo hello, usamos valores fixos para propriedades de chave e bucketName no conjunto de dados Olá Amazon S3.

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

Você pode fazer com que o Data Factory calcular chave hello e bucketName dinamicamente em tempo de execução usando variáveis de sistema como SliceStart.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

Você pode fazer Olá mesmo para a propriedade de prefixo de saudação de um conjunto de dados do Amazon S3. Veja [Funções e variáveis do sistema do Data Factory](data-factory-functions-variables.md) para obter uma lista das funções e variáveis com suporte.

Para obter mais informações, consulte o artigo [Conector do Amazon S3](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Origem do Sistema de Arquivos na Atividade de Cópia
Se você estiver copiando dados do Amazon S3, defina Olá **tipo de fonte** de hello atividade de cópia muito**FileSystemSource**e especificar propriedades no Olá a seguir **fonte** seção :


| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| recursiva |Especifica se a lista de toorecursively S3 objetos no diretório de saudação. |true/false |Não |


#### <a name="example"></a>Exemplo


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

Para obter mais informações, consulte o artigo [Conector do Amazon S3](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).

## <a name="file-system"></a>Sistema de Arquivos


### <a name="linked-service"></a>Serviço vinculado
Você pode vincular uma fábrica de dados do Azure local arquivo sistema tooan com hello **o servidor de arquivos local** serviço vinculado. Olá a tabela a seguir fornece descrições dos elementos JSON que são específico toohello serviço vinculado de servidor de arquivos local.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |Verifique se a propriedade de tipo hello está definida muito**OnPremisesFileServer**. |Sim |
| host |Especifica o caminho de raiz de saudação da pasta Olá que você deseja toocopy. Use o caractere de escape de saudação ' \ ' para caracteres especiais na cadeia de caracteres de saudação. Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos. |Sim |
| userid |Especifique a ID de saudação do usuário de saudação que tem acesso toohello server. |Não (se você escolher encryptedcredential) |
| Senha |Especifique a senha de saudação para usuário hello (userid). |Não (se você escolher encryptedcredential |
| encryptedCredential |Especifique credenciais Olá criptografado que você pode obter executando Olá AzureRmDataFactoryEncryptValue novo cmdlet. |Não (se você escolher toospecify ID de usuário e senha em texto sem formatação) |
| gatewayName |Especifica o nome de saudação do gateway de saudação que Data Factory deve usar o servidor de arquivos tooconnect toohello local. |Sim |

#### <a name="sample-folder-path-definitions"></a>Exemplos de definições de caminho de pasta 
| Cenário | Host em definição de serviço vinculado | folderPath em definição de conjunto de dados |
| --- | --- | --- |
| Pasta local no computador do Gateway de Gerenciamento de Dados  <br/><br/>Exemplos: D:\\\* ou D:\pasta\subpasta\\* |D:\\\\ (para o Gateway de Gerenciamento de Dados 2.0 e versões posteriores) <br/><br/> localhost (para versões anteriores do Gateway de Gerenciamento de Dados 2.0) |.\\\\ ou pasta\\\\subpasta (para o Gateway de Gerenciamento de Dados 2.0 e versões posteriores) <br/><br/>D:\\\\ ou D:\\\\pasta\\\\subpasta (para a versão de gateway abaixo de 2.0) |
| Pasta compartilhada remota:  <br/><br/>Exemplos: \\\\meuservidor\\compartilhar\\\* ou \\\\meuservidor\\compartilhar\\pasta\\subpasta\\* |\\\\\\\\meuservidor\\\\compartilhar |.\\\\ ou pasta\\\\subpasta |


#### <a name="example-using-username-and-password-in-plain-text"></a>Exemplo: usando username e password em texto sem formatação

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a>Exemplo: usando encryptedcredential

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Para obter mais informações, consulte o [artigo Conector do Sistema de Arquivos](data-factory-onprem-file-system-connector.md#linked-service-properties).

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados do sistema de arquivos, Olá conjunto **tipo** do conjunto de dados de saudação muito**FileShare**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| folderPath |Especifica a pasta de toohello subcaminho hello. Use o caractere de escape de saudação ' \' para caracteres especiais na cadeia de caracteres de saudação. Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.<br/><br/>Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia datas / horas de início/término. |Sim |
| fileName |Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello. Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.<br/><br/>Quando o nome de arquivo não for especificado para um conjunto de dados de saída, o nome de saudação do arquivo hello gerado está em Olá formato a seguir: <br/><br/>`Data.<Guid>.txt` (Exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Não |
| fileFilter |Especifique um filtro toobe usado tooselect um subconjunto de arquivos no hello folderPath em vez de todos os arquivos. <br/><br/>Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).<br/><br/>Exemplo 1: "fileFilter": "*.log"<br/>Exemplo 2: "fileFilter": 2016-1-?.txt"<br/><br/>Observe que fileFilter é aplicável a um conjunto de dados FileShare de entrada. |Não |
| partitionedBy |Você pode usar partitionedBy toospecify um dinâmico folderPath/nome do arquivo de dados da série temporal. Um exemplo é folderPath parametrizado para cada hora dos dados. |Não |
| formato | Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Saudação de conjunto **tipo** propriedade em formato tooone desses valores. Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída. |Não |
| compactação | Especifica tipo de saudação e nível de compactação de dados de saudação. Os tipos compatíveis são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**; e os níveis permitidos são: **Ideal** e **Mais rápido**. confira [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Não |

> [!NOTE]
> Você não pode usar fileName e fileFilter simultaneamente.

#### <a name="example"></a>Exemplo

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Para obter mais informações, consulte o [artigo Conector do Sistema de Arquivos](data-factory-onprem-file-system-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Origem do Sistema de Arquivos na Atividade de Cópia
Se você estiver copiando dados de sistema de arquivos, defina Olá **tipo de fonte** de hello atividade de cópia muito**FileSystemSource**e especificar propriedades no Olá a seguir **fonte** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| recursiva |Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello. |True, False (padrão) |Não |

#### <a name="example"></a>Exemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Para obter mais informações, consulte o [artigo Conector do Sistema de Arquivos](data-factory-onprem-file-system-connector.md#copy-activity-properties).

### <a name="file-system-sink-in-copy-activity"></a>Coletor do Sistema de Arquivos na Atividade de Cópia
Se você estiver copiando dados tooFile sistema, definir Olá **tipo de coletor** de hello atividade de cópia muito**FileSystemSink**e especificar propriedades no Olá a seguir **coletor** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| copyBehavior |Define o comportamento de cópia de saudação quando origem Olá é BlobSource ou sistema de arquivos. |**PreserveHierarchy:** preserva a hierarquia de arquivo hello na pasta de destino de saudação. Ou seja, caminho relativo do Olá Olá arquivo toohello origem da pasta de origem é Olá igual Olá o caminho relativo da pasta de destino toohello do arquivo de destino hello.<br/><br/>**FlattenHierarchy:** todos os arquivos da pasta de origem Olá são criados no primeiro nível saudação da pasta de destino. arquivos de destino de saudação são criados com um nome gerado automaticamente.<br/><br/>**MergeFiles:** mescla todos os arquivos Olá pasta tooone do arquivo de origem. Se o nome do blob/nome de arquivo hello for especificado, o nome mesclado Olá é nome especificado da saudação. Caso contrário, ele será um nome de arquivo gerado automaticamente. |Não |
auto-

#### <a name="example"></a>Exemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para obter mais informações, consulte o [artigo Conector do Sistema de Arquivos](data-factory-onprem-file-system-connector.md#copy-activity-properties).

## <a name="ftp"></a>FTP

### <a name="linked-service"></a>Serviço vinculado
toodefine um FTP o serviço saudação do conjunto vinculado **tipo** de saudação serviço vinculado muito**FtpServer**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório | Padrão |
| --- | --- | --- | --- |
| host |Nome ou endereço IP do servidor FTP de saudação |Sim |&nbsp; |
| authenticationType |Especificar tipo de autenticação |Sim |Básica, Anônima |
| Nome de Usuário |Usuário que tem acesso toohello FTP servidor |Não |&nbsp; |
| Senha |Senha do usuário da saudação (nome de usuário) |Não |&nbsp; |
| encryptedCredential |Servidor FTP credencial criptografada tooaccess Olá |Não |&nbsp; |
| gatewayName |Nome da saudação Data Management Gateway gateway tooconnect tooan servidor FTP local |Não |&nbsp; |
| porta |Porta na qual Olá FTP server está escutando |Não |21 |
| enableSsl |Especifique se toouse FTP por canal SSL/TLS |Não |verdadeiro |
| enableServerCertificateValidation |Especifique se o servidor de tooenable SSL a validação de certificado ao usar o FTP no canal SSL/TLS |Não |verdadeiro |

#### <a name="example-using-anonymous-authentication"></a>Exemplo: Usando a autenticação anônima

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a>Exemplo: Usando o nome de usuário e a senha em texto sem formatação para autenticação básica

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a>Exemplo: Usando a porta, enableSsl, enableServerCertificateValidation

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a>Exemplo: Usando encryptedCredential para autenticação e gateway

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

Para obter mais informações, consulte o artigo [Conector do FTP](data-factory-ftp-connector.md#linked-service-properties).

### <a name="dataset"></a>Conjunto de dados
toodefine um FTP de conjunto de dados, conjunto Olá **tipo** do conjunto de dados de saudação muito**FileShare**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| folderPath |Subpasta toohello mais recente para o caminho. Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres de saudação. Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.<br/><br/>Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia datas / horas de início/término. |Sim 
| fileName |Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello. Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.<br/><br/>Quando o nome de arquivo não for especificado para um conjunto de dados de saída, o nome de saudação do arquivo hello gerado aparecerá em Olá esse formato a seguir: <br/><br/>Data.<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Não |
| fileFilter |Especifique um filtro toobe usado tooselect um subconjunto de arquivos no hello folderPath em vez de todos os arquivos.<br/><br/>Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).<br/><br/>Exemplo 1: `"fileFilter": "*.log"`<br/>Exemplo 2: `"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter é aplicável a um conjunto de dados FileShare de entrada. Essa propriedade não tem suporte com HDFS. |Não |
| partitionedBy |partitionedBy pode ser usado toospecify um folderPath dinâmico, nome de arquivo para dados de série temporal. Por exemplo, folderPath parametrizado para cada hora dos dados. |Não |
| formato | Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Saudação de conjunto **tipo** propriedade em formato tooone desses valores. Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída. |Não |
| compactação | Especifica tipo de saudação e nível de compactação de dados de saudação. Os tipos compatíveis são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**; e os níveis permitidos são: **Ideal** e **Mais rápido**. Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory). |Não |
| useBinaryTransfer |Especifique se deve usar o modo de transferência Binário. True para o modo binário e ASCII false. Valor padrão: True. Essa propriedade só pode ser usada quando o tipo de serviço vinculado associado for do tipo: FtpServer. |Não |

> [!NOTE]
> filename e fileFilter não podem ser usados simultaneamente.

#### <a name="example"></a>Exemplo

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do FTP](data-factory-ftp-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Origem do Sistema de Arquivos na Atividade de Cópia
Se você estiver copiando dados de um servidor FTP, defina Olá **tipo de fonte** de hello atividade de cópia muito**FileSystemSource**e especificar propriedades no Olá a seguir **fonte** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| recursiva |Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello. |True, False (padrão) |Não |

#### <a name="example"></a>Exemplo

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

Para obter mais informações, consulte o artigo [Conector do FTP](data-factory-ftp-connector.md#copy-activity-properties).


## <a name="hdfs"></a>HDFS

### <a name="linked-service"></a>Serviço vinculado
toodefine um HDFS o serviço saudação do conjunto vinculado **tipo** de saudação serviço vinculado muito**Hdfs**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **Hdfs** |Sim |
| Url |URL toohello HDFS |Sim |
| authenticationType |Anônimo ou Windows. <br><br> toouse **a autenticação Kerberos** para conector HDFS, consulte muito[nesta seção](#use-kerberos-authentication-for-hdfs-connector) tooset seu ambiente local adequadamente. |Sim |
| userName |Nome de usuário para a autenticação do Windows. |Sim (para a Autenticação do Windows) |
| Senha |Senha para a autenticação do Windows. |Sim (para a Autenticação do Windows) |
| gatewayName |Nome do gateway Olá Olá serviço da fábrica de dados deve usar tooconnect toohello HDFS. |Sim |
| encryptedCredential |[Novo AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) saída de credencial de acesso de saudação. |Não |

#### <a name="example-using-anonymous-authentication"></a>Exemplo: Usando a autenticação anônima

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a>Exemplo: Usando a autenticação do Windows

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do HDFS](#data-factory-hdfs-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados do HDFS, Olá conjunto **tipo** do conjunto de dados de saudação muito**FileShare**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| folderPath |Pasta de toohello de caminho. Exemplo: `myfolder`<br/><br/>Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres de saudação. Por exemplo: para pasta\subpasta, especifique a pasta\\\\subpasta e para d:\pastadeexemplo, especifique d:\\\\pastadeexemplo.<br/><br/>Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia datas / horas de início/término. |Sim |
| fileName |Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello. Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.<br/><br/>Quando o nome de arquivo não for especificado para um conjunto de dados de saída, o nome de saudação do arquivo hello gerado aparecerá em Olá esse formato a seguir: <br/><br/>Data<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Não |
| partitionedBy |partitionedBy pode ser usado toospecify um folderPath dinâmico, nome de arquivo para dados de série temporal. Exemplo: folderPath parametrizado para cada hora dos dados. |Não |
| formato | Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Saudação de conjunto **tipo** propriedade em formato tooone desses valores. Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída. |Não |
| compactação | Especifica tipo de saudação e nível de compactação de dados de saudação. Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. Os níveis com suporte são **Ideal** e **O mais rápido**. Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory). |Não |

> [!NOTE]
> filename e fileFilter não podem ser usados simultaneamente.

#### <a name="example"></a>Exemplo

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do HDFS](#data-factory-hdfs-connector.md#dataset-properties). 

### <a name="file-system-source-in-copy-activity"></a>Origem do Sistema de Arquivos na Atividade de Cópia
Se você estiver copiando dados do HDFS, defina Olá **tipo de fonte** de hello atividade de cópia muito**FileSystemSource**e especificar propriedades no Olá a seguir **fonte** seção:

**FileSystemSource** dá suporte a saudação propriedades a seguir:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| recursiva |Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello. |True, False (padrão) |Não |

#### <a name="example"></a>Exemplo

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Para obter mais informações, consulte o artigo [Conector do HDFS](#data-factory-hdfs-connector.md#copy-activity-properties).

## <a name="sftp"></a>SFTP


### <a name="linked-service"></a>Serviço vinculado
toodefine um SFTP vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**Sftp**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- | --- |
| host | Nome ou endereço IP do servidor SFTP hello. |Sim |
| porta |Porta na qual Olá SFTP server está escutando. valor padrão de saudação é: 21 |Não |
| authenticationType |Especifique o tipo de autenticação. Valores permitidos: **Básica**, **SshPublicKey**. <br><br> Consulte também[usando a autenticação básica](#using-basic-authentication) e [usando SSH autenticação de chave pública](#using-ssh-public-key-authentication) seções em mais propriedades e exemplos JSON, respectivamente. |Sim |
| skipHostKeyValidation | Especifique se tooskip validação de chave do host. | Não. Olá valor padrão: false |
| hostKeyFingerprint | Especifique a impressão digital de saudação da chave de host hello. | Sim se hello `skipHostKeyValidation` é definido toofalse.  |
| gatewayName |Nome da saudação Data Management Gateway tooconnect tooan local do servidor SFTP. | Sim se estiver copiando dados de um servidor SFTP local. |
| encryptedCredential | Servidor SFTP saudação do tooaccess credencial criptografada. Gerado automaticamente quando você especificar a autenticação básica (nome de usuário + senha) ou parâmetros SshPublicKey (nome de usuário + caminho da chave privado ou conteúdo) no diálogo de pop-up de ClickOnce de assistente ou saudação de cópia. | Não. Aplique somente quando estiver copiando dados de um servidor SFTP local. |

#### <a name="example-using-basic-authentication"></a>Exemplo: Usando a autenticação básica

Definir toouse a autenticação básica, `authenticationType` como `Basic`e especifique Olá seguintes propriedades além Olá conector SFTP genérico aqueles introduzidos na última seção do hello:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- | --- |
| Nome de Usuário | Usuário que possui o servidor do acesso toohello SFTP. |Sim |
| Senha | Senha do usuário da saudação (nome de usuário). | Sim |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Exemplo: Autenticação básica com credencial criptografada**

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a>Usando a autenticação de chave pública SSH:**

Definir toouse a autenticação básica, `authenticationType` como `SshPublicKey`e especifique Olá seguintes propriedades além Olá conector SFTP genérico aqueles introduzidos na última seção do hello:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- | --- |
| Nome de Usuário |Usuário que tem acesso toohello SFTP servidor |Sim |
| privateKeyPath | Especifique o caminho absoluto toohello arquivo de chave privada pode acessar o gateway. | Especifique a saudação `privateKeyPath` ou `privateKeyContent`. <br><br> Aplique somente quando estiver copiando dados de um servidor SFTP local. |
| privateKeyContent | Uma cadeia de caracteres serializada de conteúdo da chave privada hello. Olá Assistente para cópia pode ler o arquivo de chave privada hello e extrair o conteúdo da chave privada Olá automaticamente. Se você estiver usando qualquer outra ferramenta/SDK, use a propriedade de privateKeyPath de saudação em vez disso. | Especifique a saudação `privateKeyPath` ou `privateKeyContent`. |
| Senha | Especifique Olá senha/frase toodecrypt Olá privada chave de acesso de se o arquivo de chave Olá estiver protegido por uma frase secreta. | Sim, se o arquivo de chave privada Olá é protegido por uma frase secreta. |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Exemplo: autenticação de SshPublicKey usando o conteúdo da chave privada**

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do SFTP](data-factory-sftp-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados SFTP, Olá conjunto **tipo** do conjunto de dados de saudação muito**FileShare**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| folderPath |Subpasta toohello mais recente para o caminho. Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres de saudação. Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.<br/><br/>Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia datas / horas de início/término. |Sim |
| fileName |Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello. Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.<br/><br/>Quando o nome de arquivo não for especificado para um conjunto de dados de saída, o nome de saudação do arquivo hello gerado aparecerá em Olá esse formato a seguir: <br/><br/>Data.<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Não |
| fileFilter |Especifique um filtro toobe usado tooselect um subconjunto de arquivos no hello folderPath em vez de todos os arquivos.<br/><br/>Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).<br/><br/>Exemplo 1: `"fileFilter": "*.log"`<br/>Exemplo 2: `"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter é aplicável a um conjunto de dados FileShare de entrada. Essa propriedade não tem suporte com HDFS. |Não |
| partitionedBy |partitionedBy pode ser usado toospecify um folderPath dinâmico, nome de arquivo para dados de série temporal. Por exemplo, folderPath parametrizado para cada hora dos dados. |Não |
| formato | Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Saudação de conjunto **tipo** propriedade em formato tooone desses valores. Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída. |Não |
| compactação | Especifica tipo de saudação e nível de compactação de dados de saudação. Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. Os níveis com suporte são **Ideal** e **O mais rápido**. Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory). |Não |
| useBinaryTransfer |Especifique se deve usar o modo de transferência Binário. True para o modo binário e ASCII false. Valor padrão: True. Essa propriedade só pode ser usada quando o tipo de serviço vinculado associado for do tipo: FtpServer. |Não |

> [!NOTE]
> filename e fileFilter não podem ser usados simultaneamente.

#### <a name="example"></a>Exemplo

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do SFTP](data-factory-sftp-connector.md#dataset-properties). 

### <a name="file-system-source-in-copy-activity"></a>Origem do Sistema de Arquivos na Atividade de Cópia
Se você estiver copiando dados de uma fonte SFTP, defina Olá **tipo de fonte** de hello atividade de cópia muito**FileSystemSource**e especificar propriedades no Olá a seguir **fonte** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| recursiva |Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello. |True, False (padrão) |Não |



#### <a name="example"></a>Exemplo

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

Para obter mais informações, consulte o artigo [Conector do SFTP](data-factory-sftp-connector.md#copy-activity-properties).


## <a name="http"></a>HTTP

### <a name="linked-service"></a>Serviço vinculado
serviço saudação do conjunto vinculado do toodefine um HTTP **tipo** de saudação serviço vinculado muito**Http**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| url | Base de URL toohello servidor Web | Sim |
| authenticationType | Especifica o tipo de autenticação de saudação. Os valores permitidos são: **Anônimo**, **Básico**, **Digest**, **Windows** e **ClientCertificate**. <br><br> Consulte toosections abaixo da tabela em mais propriedades e exemplos JSON para esses tipos de autenticação, respectivamente. | Sim |
| enableServerCertificateValidation | Especifique se tooenable servidor SSL a validação de certificado se origem for o servidor da Web HTTPS | Não, o padrão é true |
| gatewayName | Nome da saudação Data Management Gateway tooconnect tooan origem HTTP no local. | Sim se estiver copiando dados de uma origem HTTP local. |
| encryptedCredential | Credencial criptografada tooaccess Olá ponto de extremidade HTTP. Gerado automaticamente quando você configura as informações de autenticação de saudação no diálogo de pop-up de ClickOnce de assistente ou saudação de cópia. | Não. Aplique somente quando estiver copiando dados de um servidor HTTP local. |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Exemplo: Usando a autenticação Básica, Digest ou Windows
Definir `authenticationType` como `Basic`, `Digest`, ou `Windows`e especifique Olá seguintes propriedades além Olá conector HTTP genérico aqueles introduzido acima:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| Nome de Usuário | Nome de usuário tooaccess Olá ponto de extremidade HTTP. | Sim |
| Senha | Senha do usuário da saudação (nome de usuário). | Sim |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a>Exemplo: Usando a autenticação ClientCertificate

Definir toouse a autenticação básica, `authenticationType` como `ClientCertificate`e especifique Olá seguintes propriedades além Olá conector HTTP genérico aqueles introduzido acima:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| embeddedCertData | conteúdo codificado com Base64 Olá de dados binários do arquivo de troca de informações pessoais (PFX) hello. | Especifique a saudação `embeddedCertData` ou `certThumbprint`. |
| certThumbprint | Olá a impressão digital do certificado Olá foi instalado no repositório de certificados do computador do gateway. Aplique somente ao copiar dados de uma origem HTTP local. | Especifique a saudação `embeddedCertData` ou `certThumbprint`. |
| Senha | Senha associada com o certificado de saudação. | Não |

Se você usar `certThumbprint` para certificado de autenticação e hello está instalado no repositório pessoal de saudação do computador local hello, você precisa que o serviço de gateway do toogrant Olá permissão de leitura toohello:

1. Iniciar o MMC (Console de Gerenciamento Microsoft). Adicionar Olá **certificados** snap-in que Olá destinos **computador Local**.
2. Expanda **Certificados**, **Pessoal** e clique em **Certificados**.
3. Certificado de saudação do armazenamento pessoal hello e selecione **todas as tarefas**->**gerenciar chaves particulares...**
3. Em Olá **segurança** guia, adicione a conta de usuário Olá sob a qual o serviço de Host do Gateway de gerenciamento de dados está em execução com certificado de toohello Olá acesso de leitura.  

**Exemplo: usando o certificado de cliente:** isso vinculado links serviço seu servidor de web data factory tooan locais HTTP. Ele usa um certificado de cliente é instalado na máquina de saudação com Gateway de gerenciamento de dados instalado.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>Exemplo: usando o certificado do cliente em um arquivo
Isso vinculado links serviço seu servidor de web data factory tooan locais HTTP. Ele usa um arquivo de certificado de cliente no computador de saudação com Gateway de gerenciamento de dados instalado.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do HTTP](data-factory-http-connector.md#linked-service-properties).

### <a name="dataset"></a>Conjunto de dados
toodefine um HTTP de conjunto de dados, conjunto Olá **tipo** do conjunto de dados de saudação muito**Http**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| relativeUrl | Um relativa URL toohello de recursos que contém dados de saudação. Quando não for especificado, somente URL Olá especificado na definição de serviço vinculada de saudação é usado. <br><br> URL do tooconstruct dinâmico, você pode usar [funções da fábrica de dados e variáveis de sistema](data-factory-functions-variables.md), exemplo: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`. | Não |
| requestMethod | Método Http. Os valores permitidos são **GET** ou **POST**. | Não. O padrão é `GET`. |
| additionalHeaders | Cabeçalhos de solicitação HTTP adicionais. | Não |
| requestBody | O corpo da solicitação HTTP. | Não |
| formato | Se você quiser toosimply **recuperar dados de saudação do ponto de extremidade HTTP como-é** sem analisá-lo, ignore essa configuração de formato. <br><br> Se você quiser resposta HTTP de saudação tooparse conteúdo durante a cópia, Olá tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). |Não |
| compactação | Especifica tipo de saudação e nível de compactação de dados de saudação. Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. Os níveis com suporte são **Ideal** e **O mais rápido**. Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory). |Não |

#### <a name="example-using-hello-get-default-method"></a>Exemplo: usando o método do hello GET (padrão)

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-hello-post-method"></a>Exemplo: usando o método POST de saudação

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
Para obter mais informações, consulte o artigo [Conector do HTTP](data-factory-http-connector.md#dataset-properties).

### <a name="http-source-in-copy-activity"></a>Origem do HTTP na Atividade de Cópia
Se você estiver copiando dados de uma fonte HTTP, defina Olá **tipo de fonte** de hello atividade de cópia muito**HttpSource**e especificar propriedades no Olá a seguir **fonte** seção:

| Propriedade | Descrição | Obrigatório |
| -------- | ----------- | -------- |
| httpRequestTimeout | Olá tempo limite (TimeSpan) para tooget de solicitação HTTP Olá uma resposta. É Olá timeout tooget uma resposta não Olá timeout tooread dados de resposta. | Não. Valor padrão: 00:01:40 |


#### <a name="example"></a>Exemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para obter mais informações, consulte o artigo [Conector do HTTP](data-factory-http-connector.md#copy-activity-properties).

## <a name="odata"></a>OData

### <a name="linked-service"></a>Serviço vinculado
toodefine OData vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OData**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| url |URL da saudação serviço OData. |Sim |
| authenticationType |Tipo de autenticação usado tooconnect toohello OData source. <br/><br/> Para o OData de nuvem, os valores possíveis são Anônimo, Básico e OAuth (observe que o Azure Data Factory dá suporte no momento apenas a OAuth baseado no Azure Active Directory). <br/><br/> Para OData local, os valores possíveis são Anonymous, Basic e Windows. |Sim |
| Nome de Usuário |Especifique o nome de usuário se você estiver usando a autenticação Básica. |Sim (apenas se você estiver usando a autenticação Básica) |
| Senha |Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação. |Sim (apenas se você estiver usando a autenticação Básica) |
| authorizedCredential |Se você estiver usando o OAuth, clique em **autorizar** botão no hello Assistente para cópia de fábrica de dados ou no Editor e insira suas credenciais, valor Olá dessa propriedade será gerado automaticamente. |Sim (apenas se você estiver usando a autenticação OAuth) |
| gatewayName |Nome do gateway Olá Olá serviço da fábrica de dados deve usar um serviço OData do tooconnect toohello local. Só especifique se você estiver copiando dados da fonte OData local. |Não |

#### <a name="example---using-basic-authentication"></a>Exemplo - Usando a autenticação básica
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a>Exemplo - Usando a autenticação anônima

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a>Exemplo - Usando a autenticação do Windows para acessar uma origem de OData local

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a>Exemplo - Usando autenticação OAuth para acessar a origem de OData da nuvem
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do OData](data-factory-odata-connector.md#linked-service-properties).

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados OData, Olá conjunto **tipo** do conjunto de dados de saudação muito**ODataResource**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| path |Caminho toohello recurso do OData |Não |

#### <a name="example"></a>Exemplo

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do OData](data-factory-odata-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Origem Relacional na Atividade de Cópia
Se você estiver copiando dados de uma fonte OData, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte** seção:

| Propriedade | Descrição | Exemplo | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |"?$select=Name, Description&$top=5" |Não |

#### <a name="example"></a>Exemplo

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

Para obter mais informações, consulte o artigo [Conector do OData](data-factory-odata-connector.md#copy-activity-properties).


## <a name="odbc"></a>ODBC


### <a name="linked-service"></a>Serviço vinculado
toodefine ODBC vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesOdbc**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| connectionString |Olá credencial de acesso não parte de cadeia de caracteres de conexão hello e opcional criptografados credencial. Consulte exemplos Olá seções a seguir. |Sim |
| credencial |parte de credencial de acesso Olá de cadeia de caracteres de conexão de saudação especificada no formato de valor de propriedade específica do driver. Exemplo: "Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;". |Não |
| authenticationType |Tipo de autenticação usado o repositório de dados ODBC tooconnect toohello. Os valores possíveis são: Anonymous e Basic. |Sim |
| Nome de Usuário |Especifique o nome de usuário se você estiver usando a autenticação Básica. |Não |
| Senha |Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação. |Não |
| gatewayName |Nome do gateway Olá Olá serviço da fábrica de dados deve usar armazenamento de dados ODBC tooconnect toohello. |Sim |

#### <a name="example---using-basic-authentication"></a>Exemplo - Usando a autenticação básica

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a>Exemplo - Usando a autenticação básica com credenciais criptografadas
Você pode criptografar credenciais Olá Olá [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (1.0 versão do Azure PowerShell) ou [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 versão ou anterior do hello PowerShell do Azure).  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a>Exemplo: Usando a autenticação anônima

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do ODBC](data-factory-odbc-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados ODBC, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação no repositório de dados ODBC hello. |Sim |


#### <a name="example"></a>Exemplo

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do ODBC](data-factory-odbc-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origem Relacional na Atividade de Cópia
Se você estiver copiando dados de um repositório de dados ODBC, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: `select * from MyTable`. |Sim |

#### <a name="example"></a>Exemplo

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

Para obter mais informações, consulte o artigo [Conector do ODBC](data-factory-odbc-connector.md#copy-activity-properties).

## <a name="salesforce"></a>Salesforce


### <a name="linked-service"></a>Serviço vinculado
toodefine Salesforce o serviço saudação do conjunto vinculado **tipo** de saudação serviço vinculado muito**Salesforce**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| environmentUrl | Especifique a instância de URL da equipe de vendas de saudação. <br><br> – O padrão é "https://login.salesforce.com". <br> -toocopy dados de área restrita, especifique "https://test.salesforce.com". <br> -toocopy dados do domínio personalizado, especificar, por exemplo, "https://[domain].my.salesforce.com". |Não |
| Nome de Usuário |Especifique um nome de usuário para a conta de usuário de saudação. |Sim |
| Senha |Especifique uma senha para a conta de usuário de saudação. |Sim |
| securityToken |Especifique um token de segurança para a conta de usuário de saudação. Consulte [obter token de segurança](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para obter instruções sobre como tooreset/obter um token de segurança. em geral, consulte toolearn sobre tokens de segurança [API de segurança e hello](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Sim |

#### <a name="example"></a>Exemplo

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector da Salesforce](data-factory-salesforce-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados do Salesforce, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação na equipe de vendas. |Não (se uma **consulta** de **RelationalSource** for especificada) |

#### <a name="example"></a>Exemplo

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector da Salesforce](data-factory-salesforce-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Origem Relacional na Atividade de Cópia
Se você estiver copiando dados do Salesforce, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| query |Use dados de tooread Olá consulta personalizada. |Uma consulta SQL-92 ou uma consulta [SOQL (Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm). Por exemplo: `select * from MyTable__c`. |Não (se hello **tableName** de saudação **dataset** for especificado) |

#### <a name="example"></a>Exemplo  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> parte "__c" Olá Olá nome da API é necessária para qualquer objeto personalizado.

Para obter mais informações, consulte o artigo [Conector da Salesforce](data-factory-salesforce-connector.md#copy-activity-properties). 

## <a name="web-data"></a>Dados da Web 

### <a name="linked-service"></a>Serviço vinculado
toodefine uma Web vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**Web**e especificar propriedades no Olá a seguir **typeProperties** seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| Url |Origem da URL toohello da Web |Sim |
| authenticationType |Anônima. |Sim |
 

#### <a name="example"></a>Exemplo


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector da Tabela da Web](data-factory-web-table-connector.md#linked-service-properties). 

### <a name="dataset"></a>Conjunto de dados
toodefine um conjunto de dados da Web, Olá conjunto **tipo** do conjunto de dados de saudação muito**WebTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção: 

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| type |Tipo de conjunto de dados de saudação. deve ser definido muito**WebTable** |Sim |
| path |Um relativa URL toohello de recursos que contém a tabela de saudação. |Não. Quando não for especificado, somente URL Olá especificado na definição de serviço vinculada de saudação é usado. |
| índice |índice de saudação da tabela de saudação no recurso de saudação. Consulte [índice de obtenção de uma tabela em uma página HTML](#get-index-of-a-table-in-an-html-page) seção de índice de toogetting de etapas de uma tabela em uma página HTML. |Sim |

#### <a name="example"></a>Exemplo

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector da Tabela da Web](data-factory-web-table-connector.md#dataset-properties). 

### <a name="web-source-in-copy-activity"></a>Origem da Web na Atividade de Cópia
Se você estiver copiando dados de uma tabela da web, defina Olá **tipo de fonte** de hello atividade de cópia muito**WebSource**. Atualmente, quando a fonte de saudação na atividade de cópia é do tipo **WebSource**, sem propriedades adicionais são suportadas.

#### <a name="example"></a>Exemplo

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Para obter mais informações, consulte o artigo [Conector da Tabela da Web](data-factory-web-table-connector.md#copy-activity-properties). 

## <a name="compute-environments"></a>AMBIENTES DE COMPUTAÇÃO
Olá tabela a seguir lista os ambientes de computação de saudação suportados por Data Factory e hello atividades de transformação que podem ser executados neles. Clique Olá link para a computação Olá você está interessado em esquemas JSON toosee Olá para o serviço vinculado toolink-tooa fábrica de dados. 

| Ambiente de computação | Atividades |
| --- | --- |
| [Cluster HDInsight sob demanda](#on-demand-azure-hdinsight-cluster) ou [seu próprio cluster HDInsight](#existing-azure-hdinsight-cluster) |[Atividade personalizada de .NET](#net-custom-activity), [Atividade de Hive](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [Atividade de MapReduce](#hdinsight-mapreduce-activity), [Atividade de transmissão do Hadoop](#hdinsight-streaming-activityd), [Atividade do Spark](#hdinsight-spark-activity) |
| [Lote do Azure](#azure-batch) |[Atividade personalizada do .NET](#net-custom-activity) |
| 
            [Azure Machine Learning](#azure-machine-learning) | [Atividade de Execução de Lote de Machine Learning](#machine-learning-batch-execution-activity), [Atividade de Atualização de Recursos de Machine Learning](#machine-learning-update-resource-activity) |
| [Análise Azure Data Lake](#azure-data-lake-analytics) |[U-SQL da Análise Data Lake](#data-lake-analytics-u-sql-activity) |
| [Banco de Dados SQL do Azure](#azure-sql-database-1), [SQL Data Warehouse do Azure](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1) |[Procedimento armazenado](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a>Cluster HDInsight do Azure sob demanda
Olá serviço fábrica de dados do Azure pode criar automaticamente um dados sob demanda baseados no Windows/Linux de tooprocess de cluster HDInsight. Olá cluster é criado no hello mesma região da conta de armazenamento da saudação (propriedade linkedServiceName em JSON de saudação) associado com cluster hello. Você pode executar Olá seguintes atividades de transformação nesse serviço vinculado: [atividade personalizada do .NET](#net-custom-activity), [atividade de Hive](#hdinsight-hive-activity), [atividade de Pig] (#-pig-atividade de hdinsight, [atividade MapReduce ](#hdinsight-mapreduce-activity), [Hadoop streaming atividade](#hdinsight-streaming-activityd), [despertar atividade](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Serviço vinculado 
Olá, a tabela a seguir fornece descrições para propriedades de saudação usadas na definição do hello Azure JSON de um serviço de vinculado do HDInsight sob demanda.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade do tipo Hello deve ser definida muito**HDInsightOnDemand**. |Sim |
| clusterSize |Número de nós de dados do trabalhador em cluster hello. cluster do HDInsight Olá é criado com 2 nós de cabeçalho junto com o número de saudação de nós de trabalho que você especifica para esta propriedade. nós Olá são de tamanho Standard_D3 que tem 4 núcleos, assim, um cluster de nó do 4 operador leva 24 núcleos (4\*4 = 16 núcleos para nós de trabalho, mais 2\*4 = 8 núcleos para nós de cabeçalho). Consulte [Hadoop baseado em Linux criar clusters de HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) para obter detalhes sobre a camada de saudação Standard_D3. |Sim |
| timeToLive |Olá permitido tempo ocioso do cluster do HDInsight sob demanda hello. Especifica quanto tempo cluster do HDInsight sob demanda Olá permanece ativo após a conclusão de uma atividade executar se não houver nenhum outro trabalho ativo no cluster hello.<br/><br/>Por exemplo, se uma atividade executar levar 6 minutos e timetolive é definir too5 minutos, Olá cluster permanece ativo por 5 minutos após a saudação 6 minutos de processamento de execução da atividade hello. Se outra execução da atividade é executada com uma janela de 6 minutos hello, ela é processada pelo Olá mesmo cluster.<br/><br/>A criação de um cluster do HDInsight sob demanda é uma operação cara (pode demorar um pouco), então use essa configuração como desempenho tooimprove necessários de uma fábrica de dados com a reutilização de um cluster do HDInsight sob demanda.<br/><br/>Se você definir timetolive valor too0, cluster Olá é excluído, assim como hello atividade executada em processados. Em Olá outro lado, se você definir um valor alto, cluster Olá pode permanecer ocioso desnecessariamente, resultando em altos custos. Portanto, é importante que você defina o valor apropriado de saudação com base em suas necessidades.<br/><br/>Vários pipelines podem compartilhar Olá a mesma instância de cluster do HDInsight sob demanda Olá se o valor da propriedade timetolive hello está definido corretamente |Sim |
| version |Versão do cluster do HDInsight hello. Para obter detalhes, confira [Versões com suporte do HDInsight no Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). |Não |
| linkedServiceName |Armazenamento do Azure vinculada toobe de serviço usado pelo cluster sob demanda de saudação para armazenar e processar dados. <p>No momento, você não pode criar um cluster HDInsight sob demanda que usa um repositório Azure Data Lake como armazenamento hello. Se desejar que os dados de resultado de saudação toostore do HDInsight de processamento em um repositório Azure Data Lake, use um atividade de cópia toocopy Olá os dados de armazenamento de BLOBs do Azure de saudação toohello repositório Azure Data Lake.</p>  | Sim |
| additionalLinkedServiceNames |Especifica o serviço vinculado de contas de armazenamento adicionais para Olá HDInsight para que o serviço do Data Factory Olá pode registrá-los em seu nome. |Não |
| osType |Tipo do sistema operacional. Valores permitidos são: Windows (padrão) e Linux |Não |
| hcatalogLinkedServiceName |nome de saudação do vinculado do SQL Azure ponto toohello HCatalog banco de dados do serviço. cluster do HDInsight sob demanda Olá é criado usando o banco de dados do SQL Azure hello como Olá metastore. |Não |

### <a name="json-example"></a>Exemplo de JSON
Olá JSON a seguir define um serviço vinculado do HDInsight de sob demanda com base em Linux. Olá serviço da fábrica de dados cria automaticamente um **baseados em Linux** cluster HDInsight durante o processamento de uma fatia de dados. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Serviços vinculados de computação](data-factory-compute-linked-services.md). 

## <a name="existing-azure-hdinsight-cluster"></a>Cluster Azure HDInsight existente
Você pode criar um tooregister de serviço vinculado do Azure HDInsight seu próprio cluster HDInsight com a fábrica de dados. Você pode executar Olá atividades de transformação de dados a seguir sobre esse serviço vinculado: [atividade personalizada do .NET](#net-custom-activity), [atividade de Hive](#hdinsight-hive-activity), [atividade de Pig] (#-pig-atividade de hdinsight, [MapReduce atividade](#hdinsight-mapreduce-activity), [Hadoop streaming atividade](#hdinsight-streaming-activityd), [despertar atividade](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Serviço vinculado
Olá, a tabela a seguir fornece descrições para propriedades de saudação usadas na definição do hello Azure JSON de um serviço vinculado do HDInsight do Azure.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade do tipo Hello deve ser definida muito**HDInsight**. |Sim |
| clusterUri |Olá URI do cluster do HDInsight hello. |Sim |
| Nome de Usuário |Especifique o nome Olá Olá usuário toobe usado cluster do HDInsight tooconnect tooan existente. |Sim |
| Senha |Especifique a senha da conta de usuário de saudação. |Sim |
| linkedServiceName | Nome do serviço vinculado do armazenamento do Azure que se refere o armazenamento de BLOBs do Azure toohello de saudação usado por Olá cluster HDInsight. <p>No momento, você não pode especificar um serviço vinculado do Azure Data Lake Store para essa propriedade. Você pode acessar dados em Olá repositório Azure Data Lake de scripts de Pig/Hive se o cluster do HDInsight Olá tem acesso toohello repositório Data Lake. </p>  |Sim |

Para conferir as versões de clusters HDInsight com suporte, veja [Versões do HDInsight com suporte](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). 

#### <a name="json-example"></a>Exemplo de JSON

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a>Lote do Azure
Você pode criar um pool de lote de máquinas virtuais (VMs) de um tooregister de serviço vinculado do Azure Batch com uma fábrica de dados. Você pode executar atividades personalizadas do .NET usando o Lote do Azure ou o Azure HDInsight. Você pode executar uma [atividade personalizada do .NET](#net-custom-activity) neste serviço vinculado. 

### <a name="linked-service"></a>Serviço vinculado
Olá, a tabela a seguir fornece descrições para propriedades de saudação usadas na definição do hello Azure JSON de um serviço vinculado do Azure Batch.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade do tipo Hello deve ser definida muito**AzureBatch**. |Sim |
| accountName |Nome da saudação conta de lote do Azure. |Sim |
| accessKey |Chave de acesso para Olá conta de lote do Azure. |Sim |
| poolName |Nome do pool de saudação de máquinas virtuais. |Sim |
| linkedServiceName |Nome do serviço vinculado do armazenamento do Azure associada ao serviço vinculado do Azure Batch de saudação. Esse serviço vinculado é usado para arquivos de teste toorun atividade de saudação e armazenar os logs de execução de atividade Olá necessários. |Sim |


#### <a name="json-example"></a>Exemplo de JSON

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a>Azure Machine Learning
Você cria um tooregister de serviço vinculado do aprendizado de máquina do Azure para um ponto de extremidade com uma fábrica de dados de pontuação do lote de aprendizado de máquina. Duas atividades de transformação de dados podem ser executadas neste serviço vinculado: [Atividade de Execução de Lote de Machine Learning](#machine-learning-batch-execution-activity), [Atividade de Atualização de Recursos de Machine Learning](#machine-learning-update-resource-activity). 

### <a name="linked-service"></a>Serviço vinculado
Olá, a tabela a seguir fornece descrições para propriedades de saudação usadas na definição do hello Azure JSON de um serviço vinculado do aprendizado de máquina do Azure.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| Tipo |propriedade de tipo Hello deve ser definida como: **AzureML**. |Sim |
| mlEndpoint |URL de pontuação de lote de saudação. |Sim |
| apiKey |Olá publicados API do modelo de espaço de trabalho. |Sim |

#### <a name="json-example"></a>Exemplo de JSON

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a>Análise Azure Data Lake
Você cria um **análise Azure Data Lake** vinculado serviço toolink uma análise do Azure Data Lake computação serviço tooan data factory do Azure antes de usar o hello [atividade U-SQL do Data Lake análise](data-factory-usql-activity.md) em um pipeline .

### <a name="linked-service"></a>Serviço vinculado

Olá, a tabela a seguir fornece descrições para propriedades de saudação usadas na definição de JSON de saudação de um serviço vinculado de análise do Azure Data Lake. 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| Tipo |propriedade de tipo Hello deve ser definida como: **AzureDataLakeAnalytics**. |Sim |
| accountName |Nome da conta da Análise Azure Data Lake. |Sim |
| dataLakeAnalyticsUri |URI da Análise Azure Data Lake. |Não |
| autorização |Código de autorização é recuperado automaticamente depois de clicar em **autorizar** botão hello Editor da fábrica de dados e logon do OAuth Olá concluído. |Sim |
| subscriptionId |Id de assinatura do Azure |Não (se não especificado, a assinatura de saudação fábrica de dados é usada). |
| resourceGroupName |Nome do grupo de recursos do Azure |Não (se não especificado, o grupo de recursos de saudação fábrica de dados é usada). |
| sessionId |id de sessão da sessão de autorização de OAuth hello. Cada ID da sessão é exclusiva e pode ser usado somente uma vez. Quando você usa Olá Editor da fábrica de dados, essa ID é gerada automaticamente. |Sim |


#### <a name="json-example"></a>Exemplo de JSON
saudação de exemplo a seguir fornece a definição de JSON para um serviço vinculado de análise do Azure Data Lake.

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a>Banco de Dados SQL do Azure
Criar um serviço vinculado do SQL Azure e usá-lo com hello [atividade de procedimento armazenado](#stored-procedure-activity) tooinvoke um procedimento armazenado de um pipeline da fábrica de dados. 

### <a name="linked-service"></a>Serviço vinculado
toodefine um banco de dados do SQL Azure vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AzureSqlDatabase**e especificar propriedades no Olá a seguir **typeProperties**seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| connectionString |Especifique informações necessárias a instância de banco de dados do Azure SQL toohello tooconnect para a propriedade connectionString de saudação. |Sim |

#### <a name="json-example"></a>Exemplo de JSON

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Confira o artigo [Conector SQL do Azure](data-factory-azure-sql-connector.md#linked-service-properties) para saber mais sobre esse serviço vinculado.

## <a name="azure-sql-data-warehouse"></a>SQL Data Warehouse do Azure
Criar um serviço vinculado do Azure SQL Data Warehouse e usá-lo com hello [atividade de procedimento armazenado](data-factory-stored-proc-activity.md) tooinvoke um procedimento armazenado de um pipeline da fábrica de dados. 

### <a name="linked-service"></a>Serviço vinculado
toodefine um Azure SQL Data Warehouse vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AzureSqlDW**e especificar propriedades no Olá a seguir **typeProperties**seção:  

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| connectionString |Especifique informações necessárias a instância do tooconnect toohello Azure SQL Data Warehouse para a propriedade connectionString de saudação. |Sim |

#### <a name="json-example"></a>Exemplo de JSON

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector do SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties). 

## <a name="sql-server"></a>SQL Server 
Criar um serviço vinculado do SQL Server e usá-lo com hello [atividade de procedimento armazenado](data-factory-stored-proc-activity.md) tooinvoke um procedimento armazenado de um pipeline da fábrica de dados. 

### <a name="linked-service"></a>Serviço vinculado
Criar um serviço vinculado do tipo **OnPremisesSqlServer** toolink uma fábrica de dados tooa de banco de dados do local do SQL Server. Olá a tabela a seguir fornece uma descrição para o serviço vinculado do SQL Server do JSON elementos tooon local específico.

Olá, a tabela a seguir fornece uma descrição para o JSON de elementos específico tooSQL serviço do servidor vinculado.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **OnPremisesSqlServer**. |Sim |
| connectionString |Especifica informações de connectionString necessárias tooconnect toohello no SQL Server banco de dados local usando a autenticação do Windows ou autenticação do SQL. |Sim |
| gatewayName |Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello no local do SQL Server. |Sim |
| Nome de Usuário |Especifique o nome de usuário se você estiver usando a Autenticação do Windows. Exemplo: **domainname\\username**. |Não |
| Senha |Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação. |Não |

Você pode criptografar credenciais usando Olá **New-AzureRmDataFactoryEncryptValue** cmdlet e usá-los na cadeia de caracteres de conexão hello, conforme mostrado no exemplo a seguir de saudação (**EncryptedCredential** propriedade):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Exemplo: JSON para usar Autenticação SQL

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Exemplo: JSON para usar Autenticação Windows

Se o nome de usuário e senha forem especificados, gateway usa tooimpersonate Olá dados do usuário especificado conta tooconnect toohello local do SQL Server. Caso contrário, o gateway conecta toohello do SQL Server diretamente com o contexto de segurança de saudação do Gateway (sua conta de inicialização).

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Para obter mais informações, consulte o artigo [Conector de SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).

## <a name="data-transformation-activities"></a>ATIVIDADES DE TRANSFORMAÇÃO DE DADOS

Atividade | Descrição
-------- | -----------
[Atividade de Hive do HDInsight](#hdinsight-hive-activity) | Hello atividade Hive do HDInsight em um pipeline da fábrica de dados executa consultas de Hive por conta própria ou cluster do HDInsight baseados no Windows/Linux sob demanda. 
[Atividade de Pig do HDInsight](#hdinsight-pig-activity) | Hello atividade de Pig de HDInsight em um pipeline da fábrica de dados executa consultas de Pig por conta própria ou cluster do HDInsight baseados no Windows/Linux sob demanda.
[Atividade de MapReduce do HDInsight](#hdinsight-mapreduce-activity) | Hello atividade MapReduce do HDInsight em um pipeline da fábrica de dados executa programas de MapReduce por conta própria ou cluster do HDInsight baseados no Windows/Linux sob demanda.
[Atividade de Streaming do HDInsight](#hdinsight-streaming-activity) | Hello atividade de transmissão do HDInsight em um pipeline da fábrica de dados executa programas de transmissão do Hadoop por conta própria ou cluster do HDInsight baseados no Windows/Linux sob demanda.
[Atividade do HDInsight Spark](#hdinsight-spark-activity) | Hello atividade de HDInsight Spark em um pipeline da fábrica de dados executa programas Spark no seu próprio cluster HDInsight. 
[Atividade de Execução em Lote do Machine Learning](#machine-learning-batch-execution-activity) | Habilita de fábrica de dados do Azure tooeasily você criar pipelines que usam o aprendizado de máquina publicado web service para análise preditiva. Usando hello atividade de execução em lote em um pipeline da fábrica de dados do Azure, você pode invocar um toomake previsões do aprendizado de máquina web serviço nos dados de saudação em lote. 
[Atividade do Recurso de Atualização do Machine Learning](#machine-learning-update-resource-activity) | Ao longo do tempo, modelos de previsão de saudação em Olá aprendizado de máquina experiências de pontuação necessário toobe treinados novamente usando novos conjuntos de dados de entrada. Depois que você treinamento, você deseja tooupdate Olá pontuação serviço web com hello treinados novamente o modelo de aprendizado de máquina. Você pode usar o hello serviço web do atividade do recurso de atualização tooupdate Olá com modelo Olá recentemente treinado.
[Atividade de Procedimento Armazenado](#stored-procedure-activity) | Você pode usar a atividade de procedimento armazenado de saudação em um pipeline de fábrica de dados tooinvoke um procedimento armazenado em uma saudação armazenamentos de dados a seguir: Azure SQL Database, Azure SQL Data Warehouse, banco de dados do SQL Server em sua empresa ou de uma VM do Azure. 
[Atividade de U-SQL do Data Lake Analytics](#data-lake-analytics-u-sql-activity) | A atividade de U-SQL do Data Lake Analytics executa um script U-SQL em um cluster do Azure Data Lake Analytics.  
[Atividade personalizada do .NET](#net-custom-activity) | Se você precisar tootransform dados de forma que não é suportada pela fábrica de dados, você pode criar uma atividade personalizada com sua própria lógica de processamento de dados e usar atividade Olá no pipeline de saudação. Você pode configurar Olá personalizado .NET atividade toorun usando um serviço de lote do Azure ou um cluster Azure HDInsight. 

     
## <a name="hdinsight-hive-activity"></a>Atividade de Hive do HDInsight
Você pode especificar Olá seguintes propriedades em uma definição de JSON da atividade de Hive. a propriedade de tipo Hello atividade Olá deve ser: **HDInsightHive**. Você deve primeiro criar um serviço vinculado do HDInsight e especificar o nome de saudação-lo como um valor para Olá **linkedServiceName** propriedade. Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooHDInsightHive de atividade:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| script |Especifique o script de Hive Olá embutido |Não |
| caminho do script |Saudação de repositório Hive script em um armazenamento de BLOBs do Azure e fornecer Olá caminho toohello arquivo. Use a propriedade 'script' ou 'scriptPath'. As duas não podem ser usadas juntas. nome do arquivo Hello diferencia maiusculas de minúsculas. |Não |
| define |Especifique parâmetros como pares chave/valor para fazer referência a no script do Hive hello usando 'hiveconf' |Não |

Essas propriedades de tipo são específico toohello atividade de Hive. Há suporte para todas as atividades de outras propriedades (fora de saudação typeProperties seção).   

### <a name="json-example"></a>Exemplo de JSON
Olá JSON a seguir define uma atividade de HDInsight Hive em um pipeline.  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

Para saber mais, consulte o artigo [Atividade de Hive](data-factory-hive-activity.md). 

## <a name="hdinsight-pig-activity"></a>Atividade de Pig do HDInsight
Você pode especificar Olá seguintes propriedades em uma definição de JSON da atividade de Pig. a propriedade de tipo Hello atividade Olá deve ser: **HDInsightPig**. Você deve primeiro criar um serviço vinculado do HDInsight e especificar o nome de saudação-lo como um valor para Olá **linkedServiceName** propriedade. Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooHDInsightPig de atividade: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| script |Especificar Olá Pig script embutido |Não |
| caminho do script |Armazenar o script de Pig de saudação em um armazenamento de BLOBs do Azure e fornecer Olá caminho toohello arquivo. Use a propriedade 'script' ou 'scriptPath'. As duas não podem ser usadas juntas. nome do arquivo Hello diferencia maiusculas de minúsculas. |Não |
| define |Especifique parâmetros como pares chave/valor para fazer referência a no script de Pig de saudação |Não |

Essas propriedades de tipo são específico toohello atividade de Pig. Há suporte para todas as atividades de outras propriedades (fora de saudação typeProperties seção).   

### <a name="json-example"></a>Exemplo de JSON

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

Para saber mais, consulte o artigo [Atividade de Pig](#data-factory-pig-activity.md). 

## <a name="hdinsight-mapreduce-activity"></a>Atividade de MapReduce do HDInsight
Você pode especificar Olá seguintes propriedades em uma definição de JSON da atividade MapReduce. a propriedade de tipo Hello atividade Olá deve ser: **HDInsightMapReduce**. Você deve primeiro criar um serviço vinculado do HDInsight e especificar o nome de saudação-lo como um valor para Olá **linkedServiceName** propriedade. Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooHDInsightMapReduce de atividade: 

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| jarLinkedService | Nome do hello vinculado de serviço para Olá armazenamento do Azure que contém o arquivo JAR de saudação. | Sim |
| jarFilePath | Caminho toohello JAR arquivo no armazenamento do Azure de saudação. | Sim | 
| className | Nome da classe principal do hello no arquivo JAR de saudação. | Sim | 
| argumentos | Uma lista de argumentos separados por vírgulas para programas de MapReduce hello. Em tempo de execução, você ver alguns argumentos adicionais (por exemplo: mapreduce.job.tags) da estrutura de MapReduce hello. toodifferentiate seus argumentos com argumentos de MapReduce hello, considere o uso de opção e valor como argumentos conforme mostrado no exemplo a seguir de saudação (- s, - entrada, --saída etc., são imediatamente seguidas por seus valores de opções) | Não | 

### <a name="json-example"></a>Exemplo de JSON

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

Para saber mais, consulte o artigo [Atividade MapReduce](data-factory-map-reduce.md). 

## <a name="hdinsight-streaming-activity"></a>Atividade de Streaming do HDInsight
Você pode especificar Olá seguintes propriedades em uma definição de Hadoop Streaming JSON da atividade. a propriedade de tipo Hello atividade Olá deve ser: **HDInsightStreaming**. Você deve primeiro criar um serviço vinculado do HDInsight e especificar o nome de saudação-lo como um valor para Olá **linkedServiceName** propriedade. Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooHDInsightStreaming de atividade: 

| Propriedade | Descrição | 
| --- | --- |
| mapper | Nome do executável do mapeador de saudação. Exemplo hello, cat.exe é executável do mapeador de saudação.| 
| reducer | Nome de saudação do executável do Redutor. Exemplo hello, wc.exe é Redutor de saudação executável. | 
| input | Arquivo de entrada (incluindo local) para o mapeador de saudação. No exemplo hello: "wasb<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample é o contêiner de blob hello, example/data/Gutenberg é a pasta de saudação e davinci.txt é Olá blob. |
| output | Arquivo de saída (incluindo local) para Redutor hello. saída de saudação do trabalho de transmissão do Hadoop Olá é gravada toohello local especificado para esta propriedade. |
| filePaths | Caminhos para executáveis do mapeador e Redutor hello. No exemplo hello: "adfsample/example/apps/wc.exe", adfsample é o contêiner de blob hello, example/apps é a pasta hello e wc.exe é hello executável. | 
| fileLinkedService | Serviço vinculado do armazenamento do Azure que representa Olá armazenamento do Azure que contém arquivos de saudação especificados na seção de filePaths hello. | 
| argumentos | Uma lista de argumentos separados por vírgulas para programas de MapReduce hello. Em tempo de execução, você ver alguns argumentos adicionais (por exemplo: mapreduce.job.tags) da estrutura de MapReduce hello. toodifferentiate seus argumentos com argumentos de MapReduce hello, considere o uso de opção e valor como argumentos conforme mostrado no exemplo a seguir de saudação (- s, - entrada, --saída etc., são imediatamente seguidas por seus valores de opções) | 
| getDebugInfo | Um elemento opcional. Quando estiver definido como tooFailure, Olá logs são baixadas apenas em caso de falha. Quando estiver definido como tooAll, logs são sempre baixados independentemente do status de execução de saudação. | 

> [!NOTE]
> Você deve especificar um conjunto de dados de saída para hello Hadoop Streaming Activity para Olá **gera** propriedade. Este conjunto de dados pode ser um dataset fictício que é necessário toodrive Olá pipeline agenda (por hora, diariamente, etc.). Se a atividade de saudação não tem uma entrada, você pode ignorar especificando um conjunto de dados de entrada para a atividade de saudação para Olá **entradas** propriedade.  

## <a name="json-example"></a>Exemplo de JSON

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

Para saber mais, consulte o artigo [Atividade de Transmissão do Hadoop](data-factory-hadoop-streaming-activity.md). 

## <a name="hdinsight-spark-activity"></a>Atividade do HDInsight Spark
Você pode especificar Olá seguintes propriedades em uma definição de JSON da atividade Spark. a propriedade de tipo Hello atividade Olá deve ser: **HDInsightSpark**. Você deve primeiro criar um serviço vinculado do HDInsight e especificar o nome de saudação-lo como um valor para Olá **linkedServiceName** propriedade. Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooHDInsightSpark de atividade: 

| Propriedade | Descrição | Obrigatório |
| -------- | ----------- | -------- |
| rootPath | contêiner de BLOBs do Azure Hello e pasta que contém o arquivo do Spark hello. nome do arquivo Hello diferencia maiusculas de minúsculas. | Sim |
| entryFilePath | Pasta de raiz de toohello de caminho relativo da saudação Spark/pacote de código. | Sim |
| className | Classe principal de Java/Spark do aplicativo | Não | 
| argumentos | Uma lista de programas de Spark toohello argumentos de linha de comando. | Não | 
| proxyUser | programa de saudação usuário conta tooimpersonate tooexecute Olá Spark | Não | 
| sparkConfig | Propriedades de configuração do Spark. | Não | 
| getDebugInfo | Especifica quando arquivos de log do Spark Olá são copiado toohello usado pelo cluster do HDInsight de armazenamento do Azure (ou) especificado por sparkJobLinkedService. Valores permitidos: Nenhum, Sempre ou Falha. Valor padrão: Nenhum. | Não | 
| sparkJobLinkedService | Olá serviço vinculado do armazenamento do Azure que contém o arquivo de trabalho do Spark hello, dependências e logs.  Se você não especificar um valor para essa propriedade, armazenamento de saudação associado com o cluster HDInsight é usado. | Não |

### <a name="json-example"></a>Exemplo de JSON

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
Observe Olá pontos a seguir: 

- Olá **tipo** propriedade for definida muito**HDInsightSpark**.
- Olá **rootPath** está definido muito**adfspark\\pyFiles** onde adfspark é o contêiner de BLOBs do Azure hello e pyFiles é a pasta bem no contêiner. Neste exemplo, Olá armazenamento de BLOBs do Azure é hello que está associado ao cluster do Spark hello. Você pode carregar Olá arquivo tooa armazenamento do Azure diferente. Se você fizer isso, crie um toolink de serviço vinculado do armazenamento do Azure essa fábrica de dados de toohello de conta de armazenamento. Em seguida, especifique o nome de Olá de serviço de Olá vinculado como um valor para Olá **sparkJobLinkedService** propriedade. Consulte [propriedades da atividade Spark](#spark-activity-properties) para obter detalhes sobre essa propriedade e outras propriedades com suporte hello atividade Spark.
- Olá **entryFilePath** está definida toohello **test.py**, que é o arquivo de python hello. 
- Olá **getDebugInfo** propriedade for definida muito**sempre**, que significa que os arquivos de log Olá sempre são gerados (sucesso ou falha).  

    > [!IMPORTANT]
    > É recomendável que você não defina essa propriedade tooAlways em um ambiente de produção, a menos que você estiver solucionando um problema. 
- Olá **gera** seção tem um conjunto de dados de saída. Você deve especificar um conjunto de dados de saída, mesmo que o programa de spark Olá não produz nenhuma saída. Olá dataset unidades Olá agenda para o pipeline de saudação (por hora, diariamente, etc.).

Para obter mais informações sobre a atividade de hello, consulte [Spark atividade](data-factory-spark.md) artigo.  

## <a name="machine-learning-batch-execution-activity"></a>Atividade de Execução em Lote de Machine Learning
Você pode especificar Olá seguintes propriedades em uma definição de JSON da atividade de execução em lote do Azure ML. a propriedade de tipo Hello atividade Olá deve ser: **AzureMLBatchExecution**. Você deve criar uma primeiro o serviço vinculado de aprendizado de máquina do Azure e especificar o nome de Olá-lo como um valor para Olá **linkedServiceName** propriedade. Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooAzureMLBatchExecution de atividade:

Propriedade | Descrição | Obrigatório 
-------- | ----------- | --------
webServiceInput | Olá dataset toobe passado como entrada para Olá serviço de web do ML do Azure. Este conjunto de dados também deve ser incluído em entradas de saudação para atividade de saudação. |Use webServiceInput ou webServiceInputs. | 
webServiceInputs | Especifique toobe de conjuntos de dados passadas como entradas para Olá serviço de web do ML do Azure. Se o serviço web de saudação pega várias entradas, use a propriedade de webServiceInputs de saudação em vez de usar a propriedade de webServiceInput hello. Conjuntos de dados que são referenciados por Olá **webServiceInputs** também deve ser incluído no hello atividade **entradas**. | Use webServiceInput ou webServiceInputs. | 
webServiceOutputs | Olá conjuntos de dados que são atribuídos como saídas para serviço de web hello ML do Azure. Olá web service retorna dados de saída neste conjunto de dados. | Sim | 
globalParameters | Especifica valores para parâmetros de serviço da web hello nesta seção. | Não | 

### <a name="json-example"></a>Exemplo de JSON
Neste exemplo, a atividade de saudação tem Olá dataset **MLSqlInput** como entrada e **MLSqlOutput** como saída de hello. Olá **MLSqlInput** é passado como um serviço web de entrada toohello por usando Olá **webServiceInput** propriedade JSON. Olá **MLSqlOutput** é passado como um serviço de Web saída toohello por usando Olá **webserviceoutputs na** propriedade JSON. 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

No exemplo JSON hello, Olá implantado aprendizado de máquina do Azure Web serviço usa um leitor e um gravador módulo tooread/gravação de dados de / tooan banco de dados do SQL Azure. Esse serviço da Web expõe Olá quatro parâmetros a seguir: nome do servidor, nome do banco de dados, nome de conta de usuário do servidor e senha de conta de usuário do servidor de banco de dados.

> [!NOTE]
> Somente entradas e saídas da atividade de AzureMLBatchExecution Olá podem ser passadas como parâmetros toohello serviço da Web. Por exemplo, Olá acima trecho JSON, MLSqlInput é uma entrada toohello AzureMLBatchExecution atividade, que é passada como um serviço Web de entrada toohello por meio do parâmetro webServiceInput.

## <a name="machine-learning-update-resource-activity"></a>Atividade de Atualização de Recursos do Machine Learning
Você pode especificar Olá propriedades em uma definição de JSON da atividade do Azure ML atualização recursos a seguir. a propriedade de tipo Hello atividade Olá deve ser: **AzureMLUpdateResource**. Você deve criar uma primeiro o serviço vinculado de aprendizado de máquina do Azure e especificar o nome de Olá-lo como um valor para Olá **linkedServiceName** propriedade. Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooAzureMLUpdateResource de atividade:

Propriedade | Descrição | Obrigatório 
-------- | ----------- | --------
trainedModelName | Nome da saudação treinados novamente o modelo. | Sim |  
trainedModelDatasetName | Conjunto de dados apontando toohello arquivo iLearner retornado por Olá treinar novamente a operação. | Sim | 

### <a name="json-example"></a>Exemplo de JSON
pipeline de saudação tem duas atividades: **AzureMLBatchExecution** e **AzureMLUpdateResource**. Hello atividade de execução de lote do ML do Azure usa dados de treinamento hello como entrada e produz um arquivo iLearner como saída. atividade de Olá chama o serviço web de treinamento hello (experiência de treinamento exposto como um serviço da web) com dados de treinamento de entrada hello e recebe o arquivo ilearner de saudação do hello webservice. Olá placeholderBlob é apenas um saída fictício conjunto de dados que é exigido pelo pipeline de saudação do hello Azure Data Factory serviço toorun.


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a>Atividade do U-SQL da Análise Data Lake
Você pode especificar Olá propriedades em uma definição de JSON da atividade U-SQL a seguir. a propriedade de tipo Hello atividade Olá deve ser: **DataLakeAnalyticsU SQL**. Você deve criar um serviço vinculado de análise do Azure Data Lake e especificar o nome de Olá-lo como um valor para Olá **linkedServiceName** propriedade. Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você definir o tipo de saudação da atividade tooDataLakeAnalyticsU-SQL: 

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| scriptPath |Toofolder de caminho que contém o script hello U-SQL. Nome do arquivo hello diferencia maiusculas de minúsculas. |Não (se você usar o script) |
| scriptLinkedService |Serviço vinculado que vincula o armazenamento de saudação que contém a fábrica de dados Olá script toohello |Não (se você usar o script) |
| script |Especificar script embutido em vez de especificar scriptPath e scriptLinkedService. Por exemplo: "script": "CREATE DATABASE test". |Não (se você usar scriptPath e scriptLinkedService) |
| degreeOfParallelism |número máximo de saudação de nós usados simultaneamente toorun trabalho de saudação. |Não |
| prioridade |Determina quais trabalhos entre todos os que estão na fila devem ser selecionada toorun primeiro. Olá Olá número menor, Olá Olá prioridade. |Não |
| parâmetros |Parâmetros de script hello U-SQL |Não |

### <a name="json-example"></a>Exemplo de JSON

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

Para saber mais, consulte [Atividade de U-SQL no Data Lake Analytics](data-factory-usql-activity.md). 

## <a name="stored-procedure-activity"></a>Atividade de Procedimento Armazenado
Você pode especificar Olá seguintes propriedades em uma definição de JSON de atividade de procedimento armazenado. a propriedade de tipo Hello atividade Olá deve ser: **SqlServerStoredProcedure**. Você deve criar uma saudação serviços vinculados a seguir e especificar o nome de saudação do serviço Olá vinculado como um valor para hello **linkedServiceName** propriedade:

- SQL Server 
- Banco de Dados SQL do Azure
- SQL Data Warehouse do Azure

Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooSqlServerStoredProcedure de atividade:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| storedProcedureName |Especifique o nome de saudação do procedimento de Olá armazenado no banco de dados do SQL Azure hello ou Azure SQL Data Warehouse que é representado pelo serviço Olá vinculado que Olá usos da tabela de saída. |Sim |
| storedProcedureParameters |Especifique valores para parâmetros de procedimento armazenado. Se você precisar toopass nulo para um parâmetro, use a sintaxe de saudação: "param1": null (todas as letras minúsculas). Consulte Olá toolearn de exemplo sobre como usar essa propriedade a seguir. |Não |

Se você especificar um conjunto de dados de entrada, ele deve estar disponível (em status 'Pronto') para Olá armazenados toorun de atividade de procedimento. Olá conjunto de dados de entrada não pode ser consumido no procedimento Olá armazenado como um parâmetro. É apenas dependência de saudação toocheck usado antes de atividade de procedimento armazenado de saudação inicial. Você deve especificar um conjunto de dados de saída para uma atividade de procedimento armazenado. 

Conjunto de dados de saída especifica Olá **agenda** para Olá armazenados atividade de procedimento (por hora, semanalmente, mensalmente, etc.). Olá conjunto de dados de saída deve usar um **serviço vinculado** que se refere a tooan banco de dados do SQL Azure ou um Azure SQL Data Warehouse ou um banco de dados do SQL Server no qual você deseja Olá toorun do procedimento armazenado. Olá conjunto de dados de saída pode servir como um resultado do modo toopass Olá do procedimento armazenado de saudação para processamento subsequente por outra atividade ([encadeamento atividades](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) no pipeline de saudação. No entanto, fábrica de dados não gravará automaticamente saída Olá de um conjunto de dados do procedimento armazenado toothis. É Olá tabela gravações tooa SQL que Olá pontos do conjunto de dados de saída de procedimento armazenado. Em alguns casos, o conjunto de dados de saída de hello pode ser um **conjunto de dados fictício**, que é usado somente para atividade de procedimento armazenado de agendamento de saudação toospecify para executar a saudação.  

### <a name="json-example"></a>Exemplo de JSON

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

Para saber mais, consulte o artigo [Atividade de Procedimento Armazenado](data-factory-stored-proc-activity.md). 

## <a name="net-custom-activity"></a>Atividade personalizada do .NET
Você pode especificar Olá seguintes propriedades em uma atividade personalizada do .NET definição JSON. a propriedade de tipo Hello atividade Olá deve ser: **DotNetActivity**. Você deve criar um serviço vinculado do HDInsight do Azure ou um lote do Azure vinculado de serviço e especifique o nome de saudação do serviço vinculado de saudação como um valor para Olá **linkedServiceName** propriedade. Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooDotNetActivity de atividade:
 
| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| AssemblyName | Nome do assembly hello. Exemplo hello, ele é: **MyDotnetActivity.dll**. | Sim |
| EntryPoint |Nome da classe de saudação que implementa a interface de IDotNetActivity hello. Exemplo hello, ele é: **MyDotNetActivityNS.MyDotNetActivity** onde MyDotNetActivityNS é o namespace de saudação e MyDotNetActivity é a classe de saudação.  | Sim | 
| PackageLinkedService | Nome da saudação serviço vinculado do armazenamento do Azure que aponta toohello armazenamento de blob que contém o arquivo de zip hello atividade personalizado. Exemplo hello, ele é: **AzureStorageLinkedService**.| Sim |
| PackageFile | Nome do arquivo zip de saudação. Exemplo hello, ele é: **customactivitycontainer/MyDotNetActivity.zip**. | Sim |
| extendedProperties | Propriedades estendidas que você pode definir e passar em código .NET de toohello. Neste exemplo, Olá **SliceStart** variável estiver definida como valor tooa com base na variável de sistema SliceStart hello. | Não | 

### <a name="json-example"></a>Exemplo de JSON

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

Para saber informações detalhadas, consulte o artigo [Usar atividades personalizadas no Data Factory](data-factory-use-custom-activities.md). 

## <a name="next-steps"></a>Próximas etapas
Consulte Olá tutoriais a seguir: 

- [Tutorial: Criar um pipeline com uma atividade de cópia](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [Tutorial: Criar um pipeline com uma atividade de hive](data-factory-build-your-first-pipeline-using-editor.md)