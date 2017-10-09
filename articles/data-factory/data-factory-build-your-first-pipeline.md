---
title: 'Tutorial do Data Factory: primeiro pipeline de dados | Microsoft Docs'
description: "Este tutorial do Azure Data Factory mostra como toocreate e agendar uma fábrica de dados que processa dados usando a seção scripts em um cluster Hadoop."
services: data-factory
keywords: tutorial do azure data factory , cluster hadoop, hive do hadoop
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.assetid: 81f36c76-6e78-4d93-a3f2-0317b413f1d0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: ed9c0ade4500d4ac1f7c2c2312c1fa675e0b1f02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-pipeline-tootransform-data-using-hadoop-cluster"></a>Tutorial: Crie sua primeira pipeline tootransform de dados usando o cluster Hadoop
> [!div class="op_single_selector"]
> * [Visão geral e pré-requisitos](data-factory-build-your-first-pipeline.md)
> * [Portal do Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modelo do Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)

Neste tutorial, você deve criar sua Azure Data Factory com um pipeline de dados. pipeline de saudação transforma dados de entrada ao executar o script de Hive em um cluster de HDInsight do Azure (Hadoop) tooproduce saída dados.  

Este artigo fornece visão geral e pré-requisitos para o tutorial hello. Depois de concluir os pré-requisitos de saudação, você pode fazer tutorial hello usando uma saudação SDKs/ferramentas a seguir: portal do Azure, o Visual Studio, o PowerShell, o modelo do Gerenciador de recursos, API REST. Selecione uma das opções de saudação na lista suspensa de Olá Olá início (ou) links no final da saudação deste tutorial de saudação do artigo toodo usando uma dessas opções.    

## <a name="tutorial-overview"></a>Visão geral do tutorial
Neste tutorial, você deve executar Olá etapas a seguir:

1. Criar uma **data factory**. Um data factory pode conter um ou mais pipelines de dados que movem e transformam dados. 

    Neste tutorial, você deve criar um pipeline na fábrica de dados hello. 
2. Criar um **pipeline**. Um pipeline pode ter uma ou mais atividades (exemplos: atividade de cópia, atividade de Hive do HDInsight). Este exemplo usa hello atividade Hive do HDInsight que executa um script do Hive em um cluster HDInsight Hadoop. script Hello primeiro cria uma tabela de referências Olá dados de log web bruto armazenados no armazenamento de BLOBs do Azure e, em seguida, partições Olá dados brutos por ano e mês.

    Neste tutorial, o pipeline de saudação usa dados de tootransform de atividade de Hive saudação executando uma consulta de Hive em um cluster de Hadoop de HDInsight do Azure. 
3. Crie **serviços vinculados**. Você cria um serviço vinculado toolink um repositório de dados ou uma fábrica de dados de toohello de serviço de computação. Um repositório de dados, como o armazenamento do Azure contém os dados de entrada/saída de atividades no pipeline de saudação. Um serviço de computação, como o cluster de Hadoop do HDInsight, processa/transforma os dados.

    Neste tutorial, você deve criar dois serviços vinculados: **Armazenamento do Azure** e **Azure HDInsight**. saudação de armazenamento do Azure vinculado links de serviço uma conta de armazenamento do Azure que contém a fábrica de dados de toohello Olá dados de entrada/saída. HDInsight do Azure vinculada links de serviço um cluster HDInsight do Azure que é usado tootransform fábrica de dados de toohello de dados. 
3. Criar **conjuntos de dados**de entrada e saída. Um conjunto de dados de entrada representa a entrada de saudação para uma atividade no pipeline de saudação e um conjunto de dados de saída representa a saída de hello atividade hello.

    Neste tutorial, Olá de entrada e saída conjuntos de dados especificam locais de entrada e Olá de dados de saída no armazenamento de BLOBs do Azure. Olá serviço vinculado do armazenamento do Azure Especifica qual conta de armazenamento do Azure é usado. Um conjunto de dados de entrada especifica onde os arquivos de entrada hello estão localizados e um conjunto de dados de saída Especifica onde os arquivos de saída de hello são colocados. 


