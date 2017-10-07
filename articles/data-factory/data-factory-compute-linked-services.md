---
title: ambientes de aaaCompute com suporte do Azure Data Factory | Microsoft Docs
description: "Saiba mais sobre ambientes de computação que você pode usar no Azure Data Factory pipelines (como o Azure HDInsight) tootransform ou processam dados."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6877a7e8-1a58-4cfb-bbd3-252ac72e4145
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 07/25/2017
ms.author: shlo
ms.openlocfilehash: aba7d7de695bc1c7d475f1e741ee3b3e884151c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="compute-environments-supported-by-azure-data-factory"></a>Ambientes de computação com suporte do Azure Data Factory
Este artigo explica os ambientes de computação diferentes que você pode usar tooprocess ou transformar dados. Ele também fornece detalhes sobre as diferentes configurações (sob demanda versus traga a sua própria) tem suportados pela fábrica de dados ao configurar serviços vinculados vincular essas computação ambientes tooan data factory do Azure.

Olá tabela a seguir fornece uma lista de ambientes de computação tem suportada pela fábrica de dados e hello atividades que podem ser executados neles. 

| Ambiente de computação | atividades |
| --- | --- |
| [Cluster HDInsight sob demanda](#azure-hdinsight-on-demand-linked-service) ou [seu próprio cluster HDInsight](#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop Streaming](data-factory-hadoop-streaming-activity.md) |
| [Lote do Azure](#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| 
            [Azure Machine Learning](#azure-machine-learning-linked-service) |[Atividades de Machine Learning: execução do Lote e recurso de atualização](data-factory-azure-ml-batch-execution-activity.md) |
| [Análise Azure Data Lake](#azure-data-lake-analytics-linked-service) |[U-SQL da Análise Data Lake](data-factory-usql-activity.md) |
| [Azure SQL](#azure-sql-linked-service), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-linked-service), [SQL Server](#sql-server-linked-service) |[Procedimento armazenado](data-factory-stored-proc-activity.md) |

## <a name="supported-hdinsight-versions-in-azure-data-factory"></a>Versões com suporte do HDInsight no Azure Data Factory
O HDInsight do Azure dá suporte a várias versões do cluster Hadoop que podem ser implantadas a qualquer momento. Cada opção de versão cria uma versão específica de distribuição do hello plataforma HDP (Hortonworks Data) e um conjunto de componentes que estão contidos a essa distribuição. Microsoft mantém atualizando a lista de saudação de versões com suporte dos componentes mais recentes Hadoop ecossistema do HDInsight tooprovide e correções. Olá 3.2 do HDInsight foi preterido no dia 1 de abril de 2017. Para saber mais, confira [Versões do HDInsight com suporte](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).

Isso afeta os Azure Data Factories existentes que têm atividades em execução em clusters HDInsight 3.2. É recomendável Olá tooupdate seção a seguir da diretrizes usuários toofollow Olá Olá fábricas de dados afetados:

### <a name="for-linked-services-pointing-tooyour-own-hdinsight-clusters"></a>Para serviços vinculados apontando tooyour próprios clusters de HDInsight
* **Serviços vinculados do HDInsight apontando tooyour possui HDInsight 3.2 ou abaixo de clusters:**

  A fábrica de dados do Azure dá suporte ao envio tooyour trabalhos HDInsight próprio clusters do HDI 3.1 muito[Olá suportada mais recente versão do HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). No entanto, você não pode mais criar cluster do HDInsight 3.2 após 1 de abril de 2017 com base na política de substituição de saudação documentada em [HDInsight versões com suporte](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).  

  **Recomendações:** 
  * Executar testes tooensure Olá compatibilidade de saudação atividades que fazem referência a esse serviço vinculado muito[Olá suportada mais recente versão do HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) com informações documentadas no [Hadoop componentes disponíveis com versões diferentes do HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) e [Hortonworks notas associados a versões de HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Atualizar seu cluster HDInsight 3.2 muito[Olá suportada mais recente versão do HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget Olá componentes do ecossistema de Hadoop e correções mais recentes. 

* **Serviços vinculados do HDInsight apontando tooyour proprietário HDInsight 3.3 ou acima de clusters:**

  A fábrica de dados do Azure dá suporte ao envio tooyour trabalhos HDInsight próprio clusters do HDI 3.1 muito[Olá suportada mais recente versão do HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions). 
  
  **Recomendações:** 
  * Nenhuma ação é necessária da perspectiva do Data Factory. No entanto, se você estiver usando uma versão anterior do HDInsight, ainda é recomendável atualizar muito[Olá suportada mais recente versão do HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget Olá componentes do ecossistema de Hadoop e correções mais recentes.

### <a name="for-hdinsight-on-demand-linked-services"></a>Para serviços vinculados do HDInsight sob demanda
* **A versão 3.2 ou inferior é especificada na definição de JSON de serviços vinculados do HDInsight sob demanda:**
  
  O Azure Data Factory dará suporte à criação de clusters HDInsight sob demanda de versão 3.3 ou mais a partir de **15/05/2017**. E, fim de saudação do suporte de existente 3.2 do HDInsight sob demanda serviços vinculados é estendido muito**15/07/2017**.  

  **Recomendações:** 
  * Executar testes tooensure Olá compatibilidade de saudação atividades que fazem referência a esse serviço vinculado muito [Olá suportada mais recente versão do HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) com informações documentadas no [Hadoop componentes disponíveis com versões diferentes do HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) e [Hortonworks notas associados a versões de HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).
  * Antes de **15/07/2017**, atualize a propriedade de versão de saudação na definição de JSON de serviço vinculado sob demanda HDI muito[Olá suportada mais recente versão do HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) componentes mais recentes Hadoop ecossistema do tooget hello e correções. Para a definição de JSON detalhada, consulte toohello [exemplo de serviço vinculado do Azure HDInsight sob demanda](#azure-hdinsight-on-demand-linked-service). 

* **Versão não especificada em serviços vinculados do HDInsight sob demanda:**
  
  O Azure Data Factory dará suporte à criação de clusters HDInsight sob demanda de versão 3.3 ou mais a partir de **15/05/2017**. E, término hello tooexisting sob demanda 3.2 do HDInsight vinculados de serviços de suporte é estendido muito**15/07/2017**. 

  Antes de **15/07/2017**, se deixado em branco, o padrão de saudação valores de versão e osType propriedades são: 

  | Propriedade | Valor Padrão | Obrigatório |
  | --- | --- | --- |
  Versão   | HDI 3.1 para o cluster do Windows e HDI 3.2 para o cluster do Linux.| Não
  osType | saudação padrão é Windows | Não

  Depois de **15/07/2017**, se deixado em branco, o padrão de saudação valores de versão e osType propriedades são:

  | Propriedade | Valor Padrão | Obrigatório |
  | --- | --- | --- |
  Versão   | HDI 3.3 para o cluster do Windows e HDI 3.5 para o cluster do Linux.    | Não
  osType | padrão de saudação é Linux   | Não

  **Recomendações:** 
  * Antes de **15/07/2017**, executar testes tooensure Olá compatibilidade de saudação atividades que fazem referência a esse serviço vinculado muito[Olá suportada mais recente versão do HDInsight](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) com informações documentadas em [Hadoop componentes disponíveis com versões diferentes do HDInsight](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) e [Hortonworks notas associados a versões de HDInsight](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).  
  * Depois de **15/07/2017**, certifique-se de especificar explicitamente valores osType e versão se você deseja que as configurações padrão de saudação toooverride. 

>[!Note]
>Atualmente, o Azure Data Factory não dá suporte a clusters HDInsight usando o Azure Data Lake Store como repositório primário. Use o Armazenamento do Azure como repositório primário para clusters HDInsight. 
>  
>  

## <a name="on-demand-compute-environment"></a>Ambiente de computação sob demanda
Esse tipo de configuração, o ambiente de computação Olá totalmente é gerenciado pelo serviço do Azure Data Factory Olá. É automaticamente criado pelo Olá serviço da fábrica de dados antes de um trabalho é enviado tooprocess dados e removida quando o trabalho de saudação estiver concluído. Você pode criar um serviço vinculado para o ambiente de computação sob demanda hello, configurá-lo e controlar configurações granulares para execução do trabalho, gerenciamento de cluster e ações de inicialização.

> [!NOTE]
> configuração do Hello sob demanda é suportada atualmente apenas para clusters de HDInsight do Azure.
> 
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a>Serviço vinculado do Azure HDInsight sob demanda
Olá serviço fábrica de dados do Azure pode criar automaticamente um dados sob demanda baseados no Windows/Linux de tooprocess de cluster HDInsight. Olá cluster é criado no hello mesma região da conta de armazenamento da saudação (propriedade linkedServiceName em JSON de saudação) associado com cluster hello. conta de armazenamento Olá deve ser uma conta de armazenamento do Azure padrão de uso geral. 

Observe o seguinte Olá **importante** serviço vinculado de pontos sobre o HDInsight sob demanda:

* Você não vir Olá sob demanda cluster HDInsight criado na sua assinatura do Azure. saudação de serviço do Azure Data Factory gerencia o cluster do HDInsight sob demanda Olá em seu nome.
* Olá logs para trabalhos que são executados em um HDInsight sob demanda cluster são copiados toohello conta de armazenamento associada Olá cluster do HDInsight. Você pode acessar esses logs de saudação portal do Azure no hello **detalhes de execução da atividade** folha. Consulte o artigo [Monitorar e gerenciar pipelines](data-factory-monitor-manage-pipelines.md) para obter detalhes.
* Você é cobrado somente para o tempo de saudação quando o cluster do HDInsight hello está ativo e trabalhos em execução.

> [!IMPORTANT]
> Normalmente demora **20 minutos** ou cluster tooprovision mais um Azure HDInsight sob demanda.
> 
> 

### <a name="example"></a>Exemplo
Olá JSON a seguir define um serviço vinculado do HDInsight de sob demanda com base em Linux. Olá serviço da fábrica de dados cria automaticamente um **baseados em Linux** cluster HDInsight durante o processamento de uma fatia de dados. 

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
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

toouse um cluster HDInsight baseados no Windows, defina **osType** muito**windows** ou não use a propriedade hello como o valor padrão de saudação é: windows.  

> [!IMPORTANT]
> Olá HDInsight cluster cria um **contêiner padrão** no armazenamento de blob Olá especificado no hello JSON (**linkedServiceName**). HDInsight não exclui esse contêiner quando Olá cluster é excluído. Este comportamento ocorre por design. Com o serviço de vinculado do HDInsight sob demanda, um cluster HDInsight é criado sempre que precisa de uma fatia toobe processado a menos que haja um cluster existente de ao vivo (**timeToLive**) e é excluído quando Olá processamento é concluído. 
> 
> Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure. Se não precisar para solução de problemas de trabalhos de saudação, talvez você queira toodelete-os custos de armazenamento do tooreduce hello. nomes de saudação desses contêineres seguem um padrão: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`. Use ferramentas como [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com/) armazenamento de blobs de contêineres toodelete do Azure.
> 
> 

### <a name="properties"></a>Propriedades
| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade do tipo Hello deve ser definida muito**HDInsightOnDemand**. |Sim |
| clusterSize |Número de nós de dados do trabalhador em cluster hello. cluster do HDInsight Olá é criado com 2 nós de cabeçalho junto com o número de saudação de nós de trabalho que você especifica para esta propriedade. nós Olá são de tamanho Standard_D3 que tem 4 núcleos, assim, um cluster de nó do 4 operador leva 24 núcleos (4\*4 = 16 núcleos para nós de trabalho, mais 2\*4 = 8 núcleos para nós de cabeçalho). Consulte [Hadoop baseado em Linux criar clusters de HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) para obter detalhes sobre a camada de saudação Standard_D3. |Sim |
| timeToLive |Olá permitido tempo ocioso do cluster do HDInsight sob demanda hello. Especifica quanto tempo cluster do HDInsight sob demanda Olá permanece ativo após a conclusão de uma atividade executar se não houver nenhum outro trabalho ativo no cluster hello.<br/><br/>Por exemplo, se uma atividade executar levar 6 minutos e timetolive é definir too5 minutos, Olá cluster permanece ativo por 5 minutos após a saudação 6 minutos de processamento de execução da atividade hello. Se outra execução da atividade é executada com uma janela de 6 minutos hello, ela é processada pelo Olá mesmo cluster.<br/><br/>A criação de um cluster do HDInsight sob demanda é uma operação cara (pode demorar um pouco), então use essa configuração como desempenho tooimprove necessários de uma fábrica de dados com a reutilização de um cluster do HDInsight sob demanda.<br/><br/>Se você definir timetolive valor too0, cluster Olá é excluído assim que a conclusão da execução da atividade hello. Por outro lado, se você definir um valor alto, cluster Olá pode permanecer ocioso desnecessariamente, resultando em altos custos. Portanto, é importante que você defina o valor apropriado de saudação com base em suas necessidades.<br/><br/>Se o valor da propriedade timetolive Olá adequadamente for definido, pipelines vários podem compartilhar a instância de saudação do cluster do HDInsight sob demanda hello.  |Sim |
| version |Versão do cluster do HDInsight hello. valor padrão de saudação é 3.1 para o cluster do Windows e 3.2 para o cluster do Linux. |Não |
| linkedServiceName | Armazenamento do Azure vinculada toobe de serviço usado pelo cluster sob demanda de saudação para armazenar e processar dados. Hello cluster HDInsight é criado no hello mesma região que a conta de armazenamento do Azure.<p>No momento, você não pode criar um cluster HDInsight sob demanda que usa um repositório Azure Data Lake como armazenamento hello. Se desejar que os dados de resultado de saudação toostore do HDInsight de processamento em um repositório Azure Data Lake, use um atividade de cópia toocopy Olá os dados de armazenamento de BLOBs do Azure de saudação toohello repositório Azure Data Lake. </p>  | Sim |
| additionalLinkedServiceNames |Especifica o serviço vinculado de contas de armazenamento adicionais para Olá HDInsight para que o serviço do Data Factory Olá pode registrá-los em seu nome. Essas contas de armazenamento devem estar no hello mesma região Olá o cluster HDInsight, que é criado no hello mesmo região da conta de armazenamento Olá especificada pelo linkedServiceName. |Não |
| osType |Tipo do sistema operacional. Valores permitidos são: Windows (padrão) e Linux |Não |
| hcatalogLinkedServiceName |nome de saudação do vinculado do SQL Azure ponto toohello HCatalog banco de dados do serviço. cluster do HDInsight sob demanda Olá é criado usando o banco de dados do SQL Azure hello como Olá metastore. |Não |

#### <a name="additionallinkedservicenames-json-example"></a>Exemplo de JSON additionalLinkedServiceNames

```json
"additionalLinkedServiceNames": [
    "otherLinkedServiceName1",
    "otherLinkedServiceName2"
  ]
```

### <a name="advanced-properties"></a>Propriedades avançadas
Você também pode especificar Olá seguintes propriedades para configuração granular de saudação do cluster de HDInsight sob demanda hello.

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| coreConfiguration |Especifica os parâmetros de configuração de núcleo de hello (como Core-site.xml) para toobe de cluster do HDInsight Olá criado. |Não |
| hBaseConfiguration |Especifica os parâmetros de configuração Olá HBase (hbase-site.xml) para o cluster do HDInsight hello. |Não |
| hdfsConfiguration |Especifica os parâmetros de configuração Olá HDFS (HDFS-site.xml) para o cluster do HDInsight hello. |Não |
| hiveConfiguration |Especifica os parâmetros de configuração Olá hive (hive-site.xml) para o cluster do HDInsight hello. |Não |
| mapReduceConfiguration |Especifica os parâmetros de configuração Olá MapReduce (mapred-site.xml) para o cluster do HDInsight hello. |Não |
| oozieConfiguration |Especifica os parâmetros de configuração Olá Oozie (oozie-site.xml) para o cluster do HDInsight hello. |Não |
| stormConfiguration |Especifica os parâmetros de configuração Olá Storm (Storm-site.xml) para o cluster do HDInsight Olá. |Não |
| yarnConfiguration |Especifica os parâmetros de configuração Olá Yarn (yarn-site.xml) para o cluster do HDInsight hello. |Não |

#### <a name="example--on-demand-hdinsight-cluster-configuration-with-advanced-properties"></a>Exemplo – configuração de cluster HDInsight sob demanda com propriedades avançadas

```json
{
  "name": " HDInsightOnDemandLinkedService",
  "properties": {
    "type": "HDInsightOnDemand",
    "typeProperties": {
      "clusterSize": 16,
      "timeToLive": "01:30:00",
      "linkedServiceName": "adfods1",
      "coreConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "hiveConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "mapReduceConfiguration": {
        "mapreduce.reduce.java.opts": "-Xmx4000m",
        "mapreduce.map.java.opts": "-Xmx4000m",
        "mapreduce.map.memory.mb": "5000",
        "mapreduce.reduce.memory.mb": "5000",
        "mapreduce.job.reduce.slowstart.completedmaps": "0.8"
      },
      "yarnConfiguration": {
        "yarn.app.mapreduce.am.resource.mb": "5000",
        "mapreduce.map.memory.mb": "5000"
      },
      "additionalLinkedServiceNames": [
        "datafeeds",
        "adobedatafeed"
      ]
    }
  }
}
```

### <a name="node-sizes"></a>Tamanhos dos nós
Você pode especificar tamanhos de saudação de nós de cabeçalho, dados e zookeeper usando Olá propriedades a seguir: 

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| headNodeSize |Especifica o tamanho de saudação do nó principal hello. valor padrão de saudação é: Standard_D3. Consulte Olá **especificando os tamanhos de nós** seção para obter detalhes. |Não |
| dataNodeSize |Especifica o tamanho de saudação do nó de dados de saudação. valor padrão de saudação é: Standard_D3. |Não |
| zookeeperNodeSize |Especifica o tamanho de saudação do nó de guardião Zoo hello. valor padrão de saudação é: Standard_D3. |Não |

#### <a name="specifying-node-sizes"></a>Especificar tamanhos de nós
Consulte Olá [tamanhos de máquinas virtuais](../virtual-machines/linux/sizes.md) artigo para valores de cadeia de caracteres necessários toospecify para propriedades de saudação mencionadas na seção anterior hello. os valores Hello necessário tooconform toohello **CMDLETs & APIS** mencionado no artigo hello. Como você pode ver no artigo Olá, o nó de dados de saudação do tamanho grande (padrão) tem memória de 7 GB, que pode não ser bom o bastante para seu cenário. 

Se você quiser toocreate D4 dimensionado nós principal e trabalho, especifique **Standard_D4** como valor Olá para propriedades headNodeSize e dataNodeSize. 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

Se você especificar um valor incorreto para essas propriedades, você pode receber a seguinte Olá **erro:** falha toocreate cluster. Exceção: Cluster de saudação toocomplete não é possível criar a operação. Falha na operação com o código '400'. Cluster deixou para trás estado: ‘Erro’. Mensagem: “PreClusterCreationValidationFailure”. Quando você receber esse erro, certifique-se de que você está usando Olá **CMDLET & APIS** nome da tabela Olá Olá [tamanhos de máquinas virtuais](../virtual-machines/linux/sizes.md) artigo.  

## <a name="bring-your-own-compute-environment"></a>Traga seu próprio ambiente de computação
Nesse tipo de configuração, os usuários podem registrar um ambiente de computação já existente como um serviço vinculado no Data Factory. ambiente de computação de saudação é gerenciado por usuário hello e Olá serviço da fábrica de dados usa as atividades de saudação tooexecute.

Esse tipo de configuração tem suporte para ambientes de computação do seguinte hello:

* Azure HDInsight
* Lote do Azure
* Machine Learning do Azure
* Análise Azure Data Lake
* Banco de Dados SQL do Azure, SQL DW do Azure, SQL Server

## <a name="azure-hdinsight-linked-service"></a>Serviço vinculado do Azure HDInsight
Você pode criar um tooregister de serviço vinculado do Azure HDInsight seu próprio cluster HDInsight com a fábrica de dados.

### <a name="example"></a>Exemplo

```json
{
  "name": "HDInsightLinkedService",
  "properties": {
    "type": "HDInsight",
    "typeProperties": {
      "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
      "userName": "admin",
      "password": "<password>",
      "linkedServiceName": "MyHDInsightStoragelinkedService"
    }
  }
}
```

### <a name="properties"></a>Propriedades
| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade do tipo Hello deve ser definida muito**HDInsight**. |Sim |
| clusterUri |Olá URI do cluster do HDInsight hello. |Sim |
| Nome de Usuário |Especifique o nome Olá Olá usuário toobe usado cluster do HDInsight tooconnect tooan existente. |Sim |
| Senha |Especifique a senha da conta de usuário de saudação. |Sim |
| linkedServiceName | Nome do serviço vinculado do armazenamento do Azure que se refere o armazenamento de BLOBs do Azure toohello de saudação usado por Olá cluster HDInsight. <p>No momento, você não pode especificar um serviço vinculado do Azure Data Lake Store para essa propriedade. Se o cluster do HDInsight Olá tem acesso toohello repositório Data Lake, você pode acessar dados em Olá repositório Azure Data Lake de scripts de Pig/Hive. </p>  |Sim |

## <a name="azure-batch-linked-service"></a>Serviço vinculado de Lote do Azure
Você pode criar um pool de lote máquinas virtuais (VMs) tooa da fábrica de dados para um tooregister de serviço vinculado do Azure Batch. Você pode executar atividades personalizadas do .NET usando o Lote do Azure ou o Azure HDInsight.

Consulte o tópicos a seguir se você for novo serviço de lote tooAzure:

* [Noções básicas de lote do Azure](../batch/batch-technical-overview.md) para obter uma visão geral de saudação do serviço Azure Batch.
* [Novo AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) toocreate cmdlet uma conta de lote do Azure (ou) [portal do Azure](../batch/batch-account-create-portal.md) conta de lote do Azure Olá toocreate usando o portal do Azure. Consulte [toomanage usando o PowerShell conta de lote do Azure](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) tópico para obter instruções detalhadas sobre como usar o cmdlet hello.
* [Novo AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) cmdlet toocreate um pool de lote do Azure.

### <a name="example"></a>Exemplo

```json
{
  "name": "AzureBatchLinkedService",
  "properties": {
    "type": "AzureBatch",
    "typeProperties": {
      "accountName": "<Azure Batch account name>",
      "accessKey": "<Azure Batch account key>",
      "poolName": "<Azure Batch pool name>",
      "linkedServiceName": "<Specify associated storage linked service reference here>"
    }
  }
}
```

Acrescente "**.\< nome da região\>**"nome de toohello da sua conta de lote para Olá **accountName** propriedade. Exemplo:

```json
"accountName": "mybatchaccount.eastus"
```

Outra opção é o ponto de extremidade do tooprovide Olá batchUri conforme mostrado na saudação de exemplo a seguir:

```json
"accountName": "adfteam",
"batchUri": "https://eastus.batch.azure.com",
```

### <a name="properties"></a>Propriedades
| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade do tipo Hello deve ser definida muito**AzureBatch**. |Sim |
| accountName |Nome da saudação conta de lote do Azure. |Sim |
| accessKey |Chave de acesso para Olá conta de lote do Azure. |Sim |
| poolName |Nome do pool de saudação de máquinas virtuais. |Sim |
| linkedServiceName |Nome do serviço vinculado do armazenamento do Azure associada ao serviço vinculado do Azure Batch de saudação. Esse serviço vinculado é usado para arquivos de teste toorun atividade de saudação e armazenar os logs de execução de atividade Olá necessários. |Sim |

## <a name="azure-machine-learning-linked-service"></a>Serviço Vinculado de Machine Learning do Azure
Você cria um tooregister de serviço vinculado do aprendizado de máquina do Azure um fábrica de dados do ponto de extremidade tooa de pontuação do lote de aprendizado de máquina.

### <a name="example"></a>Exemplo

```json
{
  "name": "AzureMLLinkedService",
  "properties": {
    "type": "AzureML",
    "typeProperties": {
      "mlEndpoint": "https://[batch scoring endpoint]/jobs",
      "apiKey": "<apikey>"
    }
  }
}
```

### <a name="properties"></a>Propriedades
| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| Tipo |propriedade de tipo Hello deve ser definida como: **AzureML**. |Sim |
| mlEndpoint |URL de pontuação de lote de saudação. |Sim |
| apiKey |Olá publicados API do modelo de espaço de trabalho. |Sim |

## <a name="azure-data-lake-analytics-linked-service"></a>Serviço Vinculado da Análise Azure Data Lake
Você cria um **análise Azure Data Lake** vinculado serviço toolink uma análise do Azure Data Lake computação serviço tooan data factory do Azure. Hello atividade U-SQL do Data Lake análise no pipeline de saudação refere-se serviço toothis vinculado. 

Olá tabela a seguir fornece descrições para Olá genéricas propriedades usadas em Olá definição JSON. Você ainda pode escolher entre a autenticação de credencial do usuário e entidade de serviço.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| **tipo** |propriedade de tipo Hello deve ser definida como: **AzureDataLakeAnalytics**. |Sim |
| **accountName** |Nome da conta da Análise Azure Data Lake. |Sim |
| **dataLakeAnalyticsUri** |URI da Análise Azure Data Lake. |Não |
| **subscriptionId** |Id de assinatura do Azure |Não (se não especificado, a assinatura de saudação fábrica de dados é usada). |
| **resourceGroupName** |Nome do grupo de recursos do Azure |Não (se não especificado, o grupo de recursos de saudação fábrica de dados é usada). |

### <a name="service-principal-authentication-recommended"></a>Autenticação de entidade de serviço (recomendada)
autenticação principal do serviço toouse, registre uma entidade de aplicativo no Azure Active Directory (AD do Azure) e conceda ele Olá acessar tooData Lake repositório. Para encontrar as etapas detalhadas, consulte [Autenticação de serviço a serviço](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Anote Olá valores, que você usar a seguir toodefine Olá vinculado de serviço:
* ID do aplicativo
* Chave do aplicativo 
* ID do locatário

Use autenticação principal do serviço especificando Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| **servicePrincipalId** | Especifique a ID do cliente. do aplicativo hello | Sim |
| **servicePrincipalKey** | Especifique a chave de aplicativo hello. | Sim |
| **tenant** | Especifique as informações de locatário hello (ID de locatário ou de nome de domínio) em que o aplicativo reside. Você pode recuperá-la por focalização mouse Olá no canto superior direito Olá Olá portal do Azure. | Sim |

**Exemplo: autenticação de entidade de serviço**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Autenticação de credenciais de usuário
Como alternativa, você pode usar a autenticação de credenciais de usuário para análise Data Lake especificando Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| **authorization** | Clique em Olá **autorizar** botão no hello Editor da fábrica de dados e insira suas credenciais que atribui a propriedade toothis de URL de autorização do hello gerado automaticamente. | Sim |
| **sessionId** | ID de sessão do OAuth da sessão de autorização de OAuth hello. Cada ID da sessão é exclusiva e pode ser usada somente uma vez. Essa configuração é gerada automaticamente quando você usa Olá Editor da fábrica de dados. | Sim |

**Exemplo: autenticação de credenciais do usuário**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Expiração do token
Olá código de autorização gerado usando Olá **autorizar** botão expira após algum tempo. Consulte a tabela a seguir para tempos de expiração de saudação para diferentes tipos de contas de usuário de saudação. Você pode ver Olá a seguinte mensagem de erro hello quando a autenticação **token expira**: erro na operação de credencial: invalid_grant - AADSTS70002: erro ao validar credenciais. AADSTS70008: Olá fornecido a concessão de acesso expirou ou foi revogado. ID do Rastreamento: d18629e8-af88-43c5-88e3-d8419eb1fca1 ID da Correlação: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Carimbo de data/hora: 2015-12-15 21:09:31Z

| Tipo de usuário | Expira após |
|:--- |:--- |
| Contas de usuário NÃO gerenciadas pelo Azure Active Directory (@hotmail.com, @live.com etc.) |12 horas |
| Contas de usuários gerenciadas pelo AAD (Azure Active Directory) |Execute a 14 dias após a última fatia de saudação. <br/><br/>90 dias, se uma fatia com base em serviços vinculados do OAuth for executada pelo menos uma vez a cada 14 dias. |

tooavoid e resolver esse erro, autorize novamente usando Olá **autorizar** botão quando hello **token expira** e reimplante o serviço vinculado de saudação. Você também pode gerar valores para as propriedades **sessionId** e **authorization** de modo programático usando o código da seguinte maneira:

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

Consulte [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), e [AuthorizationSessionGetResponse classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) tópicos para obter detalhes sobre classes de fábrica de dados Olá usadas no código de saudação. Adicione uma referência a: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll para Olá WindowsFormsWebAuthenticationDialog classe. 

## <a name="azure-sql-linked-service"></a>Serviço Vinculado do SQL do Azure
Criar um serviço vinculado do SQL Azure e usá-lo com hello [atividade de procedimento armazenado](data-factory-stored-proc-activity.md) tooinvoke um procedimento armazenado de um pipeline da fábrica de dados. Confira o artigo [Conector SQL do Azure](data-factory-azure-sql-connector.md#linked-service-properties) para saber mais sobre esse serviço vinculado.

## <a name="azure-sql-data-warehouse-linked-service"></a>Serviço vinculado do SQL Data Warehouse do Azure
Criar um serviço vinculado do Azure SQL Data Warehouse e usá-lo com hello [atividade de procedimento armazenado](data-factory-stored-proc-activity.md) tooinvoke um procedimento armazenado de um pipeline da fábrica de dados. Confira o artigo [Conector SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) para saber mais sobre esse serviço vinculado.

## <a name="sql-server-linked-service"></a>Serviço vinculado do SQL Server
Criar um serviço vinculado do SQL Server e usá-lo com hello [atividade de procedimento armazenado](data-factory-stored-proc-activity.md) tooinvoke um procedimento armazenado de um pipeline da fábrica de dados. Confira o artigo [Conector SQL Server](data-factory-sqlserver-connector.md#linked-service-properties) para saber mais sobre esse serviço vinculado.

