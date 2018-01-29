---
title: "Copiar dados de maneira incremental usando o Controle de Alterações e o Azure Data Factory | Microsoft Docs"
description: "Neste tutorial, você deve criar um pipeline do Azure Data Factory que copie incrementalmente os dados delta de várias tabelas em um banco de dados do SQL Server local para um banco de dados SQL do Azure. "
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: d2cf578d6328e6e53d1081b9ab4de3ad262390df
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2018
---
# <a name="incrementally-load-data-from-azure-sql-database-to-azure-blob-storage-using-change-tracking-information"></a>Carregar incrementalmente os dados do Banco de Dados SQL do Azure para o Armazenamento de Blobs do Azure usando informações de controle de alterações 
Neste tutorial, você cria um data factory do Azure com um pipeline que carrega dados delta com base em informações de  **controle de alterações** no Banco de Dados SQL do Azure de origem para um armazenamento de blobs do Azure.  

Neste tutorial, você executa as seguintes etapas:

> [!div class="checklist"]
> * Prepare o armazenamento de dados de origem
> * Criar uma fábrica de dados.
> * Criar serviços vinculados. 
> * Crie conjuntos de dados de origem, coletor e de controle de alterações.
> * Criar, executar e monitorar o pipeline de cópia completo
> * Adicionar ou atualizar dados nas tabelas de origem
> * Criar, executar e monitorar o pipeline de cópia incremental

