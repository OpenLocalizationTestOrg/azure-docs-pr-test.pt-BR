---
title: "Pipelines aaaCreate/agendamento, atividades de cadeia de fábrica de dados | Microsoft Docs"
description: "Saiba toocreate um pipeline de dados no Azure Data Factory toomove e transformar dados. Crie uma dados controlados por informações do fluxo de trabalho tooproduce toouse pronto."
keywords: pipeline de dados, fluxo de trabalho controlados por dados
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 13b137c7-1033-406f-aea7-b66f25b313c0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: shlo
ms.openlocfilehash: 4a0fc20f98ce6453c16955e97fddb891926c173a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="pipelines-and-activities-in-azure-data-factory"></a>Pipelines e atividades no Azure Data Factory
Este artigo ajuda você a entender os pipelines e atividades do Azure Data Factory e usá-las em fluxos de trabalho do tooconstruct ponta a ponta orientados a dados para o movimento de dados e cenários de processamento de dados.  

> [!NOTE]
> Este artigo pressupõe que você ter feito [tooAzure Introdução fábrica de dados](data-factory-introduction.md). Se você não tiver experiência prática com a criação de data factories, ler o [tutorial de transformação de dados](data-factory-build-your-first-pipeline.md) e/ou [tutorial de movimentação de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ajudará a entender melhor este artigo.  

## <a name="overview"></a>Visão geral
Uma fábrica de dados pode ter um ou mais pipelines. Um pipeline é um agrupamento lógico de atividades que juntas executam uma tarefa. atividades de saudação em um pipeline definem ações tooperform em seus dados. Por exemplo, você pode usar uma cópia de dados de toocopy de atividade de um tooan do SQL Server local armazenamento de BLOBs do Azure. Em seguida, use uma atividade de Hive que executa um script de Hive em um dados do Azure HDInsight cluster tooprocess/transformação de dados de saída tooproduce do armazenamento de blob hello. Por fim, use uma segunda cópia atividade toocopy Olá saída dados tooan Azure SQL Data Warehouse sobre quais inteligência comercial (BI) soluções de relatório são criadas. 

Uma atividade pode não usar ou usar vários [conjuntos de dados](data-factory-create-datasets.md) de entrada e gerar um ou mais [conjuntos de dados](data-factory-create-datasets.md) de saída. Olá diagrama a seguir mostra Olá relação entre pipeline, a atividade e o conjunto de dados na fábrica de dados: 

![Relação entre pipeline, atividade e conjunto de dados](media/data-factory-create-pipelines/relationship-pipeline-activity-dataset.png)

Um pipeline permite toomanage atividades como um conjunto, em vez de cada um deles individualmente. Por exemplo, você pode implantar, agendar, suspender e retomar um pipeline, em vez de lidar com atividades no pipeline de saudação independentemente.

O Data Factory dá suporte a dois tipos de atividades: atividades de movimentação de dados e atividades de transformação de dados. Cada atividade pode não ter ou ter vários [conjuntos de dados](data-factory-create-datasets.md) de entrada e gerar um ou mais conjuntos de dados de saída.

Um conjunto de dados de entrada representa a entrada de saudação para uma atividade no pipeline de saudação e um conjunto de dados de saída representa a saída de hello atividade hello. Conjuntos de dados identificam dados em armazenamentos de dados diferentes, como tabelas, arquivos, pastas e documentos. Depois de criar um conjunto de dados, você pode usá-lo com atividades no pipeline. Por exemplo, um conjunto de dados pode ser o conjunto de dados de entrada/saída de uma atividade de Cópia ou uma atividade do HDInsightHive. Para saber mais sobre conjuntos de dados, confira o artigo [Conjuntos de dados no Azure Data Factory](data-factory-create-datasets.md).

### <a name="data-movement-activities"></a>Atividades de movimentação de dados
Atividade de cópia na fábrica de dados copia dados de um repositório de dados fonte dados repositório tooa coletor. Fábrica de dados oferece suporte a saudação armazenamentos de dados a seguir. Dados de qualquer fonte podem ser gravados tooany coletor. Clique em um toolearn de repositório de dados como toocopy tooand de dados do repositório.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Armazena dados com * pode ser local ou na IaaS do Azure e requer que você tooinstall [Data Management Gateway](data-factory-data-management-gateway.md) em uma máquina de IaaS no local/Azure.

Para obter mais informações, confira o artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md).

