---
title: "aaaDemand previsão na guia técnico de energia | Microsoft Docs"
description: "Um guia técnico toohello modelo de solução com o Microsoft Cortana inteligência para previsão de vendas de energia."
services: cortana-analytics
documentationcenter: 
author: yijichen
manager: ilanr9
editor: yijichen
ms.assetid: 7f1a866b-79b7-4b97-ae3e-bc6bebe8c756
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: inqiu;yijichen;ilanr9
ms.openlocfilehash: c97b7c19c9e3a317aecc329e61a0692d2f1ec53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-demand-forecast-in-energy"></a>Guia técnico toohello Cortana inteligência de solução de modelo de previsão de vendas de energia
## <a name="overview"></a>**Visão geral**
Modelos de solução são projetados tooaccelerate processo de saudação da criação de uma demonstração E2E sobre o pacote de inteligência do Cortana. Um modelo implantado provisionará sua assinatura com o componente necessário do Cortana inteligência e criar relações de saudação entre. Ele também sementes de pipeline de saudação de dados com dados de exemplo obtendo gerados a partir de um aplicativo de simulação de dados. Baixar simulador de dados de saudação do link Olá fornecido e instalá-lo em seu computador local, consulte o arquivo Leiame. txt de toohello para obter instruções sobre como usar o simulador de saudação. Dados gerados a partir de simulador hello serão alimentar pipeline de dados hello e começar a gerar a previsão de aprendizado de máquina que, em seguida, pode ser visualizado no painel do Power BI hello.

