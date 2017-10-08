---
title: "aaaCreate pipelines de dados de previsão usando o Azure Data Factory | Microsoft Docs"
description: "Descreve como toocreate criar pipelines de previsão usando o Azure Data Factory e aprendizado de máquina do Azure"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a>Criar pipelines de previsão usando Azure Machine Learning e o Azure Data Factory

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

### <a name="azure-machine-learning"></a>Azure Machine Learning
[O aprendizado de máquina do Azure](https://azure.microsoft.com/documentation/services/machine-learning/) permite toobuild, testar e implantar soluções de análise de previsão. De um ponto de vista de alto nível, isso é feito em três etapas:

1. **Crie um teste de treinamento**. Siga esta etapa usando hello Azure ML Studio. o estúdio de ML Olá é um ambiente de colaboração de desenvolvimento visual que você use tootrain e testa um modelo de análise de previsão usando dados de treinamento.
2. **Convertê-lo a experiência de previsão tooa**. Depois que o modelo foi treinado com dados existentes e você está pronto toouse-tooscore novos dados, preparar e simplificar sua experiência de pontuação.
3. **Implantá-lo como um serviço da Web**. Você pode publicar seu experimento de pontuação como um serviço Web do Azure. Você pode enviar o modelo de dados de tooyour por este ponto de extremidade de serviço web e receber previsões de resultado para o modelo de saudação.  

### <a name="azure-data-factory"></a>Fábrica de dados do Azure
Fábrica de dados é um serviço de integração de dados com base em nuvem que orquestra e automatiza Olá **movimentação** e **transformação** de dados. Você pode criar soluções de integração de dados usando a fábrica de dados do Azure que podem incluir dados de várias fontes de dados, / processo de transformação dados saudação e publicar Olá resultado dados toohello dados repositórios.

Serviço de fábrica de dados permite que você toocreate pipelines de dados que moverem e transform dados e execute pipelines Olá em um agendamento especificado (por hora, diariamente, semanalmente, etc.). Ele também fornece a linhagem de saudação toodisplay visualizações avançadas e as dependências entre seus pipelines de dados e monitorar todos os seus pipelines de dados de um problema de identificar tooeasily exibição unificada exclusiva e configurar alertas de monitoramento.

Consulte [tooAzure Introdução fábrica de dados](data-factory-introduction.md) e [criar seu primeiro pipeline](data-factory-build-your-first-pipeline.md) artigos tooquickly começar com hello serviço do Azure Data Factory.

### <a name="data-factory-and-machine-learning-together"></a>Data Factory e Machine Learning juntos
Ativa a fábrica de dados do Azure tooeasily você criar pipelines que usam uma publicação [aprendizado de máquina do Azure] [ azure-machine-learning] web service para análise preditiva. Usando Olá **atividade de execução de lote** em um pipeline da fábrica de dados do Azure, você pode invocar um previsões de toomake Azure ML web service nos dados de saudação em lote. Consulte [invocar um ML do Azure usando o serviço web hello atividade de execução de lote](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) seção para obter detalhes.

Ao longo do tempo, os modelos de previsão de saudação em experiências de pontuação do hello Azure ML necessário toobe treinados novamente usando novos conjuntos de dados de entrada. Você pode treinar novamente um modelo ML do Azure de um pipeline da fábrica de dados fazendo Olá etapas a seguir:

1. Publica a experiência de treinamento de saudação (experiência não previsão) como um serviço web. Você executar esta etapa no hello Azure ML Studio como você fez experimento previsão tooexpose como um serviço web no cenário anterior hello.
2. Use serviço de web hello atividade de execução de lote do Azure ML tooinvoke Olá para teste de treinamento hello. Basicamente, você pode usar tooinvoke de atividade de execução de lote do ML do Azure Olá treinamento serviço web e o serviço web de pontuação.

Depois de terminar com treinamento, atualizar Olá pontuação serviço da web (previsão experimento exposto como um serviço da web) com hello recentemente treinado usando Olá **a atividade de recurso de atualização do Azure ML**. Veja o artigo [Atualização de modelos usando a Atividade do Recurso de Atualização](data-factory-azure-ml-update-resource-activity.md) para obter detalhes.

## <a name="invoking-a-web-service-using-batch-execution-activity"></a>Invocar um serviço Web usando a Atividade de Execução em Lote
Você usa o processamento e a movimentação de dados do Azure Data Factory tooorchestrate e, em seguida, executar execução em lotes usando o aprendizado de máquina do Azure. Aqui estão as etapas de nível superior de saudação:

1. Criar um serviço vinculado de Azure Machine Learning. Você precisa Olá valores a seguir:

   1. **URI de solicitação** para Olá API de execução do lote. Você pode encontrar hello URI da solicitação clicando Olá **BATCH EXECUTION** link na página de serviços web hello.
   2. **Chave de API** para Olá publicado o serviço web de aprendizado de máquina do Azure. Você pode encontrar a chave de API Olá clicando Olá web service que você publicou.
   3. Saudação de uso **AzureMLBatchExecution** atividade.

      ![Painel de Machine Learning](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![URI do lote](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a>Cenário: Experiências usando entradas/saídas de serviço de Web que se referem a toodata no armazenamento de BLOBs do Azure
Nesse cenário, hello serviço da Web de aprendizado de máquina do Azure faz previsões usando dados de um arquivo em um armazenamento de BLOBs do Azure e armazena os resultados da previsão Olá no armazenamento de blob de saudação. Olá JSON a seguir define um pipeline da fábrica de dados com uma atividade AzureMLBatchExecution. atividade de saudação tem Olá dataset **DecisionTreeInputBlob** como entrada e **DecisionTreeResultBlob** como saída de hello. Olá **DecisionTreeInputBlob** é passado como um serviço web de entrada toohello por usando Olá **webServiceInput** propriedade JSON. Olá **DecisionTreeResultBlob** é passado como um serviço de Web saída toohello por usando Olá **webserviceoutputs na** propriedade JSON.  

> [!IMPORTANT]
> Se o serviço web de saudação pega várias entradas, use Olá **webServiceInputs** propriedade em vez de usar **webServiceInput**. Consulte Olá [Web service exige várias entradas](#web-service-requires-multiple-inputs) seção para obter um exemplo de como usar Olá webServiceInputs propriedade.
>
> Conjuntos de dados que são referenciados por Olá **webServiceInput**/**webServiceInputs** e **webserviceoutputs na** propriedades (em  **typeProperties**) também deve ser incluído no hello atividade **entradas** e **gera**.
>
> Em seu experimento de Azure ML, as portas de entrada e saída do serviço Web e os parâmetros globais têm nomes padrão ("input1", "input2") os quais você pode personalizar. nomes de saudação usados para configurações de globalParameters, webServiceInputs e webserviceoutputs na devem corresponder exatamente aos nomes de saudação em experiências de saudação. Você pode exibir a carga de solicitação de exemplo hello na página de ajuda de execução de lote de saudação para o mapeamento do ML do Azure ponto de extremidade tooverify Olá esperado.
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> Somente entradas e saídas da atividade de AzureMLBatchExecution Olá podem ser passadas como parâmetros toohello serviço da Web. Por exemplo, Olá acima trecho JSON, DecisionTreeInputBlob é uma entrada toohello AzureMLBatchExecution atividade, que é passada como um serviço Web de entrada toohello por meio do parâmetro webServiceInput.   
>
>

### <a name="example"></a>Exemplo
Este toohold de armazenamento do Azure do exemplo usa ambos Olá dados de entrada e saídos.

É recomendável que você passe por Olá [criar seu primeiro pipeline com a fábrica de dados] [ adf-build-1st-pipeline] tutorial antes de executar este exemplo. Use Olá Editor da fábrica de dados toocreate Data Factory artefatos (serviços vinculados, conjuntos de dados, pipeline) neste exemplo.   

1. Criar um **serviço vinculado** para o **Armazenamento do Azure**. Se hello arquivos de entrada e saídos estiverem em diferentes contas de armazenamento, você precisa de dois serviços vinculados. Aqui está um exemplo JSON:

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. Criar hello **entrada** do Azure Data Factory **conjunto de dados**. Ao contrário de alguns outros conjuntos de dados do Data Factory, esses conjuntos de dados devem conter os valores **folderPath** e **fileName**. Você pode usar particionamento toocause tooprocess de execução (cada fatia de dados) cada lote ou produzir entrada exclusiva e arquivos de saída. Talvez seja necessário tooinclude alguns Olá tootransform de atividade de upstream de entrada em formato de arquivo CSV hello e colocá-lo na conta de armazenamento de saudação de cada fatia. Nesse caso, não inclua Olá **externo** e **externalData** configurações mostradas no hello seguir exemplo e sua DecisionTreeInputBlob seria Olá o conjunto de dados de saída de uma atividade diferente.

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
          "interval": 1
        },
        "policy": {
          "externalData": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
          }
        }
      }
    }
    ```

    O arquivo csv de entrada deve ter a linha de cabeçalho de coluna de saudação. Se você estiver usando Olá **atividade de cópia** toocreate/mover Olá csv, no armazenamento de blob hello, você deve definir a propriedade de coletor de saudação **blobWriterAddHeader** muito**true**. Por exemplo:

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    Se o arquivo csv de saudação não tem linha de cabeçalho hello, você poderá ver Olá erro a seguir: **erro na atividade: erro ao ler a cadeia de caracteres. Token inesperado: StartObject. Caminho '', linha 1, posição 1**.
3. Criar hello **saída** do Azure Data Factory **conjunto de dados**. Este exemplo usa o particionamento toocreate um caminho de saída exclusivo para cada execução da fatia. Sem particionamento hello, atividade de saudação substituiria o arquivo hello.

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. Criar um **serviço vinculado** do tipo: **AzureMLLinkedService**, fornecendo a chave de API de saudação e URL de execução de lote de modelo.

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. Por fim, crie um pipeline que contenha uma atividade **AzureMLBatchScoring** . Em tempo de execução, pipeline executa Olá etapas a seguir:

   1. Obtém o local de saudação do arquivo de entrada hello de seus conjuntos de dados de entrada.
   2. Invoca a execução de lote de aprendizado de máquina do Azure Olá API
   3. Cópias Olá lote execução saída toohello blob, dado no conjunto de dados de saída.

      > [!NOTE]
      > A atividade AzureMLBatchExecution pode ter zero ou mais entradas e uma ou mais saídas.
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      Ambos os valores de data/hora de **início** e de **término** devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por exemplo: 2014-10-14T16:32:41Z. Olá **final** tempo é opcional. Se você não especificar o valor para Olá **final** propriedade, ele é calculado como "**início + 48 horas.**" pipeline de saudação toorun indefinidamente, especifique **9999-09-09** como valor Olá Olá **final** propriedade. Consulte a [Referência de script JSON](https://msdn.microsoft.com/library/dn835050.aspx) para obter detalhes sobre as propriedades JSON.

      > [!NOTE]
      > A especificação de entrada para a atividade de AzureMLBatchExecution Olá é opcional.
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a>Cenário: Experiências usando módulos de leitor/gravador toorefer toodata em vários armazenamentos
Outro cenário comum ao criar experimentos do ML do Azure é toouse módulos de leitor e gravador. Olá leitor é usada tooload dados em uma experiência e módulo de gravador Olá toosave dados de suas experiências. Para obter detalhes sobre os módulos de leitor e gravador, consulte os tópicos [Leitor](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [Gravador](https://msdn.microsoft.com/library/azure/dn905984.aspx) na biblioteca MSDN.     

Ao usar módulos de leitor e gravador Olá, é uma boa prática toouse um parâmetro de serviço da Web para cada propriedade desses módulos de leitor/gravador. Esses parâmetros da web permitem que você os valores hello tooconfigure durante o tempo de execução. Por exemplo, você poderia criar um experimento com um módulo leitor que usa um banco de dados SQL do Azure: XXX.database.windows.net. Após a implantação do serviço web de saudação, você deseja tooenable consumidores de saudação de Olá web serviço toospecify outro servidor do SQL Azure chamado YYY.database.windows.net. Você pode usar um tooallow de parâmetro de serviço Web este toobe valor configurado.

> [!NOTE]
> A saída e entrada de serviço Web são diferentes dos parâmetros de serviço Web. Primeiro cenário de saudação, você viu como entrada e saída podem ser especificados para um serviço Web do ML do Azure. Nesse cenário, você deve passar parâmetros para um serviço Web que correspondem a tooproperties dos módulos de leitor/gravador.
>
>

Vejamos um cenário para o uso de parâmetros de serviço Web. Você tem um serviço implantado de web de aprendizado de máquina do Azure que usa um leitor módulo tooread de dados de uma das fontes de dados de saudação suportadas pelo aprendizado de máquina do Azure (por exemplo: banco de dados do SQL Azure). Após a execução do lote hello, resultados de saudação são gravados usando um módulo de gravador (banco de dados do SQL Azure).  Sem as entradas e saídas são definidas em experiências de saudação. Nesse caso, é recomendável que você configure os parâmetros de serviço web relevantes para os módulos de leitor e gravador de saudação. Essa configuração permite Olá leitor/gravador toobe módulos configurado ao usar Olá AzureMLBatchExecution atividade. Especificar parâmetros de serviço da Web em Olá **globalParameters** seção atividade Olá JSON da seguinte maneira.

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

Você também pode usar [funções da fábrica de dados](data-factory-functions-variables.md) passar valores para Olá parâmetros de serviço da Web conforme mostrado no exemplo a seguir de saudação:

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> parâmetros de serviço da Web Hello diferenciam maiusculas de minúsculas, portanto, verifique que Olá você especificar na atividade de saudação JSON correspondam Olá aqueles expostos pelo Olá serviço da Web.
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a>Usando um leitor módulo tooread de dados de vários arquivos no Blob do Azure
Pipelines de Big Data com atividades como Pig e Hive podem produzir um ou mais arquivos de saída sem extensão. Por exemplo, quando você especificar uma tabela de Hive externa, hello dados para a tabela de Hive externo Olá podem ser armazenados no armazenamento de BLOBs do Azure com hello 000000_0 de nome a seguir. Você pode usar o módulo de leitor de saudação em um experimento tooread vários arquivos e usá-los para previsões.

Ao usar o módulo do leitor de saudação em uma experiência de aprendizado de máquina do Azure, você pode especificar o Blob do Azure como uma entrada. arquivos de saudação em Olá armazenamento de BLOBs do Azure podem ser arquivos de saída de hello (exemplo: 000000_0) que são produzidos por um script de Pig e Hive em execução no HDInsight. Olá módulo reader permite tooread arquivos (com nenhuma extensão) Configurando Olá **toocontainer de caminho, o diretório/blob**. Olá **caminho toocontainer** pontos toohello contêiner e **directory/blob** pontos toofolder que contém arquivos de saudação conforme Olá a imagem a seguir. Olá, ou seja, o asterisco \*) **Especifica que todos os Olá arquivos Olá/pasta do contêiner (ou seja, aggregateddata/dados/ano = mês/2014-6 /\*)** são lidas como parte da experiência de saudação.

![Propriedades de Blob do Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a>Exemplo
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a>Pipeline com a atividade AzureMLBatchExecution com parâmetros de serviço Web

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

Em Olá acima exemplo JSON:

* Olá implantado aprendizado de máquina do Azure Web serviço usa um leitor e um gravador módulo tooread/gravação de dados de / tooan banco de dados do SQL Azure. Esse serviço da Web expõe Olá quatro parâmetros a seguir: nome do servidor, nome do banco de dados, nome de conta de usuário do servidor e senha de conta de usuário do servidor de banco de dados.  
* Ambos os valores de data/hora de **início** e de **término** devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por exemplo: 2014-10-14T16:32:41Z. Olá **final** tempo é opcional. Se você não especificar o valor para Olá **final** propriedade, ele é calculado como "**início + 48 horas.**" pipeline de saudação toorun indefinidamente, especifique **9999-09-09** como valor Olá Olá **final** propriedade. Consulte a [Referência de script JSON](https://msdn.microsoft.com/library/dn835050.aspx) para obter detalhes sobre as propriedades JSON.

### <a name="other-scenarios"></a>Outros cenários
#### <a name="web-service-requires-multiple-inputs"></a>Serviço Web exige várias entradas
Se o serviço web de saudação pega várias entradas, use Olá **webServiceInputs** propriedade em vez de usar **webServiceInput**. Conjuntos de dados que são referenciados por Olá **webServiceInputs** também deve ser incluído no hello atividade **entradas**.

Em seu experimento de Azure ML, as portas de entrada e saída do serviço Web e os parâmetros globais têm nomes padrão ("input1", "input2") os quais você pode personalizar. nomes de saudação usados para configurações de globalParameters, webServiceInputs e webserviceoutputs na devem corresponder exatamente aos nomes de saudação em experiências de saudação. Você pode exibir a carga de solicitação de exemplo hello na página de ajuda de execução de lote de saudação para o mapeamento do ML do Azure ponto de extremidade tooverify Olá esperado.

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a>O serviço Web não requer uma entrada
Serviços web do Azure ML lote execução pode ser usado toorun quaisquer fluxos de trabalho, por exemplo, R ou scripts de Python, que podem não exigir qualquer entrada. Ou então, experimento Olá pode ser configurado com um módulo do leitor que não expõem quaisquer GlobalParameters. Nesse caso, hello atividade AzureMLBatchExecution será configurada da seguinte maneira:

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a>O serviço Web não requer uma entrada/saída
Olá serviço web do ML do Azure batch execução pode não ter nenhuma saída do serviço Web configurada. Neste exemplo, não há nenhum serviço Web de entrada ou saída, nem GlobalParameters configurados. Ainda há uma saída configurada na atividade de saudação em si, mas ele não é fornecido como um webServiceOutput.

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a>Web Service usa leitores e gravadores e hello atividade é executada somente quando outras atividades tiveram êxito
Olá módulos do Azure ML web service leitor e gravador podem ser configurado toorun com ou sem qualquer GlobalParameters. No entanto, talvez você queira tooembed serviço chamadas em um pipeline que usa o serviço de saudação do conjunto de dados dependências tooinvoke apenas quando algum processamento upstream foi concluída. Você também pode disparar qualquer outra ação após a execução do lote hello usando essa abordagem. Nesse caso, você pode expressar dependências hello usando atividade entradas e saídas, sem nomear qualquer um deles como o serviço Web de entrada ou saída.

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

Olá **argumentos** são:

* Se o ponto de extremidade de teste usa um webServiceInput: ele é representado por um conjunto de dados de blob e está incluído em entradas de atividade hello e propriedade de webServiceInput hello. Caso contrário, a propriedade de webServiceInput Olá é omitida.
* Se o ponto de extremidade de teste usa webServiceOutput(s): eles são representados por conjuntos de dados de blob e são incluídos nas saídas da atividade de saudação e na propriedade de webserviceoutputs na saudação. atividade Hello gera e webserviceoutputs na são mapeados por nome de saudação de cada saída experimento hello. Caso contrário, a propriedade webserviceoutputs de saudação é omitida.
* Se o ponto de extremidade do experimento expõe globalParameter(s), eles recebem na propriedade do hello atividade globalParameters como pares de chave, valor. Caso contrário, a propriedade globalParameters de saudação é omitida. chaves de saudação diferenciam maiusculas de minúsculas. [As funções do Azure Data Factory](data-factory-functions-variables.md) pode ser usada em valores hello.
* Conjuntos de dados adicionais podem ser incluídos em Olá entradas e saídas de propriedades de atividade, sem que está sendo referenciado no hello atividade typeProperties. Esses conjuntos de dados determinam a execução com dependências de fatia mas caso contrário, são ignorados pelo hello atividade AzureMLBatchExecution.


## <a name="updating-models-using-update-resource-activity"></a>Atualização dos modelos usando a Atividade de Recurso de Atualização
Depois de terminar com treinamento, atualizar Olá pontuação serviço da web (previsão experimento exposto como um serviço da web) com hello recentemente treinado usando Olá **a atividade de recurso de atualização do Azure ML**. Veja o artigo [Atualização de modelos usando a Atividade do Recurso de Atualização](data-factory-azure-ml-update-resource-activity.md) para obter detalhes.

### <a name="reader-and-writer-modules"></a>Módulos de leitor e gravador
Um cenário comum para uso de parâmetros de serviço da Web é o uso de saudação do Azure SQL leitores e gravadores. módulo do leitor de saudação é usado tooload dados em uma experiência de gerenciamento de serviços de dados fora do estúdio de aprendizado de máquina do Azure. módulo de gravador Olá é toosave dados de suas experiências em serviços de gerenciamento de dados fora do estúdio de aprendizado de máquina do Azure.  

Para obter detalhes sobre leitor/gravador do SQL do Azure/Blob do Azure, consulte os tópicos [Leitor](https://msdn.microsoft.com/library/azure/dn905997.aspx) e [Gravador](https://msdn.microsoft.com/library/azure/dn905984.aspx) na biblioteca MSDN. exemplo Hello na seção anterior Olá usado leitor de BLOBs do Azure hello e gravador de BLOBs do Azure. Esta seção discute usando o leitor do SQL do Azure e o gravador do SQL do Azure.

## <a name="frequently-asked-questions"></a>Perguntas frequentes
**P:** Tenho vários arquivos que são gerados pelos meus pipelines de Big Data. Pode usar o hello atividade AzureMLBatchExecution toowork em todos os arquivos de Olá?

**R:** Sim. Consulte Olá **usando um leitor módulo tooread de dados de vários arquivos no Blob do Azure** seção para obter detalhes.

## <a name="azure-ml-batch-scoring-activity"></a>Atividade de pontuação do lote do ML do Azure
Se você estiver usando Olá **AzureMLBatchScoring** toointegrate de atividade com o aprendizado de máquina do Azure, recomendamos que você use hello mais recente **AzureMLBatchExecution** atividade.

Hello atividade AzureMLBatchExecution é introduzido no hello versão de agosto de 2015 do SDK do Azure e o Azure PowerShell.

Se você quiser toocontinue usando Olá AzureMLBatchScoring atividade, continue a ler esta seção.  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a>Atividade de pontuação em lote do ML do Azure usando o armazenamento do Azure para entrada/saída

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a>Parâmetros de serviço Web
toospecify valores para parâmetros de serviço da Web, adicione um **typeProperties** seção toohello **AzureMLBatchScoringActivty** seção no pipeline de saudação JSON, conforme mostrado no exemplo a seguir de saudação:

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
Você também pode usar [funções da fábrica de dados](data-factory-functions-variables.md) passar valores para Olá parâmetros de serviço da Web conforme mostrado no exemplo a seguir de saudação:

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> parâmetros de serviço da Web Hello diferenciam maiusculas de minúsculas, portanto, verifique que Olá você especificar na atividade de saudação JSON correspondam Olá aqueles expostos pelo Olá serviço da Web.
>
>

## <a name="see-also"></a>Consulte também
* 
            [Postagem do blog do Azure: Introdução ao Azure Data Factory e Azure Machine Learning](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
