---
title: "aaaCreate clusters de Hadoop sob demanda usando a fábrica de dados – HDInsight do Azure | Microsoft Docs"
description: Saiba como toocreate Hadoop sob demanda clusters de HDInsight usando o Azure Data Factory.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a>Criar clusters Hadoop sob demanda usando o Azure Data Factory
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

[O Azure Data Factory](../data-factory/data-factory-introduction.md) é um serviço de integração de dados com base em nuvem que orquestra e automatiza a movimentação de saudação e a transformação de dados. Ele pode criar um tooprocess de just-in-time do cluster HDInsight Hadoop uma fatia de dados de entrada e excluir o cluster hello quando Olá processamento é concluído. Alguns dos benefícios de saudação do uso de um cluster do Hadoop de HDInsight sob demanda são:

- Pagamento somente para trabalhos de timer hello está em execução Olá cluster HDInsight Hadoop (mais um breve tempo ocioso configurável). cobrança Olá para clusters de HDInsight é proporcional por minuto, se você estiver usando ou não. Quando você usa um serviço de vinculado do HDInsight sob demanda fábrica de dados, clusters de saudação são criados sob demanda. E clusters de saudação são excluídos automaticamente quando Olá trabalhos são concluídos. Portanto, você só paga pelo trabalho de saudação tempo e tempo ocioso breve hello (configuração de tempo de vida).
- Você pode criar um fluxo de trabalho usando um pipeline do Data Factory. Por exemplo, você pode ter dados de toocopy de pipeline de saudação de um tooan do SQL Server local armazenamento de BLOBs do Azure, dados de saudação do processo executando um script de Hive e um script do Pig em um cluster do Hadoop de HDInsight sob demanda. Em seguida, copie tooan de dados de resultado hello Azure SQL Data Warehouse para tooconsume de aplicativos de BI.
- Você pode agendar Olá fluxo de trabalho toorun periodicamente (por hora, diariamente, semanalmente, mensalmente, etc.).

No Azure Data Factory, um data factory pode ter um ou mais pipelines de dados. Um pipeline de dados tem uma ou mais atividades. Há dois tipos de atividades: [Atividades de Movimentação de Dados](../data-factory/data-factory-data-movement-activities.md) e [Atividades de Transformação de Dados](../data-factory/data-factory-data-transformation-activities.md). Você pode usar dados de toomove de atividades (atualmente, apenas copiar atividade) de movimentação de dados de um repositório de dados de destino fonte dados repositório tooa. Você usar dados de processo/tootransform de atividades de transformação de dados. Atividade de Hive do HDInsight é uma das atividades de transformação Olá suportadas pela fábrica de dados. Você pode usar atividades de transformação de Hive Olá neste tutorial.

Você pode configurar um toouse de atividade de hive seu próprio cluster HDInsight Hadoop ou um cluster do Hadoop de HDInsight sob demanda. Neste tutorial, hello atividade de Hive no pipeline da fábrica de dados Olá é configurado toouse um cluster do HDInsight sob demanda. Portanto, quando a atividade Olá executa tooprocess uma fatia de dados, aqui está o que acontece:

1. Um cluster HDInsight Hadoop é criado automaticamente para a fatia Olá tooprocess just-in-time.  
2. dados de entrada Hello são processados, executando um script HiveQL no cluster hello.
3. Olá cluster HDInsight Hadoop será excluída após Olá processamento é concluído e cluster Olá estiver ocioso por Olá configurado (timeToLive configuração) de tempo. Se a próxima fatia de dados hello está disponível para processamento nesse período ocioso timeToLive, hello mesmo cluster é usado tooprocess Olá fatia.  

Neste tutorial, Olá script HiveQL associada à atividade de hive Olá executa Olá ações a seguir:

1. Cria uma tabela externa referências Olá dados de log web bruto armazenados em um armazenamento de BLOBs do Azure.
2. Dados brutos de saudação de partições por ano e mês.
3. Repositórios Olá dados particionados em Olá armazenamento de BLOBs do Azure.

Neste tutorial, Olá script HiveQL associada à atividade de hive Olá cria uma tabela externa referências Olá dados de log de web bruto armazenados em Olá armazenamento de BLOBs do Azure. Aqui estão as linhas de exemplo de saudação para cada mês no arquivo de entrada hello.

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

partições de script HiveQL Olá Olá dados brutos por ano e mês. Ele cria três pastas de saída com base na entrada de saudação anterior. Cada pasta contém um arquivo com entradas de cada mês.

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

