---
title: "aaaBuild sua primeira fábrica de dados (PowerShell) | Microsoft Docs"
description: "Neste tutorial, você cria um pipeline de exemplo do Azure Data Factory usando o Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a>Tutorial: Compilar seu primeiro data factory do Azure usando o Azure PowerShell
> [!div class="op_single_selector"]
> * [Visão geral e pré-requisitos](data-factory-build-your-first-pipeline.md)
> * [Portal do Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modelo do Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

Neste artigo, você usa toocreate do PowerShell do Azure a primeira data factory do Azure. tutorial de saudação toodo usando outras ferramentas/SDKs, selecione uma das opções de saudação da lista suspensa de saudação.

pipeline de saudação neste tutorial tem uma atividade: **atividade Hive do HDInsight**. Essa atividade executa um script do hive em um cluster de HDInsight do Azure que transforma dados de saída de tooproduce de entrada. pipeline de saudação é agendado toorun depois de um mês entre hello especificar horários de início e término. 

> [!NOTE]
> pipeline de dados Olá neste tutorial transforma dados de saída de tooproduce de dados de entrada. Ele não copia dados de um repositório de dados de destino fonte dados repositório tooa. Para obter um tutorial sobre como toocopy dados usando a fábrica de dados do Azure, consulte [Tutorial: copiar dados de armazenamento de Blob tooSQL banco de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Um pipeline pode ter mais de uma atividade. E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada. Para saber mais, confira [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

## <a name="prerequisites"></a>Pré-requisitos
* Leia [visão geral do Tutorial](data-factory-build-your-first-pipeline.md) artigo e hello completa **pré-requisito** etapas.
* Siga as instruções em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo tooinstall versão mais recente do PowerShell do Azure no seu computador.
* (opcional) Este artigo não aborda todos os cmdlets da fábrica de dados hello. Consulte [Referência de cmdlet de Data Factory](/powershell/module/azurerm.datafactories) para obter uma documentação abrangente sobre os cmdlets de Data Factory.

## <a name="create-data-factory"></a>Criar um data factory
Nesta etapa, você usar o Azure PowerShell toocreate uma fábrica de dados do Azure denominado **FirstDataFactoryPSH**. Uma fábrica de dados pode ter um ou mais pipelines. Um pipeline em um data factory pode ter uma ou mais atividades. Por exemplo, dados de toocopy uma atividade de cópia de um repositório de dados de destino do código-fonte tooa e uma atividade de Hive do HDInsight toorun um tootransform de script do Hive dados de entrada. Vamos começar com a criação de fábrica de dados Olá nesta etapa.

1. Inicie o PowerShell do Azure e execute Olá comando a seguir. Mantenha o Azure PowerShell aberta até o fim deste tutorial hello. Se você fecha e reabrir, será necessário toorun esses comandos novamente.
   * Execute Olá comando a seguir e insira o nome de usuário de saudação e a senha que você use toosign em toohello portal do Azure.
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * Execute Olá tooview de comando a seguir todas as assinaturas de saudação para esta conta.
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * Execute Olá assinatura de saudação do comando tooselect que você deseja toowork com a seguir. Essa assinatura deve ser Olá mesmas Olá aquele que você usou no portal do Azure de saudação.
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. Criar um grupo de recursos do Azure denominado **ADFTutorialResourceGroup** executando Olá comando a seguir:
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    Algumas das etapas de saudação neste tutorial presumem que você use o grupo de recursos de saudação chamado ADFTutorialResourceGroup. Se você usar um grupo de recursos diferentes, será necessário toouse-lo no lugar de ADFTutorialResourceGroup neste tutorial.
3. Executar Olá **New-AzureRmDataFactory** cmdlet que cria uma fábrica de dados denominada **FirstDataFactoryPSH**.

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
Observe Olá pontos a seguir:

* nome de saudação do hello Azure Data Factory deve ser globalmente exclusivo. Se você receber o erro Olá **"FirstDataFactoryPSH" nome da fábrica de dados não está disponível**, alterar o nome da saudação (por exemplo, yournameFirstDataFactoryPSH). Use esse nome em vez de ADFTutorialFactoryPSH ao executar as etapas neste tutorial. Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.
* toocreate instâncias de fábrica de dados, você precisa toobe um colaborador/administrador de saudação assinatura do Azure
* nome Olá Olá da fábrica de dados pode ser registrado como um nome DNS no hello futuro e, portanto, se tornarão visível publicamente.
* Se você receber o erro Olá: "**esta assinatura não está registrado toouse namespace DataFactory**", execute um dos seguintes hello e tente publicar novamente:

  * No Azure PowerShell, execute Olá provedor do comando tooregister Olá fábrica de dados a seguir:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      Você pode executar Olá tooconfirm de comando a seguir que Olá Data Factory provedor está registrado:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Usando o logon Olá assinatura do Azure em Olá [portal do Azure](https://portal.azure.com) e navegue tooa folha de fábrica de dados (ou) criar uma fábrica de dados no hello portal do Azure. Esta ação registra automaticamente o provedor de saudação para você.

Antes de criar um pipeline, é necessário toocreate algumas entidades da fábrica de dados pela primeira vez. Você primeiro criar dados de toolink serviços vinculados repositórios/calcula tooyour dados armazenam, definem a entrada e saída de dados de entrada/saída toorepresent conjuntos de dados em repositórios de dados vinculados e, em seguida, criar o pipeline de saudação com uma atividade que usa esses conjuntos de dados.

## <a name="create-linked-services"></a>Criar serviços vinculados
Nesta etapa, você pode vincular sua conta de armazenamento do Azure e uma fábrica de dados sob demanda do Azure HDInsight cluster tooyour. Olá conta de armazenamento do Azure mantém Olá dados de entrada e saídos para o pipeline de saudação neste exemplo. Olá serviço vinculado do HDInsight é toorun usado um script de Hive especificado na atividade de saudação do pipeline de saudação neste exemplo. Identificar quais dados repositório/computação serviços são usados em seu cenário e vincular a fábrica de dados desses serviços toohello criando serviços vinculados.

### <a name="create-azure-storage-linked-service"></a>Criar o serviço vinculado do armazenamento do Azure
Nesta etapa, você vincular sua fábrica de dados de tooyour de conta de armazenamento do Azure. Use Olá mesma conta de armazenamento do Azure, dados de entrada/saída toostore e hello HQL arquivo de script.

1. Crie um arquivo JSON chamado StorageLinkedService.json na pasta de C:\ADFGetStarted Olá com hello seguindo conteúdo. Crie pasta Olá ADFGetStarted se ele ainda não existir.

    ```json
    {
        "name": "StorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "description": "",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
    }
    ```
    Substituir **nome da conta** com nome de saudação da sua conta de armazenamento do Azure e **chave de conta** com a chave de acesso de saudação do Olá conta de armazenamento do Azure. toolearn como tooget acessar o armazenamento de chave, consulte Olá informações sobre como tooview, copiar e armazenamento regenerar chaves de acesso em [gerenciar sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
2. No PowerShell do Azure, alterne toohello ADFGetStarted pasta.
3. Você pode usar o hello **AzureRmDataFactoryLinkedService novo** cmdlet que cria um serviço vinculado. Esse cmdlet e outros cmdlets de fábrica de dados que você usar este tutorial requer que você toopass valores para Olá *ResourceGroupName* e *DataFactoryName* parâmetros. Como alternativa, você pode usar **Get-AzureRmDataFactory** tooget um **DataFactory** de objeto e passar o objeto de saudação sem digitar *ResourceGroupName* e  *DataFactoryName* cada vez que você executar um cmdlet. Comando a seguir de execução Olá tooassign saída Olá Olá **Get-AzureRmDataFactory** cmdlet tooa **$df** variável.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. Agora, execute Olá **New-AzureRmDataFactoryLinkedService** cmdlet que cria Olá vinculado **StorageLinkedService** service.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    Se você não executar Olá **Get-AzureRmDataFactory** toohello de saída do cmdlet e hello atribuído **$df** variável, você teria toospecify valores hello *ResourceGroupName*e *DataFactoryName* parâmetros da seguinte maneira.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    Se você fechar o Azure PowerShell no meio de saudação do tutorial hello, você tem Olá toorun **AzureRmDataFactory Get** próxima vez que iniciar o tutorial do Azure PowerShell toocomplete saudação do cmdlet.

### <a name="create-azure-hdinsight-linked-service"></a>Criar o serviço vinculado do Azure HDInsight
Nesta etapa, você vincular uma fábrica de dados sob demanda HDInsight cluster tooyour. cluster do HDInsight Olá é criado em tempo de execução e excluído após a conclusão ocioso e processamento para o período de tempo especificado Olá automaticamente. Você pode usar seu próprio cluster do HDInsight em vez de usar um cluster do HDInsight sob demanda. Veja [Serviços vinculados de computação](data-factory-compute-linked-services.md) para obter detalhes.

1. Crie um arquivo JSON chamado **HDInsightOnDemandLinkedService**. JSON no hello **C:\ADFGetStarted** pasta com hello conteúdo a seguir.

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
    Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:

   | Propriedade | Descrição |
   |:--- |:--- |
   | ClusterSize |Especifica o tamanho de saudação do cluster do HDInsight hello. |
   | TimeToLive |Especifica que Olá de tempo ocioso para um cluster do HDInsight hello, antes de ser excluído. |
   | linkedServiceName |Especifica a conta de armazenamento de saudação que é usado toostore logs de Olá gerados pelo HDInsight |

    Observe Olá pontos a seguir:

   * Olá fábrica de dados cria um **baseados em Linux** cluster HDInsight para você com hello JSON. Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.
   * Você pode usar **seu próprio cluster do HDInsight** em vez de usar um cluster do HDInsight sob demanda. Confira [Serviço vinculado do HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.
   * Olá HDInsight cluster cria um **contêiner padrão** no armazenamento de blob Olá especificado no hello JSON (**linkedServiceName**). HDInsight não exclui esse contêiner quando Olá cluster é excluído. Este comportamento ocorre por design. Com o serviço vinculado HDInsight sob demanda, um cluster HDInsight é criado sempre que uma fatia é processada, a menos que haja um cluster ativo existente (**timeToLive**). cluster de saudação é excluído automaticamente quando Olá processamento é concluído.

       Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure. Se não precisar para solução de problemas de trabalhos de saudação, talvez você queira toodelete-os custos de armazenamento do tooreduce hello. nomes de saudação desses contêineres seguem um padrão: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Use ferramentas como [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com/) armazenamento de blobs de contêineres toodelete do Azure.

     Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.
2. Executar Olá **AzureRmDataFactoryLinkedService novo** cmdlet que cria Olá vinculado serviço chamado HDInsightOnDemandLinkedService.
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a>Criar conjuntos de dados
Nesta etapa, você cria conjuntos de dados toorepresent Olá entrada e saída de dados para o processamento do Hive. Esses conjuntos de dados Consulte toohello **StorageLinkedService** você tiver criado anteriormente neste tutorial. Olá tooan de pontos de serviço vinculado conta de armazenamento do Azure e conjuntos de dados especificam contêiner, pasta, nome do arquivo no armazenamento de saudação que contém a entrada e saída de dados.

### <a name="create-input-dataset"></a>Criar conjunto de dados de entrada
1. Crie um arquivo JSON chamado **InputTable.json** em Olá **C:\ADFGetStarted** pasta com hello conteúdo a seguir:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
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
    Olá JSON define um conjunto de dados chamado **AzureBlobInput**, que representa dados de entrada de uma atividade no pipeline de saudação. Além disso, ele especifica que os dados de entrada hello estão localizados no contêiner de blob Olá chamado **adfgetstarted** e Olá pasta chamada **inputdata**.

    Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:

   | Propriedade | Descrição |
   |:--- |:--- |
   | type |propriedade de tipo de saudação é definida tooAzureBlob porque os dados residem no armazenamento de BLOBs do Azure. |
   | linkedServiceName |refere-se toohello StorageLinkedService criado anteriormente. |
   | fileName |Essa propriedade é opcional. Se você omitir essa propriedade, todos os arquivos de saudação do hello folderPath são escolhidos. Nesse caso, somente Olá input.log é processado. |
   | type |arquivos de log Olá estão no formato de texto, para que possamos usar TextFormat. |
   | columnDelimiter |colunas em arquivos de log de saudação são delimitadas pelo caractere de vírgula hello (,). |
   | frequência/intervalo |frequência definida tooMonth e o intervalo é 1, o que significa que as fatias de entrada hello estarão disponíveis mensalmente. |
   | externo |Essa propriedade é definida tootrue se os dados de entrada hello não são gerados pelo serviço da fábrica de dados hello. |
2. Execute Olá comando no conjunto de dados do Azure PowerShell toocreate Olá fábrica de dados a seguir:

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a>Criar conjunto de dados de saída
Agora, você pode criar hello saída dataset toorepresent Olá saída dados armazenados em Olá armazenamento de BLOBs do Azure.

1. Crie um arquivo JSON chamado **OutputTable.json** em Olá **C:\ADFGetStarted** pasta com hello conteúdo a seguir:

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    Olá JSON define um conjunto de dados chamado **AzureBlobOutput**, que representa dados de saída para uma atividade no pipeline de saudação. Além disso, ele especifica que resultados Olá são armazenados no contêiner de blob Olá chamado **adfgetstarted** e Olá pasta chamada **partitioneddata**. Olá **disponibilidade** seção especifica esse conjunto de dados de saída de saudação é produzido por mês.
2. Execute Olá comando no conjunto de dados do Azure PowerShell toocreate Olá fábrica de dados a seguir:

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a>Criar um pipeline
Nesta etapa, você cria seu primeiro pipeline com a atividade **HDInsightHive** . Entrada fatia está disponível mensal (frequência: mês, intervalo: 1), fatias de saída é produzida mensal e Olá Agendador para a atividade de saudação é também definida toomonthly. Olá configurações para o conjunto de dados de saída de hello e Agendador de atividade de saudação devem corresponder. Atualmente, o conjunto de dados de saída é quais unidades Olá agendamento, então você deve criar um conjunto de dados de saída, mesmo que a atividade de saudação não produz nenhuma saída. Se a atividade de saudação não tem nenhuma entrada, você poderá ignorar o dataset de entrada hello criando. Propriedades de saudação usadas em Olá JSON a seguir são explicadas no final desta seção hello.

1. Crie um arquivo JSON chamado MyFirstPipelinePSH.json na pasta de C:\ADFGetStarted Olá com hello seguindo conteúdo:

   > [!IMPORTANT]
   > Substituir **storageaccountname** com o nome da saudação de sua conta de armazenamento Olá JSON.
   >
   >

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "StorageLinkedService",
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
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```
    No trecho JSON a saudação, você está criando um pipeline que consiste em uma única atividade que usa o Hive tooprocess dados em um cluster HDInsight.

    arquivo de script do Hive Hello, **partitionweblogs.hql**, é armazenado no hello conta de armazenamento do Azure (especificado por scriptLinkedService hello, chamado **StorageLinkedService**) e, na **script**  pasta no contêiner Olá **adfgetstarted**.

    Olá **define** seção é configurações de tempo de execução do hello toospecify usado ser passado script do hive toohello como valores de configuração do Hive (por exemplo ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).

    Olá **iniciar** e **final** propriedades do pipeline de saudação especifica o período ativo de saudação do pipeline de saudação.

    Atividade Olá JSON, você especificar esse script de Hive Olá é executado em computação Olá especificada pelo Olá **linkedServiceName** – **HDInsightOnDemandLinkedService**.

   > [!NOTE]
   > Consulte "JSON de Pipeline" [Pipelines e atividades do Azure Data Factory](data-factory-create-pipelines.md) para obter detalhes sobre as propriedades JSON que são usados no exemplo hello.

2. Confirme que você vê Olá **input.log** arquivo hello **adfgetstarted/inputdata** pasta Olá armazenamento de BLOBs do Azure e execução Olá pipeline de saudação do comando toodeploy a seguir. Desde Olá **iniciar** e **final** horários são definidos no hello anterior e **isPaused** é conjunto toofalse, pipeline Olá execuções (atividade no pipeline de saudação) imediatamente após a implantação.

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. Parabéns, você criou com sucesso seu primeiro pipeline usando o Azure PowerShell!

## <a name="monitor-pipeline"></a>Monitorar o pipeline
Nesta etapa, você use toomonitor do PowerShell do Azure que está acontecendo em uma fábrica de dados do Azure.

1. Executar **Get-AzureRmDataFactory** e atribuir Olá saída tooa **$df** variável.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. Executar **Get-AzureRmDataFactorySlice** tooget detalhes sobre todas as fatias de saudação **EmpSQLTable**, que é a tabela de saída de saudação do pipeline de saudação.

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    Observe que Olá StartDateTime que você especificar aqui é hello que mesma hora de início especificada no pipeline de saudação JSON. Aqui está a saída de exemplo hello:

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Executar **Get-AzureRmDataFactoryRun** tooget detalhes de saudação da atividade é executada para uma fatia específica.

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    Aqui está a saída de exemplo hello: 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    Pode manter executar este cmdlet até que você veja fatia Olá **pronto** estado ou **falha** estado. Quando a fatia hello está no estado pronto, verificar Olá **partitioneddata** pasta Olá **adfgetstarted** dados de saída do contêiner em seu armazenamento de blob para hello.  A criação de um cluster do HDInsight sob demanda geralmente leva algum tempo.

    ![dados de saída](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> A criação de um cluster do HDInsight sob demanda geralmente leva algum tempo (20 minutos, aproximadamente). Portanto, espere Olá pipeline tootake **aproximadamente 30 minutos** tooprocess Olá fatia.
>
> arquivo de entrada Hello é excluído quando a fatia de saudação é processada com êxito. Portanto, se você deseja toorerun Olá fatia ou Olá tutorial novamente, pasta de carregamento Olá arquivo de entrada (input.log) toohello inputdata do contêiner de adfgetstarted hello.
>
>

## <a name="summary"></a>Resumo
Neste tutorial, você criou um tooprocess dados da fábrica de dados do Azure executando o script do Hive em um cluster de hadoop de HDInsight. Você usou Olá Editor da fábrica de dados em Olá toodo portal do Azure Olá etapas a seguir:

1. Foi criada uma **data factory**do Azure.
2. Foram criados dois **serviços vinculados**:
   1. **Armazenamento do Azure** vinculado serviço toolink seu armazenamento de BLOBs do Azure que contém a fábrica de dados de toohello de arquivos de entrada/saída.
   2. **HDInsight do Azure** toolink de serviço vinculado sob demanda uma fábrica de dados sob demanda HDInsight Hadoop cluster toohello. A fábrica de dados do Azure cria um HDInsight Hadoop dados de entrada do cluster tooprocess just-in-time e produzir dados de saída.
3. Criados dois **conjuntos de dados**, que descrevem os dados de entrada e saídos para a atividade de Hive do HDInsight no pipeline de saudação.
4. Foi criado um **pipeline** com uma atividade **Hive do HDInsight**.

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você criou um pipeline com uma atividade de transformação (atividade do HDInsight) que executa um script Hive em um cluster do HDInsight do Azure sob demanda. toosee como toouse dados de toocopy uma atividade de cópia de um tooAzure de BLOBs do Azure SQL, consulte [Tutorial: copiar dados de um tooAzure de BLOBs do Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="see-also"></a>Consulte também
| Tópico | Descrição |
|:--- |:--- |
| [Referência de cmdlet do Data Factory](/powershell/module/azurerm.datafactories) |Consulte a documentação abrangente sobre os cmdlets do Data Factory |
| [Pipelines](data-factory-create-pipelines.md) |Este artigo ajuda você a entender os pipelines e atividades do Azure Data Factory e como toouse-los tooconstruct ponta a ponta controladas por dados fluxos de trabalho para seu cenário ou business. |
| [Conjunto de dados](data-factory-create-datasets.md) |Este artigo o ajuda a entender os conjuntos de dados no Azure Data Factory. |
| [Planejamento e execução](data-factory-scheduling-and-execution.md) |Este artigo explica os aspectos de programação e a execução de saudação do modelo de aplicativo do Azure Data Factory. |
| [Monitorar e gerenciar pipelines usando o Aplicativo de Monitoramento](data-factory-monitor-manage-app.md) |Este artigo descreve como toomonitor, gerenciar e depurar pipelines usando Olá monitoramento e gerenciamento de aplicativo. |