### <a name="data-transformation-activities"></a>Atividades de transformação de dados
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

Para obter mais informações, confira o artigo [Atividades de transformação de dados](data-factory-data-transformation-activities.md).

### <a name="custom-net-activities"></a>Atividades personalizadas do .NET 
Se você precisar toomove dados para/de dados de um repositório que hello atividade de cópia não oferecer suporte a, ou transformar dados usando sua própria lógica, crie um **atividade personalizada do .NET**. Para obter detalhes sobre como criar e usar uma atividade personalizada, confira [Usar atividades personalizadas em um pipeline do Azure Data Factory](data-factory-use-custom-activities.md).

## <a name="schedule-pipelines"></a>Agendar pipelines
Um pipeline está ativo somente entre sua hora de **início** e de **término**. Ele não é executado antes da hora de início do hello, ou após a hora de término hello. Se Olá pipeline é pausado, ele não seja executado independentemente de seu tempo de início e término. Para um pipeline toorun, ela deve não ser pausada. Consulte [de agendamento e execução](data-factory-scheduling-and-execution.md) toounderstand funcionamento do agendamento e execução no Azure Data Factory.

## <a name="pipeline-json"></a>Pipeline de JSON
Vamos dar uma olhada mais próxima em como um pipeline é definido no formato JSON. estrutura genérica de saudação para um pipeline é da seguinte maneira:

```json
{
    "name": "PipelineName",
    "properties": 
    {
        "description" : "pipeline description",
        "activities":
        [

        ],
        "start": "<start date-time>",
        "end": "<end date-time>",
        "isPaused": true/false,
        "pipelineMode": "scheduled/onetime",
        "expirationTime": "15.00:00:00",
        "datasets": 
        [
        ]
    }
}
```

