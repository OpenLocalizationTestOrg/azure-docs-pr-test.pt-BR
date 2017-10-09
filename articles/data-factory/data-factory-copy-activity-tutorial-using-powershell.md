---
title: 'Tutorial: Criar um pipeline de dados de toomove usando o PowerShell do Azure | Microsoft Docs'
description: "Neste tutorial, você cria um pipeline do Azure Data Factory com uma Atividade de Cópia usando o Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a>Tutorial: criar um pipeline do Data Factory que move os dados usando o Azure PowerShell
> [!div class="op_single_selector"]
> * [Visão geral e pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md)
> * [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modelo do Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API do .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

Neste artigo, você aprenderá como toouse PowerShell toocreate uma fábrica de dados com um pipeline que copia dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure. Se você estiver tooAzure nova fábrica de dados, leia Olá [tooAzure Introdução Data Factory](data-factory-introduction.md) artigo antes de fazer este tutorial.   

Neste tutorial, você criará um pipeline com uma atividade: atividade de cópia. Olá Copiar atividade copia dados de um repositório de dados com suporte de dados repositório tooa coletor com suporte. Para obter uma lista de armazenamentos de dados com suporte como origens e coletores, confira [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats). atividade de saudação é alimentada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável. Para obter mais informações sobre hello atividade de cópia, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md).

