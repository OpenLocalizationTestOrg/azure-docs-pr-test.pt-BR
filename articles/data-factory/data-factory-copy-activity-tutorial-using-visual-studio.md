---
title: "Tutorial: Criar um pipeline com a Atividade de Cópia usando o Visual Studio | Microsoft Docs"
description: "Neste tutorial, você cria um pipeline do Azure Data Factory com uma Atividade de Cópia usando o Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a>Tutorial: Criar um pipeline com a Atividade de Cópia usando o Visual Studio
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

Neste artigo, você aprenderá como toouse Olá toocreate do Microsoft Visual Studio uma fábrica de dados com um pipeline que copia dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure. Se você estiver tooAzure nova fábrica de dados, leia Olá [tooAzure Introdução Data Factory](data-factory-introduction.md) artigo antes de fazer este tutorial.   

Neste tutorial, você criará um pipeline com uma atividade: atividade de cópia. Olá Copiar atividade copia dados de um repositório de dados com suporte de dados repositório tooa coletor com suporte. Para obter uma lista de armazenamentos de dados com suporte como origens e coletores, confira [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats). atividade de saudação é alimentada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável. Para obter mais informações sobre hello atividade de cópia, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md).

Um pipeline pode ter mais de uma atividade. E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada. Para saber mais, confira [Várias atividades em um pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE] 
> pipeline de dados Olá neste tutorial copia dados de um repositório de dados de destino fonte dados repositório tooa. Para obter um tutorial sobre como tootransform dados usando a fábrica de dados do Azure, consulte [Tutorial: Crie um pipeline de dados tootransform usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Pré-requisitos
1. Leia [visão geral do Tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artigo e hello completa **pré-requisito** etapas.       
2. toocreate instâncias de fábrica de dados, você deve ser um membro da saudação [colaborador da fábrica de dados](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) função no nível do grupo de recursos de assinatura/hello.
3. Você deve ter o seguinte Olá instalado em seu computador: 
   * Visual Studio 2013 ou Visual Studio 2015
   * Baixe o SDK do Azure para Visual Studio 2013 ou Visual Studio de 2015. Navegue muito[página de Download do Azure](https://azure.microsoft.com/downloads/) e clique em **VS 2013** ou **VS 2015** em Olá **.NET** seção.
   * Baixar hello mais recente do Azure Data Factory plug-in para Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) ou [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Você também pode atualizar plug-in de saudação fazendo Olá etapas a seguir: Olá menu, clique em **ferramentas** -> **extensões e atualizações** -> **Online**  ->  **Galeria do visual Studio** -> **ferramentas de fábrica de dados do Microsoft Azure para Visual Studio** -> **atualização**.

## <a name="steps"></a>Etapas
Aqui estão as etapas Olá que fazem parte deste tutorial:

1. Criar **serviços vinculados** na fábrica de dados hello. Nesta etapa, você criará dois serviços vinculados de tipos: banco de dados SQL e armazenamento do Azure. 
    
    Olá AzureStorageLinkedService vincula sua fábrica de dados de toohello de conta de armazenamento do Azure. Você criou um contêiner e carregados conta de armazenamento toothis dados como parte de [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService vincula sua fábrica de dados de toohello de banco de dados do SQL Azure. Olá dados são copiados do armazenamento de blob Olá são armazenados neste banco de dados. Você criou uma tabela SQL no banco de dados como parte dos [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).     
2. Criar a entrada e saída **conjuntos de dados** na fábrica de dados hello.  
    
    serviço de armazenamento do Azure vinculado Olá Especifica a cadeia de conexão de Olá usada pelo serviço de fábrica de dados em tempo de execução tooconnect tooyour conta de armazenamento do Azure. E, conjunto de dados de blob de entrada hello Especifica o contêiner de saudação e a pasta de saudação que contém os dados de entrada hello.  

    Da mesma forma, Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução. Além disso, conjunto de dados da tabela SQL Olá saída Especifica a tabela Olá Olá toowhich Olá de banco de dados armazenamento de blob Olá é copiada.
3. Criar um **pipeline** na fábrica de dados hello. Nesta etapa, você cria um pipeline com a atividade de cópia.   
    
    Olá Copiar atividade copia dados de um blob na tabela de tooa de armazenamento de BLOBs do Azure de Olá no banco de dados do SQL Azure hello. Você pode usar uma atividade de cópia em um pipeline toocopy os dados de qualquer destino tooany suportada de origem com suporte. Para obter uma lista de armazenamentos de dados com suporte, confira o artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
4. Crie um **data factory** do Azure ao implantar entidades de Data Factory (serviços vinculados, conjuntos de dados/tabelas e pipelines). 

## <a name="create-visual-studio-project"></a>Criar um projeto do Visual Studio
1. Inicie o **Visual Studio 2015**. Clique em **arquivo**, ponto muito**novo**e clique em **projeto**. Você deve ver Olá **novo projeto** caixa de diálogo.  
2. Em Olá **novo projeto** caixa de diálogo, selecione Olá **DataFactory** modelo e clique em **projeto vazio de fábrica de dados**.  
   
    ![Caixa de diálogo Novo projeto](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. Especifique o nome de saudação do projeto hello, local para a solução de saudação e nome da solução hello e, em seguida, clique em **Okey**.
   
    ![Gerenciador de Soluções](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a>Criar serviços vinculados
Você pode criar serviços vinculados em um toolink de fábrica de dados seus dados, armazena e fábrica de dados toohello de serviços de computação. Neste tutorial, você não usa serviços de computação, como o Azure HDInsight ou o Azure Data Lake Analytics. Você usa dois armazenamentos de dados do tipo Armazenamento do Azure (origem) e o banco de dados SQL (destino). 

Portanto, você pode criar dois serviços vinculados de tipos: AzureStorage e AzureSqlDatabase.  

saudação de armazenamento do Azure vinculada links de serviço sua fábrica de dados de toohello de conta de armazenamento do Azure. Esta conta de armazenamento é hello um no qual você criou um contêiner e carregou dados de saudação como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

SQL Azure vinculado links serviço sua fábrica de dados de toohello de banco de dados do SQL Azure. Olá dados são copiados do armazenamento de blob Olá são armazenados neste banco de dados. Você criou tabela emp de saudação neste banco de dados como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Serviços vinculados vincular armazenamentos de dados ou de computação serviços tooan data factory do Azure. Consulte [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para todos os Olá fontes e coletores suportados pelas hello atividade de cópia. Consulte [serviços vinculados de computação](data-factory-compute-linked-services.md) para lista de saudação de serviços de computação com suporte pela fábrica de dados. Neste tutorial, você não usa nenhum serviço de computação. 

### <a name="create-hello-azure-storage-linked-service"></a>Criar serviço de armazenamento do Azure vinculada Olá
1. Em **Solution Explorer**, clique com botão direito **serviços vinculados**, ponto muito**adicionar**e clique em **Novo Item**.      
2. Em Olá **Adicionar Novo Item** caixa de diálogo, selecione **serviço vinculado do armazenamento do Azure** Olá lista e clique em **adicionar**. 
   
    ![Novo serviço vinculado](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. Substituir `<accountname>` e `<accountkey>`* com nome de saudação da sua conta de armazenamento do Azure e sua chave. 
   
    ![Serviço vinculado de armazenamento do Azure](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. Salvar Olá **AzureStorageLinkedService1.json** arquivo.

    Para obter mais informações sobre as propriedades JSON na definição de serviço Olá vinculado, consulte [conector de armazenamento de BLOBs do Azure](data-factory-azure-blob-connector.md#linked-service-properties) artigo.

### <a name="create-hello-azure-sql-linked-service"></a>Criar serviço vinculado do SQL Azure de saudação
1. Clique duas vezes em **serviços vinculados** nó Olá **Solution Explorer** novamente, aponte muito**adicionar**e clique em **Novo Item**. 
2. Desta vez, selecione **Serviço Vinculado SQL do Azure** e clique em **Adicionar**. 
3. Em Olá **AzureSqlLinkedService1.json arquivo**, substitua `<servername>`, `<databasename>`, `<username@servername>`, e `<password>` com nomes de seu servidor SQL Azure, banco de dados, conta de usuário e senha.    
4. Salvar Olá **AzureSqlLinkedService1.json** arquivo. 
    
    Para saber mais sobre essas propriedades JSON, confira o [Conector do Banco de Dados SQL](data-factory-azure-sql-connector.md#linked-service-properties).


## <a name="create-datasets"></a>Criar conjuntos de dados
Na etapa anterior de saudação, você criou serviços vinculados toolink sua conta de armazenamento do Azure e a fábrica de dados de tooyour de banco de dados do SQL Azure. Nesta etapa, você definirá dois conjuntos de dados denominados InputDataset OutputDataset que representam a entrada e saída dados e que são armazenados em repositórios de dados Olá referenciados por AzureStorageLinkedService1 e AzureSqlLinkedService1, respectivamente.

serviço de armazenamento do Azure vinculado Olá Especifica a cadeia de conexão de Olá usada pelo serviço de fábrica de dados em tempo de execução tooconnect tooyour conta de armazenamento do Azure. E, Olá o conjunto de dados de blob de entrada (InputDataset) Especifica o contêiner de saudação e a pasta de saudação que contém os dados de entrada hello.  

Da mesma forma, Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução. E, Olá saída SQL o conjunto de dados de tabela (OututDataset) Especifica a tabela de saudação em Olá Olá de toowhich de banco de dados dados saudação do armazenamento de blob são copiados. 

### <a name="create-input-dataset"></a>Criar conjunto de dados de entrada
Nesta etapa, você criar um conjunto de dados chamado InputDataset que aponta o arquivo de blob tooa (emp.txt) na pasta raiz de saudação de um contêiner de blob (adftutorial) no hello representado por Olá AzureStorageLinkedService1 vinculado de serviço de armazenamento do Azure. Se você não especificar um valor para o nome de arquivo hello (ou ignorá-lo), dados de todos os blobs na pasta de entrada hello são copiados toohello destino. Neste tutorial, você deve especificar um valor para o nome de arquivo hello. 

Aqui, você usa o termo hello "tabelas" em vez de "conjuntos de dados". Uma tabela é um conjunto de dados retangular e Olá único tipo de conjunto de dados com suporte no momento. 

1. Clique com botão direito **tabelas** em Olá **Solution Explorer**, ponto muito**adicionar**e clique em **Novo Item**.
2. Em Olá **Adicionar Novo Item** caixa de diálogo, selecione **BLOBs do Azure**e clique em **adicionar**.   
3. Substituir texto JSON de Olá Olá texto a seguir e salve Olá **AzureBlobLocation1.json** arquivo. 

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
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
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

### <a name="create-output-dataset"></a>Criar conjunto de dados de saída
Nesta etapa, você cria um conjunto de dados de saída denominado **OutputDataset**. Este conjunto de dados aponta tooa SQL tabela no banco de dados do SQL Azure Olá representado por **AzureSqlLinkedService1**. 

1. Clique com botão direito **tabelas** em Olá **Solution Explorer** novamente, aponte muito**adicionar**e clique em **Novo Item**.
2. Em Olá **Adicionar Novo Item** caixa de diálogo, selecione **SQL Azure**e clique em **adicionar**. 
3. Substituir texto JSON de Olá Olá JSON a seguir e salve Olá **AzureSqlTableLocation1.json** arquivo.

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
       "linkedServiceName": "AzureSqlLinkedService1",
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

## <a name="create-pipeline"></a>Criar um pipeline
Nesta etapa, você cria um pipeline com uma **atividade de cópia** que usa **InputDataset** como entrada e **OutputDataset** como saída.

Atualmente, o conjunto de dados de saída é quais unidades Olá agenda. Neste tutorial, o conjunto de dados de saída é configurado tooproduce uma fatia de uma vez por hora. pipeline de saudação tem uma hora de início e a hora de término que são um dia de distância, que é de 24 horas. Portanto, 24 fatias de conjunto de dados de saída são produzidas pelo pipeline de saudação. 

1. Clique com botão direito **Pipelines** em Olá **Solution Explorer**, ponto muito**adicionar**e clique em **Novo Item**.  
2. Selecione **Pipeline de dados de cópia** em Olá **Adicionar Novo Item** caixa de diálogo e clique em **adicionar**. 
3. Substitua Olá JSON Olá JSON a seguir e salve Olá **CopyActivity1.json** arquivo.

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
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - Na seção de atividades hello, há apenas uma atividade cuja **tipo** está definido muito**cópia**. Para obter mais informações sobre a atividade de cópia hello, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md). Nas soluções de Data Factory, você também pode usar [atividades de transformação de dados](data-factory-data-transformation-activities.md).
    - Entrada para atividade de saudação é definida muito**InputDataset** e de saída para o conjunto de hello atividade é muito**OutputDataset**. 
    - Em Olá **typeProperties** seção, **BlobSource** é especificado como tipo de fonte hello e **SqlSink** é especificado como tipo de coletor de saudação. Para obter uma lista completa de armazenamentos de dados de atividade de cópia hello como origens e coletores com suporte, consulte [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn como toouse dados específicos com suporte são armazenados como um fonte/coletor, clique o link de saudação na tabela de saudação.  
     
    Substituir valor Olá Olá **iniciar** propriedade com hello dia atual e **final** valor com hello dia seguinte. Você pode especificar apenas parte da data hello e ignore a parte de hora de saudação da saudação data hora. Por exemplo, "2016-02-03", que é o equivalente muito "2016-02-03T00:00:00Z"
     
    Ambos os valores de data/hora de início e de término devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por exemplo: 2016-10-14T16:32:41Z. Olá **final** tempo é opcional, mas usamos neste tutorial. 
     
    Se você não especificar o valor para Olá **final** propriedade, ele é calculado como "**início + 48 horas**". pipeline de saudação toorun indefinidamente, especifique **9999-09-09** como valor Olá Olá **final** propriedade.
     
    Olá anterior de exemplo, há 24 fatias de dados como cada fatia de dados é produzida por hora.

    Para obter descrições das propriedades JSON em uma definição de pipeline, consulte o artigo [Criar pipelines](data-factory-create-pipelines.md). Para obter descrições das propriedades JSON em uma definição de atividade de cópia, consulte [Atividades de movimentação de dados](data-factory-data-movement-activities.md). Para obter descrições das propriedades JSON com suporte pelo BlobSource, consulte o [artigo sobre o conector de blobs do Azure](data-factory-azure-blob-connector.md). Para obter descrições das propriedades JSON com suporte pelo SqlSink, consulte o [artigo sobre o conector do Banco de Dados SQL](data-factory-azure-sql-connector.md).

## <a name="publishdeploy-data-factory-entities"></a>Publicar/implantar entidades de data factory
Nesta etapa, você publica as entidades de Data Factory (serviços vinculados, conjuntos de dados e pipeline) criadas anteriormente. Você também especificar o nome de saudação do hello novos dados fábrica toobe criado toohold essas entidades.  

1. Clique com botão direito no Gerenciador de soluções do hello e, em seguida, clique em **publicar**. 
2. Se você vir **entrar na conta da Microsoft de tooyour** caixa de diálogo, insira suas credenciais de conta de saudação que tenha a assinatura do Azure e clique em **entrar**.
3. Você deve ver Olá caixa de diálogo a seguir:
   
   ![Caixa de diálogo Publicar](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. Na página de fábrica de dados de configurar Olá, Olá seguintes etapas: 
   
   1. Selecione a opção **Criar Nova Data Factory** .
   2. Digite **VSTutorialFactory** para **Nome**.  
      
      > [!IMPORTANT]
      > nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo. Se você receber um erro sobre nome de saudação da fábrica de dados durante a publicação, altere o nome de saudação da fábrica de dados da saudação (por exemplo, yournameVSTutorialFactory) e tente publicar novamente. Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.        
      > 
      > 
   3. Selecione sua assinatura do Azure para Olá **assinatura** campo.
      
      > [!IMPORTANT]
      > Se você não vir nenhuma assinatura, certifique-se de que você fez logon usando uma conta que seja um administrador ou coadministrador da assinatura de saudação.  
      > 
      > 
   4. Selecione Olá **grupo de recursos** para Olá toobe de fábrica de dados criado. 
   5. Selecione Olá **região** Olá fábrica de dados. Somente regiões Olá serviço da fábrica de dados com suporte são mostrados na lista suspensa de saudação.
   6. Clique em **próximo** tooswitch toohello **publicar itens** página.
      
       ![Configurar página de data factory](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. Em Olá **publicar itens** página, certifique-se de que todos os Olá fábricas de dados de entidades são selecionadas e clique em **próximo** tooswitch toohello **resumo** página.
   
   ![Publicar página de item](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. Revise o resumo de saudação e clique em **próximo** Olá de processo e o modo de exibição de implantação de saudação do toostart **Status da implantação**.
   
   ![Publicar página de resumo](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. Em Olá **Status da implantação** página, você deve ver o status de Olá Olá do processo de implantação. Após a conclusão da implantação de saudação, clique em Concluir.
 
   ![Página Status da implantação](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

Observe Olá pontos a seguir: 

* Se você receber o erro Olá: "Esta assinatura não está registrado toouse namespace DataFactory", execute um dos seguintes hello e tente publicar novamente: 
  
  * No Azure PowerShell, execute Olá provedor do comando tooregister Olá fábrica de dados a seguir. 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    Você pode executar Olá tooconfirm de comando a seguir que Olá Data Factory provedor está registrado. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Usando o logon Olá assinatura do Azure em Olá [portal do Azure](https://portal.azure.com) e navegue tooa folha de fábrica de dados (ou) criar uma fábrica de dados no hello portal do Azure. Esta ação registra automaticamente o provedor de saudação para você.
* nome Olá Olá da fábrica de dados pode ser registrado como um nome DNS no hello futuro e, portanto, se tornarão visível publicamente.

> [!IMPORTANT]
> toocreate instâncias de fábrica de dados, você precisa toobe um administrador/coadministrador da saudação assinatura do Azure

## <a name="monitor-pipeline"></a>Monitorar o pipeline
Navegue até a página inicial de toohello sua fábrica de dados:

1. Faça logon no muito[portal do Azure](https://portal.azure.com).
2. Clique em **mais serviços** Olá menus à esquerda e clique em **fábricas de dados**.

    ![Procurar data factories](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. Comece a digitar nome de saudação da sua fábrica de dados.

    ![Nome do data factory](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. Clique em sua fábrica de dados em Olá resultados lista toosee Olá home page de sua fábrica de dados.

    ![Página inicial da data factory](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. Siga as instruções de [monitorar conjuntos de dados e pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) pipeline de saudação toomonitor e conjuntos de dados, você criou neste tutorial. Atualmente, o Visual Studio não dá suporte a monitoramento de pipelines do Data Factory. 

## <a name="summary"></a>Resumo
Neste tutorial, você criou um Azure fábrica toocopy dados de um banco de dados do SQL Azure de tooan BLOBs do Azure. Você usou a fábrica de dados do Visual Studio toocreate hello, serviços vinculados, conjuntos de dados e um pipeline. Aqui estão as etapas de alto nível Olá executada neste tutorial:  

1. Foi criada uma **data factory**do Azure.
2. Foram criados **serviços vinculados**:
   1. Um **armazenamento do Azure** vinculado serviço toolink sua conta de armazenamento do Azure que contém dados de entrada.     
   2. Um **SQL Azure** vinculado serviço toolink seu banco de dados SQL do Azure que contém dados de saída de saudação. 
3. Foram criados **conjuntos de dados**que descrevem os dados de entrada e de saída para os pipelines.
4. Foi criado um **pipeline** com uma **Atividade de Cópia** com **BlobSource** como origem e **SqlSink** como coletor. 

toosee como toouse dados de tootransform uma atividade de Hive do HDInsight usando o cluster HDInsight do Azure, consulte [ Tutorial: Crie sua primeira pipeline tootransform de dados usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).

É possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada. Veja [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md) para obter informações detalhadas. 

## <a name="view-all-data-factories-in-server-explorer"></a>Exibir todos os data factories no Gerenciador de Servidores
Esta seção descreve como toouse Olá Server Explorer no Visual Studio tooview todas as fábricas de dados de saudação em sua assinatura do Azure e criar um projeto do Visual Studio com base em uma fábrica de dados existente. 

1. Em **Visual Studio**, clique em **exibição** Olá menu e clique em **Server Explorer**.
2. Na janela do Gerenciador de servidores hello, expanda **Azure** e expanda **Data Factory**. Se você vir **entrar tooVisual Studio**, digite Olá **conta** associado à sua assinatura do Azure e clique em **continuar**. Insira a **senha** e clique em **Entrar**. O Visual Studio tenta tooget informações sobre todas as fábricas de dados do Azure em sua assinatura. Consulte status Olá dessa operação no hello **lista de tarefas de fábrica de dados** janela.

    ![Gerenciador de Servidores](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a>Criar um projeto do Visual Studio para um data factory existente

- Uma fábrica de dados no Gerenciador de servidores e selecione **tooNew exportar Data Factory projeto** toocreate um projeto do Visual Studio com base em uma fábrica de dados existente.

    ![Exportar dados fábrica tooa VS projeto](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a>Atualizar ferramentas de data factory para o Visual Studio
ferramentas do Azure Data Factory tooupdate para Visual Studio, Olá etapas a seguir:

1. Clique em **ferramentas** no menu hello e selecione **extensões e atualizações**. 
2. Selecione **atualizações** Olá painel esquerdo e, em seguida, selecione **Galeria do Visual Studio**.
3. Selecione **Ferramentas do Azure Data Factory para Visual Studio** e clique em **Atualizar**. Se você não vir essa entrada, você já tem a versão mais recente Olá das ferramentas de saudação. 

## <a name="use-configuration-files"></a>Usar arquivos de configuração
Você pode usar arquivos de configuração nas propriedades do Visual Studio tooconfigure para serviços/tabelas/pipelines vinculados diferentes para cada ambiente.

Considere Olá após a definição de JSON para um serviço vinculado do armazenamento do Azure. toospecify **connectionString** com valores diferentes para accountname e accountkey com base em Olá toowhich de ambiente (desenvolvimento/teste/produção), você está implantando entidades da fábrica de dados. Você pode obter esse comportamento usando um arquivo de configuração separado para cada ambiente.

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

### <a name="add-a-configuration-file"></a>Adicionar um arquivo de configuração
Adiciona um arquivo de configuração para cada ambiente executando Olá etapas a seguir:   

1. Clique com botão direito Olá fábrica de dados em sua solução do Visual Studio, aponte muito**adicionar**e clique em **novo item**.
2. Selecione **Config** na lista de saudação de modelos instalados Olá esquerda, selecione **arquivo de configuração**, insira um **nome** para a configuração de saudação do arquivo e, em seguida, clique em **Adicionar**.

    ![Adicionar arquivo de configuração](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. Adicione os parâmetros de configuração e seus valores hello formato a seguir:

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    Este exemplo configura a propriedade connectionString de um serviço de Armazenamento do Azure vinculado e um serviço vinculado do Azure SQL. Observe que a sintaxe de saudação para especificar o nome é [JsonPath](http://goessner.net/articles/JsonPath/).   

    Se o JSON tem uma propriedade que tem uma matriz de valores, conforme mostrado na saudação de código a seguir:  

    ```json
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
    ```

    Configure as propriedades conforme mostrado no hello (use indexação com base em zero) do arquivo de configuração a seguir:

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a>Nomes de propriedade com espaços
Se um nome de propriedade tiver espaços, use colchetes, conforme mostrado no hello (nome do servidor de banco de dados) de exemplo a seguir:

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a>Implantar a solução usando uma configuração
Quando você estiver publicando entidades do Azure Data Factory no VS, você pode especificar a configuração de saudação que você deseja toouse para essa operação de publicação.

toopublish entidades em um projeto do Azure Data Factory usando arquivo de configuração:   

1. Clique com botão direito fábrica de dados e clique em **publicar** toosee Olá **publicar itens** caixa de diálogo.
2. Selecione uma fábrica de dados existente ou especificar valores para a criação de uma fábrica de dados em Olá **fábrica de dados configurar** página e, em seguida, clique em **próximo**.   
3. Em Olá **publicar itens** página: você verá uma lista suspensa com as configurações disponíveis para Olá **Selecionar configuração de implantação** campo.

    ![Selecionar arquivo de configuração](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. Selecione Olá **arquivo de configuração** que deseja toouse e clique em **próximo**.
5. Confirme que você vê o nome de saudação do arquivo JSON Olá **resumo** página e clique em **próximo**.
6. Clique em **concluir** após a operação de implantação de saudação.

Quando você implanta, valores de saudação do arquivo de configuração de saudação são tooset usados valores para as propriedades nos arquivos de JSON Olá antes entidades Olá tooAzure implantado o serviço de fábrica de dados.   

## <a name="use-azure-key-vault"></a>Usar o Cofre de Chaves do Azure
Não é aconselhável e em relação a dados confidenciais de segurança política toocommit como repositório de código de toohello de cadeias de caracteres de conexão. Consulte [ADF seguro publicar](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) no GitHub toolearn sobre como armazenar informações confidenciais no cofre de chaves do Azure e usá-lo durante a publicação de entidades da fábrica de dados de exemplo. Olá seguro publicar a extensão do Visual Studio permite Olá toobe de segredos armazenada no cofre de chave e somente referências toothem são especificados em serviços vinculados / configurações de implantação. Essas referências são resolvidas quando você publica tooAzure de entidades da fábrica de dados. Esses arquivos podem ser confirmadas toosource repositório sem expor nenhum segredo.


## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você usou o armazenamento de blobs do Azure como um armazenamento de dados de origem e um banco de dados SQL do Azure como um armazenamento de dados de destino em uma operação de cópia. Olá tabela a seguir fornece uma lista de repositórios de dados com suporte como origens e destinos de atividade de cópia de saudação: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn sobre como armazenam dados toocopy para/de uma data, clique o link Olá Olá repositório de dados na tabela de saudação.
