---
title: aaaSQL atividade de procedimento armazenado do servidor
description: "Saiba como você pode usar o hello atividade de procedimento armazenado do SQL Server tooinvoke um procedimento armazenado em um banco de dados do SQL Azure ou Azure SQL Data Warehouse de um pipeline da fábrica de dados."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a>Atividade de procedimento armazenado do SQL Server
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Atividade de Hive](data-factory-hive-activity.md) 
> * [Atividade Pig](data-factory-pig-activity.md)
> * [Atividade MapReduce](data-factory-map-reduce.md)
> * [Atividade de Transmissão do Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Atividade do Spark](data-factory-spark.md)
> * [Atividade de Execução em Lote do Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Atividade do Recurso de Atualização do Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Atividade de Procedimento Armazenado](data-factory-stored-proc-activity.md)
> * [Atividade do U-SQL do Data Lake Analytics](data-factory-usql-activity.md)
> * [Atividade Personalizada do .NET](data-factory-use-custom-activities.md)

## <a name="overview"></a>Visão geral
Use atividades de transformação de dados em uma fábrica de dados [pipeline](data-factory-create-pipelines.md) tootransform e processar dados brutos em previsões e ideias. Hello atividade de procedimento armazenado é uma das atividades de transformação de saudação que dá suporte a fábrica de dados. Este artigo aproveita Olá [atividades de transformação de dados](data-factory-data-transformation-activities.md) artigo, que apresenta uma visão geral de transformação de dados e atividades de transformação de saudação tem suportada na fábrica de dados.

Você pode usar o hello atividade de procedimento armazenado tooinvoke um procedimento armazenado em um dos seguintes dados de saudação armazena em sua empresa ou em uma máquina virtual do Azure (VM): 

- Banco de Dados SQL do Azure
- SQL Data Warehouse do Azure
- Banco de Dados do SQL Server.  Se você estiver usando o SQL Server, instale o Gateway de gerenciamento de dados no mesmo computador que hospeda Olá banco de dados ou em um computador separado que tem o banco de dados do access toohello de saudação. O Gateway de Gerenciamento de Dados é um componente que conecta fontes de dados locais ou em uma VM do Azure a serviços de nuvem de maneira segura e gerenciada. Consulte o artigo [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md) para obter detalhes.