Consulte [tooAzure Introdução Data Factory](data-factory-introduction.md) artigo para uma visão geral detalhada da fábrica de dados do Azure.
  
Aqui está a saudação **exibição de diagrama** da fábrica de dados de exemplo hello compilação neste tutorial. **MyFirstPipeline** tem uma atividade de Hive que consome o conjunto de dados **AzureBlobInput** como uma entrada e produz o conjunto de dados **AzureBlobOutput** como uma saída. 

![Exibição de diagrama no tutorial do Data Factory](media/data-factory-build-your-first-pipeline/data-factory-tutorial-diagram-view.png)


Neste tutorial, **inputdata** pasta da saudação **adfgetstarted** contêiner de BLOBs do Azure contém um arquivo chamado input.log. Esse arquivo de log tem entradas de três meses: janeiro, fevereiro e março de 2016. Aqui estão as linhas de exemplo de saudação para cada mês no arquivo de entrada hello. 

```
2016-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871 
2016-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2016-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

Quando o arquivo hello é processado pelo pipeline de saudação com atividade de Hive do HDInsight, atividade Olá executa um script de Hive no cluster do HDInsight Olá que partições de dados de entrada por ano e mês. script Hello cria três pastas de saída que contém um arquivo com entradas de cada mês.  

```
adfgetstarted/partitioneddata/year=2016/month=1/000000_0
adfgetstarted/partitioneddata/year=2016/month=2/000000_0
adfgetstarted/partitioneddata/year=2016/month=3/000000_0
```

De linhas de saudação de exemplo mostradas acima, hello primeiro (com o 2016-01-01) é gravado toohello 000000_0 arquivo mês hello = 1 pasta. Da mesma forma, hello segunda escrita arquivo toohello em mês hello = 2 pasta e hello terceiro um escrito arquivo toohello em mês hello = 3 de pasta.  

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deve ter Olá pré-requisitos a seguir:

1. **Uma assinatura do Azure** - se você não tiver uma, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Consulte Olá [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/) artigo sobre como você pode obter uma conta de avaliação gratuita.
2. **Armazenamento do Azure** – use uma conta de finalidade geral de armazenamento do Azure padrão para armazenar dados de saudação neste tutorial. Se você não tiver uma conta de armazenamento do Azure padrão para diversos fins, consulte Olá [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artigo. Depois que você criou a conta de armazenamento hello, anote Olá **nome da conta** e **chave de acesso**. Consulte [Exibir, copiar e regenerar chaves de acesso de armazenamento](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).
3. Baixe e leia o arquivo de consulta de Hive hello (**HQL**) localizado em: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql). Essa consulta transforma dados de saída de tooproduce de dados de entrada. 
4. Baixe e leia o arquivo de entrada de exemplo hello (**input.log**) localizado em: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)
5. Crie um contêiner de blobs denominado **adfgetstarted** em seu armazenamento de blobs do Azure. 
6. Carregar **partitionweblogs.hql** arquivo toohello **script** pasta Olá **adfgetstarted** contêiner. Use ferramentas como o [Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com/). 
7. Carregar **input.log** arquivo toohello **inputdata** pasta Olá **adfgetstarted** contêiner. 

Depois de concluir os pré-requisitos de saudação, selecione uma das Olá seguir ferramentas/SDKs toodo Olá tutorial: 

- [Portal do Azure](data-factory-build-your-first-pipeline-using-editor.md)
- [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
- [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
- [Modelo do Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
- [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)

O portal do Azure e o Visual Studio permitem criar data factories com a GUI. Enquanto isso, as opções do PowerShell, do modelo do Resource Manager e a API REST permitem criar data factories com script/programação.

> [!NOTE]
> pipeline de dados Olá neste tutorial transforma dados de saída de tooproduce de dados de entrada. Ele não copia dados de um repositório de dados de destino fonte dados repositório tooa. Para obter um tutorial sobre como toocopy dados usando a fábrica de dados do Azure, consulte [Tutorial: copiar dados de armazenamento de Blob tooSQL banco de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> É possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada. Veja [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md) para obter informações detalhadas. 





  
