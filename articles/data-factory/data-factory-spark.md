---
title: programas aaaInvoke Spark do Azure Data Factory | Microsoft Docs
description: "Saiba como programas de Spark tooinvoke de uma fábrica de dados do Azure usando hello atividade MapReduce."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a>Invocar programas Spark dos pipelines do Azure Data Factory

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

## <a name="introduction"></a>Introdução
Atividade do Spark é uma saudação [atividades de transformação de dados](data-factory-data-transformation-activities.md) com suporte do Azure Data Factory. Esta atividade é executada Olá especificado programa Spark no cluster do Apache Spark no HDInsight do Azure.    

> [!IMPORTANT]
> - A atividade do Spark não oferece suporte a clusters HDInsight Spark que usam um Azure Data Lake Store como armazenamento primário.
> - A atividade do Spark dá suporte apenas a clusters HDInsight Spark existentes (seus próprios). Ele não dá suporte a serviço vinculado ao HDInsight sob demanda.

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a>Passo a passo: criar um pipeline com atividade do Spark
Aqui estão as etapas típicas de saudação toocreate um pipeline da fábrica de dados com uma atividade Spark.  

1. Criar uma fábrica de dados.
2. Crie um toolink de serviço vinculado do armazenamento do Azure o armazenamento do Azure que está associado a sua fábrica de dados de toohello de cluster do HDInsight Spark.     
2. Crie um toolink de serviço vinculado do Azure HDInsight cluster Apache Spark na fábrica de dados do Azure HDInsight toohello.
3. Crie um conjunto de dados refere-se o serviço de armazenamento do Azure vinculada toohello. No momento, você deve especificar um conjunto de dados de saída para uma atividade mesmo que não exista nenhuma saída sendo produzida.  
4. Crie um pipeline com atividades Spark que refere-se o serviço vinculado do HDInsight de toohello criado no #2. Hello atividade está configurada com conjunto de dados de saudação que você criou na etapa anterior, Olá como um conjunto de dados de saída. conjunto de dados de saída de saudação é quais unidades Olá agenda (por hora, diariamente, etc.). Portanto, você deve especificar o conjunto de dados de saída de hello mesmo que a atividade de saudação realmente não produzir uma saída.

### <a name="prerequisites"></a>Pré-requisitos
1. Criar um **conta de armazenamento do Azure para fins gerais** seguindo as instruções passo a passo de saudação: [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account).  
2. Criar um **cluster Apache Spark no Azure HDInsight** seguindo as instruções no tutorial Olá: [cluster criar Apache Spark no Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Associe conta de armazenamento do Azure Olá criado na etapa &#1; com este cluster.  
3. Baixe e leia o arquivo de script de python Olá **test.py** localizado em: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).  
3.  Carregar **test.py** toohello **pyFiles** pasta Olá **adfspark** contêiner no seu armazenamento de BLOBs do Azure. Crie contêiner de saudação e a pasta de saudação se não existirem.