> [!IMPORTANT]
> Ao copiar dados em um banco de dados do SQL Azure ou o SQL Server, você pode configurar Olá **SqlSink** na atividade de cópia tooinvoke um procedimento armazenado usando Olá **sqlWriterStoredProcedureName** propriedade. Para obter mais informações, consulte [Invocar um procedimento armazenado por meio da atividade de cópia](data-factory-invoke-stored-procedure-from-copy-activity.md). Para obter detalhes sobre a propriedade hello, veja a seguir os artigos de conector: [banco de dados do SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [do SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). Não há suporte para invocar um procedimento armazenado ao copiar dados em um SQL Data Warehouse do Azure usando uma atividade de cópia. Porém, você pode usar tooinvoke atividade de procedimento armazenada de saudação um procedimento armazenado em um SQL Data Warehouse. 
>  
> Ao copiar dados de banco de dados do SQL Azure ou o SQL Server ou o Azure SQL Data Warehouse, você pode configurar **SqlSource** na atividade de cópia tooinvoke um procedimento armazenado tooread os dados de banco de dados de origem de saudação usando Olá  **sqlReaderStoredProcedureName** propriedade. Para obter mais informações, consulte Olá seguintes artigos de conector: [banco de dados do SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [do SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          


Olá, seguindo as instruções passo a passo usa hello atividade de procedimento armazenado em um pipeline tooinvoke um procedimento armazenado em um banco de dados do SQL Azure. 

## <a name="walkthrough"></a>Passo a passo
### <a name="sample-table-and-stored-procedure"></a>Tabela de exemplo e procedimento armazenado
1. Crie seguinte Olá **tabela** em seu banco de dados SQL usando o SQL Server Management Studio ou qualquer outra ferramenta que você estiver familiarizado com o. coluna de datetimestamp Olá é date de hello e hora em que a ID correspondente Olá é gerado.

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    ID exclusivo Olá identificado de Olá datetimestamp está date de hello e hora em que a ID correspondente Olá é gerado.
    
    ![Dados de amostra](./media/data-factory-stored-proc-activity/sample-data.png)

    Neste exemplo, procedimento armazenado de saudação está em um banco de dados do SQL Azure. Se hello procedimento armazenado está em um Data warehouse do SQL Azure e o banco de dados do SQL Server, a abordagem de saudação é semelhante. Para um Banco de Dados do SQL Server, você deve instalar um [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md).
2. Crie seguinte Olá **procedimento armazenado** que insere dados na toohello **sampletable**.

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > **Nome** e **maiusculas e minúsculas** de saudação (DateTime neste exemplo) do parâmetro deve corresponder de parâmetro especificado em Olá pipeline/atividade JSON. Olá a definição do procedimento armazenado no, certifique-se de que  **@**  é usado como um prefixo para o parâmetro hello.

### <a name="create-a-data-factory"></a>Criar uma data factory
1. Faça logon no muito[portal do Azure](https://portal.azure.com/).
2. Clique em **novo** no menu esquerdo Olá **Intelligence + análise**e clique em **fábrica de dados**.

    ![Novo data factory](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. Em Olá **nova fábrica de dados** folha, digite **SProcDF** para Olá nome. Os nomes do Azure Data Factory são **globalmente exclusivos**. Você precisará tooprefix nome de Olá Olá da fábrica de dados com seu nome, tooenable Olá êxito na criação da fábrica de saudação.

   ![Novo data factory](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. Selecione sua **assinatura do Azure**.
5. Para **grupo de recursos**, siga um destes Olá etapas a seguir:
   1. Clique em **criar novo** e insira um nome para o grupo de recursos de saudação.
   2. Clique em **Usar existente** e selecione um grupo de recursos existente.  
6. Selecione Olá **local** Olá fábrica de dados.
7. Selecione **toodashboard Pin** para que possa ver fábrica de dados de saudação no painel de saudação próxima vez que você efetuar logon.
8. Clique em **criar** em Olá **nova fábrica de dados** folha.
9. Você verá a fábrica de dados hello está sendo criada no hello **painel** de saudação portal do Azure. Depois de fábrica de dados Olá tiver sido criada com êxito, você ver a página de fábrica de dados hello, que mostra Olá conteúdo Olá da fábrica de dados.

   ![Home page do Data Factory](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a>Criar um serviço vinculado do SQL do Azure
Depois de criar a fábrica de dados hello, crie um serviço vinculado do SQL Azure que vincula o banco de dados do SQL Azure, que contém a tabela de sampletable hello e procedimento armazenado de sp_sample, tooyour fábrica de dados.

1. Clique em **autor e implantar** em Olá **Data Factory** folha para **SProcDF** toolaunch Olá Editor da fábrica de dados.
2. Clique em **novo repositório de dados** Olá barra de comandos e escolha **banco de dados do SQL Azure**. Você deve ver Olá script JSON para a criação de um SQL do Azure vinculada serviço no editor de saudação.

   ![Novo armazenamento de dados](media/data-factory-stored-proc-activity/new-data-store.png)
3. No hello script JSON, faça as seguintes alterações de saudação:

   1. Substituir `<servername>` com nome de saudação do seu servidor de banco de dados SQL.
   2. Substituir `<databasename>` com banco de dados de saudação em que você criou tabela hello e hello procedimento armazenado.
   3. Substituir `<username@servername>` com conta de usuário de saudação que tem o banco de dados do access toohello.
   4. Substituir `<password>` com senha Olá Olá conta de usuário.

      ![Novo armazenamento de dados](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. toodeploy Olá serviço vinculado, clique em **implantar** na barra de comandos de saudação. Confirme que você vê Olá AzureSqlLinkedService na árvore de saudação exibir hello esquerda.

    ![modo de exibição de árvore com serviço vinculado](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a>Criar um conjunto de dados de saída
Você deve especificar um conjunto de dados de saída para uma atividade de procedimento armazenado mesmo que o procedimento armazenado de saudação não produz nenhum dado. Isso ocorre porque Olá seu conjunto de dados que orienta a agenda de saudação da atividade de saudação (frequência hello atividade é executada - hora, diariamente, etc.) de saída. Olá conjunto de dados de saída deve usar um **serviço vinculado** que se refere a tooan banco de dados do SQL Azure ou um Azure SQL Data Warehouse ou um banco de dados do SQL Server no qual você deseja Olá toorun do procedimento armazenado. Olá conjunto de dados de saída pode servir como um resultado do modo toopass Olá do procedimento armazenado de saudação para processamento subsequente por outra atividade ([encadeamento atividades](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) no pipeline de saudação. No entanto, fábrica de dados não gravará automaticamente saída Olá de um conjunto de dados do procedimento armazenado toothis. É Olá tabela gravações tooa SQL que Olá pontos do conjunto de dados de saída de procedimento armazenado. Em alguns casos, o conjunto de dados de saída de hello pode ser um **conjunto de dados fictício** (um conjunto de dados que aponta tooa tabela que não tem saída de hello procedimento armazenado). Este conjunto de dados fictício é usado somente para atividade de procedimento armazenado de agendamento de saudação toospecify para executar a saudação. 

1. Clique em **... Mais** na barra de ferramentas hello, clique em **novo conjunto de dados**e clique em **SQL Azure**. **Novo conjunto de dados** no comando Olá barra e selecione **SQL Azure**.

    ![modo de exibição de árvore com serviço vinculado](media/data-factory-stored-proc-activity/new-dataset.png)
2. Saudação de copiar/colar o script JSON no editor de JSON toohello a seguir.

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy Olá conjunto de dados, clique em **implantar** na barra de comandos de saudação. Confirme que você vê Olá conjunto de dados na exibição de árvore de saudação.

    ![modo de exibição de árvore com serviços vinculados](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a>Criar um pipeline com atividade de SqlServerStoredProcedure
Agora, vamos criar um pipeline com uma atividade de procedimento armazenado. 

Observe Olá propriedades a seguir: 

- Olá **tipo** propriedade for definida muito**SqlServerStoredProcedure**. 
- Olá **storedProcedureName** no tipo de propriedades está definido muito**sp_sample** (nome da saudação procedimento armazenado).
- Olá **storedProcedureParameters** seção contém um parâmetro denominado **DataTime**. Nome e o uso de maiusculas e minúsculas do parâmetro hello em JSON devem corresponder Olá nome e o uso de maiusculas e minúsculas do parâmetro hello na definição do procedimento armazenada de saudação. Se você precisar passar null para um parâmetro, use a sintaxe de saudação: `"param1": null` (todas as minúsculas).
 
1. Clique em **... Mais** Olá barra de comandos e clique em **novo pipeline**.
2. Saudação de copiar/colar trecho JSON a seguir:   

    ```JSON
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
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. pipeline de saudação toodeploy, clique em **implantar** na barra de ferramentas de saudação.  

### <a name="monitor-hello-pipeline"></a>Pipeline de saudação do monitor
1. Clique em **X** tooclose Editor da fábrica de dados folhas toonavigate fazer toohello folha de fábrica de dados e clique em **diagrama**.

    ![bloco do diagrama](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. Em Olá **exibição de diagrama**, consulte uma visão geral dos pipelines hello e conjuntos de dados usados neste tutorial.

    ![bloco do diagrama](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. Na exibição de diagrama de Olá, clique duas vezes em dataset Olá `sprocsampleout`. Você verá fatias Olá no estado pronto. Deve haver cinco fatias porque uma fatia é produzida para cada hora entre a hora de início de saudação e a hora de término da saudação JSON.

    ![bloco do diagrama](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. Quando uma fatia está em **pronto** estado, execute uma `select * from sampletable` consulta Olá tooverify de banco de dados de SQL do Azure que Olá dados foi inserida na tabela de toohello pelo procedimento armazenado de saudação.

   ![Dados de saída](./media/data-factory-stored-proc-activity/output.png)

   Consulte [pipeline de saudação do Monitor](data-factory-monitor-manage-pipelines.md) para obter informações detalhadas sobre o monitoramento do Azure Data Factory pipelines.  


## <a name="specify-an-input-dataset"></a>Especificar um conjunto de dados de entrada
Passo a passo hello, atividade de procedimento armazenado não tem quaisquer conjuntos de dados de entrada. Se você especificar um conjunto de dados de entrada, hello atividade de procedimento armazenado não será executado até que a fatia de saudação do conjunto de dados de entrada está disponível (no estado pronto). saudação de conjunto de dados pode ser um conjunto de dados externo (que não é produzido por outra atividade no hello mesmo pipeline) ou um conjunto de dados interno que é produzido por uma atividade de upstream (atividade de saudação executada antes que essa atividade). Você pode especificar vários conjuntos de dados de entrada para a atividade de procedimento armazenada de saudação. Se você fizer isso, hello atividade de procedimento armazenado é executado somente quando todas as fatias de conjunto de dados de entrada hello estão disponíveis (no estado pronto). Olá conjunto de dados de entrada não pode ser consumido no procedimento Olá armazenado como um parâmetro. É apenas dependência de saudação toocheck usado antes de atividade de procedimento armazenado de saudação inicial.

## <a name="chaining-with-other-activities"></a>Encadeando com outras atividades
Se você quiser toochain uma atividade de upstream com essa atividade, Especifica saída de saudação da atividade de upstream hello como uma entrada dessa atividade. Quando você fizer isso, hello atividade de procedimento armazenado não executado até a conclusão da atividade de upstream hello e Olá o conjunto de dados de saída da atividade de upstream hello está disponível (em status Pronto). Você pode especificar conjuntos de dados de saída de várias atividades de upstream como conjuntos de dados de entrada da atividade de procedimento armazenada de saudação. Ao fazer isso, a atividade de procedimento armazenado de saudação é executado somente quando todas as fatias de conjunto de dados de entrada hello estão disponíveis.  

No hello exemplo a seguir, a saída de saudação da atividade de cópia de saudação é: atividade de procedimento armazenado de OutputDataset, que é uma entrada de saudação. Portanto, hello atividade de procedimento armazenado não será executado até hello atividade de cópia é concluída e a fatia de OutputDataset hello está disponível (no estado pronto). Se você especificar vários conjuntos de dados de entrada, hello atividade de procedimento armazenado não será executado até que todas as fatias de conjunto de dados de entrada hello estão disponíveis (no estado pronto). Olá conjuntos de dados de entrada não podem ser usados diretamente como atividade de procedimento armazenado de toohello de parâmetros. 

Para obter mais informações sobre atividades de encadeamento, consulte [várias atividades em um pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

Da mesma forma, toolink Olá repositório de atividade de procedimento com **atividades downstream** (Olá as atividades que executam após hello atividade de procedimento armazenado), especifique Olá o conjunto de dados de saída da atividade de procedimento Olá armazenado como um entrada de atividade de downstream Olá no pipeline de saudação.

> [!IMPORTANT]
> Ao copiar dados em um banco de dados do SQL Azure ou o SQL Server, você pode configurar Olá **SqlSink** na atividade de cópia tooinvoke um procedimento armazenado usando Olá **sqlWriterStoredProcedureName** propriedade. Para obter mais informações, consulte [Invocar um procedimento armazenado por meio da atividade de cópia](data-factory-invoke-stored-procedure-from-copy-activity.md). Para obter detalhes sobre a propriedade hello, consulte Olá seguintes artigos de conector: [banco de dados do SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [do SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).
>  
> Ao copiar dados de banco de dados do SQL Azure ou o SQL Server ou o Azure SQL Data Warehouse, você pode configurar **SqlSource** na atividade de cópia tooinvoke um procedimento armazenado tooread os dados de banco de dados de origem de saudação usando Olá  **sqlReaderStoredProcedureName** propriedade. Para obter mais informações, consulte Olá seguintes artigos de conector: [banco de dados do SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [do SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          

## <a name="json-format"></a>Formato JSON
Este é o formato JSON de saudação para definir uma atividade de procedimento armazenado:

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

Olá, a tabela a seguir descreve as propriedades JSON:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| name | Nome da atividade de saudação |Sim |
| description |Texto que descreve quais atividade Olá é usada para |Não |
| type | Deve ser definido como: **SqlServerStoredProcedure** | Sim |
| inputs | Opcional. Se você especificar um conjunto de dados de entrada, ele deve estar disponível (em status 'Pronto') para Olá armazenados toorun de atividade de procedimento. Olá conjunto de dados de entrada não pode ser consumido no procedimento Olá armazenado como um parâmetro. É apenas dependência de saudação toocheck usado antes de atividade de procedimento armazenado de saudação inicial. |Não |
| outputs | Você deve especificar um conjunto de dados de saída para uma atividade de procedimento armazenado. Conjunto de dados de saída especifica Olá **agenda** para Olá armazenados atividade de procedimento (por hora, semanalmente, mensalmente, etc.). <br/><br/>Olá conjunto de dados de saída deve usar um **serviço vinculado** que se refere a tooan banco de dados do SQL Azure ou um Azure SQL Data Warehouse ou um banco de dados do SQL Server no qual você deseja Olá toorun do procedimento armazenado. <br/><br/>Olá conjunto de dados de saída pode servir como um resultado do modo toopass Olá do procedimento armazenado de saudação para processamento subsequente por outra atividade ([encadeamento atividades](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) no pipeline de saudação. No entanto, fábrica de dados não gravará automaticamente saída Olá de um conjunto de dados do procedimento armazenado toothis. É Olá tabela gravações tooa SQL que Olá pontos do conjunto de dados de saída de procedimento armazenado. <br/><br/>Em alguns casos, o conjunto de dados de saída de hello pode ser um **conjunto de dados fictício**, que é usado somente para atividade de procedimento armazenado de agendamento de saudação toospecify para executar a saudação. |Sim |
| storedProcedureName |Especifique o nome de saudação do procedimento de saudação armazenado no banco de dados do SQL Azure hello ou banco de dados Azure SQL Data Warehouse ou o SQL Server que é representado pelo serviço Olá vinculado que Olá usos da tabela de saída. |Sim |
| storedProcedureParameters |Especifique valores para parâmetros de procedimento armazenado. Se você precisar toopass nulo para um parâmetro, use a sintaxe de saudação: "param1": null (todas as letras minúsculas). Consulte Olá toolearn de exemplo sobre como usar essa propriedade a seguir. |Não |

## <a name="passing-a-static-value"></a>Passando um valor estático
Agora, vamos considerar adicionar outra coluna denominada 'Cenário' na tabela de saudação que contém um valor estático chamado 'Exemplo de documento'.

![Dados de exemplo 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

**Tabela:**

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

**Procedimento armazenado:**

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

Agora, passar Olá **cenário** atividade de procedimento armazenado do valor de parâmetro e hello da saudação. Olá **typeProperties** seção Olá anterior exemplo parece Olá trecho de código a seguir:

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

**Conjunto de dados do Data Factory:**

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Pipeline do Data Factory**

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```