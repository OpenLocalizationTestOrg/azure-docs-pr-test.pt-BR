---
title: 'Tutorial: Criar um Azure Data Factory pipeline toocopy de dados (portal do Azure) | Microsoft Docs'
description: "Neste tutorial, você pode usar toocreate portal do Azure um pipeline da fábrica de dados do Azure com um dado de toocopy de atividade de cópia de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fadd840fe9a15cd8831cdb25dccbd10ac42fa161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-portal-toocreate-a-data-factory-pipeline-toocopy-data"></a>Tutorial: Usar toocreate portal do Azure uma fábrica de dados pipeline toocopy de dados 
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

Neste artigo, você aprenderá como toouse [portal do Azure](https://portal.azure.com) toocreate uma fábrica de dados com um pipeline que copia dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure. Se você estiver tooAzure nova fábrica de dados, leia Olá [tooAzure Introdução Data Factory](data-factory-introduction.md) artigo antes de fazer este tutorial.   

Neste tutorial, você criará um pipeline com uma atividade: atividade de cópia. Olá Copiar atividade copia dados de um repositório de dados com suporte de dados repositório tooa coletor com suporte. Para obter uma lista de armazenamentos de dados com suporte como origens e coletores, confira [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats). atividade de saudação é alimentada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável. Para obter mais informações sobre hello atividade de cópia, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md).

