---
title: aaaAzure Data Factory - perguntas frequentes
description: Perguntas frequentes sobre o Azure Data Factory.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 532dec5a-7261-4770-8f54-bfe527918058
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 78289fb4b6e15d74772af6c71ec25c7d2ca1a0bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---frequently-asked-questions"></a>Azure Data Factory - Perguntas frequentes
## <a name="general-questions"></a>Perguntas gerais
### <a name="what-is-azure-data-factory"></a>O que é o Data Factory do Azure?
Fábrica de dados é uma nuvem com base em integração de dados de serviço que **automatiza a movimentação de saudação e a transformação de dados**. Assim como uma fábrica que executa o equipamento tootake matérias-primas e transformá-las em mercadorias concluídas, a fábrica de dados orquestra serviços existentes que coletam dados brutos e transformação-los em informações pronta para uso.

Fábrica de dados permite que dados de toomove toocreate fluxos de trabalho orientados a dados entre os locais e repositórios de dados de nuvem, bem como processo/transformar dados usando os serviços de computação como HDInsight do Azure e análise do Azure Data Lake. Depois de criar um pipeline que executa a ação de saudação que você precisa, você pode agendar toorun periodicamente (por hora, diariamente, semanalmente, etc.).   

Para obter mais informações, consulte [Visão geral e principais conceitos](data-factory-introduction.md).

### <a name="where-can-i-find-pricing-details-for-azure-data-factory"></a>Onde posso encontrar detalhes de preços do Data Factory do Azure?
Consulte [página de detalhes de preços de fábrica de dados] [ adf-pricing-details] para Olá detalhes de saudação do Azure Data Factory preços.  