Para obter uma lista de atividades de transformação de dados de fábrica de dados na atividade de tooHive de adição, consulte [transformar e analisar o uso do Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> No momento, você só pode criar o cluster HDInsight versão 3.2 do Azure Data Factory.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar a instruções Olá neste artigo, você deve ter Olá itens a seguir:

* [Assinatura do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* PowerShell do Azure.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a>Preparar a conta de armazenamento
Você pode usar as contas de armazenamento toothree neste cenário:

- conta de armazenamento padrão para o cluster do HDInsight Olá
- conta de armazenamento para dados de entrada hello
- conta de armazenamento para dados de saída de saudação

tutorial de saudação toosimplify, você usar uma conta tooserve Olá três fins de armazenamento. script de exemplo do PowerShell do Azure Olá encontrado nesta seção executa Olá tarefas a seguir:

1. Faça logon em tooAzure.
2. Crie um grupo de recursos do Azure.
3. Criar uma conta do Armazenamento do Azure.
4. Criar um contêiner de Blob na conta de armazenamento de saudação
5. Copie Olá dois contêiner de Blob de toohello arquivos a seguir:

   * Arquivo de dados de entrada: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)
   * Script HiveQL: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)

     Os dois arquivos são armazenados em um contêiner de Blob público.


**tooprepare Olá armazenamento e copiar Olá arquivos usando o Azure PowerShell:**
> [!IMPORTANT]
> Especifique os nomes de grupo de recursos do Azure hello e conta de armazenamento do Azure Olá que será criada pelo script hello.
> Anote **nome do grupo de recursos**, **nome da conta de armazenamento**, e **chave da conta de armazenamento** gerados por script hello. Necessário na próxima seção, Olá.

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