Um pipeline pode ter mais de uma atividade. E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada. Para saber mais, confira [Várias atividades em um pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> pipeline de dados Olá neste tutorial copia dados de um repositório de dados de destino fonte dados repositório tooa. Para obter um tutorial sobre como tootransform dados usando a fábrica de dados do Azure, consulte [Tutorial: Crie um pipeline de dados tootransform usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Pré-requisitos
Conclua os pré-requisitos listados em Olá [pré-requisitos do tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artigo antes de executar este tutorial.

## <a name="steps"></a>Etapas
Aqui estão as etapas Olá que fazem parte deste tutorial:

1. Crie um **data factory** do Azure. Nesta etapa, você cria um data factory denominado ADFTutorialDataFactory. 
2. Criar **serviços vinculados** na fábrica de dados hello. Nesta etapa, você criará dois serviços vinculados de tipos: banco de dados SQL e armazenamento do Azure. 
    
    Olá AzureStorageLinkedService vincula sua fábrica de dados de toohello de conta de armazenamento do Azure. Você criou um contêiner e carregados conta de armazenamento toothis dados como parte de [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService vincula sua fábrica de dados de toohello de banco de dados do SQL Azure. Olá dados são copiados do armazenamento de blob Olá são armazenados neste banco de dados. Você criou uma tabela SQL no banco de dados como parte dos [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   
3. Criar a entrada e saída **conjuntos de dados** na fábrica de dados hello.  
    
    serviço de armazenamento do Azure vinculado Olá Especifica a cadeia de conexão de Olá usada pelo serviço de fábrica de dados em tempo de execução tooconnect tooyour conta de armazenamento do Azure. E, conjunto de dados de blob de entrada hello Especifica o contêiner de saudação e a pasta de saudação que contém os dados de entrada hello.  

    Da mesma forma, Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução. Além disso, conjunto de dados da tabela SQL Olá saída Especifica a tabela Olá Olá toowhich Olá de banco de dados armazenamento de blob Olá é copiada.
4. Criar um **pipeline** na fábrica de dados hello. Nesta etapa, você cria um pipeline com a atividade de cópia.   
    
    Olá Copiar atividade copia dados de um blob na tabela de tooa de armazenamento de BLOBs do Azure de Olá no banco de dados do SQL Azure hello. Você pode usar uma atividade de cópia em um pipeline toocopy os dados de qualquer destino tooany suportada de origem com suporte. Para obter uma lista de armazenamentos de dados com suporte, confira o artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
5. Pipeline de saudação do monitor. Nesta etapa, você **monitor** Olá fatias de conjuntos de dados de entrada e saídas usando o portal do Azure. 

## <a name="create-data-factory"></a>Criar um data factory
> [!IMPORTANT]
> Concluída [pré-requisitos para o tutorial Olá](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) se você ainda não tiver feito isso.   

Uma fábrica de dados pode ter um ou mais pipelines. Um pipeline em um data factory pode ter uma ou mais atividades. Por exemplo, dados de toocopy uma atividade de cópia de um repositório de dados de destino do código-fonte tooa e uma atividade de Hive do HDInsight toorun um tootransform de script do Hive dados de saída de tooproduct dados de entrada. Vamos começar com a criação de fábrica de dados Olá nesta etapa.

1. Depois de fazer logon em toohello [portal do Azure](https://portal.azure.com/), clique em **novo** no menu esquerdo Olá **dados + análise**e clique em **fábrica de dados**. 
   
   ![Novo -> DataFactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. Em Olá **nova fábrica de dados** folha:
   
   1. Digite **ADFTutorialDataFactory** para Olá **nome**. 
      
         ![Folha Nova data factory](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       nome de saudação do hello data factory do Azure deve ser **globalmente exclusivo**. Se você receber Olá erro a seguir, altere o nome de saudação da fábrica de dados da saudação (por exemplo, yournameADFTutorialDataFactory) e tente criar novamente. Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![Nome da data factory indisponível](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. Selecione o Azure **assinatura** no qual você deseja a fábrica de dados toocreate hello. 
   3. Para Olá **grupo de recursos**, siga um destes Olá etapas a seguir:
      
      - Selecione **usar existente**e selecione um grupo de recursos existente na lista suspensa de saudação. 
      - Selecione **criar novo**e insira o nome de saudação de um grupo de recursos.   
         
          Algumas das etapas neste tutorial Olá pressupõem que você use o nome da saudação: **ADFTutorialResourceGroup** Olá para grupo de recursos. toolearn sobre grupos de recursos, consulte [usando o recurso de grupos de toomanage os recursos do Azure](../azure-resource-manager/resource-group-overview.md).  
   4. Selecione Olá **local** Olá fábrica de dados. Somente regiões Olá serviço da fábrica de dados com suporte são mostrados na lista suspensa de saudação.
   5. Selecione **toodashboard Pin**.     
   6. Clique em **Criar**.
      
      > [!IMPORTANT]
      > toocreate instâncias de fábrica de dados, você deve ser um membro da saudação [colaborador da fábrica de dados](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) função no nível do grupo de recursos de assinatura/hello.
      > 
      > nome Olá Olá da fábrica de dados pode ser registrado como um nome DNS no hello futuro e, portanto, se tornarão visível publicamente.                
      > 
      > 
3. No painel hello, você vê Olá seguinte lado a lado com o status: **fábrica de dados implantando**. 

    ![implantando bloco data factory](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. Após a conclusão da criação de saudação, você ver Olá **Data Factory** folha, conforme mostrado na imagem de saudação.
   
   ![Página inicial da data factory](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a>Criar serviços vinculados
Você pode criar serviços vinculados em um toolink de fábrica de dados seus dados, armazena e fábrica de dados toohello de serviços de computação. Neste tutorial, você não usa serviços de computação, como o Azure HDInsight ou o Azure Data Lake Analytics. Você usa dois armazenamentos de dados do tipo Armazenamento do Azure (origem) e o banco de dados SQL (destino). 

Portanto, você pode criar dois serviços vinculados, chamados AzureStorageLinkedService e AzureSqlLinkedService, dos tipos: AzureStorage e AzureSqlDatabase.  

Olá AzureStorageLinkedService vincula sua fábrica de dados de toohello de conta de armazenamento do Azure. Esta conta de armazenamento é hello um no qual você criou um contêiner e carregou dados de saudação como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService vincula sua fábrica de dados de toohello de banco de dados do SQL Azure. Olá dados são copiados do armazenamento de blob Olá são armazenados neste banco de dados. Você criou tabela emp de saudação neste banco de dados como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Criar o serviço vinculado do armazenamento do Azure
Nesta etapa, você vincular sua fábrica de dados de tooyour de conta de armazenamento do Azure. Especifique o nome hello e a chave da sua conta de armazenamento do Azure nesta seção.  

1. Em Olá **Data Factory** folha, clique em **autor e implantar** lado a lado.
   
   ![Bloco Criar e implantar](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. Consulte Olá **Editor da fábrica de dados** conforme Olá a imagem a seguir: 

    ![Editor Data Factory](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. No editor de saudação, clique em **novo repositório de dados** botão na barra de ferramentas hello e selecione **armazenamento do Azure** do menu suspenso de saudação. Você deve ver o modelo JSON Olá para criar um serviço vinculado do armazenamento do Azure no painel direito da saudação. 
   
    ![Botão Novo repositório de dados do editor](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. Substituir `<accountname>` e `<accountkey>` com hello conta nome e a conta de valores de chave para sua conta de armazenamento do Azure. 
   
    ![JSON do armazenamento de Blob do editor](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. Clique em **implantar** na barra de ferramentas de saudação. Você deve ver Olá implantado **AzureStorageLinkedService** na árvore de saudação exibir agora. 
   
    ![Implantar armazenamento de Blob do editor](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    Para obter mais informações sobre as propriedades JSON na definição de serviço Olá vinculado, consulte [conector de armazenamento de BLOBs do Azure](data-factory-azure-blob-connector.md#linked-service-properties) artigo.

### <a name="create-a-linked-service-for-hello-azure-sql-database"></a>Criar um serviço vinculado para hello Azure SQL Database
Nesta etapa, você vincular sua fábrica de dados de tooyour de banco de dados do SQL Azure. Especifique o nome do servidor SQL Azure Olá, nome do banco de dados, nome de usuário e senha de usuário nesta seção. 

1. Em Olá **Editor da fábrica de dados**, clique em **novo repositório de dados** botão na barra de ferramentas hello e selecione **banco de dados do SQL Azure** do menu suspenso de saudação. Você deve ver o modelo JSON Olá para a criação de serviço vinculado do SQL Azure de saudação no painel direito da saudação.
2. Substitua `<servername>`, `<databasename>`, `<username>@<servername>` e `<password>` pelos nomes de seu servidor, banco de dados, conta de usuário e senha SQL do Azure. 
3. Clique em **implantar** Olá toocreate da barra de ferramentas e implantar Olá **AzureSqlLinkedService**.
4. Confirme que você vê **AzureSqlLinkedService** na exibição de árvore de saudação em **serviços vinculados**.  

    Para saber mais sobre essas propriedades JSON, confira o [Conector do Banco de Dados SQL](data-factory-azure-sql-connector.md#linked-service-properties).

## <a name="create-datasets"></a>Criar conjuntos de dados
Na etapa anterior de saudação, você criou serviços vinculados toolink sua conta de armazenamento do Azure e a fábrica de dados de tooyour de banco de dados do SQL Azure. Nesta etapa, você definirá dois conjuntos de dados denominados InputDataset OutputDataset que representam a entrada e saída dados e que são armazenados em repositórios de dados Olá referenciados por AzureStorageLinkedService e AzureSqlLinkedService, respectivamente.

serviço de armazenamento do Azure vinculado Olá Especifica a cadeia de conexão de Olá usada pelo serviço de fábrica de dados em tempo de execução tooconnect tooyour conta de armazenamento do Azure. E, Olá o conjunto de dados de blob de entrada (InputDataset) Especifica o contêiner de saudação e a pasta de saudação que contém os dados de entrada hello.  

Da mesma forma, Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução. E, Olá saída SQL o conjunto de dados de tabela (OututDataset) Especifica a tabela de saudação em Olá Olá de toowhich de banco de dados dados saudação do armazenamento de blob são copiados. 

### <a name="create-input-dataset"></a>Criar conjunto de dados de entrada
Nesta etapa, você criar um conjunto de dados chamado InputDataset que aponta o arquivo de blob tooa (emp.txt) na pasta raiz de saudação de um contêiner de blob (adftutorial) no hello representado por Olá AzureStorageLinkedService vinculado de serviço de armazenamento do Azure. Se você não especificar um valor para o nome de arquivo hello (ou ignorá-lo), dados de todos os blobs na pasta de entrada hello são copiados toohello destino. Neste tutorial, você deve especificar um valor para o nome de arquivo hello. 

1. Em Olá **Editor** para Olá fábrica de dados, clique em **... Mais**, clique em **novo conjunto de dados**e clique em **armazenamento de BLOBs do Azure** do menu suspenso de saudação. 
   
    ![Menu Novo conjunto de dados](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. Substitua o JSON no painel direito da saudação com hello trecho JSON a seguir: 
   
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
          "folderPath": "adftutorial/",
          "fileName": "emp.txt",
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
3. Clique em **implantar** Olá toocreate da barra de ferramentas e implantar Olá **InputDataset** conjunto de dados. Confirme que você vê Olá **InputDataset** na exibição de árvore de saudação.

### <a name="create-output-dataset"></a>Criar conjunto de dados de saída
Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução. Olá saída SQL tabela dataset (OututDataset) você criar nessa etapa Especifica a tabela Olá Olá toowhich Olá de banco de dados armazenamento de blob de saudação é copiada.

1. Em Olá **Editor** para Olá fábrica de dados, clique em **... Mais**, clique em **novo conjunto de dados**e clique em **SQL Azure** do menu suspenso de saudação. 
2. Substitua o JSON no painel direito da saudação com hello trecho JSON a seguir:

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
3. Clique em **implantar** Olá toocreate da barra de ferramentas e implantar Olá **OutputDataset** conjunto de dados. Confirme que você vê Olá **OutputDataset** na exibição de árvore de saudação em **conjuntos de dados**. 

## <a name="create-pipeline"></a>Criar um pipeline
Nesta etapa, você cria um pipeline com uma **atividade de cópia** que usa **InputDataset** como entrada e **OutputDataset** como saída.

Atualmente, o conjunto de dados de saída é quais unidades Olá agenda. Neste tutorial, o conjunto de dados de saída é configurado tooproduce uma fatia de uma vez por hora. pipeline de saudação tem uma hora de início e a hora de término que são um dia de distância, que é de 24 horas. Portanto, 24 fatias de conjunto de dados de saída são produzidas pelo pipeline de saudação. 

1. Em Olá **Editor** para Olá fábrica de dados, clique em **... Mais** e clique em **Novo pipeline**. Como alternativa, clique **Pipelines** no modo de exibição de árvore de saudação e clique em **novo pipeline**.
2. Substitua o JSON no painel direito da saudação com hello trecho JSON a seguir: 

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
    - Ambos os valores de data/hora de início e de término devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por exemplo: 2016-10-14T16:32:41Z. Olá **final** tempo é opcional, mas usamos neste tutorial. Se você não especificar o valor para Olá **final** propriedade, ele é calculado como "**início + 48 horas**". pipeline de saudação toorun indefinidamente, especifique **9999-09-09** como valor Olá Olá **final** propriedade.
     
    Olá anterior de exemplo, há 24 fatias de dados como cada fatia de dados é produzida por hora.

    Para obter descrições das propriedades JSON em uma definição de pipeline, consulte o artigo [Criar pipelines](data-factory-create-pipelines.md). Para obter descrições das propriedades JSON em uma definição de atividade de cópia, consulte [Atividades de movimentação de dados](data-factory-data-movement-activities.md). Para obter descrições das propriedades JSON com suporte pelo BlobSource, consulte o [artigo sobre o conector de blobs do Azure](data-factory-azure-blob-connector.md). Para obter descrições das propriedades JSON com suporte pelo SqlSink, consulte o [artigo sobre o conector do Banco de Dados SQL](data-factory-azure-sql-connector.md).
3. Clique em **implantar** Olá toocreate da barra de ferramentas e implantar Olá **ADFTutorialPipeline**. Confirme que você vê pipeline Olá Olá na exibição em árvore. 
4. Agora, feche Olá **Editor** folha clicando **X**. Clique em **X** novamente toosee Olá **Data Factory** home page do hello **ADFTutorialDataFactory**.

**Parabéns!** Você criou com êxito uma fábrica de dados do Azure com um pipeline toocopy os dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure. 


## <a name="monitor-pipeline"></a>Monitorar o pipeline
Nesta etapa, você deve usar Olá toomonitor de portal do Azure que está acontecendo em uma fábrica de dados do Azure.    

### <a name="monitor-pipeline-using-monitor--manage-app"></a>Monitorar o pipeline usando o aplicativo Monitorar e Gerenciar
Olá etapas a seguir mostram como toomonitor pipelines sua fábrica de dados usando o aplicativo hello de monitorar e gerenciar: 

1. Clique em **monitorar e gerenciar** lado a lado na página inicial do hello sua fábrica de dados.
   
    ![Bloco Monitorar e Gerenciar](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. Você deverá ver **Monitorar e gerenciar aplicativo** em uma guia separada. 

    > [!NOTE]
    > Se você vir esse navegador da web hello está preso em "Autorizar...", siga um destes procedimentos Olá: Olá limpar **bloquear cookies de terceiros e dados do site** caixa de seleção (ou) criar uma exceção para **login.microsoftonline.com**e, em seguida, tente tooopen Olá aplicativo novamente.

    ![Aplicativo Monitorar e Gerenciar](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. Saudação de alteração **hora de início** e **hora de término** tooinclude (2017-05-11) de início e término (2017-05-12) do pipeline e clique em **aplicar**.     
3. Consulte Olá **windows atividade** associados a cada hora entre o início do pipeline e de término vezes na lista de saudação no painel do meio Olá. 
4. Olá toosee detalhes sobre uma janela de atividade, selecione a janela de atividade no hello **atividade Windows** lista. 
    ![Detalhes da janela Atividade](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)

    No Gerenciador de janela de atividade no hello direita, verá que Olá fatias de tempo de UTC atual toohello (8:12 PM) são processados (na cor verde). fatias de 8-9 PM, 9-10 PM, 10-11 PM, 11 PM - 12: 00 Olá não são processadas.

    Olá **tentativas** seção Olá direita painel fornece informações sobre a execução para a fatia de dados Olá da atividade Olá. Se houver um erro, ele fornece detalhes sobre o erro de saudação. Por exemplo, se a pasta ou um contêiner de entrada hello não existe e falha de processamento da fatia hello, você verá uma mensagem de erro informando contêiner hello ou pasta não existe.

    ![Tentativas de execução da atividade](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. Iniciar **SQL Server Management Studio**, conectar toohello banco de dados do SQL Azure e verificar se as linhas de saudação são inseridas no toohello **emp** tabela no banco de dados de saudação.
    
    ![resultados da consulta sql](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

Para obter informações detalhadas sobre como usar esse aplicativo, veja [Monitorar e gerenciar confira do Azure Data Factory usando o aplicativo Monitorar e Gerenciar](data-factory-monitor-manage-app.md).

### <a name="monitor-pipeline-using-diagram-view"></a>Monitorar o pipeline usando a Exibição de Diagrama
Você também pode monitorar pipelines de dados usando o modo de exibição de diagrama de saudação.  

1. Em Olá **Data Factory** folha, clique em **diagrama**.
   
    ![Folha Data Factory — bloco Diagrama](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. Você deve ver toohello semelhante do diagrama Olá imagem a seguir: 
   
    ![Exibição de diagrama](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. No modo de exibição de diagrama hello, clique duas vezes em **InputDataset** toosee fatias de saudação de conjunto de dados.  
   
    ![Conjuntos de dados com InputDataset selecionado](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. Clique em **ver mais** link toosee todas as fatias de dados hello. Você verá 24 fatias horárias entre as horas de início e término do pipeline. 
   
    ![Todas as fatias de dados de entrada](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    Observe que todos os Olá fatias de dados o tempo de UTC atual toohello **pronto** porque Olá **emp.txt** arquivo existe todo o tempo de saudação no contêiner de blob Olá: **adftutorial\input**. fatias de saudação para horários futuras Olá ainda não estão no estado pronto. Confirme que nenhuma fatia aparecerão em Olá **recentemente falha fatias** seção na parte inferior da saudação.
6. Folhas de saudação fechar até que você consulte Olá diagrama de modo de exibição (ou) rolagem esquerdo toosee Olá exibir. Em seguida, clique duas vezes em **OutputDataset**. 
8. Clique em **ver mais** link Olá **tabela** folha para **OutputDataset** toosee todos Olá fatias.

    ![folha fatias de dados](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. Observe que todos os Olá frações de tempo de UTC atual toohello mover de **pendentes execução** estado = > **em andamento** ==> **pronto** estado. Olá fatias de saudação anterior (antes da hora atual) são processados de toooldest mais recente por padrão. Por exemplo, se Olá hora atual for 8:12 PM UTC, fatia Olá para 19: 00 - 8 PM é processada à frente da fatia de 18: 00 - 7 P.M. hello. fatia de 8 PM - 9 PM Olá é processada final Olá Olá do intervalo de tempo por padrão, o que está depois às 21H.  
10. Clique em qualquer fatia de dados da lista de saudação e você deverá ver Olá **fatia de dados** folha. Uma parte dos dados associados a uma janela de atividade é chamada de fatia. Uma fatia pode ser um ou vários arquivos.  
    
     ![folha fatia de dados](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     Se fatia Olá não está em Olá **pronto** estado, você pode ver fatias de upstream Olá que não estão prontos e estão bloqueando a fatia atual Olá executadas em Olá **fatias de Upstream que não estão prontas** lista.
11. Em Olá **FATIA de dados** folha, você deve ver todas as atividades é executado na lista de saudação na parte inferior da saudação. Clique em uma **execução da atividade** toosee Olá **detalhes da execução de atividade** folha. 
    
    ![Detalhes da execução da atividade](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    Nessa folha, você deve ver como levou a operação de cópia Olá longo, quais taxa de transferência é, o número de bytes de dados foram leitura e a hora de início escrito, executar, tempo de execução final etc.  
12. Clique em **X** tooclose todas as folhas de saudação até que você voltar toohello folha de base para Olá **ADFTutorialDataFactory**.
13. (opcional) clique Olá **conjuntos de dados** lado a lado ou **Pipelines** folhas de saudação do bloco tooget você viu Olá etapas anteriores. 
14. Iniciar **SQL Server Management Studio**, conectar toohello banco de dados do SQL Azure e verificar se as linhas de saudação são inseridas no toohello **emp** tabela no banco de dados de saudação.
    
    ![resultados da consulta sql](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a>Resumo
Neste tutorial, você criou um Azure fábrica toocopy dados de um banco de dados do SQL Azure de tooan BLOBs do Azure. Você usou a fábrica de dados de Olá Olá toocreate portal do Azure, serviços vinculados, conjuntos de dados e um pipeline. Aqui estão as etapas de alto nível Olá executada neste tutorial:  

1. Foi criada uma **data factory**do Azure.
2. Foram criados **serviços vinculados**:
   1. Um **armazenamento do Azure** vinculado serviço toolink sua conta de armazenamento do Azure que contém dados de entrada.     
   2. Um **SQL Azure** vinculado serviço toolink seu banco de dados SQL do Azure que contém dados de saída de saudação. 
3. Foram criados **conjuntos de dados** que descrevem os dados de entrada e de saída para os pipelines.
4. Foi criado um **pipeline** com uma **Atividade de Cópia** com **BlobSource** como origem e **SqlSink** como coletor.  

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você usou o armazenamento de blobs do Azure como um armazenamento de dados de origem e um banco de dados SQL do Azure como um armazenamento de dados de destino em uma operação de cópia. Olá tabela a seguir fornece uma lista de repositórios de dados com suporte como origens e destinos de atividade de cópia de saudação: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn sobre como armazenam dados toocopy para/de uma data, clique o link Olá Olá repositório de dados na tabela de saudação.