Um pipeline pode ter mais de uma atividade. E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada. Para saber mais, confira [Várias atividades em um pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> Este artigo não aborda todos os cmdlets da fábrica de dados hello. Consulte a [Referência de Cmdlet do Data Factory](/powershell/module/azurerm.datafactories) para ter uma documentação completa sobre esses cmdlets.
> 
> pipeline de dados Olá neste tutorial copia dados de um repositório de dados de destino fonte dados repositório tooa. Para obter um tutorial sobre como tootransform dados usando a fábrica de dados do Azure, consulte [Tutorial: Crie um pipeline de dados tootransform usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Pré-requisitos
- Conclua os pré-requisitos listados em Olá [pré-requisitos do tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artigo.
- Instale o **Azure PowerShell**. Siga as instruções de saudação em [como tooinstall e configurar o Azure PowerShell](../powershell-install-configure.md).

## <a name="steps"></a>Etapas
Aqui estão as etapas Olá que fazem parte deste tutorial:

1. Crie um **data factory** do Azure. Nesta etapa, você cria um data factory denominado ADFTutorialDataFactoryPSH. 
2. Criar **serviços vinculados** na fábrica de dados hello. Nesta etapa, você criará dois serviços vinculados de tipos: banco de dados SQL e armazenamento do Azure. 
    
    Olá AzureStorageLinkedService vincula sua fábrica de dados de toohello de conta de armazenamento do Azure. Você criou um contêiner e carregados conta de armazenamento toothis dados como parte de [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService vincula sua fábrica de dados de toohello de banco de dados do SQL Azure. Olá dados são copiados do armazenamento de blob Olá são armazenados neste banco de dados. Você criou uma tabela SQL no banco de dados como parte dos [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   
3. Criar a entrada e saída **conjuntos de dados** na fábrica de dados hello.  
    
    serviço de armazenamento do Azure vinculado Olá Especifica a cadeia de conexão de Olá usada pelo serviço de fábrica de dados em tempo de execução tooconnect tooyour conta de armazenamento do Azure. E, conjunto de dados de blob de entrada hello Especifica o contêiner de saudação e a pasta de saudação que contém os dados de entrada hello.  

    Da mesma forma, Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução. Além disso, conjunto de dados da tabela SQL Olá saída Especifica a tabela Olá Olá toowhich Olá de banco de dados armazenamento de blob Olá é copiada.
4. Criar um **pipeline** na fábrica de dados hello. Nesta etapa, você cria um pipeline com a atividade de cópia.   
    
    Olá Copiar atividade copia dados de um blob na tabela de tooa de armazenamento de BLOBs do Azure de Olá no banco de dados do SQL Azure hello. Você pode usar uma atividade de cópia em um pipeline toocopy os dados de qualquer destino tooany suportada de origem com suporte. Para obter uma lista de armazenamentos de dados com suporte, confira o artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
5. Pipeline de saudação do monitor. Nesta etapa, você **monitor** Olá fatias de conjuntos de dados de entrada e saídas usando o PowerShell.

## <a name="create-a-data-factory"></a>Criar uma data factory
> [!IMPORTANT]
> Concluída [pré-requisitos para o tutorial Olá](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) se você ainda não tiver feito isso.   

Uma fábrica de dados pode ter um ou mais pipelines. Um pipeline em um data factory pode ter uma ou mais atividades. Por exemplo, dados de toocopy uma atividade de cópia de um repositório de dados de destino do código-fonte tooa e uma atividade de Hive do HDInsight toorun um tootransform de script do Hive dados de saída de tooproduct dados de entrada. Vamos começar com a criação de fábrica de dados Olá nesta etapa.

1. Inicie o **PowerShell**. Mantenha o Azure PowerShell aberta até o fim deste tutorial hello. Se você fecha e reabrir o, será necessário comandos de saudação toorun novamente.

    Execute Olá comando a seguir e insira o nome de usuário de saudação e a senha que você use toosign em toohello portal do Azure:

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    Execute todas as assinaturas de saudação para esta conta de Olá tooview de comando a seguir:

    ```PowerShell
    Get-AzureRmSubscription
    ```

    Execute Olá assinatura de saudação do comando tooselect que você deseja toowork com a seguir. Substituir  **&lt;NameOfAzureSubscription** &gt; com o nome da saudação de sua assinatura do Azure:

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. Criar um grupo de recursos do Azure denominado **ADFTutorialResourceGroup** executando Olá comando a seguir:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    Algumas das etapas neste tutorial Olá pressupõem que você use o grupo de recursos de saudação chamado **ADFTutorialResourceGroup**. Se você usar um grupo de recursos diferentes, será necessário toouse-lo no lugar de ADFTutorialResourceGroup neste tutorial.
3. Executar Olá **New-AzureRmDataFactory** toocreate cmdlet uma fábrica de dados denominada **ADFTutorialDataFactoryPSH**:  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    Esse nome pode já ter sido usado. Portanto, tornar nome Olá Olá da fábrica de dados exclusivo, adicionando um prefixo ou sufixo (por exemplo: ADFTutorialDataFactoryPSH05152017) e execute novamente o comando hello.  

Observe Olá pontos a seguir:

* nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo. Se você receber Olá erro a seguir, altere o nome de saudação (por exemplo, yournameADFTutorialDataFactoryPSH). Use esse nome em vez de ADFTutorialFactoryPSH ao executar as etapas neste tutorial. Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver os artefatos do Data Factory.

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* toocreate instâncias de fábrica de dados, você deve ser um colaborador ou o administrador de saudação assinatura do Azure.
* nome Olá Olá da fábrica de dados pode ser registrado como um nome DNS no hello futuro e, portanto, se tornar publicamente visível.
* Você pode receber Olá erro a seguir: "**esta assinatura não está registrado toouse namespace DataFactory.**" Execute um dos seguintes hello e tente publicar novamente:

  * No Azure PowerShell, execute Olá provedor do comando tooregister Olá fábrica de dados a seguir:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    Olá execução tooconfirm de comando que Olá provedor de fábrica de dados a seguir está registrado:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Entrar usando Olá assinatura do Azure toohello [portal do Azure](https://portal.azure.com). Vá tooa folha de fábrica de dados ou criar uma fábrica de dados no hello portal do Azure. Esta ação registra automaticamente o provedor de saudação para você.

## <a name="create-linked-services"></a>Criar serviços vinculados
Você pode criar serviços vinculados em um toolink de fábrica de dados seus dados, armazena e fábrica de dados toohello de serviços de computação. Neste tutorial, você não usa serviços de computação, como o Azure HDInsight ou o Azure Data Lake Analytics. Você usa dois armazenamentos de dados do tipo Armazenamento do Azure (origem) e o banco de dados SQL (destino). 

Portanto, você pode criar dois serviços vinculados, chamados AzureStorageLinkedService e AzureSqlLinkedService, dos tipos: AzureStorage e AzureSqlDatabase.  

Olá AzureStorageLinkedService vincula sua fábrica de dados de toohello de conta de armazenamento do Azure. Esta conta de armazenamento é hello um no qual você criou um contêiner e carregou dados de saudação como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService vincula sua fábrica de dados de toohello de banco de dados do SQL Azure. Olá dados são copiados do armazenamento de blob Olá são armazenados neste banco de dados. Você criou tabela emp de saudação neste banco de dados como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a>Criar um serviço vinculado para uma conta de armazenamento do Azure
Nesta etapa, você vincular sua fábrica de dados de tooyour de conta de armazenamento do Azure.

1. Crie um arquivo JSON chamado **AzureStorageLinkedService.json** na **C:\ADFGetStartedPSH** pasta com hello conteúdo a seguir: (criar hello pasta ADFGetStartedPSH se ele ainda não existir.)

    > [!IMPORTANT]
    > Substituir &lt;accountname&gt; e &lt;accountkey&gt; com o nome e a chave da sua conta de armazenamento do Azure antes de salvar o arquivo hello. 

    ```json
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
2. Em **Azure PowerShell**, alternar toohello **ADFGetStartedPSH** pasta.
4. Executar Olá **New-AzureRmDataFactoryLinkedService** serviço vinculado do cmdlet toocreate Olá: **AzureStorageLinkedService**. Esse cmdlet e outros cmdlets de fábrica de dados que você usar este tutorial requer que você toopass valores para Olá **ResourceGroupName** e **DataFactoryName** parâmetros. Como alternativa, você pode passar o objeto de DataFactory de saudação retornado o cmdlet New-AzureRmDataFactory Olá sem digitar ResourceGroupName e DataFactoryName toda vez que você executar um cmdlet. 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    Aqui está a saída de exemplo hello:

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    Outra maneira de criar esse serviço vinculado é toospecify nome do grupo de recursos e o nome da fábrica de dados em vez de especificar o objeto de DataFactory hello.  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a>Criar um serviço vinculado para um banco de dados SQL do Azure
Nesta etapa, você vincular sua fábrica de dados de tooyour de banco de dados do SQL Azure.

1. Crie um arquivo JSON chamado AzureSqlLinkedService.json na pasta C:\ADFGetStartedPSH com hello seguindo conteúdo:

    > [!IMPORTANT]
    > Substitua &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; e &lt;password&gt; pelos nomes de seu servidor SQL do Azure, banco de dados, conta de usuário e senha.
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. Execute um serviço vinculado de saudação toocreate de comando a seguir:

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    Aqui está a saída de exemplo hello:

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   Confirme se **permitir acesso a serviços tooAzure** configuração está ativada para o servidor de banco de dados SQL. tooverify e ativá-lo, Olá seguintes etapas:

    1. Faça logon no toohello [portal do Azure](https://portal.azure.com)
    2. Clique em **mais serviços >** Olá esquerda e clique em **servidores SQL** em Olá **bancos de dados** categoria.
    3. Selecione o servidor na lista de saudação de SQL servers.
    4. Na folha saudação do SQL server, clique em **Mostrar configurações de firewall** link.
    5. Em Olá **configurações de Firewall** folha, clique em **ON** para **permitir acesso a serviços tooAzure**.
    6. Clique em **salvar** na barra de ferramentas de saudação. 

## <a name="create-datasets"></a>Criar conjuntos de dados
Na etapa anterior de saudação, você criou serviços vinculados toolink sua conta de armazenamento do Azure e a fábrica de dados de tooyour de banco de dados do SQL Azure. Nesta etapa, você definirá dois conjuntos de dados denominados InputDataset OutputDataset que representam a entrada e saída dados e que são armazenados em repositórios de dados Olá referenciados por AzureStorageLinkedService e AzureSqlLinkedService, respectivamente.

serviço de armazenamento do Azure vinculado Olá Especifica a cadeia de conexão de Olá usada pelo serviço de fábrica de dados em tempo de execução tooconnect tooyour conta de armazenamento do Azure. E, Olá o conjunto de dados de blob de entrada (InputDataset) Especifica o contêiner de saudação e a pasta de saudação que contém os dados de entrada hello.  

Da mesma forma, Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução. E, Olá saída SQL o conjunto de dados de tabela (OututDataset) Especifica a tabela de saudação em Olá Olá de toowhich de banco de dados dados saudação do armazenamento de blob são copiados. 

### <a name="create-an-input-dataset"></a>Criar um conjunto de dados de entrada
Nesta etapa, você criar um conjunto de dados chamado InputDataset que aponta o arquivo de blob tooa (emp.txt) na pasta raiz de saudação de um contêiner de blob (adftutorial) no hello representado por Olá AzureStorageLinkedService vinculado de serviço de armazenamento do Azure. Se você não especificar um valor para o nome de arquivo hello (ou ignorá-lo), dados de todos os blobs na pasta de entrada hello são copiados toohello destino. Neste tutorial, você deve especificar um valor para o nome de arquivo hello.  

1. Crie um arquivo JSON chamado **InputDataset.json** em Olá **C:\ADFGetStartedPSH** pasta com hello conteúdo a seguir:

    ```json
    {
        "name": "InputDataset",
        "properties": {
            "structure": [
                {
                    "name": "FirstName",
                    "type": "String"
                },
                {
                    "name": "LastName",
                    "type": "String"
                }
            ],
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "emp.txt",
                "folderPath": "adftutorial/",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```

    Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:

    | Propriedade | Descrição |
    |:--- |:--- |
    | type | propriedade do tipo Hello está definida muito**AzureBlob** porque os dados residem em um armazenamento de BLOBs do Azure. |
    | linkedServiceName | Refere-se toohello **AzureStorageLinkedService** que você criou anteriormente. |
    | folderPath | Especifica o blob Olá **contêiner** e hello **pasta** que contém blobs de entrada. Neste tutorial, adftutorial é o contêiner de blob hello e pasta é a pasta raiz de saudação. | 
    | fileName | Essa propriedade é opcional. Se você omitir essa propriedade, todos os arquivos de saudação folderPath são escolhidos. Neste tutorial, **emp.txt** é especificado para hello fileName, portanto, somente esse arquivo é escolhida para processamento. |
    | formato -> tipo |arquivo de entrada Hello está no formato de texto de saudação, para que possamos usar **TextFormat**. |
    | columnDelimiter | saudação de colunas no arquivo de entrada hello é delimitadas por **caractere de vírgula (`,`)**. |
    | frequência/intervalo | frequência de saudação está definida muito**hora** e o intervalo é definido muito**1**, que significa que Olá entrada fatias estão disponíveis **por hora**. Em outras palavras, Olá serviço da fábrica de dados procura por dados de entrada a cada hora na pasta raiz de saudação do contêiner de blob (**adftutorial**) especificado. Ele procura os dados de saudação em Olá pipeline início e término vezes, não antes ou depois desses tempos.  |
    | externo | Essa propriedade é definida, muito**true** se os dados de saudação não são gerados por este pipeline. dados de entrada Hello neste tutorial estão no arquivo de emp.txt hello, que não é gerado por este pipeline, portanto vamos definir essa propriedade tootrue. |

    Para saber mais sobre essas propriedades JSON, confira o [artigo sobre o conector do Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties).
2. Execute Olá o conjunto de dados do comando toocreate Olá fábrica de dados a seguir.

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    Aqui está a saída de exemplo hello:

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a>Criar um conjunto de dados de saída
Nesta parte da etapa hello, você cria um conjunto de dados de saída denominado **OutputDataset**. Este conjunto de dados aponta tooa SQL tabela no banco de dados do SQL Azure Olá representado por **AzureSqlLinkedService**. 

1. Crie um arquivo JSON chamado **OutputDataset.json** em Olá **C:\ADFGetStartedPSH** pasta com hello conteúdo a seguir:

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "structure": [
                {
                    "name": "FirstName",
                    "type": "String"
                },
                {
                    "name": "LastName",
                    "type": "String"
                }
            ],
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

    Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:

    | Propriedade | Descrição |
    |:--- |:--- |
    | type | propriedade do tipo Hello está definida muito**AzureSqlTable** porque os dados são copiados tooa tabela em um banco de dados do SQL Azure. |
    | linkedServiceName | Refere-se toohello **AzureSqlLinkedService** que você criou anteriormente. |
    | tableName | Olá especificado **tabela** toowhich Olá dados são copiados. | 
    | frequência/intervalo | Olá frequência é definida muito**hora** e o intervalo é **1**, o que significa que Olá fatias de saída são produzidas **por hora** entre Olá pipeline início e término vezes, não antes ou Após esses horários.  |

    Há três colunas – **ID**, **FirstName**, e **LastName** – na tabela de emp Olá no banco de dados de saudação. ID é uma coluna de identidade, portanto, você precisa apenas toospecify **FirstName** e **LastName** aqui.

    Para saber mais sobre essas propriedades JSON, confira o [artigo sobre o conector do SQL](data-factory-azure-sql-connector.md#dataset-properties).
2. Execute Olá comando toocreate Olá dados fábrica conjunto de dados a seguir.

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    Aqui está a saída de exemplo hello:

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a>Criar uma pipeline
Nesta etapa, você cria um pipeline com uma **atividade de cópia** que usa **InputDataset** como entrada e **OutputDataset** como saída.

Atualmente, o conjunto de dados de saída é quais unidades Olá agenda. Neste tutorial, o conjunto de dados de saída é configurado tooproduce uma fatia de uma vez por hora. pipeline de saudação tem uma hora de início e a hora de término que são um dia de distância, que é de 24 horas. Portanto, 24 fatias de conjunto de dados de saída são produzidas pelo pipeline de saudação. 


1. Crie um arquivo JSON chamado **ADFTutorialPipeline.json** em Olá **C:\ADFGetStartedPSH** pasta com hello conteúdo a seguir:

    ```json   
    {
      "name": "ADFTutorialPipeline",
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
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```
    Observe Olá pontos a seguir:
   
    - Na seção de atividades hello, há apenas uma atividade cuja **tipo** está definido muito**cópia**. Para obter mais informações sobre a atividade de cópia hello, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md). Nas soluções de Data Factory, você também pode usar [atividades de transformação de dados](data-factory-data-transformation-activities.md).
    - Entrada para atividade de saudação é definida muito**InputDataset** e de saída para o conjunto de hello atividade é muito**OutputDataset**. 
    - Em Olá **typeProperties** seção, **BlobSource** é especificado como tipo de fonte hello e **SqlSink** é especificado como tipo de coletor de saudação. Para obter uma lista completa de armazenamentos de dados de atividade de cópia hello como origens e coletores com suporte, consulte [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn como toouse dados específicos com suporte são armazenados como um fonte/coletor, clique o link de saudação na tabela de saudação.  
     
    Substituir valor Olá Olá **iniciar** propriedade com hello dia atual e **final** valor com hello dia seguinte. Você pode especificar apenas parte da data hello e ignore a parte de hora de saudação da saudação data hora. Por exemplo, "2016-02-03", que é o equivalente muito "2016-02-03T00:00:00Z"
     
    Ambos os valores de data/hora de início e de término devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por exemplo: 2016-10-14T16:32:41Z. Olá **final** tempo é opcional, mas usamos neste tutorial. 
     
    Se você não especificar o valor para Olá **final** propriedade, ele é calculado como "**início + 48 horas**". pipeline de saudação toorun indefinidamente, especifique **9999-09-09** como valor Olá Olá **final** propriedade.
     
    Olá anterior de exemplo, há 24 fatias de dados como cada fatia de dados é produzida por hora.

    Para obter descrições das propriedades JSON em uma definição de pipeline, consulte o artigo [Criar pipelines](data-factory-create-pipelines.md). Para obter descrições das propriedades JSON em uma definição de atividade de cópia, consulte [Atividades de movimentação de dados](data-factory-data-movement-activities.md). Para obter descrições das propriedades JSON com suporte pelo BlobSource, consulte o [artigo sobre o conector de blobs do Azure](data-factory-azure-blob-connector.md). Para obter descrições das propriedades JSON com suporte pelo SqlSink, consulte o [artigo sobre o conector do Banco de Dados SQL](data-factory-azure-sql-connector.md).
2. Execute Olá comando toocreate Olá dados fábrica a tabela a seguir.

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    Aqui está a saída de exemplo hello: 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

**Parabéns!** Você criou com êxito uma fábrica de dados do Azure com um pipeline toocopy os dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure. 

## <a name="monitor-hello-pipeline"></a>Pipeline de saudação do monitor
Nesta etapa, você use toomonitor do PowerShell do Azure que está acontecendo em uma fábrica de dados do Azure.

1. Substituir &lt;DataFactoryName&gt; com o nome da saudação de fábrica de dados e executar **Get-AzureRmDataFactory**e atribuir Olá saída tooa $df variável.

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    Por exemplo:
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    Em seguida, execute o conteúdo Olá impressão $df toosee Olá saída a seguir: 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. Executar **Get-AzureRmDataFactorySlice** tooget detalhes sobre todas as fatias de saudação **OutputDataset**, que é o conjunto de dados de saída de saudação do pipeline de saudação.  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   Essa configuração deve corresponder a saudação **iniciar** valor em JSON de pipeline hello. Você deve ver 24 fatias, uma para cada hora de 12 AM de saudação dia atual too12 estou de saudação dia seguinte.

   Aqui estão os três intervalos de exemplo de saída de hello: 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Executar **Get-AzureRmDataFactoryRun** tooget detalhes de saudação da atividade for executada por um **específico** fatia. Copie o valor de data e hora de saudação da saída Olá Olá comando toospecify Olá valor anterior para o parâmetro de StartDateTime hello. 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   Aqui está a saída de exemplo hello: 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

Para obter uma documentação abrangente sobre os cmdlets de Data Factory, consulte [Referência de cmdlet de Data Factory](/powershell/module/azurerm.datafactories).

## <a name="summary"></a>Resumo
Neste tutorial, você criou um Azure fábrica toocopy dados de um banco de dados do SQL Azure de tooan BLOBs do Azure. Você usou a fábrica de dados do PowerShell toocreate hello, serviços vinculados, conjuntos de dados e um pipeline. Aqui estão as etapas de alto nível Olá executada neste tutorial:  

1. Foi criada uma **data factory**do Azure.
2. Foram criados **serviços vinculados**:

   a. Um **armazenamento do Azure** vinculado serviço toolink sua conta de armazenamento do Azure que contém dados de entrada.     
   b. Um **SQL Azure** vinculado serviço toolink banco de dados SQL que contém dados de saída de saudação.
3. Foram criados **conjuntos de dados** que descrevem os dados de entrada e de saída para os pipelines.
4. Criado um **pipeline** com **atividade de cópia**, com **BlobSource** como origem hello e **SqlSink** como coletor hello.

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você usou o armazenamento de blobs do Azure como um armazenamento de dados de origem e um banco de dados SQL do Azure como um armazenamento de dados de destino em uma operação de cópia. Olá tabela a seguir fornece uma lista de repositórios de dados com suporte como origens e destinos de atividade de cópia de saudação: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn sobre como armazenam dados toocopy para/de uma data, clique o link Olá Olá repositório de dados na tabela de saudação. 