o modelo de solução Olá pode ser encontrado [aqui](https://gallery.cortanaintelligence.com/SolutionTemplate/Demand-Forecasting-for-Energy-1)

o processo de implantação Olá orientará tooset de várias etapas as credenciais de sua solução. Certifique-se de que registrar essas credenciais como nome da solução, o nome de usuário e a senha fornecidos durante a implantação de saudação.

meta de saudação deste documento é arquitetura de referência tooexplain hello e diferentes componentes provisionados em sua assinatura como parte desse modelo de solução. documento de saudação também fala sobre como tooreplace Olá dados de exemplo, com dados reais de seus próprios toobe toosee capaz de insights/previsões você ganha dados. Além disso, Olá documento fala sobre partes de saudação do hello modelo de solução que seria necessário toobe modificado se você quiser solução de saudação do toocustomize com seus próprios dados. São fornecidas instruções sobre como toobuild hello o painel do Power BI para este modelo de solução final hello.

## <a name="big-picture"></a>**Visão global**
![](media/cortana-analytics-technical-guide-demand-forecast/ca-topologies-energy-forecasting.png)

### <a name="architecture-explained"></a>Arquitetura explicada
Quando Olá solução for implantada, vários serviços do Azure no Cortana Analytics Suite são ativados (*ou seja,* o Hub de Eventos, o Stream Analytics, o HDInsight, o Data Factory, o Machine Learning, *etc.*). diagrama de arquitetura de saudação acima mostra, em um nível alto, como Olá previsão de demanda para o modelo de solução de energia é construída de ponta a ponta. Você será capaz de tooinvestigate esses serviços clicando neles em Olá diagrama do modelo de solução criado com a implantação de saudação de solução de saudação. Olá seções a seguir descreve cada parte.

## <a name="data-source-and-ingestion"></a>**Fonte de dados e ingestão**
### <a name="synthetic-data-source"></a>Fonte de dados sintética
Fonte usada é gerado para esses dados de saudação do modelo de um aplicativo de área de trabalho que você irá baixar e executar localmente após a implantação bem-sucedida. Você encontrará toodownload de instruções hello e instalar este aplicativo na barra de propriedades hello quando você seleciona o primeiro nó de saudação chamado simulador de dados de previsão de energia no diagrama de modelo de solução de saudação. Este aplicativo feeds Olá [Hub de eventos do Azure](#azure-event-hub) serviço com pontos de dados ou eventos, que serão usados no restante de saudação do fluxo de solução de saudação.

aplicativo de geração de eventos Hello populará hello Azure Hub de eventos apenas enquanto ele está em execução no seu computador.

### <a name="azure-event-hub"></a>Hub de Eventos do Azure
Olá [Hub de eventos do Azure](https://azure.microsoft.com/services/event-hubs/) service é o destinatário de saudação de entrada hello fornecido pelo Olá sintética fonte de dados descrito acima.

## <a name="data-preparation-and-analysis"></a>**Preparação e análise de dados**
### <a name="azure-stream-analytics"></a>Stream Analytics do Azure
Olá [Stream Analytics do Azure](https://azure.microsoft.com/services/stream-analytics/) service é usado tooprovide próximo a análise em tempo real no fluxo de entrada de saudação do hello [Hub de eventos do Azure](#azure-event-hub) de serviço e publicar os resultados em um [doPowerBI](https://powerbi.microsoft.com) dashboard, bem como arquivamento todos bruto toohello de eventos de entrada [armazenamento do Azure](https://azure.microsoft.com/services/storage/) serviço para processamento posterior por Olá [do Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) serviço.

### <a name="hd-insights-custom-aggregation"></a>Agregação personalizada do HDInsight
Olá serviço Azure HD Insight é usado toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts (gerenciados pelo Azure Data Factory) tooprovide agregações em eventos brutos Olá foram arquivados usando o serviço do Azure Stream Analytics hello.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Olá [aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/) serviço é usado (orquestrada pelo Azure Data Factory) toomake de previsão no consumo de energia futuras de uma determinada região Olá entrada recebidas.

## <a name="data-publishing"></a>**Publicação de dados**
### <a name="azure-sql-database-service"></a>Serviço Banco de Dados SQL do Azure
Olá [banco de dados do SQL Azure](https://azure.microsoft.com/services/sql-database/) service é previsões de saudação toostore usado (gerenciado pelo Azure Data Factory) recebidas por Olá service de aprendizado de máquina do Azure que será consumido no hello [Power BI](https://powerbi.microsoft.com) painel.

## <a name="data-consumption"></a>**Consumo de dados**
### <a name="power-bi"></a>Power BI
Olá [Power BI](https://powerbi.microsoft.com) service é usado tooshow um painel que contém as agregações fornecidas pelo Olá [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) serviço, bem como a demanda prever os resultados armazenados em [SQL Azure Banco de dados](https://azure.microsoft.com/services/sql-database/) que foram produzidas usando Olá [aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/) serviço. Para obter instruções sobre como toobuild hello o painel do Power BI para este modelo de solução, consulte a seção de toohello abaixo.

## <a name="how-toobring-in-your-own-data"></a>**Como toobring em seus próprios dados**
Esta seção descreve como toobring tooAzure seus próprios dados e áreas que exigiria alterações de dados de saudação trazer para essa arquitetura.

É improvável que qualquer conjunto de dados que você coloque corresponderia a saudação de conjunto de dados usado para esse modelo de solução. Noções básicas sobre seus dados e os requisitos serão fundamental como modificar esse modelo toowork com seus próprios dados. Se esse for o primeiro toohello de exposição service de aprendizado de máquina do Azure, você pode obter uma introdução tooit usando o exemplo hello [como toocreate sua primeira experiência](machine-learning/machine-learning-create-experiment.md).

Olá seções a seguir sobre seções de saudação do modelo de saudação que exigem modificações quando um novo conjunto de dados é apresentado.

### <a name="azure-event-hub"></a>Hub de Eventos do Azure
Olá [Hub de eventos do Azure](https://azure.microsoft.com/services/event-hubs/) serviço é muito genérico, de modo que os dados podem ser publicados toohello hub no formato CSV ou JSON. Não há processamento especial ocorre no hello Hub de eventos do Azure, mas é importante que entender dados de saudação são alimentados nele.

Este documento descreve como tooingest seus dados, mas um pode facilmente enviar eventos ou dados tooan Hub de eventos do Azure, usando Olá [API de Hub de eventos](event-hubs/event-hubs-programming-guide.md).

### <a name="azure-stream-analytics"></a>Stream Analytics do Azure
Olá [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) serviço é usado tooprovide próximo a análise em tempo real lendo de fluxos de dados e gerando o número de tooany de dados de fontes.

Para Olá previsão de demanda para o modelo de solução de energia, hello Azure Stream Analytics consulta consiste em duas subconsultas, cada consome eventos de saudação serviço Hub de eventos do Azure como entradas e saídas tootwo distintos locais de ter. Essas saídas são formadas por um conjunto de dados do Power BI e em um local do Armazenamento do Azure.

Olá [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) consulta pode ser encontrada:

* Fazer logon no hello [portal de gerenciamento do Azure](https://manage.windowsazure.com/)
* Localizando trabalhos do stream analytics Olá ![](media/cortana-analytics-technical-guide-demand-forecast/icon-stream-analytics.png) que foram geradas quando Olá solução foi implantada. Uma é para enviar por push o armazenamento tooblob de dados (por exemplo, mytest1streaming432822asablob) e Olá outros uma é para enviar dados tooPower BI (por exemplo, mytest1streaming432822asapbi).
* Seleção

  * ***ENTRADAS*** tooview Olá entrada da consulta
  * ***CONSULTA*** tooview Olá consulta
  * ***GERA*** tooview Olá saídas diferentes

Informações sobre a construção de consulta do Stream Analytics do Azure podem ser encontradas no hello [referência de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) no MSDN.

Nesta solução, Olá trabalho do Stream Analytics do Azure que produz o conjunto de dados com informações de análise em tempo real sobre Olá entrada dados fluxo tooa painel do Power BI quase é fornecido como parte desse modelo de solução. Porque não há conhecimento implícito sobre o formato de dados de entrada de hello, essas consultas precisaria toobe alterado com base no seu formato de dados.

Olá outro trabalho do Stream Analytics do Azure gera todos os [Hub de eventos](https://azure.microsoft.com/services/event-hubs/) eventos [armazenamento do Azure](https://azure.microsoft.com/services/storage/) e, portanto, não requer nenhuma alteração, independentemente de seu formato de dados, como informações de evento completa de saudação são transmitidas toostorage.

### <a name="azure-data-factory"></a>Fábrica de dados do Azure
Olá [do Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) orquestrada pelo serviço movimentação hello e processamento de dados. Em hello previsão de demanda para dados de saudação do modelo de solução de energia fábrica é composta por doze [pipelines](data-factory/data-factory-create-pipelines.md) que mover e processar dados hello usando diversas tecnologias.

  Você pode acessar sua fábrica de dados abrindo o nó de fábrica de dados Olá na parte inferior de saudação do diagrama de modelo de solução Olá criado com a implantação de saudação de solução de saudação. Isso levará você toohello fábrica de dados em seu portal de gerenciamento do Azure. Se você encontrar erros em seus conjuntos de dados, você pode ignorar os conforme forem devido a fábrica toodata que está sendo implantada antes de gerador de dados Olá foi iniciado. Esses erros não impedem o funcionamento do seu data factory.

Esta seção discute Olá necessário [pipelines](data-factory/data-factory-create-pipelines.md) e [atividades](data-factory/data-factory-create-pipelines.md) contidos em Olá [do Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/). Abaixo está o modo de exibição de diagrama de saudação de solução de saudação.

![](media/cortana-analytics-technical-guide-demand-forecast/ADF2.png)

Cinco pipelines de saudação desta fábrica contêm [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts que são usado toopartition e dados agregados de saudação. Quando observado, scripts Olá estará localizados em Olá [armazenamento do Azure](https://azure.microsoft.com/services/storage/) conta criada durante a instalação. A localização deles será: demandforecasting\\\\script\\\\hive\\\\ (ou https://[nome da sua solução].blob.core.windows.net/demandforecasting).

Semelhante toohello [Azure Stream Analytics](#azure-stream-analytics-1) consultas, o [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts tem conhecimento implícito sobre o formato de dados de entrada de saudação, essas consultas precisaria toobe alterado com base em seu formato de dados e [recurso engenharia](machine-learning/machine-learning-feature-selection-and-engineering.md) requisitos.

#### <a name="aggregatedemanddatato1hrpipeline"></a>*AggregateDemandDataTo1HrPipeline*
Isso [pipeline](data-factory/data-factory-create-pipelines.md) pipeline contém uma única atividade - um [HDInsightHive](data-factory/data-factory-hive-activity.md) atividade usando um [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) que executa um [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)Olá tooaggregate de script a cada 10 segundos de dados no nível de região de nível toohourly Subestação demanda de streaming e colocar em [armazenamento do Azure](https://azure.microsoft.com/services/storage/) por meio do trabalho do Stream Analytics do Azure hello.

O script do [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) para essa tarefa de particionamento é ***AggregateDemandRegion1Hr.hql***

#### <a name="loadhistorydemanddatapipeline"></a>*LoadHistoryDemandDataPipeline*
Esse [pipeline](data-factory/data-factory-create-pipelines.md) contém duas atividades:

* [HDInsightHive](data-factory/data-factory-hive-activity.md) atividade usando um [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) que executa um Hive script tooaggregate Olá por hora por demanda dados de histórico no nível de região de nível toohourly Subestação e colocado no armazenamento do Azure durante a saudação do Azure Trabalho do Stream Analytics
* [Cópia](https://msdn.microsoft.com/library/azure/dn835035.aspx) atividade que move Olá dados agregados de armazenamento do Azure blob toohello banco de dados SQL que foi configurado como parte da instalação do modelo de solução de saudação.

Olá [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) script para esta tarefa é ***AggregateDemandHistoryRegion.hql***.

#### <a name="mlscoringregionxpipeline"></a>*MLScoringRegionXPipeline*
Essas [pipelines](data-factory/data-factory-create-pipelines.md) conter várias atividades e cujo resultado final é Olá pontuada de previsões de experiência de aprendizado de máquina do Azure Olá associado a esse modelo de solução. Eles são quase idênticos, exceto pelo fato de cada um deles só trata Olá uma região diferente que está sendo feita por diferente RegionID passado no pipeline ADF hello e script de hive Olá para cada região.  
Olá atividades contidas neste são:

* [HDInsightHive](data-factory/data-factory-hive-activity.md) atividade usando um [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) que executa um Hive script tooperform agregações e recursos de engenharia necessária para Olá experiência de aprendizado de máquina do Azure. Olá scripts de Hive para essa tarefa são respectivos ***PrepareMLInputRegionX.hql***.
* [Cópia](https://msdn.microsoft.com/library/azure/dn835035.aspx) atividade que move os resultados de saudação do hello [HDInsightHive](data-factory/data-factory-hive-activity.md) atividade tooa único armazenamento do Azure blob que pode ser acessado por Olá [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) atividade.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) atividade que chama a experiência de aprendizado de máquina do Azure Olá que resulta em Olá resultados sejam colocadas em um único blob de armazenamento do Azure.

#### <a name="copyscoredresultregionxpipeline"></a>*CopyScoredResultRegionXPipeline*
Essas [pipelines](data-factory/data-factory-create-pipelines.md) contenha uma única atividade - um [cópia](https://msdn.microsoft.com/library/azure/dn835035.aspx) atividade que move os resultados de saudação do hello experiência de aprendizado de máquina do Azure do respectivos de saudação ***MLScoringRegionXPipeline *** toohello banco de dados SQL que foi configurado como parte da instalação do modelo de solução de saudação.

#### <a name="copyaggdemandpipeline"></a>*CopyAggDemandPipeline*
Isso [pipelines](data-factory/data-factory-create-pipelines.md) contenha uma única atividade - um [cópia](https://msdn.microsoft.com/library/azure/dn835035.aspx) atividade que move Olá agregados dados demanda em andamento de ***LoadHistoryDemandDataPipeline*** toohello do Azure Banco de dados SQL que foi configurado como parte da instalação do modelo de solução de saudação.

#### <a name="copyregiondatapipeline-copysubstationdatapipeline-copytopologydatapipeline"></a>*CopyRegionDataPipeline, CopySubstationDataPipeline, CopyTopologyDataPipeline*
Essas [pipelines](data-factory/data-factory-create-pipelines.md) contenha uma única atividade - um [cópia](https://msdn.microsoft.com/library/azure/dn835035.aspx) atividade que move os dados de referência de saudação do Subestação/região/Topologygeo que são carregados tooAzure blob de armazenamento como parte da solução Olá instalação de modelo toohello banco de dados SQL que foi configurado como parte da instalação do modelo de solução de saudação.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Olá [aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/) experimentar usado para este modelo de solução fornece a previsão de saudação de demanda de região. experiência de saudação é consumido de conjunto de dados toohello específico e, portanto, exigirá modificação ou substituição de dados toohello específico que são colocados no.

## <a name="monitor-progress"></a>**Monitorar o progresso**
Quando Olá gerador de dados é iniciado, pipeline hello começa tooget serializado e hello diferentes componentes de sua solução iniciar iniciar em ação comandos a seguir Olá emitidos por Olá fábrica de dados. Há duas maneiras que você pode monitorar o pipeline de saudação.

1. Verifique se os dados de saudação do armazenamento de BLOBs do Azure.

    Um trabalho do Stream Analytics Olá grava Olá entrada dados tooblob um armazenamento bruto. Se você clicar em **armazenamento de BLOBs do Azure** componente da sua solução Olá tela você solução Olá implantado com êxito e, em seguida, clique em **abrir** no painel direito da saudação, levará toohello [Portal de gerenciamento do azure](https://portal.azure.com). Uma vez lá, clique em **Blobs**. No painel de Avançar hello, você verá uma lista de contêineres. Clique em **"energysadata"**. No painel de Avançar hello, você verá Olá **"demandongoing"** pasta. Pasta de dados brutos hello, você verá pastas com nomes como data = 2016-01-28 etc. Se você ver essas pastas, indica que dados brutos de saudação são com êxito sendo gerados no seu computador e armazenados no armazenamento de blob. Você deverá ver arquivos com tamanhos finitos em MB nessas pastas.
2. Verifique se os dados de saudação do banco de dados do SQL Azure.

    Olá última etapa do pipeline de saudação é toowrite dados (por exemplo, as previsões do aprendizado de máquina) no banco de dados SQL. Você pode ter toowait um máximo de 2 horas para Olá dados tooappear no banco de dados do SQL. Uma maneira toomonitor a quantidade de dados está disponível no banco de dados SQL é por meio de [portal de gerenciamento do Azure](https://manage.windowsazure.com/). No painel esquerdo do hello Localize bancos de dados SQL![](media/cortana-analytics-technical-guide-demand-forecast/SQLicon2.png) e clique nele. Em seguida, localize seu banco de dados (ou seja, demo123456db) e clique nele. Na próxima página Olá em **"Conectar tooyour database"** seção, clique em **"Consultas de execução Transact-SQL no banco de dados SQL"**.

    Aqui, você pode clicar em nova consulta e consultar Olá número de linhas (por exemplo, "select count(*) de DemandRealHourly)" como seu banco de dados cresce, Olá número de linhas na tabela de saudação aumentará.)
3. Verifique se os dados de saudação do painel do Power BI.

    Você pode configurar o Power BI afunilamento painel toomonitor Olá entrados dados brutos. Siga a instrução Olá Olá seção "Painel do Power BI".

## <a name="power-bi-dashboard"></a>**Painel do Power BI**
### <a name="overview"></a>Visão geral
Esta seção descreve como tooset o Power BI painel toovisualize seus dados em tempo real do Azure fluxo analytics (afunilamento), como previsão bem como resultados de aprendizado de máquina do Azure (caminho frio).

### <a name="setup-hot-path-dashboard"></a>Configurar o painel de afunilamento
Olá etapas a seguir irá guiá-lo como toovisualize em tempo real de saída de dados de análise de fluxo de trabalhos que foram gerados em tempo de saudação da implantação da solução. Um [Power BI online](http://www.powerbi.com/) conta é necessário tooperform Olá etapas a seguir. Se não tiver uma conta, você poderá [criar uma](https://powerbi.microsoft.com/pricing).

1. Adicione a saída do Power BI ao Stream Analytics (ASA).

   * Você precisará de instruções Olá toofollow [Stream Analytics do Azure e Power BI: um painel de análise em tempo real para visibilidade em tempo real do fluxo de dados](stream-analytics/stream-analytics-power-bi-dashboard.md) tooset a saída de saudação do seu trabalho do Stream Analytics do Azure como a potência Painel BI.
   * Localize o trabalho do stream analytics Olá no seu [portal de gerenciamento do Azure](https://manage.windowsazure.com). nome de saudação do trabalho Olá deve ser: YourSolutionName + streamingjob"" + o número aleatório + "asapbi" (ou seja, demostreamingjob123456asapbi).
   * Adicione uma saída do Power BI para o trabalho ASA hello. Saudação de conjunto **Alias de saída** como **'PBIoutput'**. Defina o **Nome do Conjunto de Dados** e o **Nome da Tabela** como **‘EnergyStreamData’**. Depois que você adicionou a saída de hello, clique em **"Iniciar"** na parte inferior de saudação do trabalho do Stream Analytics do hello página toostart Olá. Você deverá receber uma mensagem de confirmação (*por exemplo*, "Iniciando o trabalho do stream analytics myteststreamingjob12345asablob com êxito").
2. Faça logon no muito[online para o Power BI](http://www.powerbi.com)

   * Em Olá seção de conjuntos de dados do painel da esquerda no meu espaço de trabalho, você deve ser capaz de toosee um novo mostrando de conjunto de dados no painel esquerdo de saudação do Power BI. Isso é hello fluxo de dados que enviados por push do Azure Stream Analytics na etapa anterior hello.
   * Verifique se Olá ***visualizações*** painel está aberto e é exibido no lado direito da tela hello.
3. Crie hello "Demanda pelo carimbo de hora" lado a lado:

   * Clique em conjunto de dados **'EnergyStreamData'** em Olá seção de conjuntos de dados do painel da esquerda.
   * Clique no ícone **"Gráfico de Linhas"**![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic8.png).
   * Clique em 'EnergyStreamData' no painel **Campos** .
   * Clique em **“Timestamp”** e verifique se isso é exibido em "Eixo". Clique em **"Carregar"** e verifique se isso é exibido em "Valores".
   * Clique em **salvar** Olá superior e nome do relatório de saudação como "EnergyStreamDataReport". relatório de saudação denominado "EnergyStreamDataReport" será mostrado na seção de relatórios no painel de navegação da saudação esquerda.
   * Clique em **"Pin Visual"** ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) ícone no canto superior direito do gráfico de linhas, uma janela de "Pin tooDashboard" poderá aparecer para você toochoose um painel. Selecione "EnergyStreamDataReport" e clique em "Fixar".
   * Passe o mouse Olá sobre esse bloco no painel de saudação, clique em "Editar" ícone no canto superior direito toochange seu título como "Demanda pelo carimbo de hora"
4. Crie outros blocos de painel com base em conjuntos de dados apropriados. Olá final de exibição de painel é mostrado abaixo.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PBIFullScreen.png)

### <a name="setup-cold-path-dashboard"></a>Configurar o painel de caminho frio
No pipeline de dados frios caminho, a saudação principal objetivo é previsão de demanda de saudação do tooget de cada região. Power BI se conecta a banco de dados do SQL Azure tooan como sua fonte de dados, onde os resultados da previsão Olá são armazenados.

> [!NOTE]
> 1) Levará alguns toocollect de horas resultados de previsão suficiente para o painel de saudação. Recomendamos que você inicia esse processo 2 a 3 horas depois almoçar gerador de dados hello. 2) nessa etapa, pré-requisito Olá é toodownload e instale o software livre de saudação [Power BI desktop](https://powerbi.microsoft.com/desktop).
>
>

1. Obtenha as credenciais de banco de dados de saudação.

   Você precisará **nome do servidor, o nome do banco de dados, o nome de usuário e senha de banco de dados** antes de mover toonext etapas. Aqui estão Olá etapas tooguide você como toofind-los.

   * Quando **"Banco de Dados SQL do Azure"** ficar verde no diagrama do modelo da solução, clique nele e em **"Abrir"**. Você será guiado tooAzure portal de gerenciamento e a página de informações do banco de dados será aberta também.
   * Na página de saudação, você pode encontrar uma seção de "Database". Ele lista o banco de dados de saudação que você criou. nome de saudação do seu banco de dados deve ser **"O nome da solução + número aleatório + 'db'"** (por exemplo, "mytest12345db").
   * Clique em seu banco de dados, em Olá novo que pop-out do painel, você pode encontrar o nome do seu servidor de banco de dados na parte superior da saudação. O nome do servidor de banco de dados deve ser **“Nome da Solução + Número Aleatório + 'database.windows.net,1433'”** (por exemplo, “mytest12345.database.windows.net,1433”).
   * O banco de dados **nome de usuário** e **senha** são Olá mesmo Olá nome de usuário e senha registrada anteriormente durante a implantação da solução de saudação.
2. Atualizar fonte de dados de saudação do caminho de frios Olá arquivo do Power BI

   * Verifique se você instalou a versão mais recente de saudação do [Power BI desktop](https://powerbi.microsoft.com/desktop).
   * Em Olá **"DemandForecastingDataGeneratorv1.0"** pasta baixado, clique duas vezes em Olá **'Power BI Template\DemandForecastPowerBI.pbix'** arquivo. visualizações de saudação inicial se baseiam em dados fictícios. **Observação:** se você vir um erro manipulá, verifique se você instalou a versão mais recente de saudação do Power BI Desktop.

     Quando você abri-lo, na parte superior de saudação do arquivo hello, clique em **editar consultas**. Olá pop-out da janela, clique duas vezes em **'Source'** no painel à direita da saudação.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic1.png)
   * Olá pop-out de janela, substitua **"Server"** e **"Database"** com seus próprios nomes de servidor e banco de dados e clique **"Okey"**. Para o nome do servidor, certifique-se de especificar a porta 1433 hello (**YourSolutionName.database.windows.net, 1433**). Ignore mensagens de aviso de saudação que aparecem na tela hello.
   * No pop-Olá próxima janela, você verá duas opções no painel esquerdo da saudação (**Windows** e **banco de dados**). Clique em **"Database"**, preencha o **"Username"** e **"Senha"** (Olá nome de usuário e a senha inseridas quando você primeiro implantou solução hello e criado um Azure SQL database). Em ***selecione qual nível tooapply essas configurações***, marque a opção de nível de banco de dados. Clique em **"Conectar"**.
   * Uma vez página anterior toohello back interativa, feche a janela de saudação. Será exibida uma mensagem - clique em **Aplicar**. Por fim, clique em Olá **salvar** botão toosave alterações de saudação. O arquivo do Power BI agora estabeleceu servidor toohello de conexão. Se suas visualizações estiverem vazias, verifique se que você limpar todos os dados de saudação seleções Olá em Olá visualizações toovisualize Olá borracha ícone no canto superior direito de saudação de legendas de saudação. Use Olá atualização botão tooreflect novos dados em visualizações de saudação. Inicialmente, você só verá Olá semente dados em suas visualizações como fábrica de dados Olá é agendado toorefresh cada três horas. Depois de 3 horas, você verá novas previsões refletidas nas visualizações, quando você atualizar os dados de saudação.
3. (Opcional) Publicar o painel do caminho frios Olá muito[Power BI online](http://www.powerbi.com/). Observe que esta etapa precisa de uma conta do Power BI (ou de uma conta do Office 365).

   * Clique em **"Publicar"** e depois de alguns minutos uma janela aparece exibindo "Publicando tooPower BI sucesso!" com uma marca de seleção verde. Clique o link da saudação abaixo "Demoprediction.pbix abrir no Power BI". toofind obter instruções, consulte [publicar por meio do Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * toocreate um novo painel: clique Olá  **+**  entrar próximo toothe **painéis** seção no painel esquerdo da saudação. Insira o nome de hello "Demonstração de previsão de demanda" para esse novo painel.
   * Depois de abrir o relatório de saudação, clique em ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) toopin todas as visualizações tooyour painel. toofind obter instruções, consulte [fixar um painel do Power BI de tooa lado a lado de um relatório](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     Acesse a página do painel toohello e ajustar o tamanho de saudação e o local de suas visualizações e editar seus títulos. toofind instruções detalhadas sobre como tooedit seus blocos, consulte [editar um bloco, redimensionar, mover, renomear, fixar, excluir, Adicionar hiperlink](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Aqui está um exemplo de painel com alguns tooit de visualizações fixadas caminho frios.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic7.png)
4. (Opcional) Agendar atualização Olá da fonte de dados.

   * tooschedule atualização de dados hello, passe o mouse sobre Olá **EnergyBPI Final** conjunto de dados, clique em ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic3.png) e, em seguida, escolha **agendar atualização**.
     **Observação:** se você vir Massagem um aviso, clique em **Editar credenciais** e verifique se suas credenciais de banco de dados são Olá mesmo daqueles descritos na etapa 1.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic4.png)
   * Expanda Olá **agendar atualização** seção. Ative "manter os dados atualizados".
   * Agendar a atualização de saudação com base em suas necessidades. toofind obter mais informações, consulte [de atualização de dados no Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/).

## <a name="how-toodelete-your-solution"></a>**Como toodelete sua solução**
Certifique-se de que você interrompa o gerador de dados hello quando usando ativamente a solução de saudação como executar gerador de dados Olá incorrerá em custos mais altos. Exclua solução Olá se não estiver usando. A exclusão de sua solução excluirá todos os componentes de saudação provisionados em sua assinatura quando você implantou a solução de saudação. solução de saudação do toodelete clique em seu nome da solução no painel esquerdo de saudação do modelo de solução de saudação e clique em Excluir.

## <a name="cost-estimation-tools"></a>**Ferramentas de estimativa de custo**
Olá duas ferramentas a seguir estão disponível toohelp você entender melhor os custos totais envolvido na execução Olá previsão de demanda para o modelo de solução de energia em sua assinatura:

* [Ferramenta Calculadora de Preço do Microsoft Azure (online)](https://azure.microsoft.com/pricing/calculator/)
* [Ferramenta Calculadora de Preço do Microsoft Azure (área de trabalho)](http://www.microsoft.com/download/details.aspx?id=43376)

## <a name="acknowledgements"></a>**Confirmações**
Este artigo foi escrito pelo cientista de dados Yijing Chen e pelo engenheiro de software Qiu Min da Microsoft.