Se você precisar de ajuda com script do PowerShell hello, consulte [hello usando o PowerShell do Azure com o armazenamento do Azure](../storage/common/storage-powershell-guide-full.md). Se você deseja toouse CLI do Azure em vez disso, consulte Olá [apêndice](#appendix) seção para Olá script CLI do Azure.

**conteúdo de saudação e de conta de armazenamento de saudação do tooexamine**

1. Logon toohello [portal do Azure](https://portal.azure.com).
2. Clique em **grupos de recursos** no painel esquerdo da saudação.
3. Clique duas vezes no nome do grupo de recursos Olá criado em seu script do PowerShell. Use o filtro de saudação se você tiver muitos grupos de recursos listados.
4. Em Olá **recursos** lado a lado, você deve ter um recurso listado, a menos que você compartilhar o grupo de recursos de saudação com outros projetos. Esse recurso é a conta de armazenamento de saudação com nome hello especificado anteriormente. Clique no nome de conta de armazenamento hello.
5. Clique em Olá **Blobs** lado a lado.
6. Clique em Olá **adfgetstarted** contêiner. Você verá duas pastas: **inputdata** e **script**.
7. Abra a pasta de saudação e verifique arquivos Olá Olá das pastas. Olá inputdata contém o arquivo de input.log de saudação com dados de entrada e a pasta de scripts Olá contém o arquivo de script hello HiveQL.

## <a name="create-a-data-factory-using-resource-manager-template"></a>Criar um data factory usando o modelo do Resource Manager
Com conta de armazenamento hello, dados de entrada hello e Olá script HiveQL preparado, você estará pronto toocreate uma fábrica de dados do Azure. Há vários métodos para criar um data factory. Neste tutorial, você pode criar uma fábrica de dados implantando um modelo de Gerenciador de recursos do Azure usando Olá portal do Azure. Você também pode implantar um modelo do Resource Manager usando a [CLI do Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) e o [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template). Para conferir outros métodos de criação de data factory, consulte [Tutorial: compilar seu primeiro data factory](../data-factory/data-factory-build-your-first-pipeline.md).

1. Clique em Olá toosign de imagem no tooAzure e modelo do Gerenciador de recursos de saudação abrir no portal do Azure de saudação a seguir. modelo de saudação está localizado em https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json. Consulte Olá [entidades da fábrica de dados no modelo de saudação](#data-factory-entities-in-the-template) seção para obter informações detalhadas sobre as entidades definidas no modelo de saudação. 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Selecione **usar existente** opção Olá **grupo de recursos** configuração e o nome de select Olá Olá do grupo de recursos criado na etapa anterior de saudação (usando o script do PowerShell).
3. Insira um nome para a fábrica de dados da saudação (**nome da fábrica de dados**). Esse nome deve ser globalmente exclusivo.
4. Digite hello **nome da conta de armazenamento** e **chave da conta de armazenamento** você anotou na etapa anterior hello.
5. Selecione **concordo toohello termos e condições** indicado acima, após a leitura por meio de **termos e condições**.
6. Selecione **toodashboard Pin** opção.
6. Clique em **Comprar/Criar**. Você vê um bloco na Olá painel chamado **implantação de modelo de implantação**. Aguarde até que a saudação **grupo de recursos** folha para seu grupo de recursos é aberto. Você também pode clicar em bloco Olá intitulado como a recurso grupo nome tooopen Olá grupo folha de recursos do.
6. Clique em grupo de recursos de saudação do hello bloco tooopen se folha de grupo de recursos de saudação não ainda estiver aberta. Agora você deverá ver que um recurso de fábrica de dados mais além listados toohello recurso de conta de armazenamento.
7. Clique em nome de saudação da sua fábrica de dados (valor especificado para Olá **nome da fábrica de dados** parâmetro).
8. Na folha de fábrica de dados de saudação, clique em Olá **diagrama** lado a lado. diagrama de saudação mostra uma atividade com um conjunto de dados de entrada e um conjunto de dados de saída:

    ![Diagrama de pipeline de atividade do hive HDInsight sob demanda do Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    Olá nomes são definidos no modelo do Gerenciador de recursos de saudação.
9. Clique duas vezes em **AzureBlobOutput**.
10. Em Olá **recente atualizado fatias**, você deverá ver uma fatia. Se o status de saudação é **em andamento**, aguarde até que seja alterado muito**pronto**. Geralmente demora cerca de **20 minutos** toocreate um cluster HDInsight.

### <a name="check-hello-data-factory-output"></a>Verifique a saída de fábrica de dados Olá

1. Use Olá mesmo procedimento Olá última sessão toocheck Olá contêiner de saudação adfgetstarted contêiner. Há dois novos contêineres além muito**adfgetsarted**:

   * Um contêiner com o nome que segue o padrão de saudação: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`. Esse contêiner é o contêiner de padrão de Olá para o cluster do HDInsight hello.
   * adfjobs: este contêiner é o contêiner de saudação para logs de trabalho Olá ADF.

     Olá saída de fábrica de dados é armazenada em **afgetstarted** conforme configurado no modelo do Gerenciador de recursos de saudação.
2. Clique em **adfgetstarted**.
3. Clique duas vezes em **partitioneddata**. Você verá um **ano = 2014** pasta porque todos os logs da web hello com data no ano de 2014.

    ![Saída do pipeline de atividade do hive HDInsight sob demanda do Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    Se você fazer drill down lista hello, você deverá ver três pastas para janeiro, fevereiro e março. E há um log para cada mês.

    ![Saída do pipeline de atividade do hive HDInsight sob demanda do Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a>Entidades da fábrica de dados no modelo de saudação
Aqui está como modelo de Gerenciador de recursos nível superior Olá para uma fábrica de dados se parece com:

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a>Definir Data Factory
Você pode definir uma fábrica de dados no modelo do Gerenciador de recursos de saudação conforme Olá exemplo a seguir:  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
Olá dataFactoryName é o nome de Olá Olá da fábrica de dados que especifique quando você implanta o modelo de saudação. Fábrica de dados está atualmente só tem suporte em regiões Leste dos EUA, oeste dos EUA e Europa Setentrional de saudação.

### <a name="defining-entities-within-hello-data-factory"></a>Definir entidades dentro de fábrica de dados Olá
Hello seguintes entidades da fábrica de dados estão definidas no modelo JSON hello:

* [Serviço vinculado de armazenamento do Azure](#azure-storage-linked-service)
* [Serviço vinculado do HDInsight sob demanda](#hdinsight-on-demand-linked-service)
* [Conjunto de dados de entrada de Blob do Azure](#azure-blob-input-dataset)
* [Conjunto de dados de saída do blob do Azure](#azure-blob-output-dataset)
* [Pipeline com a Atividade de cópia](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Serviço vinculado de armazenamento do Azure
saudação de armazenamento do Azure vinculada links de serviço sua fábrica de dados de toohello de conta de armazenamento do Azure. Neste tutorial, hello mesma conta de armazenamento é usada como conta de armazenamento de HDInsight saudação padrão, o armazenamento de dados de entrada e o armazenamento de dados de saída. Portanto, você define somente um serviço vinculado do Armazenamento do Azure. Na definição de serviço Olá vinculado, você pode especificar nome hello e a chave da sua conta de armazenamento do Azure. Consulte [serviço vinculado do armazenamento do Azure](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter detalhes sobre o JSON propriedades usadas toodefine um armazenamento do Azure serviço vinculado.

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
Olá **connectionString** usa Olá parâmetros storageAccountName e storageAccountKey. Você pode especificar valores para esses parâmetros durante a implantação de modelo de saudação.  

#### <a name="hdinsight-on-demand-linked-service"></a>Serviço vinculado do HDInsight sob demanda
Olá HDInsight sob demanda vinculado definição de serviço, você especificar valores para parâmetros de configuração que são usados por Olá toocreate de serviço de fábrica de dados um HDInsight Hadoop de cluster em tempo de execução. Consulte [serviços vinculados de computação](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) artigo para obter detalhes sobre o JSON propriedades usadas toodefine um serviço vinculado do HDInsight sob demanda.  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
Observe Olá pontos a seguir:

* Olá fábrica de dados cria um **baseados em Linux** cluster HDInsight para você.
* Olá cluster HDInsight Hadoop é criado no hello mesma região da conta de armazenamento hello.
* Saudação de aviso *timeToLive* configuração. fábrica de dados Olá exclui cluster Olá automaticamente depois que o cluster Olá ficar ocioso por 30 minutos.
* Olá HDInsight cluster cria um **contêiner padrão** no armazenamento de blob Olá especificado no hello JSON (**linkedServiceName**). HDInsight não exclui esse contêiner quando Olá cluster é excluído. Este comportamento ocorre por design. Com o serviço de vinculado do HDInsight sob demanda, um cluster HDInsight é criado sempre que precisa de uma fatia toobe processado a menos que haja um cluster existente de ao vivo (**timeToLive**) e é excluído quando Olá processamento é concluído.

Confira [Serviço vinculado do HDInsight sob demanda](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.

> [!IMPORTANT]
> Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure. Se não precisar para solução de problemas de trabalhos de saudação, talvez você queira toodelete-os custos de armazenamento do tooreduce hello. nomes de saudação desses contêineres seguem um padrão: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Use ferramentas como [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com/) armazenamento de blobs de contêineres toodelete do Azure.

#### <a name="azure-blob-input-dataset"></a>Conjunto de dados de entrada de Blob do Azure
Na definição de conjunto de dados de entrada hello, você deve especificar nomes de saudação do contêiner de blob, a pasta e o arquivo que contém os dados de entrada hello. Consulte [propriedades de conjunto de dados de Blob do Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um conjunto de dados de Blob do Azure.

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
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

Observe Olá configurações específicas na definição do hello JSON a seguir:

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a>Conjunto de dados de saída de Blob do Azure
Na definição de conjunto de dados de saída de hello, você especificar nomes de saudação do contêiner de blob e a pasta que contém os dados de saída de hello. Consulte [propriedades de conjunto de dados de Blob do Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um conjunto de dados de Blob do Azure.  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

Olá folderPath Especifica a pasta de toohello de caminho de saudação que mantém os dados de saída de hello:

```json
"folderPath": "adfgetstarted/partitioneddata",
```

Olá [conjunto de dados disponibilidade](../data-factory/data-factory-create-datasets.md#dataset-availability) configuração é o seguinte:

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

Fábrica de dados do Azure, saída do pipeline de saudação de unidades de disponibilidade de conjunto de dados. Neste exemplo, a fatia de saudação é produzida mensal no Olá último dia do mês (EndOfInterval). Para saber mais, confira [Agendamento e execução do Data Factory](../data-factory/data-factory-scheduling-and-execution.md).

#### <a name="data-pipeline"></a>Pipeline de dados
Você define um pipeline que transforma dados executando o script Hive em um cluster do Azure HDInsight sob demanda. Consulte [JSON de Pipeline](../data-factory/data-factory-create-pipelines.md#pipeline-json) para obter descrições dos elementos usados de JSON toodefine um pipeline neste exemplo.

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
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
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

pipeline de saudação contém uma atividade, atividade de HDInsightHive. Como as datas de início e término são em janeiro de 2016, os dados de apenas um mês (uma fatia) são processados. Ambos *iniciar* e *final* de atividade de saudação têm uma data passada, portanto Olá fábrica de dados processa os dados para o mês de saudação imediatamente. Se a fim de saudação é uma data futura, fábrica de dados Olá cria outra fatia quando chegar a hora da saudação. Para saber mais, confira [Agendamento e execução do Data Factory](../data-factory/data-factory-scheduling-and-execution.md).

## <a name="clean-up-hello-tutorial"></a>Limpar tutorial Olá

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a>Exclua os contêineres de blob Olá criados pelo cluster do HDInsight sob demanda
Com o serviço de vinculado do HDInsight sob demanda, um cluster HDInsight é criado sempre que precisa de uma fatia toobe processado a menos que haja um cluster existente ao vivo (timeToLive); e cluster Olá é excluído quando Olá processamento é concluído. Para cada cluster, o Azure Data Factory cria um contêiner de blob no hello usado como conta de armazenamento padrão Olá para cluster Olá de armazenamento de BLOBs do Azure. Mesmo que o cluster HDInsight é excluído, contêiner de armazenamento de blob saudação padrão e a conta de armazenamento de saudação associada não são excluídos. Este comportamento ocorre por design. Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure. Se não precisar para solução de problemas de trabalhos de saudação, talvez você queira toodelete-os custos de armazenamento do tooreduce hello. nomes de saudação desses contêineres seguem um padrão: `adfyourdatafactoryname-linkedservicename-datetimestamp`.

Excluir Olá **adfjobs** e **adfyourdatafactoryname-linkedservicename-datetimestamp** pastas. contêiner de adfjobs Olá contém logs de trabalho do Azure Data Factory.

### <a name="delete-hello-resource-group"></a>Excluir grupo de recursos de saudação
[Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md) é usado toodeploy, gerenciar e monitorar sua solução como um grupo.  Excluir um grupo de recursos exclui todos os componentes de Olá Olá grupo.  

1. Logon toohello [portal do Azure](https://portal.azure.com).
2. Clique em **grupos de recursos** no painel esquerdo da saudação.
3. Clique no nome de grupo de recursos Olá criado em seu script do PowerShell. Use o filtro de saudação se você tiver muitos grupos de recursos listados. Ele abre o grupo de recursos de saudação em uma nova folha.
4. Em Olá **recursos** lado a lado, você deverá ter conta de armazenamento padrão hello e Olá data factory listado, a menos que você compartilhar o grupo de recursos de saudação com outros projetos.
5. Clique em **excluir** na parte superior de saudação da folha de saudação. Isso exclui a conta de armazenamento hello e dados de Olá armazenados na conta de armazenamento de saudação.
6. Insira a exclusão de tooconfirm nome do grupo de recursos hello e, em seguida, clique em **excluir**.

Caso você não quiser conta de armazenamento toodelete hello quando você excluir o grupo de recursos hello, considere Olá seguir arquitetura separando dados de negócios Olá Olá padrão da conta de armazenamento. Nesse caso, ter um grupo de recursos para conta de armazenamento Olá com dados de negócios hello e Olá outro grupo de recursos para conta de armazenamento padrão Olá HDInsight vinculado hello e serviço de fábrica de dados. Quando você exclui um segundo grupo de recursos hello, ele não afeta o conta de armazenamento de dados de negócios de saudação. toodo para:

* Adicione Olá toohello grupo de recursos de nível superior com hello Microsoft.DataFactory/datafactories recursos em seu modelo do Gerenciador de recursos a seguir. Ele cria uma conta de armazenamento:

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* Adicione uma novo serviço vinculado toohello de ponto de nova conta de armazenamento:

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* Configure Olá HDInsight sob demanda vinculado serviço com um dependsOn adicional e um additionalLinkedServiceNames:

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como toouse toocreate de fábrica de dados do Azure sob demanda HDInsight cluster tooprocess trabalhos Hive. tooread mais:

* [Tutorial do Hadoop: introdução ao uso do Hadoop baseado em Linux no HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Criar clusters Hadoop baseados em Linux em HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Documentação do HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Documentação do data factory](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a>Apêndice

### <a name="azure-cli-script"></a>Script da CLI do Azure
Você pode usar a CLI do Azure em vez de usar o tutorial do Azure PowerShell toodo hello. toouse CLI do Azure, primeiro instale CLI do Azure de acordo com a saudação instruções a seguir:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a>Usar o armazenamento do Azure CLI tooprepare hello e copiar arquivos de saudação

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

nome de contêiner de saudação é *adfgetstarted*. Mantenha-o como está. Caso contrário, será necessário o modelo do tooupdate Olá Gerenciador de recursos. Se você precisar de ajuda com esse script CLI, consulte [hello usando a CLI do Azure com o armazenamento do Azure](../storage/common/storage-azure-cli.md).