| Marca | Descrição | Obrigatório |
| --- | --- | --- |
| name |Nome do pipeline de saudação. Especifique um nome que representa a ação Olá Olá pipeline executa. <br/><ul><li>Número máximo de caracteres: 260</li><li>Deve começar com uma letra, um número ou um sublinhado (_)</li><li>Os seguintes caracteres não são permitidos: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</li></ul> |Sim |
| description | Especifique o texto de saudação que descreve quais Olá pipeline é usado para. |Sim |
| atividades | Olá **atividades** seção pode ter uma ou mais atividades definidas nela. Consulte a próxima seção Olá para obter detalhes sobre o elemento JSON de atividades de saudação. | Sim |  
| iniciar | Data-hora de início para o pipeline de saudação. Deve estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por exemplo: `2016-10-14T16:32:41Z`. <br/><br/>É possível toospecify a hora local, por exemplo um tempo estimado. Veja este exemplo: `2016-02-27T06:00:00-05:00`", que é 6 AM EST.<br/><br/>Hello propriedades de início e término juntas especificam o período ativo para o pipeline de saudação. Fatias de saída são produzidas somente nesse período ativo. |Não<br/><br/>Se você especificar um valor para a propriedade end hello, você deve especificar o valor para a propriedade de início de saudação.<br/><br/>Olá horários de início e término podem ser vazio toocreate um pipeline. Você deve especificar os dois valores tooset um período ativo para Olá toorun de pipeline. Se você não especificar horários de início e término durante a criação de um pipeline, você pode defini-las usando o cmdlet Olá AzureRmDataFactoryPipelineActivePeriod conjunto mais tarde. |
| end | Data-hora de término para o pipeline de saudação. Se especificado, deve estar no formato ISO. Por exemplo: `2016-10-14T17:32:41Z` <br/><br/>É possível toospecify a hora local, por exemplo um tempo estimado. Aqui está um exemplo: `2016-02-27T06:00:00-05:00`, que é 6 AM EST.<br/><br/>pipeline de saudação toorun indefinidamente, especificar 9999-09-09 como valor de saudação para a propriedade end hello. <br/><br/> Um pipeline está ativo somente entre sua hora de início e de término. Ele não é executado antes da hora de início do hello, ou após a hora de término hello. Se Olá pipeline é pausado, ele não seja executado independentemente de seu tempo de início e término. Para um pipeline toorun, ela deve não ser pausada. Consulte [de agendamento e execução](data-factory-scheduling-and-execution.md) toounderstand funcionamento do agendamento e execução no Azure Data Factory. |Não <br/><br/>Se você especificar um valor para a propriedade de início Olá, você deve especificar o valor para a propriedade end hello.<br/><br/>Consulte as observações para Olá **iniciar** propriedade. |
| isPaused | Se set tootrue, pipeline de saudação não for executado. Ele tem em Olá pausa. Valor padrão = falso. Você pode usar essa propriedade tooenable ou desabilitar um pipeline. |Não |
| pipelineMode | método Hello para o agendamento é executado para o pipeline de saudação. Os valores permitidos são: scheduled (padrão), onetime.<br/><br/>'Agendado' indica que esse pipeline Olá é executado em um intervalo de tempo especificado de acordo com o período ativo de tooits (hora de início e de término). 'Única' indica que esse pipeline Olá é executado apenas uma vez. Pipelines Onetime não podem ser modificados e atualizados depois de criados atualmente. Confira [Pipeline avulso](#onetime-pipeline) para obter detalhes sobre a configuração única. |Não |
| expirationTime | Duração de tempo após a criação do qual Olá [pipeline avulso](#onetime-pipeline) é válido e deve permanecer provisionado. Se ele não tem qualquer ativo, falha, ou pendente é executado, o pipeline de saudação é automaticamente excluído uma vez atingir o tempo de expiração hello. valor de padrão de saudação:`"expirationTime": "3.00:00:00"`|Não |
| conjuntos de dados |Lista de toobe de conjuntos de dados usado por atividades definidas no pipeline de saudação. Essa propriedade pode ser conjuntos de dados usado toodefine pipeline toothis específico e não definidos na fábrica de dados hello. Conjuntos de dados definidos dentro este pipeline só podem ser usados por este pipeline e não podem ser compartilhados. Confira [Conjuntos de dados com escopo](data-factory-create-datasets.md#scoped-datasets) para obter detalhes. |Não |

## <a name="activity-json"></a>Atividade JSON
Olá **atividades** seção pode ter uma ou mais atividades definidas nela. Cada atividade tem Olá estrutura de nível superior a seguir:

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
    },
    "scheduler":
    {
    }
}
```

Tabela a seguir descreve as propriedades na atividade de saudação definição JSON:

| Marca | Descrição | Obrigatório |
| --- | --- | --- |
| name | Nome da atividade de saudação. Especifique um nome que representa a ação de saudação hello atividade executa. <br/><ul><li>Número máximo de caracteres: 260</li><li>Deve começar com uma letra, um número ou um sublinhado (_)</li><li>Os seguintes caracteres não são permitidos: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</li></ul> |Sim |
| description | Texto que descreve o que hello atividade ou é usado para |Sim |
| type | Tipo de atividade de saudação. Consulte Olá [atividades de movimentação de dados](#data-movement-activities) e [atividades de transformação de dados](#data-transformation-activities) seções para diferentes tipos de atividades. |Sim |
| inputs |Tabelas de entrada usadas pela atividade Olá<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Sim |
| outputs |Tabelas de saída usadas pela atividade de saudação.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": "outputtable1" } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": "outputtable1" }, { "name": "outputtable2" }  ],` |Sim |
| linkedServiceName |Nome do serviço de saudação vinculado usado pela atividade de saudação. <br/><br/>Uma atividade pode exigir que você especifique que o serviço Olá vinculado que vincula o ambiente de computação necessária toohello. |Sim para Atividade do HDInsight e Atividade de Pontuação de Lote do Azure Machine Learning <br/><br/>Não para todas as outros |
| typeProperties |Propriedades em Olá **typeProperties** seção dependem do tipo de atividade de saudação. Propriedades de tipo de toosee para uma atividade, clique em atividade de toohello links na seção anterior hello. | Não |
| policy |Diretivas que afetam o comportamento de tempo de execução de saudação da atividade de saudação. Se não for especificado, as políticas padrão serão utilizadas. |Não |
| agendador | propriedade "Agendador" é usado toodefine desejado de agendamento para a atividade de saudação. Seus subpropriedades são Olá mesmo Olá na Olá [propriedade de disponibilidade em um conjunto de dados](data-factory-create-datasets.md#dataset-availability). |Não |


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

## <a name="sample-copy-pipeline"></a>Pipeline de cópia de exemplo
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
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
} 
```

Observe Olá pontos a seguir:

* Na seção de atividades hello, há apenas uma atividade cuja **tipo** está definido muito**cópia**.
* Entrada para atividade de saudação é definida muito**InputDataset** e de saída para o conjunto de hello atividade é muito**OutputDataset**. Confira o artigo [Conjuntos de dados](data-factory-create-datasets.md) para definir conjuntos de dados em JSON. 
* Em Olá **typeProperties** seção, **BlobSource** é especificado como tipo de fonte hello e **SqlSink** é especificado como tipo de coletor de saudação. Em Olá [atividades de movimentação de dados](#data-movement-activities) seção, clique em saudação do repositório de dados que você deseja toouse como uma origem ou um coletor toolearn mais sobre como mover dados de/para o repositório de dados. 

Para obter uma explicação completa de criar esse pipeline, consulte [Tutorial: copiar dados de armazenamento de Blob tooSQL banco de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="sample-transformation-pipeline"></a>Pipeline de transformação de exemplo
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
        "start": "2016-04-01T00:00:00Z",
        "end": "2016-04-02T00:00:00Z",
        "isPaused": false
    }
}
```

Observe Olá pontos a seguir: 

* Na seção de atividades hello, há apenas uma atividade cuja **tipo** está definido muito**HDInsightHive**.
* arquivo de script do Hive Hello, **partitionweblogs.hql**, é armazenado no hello conta de armazenamento do Azure (especificado por scriptLinkedService hello, chamado **AzureStorageLinkedService**) e em  **script** pasta no contêiner Olá **adfgetstarted**.
* Olá `defines` seção é toospecify usadas configurações de tempo de execução de saudação que são passadas script do hive toohello como valores de configuração do Hive (por exemplo `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Olá **typeProperties** seção é diferente para cada atividade de transformação. toolearn sobre propriedades de tipo com suporte para uma atividade de transformação, clique em atividade transformação Olá Olá [atividades de transformação de dados](#data-transformation-activities) tabela. 

Para obter uma explicação completa de criar esse pipeline, consulte [Tutorial: Crie sua primeira pipeline tooprocess de dados usando o cluster Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="multiple-activities-in-a-pipeline"></a>Várias atividades em um pipeline
pipelines de dois exemplos anteriores Olá possuem apenas uma atividade. Você pode ter mais de uma atividade em um pipeline.  

Se você tiver várias atividades em um pipeline e a saída de uma atividade não é uma entrada de outra atividade, atividades Olá podem executados em paralelo, se as fatias de dados de entrada para atividades de saudação estão prontas. 

É possível encadear duas atividades tendo Olá o conjunto de dados de saída de uma atividade como conjunto de dados de entrada de saudação do hello outra atividade. atividade de segundo Olá executa somente quando hello primeiro uma for concluída com êxito.

![Encadeamento de atividades no hello mesmo pipeline](./media/data-factory-create-pipelines/chaining-one-pipeline.png)

Neste exemplo, o pipeline de saudação tem duas atividades: atividade1 e da atividade2. Olá atividade1 leva Dataset1 como entrada e produz uma saída Dataset2. Hello atividade leva Dataset2 como entrada e produz uma saída Dataset3. Desde a saída atividade1 Olá (Dataset2) é a entrada de saudação da atividade2, Olá atividade2 é executada somente após hello atividade é concluída com êxito e produz Olá Dataset2 fatia. Se falha por algum motivo de saudação atividade1 e não produz a fatia Olá Dataset2, hello atividade 2 não será executado para essa fatia (por exemplo: Estou too10 9 de AM). 

Também é possível encadear atividades que estão em pipelines diferentes.

![Encadeando atividades em dois pipelines](./media/data-factory-create-pipelines/chaining-two-pipelines.png)

Neste exemplo, Pipeline1 tem apenas uma atividade que usa Dataset1 como entrada e gera Dataset2 como saída. Olá Pipeline2 também tem apenas uma atividade que usa Dataset2 como uma entrada e Dataset3 como saída. 

Para saber mais, confira [agendamento e execução](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="create-and-monitor-pipelines"></a>Criar e monitorar pipelines
Você pode criar pipelines usando uma destas ferramentas ou SDKs. 

- Assistente de Cópia. 
- Portal do Azure
- Visual Studio
- Azure PowerShell
- Modelo do Azure Resource Manager
- API REST
- API do .NET

Consulte Olá tutoriais para obter instruções passo a passo para criar pipelines usando uma dessas ferramentas ou SDKs a seguir.
 
- [Crie um pipeline com uma atividade de transformação de dados](data-factory-build-your-first-pipeline.md)
- [Crie um pipeline com uma atividade de movimentação de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Depois de um pipeline é criado/implantado, você pode gerenciar e monitorar seus pipelines usando Olá folhas portais do Azure ou monitorar e gerenciar aplicativos. Consulte Olá seguintes tópicos para obter instruções passo a passo. 

- [Monitorar e gerenciar os pipelines usando as folhas do portal do Azure](data-factory-monitor-manage-pipelines.md).
- [Monitorar e gerenciar pipelines usando Monitorar e Gerenciar Aplicativos](data-factory-monitor-manage-app.md)


## <a name="onetime-pipeline"></a>Pipeline Onetime
Você pode criar e agendar um pipeline toorun periodicamente (por exemplo: por hora ou diariamente) dentro de saudação inicial e final horários especificados na definição do pipeline de saudação. Veja [Agendando atividades](#scheduling-and-execution) para obter detalhes. Você também pode criar um pipeline que executa apenas uma vez. toodo assim, você pode definir Olá **pipelineMode** propriedade Olá pipeline definição muito**única** conforme Olá amostra JSON a seguir. Olá valor padrão dessa propriedade é **agendado**.

```json
{
    "name": "CopyPipeline",
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
                        "name": "InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ]
                "name": "CopyActivity-0"
            }
        ]
        "pipelineMode": "OneTime"
    }
}
```

Observe o seguinte hello:

* **Iniciar** e **final** tempos pipeline Olá não forem especificados.
* **Disponibilidade** de entrada e saída de conjuntos de dados for especificado (**frequência** e **intervalo**), mesmo que a fábrica de dados não usa os valores hello.  
* A exibição de diagrama não mostra pipelines únicos. Este comportamento ocorre por design.
* Pipelines avulsos não podem ser atualizados. Clonar um único pipeline, renomeá-lo, atualizar propriedades e implantá-lo toocreate outro.


## <a name="next-steps"></a>Próximas etapas
- Para saber mais sobre conjuntos de dados, confira o artigo [Criar conjuntos de dados](data-factory-create-datasets.md). 
- Para saber mais sobre como os pipelines são agendados e executados, confira o artigo [Agendamento e execução no Azure Data Factory](data-factory-scheduling-and-execution.md). 
  

