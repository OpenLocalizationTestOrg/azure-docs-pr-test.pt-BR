---
title: "aaaIntroduction tooData fábrica, o serviço de integração de dados | Microsoft Docs"
description: "Saiba o que é o Azure Data Factory: um serviço de integração de dados de nuvem que orquestra e automatiza a movimentação e a transformação dos dados."
keywords: "integração de dados, integração de dados de nuvem, o que é o azure data factory"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: cec68cb5-ca0d-473b-8ae8-35de949a009e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 4cc30515315efc938951057743ff8eb3701214ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-data-factory"></a>Introdução tooAzure fábrica de dados 
## <a name="what-is-azure-data-factory"></a>O que é o Data Factory do Azure?
Em Olá mundo de dados grandes, como é dados existentes utilizados na empresa? É possível tooenrich dados gerados na nuvem hello usando dados de referência de fontes de dados locais ou outras fontes de dados diferentes? Por exemplo, uma empresa de jogos coleta muitos logs produzidos por jogos na nuvem hello. Ele deseja tooanalyze desses insights toogain de logs no comportamento de uso, dados demográficos, toocustomer preferências etc. tooidentify vendas e venda cruzada oportunidades, desenvolver novos interessantes de crescimento recursos toodrive comercial e fornecer uma melhor experiência toocustomers. 

tooanalyze esses logs, a empresa Olá precisa de dados de referência de saudação toouse como informações do cliente, informações sobre o jogo, informações de campanha em um repositório de dados do local de marketing. Portanto, a empresa de Olá deseja tooingest dados de log de armazenamento de dados de nuvem hello e dados de referência do armazenamento de dados local hello. Em seguida, processar dados de saudação usando Hadoop no hello nuvem (Azure HDInsight) e publicar resultados de saudação do repositório de dados em um data warehouse de nuvem, como o Azure SQL Data Warehouse ou dados de um local como o SQL Server. Ele deseja toorun este fluxo de trabalho semanal uma vez. 

O que é necessário é uma plataforma que permite a saudação da empresa toocreate um fluxo de trabalho pode ingestão de dados de locais e repositórios de dados de nuvem e transformação ou processam dados por meio de serviços de computação existente como o Hadoop e publicar Olá resultados tooan local ou o armazenamento de dados de nuvem para tooconsume de aplicativos de BI. 

![Visão geral do Data Factory](media/data-factory-introduction/what-is-azure-data-factory.png) 

A fábrica de dados do Azure é a plataforma de saudação para esse tipo de cenários. É um **serviço de integração de dados com base em nuvem que permite que você toocreate fluxos de trabalho controlados por dados na nuvem Olá para orquestrar e automatizar a movimentação de dados e a transformação de dados**. Utilizando a fábrica de dados do Azure, você pode criar e agendar controladas por dados fluxos de trabalho (chamados de pipelines) que pode incluir dados de armazenamentos de dados diferentes, processo/transformar dados saudação usando os serviços de computação, como Hadoop de HDInsight do Azure, Spark, Azure Data Lake Análise e aprendizado de máquina do Azure e publicar dados toodata armazena como Azure SQL Data Warehouse para business intelligence (BI) aplicativos tooconsume de saída.  

Essa é uma plataforma mais de Extrair e Carregar (EL) e, em seguida, Transformar e Carregar (TL) do que uma plataforma de Extrair, Carregar e Transformar (ETL) tradicional. transformações de saudação que são executadas são tootransform/processar dados usando os serviços de computação em vez de derivados de transformações tooperform como Olá aqueles para adicionar colunas, contando o número de linhas, classificação de dados, etc. 

Atualmente, na fábrica de dados do Azure, dados de saudação que são consumidos e produzidos por fluxos de trabalho são **dados segmentados de tempo** (por hora, diariamente, semanalmente, etc.). Por exemplo, um pipeline pode ler dados de entrada, processar dados e produzir dados de saída uma vez por dia. Você também pode executar um fluxo de trabalho apenas uma vez.  
  

## <a name="how-does-it-work"></a>Como ele funciona? 
pipelines de saudação (fluxos de trabalho orientados a dados) no Azure Data Factory normalmente executam Olá três etapas a seguir:

![As três etapas do Azure Data Factory](media/data-factory-introduction/three-information-production-stages.png)

### <a name="connect-and-collect"></a>Conectar e coletar
As empresas possuem dados de diferentes tipos, localizados em diferentes fontes. primeira etapa na criação de um sistema de produção informações Hello é fontes de saudação necessária tooall tooconnect de dados e processamento, como os serviços de SaaS, serviços da web FTP, compartilhamentos de arquivos e mover Olá dados conforme necessário tooa centralizado local para subsequentes processamento.

Sem dados de fábrica, as empresas devem criar componentes de movimentação de dados personalizados ou escrever serviços personalizados toointegrate essas fontes de dados e o processamento. É caro e difícil toointegrate e manter esses sistemas, e geralmente não tem pequeno porte de saudação de monitoramento e alertas e controles de saudação que pode oferecer um serviço totalmente gerenciado.