> [!NOTE]
> Este artigo aplica-se à versão 2 do Data Factory, que está atualmente em versão prévia. Se você estiver usando a versão 1 do serviço Data Factory, que já está disponível (GA), confira a [documentação do Data Factory versão 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="overview"></a>Visão geral
Em uma solução de integração de dados, o carregamento incremental de dados depois de uma carga de dados inicial é um cenário amplamente usado. Em alguns casos, os dados alterados dentro de um período em seu armazenamento de dados de origem podem ser facilmente divididos (por exemplo, LastModifyTime, CreationTime). Em alguns casos, não há uma forma explícita de identificar os dados delta da última vez que você processou os dados. A tecnologia de Controle de Alterações com suporte dos repositórios de dados, como o Banco de Dados SQL do Azure e SQL Server, pode ser usada para identificar os dados delta.  Este tutorial descreve como usar o Azure Data Factory versão 2 para trabalhar com a tecnologia de Controle de Alterações do SQL a fim de carregar incrementalmente os dados delta do Banco de Dados SQL do Azure no Armazenamento de Blobs do Azure.  Para obter informações mais concretas sobre a tecnologia de Controle de Alterações do SQL, consulte [Controle de alterações no SQL Server](/sql/relational-databases/track-changes/about-change-tracking-sql-server). 

## <a name="end-to-end-workflow"></a>Fluxos de trabalho completos
Estas são as etapas normais de fluxo de trabalho de ponta a ponta para carregar incrementalmente os dados usando a tecnologia de Controle de Alterações.

> [!NOTE]
> O Banco de Dados SQL do Azure e o SQL Server oferecem suporte à tecnologia de Controle de Alterações. Este tutorial usa o Banco de Dados SQL do Azure como o armazenamento de dados de origem. Você também pode usar um SQL Server local. 

1. **Carregamento inicial de dados históricos** (execução única):
    1. Habilite a tecnologia de Controle de Alterações no Banco de Dados SQL do Azure de origem.
    2. Obtenha o valor inicial de SYS_CHANGE_VERSION no Banco de Dados SQL do Azure como a linha de base para capturar os dados alterados.
    3. Carregue todos os dados do Banco de Dados SQL do Azure na conta de Armazenamento de Blobs do Azure. 
2. **Carregamento incremental de dados delta em uma agenda** (executar periodicamente após o carregamento inicial de dados):
    1. Obtenha os valores de SYS_CHANGE_VERSION antigos e novos.
    3. Carregue os dados delta unindo as chaves primárias de linhas alteradas (entre dois valores SYS_CHANGE_VERSION) de **sys.change_tracking_tables** com os dados na **tabela de origem** e, em seguida, mova os dados delta para destino.
    4. Atualize o SYS_CHANGE_VERSION para o carregamento de delta na próxima vez.

## <a name="high-level-solution"></a>Solução de alto nível
Neste tutorial, você cria dois pipelines que executam as duas operações a seguir:  

1. **Carregamento inicial:** crie um pipeline com uma atividade de cópia que copia todos os dados de armazenamento de dados de origem (Banco de Dados SQL do Azure) para o armazenamento de dados de destino (Armazenamento de Blobs do Azure).

    ![Carregamento completo dos dados](media/tutorial-incremental-copy-change-tracking-feature-powershell/full-load-flow-diagram.png)
1.  **Carga incremental:** crie um pipeline com as seguintes atividades e execute-o periodicamente. 
    1. Crie **duas atividades de pesquisa** para obter o SYS_CHANGE_VERSION novo e antigo do Banco de Dados SQL do Azure e passe-o para a atividade de cópia.
    2. Crie **uma atividade de cópia** para copiar os dados inseridos/atualizados/excluídos entre os dois valores SYS_CHANGE_VERSION do Banco de Dados SQL do Azure para o Armazenamento de Blobs do Azure.
    3. Crie **uma atividade de procedimento armazenado** para atualizar o valor de SYS_CHANGE_VERSION para a próxima execução do pipeline.

    ![Incrementar o diagrama de fluxo de carga](media/tutorial-incremental-copy-change-tracking-feature-powershell/incremental-load-flow-diagram.png)


Se você não tiver uma assinatura do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="prerequisites"></a>pré-requisitos
* PowerShell do Azure. Instale os módulos mais recentes do Azure PowerShell seguindo as instruções em [Como instalar e configurar o Azure PowerShell](/powershell/azure/install-azurerm-ps).
* **Banco de dados SQL do Azure**. Você usa o banco de dados como um armazenamento de dados de **origem**. Se você não tiver um Banco de Dados SQL do Azure, veja o artigo [Criar um Banco de Dados SQL do Azure](../sql-database/sql-database-get-started-portal.md) para conhecer as etapas para criar um.
* **Conta de Armazenamento do Azure**. Você usa o Armazenamento de Blobs como um armazenamento de dados de **coletor**. Se você não tiver uma conta de Armazenamento do Azure, veja o artigo [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) para conhecer as etapas para criar uma. Crie um contêiner denominado **adftutorial**. 

### <a name="create-a-data-source-table-in-your-azure-sql-database"></a>Criar uma tabela de fonte de dados no Banco de Dados SQL do Azure
1. Inicie o **SQL Server Management Studio** e conecte-se à réplica principal. 
2. No **Gerenciador de Servidores**, clique com o botão direito do mouse no **banco de dados** e escolha **Nova Consulta**.
3. Execute o comando SQL a seguir no Banco de Dados SQL do Azure para criar uma tabela chamada `data_source_table` como o repositório de fonte de dados.  
    
    ```sql
    create table data_source_table
    (
        PersonID int NOT NULL,
        Name varchar(255),
        Age int
        PRIMARY KEY (PersonID)
    );

    INSERT INTO data_source_table
        (PersonID, Name, Age)
    VALUES
        (1, 'aaaa', 21),
        (2, 'bbbb', 24),
        (3, 'cccc', 20),
        (4, 'dddd', 26),
        (5, 'eeee', 22);

    ```
4. Habilite o mecanismo de **Controle de Alterações** em seu banco de dados e na tabela de origem (data_source_table) executando a seguinte consulta SQL: 

    > [!NOTE]
    > - Substitua &lt;seu nome de banco de dados&gt; pelo nome do Banco de Dados SQL do Azure que tenha data_source_table. 
    > - Os dados alterados são mantidos por dois dias no exemplo atual. Se você carregar os dados alterados a cada três dias ou mais, alguns dados alterados não serão incluídos.  Você precisa de como alterar o valor de CHANGE_RETENTION para um número maior. Como alternativa, certifique-se de que seu período de carregamento dos dados alterados esteja dentro de dois dias. Para saber mais, consulte [Habilitar o controle de alterações de um banco de dados](/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server#enable-change-tracking-for-a-database)
 
    ```sql
    ALTER DATABASE <your database name>
    SET CHANGE_TRACKING = ON  
    (CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON)  
  
    ALTER TABLE data_source_table
    ENABLE CHANGE_TRACKING  
    WITH (TRACK_COLUMNS_UPDATED = ON)
    ```
5. Crie uma nova tabela e armazene o ChangeTracking_version com um valor padrão executando a consulta a seguir: 

    ```sql
    create table table_store_ChangeTracking_version
    (
        TableName varchar(255),
        SYS_CHANGE_VERSION BIGINT,
    );

    DECLARE @ChangeTracking_version BIGINT
    SET @ChangeTracking_version = CHANGE_TRACKING_CURRENT_VERSION();  

    INSERT INTO table_store_ChangeTracking_version
    VALUES ('data_source_table', @ChangeTracking_version)
    ```
    
    > [!NOTE]
    > Se os dados não forem alterados após a habilitação do controle de alterações para o Banco de Dados SQL, o valor da versão do controle de alterações será 0.
6. Execute a consulta a seguir para criar um procedimento armazenado em seu Banco de Dados SQL do Azure. O pipeline chama esse procedimento armazenado para atualizar a versão do controle de alteração na tabela criada na etapa anterior. 

    ```sql
    CREATE PROCEDURE Update_ChangeTracking_Version @CurrentTrackingVersion BIGINT, @TableName varchar(50)
    AS
    
    BEGIN
    
        UPDATE table_store_ChangeTracking_version
        SET [SYS_CHANGE_VERSION] = @CurrentTrackingVersion
    WHERE [TableName] = @TableName
    
    END    
    ```

### <a name="azure-powershell"></a>Azure PowerShell
Instale os módulos mais recentes do Azure PowerShell seguindo as instruções em [Como instalar e configurar o Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="create-a-data-factory"></a>Criar uma data factory
1. Defina uma variável para o nome do grupo de recursos que você usa nos comandos do PowerShell posteriormente. Copie o seguinte texto de comando para o PowerShell, especifique um nome para o [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) entre aspas duplas e, em seguida, execute o comando. Por exemplo: `"adfrg"`. 
   
     ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup";
    ```

    Se o grupo de recursos já existir, não convém substituí-lo. Atribua um valor diferente para a variável `$resourceGroupName` e execute o comando novamente
2. Defina uma variável para o local do data factory: 

    ```powershell
    $location = "East US"
    ```
3. Para criar o grupo de recursos do Azure, execute o seguinte comando: 

    ```powershell
    New-AzureRmResourceGroup $resourceGroupName $location
    ``` 
    Se o grupo de recursos já existir, não convém substituí-lo. Atribua um valor diferente para a variável `$resourceGroupName` e execute o comando novamente. 
3. Defina uma variável para o nome do data factory. 

    > [!IMPORTANT]
    >  Atualize o Nome do data factory para ser globalmente exclusivo.  

    ```powershell
    $dataFactoryName = "IncCopyChgTrackingDF";
    ```
5. Para criar o data factory, execute o cmdlet **Set-AzureRmDataFactoryV2** a seguir: 
    
    ```powershell       
    Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location $location -Name $dataFactoryName 
    ```

Observe os seguintes pontos:

* O nome da data factory do Azure deve ser globalmente exclusivo. Se você receber o erro a seguir, altere o nome e tente novamente.

    ```
    The specified Data Factory name 'ADFIncCopyChangeTrackingTestFactory' is already in use. Data Factory names must be globally unique.
    ```
* Para criar instâncias de Data Factory, a conta de usuário usada para fazer logon no Azure deve ser um membro das funções **colaborador** ou **proprietário**, ou um **administrador** da assinatura do Azure.
* Atualmente, o Data Factory versão 2 permite que você crie os data factories somente nas regiões Leste dos EUA, Leste dos EUA 2 e Europa Ocidental. Os armazenamentos de dados (Armazenamento do Azure, Banco de Dados SQL do Azure, etc.) e serviços de computação (HDInsight, etc.) usados pelo data factory podem estar em outras regiões.


## <a name="create-linked-services"></a>Criar serviços vinculados
Os serviços vinculados são criados em um data factory para vincular seus armazenamentos de dados e serviços de computação ao data factory. Nesta seção, você cria serviços vinculados para sua conta de Armazenamento do Azure e o Banco de Dados SQL do Azure. 

### <a name="create-azure-storage-linked-service"></a>Crie um serviço vinculado do Armazenamento do Azure.
Nesta etapa, você vincula a Conta de Armazenamento do Azure ao data factory.

1. Crie um arquivo JSON chamado **AzureStorageLinkedService.json** na pasta **C:\ADFTutorials\IncCopyChangeTrackingTutorial** com o seguinte conteúdo: (crie a pasta se ela ainda não existir). Antes de salvar o arquivo, substitua `<accountName>` e `<accountKey>` pelo nome e pela chave da sua conta de armazenamento do Azure, respectivamente.

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": {
                    "value": "DefaultEndpointsProtocol=https;AccountName=<accountName>;AccountKey=<accountKey>",
                    "type": "SecureString"
                }
            }
        }
    }
    ```
2. No **Azure PowerShell**, alterne para a pasta **C:\ADFTutorials\IncCopyChgTrackingTutorial**.
3. Execute o cmdlet **Set-AzureRmDataFactoryV2LinkedService** para criar o serviço vinculado **AzureStorageLinkedService**. No exemplo a seguir, você passa valores para os parâmetros **ResourceGroupName** e **DataFactoryName**. 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureStorageLinkedService" -File ".\AzureStorageLinkedService.json"
    ```

    Veja o exemplo de saída:

    ```json
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureStorageLinkedService
    ```

### <a name="create-azure-sql-database-linked-service"></a>Crie um serviço vinculado do Banco de Dados SQL do Azure.
Nesta etapa, você vincula o banco de dados SQL do Azure ao data factory.

1. Crie um arquivo JSON chamado **AzureSQLDatabaseLinkedService.json** na pasta **C:\ADFTutorials\IncCopyChangeTrackingTutorial** com o seguinte conteúdo: substitua **&lt; servidor&gt; &lt;nome do banco de dados&gt;, &lt;id de usuário&gt;, e &lt;senha&gt;** pelo nome do seu servidor SQL do Azure, o nome do banco de dados, a ID do usuário e a senha antes de salvar o arquivo. 

    ```json
    {
        "name": "AzureSQLDatabaseLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": {
                    "value": "Server = tcp:<server>.database.windows.net,1433;Initial Catalog=<database name>; Persist Security Info=False; User ID=<user name>; Password=<password>; MultipleActiveResultSets = False; Encrypt = True; TrustServerCertificate = False; Connection Timeout = 30;",
                    "type": "SecureString"
                }
            }
        }
    }
    ```
2. No **Azure PowerShell**, execute o cmdlet **Set-AzureRmDataFactoryV2LinkedService** para criar o serviço vinculado: **AzureSQLDatabaseLinkedService**. 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSQLDatabaseLinkedService" -File ".\AzureSQLDatabaseLinkedService.json"
    ```

    Veja o exemplo de saída:

    ```json
    LinkedServiceName : AzureSQLDatabaseLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDatabaseLinkedService
    ```

## <a name="create-datasets"></a>Criar conjuntos de dados
Nesta etapa, você cria conjuntos de dados para representar a fonte de dados, o destino de dados. e o local para armazenar o SYS_CHANGE_VERSION.

### <a name="create-a-source-dataset"></a>Criar um conjunto de dados de origem
Nesta etapa, você cria conjuntos de dados para representar os dados de origem. 

1. Crie um arquivo JSON denominado SourceDataset.json na mesma pasta, com o seguinte conteúdo: 

    ```json
    {
        "name": "SourceDataset",
        "properties": {
            "type": "AzureSqlTable",
            "typeProperties": {
                "tableName": "data_source_table"
            },
            "linkedServiceName": {
                "referenceName": "AzureSQLDatabaseLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }   
    ```

2.  Para criar o conjunto de dados SourceDataset, execute o cmdlet Set-AzureRmDataFactoryV2Dataset
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SourceDataset" -File ".\SourceDataset.json"
    ```

    Aqui está a amostra de saída do cmdlet:
    
    ```json
    DatasetName       : SourceDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset
    ```

### <a name="create-a-sink-dataset"></a>Criar um conjunto de dados de coletor
Nesta etapa, você cria um conjunto de dados para representar os dados copiados do armazenamento de dados de origem. 

1. Crie um arquivo JSON denominado SinkDataset.json na mesma pasta, com o seguinte conteúdo: 

    ```json
    {
        "name": "SinkDataset",
        "properties": {
            "type": "AzureBlob",
            "typeProperties": {
                "folderPath": "adftutorial/incchgtracking",
                "fileName": "@CONCAT('Incremental-', pipeline().RunId, '.txt')",
                "format": {
                    "type": "TextFormat"
                }
            },
            "linkedServiceName": {
                "referenceName": "AzureStorageLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }
    ```

    Você cria o contêiner adftutorial em seu Armazenamento de Blobs do Azure como parte dos pré-requisitos. Crie o contêiner caso ele não exista ou defina-o para o nome de um contêiner existente. Neste tutorial, o nome do arquivo de saída é gerado dinamicamente pelo uso da expressão: @CONCAT ('Incremental-', pipeline().RunId, '.txt').
2.  Para criar o conjunto de dados SinkDataset, execute o cmdlet Set-AzureRmDataFactoryV2Dataset
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SinkDataset" -File ".\SinkDataset.json"
    ```

    Aqui está a amostra de saída do cmdlet:
    
    ```json
    DatasetName       : SinkDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureBlobDataset
    ```

### <a name="create-a-change-tracking-dataset"></a>Criar um conjunto de dados de controle de alterações
Nesta etapa, você cria um conjunto de dados para armazenar a versão do controle de alterações.  

1. Crie um arquivo JSON denominado ChangeTrackingDataset.json na mesma pasta com o seguinte conteúdo: 

    ```json
    {
        "name": " ChangeTrackingDataset",
        "properties": {
            "type": "AzureSqlTable",
            "typeProperties": {
                "tableName": "table_store_ChangeTracking_version"
            },
            "linkedServiceName": {
                "referenceName": "AzureSQLDatabaseLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }
    ```

    Você pode criar a tabela table_store_ChangeTracking_version como parte dos pré-requisitos.
2.  Para criar o conjunto de dados WatermarkDataset, execute o cmdlet Set-AzureRmDataFactoryV2Dataset
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "ChangeTrackingDataset" -File ".\ChangeTrackingDataset.json"
    ```

    Aqui está a amostra de saída do cmdlet:
    
    ```json
    DatasetName       : ChangeTrackingDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset
    ```

## <a name="create-a-pipeline-for-the-full-copy"></a>Criar um pipeline para a cópia completa
Nesta etapa, crie um pipeline com uma atividade de cópia que copia todos os dados de armazenamento de dados de origem (Banco de Dados SQL do Azure) para o armazenamento de dados de destino (Armazenamento de Blobs do Azure).

1. Crie um arquivo JSON denominado FullCopyPipeline.json na mesma pasta, com o conteúdo a seguir: 

    ```json
    {
        "name": "FullCopyPipeline",
        "properties": {
            "activities": [{
                "name": "FullCopyActivity",
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
    
                "inputs": [{
                    "referenceName": "SourceDataset",
                    "type": "DatasetReference"
                }],
                "outputs": [{
                    "referenceName": "SinkDataset",
                    "type": "DatasetReference"
                }]
            }]
        }
    }
    ```
2. Execute o cmdlet Set-AzureRmDataFactoryV2Pipeline para criar o pipeline: FullCopyPipeline.
    
   ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "FullCopyPipeline" -File ".\FullCopyPipeline.json"
   ``` 

   Veja o exemplo de saída: 

   ```json
    PipelineName      : FullCopyPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Activities        : {FullCopyActivity}
    Parameters        :
   ```
 
### <a name="run-the-full-copy-pipeline"></a>Executar o pipeline de cópia completa
Execute o pipeline **FullCopyPipeline** usando o cmdlet **Invoke-AzureRmDataFactoryV2Pipeline**. 

```powershell
Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "FullCopyPipeline" -ResourceGroup $resourceGroupName -dataFactoryName $dataFactoryName        
``` 

### <a name="monitor-the-full-copy-pipeline"></a>Monitorar o pipeline de cópia completa

1. Faça logon no [portal do Azure](https://portal.azure.com).
2. Clique em **Mais serviços**, pesquise com a palavra-chave `data factories` e selecione **Data factories**. 

    ![Menu Data factories](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-data-factories-menu-1.png)
3. Procure **seu data factory** na lista de data factories e selecione-o para iniciar a página Data factory. 

    ![Procurar seu data factory](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-search-data-factory-2.png)
4. Na página Data factory, clique no bloco **Monitorar e Gerenciar**. 

    ![Bloco Monitorar e Gerenciar](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-monitor-manage-tile-3.png)    
5. O **Aplicativo de Integração de Dados** inicia em uma guia separada. Você pode ver todas as **execuções de pipeline** e seus status. Observe que, no exemplo a seguir, o status do pipeline de execução é **Com Êxito**. Você pode verificar os parâmetros passados para o pipeline ao clicar no link da coluna **Parâmetros**. Se houver um erro, você verá um link na coluna **Erro**. Clique no link na coluna **Ações**. 

    ![Execuções de pipeline](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-pipeline-runs-4.png)    
6. Quando você clicar no link na coluna **Ações**, verá a página a seguir, que mostra todas as **execuções de atividade** para o pipeline. 

    ![Execuções de atividade](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-activity-runs-5.png)
7. Para alternar novamente para a exibição **Pipeline é executado**, clique em **Pipelines** como mostrado na imagem. 


### <a name="review-the-results"></a>Revise os resultados
Você verá um arquivo chamado `incremental-<GUID>.txt` na pasta `incchgtracking` do contêiner `adftutorial`. 

![Arquivo de saída da cópia completa](media\tutorial-incremental-copy-change-tracking-feature-powershell\full-copy-output-file.png)

O arquivo deve ter os dados do Banco de Dados SQL do Azure:

```
1,aaaa,21
2,bbbb,24
3,cccc,20
4,dddd,26
5,eeee,22
```

## <a name="add-more-data-to-the-source-table"></a>Adicionar mais dados à tabela de origem

Execute a seguinte consulta no Banco de Dados SQL do Azure para adicionar uma linha e atualizar uma linha. 

```sql
INSERT INTO data_source_table
(PersonID, Name, Age)
VALUES
(6, 'new','50');


UPDATE data_source_table
SET [Age] = '10', [name]='update' where [PersonID] = 1

``` 

## <a name="create-a-pipeline-for-the-delta-copy"></a>Criar um pipeline para a cópia delta
Nesta etapa, você cria um pipeline com as seguintes atividades e execute-o periodicamente. As **atividades de pesquisa** obtêm o SYS_CHANGE_VERSION novo e antigo do Banco de Dados SQL do Azure e o passa para a atividade de cópia. A **atividade de cópia** copia os dados inseridos/atualizados/excluídos entre os dois valores SYS_CHANGE_VERSION do Banco de Dados SQL do Azure para o Armazenamento de Blobs do Azure. A **atividade de procedimento armazenado** atualiza o valor de SYS_CHANGE_VERSION para a próxima execução do pipeline.

1. Crie um arquivo JSON denominado IncrementalCopyPipeline.json na mesma pasta, com o conteúdo a seguir: 

    ```json
    {
            "name": "IncrementalCopyPipeline",
            "properties": {
                "activities": [
                {
                        "name": "LookupLastChangeTrackingVersionActivity",
                        "type": "Lookup",
                        "typeProperties": {
                        "source": {
                            "type": "SqlSource",
                            "sqlReaderQuery": "select * from table_store_ChangeTracking_version"
                            },
        
                            "dataset": {
                            "referenceName": "ChangeTrackingDataset",
                            "type": "DatasetReference"
                            }
                        }
                    },
                    {
                        "name": "LookupCurrentChangeTrackingVersionActivity",
                        "type": "Lookup",
                        "typeProperties": {
                            "source": {
                                "type": "SqlSource",
                                "sqlReaderQuery": "SELECT CHANGE_TRACKING_CURRENT_VERSION() as CurrentChangeTrackingVersion"
                        },
    
                            "dataset": {
                            "referenceName": "SourceDataset",
                            "type": "DatasetReference"
                            }
                        }
                    },
    
                    {
                        "name": "IncrementalCopyActivity",
                        "type": "Copy",
                        "typeProperties": {
                            "source": {
                                "type": "SqlSource",
                                "sqlReaderQuery": "select data_source_table.PersonID,data_source_table.Name,data_source_table.Age, CT.SYS_CHANGE_VERSION, SYS_CHANGE_OPERATION from data_source_table RIGHT OUTER JOIN CHANGETABLE(CHANGES data_source_table, @{activity('LookupLastChangeTrackingVersionActivity').output.firstRow.SYS_CHANGE_VERSION}) as CT on data_source_table.PersonID = CT.PersonID where CT.SYS_CHANGE_VERSION <= @{activity('LookupCurrentChangeTrackingVersionActivity').output.firstRow.CurrentChangeTrackingVersion}"
                            },
                            "sink": {
                                "type": "BlobSink"
                            }
                        },
                        "dependsOn": [
                            {
                                "activity": "LookupLastChangeTrackingVersionActivity",
                                "dependencyConditions": [
                                    "Succeeded"
                                ]
                            },
                            {
                                "activity": "LookupCurrentChangeTrackingVersionActivity",
                                "dependencyConditions": [
                                    "Succeeded"
                                ]
                        }
                        ],
        
                        "inputs": [
                            {
                            "referenceName": "SourceDataset",
                                "type": "DatasetReference"
                        }
                        ],
                        "outputs": [
                            {
                                "referenceName": "SinkDataset",
                                "type": "DatasetReference"
                            }
                        ]
                    },
        
                {
                        "name": "StoredProceduretoUpdateChangeTrackingActivity",
                        "type": "SqlServerStoredProcedure",
                        "typeProperties": {
    
                            "storedProcedureName": "Update_ChangeTracking_Version",
                            "storedProcedureParameters": {
                            "CurrentTrackingVersion": {"value": "@{activity('LookupCurrentChangeTrackingVersionActivity').output.firstRow.CurrentChangeTrackingVersion}", "type": "INT64" },
                                "TableName":  { "value":"@{activity('LookupLastChangeTrackingVersionActivity').output.firstRow.TableName}", "type":"String"}
                            }
                    },
        
                        "linkedServiceName": {
                        "referenceName": "AzureSQLDatabaseLinkedService",
                            "type": "LinkedServiceReference"
                        },
        
                        "dependsOn": [
                        {
                                "activity": "IncrementalCopyActivity",
                            "dependencyConditions": [
                                    "Succeeded"
                                ]
                            }
                        ]
                    }
                ]
        
            }
    }
    
    ```
2. Execute o cmdlet Set-AzureRmDataFactoryV2Pipeline para criar o pipeline: FullCopyPipeline.
    
   ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "IncrementalCopyPipeline" -File ".\IncrementalCopyPipeline.json"
   ``` 

   Veja o exemplo de saída: 

   ```json
    PipelineName      : IncrementalCopyPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Activities        : {LookupLastChangeTrackingVersionActivity, LookupCurrentChangeTrackingVersionActivity, IncrementalCopyActivity, StoredProceduretoUpdateChangeTrackingActivity}
    Parameters        :
   ```

### <a name="run-the-incremental-copy-pipeline"></a>Executar o pipeline de cópia incremental
Execute o pipeline **IncrementalCopyPipeline** usando o cmdlet **Invoke-AzureRmDataFactoryV2Pipeline**. 

```powershell
Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "IncrementalCopyPipeline" -ResourceGroup $resourceGroupName -dataFactoryName $dataFactoryName     
``` 


### <a name="monitor-the-incremental-copy-pipeline"></a>Monitorar o pipeline de cópia incremental
1. No **Aplicativo de Integração de Dados**, atualize a exibição de **execuções de pipeline**. Confirme que você vê o IncrementalCopyPipeline na lista. Clique no link na coluna **Ações**.  

    ![Execuções de pipeline](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-pipeline-runs-6.png)    
2. Quando você clicar no link na coluna **Ações**, verá a página a seguir, que mostra todas as **execuções de atividade** para o pipeline. 

    ![Execuções de atividade](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-activity-runs-7.png)
3. Para alternar novamente para a exibição **Pipeline é executado**, clique em **Pipelines** como mostrado na imagem. 

### <a name="review-the-results"></a>Revise os resultados
Você verá o segundo arquivo na pasta `incchgtracking` do contêiner `adftutorial`. 

![Arquivo de saída da cópia incremental](media\tutorial-incremental-copy-change-tracking-feature-powershell\incremental-copy-output-file.png)

O arquivo deve ter apenas os dados delta do Banco de Dados SQL do Azure. O registro com `U` é a linha atualizada no banco de dados, e `I` é aquele adicionado à linha. 

```
1,update,10,2,U
6,new,50,1,I
```
As três primeiras colunas são dados alterados do data_source_table. As duas últimas colunas são os metadados da tabela do sistema de controle de alterações. A quarta coluna é SYS_CHANGE_VERSION de cada linha alterada. A quinta coluna é a operação: U = atualização, I = inserir.  Para obter detalhes sobre as informações de controle de alterações, consulte [CHANGETABLE](/sql/relational-databases/system-functions/changetable-transact-sql). 

```
==================================================================
PersonID Name    Age    SYS_CHANGE_VERSION    SYS_CHANGE_OPERATION
==================================================================
1        update  10     2                     U
6        new     50     1                     I
```

    
## <a name="next-steps"></a>Próximas etapas
Avance para o tutorial a seguir para saber mais sobre como transformar dados usando um cluster Spark no Azure:

> [!div class="nextstepaction"]
>[Transformar dados usando o cluster Spark na nuvem](tutorial-transform-data-spark-powershell.md)