### <a name="how-do-i-get-started-with-azure-data-factory"></a>Como faço para começar a utilizar o Azure Data Factory?
* Para obter uma visão geral do Azure Data Factory, consulte [tooAzure Introdução fábrica de dados](data-factory-introduction.md).
* Para obter um tutorial sobre como muito**copiar/mover dados** usando a atividade de cópia, consulte [copiar dados de armazenamento de BLOBs do Azure tooAzure banco de dados SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
* Para obter um tutorial sobre como muito**transformar dados** usando a atividade de Hive do HDInsight. Consulte [Processar dados executando o script do Hive no cluster do Hadoop](data-factory-build-your-first-pipeline.md)

### <a name="what-is-hello-data-factorys-region-availability"></a>O que é a disponibilidade de região da fábrica de dados Olá?
O Data Factory está disponível no **Oeste dos EUA** e no **Europa Setentrional**. Olá computação e serviços de armazenamento usados por fábricas de dados podem estar em outras regiões. Consulte [Regiões com suporte](data-factory-introduction.md#supported-regions).

### <a name="what-are-hello-limits-on-number-of-data-factoriespipelinesactivitiesdatasets"></a>Quais são os limites de saudação no número de fábricas/pipelines/atividades/conjuntos de dados?
Consulte **limites de fábrica de dados do Azure** seção Olá [assinatura do Azure e limites de serviço, cotas e restrições](../azure-subscription-service-limits.md#data-factory-limits) artigo.

### <a name="what-is-hello-authoringdeveloper-experience-with-azure-data-factory-service"></a>O que é a experiência de criação/desenvolvedor de saudação com o serviço do Azure Data Factory?
Você pode criar/criar as fábricas de dados usando uma saudação SDKs/ferramentas a seguir:

* **Portal do Azure** folhas de fábrica de dados Olá no portal do Azure de saudação fornecem interface do usuário avançada para você toocreate serviços de ad vinculado de fábricas de dados. Olá **Editor da fábrica de dados**, que também faz parte do portal hello, permite que você tooeasily criar serviços vinculados, tabelas, conjuntos de dados e pipelines especificando definições de JSON para esses artefatos. Consulte [criar seu primeiro pipeline de dados usando o portal do Azure](data-factory-build-your-first-pipeline-using-editor.md) para um exemplo de uso Olá toocreate editor do portal e implantar uma fábrica de dados.
* **O Visual Studio** você pode usar o Visual Studio toocreate uma fábrica de dados do Azure. Consulte [Criar seu primeiro pipeline de dados usando o Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) para obter detalhes.
* **Azure PowerShell** Veja [Criar e monitorar o Azure Data Factory usando o Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md) para ver um tutorial/passo a passo da criação de uma fábrica de dados usando o PowerShell. Confira o conteúdo de [Referência de cmdlets do Data Factory][adf-powershell-reference] na Biblioteca do MSDN para obter uma documentação abrangente de cmdlets de Data Factory.
* **Biblioteca de classes .NET** Você pode criar fábricas de dados programaticamente usando o SDK do .NET de Data Factory. Confira [Criar, monitorar e gerenciar fábricas de dados usando o SDK do .NET](data-factory-create-data-factories-programmatically.md) para obter uma explicação sobre a criação de uma fábrica de dados usando o SDK do .NET. Confira a [Referência da Biblioteca de Classes de Data Factory][msdn-class-library-reference] para obter uma documentação abrangente sobre o SDK do .NET de Data Factory.
* **API REST** também pode usar Olá API REST expostos pelo toocreate de serviço do Azure Data Factory hello e implantar as fábricas de dados. Confira a [Referência da API REST de Data Factory][msdn-rest-api-reference] para obter uma documentação abrangente da API REST de Data Factory.
* **Modelo do Azure Resource Manager** Consulte [Tutorial: Criar a sua primeira Azure Data Factory usando o modelo do Azure Resource Manager](data-factory-build-your-first-pipeline-using-arm.md) para obter detalhes.

### <a name="can-i-rename-a-data-factory"></a>Posso renomear um Data Factory?
Não. Como os outros recursos do Azure, o nome de saudação de uma fábrica de dados do Azure não pode ser alterado.

### <a name="can-i-move-a-data-factory-from-one-azure-subscription-tooanother"></a>Pode mover uma fábrica de dados de um tooanother de assinatura do Azure?
Sim. Saudação de uso **mover** botão na sua folha de fábrica de dados, conforme mostrado no diagrama a seguir de saudação:

![Mover o Data Factory](media/data-factory-faq/move-data-factory.png)

### <a name="what-are-hello-compute-environments-supported-by-data-factory"></a>Quais são os ambientes de computação de saudação suportados pela fábrica de dados?
Olá tabela a seguir fornece uma lista de ambientes de computação tem suportada pela fábrica de dados e hello atividades que podem ser executados neles.

| Ambiente de computação | atividades |
| --- | --- |
| [Cluster HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) ou [seu próprio cluster HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop Streaming](data-factory-hadoop-streaming-activity.md) |
| [Lote do Azure](data-factory-compute-linked-services.md#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| 
            [Azure Machine Learning](data-factory-compute-linked-services.md#azure-machine-learning-linked-service) |[Atividades de Machine Learning: execução do Lote e recurso de atualização](data-factory-azure-ml-batch-execution-activity.md) |
| [Análise Azure Data Lake](data-factory-compute-linked-services.md#azure-data-lake-analytics-linked-service) |[U-SQL da Análise Data Lake](data-factory-usql-activity.md) |
| [Azure SQL](data-factory-compute-linked-services.md#azure-sql-linked-service), [Azure SQL Data Warehouse](data-factory-compute-linked-services.md#azure-sql-data-warehouse-linked-service), [SQL Server](data-factory-compute-linked-services.md#sql-server-linked-service) |[Procedimento armazenado](data-factory-stored-proc-activity.md) |

### <a name="how-does-azure-data-factory-compare-with-sql-server-integration-services-ssis"></a>Como o Azure Data Factory se compara com o SSIS (SQL Server Integration Services)? 
Consulte Olá [do Azure Data Factory vs. SSIS](http://www.sqlbits.com/Sessions/Event15/Azure_Data_Factory_vs_SSIS) de um dos nossos MVPs (Most Valued Professionals): Reza Rad. Algumas das alterações recentes de saudação na fábrica de dados não podem ser listadas na apresentação de slides Olá. Estamos continuamente adicionando mais recursos tooAzure fábrica de dados. Estamos continuamente adicionando mais recursos tooAzure fábrica de dados. Podemos será incorporar essas atualizações comparação Olá das tecnologias de integração de dados da Microsoft mais tarde neste ano.   

## <a name="activities---faq"></a>Atividades - Perguntas frequentes
### <a name="what-are-hello-different-types-of-activities-you-can-use-in-a-data-factory-pipeline"></a>Quais são Olá diferentes tipos de atividades que você pode usar em um pipeline da fábrica de dados?
* [As atividades de movimentação de dados](data-factory-data-movement-activities.md) toomove dados.
* [Atividades de transformação de dados](data-factory-data-transformation-activities.md) tooprocess/transformar dados.

### <a name="when-does-an-activity-run"></a>Quando uma atividade é executada?
Olá **disponibilidade** configuração Olá saída de tabela de dados determina quando a atividade de saudação é executada. Se os conjuntos de dados de entrada forem especificados, atividade de saudação verifica se todas as dependências de dados de entrada hello forem atendidas (ou seja, **pronto** estado) antes de iniciar a execução.

## <a name="copy-activity---faq"></a>Atividade de Cópia - Perguntas frequentes
### <a name="is-it-better-toohave-a-pipeline-with-multiple-activities-or-a-separate-pipeline-for-each-activity"></a>É melhor toohave um pipeline com várias atividades ou um pipeline separado para cada atividade?
Pipelines devem atividades relacionadas à toobundle. Se Olá conjuntos de dados que se conectam a eles não são consumidos por qualquer outra atividade fora Olá pipeline, você pode manter atividades de saudação em um pipeline. Dessa forma, você não precisará períodos ativos do pipeline toochain para que elas se alinham com o outro. Além disso, Olá integridade de dados em tabelas de saudação pipeline toohello interno é preservado melhor ao atualizar o pipeline de saudação. Atualização do pipeline essencialmente interrompe todas as atividades de saudação no pipeline de saudação, remove e criá-los novamente. Da perspectiva de criação, também pode ser mais fácil fluxo de saudação toosee de dados dentro de saudação relacionado atividades em JSON de um arquivo para o pipeline de saudação.

### <a name="what-are-hello-supported-data-stores"></a>Quais são Olá suporte para armazenamentos de dados?
Atividade de cópia na fábrica de dados copia dados de um repositório de dados fonte dados repositório tooa coletor. Fábrica de dados oferece suporte a saudação armazenamentos de dados a seguir. Dados de qualquer fonte podem ser gravados tooany coletor. Clique em um toolearn de repositório de dados como toocopy tooand de dados do repositório.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Armazena dados com * pode ser local ou na IaaS do Azure e requer que você tooinstall [Data Management Gateway](data-factory-data-management-gateway.md) em uma máquina de IaaS no local/Azure.

### <a name="what-are-hello-supported-file-formats"></a>Quais são Olá suporte para formatos de arquivo?
[!INCLUDE [data-factory-file-format](../../includes/data-factory-file-format.md)]

### <a name="where-is-hello-copy-operation-performed"></a>Em que a operação de cópia de saudação é executada?
Consulte [Movimento de dados globalmente disponível](data-factory-data-movement-activities.md#global) seção para obter detalhes. Em suma, quando um armazenamento de dados local estiver envolvido, operação de cópia de saudação é executada por Olá Data Management Gateway em seu ambiente local. E, quando a movimentação de dados Olá entre dois armazenamentos de nuvem, a operação de cópia de saudação é executada em Olá região mais próxima toohello coletor local Olá mesmo Geografia.

## <a name="hdinsight-activity---faq"></a>Atividade de HDInsight - Perguntas frequentes
### <a name="what-regions-are-supported-by-hdinsight"></a>O HDInsight dá suporte a quais regiões?
Consulte Olá seção disponibilidade geográfica Olá artigo a seguir: ou [detalhes de preços do HDInsight][hdinsight-supported-regions].

### <a name="what-region-is-used-by-an-on-demand-hdinsight-cluster"></a>Qual região é utilizada por um cluster HDInsight sob demanda?
Olá cluster do HDInsight sob demanda é criado no hello mesmo região onde o armazenamento Olá especificado toobe usado com cluster Olá existe.    

### <a name="how-tooassociate-additional-storage-accounts-tooyour-hdinsight-cluster"></a>Como contas de armazenamento adicionais tooassociate tooyour HDInsight cluster?
Se você estiver usando seu próprio HDInsight Cluster (BYOC - traga seu próprio Cluster), consulte Olá seguintes tópicos:

* [Usando um Cluster HDInsight com metastores e contas de armazenamento alternativas][hdinsight-alternate-storage]
* [Usar contas de armazenamento adicionais com o HDInsight Hive][hdinsight-alternate-storage-2]

Se você estiver usando um cluster sob demanda que é criado pela Olá serviço da fábrica de dados, especifique as contas de armazenamento adicional para Olá HDInsight serviço vinculado para que o serviço do Data Factory Olá pode registrá-los em seu nome. Olá definição JSON para o serviço vinculado do hello sob demanda, usar **additionalLinkedServiceNames** contas de armazenamento alternativo de toospecify de propriedade conforme mostrado no hello trecho JSON a seguir:

```JSON
{
    "name": "MyHDInsightOnDemandLinkedService",
    "properties":
    {
        "type": "HDInsightOnDemandLinkedService",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "LinkedService-SampleData",
            "additionalLinkedServiceNames": [ "otherLinkedServiceName1", "otherLinkedServiceName2" ]
        }
    }
}
```
No exemplo hello acima, otherLinkedServiceName1 e otherLinkedServiceName2 representam serviços vinculados cujas definições contêm as credenciais que Olá contas de armazenamento alternativo do HDInsight cluster necessidades tooaccess.

## <a name="slices---faq"></a>Fatias - Perguntas frequentes
### <a name="why-are-my-input-slices-not-in-ready-state"></a>Por que minhas fatias de entrada não estão no estado Pronto?
Um erro comum não está configurando **externo** propriedade muito**true** em Olá dataset de entrada quando os dados de entrada hello é fábrica de dados toohello externo (não produzida pela fábrica de dados Olá).

Na saudação de exemplo a seguir, você precisa apenas tooset **externo** tootrue na **dataset1**.  

**DataFactory1** Pipeline 1: dataset1 -> activity1 -> dataset2 -> activity2 -> dataset3 Pipeline 2: dataset3-> activity3 -> dataset4

Se você tiver outro fábrica de dados com um pipeline que usa dataset4 (produzido pelo pipeline 2 na fábrica de dados 1), marca dataset4 como um conjunto de dados externo, pois Olá dataset é produzido por uma fábrica de dados diferentes (DataFactory1, não DataFactory2).  

**DataFactory2**    
Pipeline 1: dataset4->activity4->dataset5

Se a propriedade externa Olá esteja definida corretamente, verifique se os dados de entrada hello existem no local de saudação especificado na definição de conjunto de dados de entrada hello.

### <a name="how-toorun-a-slice-at-another-time-than-midnight-when-hello-slice-is-being-produced-daily"></a>Como toorun uma fatia em outro momento de meia-noite quando fatia hello está sendo produzida diariamente?
Saudação de uso **deslocamento** tempo de saudação toospecify de propriedade no qual você deseja Olá fatia toobe produzido. Confira a seção [Disponibilidade do conjunto de dados](data-factory-create-datasets.md#dataset-availability) para obter detalhes sobre essa propriedade. Aqui está um exemplo rápido:

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
Intervalos diários começam em **6H** em vez de meia-noite do saudação padrão.     

### <a name="how-can-i-rerun-a-slice"></a>Como executo novamente uma fatia?
Você pode executar novamente uma fatia em uma saudação maneiras a seguir:

* Use uma janela de atividade de toorerun de monitorar e gerenciar o aplicativo ou fatia. Veja [Executar novamente as janelas de atividades selecionadas](data-factory-monitor-manage-app.md#perform-batch-actions) para obter instruções.   
* Clique em **executar** na barra de comando Olá Olá **FATIA de dados** folha de fatia Olá Olá portal do Azure.
* Executar **conjunto AzureRmDataFactorySliceStatus** cmdlet com Status definido muito**esperando** fatia hello.   

    ```PowerShell
    Set-AzureRmDataFactorySliceStatus -Status Waiting -ResourceGroupName $ResourceGroup -DataFactoryName $df -TableName $table -StartDateTime "02/26/2015 19:00:00" -EndDateTime "02/26/2015 20:00:00"
    ```
Consulte [conjunto AzureRmDataFactorySliceStatus] [ set-azure-datafactory-slice-status] para obter detalhes sobre o cmdlet hello.

### <a name="how-long-did-it-take-tooprocess-a-slice"></a>Quanto tempo demorou tooprocess uma fatia?
Use o Gerenciador de janela de atividade no Monitor do & aplicativo gerenciar tooknow quanto tempo levou tooprocess uma fatia de dados. Confira [Gerenciador de Janelas de Atividades](data-factory-monitor-manage-app.md#activity-window-explorer) para obter detalhes.

Você também pode fazer Olá seguinte em Olá portal do Azure:  

1. Clique em **conjuntos de dados** bloco Olá **DATA FACTORY** folha sua fábrica de dados.
2. Clique em conjunto de dados específico em Olá Olá **conjuntos de dados** folha.
3. Fatia Olá Select que você está interessado em da saudação **fatias recentes** lista Olá **tabela** folha.
4. Clique hello atividade executar da saudação **execuções de atividade** lista Olá **FATIA de dados** folha.
5. Clique em **propriedades** bloco Olá **detalhes de execução da atividade** folha.
6. Você deve ver Olá **duração** campo com um valor. Esse valor é o tempo Olá tooprocess fatia de saudação.   

### <a name="how-toostop-a-running-slice"></a>Como toostop uma fatia em execução?
Se você precisar de pipeline de saudação toostop da execução, você poderá usar [AzureRmDataFactoryPipeline Suspend](/powershell/module/azurerm.datafactories/suspend-azurermdatafactorypipeline) cmdlet. Atualmente, suspender pipeline Olá não pare execuções de fatia Olá que estão em andamento. Depois de terminar de execuções do hello em andamento, nenhuma fatia extra é selecionada.

Se você realmente deseja toostop todas as execuções de saudação imediatamente, hello somente forma seria toodelete Olá pipeline e criá-la novamente. Se você escolher o pipeline de saudação toodelete, não é necessário toodelete tabelas e serviços vinculados usados pelo pipeline de saudação.

[create-factory-using-dotnet-sdk]: data-factory-create-data-factories-programmatically.md
[msdn-class-library-reference]: /dotnet/api/microsoft.azure.management.datafactories.models
[msdn-rest-api-reference]: /rest/api/datafactory/

[adf-powershell-reference]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/azurerm.datafactories
[azure-portal]: http://portal.azure.com
[set-azure-datafactory-slice-status]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/set-azurermdatafactoryslicestatus

[adf-pricing-details]: http://go.microsoft.com/fwlink/?LinkId=517777
[hdinsight-supported-regions]: http://azure.microsoft.com/pricing/details/hdinsight/
[hdinsight-alternate-storage]: http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx
[hdinsight-alternate-storage-2]: http://blogs.msdn.com/b/cindygross/archive/2014/05/05/use-additional-storage-accounts-with-hdinsight-hive.aspx