Com a fábrica de dados, você pode usar o hello atividade de cópia em um pipeline de dados toomove dados de ambos os locais e na nuvem fonte dados repositórios tooa centralizar o armazenamento de dados na nuvem Olá para análise posterior. Por exemplo, você pode coletar dados em um repositório Azure Data Lake e transformação de dados hello mais tarde por meio de um serviço de computação da análise Azure Data Lake. Ou, coletar dados em Armazenamento de Blobs do Azure e transformam dados posteriormente usando um cluster de Hadoop do Azure HDInsight.

### <a name="transform-and-enrich"></a>Transformar e enriquecer
Depois que os dados estão presentes em um repositório de dados centralizado na nuvem hello, convém Olá coletado dados toobe processado ou transformados usando os serviços de computação como HDInsight Hadoop, Spark, análise Data Lake e aprendizado de máquina. Deseja que os dados de produção transformado de tooreliably em ambientes de produção de toofeed uma agenda de manutenção e controlado com dados confiáveis. 

### <a name="publish"></a>Publicar 
Entregar os dados transformados de nuvem Olá fontes tooon local como o SQL Server, ou mantê-lo em sua nuvem de fontes de armazenamento para consumo pelo business intelligence (BI) e ferramentas de análise e outros aplicativos.

## <a name="key-components"></a>Principais componentes
Uma assinatura do Azure pode ter um ou mais instâncias do Azure Data Factory (ou fábricas de dados). A fábrica de dados do Azure é composta por quatro componentes principais que funcionam em conjunto tooprovide plataforma de saudação no qual você pode compor controladas por dados fluxos de trabalho com etapas toomove e transformar dados. 

### <a name="pipeline"></a>Pipeline
Um data factory pode ter um ou mais pipelines. Um pipeline é um grupo de atividades. Juntas, as atividades de saudação em um pipeline executam uma tarefa. Por exemplo, um pipeline pode conter um grupo de atividades que recebe dados de um blob do Azure e, em seguida, executar uma consulta de Hive em um HDInsight cluster toopartition Olá de dados. Olá vantagem disso é que pipeline Olá permite que você toomanage atividades de saudação como um conjunto em vez de cada um deles individualmente. Por exemplo, você pode implantar e agendar pipeline hello, em vez de atividades de saudação independentemente. 

### <a name="activity"></a>Atividade
Um pipeline pode ter uma ou mais atividades. Atividades definem Olá ações tooperform em seus dados. Por exemplo, você pode usar um toocopy dados da atividade de cópia de repositório de dados de tooanother de repositório de dados. Da mesma forma, você pode usar uma atividade de Hive, que executa uma consulta de Hive em um tootransform de cluster do HDInsight do Azure ou analisar seus dados. O Data Factory dá suporte a dois tipos de atividades: atividades de movimentação de dados e atividades de transformação de dados.

### <a name="data-movement-activities"></a>Atividades de movimentação de dados
Atividade de cópia na fábrica de dados copia dados de um repositório de dados fonte dados repositório tooa coletor. Fábrica de dados oferece suporte a saudação armazenamentos de dados a seguir. Dados de qualquer fonte podem ser gravados tooany coletor. Clique em um toolearn de repositório de dados como toocopy tooand de dados do repositório.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

Para obter mais informações, confira o artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md).

### <a name="data-transformation-activities"></a>Atividades de transformação de dados
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

Para obter mais informações, confira o artigo [Atividades de transformação de dados](data-factory-data-transformation-activities.md).

### <a name="custom-net-activities"></a>Atividades personalizadas do .NET
Se você precisar toomove dados para/de um repositório de dados dessa atividade de cópia não oferecer suporte a, ou transformar dados usando sua própria lógica, crie um **atividade personalizada do .NET**. Para obter detalhes sobre como criar e usar uma atividade personalizada, confira [Usar atividades personalizadas em um pipeline do Azure Data Factory](data-factory-use-custom-activities.md).

### <a name="datasets"></a>Conjunto de dados
Uma atividade aceita zero ou mais conjuntos de dados como entrada e produz um ou mais conjuntos de dados como saídas. Conjuntos de dados representam estruturas de dados em repositórios de dados hello, que simplesmente aponte ou fazem referência a dados Olá que deseja toouse em suas atividades como entradas ou saídas. Por exemplo, um conjunto de dados de Blob do Azure Especifica Olá contêiner de blob e a pasta no armazenamento de BLOBs do Azure saudação do qual Olá pipeline deve ler dados de saudação. Ou, um conjunto de dados de tabela do SQL Azure Especifica dados de saída de saudação do hello tabela toowhich foi criados pela atividade de saudação. 