### <a name="create-data-factory"></a>Criar um data factory
Vamos começar com a criação de fábrica de dados Olá nesta etapa.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. Clique em **novo** no menu esquerdo Olá **dados + análise**e clique em **fábrica de dados**.
3. Em Olá **nova fábrica de dados** folha, digite **SparkDF** para Olá nome.

   > [!IMPORTANT]
   > nome de saudação do hello data factory do Azure deve ser **globalmente exclusivo**. Se você vir o erro Olá: **"SparkDF" nome da fábrica de dados não está disponível**. Alterar nome Olá Olá da fábrica de dados (por exemplo, yournameSparkDFdate e tente criar novamente. Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.   
4. Selecione Olá **assinatura do Azure** onde você deseja Olá toobe de fábrica de dados criado.
5. Selecione um **grupo de recursos** existente ou crie um grupo de recursos do Azure.
6. Selecione **toodashboard Pin** opção.  
6. Clique em **criar** em Olá **nova fábrica de dados** folha.

   > [!IMPORTANT]
   > toocreate instâncias de fábrica de dados, você deve ser um membro da saudação [colaborador da fábrica de dados](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) função no nível do grupo de recursos de assinatura/hello.
7. Você verá a fábrica de dados hello está sendo criada no hello **painel** de saudação portal do Azure da seguinte maneira:   
8. Depois de fábrica de dados Olá tiver sido criada com êxito, você ver a página de fábrica de dados hello, que mostra Olá conteúdo Olá da fábrica de dados. Se você não vir a página de fábrica de dados hello, clique em lado a lado para sua fábrica de dados no painel de Olá Olá.

    ![Folha Data Factory](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a>Criar serviços vinculados
Nesta etapa, você cria dois serviços vinculados, um toolink sua fábrica de dados Spark cluster tooyour e Olá outros toolink sua fábrica de dados do armazenamento do Azure tooyour.  

#### <a name="create-azure-storage-linked-service"></a>Criar o serviço vinculado do armazenamento do Azure
Nesta etapa, você vincular sua fábrica de dados de tooyour de conta de armazenamento do Azure. Um conjunto de dados que você criar em uma etapa posterior neste passo a passo refere-se o serviço toothis vinculado. Olá serviço vinculado do HDInsight que você define na próxima etapa do hello se refere a serviço toothis vinculado.  

1. Clique em **autor e implantar** em Olá **Data Factory** folha sua fábrica de dados. Você deve ver Olá Editor da fábrica de dados.
2. Clique em **Novo repositório de dados** e escolha **Armazenamento do Azure**.

   ![Novo armazenamento de dados - Armazenamento do Azure - menu](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. Você deve ver Olá **script JSON** para a criação de um armazenamento do Azure serviço no editor de saudação vinculado.

   ![Serviço vinculado de armazenamento do Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Substituir **nome da conta** e **chave de conta** com hello nome e chave de acesso da sua conta de armazenamento do Azure. toolearn como tooget acessar o armazenamento de chave, consulte Olá informações sobre como tooview, copiar e armazenamento regenerar chaves de acesso em [gerenciar sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. toodeploy Olá serviço vinculado, clique em **implantar** na barra de comandos de saudação. Depois de hello serviço vinculado foi implantado com êxito, Olá **rascunho 1** janela desaparecerá e você verá **AzureStorageLinkedService** na exibição de árvore Olá Olá esquerda.

#### <a name="create-hdinsight-linked-service"></a>Criar o serviço vinculado ao HDInsight
Nesta etapa, você criará toolink de serviço vinculado do Azure HDInsight sua fábrica de dados de toohello de cluster do HDInsight Spark. cluster do HDInsight Olá é programa de Spark de saudação toorun usado especificado na atividade de Spark saudação do pipeline de saudação neste exemplo.  

1. Clique em **... Mais** na barra de ferramentas hello, clique em **nova computação**e, em seguida, clique em **cluster HDInsight**.

    ![Criar o serviço vinculado ao HDInsight](media/data-factory-spark/new-hdinsight-linked-service.png)
2. Copie e cole Olá toohello de trecho de código a seguir **rascunho 1** janela. No editor de JSON de Olá Olá etapas a seguir:
    1. Especifique a saudação **URI** para Olá HDInsight Spark do cluster. Por exemplo: `https://<sparkclustername>.azurehdinsight.net/`.
    2. Especificar nome de saudação do hello **usuário** quem possui o cluster do Spark toohello acesso.
    3. Especifique a saudação **senha** do usuário.
    4. Especifique a saudação **serviço vinculado do armazenamento do Azure** associada à saudação cluster HDInsight Spark. Neste exemplo, é: **AzureStorageLinkedService**.

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - A atividade do Spark não oferece suporte a clusters HDInsight Spark que usam um Azure Data Lake Store como armazenamento primário.
    > - A atividade do Spark dá suporte apenas ao cluster HDInsight Spark existente (seu próprio). Ele não dá suporte a serviço vinculado ao HDInsight sob demanda.

    Consulte [serviço vinculado HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes sobre Olá HDInsight serviço vinculado.
3.  toodeploy Olá serviço vinculado, clique em **implantar** na barra de comandos de saudação.  

### <a name="create-output-dataset"></a>Criar conjunto de dados de saída
conjunto de dados de saída de saudação é quais unidades Olá agenda (por hora, diariamente, etc.). Portanto, você deve especificar um conjunto de dados de saída para a atividade do spark Olá no pipeline de saudação mesmo que a atividade de saudação realmente não produzir qualquer saída. A especificação de um conjunto de dados de entrada para a atividade de saudação é opcional.

1. Em Olá **Editor da fábrica de dados**, clique em **... Mais** na barra de comandos de saudação, clique em **novo conjunto de dados**e selecione **armazenamento de BLOBs do Azure**.  
2. Copie e cole Olá janela toohello rascunho-1 de trecho de código a seguir. trecho JSON a saudação define um conjunto de dados chamado **OutputDataset**. Além disso, você especificar que os resultados de hello são armazenados no contêiner de blob Olá chamado **adfspark** e Olá pasta chamada **pyFiles/saída**. Como mencionado anteriormente, esse conjunto de dados é fictício. programa Spark Olá neste exemplo não gera nenhuma saída. Olá **disponibilidade** seção especifica esse conjunto de dados de saída de saudação é produzido diariamente.  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy Olá conjunto de dados, clique em **implantar** na barra de comandos de saudação.


### <a name="create-pipeline"></a>Criar um pipeline
Nesta etapa, você cria um pipeline com a atividade **HDInsightSpark**. Atualmente, o conjunto de dados de saída é quais unidades Olá agendamento, então você deve criar um conjunto de dados de saída, mesmo que a atividade de saudação não produz nenhuma saída. Se a atividade de saudação não tem nenhuma entrada, você poderá ignorar o dataset de entrada hello criando. Portanto, nenhum conjunto de dados de entrada é especificado neste exemplo.

1. Em Olá **Editor da fábrica de dados**, clique em **... Mais** Olá barra de comandos e, em seguida, clique em **novo pipeline**.
2. Substitua script hello na janela Olá rascunho-1 com hello script a seguir:

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    Observe Olá pontos a seguir:
    - Olá **tipo** propriedade for definida muito**HDInsightSpark**.
    - Olá **rootPath** está definido muito**adfspark\\pyFiles** onde adfspark é o contêiner de BLOBs do Azure hello e pyFiles é a pasta bem no contêiner. Neste exemplo, Olá armazenamento de BLOBs do Azure é hello que está associado ao cluster do Spark hello. Você pode carregar Olá arquivo tooa armazenamento do Azure diferente. Se você fizer isso, crie um toolink de serviço vinculado do armazenamento do Azure essa fábrica de dados de toohello de conta de armazenamento. Em seguida, especifique o nome de Olá de serviço de Olá vinculado como um valor para Olá **sparkJobLinkedService** propriedade. Consulte [propriedades da atividade Spark](#spark-activity-properties) para obter detalhes sobre essa propriedade e outras propriedades com suporte hello atividade Spark.  
    - Olá **entryFilePath** está definida toohello **test.py**, que é o arquivo de python hello.
    - Olá **getDebugInfo** propriedade for definida muito**sempre**, que significa que os arquivos de log Olá sempre são gerados (sucesso ou falha).

        > [!IMPORTANT]
        > É recomendável que você não defina essa propriedade muito`Always` em um ambiente de produção, a menos que você estiver solucionando um problema.
    - Olá **gera** seção tem um conjunto de dados de saída. Você deve especificar um conjunto de dados de saída, mesmo que o programa de spark Olá não produz nenhuma saída. Olá dataset unidades Olá agenda para o pipeline de saudação (por hora, diariamente, etc.).  

        Para obter detalhes sobre as propriedades de hello atividade Spark com suporte, consulte [despertar propriedades da atividade](#spark-activity-properties) seção.
3. pipeline de saudação toodeploy, clique em **implantar** na barra de comandos de saudação.

### <a name="monitor-pipeline"></a>Monitorar o pipeline
1. Clique em **X** tooclose folhas de Editor de fábrica de dados e toonavigate home page do toohello fábrica de dados de volta. Clique em **monitorar e gerenciar** toolaunch Olá monitoramento do aplicativo em outra guia.

    ![Bloco Monitorar e Gerenciar](media/data-factory-spark/monitor-and-manage-tile.png)
2. Saudação de alteração **hora de início** filtrar na parte superior da saudação muito**1/2/2017**e clique em **aplicar**.
3. Como há somente um dia entre hello (2017-02-01) de início e término (2017-02-02) do pipeline Olá, você verá somente uma janela de atividade. Confirmar que a fatia de dados hello está **pronto** estado.

    ![Pipeline de saudação do monitor](media/data-factory-spark/monitor-and-manage-app.png)    
4. Selecione Olá **janela de atividade** toosee detalhes sobre a atividade de saudação executar. Se houver um erro, você pode ver detalhes sobre ele no painel direito da saudação.

### <a name="verify-hello-results"></a>Verificar os resultados de saudação

1. Inicie o **Notebook Jupyter** para seu cluster do HDInsight Spark, navegando até: https://NOMEDOCLUSTER.azurehdinsight.net/jupyter. Você pode também iniciar o painel do cluster para o cluster do HDInsight Spark e, em seguida, iniciar **Notebook Jupyter**.
2. Clique em **novo** -> **PySpark** toostart um novo bloco de anotações.

    ![Novo notebook Jupyter](media/data-factory-spark/jupyter-new-book.png)
3. Execução hello seguinte comando copiar/colar o texto de saudação e pressionando **SHIFT + ENTER** final Olá da segunda instrução de saudação.  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. Certifique-se de que você vê dados saudação da tabela de hvac hello:  

    ![Resultados da consulta do Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

Veja a seção [Executar uma consulta SQL do Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) para obter instruções detalhadas. 

### <a name="troubleshooting"></a>Solucionar problemas
Desde que você definir **getDebugInfo** muito**sempre**, você verá um **log** subpasta Olá **pyFiles** pasta em seu contêiner de BLOBs do Azure. arquivo de log de saudação na pasta de log Olá fornece detalhes adicionais. Esse arquivo de log é especialmente útil quando há um erro. Em um ambiente de produção, convém tooset-muito**falha**.

Para solução de problemas, Olá etapas a seguir:


1. Navegue muito`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.

    ![Aplicativo de interface do usuário do YARN](media/data-factory-spark/yarnui-application.png)  
2. Clique em **Logs** para uma saudação executar tentativas.

    ![Página do aplicativo](media/data-factory-spark/yarn-applications.png)
3. Você deve ver as informações de erro adicionais na página de registro de saudação.

    ![Log de erros](media/data-factory-spark/yarnui-application-error.png)

Olá seções a seguir fornece informações sobre o cluster do Data Factory entidades toouse Apache Spark e atividade do Spark sua fábrica de dados.

## <a name="spark-activity-properties"></a>Propriedades da Atividade do Spark
Aqui está a definição de JSON de exemplo hello de um pipeline com Spark atividade:    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

Olá tabela a seguir descreve as propriedades JSON Olá usadas na definição JSON da saudação:

| Propriedade | Descrição | Obrigatório |
| -------- | ----------- | -------- |
| name | Nome da atividade de saudação no pipeline de saudação. | Sim |
| description | Texto que descreve quais atividade Olá faz. | Não |
| type | Essa propriedade deve ser definida como tooHDInsightSpark. | Sim |
| linkedServiceName | Nome do hello HDInsight vinculado no qual Olá Spark executa o programa de serviço. | Sim |
| rootPath | contêiner de BLOBs do Azure Hello e pasta que contém o arquivo do Spark hello. nome do arquivo Hello diferencia maiusculas de minúsculas. | Sim |
| entryFilePath | Pasta de raiz de toohello de caminho relativo da saudação Spark/pacote de código. | Sim |
| className | Classe principal de Java/Spark do aplicativo | Não |
| argumentos | Uma lista de programas de Spark toohello argumentos de linha de comando. | Não |
| proxyUser | programa de saudação usuário conta tooimpersonate tooexecute Olá Spark | Não |
| sparkConfig | Especificar valores para propriedades de configuração do Spark listados no tópico Olá: [Spark configuração - propriedades de aplicativo](https://spark.apache.org/docs/latest/configuration.html#available-properties). | Não |
| getDebugInfo | Especifica quando arquivos de log do Spark Olá são copiado toohello usado pelo cluster do HDInsight de armazenamento do Azure (ou) especificado por sparkJobLinkedService. Valores permitidos: Nenhum, Sempre ou Falha. Valor padrão: Nenhum. | Não |
| sparkJobLinkedService | Olá serviço vinculado do armazenamento do Azure que contém o arquivo de trabalho do Spark hello, dependências e logs.  Se você não especificar um valor para essa propriedade, armazenamento de saudação associado com o cluster HDInsight é usado. | Não |

## <a name="folder-structure"></a>Estrutura de pastas
Hello atividade Spark não oferece suporte a um script em linha como o Pig e Hive atividades realizar. Os trabalhos do Spark também são mais extensíveis do que trabalhos do Pig/Hive. Para trabalhos de Spark, você pode fornecer várias dependências, como jar pacotes (colocados em java Olá CLASSPATH), arquivos de python (colocados nos Olá PYTHONPATH) e outros arquivos.

Crie hello seguindo a estrutura de pastas no hello referenciado por Olá serviço vinculado do HDInsight de armazenamento de Blob do Azure. Em seguida, carregue os arquivos dependentes toohello apropriado subpastas na pasta raiz de saudação representado por **entryFilePath**. Por exemplo, carregar subpasta do python arquivos toohello pyFiles e jar arquivos toohello jars subpasta da pasta raiz de saudação. Em tempo de execução, o serviço de fábrica de dados espera Olá seguindo a estrutura de pastas no hello armazenamento de BLOBs do Azure:     

| Caminho | Descrição | Obrigatório | Tipo |
| ---- | ----------- | -------- | ---- |
| . | caminho de raiz de saudação do trabalho do Spark Olá no serviço vinculado de armazenamento de saudação    | Sim | Pasta |
| &lt;definido pelo usuário&gt; | caminho de saudação apontando toohello arquivo de entrada do trabalho de Spark Olá | Sim | Arquivo |
| ./jars | Todos os arquivos nesta pasta são carregados e colocados no classpath java de saudação do cluster de saudação | Não | Pasta |
| ./pyFiles | Todos os arquivos nesta pasta são carregados e colocados em Olá PYTHONPATH de cluster Olá | Não | Pasta |
| ./files | Todos os arquivos nessa pasta são carregados e colocados no diretório de trabalho executor | Não | Pasta |
| ./archives | Todos os arquivos nessa pasta são descompactados | Não | Pasta |
| ./logs | pasta Olá onde os logs de cluster do Spark Olá são armazenados.| Não | Pasta |

Aqui está um exemplo de um armazenamento que contém dois arquivos de trabalho do Spark no hello armazenamento de BLOBs do Azure referenciada por Olá serviço vinculado do HDInsight.

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
