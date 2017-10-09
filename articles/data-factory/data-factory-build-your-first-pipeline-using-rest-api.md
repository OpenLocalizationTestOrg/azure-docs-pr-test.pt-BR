---
title: "aaaBuild sua fábrica de dados primeiro (REST) | Microsoft Docs"
description: "Neste tutorial, você cria um pipeline de exemplo do Azure Data Factory usando a API REST do Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a>Tutorial: Criar seu primeiro data factory do Azure usando a API REST do Data Factory
> [!div class="op_single_selector"]
> * [Visão geral e pré-requisitos](data-factory-build-your-first-pipeline.md)
> * [Portal do Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modelo do Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


Neste artigo, você usar a API de REST de fábrica de dados toocreate sua primeira data factory do Azure. tutorial de saudação toodo usando outras ferramentas/SDKs, selecione uma das opções de saudação da lista suspensa de saudação.

pipeline de saudação neste tutorial tem uma atividade: **atividade Hive do HDInsight**. Essa atividade executa um script do hive em um cluster de HDInsight do Azure que transforma dados de saída de tooproduce de entrada. pipeline de saudação é agendado toorun depois de um mês entre hello especificar horários de início e término.

> [!NOTE]
> Este artigo não aborda todos os Olá API REST. Para obter uma documentação abrangente sobre a API REST, confira a [referência da API REST do Data Factory](/rest/api/datafactory/).
> 
> Um pipeline pode ter mais de uma atividade. E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada. Para saber mais, confira [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="prerequisites"></a>Pré-requisitos
* Leia [visão geral do Tutorial](data-factory-build-your-first-pipeline.md) artigo e hello completa **pré-requisito** etapas.
* Instale o [Curl](https://curl.haxx.se/dlwiz/) em seu computador. Use ferramenta de ONDULAÇÃO Olá com REST comandos toocreate uma fábrica de dados.
* Siga as instruções [deste artigo](../azure-resource-manager/resource-group-create-service-principal-portal.md) para:
  1. Crie um aplicativo Web chamado **ADFGetStartedApp** no Azure Active Directory.
  2. Obtenha a **ID do cliente** e a **chave secreta**.
  3. Obtenha a **ID do locatário**.
  4. Atribuir Olá **ADFGetStartedApp** aplicativo toohello **colaborador da fábrica de dados** função.
* Instale o [Azure PowerShell](/powershell/azure/overview).
* Iniciar **PowerShell** e execução Olá comando a seguir. Mantenha o Azure PowerShell aberta até o fim deste tutorial hello. Se você fecha e reabrir o, será necessário comandos de saudação toorun novamente.
  1. Executar **AzureRmAccount Login** e insira o nome de usuário de saudação e a senha que você use toosign em toohello portal do Azure.
  2. Executar **Get-AzureRmSubscription** tooview todos Olá assinaturas para esta conta.
  3. Executar **AzureRmSubscription Get - SubscriptionName NameOfAzureSubscription | Conjunto AzureRmContext** assinatura de saudação tooselect que você deseja toowork com. Substituir **NameOfAzureSubscription** com o nome da saudação de sua assinatura do Azure.
* Criar um grupo de recursos do Azure denominado **ADFTutorialResourceGroup** executando Olá comando de saudação do PowerShell a seguir:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   Algumas das etapas de saudação neste tutorial presumem que você use o grupo de recursos de saudação chamado ADFTutorialResourceGroup. Se você usar um grupo de recursos diferentes, você precisa toouse nome de saudação do seu grupo de recursos no lugar de ADFTutorialResourceGroup neste tutorial.

## <a name="create-json-definitions"></a>Criar definições JSON
Crie arquivos JSON na pasta Olá onde se encontra curl.exe a seguir.

### <a name="datafactoryjson"></a>datafactory.json
> [!IMPORTANT]
> Nome deve ser globalmente exclusivo, portanto, talvez você queira tooprefix/sufixo ADFCopyTutorialDF toomake ele um nome exclusivo.
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> Substitua **nome da conta** e **chave da conta** pelo nome e pela chave da sua conta de armazenamento do Azure. toolearn como tooget acessar o armazenamento de chave, consulte Olá informações sobre como tooview, copiar e armazenamento regenerar chaves de acesso em [gerenciar sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
>
>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="hdinsightondemandlinkedservicejson"></a>hdinsightondemandlinkedservice.json

```JSON
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:

| Propriedade | Descrição |
|:--- |:--- |
| ClusterSize |Tamanho do cluster do HDInsight hello. |
| TimeToLive |Especifica que Olá de tempo ocioso para um cluster do HDInsight hello, antes de ser excluído. |
| linkedServiceName |Especifica a conta de armazenamento de saudação que é usado toostore logs de Olá gerados pelo HDInsight |

Observe Olá pontos a seguir:

* Olá fábrica de dados cria um **baseados em Linux** cluster HDInsight para você com hello acima JSON. Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.
* Você pode usar **seu próprio cluster do HDInsight** em vez de usar um cluster do HDInsight sob demanda. Confira [Serviço vinculado do HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.
* Olá HDInsight cluster cria um **contêiner padrão** no armazenamento de blob Olá especificado no hello JSON (**linkedServiceName**). HDInsight não exclui esse contêiner quando Olá cluster é excluído. Este comportamento ocorre por design. Com o serviço de vinculado do HDInsight sob demanda, um cluster HDInsight é criado sempre que uma fatia é processada, a menos que haja um cluster existente de ao vivo (**timeToLive**) e é excluído quando Olá processamento é concluído.

    Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure. Se não precisar para solução de problemas de trabalhos de saudação, talvez você queira toodelete-os custos de armazenamento do tooreduce hello. nomes de saudação desses contêineres seguem um padrão: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Use ferramentas como [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com/) armazenamento de blobs de contêineres toodelete do Azure.

Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.

### <a name="inputdatasetjson"></a>inputdataset.json

```JSON
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

Olá JSON define um conjunto de dados chamado **AzureBlobInput**, que representa dados de entrada de uma atividade no pipeline de saudação. Além disso, ele especifica que os dados de entrada hello estão localizados no contêiner de blob Olá chamado **adfgetstarted** e Olá pasta chamada **inputdata**.

Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:

| Propriedade | Descrição |
|:--- |:--- |
| type |propriedade de tipo de saudação é definida tooAzureBlob porque os dados residem no armazenamento de BLOBs do Azure. |
| linkedServiceName |refere-se toohello StorageLinkedService criado anteriormente. |
| fileName |Essa propriedade é opcional. Se você omitir essa propriedade, todos os arquivos de saudação do hello folderPath são escolhidos. Nesse caso, somente Olá input.log é processado. |
| type |arquivos de log Olá estão no formato de texto, para que possamos usar TextFormat. |
| columnDelimiter |as colunas nos arquivos de log de saudação são delimitadas por um caractere de vírgula () |
| frequência/intervalo |frequência definida tooMonth e o intervalo é 1, o que significa que as fatias de entrada hello estarão disponíveis mensalmente. |
| externo |Essa propriedade é definida tootrue se os dados de entrada hello não são gerados pelo serviço da fábrica de dados hello. |

### <a name="outputdatasetjson"></a>outputdataset.json

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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

### <a name="pipelinejson"></a>pipeline.json
> [!IMPORTANT]
> Substitua **storageaccountname** pelo nome da sua conta de armazenamento do Azure.
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

No trecho JSON a saudação, você está criando um pipeline que consiste em uma única atividade que usa dados de tooprocess do Hive em um cluster HDInsight.

arquivo de script do Hive Hello, **partitionweblogs.hql**, é armazenado no hello conta de armazenamento do Azure (especificado por scriptLinkedService hello, chamado **StorageLinkedService**) e, na **script**  pasta no contêiner Olá **adfgetstarted**.

Olá **define** seção especifica as configurações de tempo de execução que são passadas script do hive toohello como valores de configuração do Hive (por exemplo ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).

Olá **iniciar** e **final** propriedades do pipeline de saudação especifica o período ativo de saudação do pipeline de saudação.

Atividade Olá JSON, você especificar esse script de Hive Olá é executado em computação Olá especificada pelo Olá **linkedServiceName** – **HDInsightOnDemandLinkedService**.

> [!NOTE]
> Consulte "JSON de Pipeline" [Pipelines e atividades do Azure Data Factory](data-factory-create-pipelines.md) para obter detalhes sobre as propriedades JSON usados em Olá anterior de exemplo.
>
>

## <a name="set-global-variables"></a>Definir variáveis globais
No Azure PowerShell, execute Olá comandos a seguir depois de substituir os valores hello com seu próprio:

> [!IMPORTANT]
> Veja a seção [Pré-requisitos](#prerequisites) para obter instruções sobre como obter a ID do cliente, o segredo do cliente, a ID do locatário e ID da assinatura.
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a>Autenticar com o AAD

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a>Criar um data factory
Nesta etapa, você criará um Azure Data Factory chamado **FirstDataFactoryREST**. Uma fábrica de dados pode ter um ou mais pipelines. Um pipeline em um data factory pode ter uma ou mais atividades. Por exemplo, um atividade de cópia toocopy dados de um repositório de dados de destino do código-fonte tooa e uma atividade de Hive do HDInsight toorun os dados de um Hive script tootransform. Execute Olá fábrica de dados de saudação de toocreate comandos a seguir:

1. Atribuir Olá comando toovariable chamado **cmd**.

    Confirmar esse nome Olá Olá da fábrica de dados especificadas aqui (ADFCopyTutorialDF) correspondências Olá nome especificado no hello **datafactory.json**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. Execute o comando hello usando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Exibir resultados de saudação. Se a fábrica de dados Olá foi criada com êxito, você vê Olá JSON Olá fábrica de dados em Olá **resultados**; caso contrário, você verá uma mensagem de erro.

    ```PowerShell
    Write-Host $results
    ```

Observe Olá pontos a seguir:

* nome de saudação do hello Azure Data Factory deve ser globalmente exclusivo. Se você vir o erro Olá nos resultados: **"FirstDataFactoryREST" nome da fábrica de dados não está disponível**, Olá seguintes etapas:
  1. Alterar nome da saudação (por exemplo, yournameFirstDataFactoryREST) em Olá **datafactory.json** arquivo. Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.
  2. No comando primeiro Olá Olá onde **$cmd** variável é atribuída a um valor, substitua FirstDataFactoryREST pelo novo nome de saudação e execute o comando de saudação.
  3. Execute Olá dois comandos tooinvoke Olá API REST toocreate Olá dados fábrica e impressão Olá resultados da operação de saudação.
* toocreate instâncias de fábrica de dados, você precisa toobe um colaborador/administrador de saudação assinatura do Azure
* nome Olá Olá da fábrica de dados pode ser registrado como um nome DNS no futuro de saudação e, portanto, se tornar publicamente visível.
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

Antes de criar um pipeline, é necessário toocreate algumas entidades da fábrica de dados pela primeira vez. Você primeiro criar dados de toolink serviços vinculados repositórios/calcula tooyour dados armazenam, definem a entrada e saída de dados de toorepresent de conjuntos de dados em repositórios de dados vinculados.

## <a name="create-linked-services"></a>Criar serviços vinculados
Nesta etapa, você pode vincular sua conta de armazenamento do Azure e uma fábrica de dados sob demanda do Azure HDInsight cluster tooyour. Olá conta de armazenamento do Azure mantém Olá dados de entrada e saídos para o pipeline de saudação neste exemplo. Olá serviço vinculado do HDInsight é toorun usado um script de Hive especificado na atividade de saudação do pipeline de saudação neste exemplo.

### <a name="create-azure-storage-linked-service"></a>Criar o serviço vinculado do armazenamento do Azure
Nesta etapa, você vincular sua fábrica de dados de tooyour de conta de armazenamento do Azure. Com este tutorial, você usar Olá mesma conta de armazenamento do Azure, dados de entrada/saída toostore e hello HQL arquivo de script.

1. Atribuir Olá comando toovariable chamado **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Execute o comando hello usando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Exibir resultados de saudação. Se Olá vinculado serviço foi criado com êxito, consulte Olá JSON para o serviço de saudação vinculado no hello **resultados**; caso contrário, você verá uma mensagem de erro.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a>Criar o serviço vinculado do Azure HDInsight
Nesta etapa, você vincular uma fábrica de dados sob demanda HDInsight cluster tooyour. cluster do HDInsight Olá é criado em tempo de execução e excluído após a conclusão ocioso e processamento para o período de tempo especificado Olá automaticamente. Você pode usar seu próprio cluster do HDInsight em vez de usar um cluster do HDInsight sob demanda. Veja [Serviços vinculados de computação](data-factory-compute-linked-services.md) para obter detalhes.

1. Atribuir Olá comando toovariable chamado **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. Execute o comando hello usando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Exibir resultados de saudação. Se Olá vinculado serviço foi criado com êxito, consulte Olá JSON para o serviço de saudação vinculado no hello **resultados**; caso contrário, você verá uma mensagem de erro.

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a>Criar conjuntos de dados
Nesta etapa, você cria conjuntos de dados toorepresent Olá entrada e saída de dados para o processamento do Hive. Esses conjuntos de dados Consulte toohello **StorageLinkedService** você tiver criado anteriormente neste tutorial. Olá tooan de pontos de serviço vinculado conta de armazenamento do Azure e conjuntos de dados especificam contêiner, pasta, nome do arquivo no armazenamento de saudação que contém a entrada e saída de dados.

### <a name="create-input-dataset"></a>Criar conjunto de dados de entrada
Nesta etapa, você deve criar hello conjunto de dados de entrada toorepresent entrada dados armazenados no armazenamento de BLOBs do Azure hello.

1. Atribuir Olá comando toovariable chamado **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. Execute o comando hello usando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Exibir resultados de saudação. Se Olá conjunto de dados foi criado com êxito, você verá hello JSON para o conjunto de dados Olá Olá **resultados**; caso contrário, você verá uma mensagem de erro.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a>Criar conjunto de dados de saída
Nesta etapa, você deve criar Olá saída conjunto toorepresent saída de dados armazenados em Olá armazenamento de BLOBs do Azure.

1. Atribuir Olá comando toovariable chamado **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. Execute o comando hello usando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Exibir resultados de saudação. Se Olá conjunto de dados foi criado com êxito, você verá hello JSON para o conjunto de dados Olá Olá **resultados**; caso contrário, você verá uma mensagem de erro.

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a>Criar um pipeline
Nesta etapa, você cria seu primeiro pipeline com a atividade **HDInsightHive** . Entrada fatia está disponível mensal (frequência: mês, intervalo: 1), fatias de saída é produzida mensal e Olá Agendador para a atividade de saudação é também definida toomonthly. Olá configurações para o conjunto de dados de saída de hello e Agendador de atividade de saudação devem corresponder. Atualmente, o conjunto de dados de saída é quais unidades Olá agendamento, então você deve criar um conjunto de dados de saída, mesmo que a atividade de saudação não produz nenhuma saída. Se a atividade de saudação não tem nenhuma entrada, você poderá ignorar o dataset de entrada hello criando.

Confirme que você vê Olá **input.log** arquivo hello **adfgetstarted/inputdata** pasta Olá armazenamento de BLOBs do Azure e execução Olá pipeline de saudação do comando toodeploy a seguir. Desde Olá **iniciar** e **final** horários são definidos no hello anterior e **isPaused** é conjunto toofalse, pipeline Olá execuções (atividade no pipeline de saudação) imediatamente após a implantação.

1. Atribuir Olá comando toovariable chamado **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. Execute o comando hello usando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Exibir resultados de saudação. Se Olá conjunto de dados foi criado com êxito, você verá hello JSON para o conjunto de dados Olá Olá **resultados**; caso contrário, você verá uma mensagem de erro.

    ```PowerShell
    Write-Host $results
    ```
4. Parabéns, você criou com sucesso seu primeiro pipeline usando o Azure PowerShell!

## <a name="monitor-pipeline"></a>Monitorar o pipeline
Nesta etapa, você deve usar fatias de toomonitor de API de REST de fábrica de dados produzidas pelo pipeline de saudação.

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> A criação de um cluster do HDInsight sob demanda geralmente leva algum tempo (20 minutos, aproximadamente). Portanto, espere Olá pipeline tootake **aproximadamente 30 minutos** tooprocess Olá fatia.
>
>

Executar Olá Invoke-Command e hello próximo até que você veja fatia Olá **pronto** estado ou **falha** estado. Quando a fatia hello está no estado pronto, verificar Olá **partitioneddata** pasta Olá **adfgetstarted** dados de saída do contêiner em seu armazenamento de blob para hello.  a criação de um cluster do HDInsight sob demanda Olá normalmente leva algum tempo.

![dados de saída](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> arquivo de entrada Hello é excluído quando a fatia de saudação é processada com êxito. Portanto, se você deseja toorerun Olá fatia ou Olá tutorial novamente, pasta de carregamento Olá arquivo de entrada (input.log) toohello inputdata do contêiner de adfgetstarted hello.
>
>

Você também pode usar fatias toomonitor portal do Azure e solucionar problemas. Veja os detalhes em [Monitorar pipelines usando o portal do Azure](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) .

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
| [Referência de API REST do Data Factory](/rest/api/datafactory/) |Consulte a documentação abrangente sobre os cmdlets do Data Factory |
| [Pipelines](data-factory-create-pipelines.md) |Este artigo ajuda você a entender os pipelines e atividades do Azure Data Factory e como toouse-los tooconstruct ponta a ponta controladas por dados fluxos de trabalho para seu cenário ou business. |
| [Conjunto de dados](data-factory-create-datasets.md) |Este artigo o ajuda a entender os conjuntos de dados no Azure Data Factory. |
| [Planejamento e execução](data-factory-scheduling-and-execution.md) |Este artigo explica os aspectos de programação e a execução de saudação do modelo de aplicativo do Azure Data Factory. |
| [Monitorar e gerenciar pipelines usando o Aplicativo de Monitoramento](data-factory-monitor-manage-app.md) |Este artigo descreve como toomonitor, gerenciar e depurar pipelines usando Olá monitoramento e gerenciamento de aplicativo. |
