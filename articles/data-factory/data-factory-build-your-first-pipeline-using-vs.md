---
title: "aaaBuild sua primeira fábrica de dados (Visual Studio) | Microsoft Docs"
description: "Neste tutorial, você cria um pipeline de exemplo do Azure Data Factory usando o Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 0c5eb01b685d978d80916da0293cc2d3701b2d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a>Tutorial: Como criar uma data factory usando o Visual Studio
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [Visão geral e pré-requisitos](data-factory-build-your-first-pipeline.md)
> * [Portal do Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modelo do Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)

Este tutorial mostra como toocreate uma fábrica de dados do Azure usando o Visual Studio. Criar um projeto do Visual Studio usando o modelo de projeto Olá fábrica de dados, definir entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline) no formato JSON e, em seguida, publicar/implantar essas entidades toohello nuvem. 

pipeline de saudação neste tutorial tem uma atividade: **atividade Hive do HDInsight**. Essa atividade executa um script do hive em um cluster de HDInsight do Azure que transforma dados de saída de tooproduce de entrada. pipeline de saudação é agendado toorun depois de um mês entre hello especificar horários de início e término. 

> [!NOTE]
> Este tutorial não mostra como copiar dados usando Azure Data Factory. Para obter um tutorial sobre como toocopy dados usando a fábrica de dados do Azure, consulte [Tutorial: copiar dados de armazenamento de Blob tooSQL banco de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Um pipeline pode ter mais de uma atividade. E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada. Para saber mais, confira [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="walkthrough-create-and-publish-data-factory-entities"></a>Passo a passo: Como criar e publicar as entidades da Data Factory
Aqui estão as etapas Olá que fazem parte deste passo a passo:

1. Crie dois serviços vinculados: **AzureStorageLinkedService1** e **HDInsightOnDemandLinkedService1**. 
   
    Neste tutorial, os dados de entrada e saídos para a atividade de hive Olá estão em Olá mesmo armazenamento de BLOBs do Azure. Usar um sob demanda HDInsight cluster tooprocess dados de entrada tooproduce saída os dados existentes. cluster do HDInsight sob demanda Olá é criado automaticamente para você pela fábrica de dados do Azure em tempo de execução quando os dados de entrada hello estão pronto toobe processado. É necessário toolink seus dados armazenam ou calcula tooyour fábrica de dados para que o serviço da fábrica de dados Olá pode se conectar a toothem em tempo de execução. Portanto, você vincular sua fábrica de dados de toohello de conta de armazenamento do Azure usando Olá AzureStorageLinkedService1 e vincular um cluster do HDInsight sob demanda usando Olá HDInsightOnDemandLinkedService1. Ao publicar, você deve especificar nome Olá Olá toobe de fábrica de dados criado ou uma fábrica de dados existente.  
2. Criar dois conjuntos de dados: **InputDataset** e **OutputDataset**, que representam dados de entrada/saída de saudação que são armazenados no hello armazenamento de BLOBs do Azure. 
   
    Essas definições de conjunto de dados Consulte toohello vinculado do armazenamento do Azure serviço criado na etapa anterior hello. Para Olá InputDataset, você especifica o contêiner de blob da saudação (adfgetstarted) e Olá pasta (inptutdata) que contém um blob com dados de entrada hello. Para Olá OutputDataset, especifique o contêiner de blob da saudação (adfgetstarted) e pasta hello (partitioneddata) que contém dados de saída de saudação. Você também pode especificar outras propriedades, como estrutura, disponibilidade e política.
3. Crie um pipeline chamado **MyFirstPipeline**. 
  
    Neste passo a passo, o pipeline de saudação tem apenas uma atividade: **atividade Hive do HDInsight**. Atividade transformar dados de entrada tooproduce os dados de saída ao executar um script de hive em um cluster do HDInsight sob demanda. toolearn mais sobre a atividade de hive, consulte [atividade de Hive](data-factory-hive-activity.md) 
4. Crie uma data factory denominada **DataFactoryUsingVS**. Implante Olá data factory e todas as entidades da fábrica de dados (serviços vinculados, tabelas e pipeline de saudação).
5. Depois de publicar, você usar folhas de portal do Azure e pipeline de saudação toomonitor monitoramento e gerenciamento de aplicativo. 
  
### <a name="prerequisites"></a>Pré-requisitos
1. Leia [visão geral do Tutorial](data-factory-build-your-first-pipeline.md) artigo e hello completa **pré-requisito** etapas. Você também pode selecionar Olá **visão geral e pré-requisitos** opção na lista de lista suspensa Olá no artigo do hello tooswitch superior toohello. Depois de concluir os pré-requisitos de hello, alternar toothis back artigo selecionando **Visual Studio** opção na lista suspensa de saudação.
2. toocreate instâncias de fábrica de dados, você deve ser um membro da saudação [colaborador da fábrica de dados](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) função no nível do grupo de recursos de assinatura/hello.  
3. Você deve ter o seguinte Olá instalado em seu computador:
   * Visual Studio 2013 ou Visual Studio 2015
   * Baixe o SDK do Azure para Visual Studio 2013 ou Visual Studio de 2015. Navegue muito[página de Download do Azure](https://azure.microsoft.com/downloads/) e clique em **VS 2013** ou **VS 2015** em Olá **.NET** seção.
   * Baixar hello mais recente do Azure Data Factory plug-in para Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) ou [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Você também pode atualizar plug-in de saudação fazendo Olá etapas a seguir: Olá menu, clique em **ferramentas** -> **extensões e atualizações** -> **Online**  ->  **Galeria do visual Studio** -> **ferramentas de fábrica de dados do Microsoft Azure para Visual Studio** -> **atualização**.

Agora, vamos usar o Visual Studio toocreate uma fábrica de dados do Azure.

### <a name="create-visual-studio-project"></a>Criar um projeto do Visual Studio
1. Inicie o **Visual Studio 2013** ou o **Visual Studio 2015**. Clique em **arquivo**, ponto muito**novo**e clique em **projeto**. Você deve ver Olá **novo projeto** caixa de diálogo.  
2. Em Olá **novo projeto** caixa de diálogo, selecione Olá **DataFactory** modelo e clique em **projeto vazio de fábrica de dados**.   

    ![Caixa de diálogo Novo projeto](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. Insira um **nome** para projeto hello, **local**e um nome para Olá **solução**e clique em **Okey**.

    ![Gerenciador de Soluções](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a>Criar serviços vinculados
Nesta etapa, você criará dois serviços vinculados: **Armazenamento do Azure** e **HDInsight sob demanda**. 

Olá armazenamento do Azure vinculada links de serviço sua fábrica de dados de toohello de conta de armazenamento do Azure, fornecendo informações de conexão de saudação. Serviço de fábrica de dados usa a cadeia de caracteres de conexão de saudação da configuração de serviço vinculada de saudação tooconnect toohello armazenamento do Azure em tempo de execução. Esse armazenamento contém entrado e dados de saída para o pipeline hello e hello hive usado pela atividade de hive de saudação do arquivo de script. 

Com o serviço vinculado do HDInsight sob demanda Olá cluster HDInsight é criado automaticamente em tempo de execução quando os dados de entrada hello estão tooprocessed pronto. cluster Olá é excluída após a conclusão ocioso e processamento para o período de tempo especificado hello. 

> [!NOTE]
> Você pode criar uma fábrica de dados especificando seu nome e as configurações em tempo de saudação de sua solução de fábrica de dados de publicação.

#### <a name="create-azure-storage-linked-service"></a>Criar o serviço vinculado do armazenamento do Azure
1. Clique com botão direito **serviços vinculados** no Gerenciador de soluções hello, ponto muito**adicionar**e clique em **Novo Item**.      
2. Em Olá **Adicionar Novo Item** caixa de diálogo, selecione **serviço vinculado do armazenamento do Azure** Olá lista e clique em **adicionar**.
    ![Serviço vinculado de armazenamento do Azure](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)
3. Substituir `<accountname>` e `<accountkey>` com o nome da saudação de sua conta de armazenamento do Azure e sua chave. toolearn como tooget acessar o armazenamento de chave, consulte Olá informações sobre como tooview, copiar e armazenamento regenerar chaves de acesso em [gerenciar sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
    ![Serviço vinculado de armazenamento do Azure](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)
4. Salvar Olá **AzureStorageLinkedService1.json** arquivo.

#### <a name="create-azure-hdinsight-linked-service"></a>Criar o serviço vinculado do Azure HDInsight
1. Em Olá **Solution Explorer**, clique com botão direito **serviços vinculados**, ponto muito**adicionar**e clique em **Novo Item**.
2. Selecione **erviço Vinculado Sob Demanda do HDInsight**  e clique em **Adicionar**.
3. Substituir saudação **JSON** com hello JSON a seguir:

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
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:

    Propriedade | Descrição
    -------- | ----------- 
    ClusterSize | Especifica o tamanho de saudação do hello cluster HDInsight Hadoop.
    TimeToLive | Especifica que Olá de tempo ocioso para um cluster do HDInsight hello, antes de ser excluído.
    linkedServiceName | Especifica a conta de armazenamento de saudação que é usado toostore logs de Olá gerados pelo cluster HDInsight Hadoop. 

    > [!IMPORTANT]
    > Olá HDInsight cluster cria um **contêiner padrão** no armazenamento de blob Olá especificado no hello JSON (linkedServiceName). HDInsight não exclui esse contêiner quando Olá cluster é excluído. Este comportamento ocorre por design. Com o serviço vinculado HDInsight sob demanda, um cluster do HDInsight é criado sempre que uma fatia é processada, a menos que haja um cluster ativo existente (timeToLive). cluster de saudação é excluído automaticamente quando Olá processamento é concluído.
    > 
    > Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure. Se não precisar para solução de problemas de trabalhos de saudação, talvez você queira toodelete-os custos de armazenamento do tooreduce hello. nomes de saudação desses contêineres seguem um padrão: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`. Use ferramentas como [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com/) armazenamento de blobs de contêineres toodelete do Azure.

    Para obter mais informações sobre as propriedades JSON, confira o artigo [Serviços vinculados de computação](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). 
4. Salvar Olá **HDInsightOnDemandLinkedService1.json** arquivo.

### <a name="create-datasets"></a>Criar conjuntos de dados
Nesta etapa, você cria conjuntos de dados toorepresent Olá entrada e saída de dados para o processamento do Hive. Esses conjuntos de dados Consulte toohello **AzureStorageLinkedService1** você tiver criado anteriormente neste tutorial. Olá tooan de pontos de serviço vinculado conta de armazenamento do Azure e conjuntos de dados especificam contêiner, pasta, nome do arquivo no armazenamento de saudação que contém a entrada e saída de dados.   

#### <a name="create-input-dataset"></a>Criar conjunto de dados de entrada
1. Em Olá **Solution Explorer**, clique com botão direito **tabelas**, ponto muito**adicionar**e clique em **Novo Item**.
2. Selecione **BLOBs do Azure** na lista de hello, altere o nome de saudação do arquivo de saudação muito**InputDataSet.json**e clique em **adicionar**.
3. Substituir saudação **JSON** no editor de saudação com hello trecho JSON a seguir:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    Este trecho JSON define um conjunto de dados chamado **AzureBlobInput** que representa dados de entrada para a atividade de hive Olá no pipeline de saudação. Você especificar que os dados de entrada hello estão localizados no contêiner de blob Olá chamado `adfgetstarted` e Olá pasta chamada `inputdata`.

    Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:

    Propriedade | Descrição |
    -------- | ----------- |
    type |propriedade do tipo Hello está definida muito**AzureBlob** porque os dados residem no armazenamento de BLOBs do Azure.
    linkedServiceName | Refere-se toohello AzureStorageLinkedService1 criado anteriormente.
    fileName |Essa propriedade é opcional. Se você omitir essa propriedade, todos os arquivos de saudação do hello folderPath são escolhidos. Nesse caso, somente Olá input.log é processado.
    type | arquivos de log Olá estão no formato de texto, para que possamos usar TextFormat. |
    columnDelimiter | colunas em arquivos de log de saudação são delimitadas por vírgula de saudação (`,`)
    frequência/intervalo | frequência definida tooMonth e o intervalo é 1, o que significa que as fatias de entrada hello estarão disponíveis mensalmente.
    externo | Essa propriedade é definida tootrue se os dados de entrada hello atividade Olá não são gerados pelo pipeline de saudação. Essa propriedade só é especificada em conjuntos de dados de entrada. Olá entrada conjunto de dados de atividade primeiro hello, sempre defina-tootrue.
4. Salvar Olá **InputDataset.json** arquivo.

#### <a name="create-output-dataset"></a>Criar conjunto de dados de saída
Agora, você pode criar dados de saída de toorepresent do hello saída conjunto de dados armazenados em Olá armazenamento de BLOBs do Azure.

1. Em Olá **Solution Explorer**, clique com botão direito **tabelas**, ponto muito**adicionar**e clique em **Novo Item**.
2. Selecione **BLOBs do Azure** na lista de hello, altere o nome de saudação do arquivo de saudação muito**OutputDataset.json**e clique em **adicionar**.
3. Substituir saudação **JSON** no editor de saudação com hello JSON a seguir:
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    trecho JSON a saudação define um conjunto de dados chamado **AzureBlobOutput** que representa os dados produzidos pela atividade de hive Olá no pipeline de saudação de saída. Você especificar que saída Olá dados são produzidos pela atividade de hive Olá é colocada no contêiner de blob Olá chamado `adfgetstarted` e Olá pasta chamada `partitioneddata`. 
    
    Olá **disponibilidade** seção especifica esse conjunto de dados de saída de saudação é produzido por mês. Olá dataset unidades Olá agenda do pipeline de saudação. pipeline de saudação é executado mensalmente entre suas horas de início e término. 

    Consulte **criar conjunto de dados de entrada hello** seção para obter descrições dessas propriedades. Você não definir propriedade externa Olá em um conjunto de dados de saída como Olá dataset é produzido pelo pipeline de saudação.
4. Salvar Olá **OutputDataset.json** arquivo.

### <a name="create-pipeline"></a>Criar um pipeline
Criar serviço de armazenamento do Azure vinculada Olá e conjuntos de dados de entrada e saídos até o momento. Agora, você pode criar um pipeline com uma atividade **HDInsightHive**. Olá **entrada** para hive hello atividade está definida muito**AzureBlobInput** e **saída** está definido muito**AzureBlobOutput**. Uma fatia de um conjunto de dados de entrada está disponível mensal (frequência: mês, intervalo: 1), e Olá saída fatia é produzida mensal muito. 

1. Em Olá **Solution Explorer**, clique com botão direito **Pipelines**, ponto muito**adicionar**e clique em **Novo Item.**
2. Selecione **Pipeline de transformação de Hive** Olá lista e clique em **adicionar**.
3. Substituir saudação **JSON** com hello trecho de código a seguir:

    > [!IMPORTANT]
    > Substituir `<storageaccountname>` com nome de saudação da sua conta de armazenamento.

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
                        "scriptLinkedService": "AzureStorageLinkedService1",
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

    > [!IMPORTANT]
    > Substituir `<storageaccountname>` com nome de saudação da sua conta de armazenamento.

    trecho JSON a saudação define um pipeline que consiste em uma única atividade (atividade de Hive). Essa atividade executa um script tooprocess entrada os dados de Hive em um cluster de HDInsight sob demanda dados de saída de tooproduce. Na seção de atividades de saudação do JSON de pipeline Olá, verá apenas uma atividade na matriz de saudação com o tipo definido muito**HDInsightHive**. 

    Propriedades de tipo hello que atividade de Hive tooHDInsight específico, você especifica qual serviço vinculado do armazenamento do Azure tem o arquivo de script de hive hello, o arquivo de script hello caminho toohello e o arquivo de script de toohello de parâmetros. 

    arquivo de script do Hive Hello, **partitionweblogs.hql**, são armazenados na conta de armazenamento do Azure hello (especificado pela Olá scriptLinkedService) e, em Olá `script` pasta no contêiner Olá `adfgetstarted`.

    Olá `defines` seção é toospecify usadas configurações de tempo de execução de saudação que são passadas script do hive toohello como valores de configuração do Hive (por exemplo `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.

    Olá **iniciar** e **final** propriedades do pipeline de saudação especifica o período ativo de saudação do pipeline de saudação. Você configurou Olá toobe de conjunto de dados produzido mensalmente, portanto, apenas uma vez a fatia é produzida pelo pipeline de saudação (porque o mês de saudação é a mesma datas inicial e final).

    Atividade Olá JSON, você especificar esse script de Hive Olá é executado em computação Olá especificada pelo Olá **linkedServiceName** – **HDInsightOnDemandLinkedService**.
4. Salvar Olá **HiveActivity1.json** arquivo.

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a>Adicionar partitionweblogs.hql e input.log como uma dependência
1. Clique com botão direito **dependências** em Olá **Solution Explorer** janela, ponto muito**adicionar**e clique em **Item existente**.  
2. Navegue toohello **C:\ADFGettingStarted** e selecione **partitionweblogs.hql**, **input.log** arquivos e clique em **adicionar**. Você criou esses dois arquivos como parte dos pré-requisitos de saudação [visão geral do Tutorial](data-factory-build-your-first-pipeline.md).

Quando você publica solução Olá na próxima etapa do hello, Olá **partitionweblogs.hql** arquivo é carregado toohello **script** pasta Olá `adfgetstarted` contêiner de blob.   

### <a name="publishdeploy-data-factory-entities"></a>Publicar/implantar entidades de data factory
Nesta etapa, você pode publicar entidades de fábrica de dados da saudação (serviços vinculados, conjuntos de dados e pipeline) no seu projeto toohello serviço do Azure Data Factory. No processo de saudação de publicação, você especifica o nome de saudação sua fábrica de dados. 

1. Clique com botão direito no Gerenciador de soluções do hello e, em seguida, clique em **publicar**.
2. Se você vir **entrar na conta da Microsoft de tooyour** caixa de diálogo, insira suas credenciais de conta de saudação que tenha a assinatura do Azure e clique em **entrar**.
3. Você deve ver Olá caixa de diálogo a seguir:

   ![Caixa de diálogo Publicar](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. Em Olá **fábrica de dados configurar** página, Olá seguintes etapas:

    ![Publicação - configurações da nova data factory](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. Selecione a opção **Criar Nova Data Factory** .
   2. Insira um único **nome** Olá fábrica de dados. Por exemplo: **DataFactoryUsingVS09152016**. Olá nome deve ser exclusivo.
   3. Selecione a assinatura à direita Olá para Olá **assinatura** campo. 
        > [!IMPORTANT]
        > Se você não vir nenhuma assinatura, certifique-se de que você fez logon usando uma conta que seja um administrador ou coadministrador da assinatura de saudação.
   4. Selecione Olá **grupo de recursos** para Olá toobe de fábrica de dados criado.
   5. Selecione Olá **região** Olá fábrica de dados.
   6. Clique em **próximo** tooswitch toohello **publicar itens** página. (Pressione **guia** toomove fora Olá Olá de tooif do campo de nome **próximo** botão será desabilitado.)

    > [!IMPORTANT]
    > Se você receber o erro Olá **"DataFactoryUsingVS" nome da fábrica de dados não está disponível** ao publicar, altere o nome de saudação (por exemplo, yournameDataFactoryUsingVS). Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.   
1. Em Olá **publicar itens** página, certifique-se de que todos os Olá fábricas de dados de entidades são selecionadas e clique em **próximo** tooswitch toohello **resumo** página.

    ![Publicar página de item](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. Revise o resumo de saudação e clique em **próximo** Olá de processo e o modo de exibição de implantação de saudação do toostart **Status da implantação**.

    ![Página Resumo](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. Em Olá **Status da implantação** página, você deve ver o status de Olá Olá do processo de implantação. Após a conclusão da implantação de saudação, clique em Concluir.

Toonote pontos importantes:

- Se você receber o erro Olá: **esta assinatura não está registrado toouse namespace DataFactory**, execute um dos seguintes hello e tente publicar novamente:
    - No Azure PowerShell, execute Olá provedor do comando tooregister Olá fábrica de dados a seguir.
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        Você pode executar Olá tooconfirm de comando a seguir que Olá Data Factory provedor está registrado.

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - Usando o logon Olá assinatura do Azure na toohello [portal do Azure](https://portal.azure.com) e navegue tooa folha de fábrica de dados (ou) criar uma fábrica de dados no hello portal do Azure. Esta ação registra automaticamente o provedor de saudação para você.
- nome Olá Olá da fábrica de dados pode ser registrado como um nome DNS no hello futuro e, portanto, se tornarão visível publicamente.
- toocreate instâncias de fábrica de dados, você precisa toobe um administrador ou coadministrador da saudação assinatura do Azure

### <a name="monitor-pipeline"></a>Monitorar o pipeline
Nesta etapa, você deve monitorar pipeline hello usando o modo de exibição de diagrama Olá da fábrica de dados. 

#### <a name="monitor-pipeline-using-diagram-view"></a>Monitorar o pipeline usando a Exibição de Diagrama
1. Faça logon no toohello [portal do Azure](https://portal.azure.com/), Olá seguintes etapas:
   1. Clique em **Mais serviços** e **Data factories**.
       
        ![Procurar data factories](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. Nome de saudação Select de sua fábrica de dados (por exemplo: **DataFactoryUsingVS09152016**) na lista de saudação de fábricas de dados.
   
       ![Selecionar o data factory](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. Na página de home Olá sua fábrica de dados, clique em **diagrama**.

    ![Bloco do diagrama](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. Saudação de exibição de diagrama, você verá uma visão geral dos pipelines hello e conjuntos de dados usados neste tutorial.

    ![Exibição de diagrama](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. tooview todas as atividades no pipeline hello, pipeline com o botão direito no hello diagrama e clique em Abrir Pipeline.

    ![Menu do pipeline aberto](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. Confirme que você ver a atividade de HDInsightHive Olá no pipeline de saudação.

    ![Abrir a exibição do pipeline](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    toonavigate fazer toohello modo de exibição anterior, clique em **fábrica de dados** no menu de navegação estrutural Olá na parte superior da saudação.
6. Em Olá **exibição de diagrama**, clique duas vezes no conjunto de dados Olá **AzureBlobInput**. Confirmar essa fatia hello está **pronto** estado. Pode levar alguns minutos para Olá fatia tooshow até em estado pronto. Se isso não acontece depois que você aguarde algum tempo, ver se há Olá arquivo de entrada (input.log) colocado no contêiner direito da saudação (`adfgetstarted`) e a pasta (`inputdata`). E, certifique-se de que Olá **externo** propriedade no conjunto de dados de entrada hello está definida muito**true**. 

   ![Fatia de entrada no estado pronto](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. Clique em **X** tooclose **AzureBlobInput** folha.
8. Em Olá **exibição de diagrama**, clique duas vezes no conjunto de dados Olá **AzureBlobOutput**. Você verá essa fatia Olá que está sendo processada atualmente.

   ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. Quando o processamento é concluído, você verá fatia Olá **pronto** estado.

   > [!IMPORTANT]
   > A criação de um cluster do HDInsight sob demanda geralmente leva algum tempo (20 minutos, aproximadamente). Portanto, espere Olá pipeline tootake **aproximadamente 30 minutos** tooprocess Olá fatia.  
   
    ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. Quando a fatia hello está em **pronto** de estado, verifique Olá `partitioneddata` pasta Olá `adfgetstarted` contêiner no seu armazenamento de blob para Olá dados de saída.  

    ![dados de saída](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. Clique em Olá fatia toosee detalhes sobre ele em um **fatia de dados** folha.

    ![Detalhes da fatia de dados](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. Clique em uma saudação de execução da atividade **atividade é executada a lista** toosee detalhes sobre uma atividade de execução (atividade de Hive em nosso cenário) um **detalhes da execução de atividade** janela. 
  
    ![Detalhes da execução da atividade](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    Olá dos arquivos de log, você pode ver informações de status e de consulta de Hive Olá que foi executada. Esses logs são úteis para solucionar problemas.  

Consulte [monitorar conjuntos de dados e pipeline](data-factory-monitor-manage-pipelines.md) para obter instruções sobre como pipeline de saudação do toouse Olá toomonitor portal do Azure e conjuntos de dados você tiver criado neste tutorial.

#### <a name="monitor-pipeline-using-monitor--manage-app"></a>Monitorar o pipeline usando o aplicativo Monitorar e Gerenciar
Você também pode usar o Monitor de & Gerenciar aplicativo toomonitor seus pipelines. Para obter informações detalhadas sobre como usar esse aplicativo, confira [Monitorar e gerenciar pipelines do Azure Data Factory usando o aplicativo Monitorar e Gerenciar](data-factory-monitor-manage-app.md).

1. Clique no bloco Monitorar e Gerenciar.

    ![Bloco Monitorar e Gerenciar](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. Você deve ver o aplicativo Monitorar e Gerenciar. Saudação de alteração **hora de início** e **hora de término** toomatch início (04-01-2016 12:00 AM) e término (2016-02-04 12:00 AM) do seu pipeline e clique em **aplicar**.

    ![Aplicativo Monitorar e Gerenciar](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. toosee detalhes sobre uma janela de atividade, selecione-o no hello **lista atividade Windows** toosee detalhes sobre ele.
    ![Detalhes da janela Atividade](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)

> [!IMPORTANT]
> arquivo de entrada Hello é excluído quando a fatia de saudação é processada com êxito. Portanto, se você deseja toorerun Olá fatia ou Olá tutorial novamente, carregar Olá arquivo de entrada (input.log) toohello `inputdata` pasta da saudação `adfgetstarted` contêiner.

### <a name="additional-notes"></a>Observações adicionais
- Uma fábrica de dados pode ter um ou mais pipelines. Um pipeline em um data factory pode ter uma ou mais atividades. Por exemplo, dados de toocopy uma atividade de cópia de um repositório de dados de destino do código-fonte tooa e uma atividade de Hive do HDInsight toorun um tootransform de script do Hive dados de entrada. Consulte [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para todos os Olá fontes e coletores suportados pelas hello atividade de cópia. Consulte [serviços vinculados de computação](data-factory-compute-linked-services.md) para lista de saudação de serviços de computação com suporte pela fábrica de dados.
- Serviços vinculados vincular armazenamentos de dados ou de computação serviços tooan data factory do Azure. Consulte [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para todos os Olá fontes e coletores suportados pelas hello atividade de cópia. Consulte [serviços vinculados de computação](data-factory-compute-linked-services.md) para lista de saudação de serviços de computação com suporte pela fábrica de dados e [atividades de transformação](data-factory-data-transformation-activities.md) que podem ser executadas neles.
- Consulte [mover dados do / Blob tooAzure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter detalhes sobre as propriedades JSON usados em Olá armazenamento do Azure vinculada a definição de serviço.
- Você pode usar seu próprio cluster do HDInsight em vez de usar um cluster do HDInsight sob demanda. Veja [Serviços vinculados de computação](data-factory-compute-linked-services.md) para obter detalhes.
-  Olá fábrica de dados cria um **baseados em Linux** cluster HDInsight para você com hello anterior JSON. Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.
- Olá HDInsight cluster cria um **contêiner padrão** no armazenamento de blob Olá especificado no hello JSON (linkedServiceName). HDInsight não exclui esse contêiner quando Olá cluster é excluído. Este comportamento ocorre por design. Com o serviço vinculado HDInsight sob demanda, um cluster do HDInsight é criado sempre que uma fatia é processada, a menos que haja um cluster ativo existente (timeToLive). cluster de saudação é excluído automaticamente quando Olá processamento é concluído.
    
    Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure. Se não precisar para solução de problemas de trabalhos de saudação, talvez você queira toodelete-os custos de armazenamento do tooreduce hello. nomes de saudação desses contêineres seguem um padrão: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Use ferramentas como [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com/) armazenamento de blobs de contêineres toodelete do Azure.
- Atualmente, o conjunto de dados de saída é quais unidades Olá agendamento, então você deve criar um conjunto de dados de saída, mesmo que a atividade de saudação não produz nenhuma saída. Se a atividade de saudação não tem nenhuma entrada, você poderá ignorar o dataset de entrada hello criando. 
- Este tutorial não mostra como copiar dados usando Azure Data Factory. Para obter um tutorial sobre como toocopy dados usando a fábrica de dados do Azure, consulte [Tutorial: copiar dados de armazenamento de Blob tooSQL banco de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).


## <a name="use-server-explorer-tooview-data-factories"></a>Use as fábricas de dados do Gerenciador de servidores tooview
1. Em **Visual Studio**, clique em **exibição** Olá menu e clique em **Server Explorer**.
2. Na janela do Gerenciador de servidores hello, expanda **Azure** e expanda **Data Factory**. Se você vir **entrar tooVisual Studio**, digite Olá **conta** associado à sua assinatura do Azure e clique em **continuar**. Insira a **senha** e clique em **Entrar**. O Visual Studio tenta tooget informações sobre todas as fábricas de dados do Azure em sua assinatura. Consulte status Olá dessa operação no hello **lista de tarefas de fábrica de dados** janela.

    ![Gerenciador de Servidores](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. Você pode uma fábrica de dados e selecione **tooNew exportar Data Factory projeto** toocreate um projeto do Visual Studio com base em uma fábrica de dados existente.

    ![Exportar data factory](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

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

## <a name="summary"></a>Resumo
Neste tutorial, você criou um tooprocess dados da fábrica de dados do Azure executando o script do Hive em um cluster de hadoop de HDInsight. Você usou Olá Editor da fábrica de dados em Olá toodo portal do Azure Olá etapas a seguir:  

1. Foi criada uma **data factory**do Azure.
2. Foram criados dois **serviços vinculados**:
   1. **Armazenamento do Azure** vinculado serviço toolink seu armazenamento de BLOBs do Azure que contém a fábrica de dados de toohello de arquivos de entrada/saída.
   2. **HDInsight do Azure** toolink de serviço vinculado sob demanda uma fábrica de dados sob demanda HDInsight Hadoop cluster toohello. A fábrica de dados do Azure cria um HDInsight Hadoop dados de entrada do cluster tooprocess just-in-time e produzir dados de saída.
3. Criados dois **conjuntos de dados**, que descrevem os dados de entrada e saídos para a atividade de Hive do HDInsight no pipeline de saudação.
4. Foi criado um **pipeline** com uma atividade **Hive do HDInsight**.  

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você criou um pipeline com uma atividade de transformação (atividade do HDInsight) que executa um script Hive em um cluster do HDInsight sob demanda. toosee como toouse dados de toocopy uma atividade de cópia de um tooAzure de BLOBs do Azure SQL, consulte [Tutorial: copiar dados de um tooAzure de BLOBs do Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

É possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada. Veja [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md) para obter informações detalhadas. 


## <a name="see-also"></a>Consulte também
| Tópico | Descrição |
|:--- |:--- |
| [Pipelines](data-factory-create-pipelines.md) |Este artigo ajuda você a entender os pipelines e atividades do Azure Data Factory e como toouse-los tooconstruct fluxos de trabalho controlados por dados para seu cenário ou business. |
| [Conjunto de dados](data-factory-create-datasets.md) |Este artigo o ajuda a entender os conjuntos de dados no Azure Data Factory. |
| [Atividades de transformação de dados](data-factory-data-transformation-activities.md) |Este artigo fornece uma lista de atividades de transformação de dados (como a transformação do Hive do HDInsight usado neste tutorial) com suporte do Azure Data Factory. |
| [Agendamento e execução](data-factory-scheduling-and-execution.md) |Este artigo explica os aspectos de programação e a execução de saudação do modelo de aplicativo do Azure Data Factory. |
| [Monitorar e gerenciar pipelines usando o Aplicativo de Monitoramento](data-factory-monitor-manage-app.md) |Este artigo descreve como toomonitor, gerenciar e depurar pipelines usando Olá monitoramento e gerenciamento de aplicativo. |