### <a name="linked-services"></a>Serviços vinculados
Serviços vinculados são bem semelhantes às cadeias de caracteres de conexão, que definem informações de conexão de Olá necessárias para os recursos do Data Factory tooconnect tooexternal. Pense desta maneira - um serviço vinculado define a fonte de dados de toohello Olá conexão e um conjunto de dados representa a estrutura de saudação de dados de saudação. Por exemplo, um serviço vinculado do armazenamento do Azure Especifica a conta de armazenamento Azure toohello do tooconnect de cadeia de caracteres de conexão. E, um conjunto de dados de Blob do Azure Especifica o contêiner de blob hello e a pasta de saudação que contém dados de saudação.   

Serviços vinculados são usados para duas finalidades no Data Factory:

* toorepresent um **repositório de dados** incluindo, mas não limitado a, um SQL Server no local, o banco de dados Oracle, compartilhamento de arquivos ou uma conta de armazenamento de BLOBs do Azure. Consulte Olá [atividades de movimentação de dados](#data-movement-activities) seção para obter uma lista de repositórios de dados com suporte.
* toorepresent um **de recursos de computação** que pode hospedar a execução de saudação de uma atividade. Por exemplo, hello atividade HDInsightHive é executado em um cluster HDInsight Hadoop. Confira a seção [Atividades de transformação de dados](#data-transformation-activities) para obter uma lista de ambientes de computação com suporte.

### <a name="relationship-between-data-factory-entities"></a>Relação entre entidades de Data Factory
![Diagrama: Data Factory, um serviço de integração de dados de nuvem - conceitos principais](./media/data-factory-introduction/data-integration-service-key-concepts.png)
**Figure 2.** Relações entre o Conjunto de dados, Atividade, Pipeline e Serviço vinculado

## <a name="supported-regions"></a>Regiões com suporte
No momento, você pode criar as fábricas de dados em Olá **Oeste dos EUA**, **Leste dos EUA**, e **Norte da Europa** regiões. No entanto, uma fábrica de dados pode acessar repositórios de dados e computação serviços em outros dados de toomove regiões do Azure entre armazenamentos de dados ou processar dados usando os serviços de computação.

O Azure Data Factory em si não armazena dados. Ele permite que você crie fluxos de trabalho controlados por dados tooorchestrate movimentação de dados entre [suporte para armazenamentos de dados](#data-movement-activities) e processamento de dados usando [serviços de computação](#data-transformation-activities) em outras regiões ou em um local ambiente. Ele também permite que você muito[monitorar e gerenciar fluxos de trabalho](data-factory-monitor-manage-pipelines.md) usando programático e mecanismos de interface do usuário.

Mesmo que a fábrica de dados está disponível somente em **Oeste dos EUA**, **Leste dos EUA**, e **Norte da Europa** regiões, o serviço de saudação habilitação de movimentação de dados de saudação na fábrica de dados está disponível [globalmente](data-factory-data-movement-activities.md#global) em várias regiões. Se um repositório de dados estiver protegido por um firewall, em seguida, um [Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) instalado em seu ambiente move Olá de dados locais em vez disso.

Por exemplo, digamos que seus ambientes de computação, como o cluster Azure HDInsight e o Azure Machine Learning, estejam ficando sem a região Europa Ocidental. Você pode criar e usar uma instância do Azure Data Factory no Norte da Europa e usá-lo tooschedule trabalhos em seus ambientes de computação na Europa Ocidental. Leva alguns milissegundos para o trabalho de saudação tootrigger fábrica de dados em seu ambiente de computação, mas não altera o tempo de saudação para executar o trabalho de saudação em seu ambiente de computação.

## <a name="get-started-with-creating-a-pipeline"></a>Introdução à criação de um pipeline
Você pode usar uma dessas ferramentas ou pipelines de dados APIs toocreate na fábrica de dados do Azure: 

- Portal do Azure
- Visual Studio
- PowerShell
- API do .NET
- API REST
- Modelo do Azure Resource Manager. 

toolearn como toobuild fábricas de dados com dados pipelines, siga as instruções passo a passo em Olá tutoriais a seguir:

| Tutorial | Descrição |
| --- | --- |
| [Mover dados entre dois armazenamentos de dados em nuvem](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) |Neste tutorial, você criará uma fábrica de dados com um pipeline que **move dados** do banco de dados de tooSQL de armazenamento de Blob. |
| [Transformar dados usando o cluster Hadoop](data-factory-build-your-first-pipeline.md) |Neste tutorial, você cria seu primeiro data factory no Azure com um pipeline de dados que **processa os dados** executando o script do Hive em um cluster Azure HDInsight (Hadoop). |
| [Mover dados entre um armazenamento de dados local e um armazenamento de dados em nuvem usando o Gateway de Gerenciamento de Dados](data-factory-move-data-between-onprem-and-cloud.md) |Neste tutorial, você criará uma fábrica de dados com um pipeline que **move dados** de um **local** tooan de banco de dados do SQL Server BLOBs do Azure. Como parte da saudação passo a passo, você instale e configure Olá Data Management Gateway em seu computador. |
