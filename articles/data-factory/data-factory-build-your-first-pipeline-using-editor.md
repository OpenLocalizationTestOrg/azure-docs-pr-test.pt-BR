---
title: "aaaBuild sua primeira fábrica de dados (portal do Azure) | Microsoft Docs"
description: "Neste tutorial, você deve criar um pipeline do Azure Data Factory de exemplo usando o Editor de fábrica de dados em Olá portal do Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a>Tutorial: Compilar sua primeira Azure Data Factory usando o portal do Azure
> [!div class="op_single_selector"]
> * [Visão geral e pré-requisitos](data-factory-build-your-first-pipeline.md)
> * [Portal do Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modelo do Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)


Neste artigo, você aprenderá como toouse [portal do Azure](https://portal.azure.com/) toocreate sua primeira data factory do Azure. tutorial de saudação toodo usando outras ferramentas/SDKs, selecione uma das opções de saudação da lista suspensa de saudação. 

pipeline de saudação neste tutorial tem uma atividade: **atividade Hive do HDInsight**. Essa atividade executa um script do hive em um cluster de HDInsight do Azure que transforma dados de saída de tooproduce de entrada. pipeline de saudação é agendado toorun depois de um mês entre hello especificar horários de início e término. 

> [!NOTE]
> pipeline de dados Olá neste tutorial transforma dados de saída de tooproduce de dados de entrada. Para obter um tutorial sobre como toocopy dados usando a fábrica de dados do Azure, consulte [Tutorial: copiar dados de armazenamento de Blob tooSQL banco de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Um pipeline pode ter mais de uma atividade. E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada. Para saber mais, confira [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

## <a name="prerequisites"></a>Pré-requisitos
1. Leia [visão geral do Tutorial](data-factory-build-your-first-pipeline.md) artigo e hello completa **pré-requisito** etapas.
2. Este artigo não fornece uma visão geral conceitual de saudação serviço do Azure Data Factory. É recomendável que você passe por [tooAzure Introdução Data Factory](data-factory-introduction.md) artigo para uma visão geral detalhada do serviço de saudação.  

## <a name="create-data-factory"></a>Criar um data factory
Uma fábrica de dados pode ter um ou mais pipelines. Um pipeline em um data factory pode ter uma ou mais atividades. Por exemplo, dados de toocopy uma atividade de cópia de um repositório de dados de destino do código-fonte tooa e uma atividade de Hive do HDInsight toorun um tootransform de script do Hive dados de saída de tooproduct dados de entrada. Vamos começar com a criação de fábrica de dados Olá nesta etapa.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. Clique em **novo** no menu esquerdo Olá **dados + análise**e clique em **fábrica de dados**.

   ![Folha Criar](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. Em Olá **nova fábrica de dados** folha, digite **GetStartedDF** para Olá nome.

   ![Folha Nova data factory](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > nome de saudação do hello data factory do Azure deve ser **globalmente exclusivo**. Se você receber o erro Olá: **"GetStartedDF" nome da fábrica de dados não está disponível**. Alterar nome Olá Olá da fábrica de dados (por exemplo, yournameGetStartedDF) e tente criar novamente. Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.
   >
   > nome de Olá Olá da fábrica de dados pode ser registrado como um **DNS** nome no futuro hello e, portanto, se tornarão visíveis publicamente.
   >
   >
4. Selecione Olá **assinatura do Azure** onde você deseja Olá toobe de fábrica de dados criado.
5. Selecione um **grupo de recursos** existente ou crie um grupo de recursos. Tutorial de hello, crie um grupo de recursos chamado: **ADFGetStartedRG**.
6. Selecione Olá **local** Olá fábrica de dados. Somente regiões Olá serviço da fábrica de dados com suporte são mostrados na lista suspensa de saudação.
7. Selecione **toodashboard Pin**. 
8. Clique em **criar** em Olá **nova fábrica de dados** folha.

   > [!IMPORTANT]
   > toocreate instâncias de fábrica de dados, você deve ser um membro da saudação [colaborador da fábrica de dados](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) função no nível do grupo de recursos de assinatura/hello.
   >
   >
7. No painel hello, você vê Olá seguinte lado a lado com o status: Implantando fábrica de dados.    

   ![Status da criação da data factory](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. Parabéns! Você criou com êxito sua primeira data factory. Depois de fábrica de dados Olá tiver sido criada com êxito, você ver a página de fábrica de dados hello, que mostra Olá conteúdo Olá da fábrica de dados.     

    ![Folha Data Factory](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

Antes de criar um pipeline na fábrica de dados Olá, é necessário toocreate algumas entidades da fábrica de dados pela primeira vez. Você primeiro criar dados de toolink serviços vinculados repositórios/calcula tooyour dados armazenam, definem a entrada e saída de dados de entrada/saída toorepresent conjuntos de dados em repositórios de dados vinculados e, em seguida, criar o pipeline de saudação com uma atividade que usa esses conjuntos de dados.

## <a name="create-linked-services"></a>Criar serviços vinculados
Nesta etapa, você pode vincular sua conta de armazenamento do Azure e uma fábrica de dados sob demanda do Azure HDInsight cluster tooyour. Olá conta de armazenamento do Azure mantém Olá dados de entrada e saídos para o pipeline de saudação neste exemplo. Olá serviço vinculado do HDInsight é toorun usado um script de Hive especificado na atividade de saudação do pipeline de saudação neste exemplo. Identificar o que [repositório de dados](data-factory-data-movement-activities.md)/[serviços de computação](data-factory-compute-linked-services.md) são usados em seu cenário e vincular a fábrica de dados desses serviços toohello criando serviços vinculados.  

### <a name="create-azure-storage-linked-service"></a>Criar o serviço vinculado do armazenamento do Azure
Nesta etapa, você vincular sua fábrica de dados de tooyour de conta de armazenamento do Azure. Neste tutorial, você use Olá mesma conta de armazenamento do Azure, dados de entrada/saída toostore e hello HQL arquivo de script.

1. Clique em **autor e implantar** em Olá **DATA FACTORY** folha para **GetStartedDF**. Você deve ver Olá Editor da fábrica de dados.

   ![Bloco Criar e implantar](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. Clique em **Novo repositório de dados** e escolha **Armazenamento do Azure**.

   ![Novo armazenamento de dados - Armazenamento do Azure - menu](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. Você deve ver Olá script JSON para a criação de um armazenamento do Azure vinculada serviço no editor de saudação.

   ![Serviço vinculado de armazenamento do Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Substituir **nome da conta** com nome de saudação da sua conta de armazenamento do Azure e **chave de conta** com a chave de acesso de saudação do Olá conta de armazenamento do Azure. toolearn como tooget acessar o armazenamento de chave, consulte Olá informações sobre como tooview, copiar e armazenamento regenerar chaves de acesso em [gerenciar sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. Clique em **implantar** no comando Olá barra toodeploy Olá vinculado serviço.

    ![Botão Implantar](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   Depois de hello serviço vinculado foi implantado com êxito, Olá **rascunho 1** janela desaparecerá e você verá **AzureStorageLinkedService** na exibição de árvore Olá Olá esquerda.

    ![Serviço Vinculado de Armazenamento no menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a>Criar o serviço vinculado do Azure HDInsight
Nesta etapa, você vincular uma fábrica de dados sob demanda HDInsight cluster tooyour. cluster do HDInsight Olá é criado em tempo de execução e excluído após a conclusão ocioso e processamento para o período de tempo especificado Olá automaticamente.

1. Em Olá **Editor da fábrica de dados**, clique em **... Mais**, clique em **Nova computação** e selecione **Cluster HDInsight sob demanda**.

    ![Nova computação](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. Copie e cole Olá toohello de trecho de código a seguir **rascunho 1** janela. trecho JSON a saudação descreve propriedades Olá Olá toocreate usado cluster de HDInsight sob demanda.

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
   | ClusterSize |Especifica o tamanho de saudação do cluster do HDInsight hello. |
   | TimeToLive | Especifica que Olá de tempo ocioso para um cluster do HDInsight hello, antes de ser excluído. |
   | linkedServiceName | Especifica a conta de armazenamento de saudação que é usado toostore logs de Olá gerados pelo HDInsight. |

    Observe Olá pontos a seguir:

   * Olá fábrica de dados cria um **baseados em Linux** cluster HDInsight para você com hello JSON. Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.
   * Você pode usar **seu próprio cluster do HDInsight** em vez de usar um cluster do HDInsight sob demanda. Confira [Serviço vinculado do HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.
   * Olá HDInsight cluster cria um **contêiner padrão** no armazenamento de blob Olá especificado no hello JSON (**linkedServiceName**). HDInsight não exclui esse contêiner quando Olá cluster é excluído. Este comportamento ocorre por design. Com o serviço vinculado HDInsight sob demanda, um cluster HDInsight é criado sempre que uma fatia é processada, a menos que haja um cluster ativo existente (**timeToLive**). cluster de saudação é excluído automaticamente quando Olá processamento é concluído.

       Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure. Se não precisar para solução de problemas de trabalhos de saudação, talvez você queira toodelete-os custos de armazenamento do tooreduce hello. nomes de saudação desses contêineres seguem um padrão: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Use ferramentas como [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com/) armazenamento de blobs de contêineres toodelete do Azure.

     Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.
3. Clique em **implantar** no comando Olá barra toodeploy Olá vinculado serviço.

    ![Implantar o serviço vinculado do HDInsight sob demanda](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. Confirme que você vê ambos **AzureStorageLinkedService** e **HDInsightOnDemandLinkedService** na exibição de árvore Olá Olá esquerda.

    ![Modo de exibição de árvore com serviços vinculados](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a>Criar conjuntos de dados
Nesta etapa, você cria conjuntos de dados toorepresent Olá entrada e saída de dados para o processamento do Hive. Esses conjuntos de dados Consulte toohello **AzureStorageLinkedService** você tiver criado anteriormente neste tutorial. Olá tooan de pontos de serviço vinculado conta de armazenamento do Azure e conjuntos de dados especificam contêiner, pasta, nome do arquivo no armazenamento de saudação que contém a entrada e saída de dados.   

### <a name="create-input-dataset"></a>Criar conjunto de dados de entrada
1. Em Olá **Editor da fábrica de dados**, clique em **... Mais** na barra de comandos de saudação, clique em **novo conjunto de dados**e selecione **armazenamento de BLOBs do Azure**.

    ![Novo conjunto de dados](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. Copie e cole Olá janela toohello rascunho-1 de trecho de código a seguir. No trecho JSON a saudação, você está criando um conjunto de dados chamado **AzureBlobInput** que representa dados de entrada de uma atividade no pipeline de saudação. Além disso, você especificar que os dados de entrada hello estão localizados no contêiner de blob Olá chamado **adfgetstarted** e Olá pasta chamada **inputdata**.

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
    Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:

   | Propriedade | Descrição |
   |:--- |:--- |
   | type |propriedade do tipo Hello está definida muito**AzureBlob** porque os dados residem em um armazenamento de BLOBs do Azure. |
   | linkedServiceName |Refere-se toohello **AzureStorageLinkedService** criado anteriormente. |
   | folderPath | Especifica o blob Olá **contêiner** e hello **pasta** que contém blobs de entrada. | 
   | fileName |Essa propriedade é opcional. Se você omitir essa propriedade, todos os arquivos de saudação do hello folderPath são escolhidos. Neste tutorial, apenas Olá **input.log** é processado. |
   | type |arquivos de log de saudação estão no formato de texto, para que possamos usar **TextFormat**. |
   | columnDelimiter |as colunas nos arquivos de log de saudação são delimitadas por **caractere de vírgula (`,`)** |
   | frequência/intervalo |frequência definida muito**mês** e o intervalo é **1**, que significa que Olá fatias estão disponíveis mensal de entrada. |
   | externo | Essa propriedade é definida, muito**true** se os dados de entrada hello não foi gerados por este pipeline. Neste tutorial, o arquivo de input.log de saudação não é gerado por este pipeline para definimos Olá tootrue de propriedade. |

    Para saber mais sobre essas propriedades JSON, confira o [artigo sobre o conector do Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties).
3. Clique em **implantar** no comando Olá barra toodeploy Olá recém-criado dataset. Você deve ver a saudação de conjunto de dados na exibição de árvore Olá Olá esquerda.

### <a name="create-output-dataset"></a>Criar conjunto de dados de saída
Agora, você pode criar hello saída dataset toorepresent Olá saída dados armazenados em Olá armazenamento de BLOBs do Azure.

1. Em Olá **Editor da fábrica de dados**, clique em **... Mais** na barra de comandos de saudação, clique em **novo conjunto de dados**e selecione **armazenamento de BLOBs do Azure**.  
2. Copie e cole Olá janela toohello rascunho-1 de trecho de código a seguir. No trecho JSON a saudação, você está criando um conjunto de dados chamado **AzureBlobOutput**e especificar a estrutura de saudação de dados de saudação que são produzidos pelo script do Hive hello. Além disso, você especificar que os resultados de hello são armazenados no contêiner de blob Olá chamado **adfgetstarted** e Olá pasta chamada **partitioneddata**. Olá **disponibilidade** seção especifica esse conjunto de dados de saída de saudação é produzido por mês.

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
    Consulte **criar conjunto de dados de entrada hello** seção para obter descrições dessas propriedades. Você não definir propriedade externa Olá em um conjunto de dados de saída como Olá dataset é produzido pelo serviço da fábrica de dados hello.
3. Clique em **implantar** no comando Olá barra toodeploy Olá recém-criado dataset.
4. Verifique se o que conjunto de dados Olá é criado com êxito.

    ![Modo de exibição de árvore com serviços vinculados](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a>Criar um pipeline
Nesta etapa, você cria seu primeiro pipeline com a atividade **HDInsightHive** . Entrada fatia está disponível mensal (frequência: mês, intervalo: 1), fatias de saída é produzida mensal e Olá Agendador para a atividade de saudação é também definida toomonthly. Olá configurações para o conjunto de dados de saída de hello e Agendador de atividade de saudação devem corresponder. Atualmente, o conjunto de dados de saída é quais unidades Olá agendamento, então você deve criar um conjunto de dados de saída, mesmo que a atividade de saudação não produz nenhuma saída. Se a atividade de saudação não tem nenhuma entrada, você poderá ignorar o dataset de entrada hello criando. Propriedades de saudação usadas em Olá JSON a seguir são explicadas no final desta seção hello.

1. Em Olá **Editor da fábrica de dados**, clique em **reticências (...) Comandos mais** e, em seguida, clique em **novo pipeline**.

    ![botão novo pipeline](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. Copie e cole Olá janela toohello rascunho-1 de trecho de código a seguir.

   > [!IMPORTANT]
   > Substituir **storageaccountname** com o nome da saudação de sua conta de armazenamento Olá JSON.
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
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
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    No trecho JSON a saudação, você está criando um pipeline que consiste em uma única atividade que usa o Hive tooprocess dados em um cluster HDInsight.

    arquivo de script do Hive Hello, **partitionweblogs.hql**, é armazenado no hello conta de armazenamento do Azure (especificado por scriptLinkedService hello, chamado **AzureStorageLinkedService**) e em  **script** pasta no contêiner Olá **adfgetstarted**.

    Olá **define** seção é toospecify usadas configurações de tempo de execução de saudação que são passadas script do hive toohello como valores de configuração do Hive (por exemplo ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).

    Olá **iniciar** e **final** propriedades do pipeline de saudação especifica o período ativo de saudação do pipeline de saudação.

    Atividade Olá JSON, você especificar esse script de Hive Olá é executado em computação Olá especificada pelo Olá **linkedServiceName** – **HDInsightOnDemandLinkedService**.

   > [!NOTE]
   > Consulte "JSON de Pipeline" [Pipelines e atividades do Azure Data Factory](data-factory-create-pipelines.md) para obter detalhes sobre as propriedades JSON usados no exemplo hello.
   >
   >
3. Confirme a seguir hello:

   1. **Input.log** arquivo existe no hello **inputdata** pasta da saudação **adfgetstarted** contêiner no hello armazenamento de BLOBs do Azure
   2. **partitionweblogs.HQL** arquivo existe no hello **script** pasta da saudação **adfgetstarted** contêiner no hello armazenamento de BLOBs do Azure. Etapas de pré-requisito concluída Olá no hello [visão geral do Tutorial](data-factory-build-your-first-pipeline.md) se você não vir esses arquivos.
   3. Confirme que você substituiu **storageaccountname** com o nome da saudação de sua conta de armazenamento Olá JSON de pipeline.
4. Clique em **implantar** no pipeline de saudação toodeploy da barra de comandos de saudação. Desde Olá **iniciar** e **final** horários são definidos no hello anterior e **isPaused** é conjunto toofalse, pipeline Olá execuções (atividade no pipeline de saudação) imediatamente após a implantação.
5. Confirme que você vê pipeline Olá Olá na exibição em árvore.

    ![Modo de exibição de árvore com pipeline](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. Parabéns, você criou com sucesso seu primeiro pipeline!

## <a name="monitor-pipeline"></a>Monitorar o pipeline
### <a name="monitor-pipeline-using-diagram-view"></a>Monitorar o pipeline usando a Exibição de Diagrama
1. Clique em **X** tooclose Editor da fábrica de dados folhas toonavigate fazer toohello folha de fábrica de dados e clique em **diagrama**.

    ![Bloco do diagrama](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. Saudação de exibição de diagrama, você verá uma visão geral dos pipelines hello e conjuntos de dados usados neste tutorial.

    ![Exibição de diagrama](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. tooview todas as atividades no pipeline hello, pipeline com o botão direito no hello diagrama e clique em Abrir Pipeline.

    ![Menu do pipeline aberto](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. Confirme que você ver a atividade de HDInsightHive Olá no pipeline de saudação.

    ![Abrir a exibição do pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    toonavigate fazer toohello modo de exibição anterior, clique em **fábrica de dados** no menu de navegação estrutural Olá na parte superior da saudação.
5. Em Olá **exibição de diagrama**, clique duas vezes no conjunto de dados Olá **AzureBlobInput**. Confirmar essa fatia hello está **pronto** estado. Pode levar alguns minutos para Olá fatia tooshow até em estado pronto. Se isso não acontece depois que você aguarde algum tempo, ver se há Olá arquivo de entrada (input.log) colocado no contêiner de saudação à direita (adfgetstarted) e na pasta (inputdata).

   ![Fatia de entrada no estado pronto](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. Clique em **X** tooclose **AzureBlobInput** folha.
7. Em Olá **exibição de diagrama**, clique duas vezes no conjunto de dados Olá **AzureBlobOutput**. Você verá essa fatia Olá que está sendo processada atualmente.

   ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. Quando o processamento é concluído, você verá fatia Olá **pronto** estado.

   ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > A criação de um cluster do HDInsight sob demanda geralmente leva algum tempo (20 minutos, aproximadamente). Portanto, espere pipeline Olá levar muito **aproximadamente 30 minutos** tooprocess Olá fatia.
   >
   >

9. Quando a fatia hello está em **pronto** de estado, verifique Olá **partitioneddata** pasta Olá **adfgetstarted** contêiner no seu armazenamento de blob para Olá dados de saída.  

   ![dados de saída](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. Clique em Olá fatia toosee detalhes sobre ele em um **fatia de dados** folha.

   ![Detalhes da fatia de dados](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. Clique em uma saudação de execução da atividade **atividade é executada a lista** toosee detalhes sobre uma atividade de execução (atividade de Hive em nosso cenário) um **detalhes da execução de atividade** janela.   

   ![Detalhes da execução da atividade](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   Olá dos arquivos de log, você pode ver informações de status e de consulta de Hive Olá que foi executada. Esses logs são úteis para solucionar problemas.
   Confira o artigo [Monitorar e gerenciar pipelines usando as folhas do portal do Azure](data-factory-monitor-manage-pipelines.md) para obter mais detalhes.

> [!IMPORTANT]
> arquivo de entrada Hello é excluído quando a fatia de saudação é processada com êxito. Portanto, se você deseja toorerun Olá fatia ou Olá tutorial novamente, pasta de carregamento Olá arquivo de entrada (input.log) toohello inputdata do contêiner de adfgetstarted hello.
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a>Monitorar o pipeline usando o aplicativo Monitorar e Gerenciar
Você também pode usar o Monitor de & Gerenciar aplicativo toomonitor seus pipelines. Para obter informações detalhadas sobre como usar esse aplicativo, confira [Monitorar e gerenciar pipelines do Azure Data Factory usando o aplicativo Monitorar e Gerenciar](data-factory-monitor-manage-app.md).

1. Clique em **monitorar e gerenciar** lado a lado na página inicial do hello sua fábrica de dados.

    ![Bloco Monitorar e Gerenciar](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. Você deve ver **Monitorar e Gerenciar aplicativo**. Saudação de alteração **hora de início** e **hora de término** toomatch início e término do pipeline e clique em **aplicar**.

    ![Aplicativo Monitorar e Gerenciar](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. Selecione uma janela de atividade no hello **atividade Windows** lista toosee detalhes sobre ele.

    ![Detalhes da janela Atividade](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

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

## <a name="see-also"></a>Consulte também
| Tópico | Descrição |
|:--- |:--- |
| [Pipelines](data-factory-create-pipelines.md) |Este artigo ajuda você a entender os pipelines e atividades do Azure Data Factory e como toouse-los tooconstruct ponta a ponta controladas por dados fluxos de trabalho para seu cenário ou business. |
| [Conjunto de dados](data-factory-create-datasets.md) |Este artigo o ajuda a entender os conjuntos de dados no Azure Data Factory. |
| [Agendamento e execução](data-factory-scheduling-and-execution.md) |Este artigo explica os aspectos de programação e a execução de saudação do modelo de aplicativo do Azure Data Factory. |
| [Monitorar e gerenciar pipelines usando o Aplicativo de Monitoramento](data-factory-monitor-manage-app.md) |Este artigo descreve como toomonitor, gerenciar e depurar pipelines usando Olá monitoramento e gerenciamento de aplicativo. |
