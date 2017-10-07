---
title: "manutenção de aaaPredictive em aeroespacial com o Azure - guia técnico de solução de inteligência Cortana | Microsoft Docs"
description: "Um guia técnico toohello modelo de solução com o Microsoft Cortana inteligência para manutenção preditiva aeroespacial, utilitários e transporte."
services: cortana-analytics
documentationcenter: 
author: fboylu
manager: jhubbard
editor: cgronlun
ms.assetid: 2c4d2147-0f05-4705-8748-9527c2c1f033
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: fboylu
ms.openlocfilehash: 30ddc1c101007546ae1b303bccebae3ecdacb442
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-predictive-maintenance-in-aerospace-and-other-businesses"></a>Guia técnico toohello Cortana modelo de solução de inteligência para manutenção preditiva aeroespacial e outras empresas

## <a name="important"></a>**Importante**
Este artigo foi preterido. informações de saudação são toohello ainda relevantes problema em questão, ou seja, a manutenção preditiva em aeroespacial, mas artigo mais recente da saudação com hello mais as informações de toodate pode ser encontrado [aqui](https://github.com/Azure/cortana-intelligence-predictive-maintenance-aerospace). 

## <a name="acknowledgements"></a>**Confirmações**
Este artigo foi autorizado pelos cientistas de dados Yan Zhang, Gauher Shaheen, Fidan Boylu Uz e o engenheiro de software Dan Grecoe da Microsoft.

## <a name="overview"></a>**Visão geral**
Modelos de solução são projetados tooaccelerate processo de saudação da criação de uma demonstração E2E sobre o pacote de inteligência do Cortana. Um modelo implantado provisionará sua assinatura com os componentes necessários do Cortana inteligência e criar relações de saudação entre eles. Ele também sementes de pipeline de saudação de dados com dados de exemplo gerados a partir de um aplicativo de gerador de dados que você baixar e instalar em seu computador local depois de implantar o modelo de solução de saudação. dados Olá gerados a partir de gerador de saudação serão alimentar pipeline de dados hello e iniciar a geração de previsões de aprendizado de máquina que, em seguida, podem ser visualizados no painel do Power BI hello. o processo de implantação Olá orientará tooset de várias etapas as credenciais de sua solução. Certifique-se de que registrar essas credenciais como nome da solução, o nome de usuário e a senha fornecidos durante a implantação de saudação.  

meta de saudação deste documento é arquitetura de referência tooexplain hello e diferentes componentes provisionados em sua assinatura como parte desse modelo de solução. documento de saudação também fala sobre como tooreplace os dados de exemplo com dados reais de seus próprios toobe toosee capaz de ideias e previsões de seus próprios dados. Além disso, o documento de saudação discute as partes da saudação modelo de solução que seria necessário toobe modificado se você quisesse solução de saudação toocustomize com seus próprios dados. São fornecidas instruções sobre como toobuild hello o painel do Power BI para este modelo de solução final hello.

> [!TIP]
> Você pode baixar e imprimir uma [versão em PDF deste documento](http://download.microsoft.com/download/F/4/D/F4D7D208-D080-42ED-8813-6030D23329E9/cortana-analytics-technical-guide-predictive-maintenance.pdf).
> 
> 

## <a name="big-picture"></a>**Visão global**
![Arquitetura de manutenção preditiva](media/cortana-analytics-technical-guide-predictive-maintenance/predictive-maintenance-architecture.png)

Quando Olá solução for implantada, vários serviços do Azure no Cortana Analytics Suite são ativados (*ou seja,* o Hub de Eventos, o Stream Analytics, o HDInsight, o Data Factory, o Machine Learning, *etc.*). diagrama de arquitetura de saudação acima mostra, em um nível alto, como Olá manutenção preditiva para o modelo de solução aeroespacial é construída de ponta a ponta. Você será capaz de tooinvestigate esses serviços no portal de saudação do azure clicando no diagrama de modelo de solução Olá criado com a implantação de saudação da solução Olá com exceção de saudação do HDInsight como esse serviço é provisionado sob demanda quando Olá relacionados atividades do pipeline são toorun necessária e excluídos posteriormente.
Você pode baixar um [versão em tamanho normal do diagrama Olá](http://download.microsoft.com/download/1/9/B/19B815F0-D1B0-4F67-AED3-A40544225FD1/ca-topologies-maintenance-prediction.png).

Olá seções a seguir descreve cada parte.

## <a name="data-source-and-ingestion"></a>**Fonte de dados e ingestão**
### <a name="synthetic-data-source"></a>Fonte de dados sintética
Fonte usada é gerado para esses dados de saudação do modelo de um aplicativo de área de trabalho que você irá baixar e executar localmente após a implantação bem-sucedida. Você encontrará toodownload de instruções hello e instalar este aplicativo na barra de propriedades hello quando você seleciona o primeiro nó de saudação chamado previsão gerador de dados de manutenção no diagrama de modelo de solução de saudação. Este aplicativo feeds Olá [Hub de eventos do Azure](#azure-event-hub) serviço com pontos de dados ou eventos, que serão usados no restante de saudação do fluxo de solução de saudação. Esta fonte de dados é composta por ou derivada de dados publicamente disponíveis do [repositório de dados da NASA](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/) usando Olá [o conjunto de dados de simulação do Turbofan mecanismo degradação](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan).

aplicativo de geração de eventos Hello populará hello Azure Hub de eventos apenas enquanto ele está em execução no seu computador.

### <a name="azure-event-hub"></a>Hub de Eventos do Azure
Olá [Hub de eventos do Azure](https://azure.microsoft.com/services/event-hubs/) service é o destinatário de saudação de entrada hello fornecido pelo Olá sintética fonte de dados descrito acima.

## <a name="data-preparation-and-analysis"></a>**Preparação e análise de dados**
### <a name="azure-stream-analytics"></a>Stream Analytics do Azure
Olá [Stream Analytics do Azure](https://azure.microsoft.com/services/stream-analytics/) service é usado tooprovide próximo a análise em tempo real no fluxo de entrada de saudação do hello [Hub de eventos do Azure](#azure-event-hub) de serviço e publicar os resultados em um [doPowerBI](https://powerbi.microsoft.com) dashboard, bem como arquivamento todos bruto toohello de eventos de entrada [armazenamento do Azure](https://azure.microsoft.com/services/storage/) serviço para processamento posterior por Olá [do Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) serviço.

### <a name="hd-insights-custom-aggregation"></a>Agregação personalizada do HDInsight
Olá serviço Azure HD Insight é usado toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts (gerenciados pelo Azure Data Factory) tooprovide agregações em eventos brutos Olá foram arquivados usando o serviço do Azure Stream Analytics hello.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Olá [aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/) serviço é usado (orquestrada pelo Azure Data Factory) toomake previsões em Olá restantes (regra) de vida útil de um mecanismo de aeronave específico Olá entrada recebidas.

## <a name="data-publishing"></a>**Publicação de dados**
### <a name="azure-sql-database-service"></a>Serviço Banco de Dados SQL do Azure
Olá [banco de dados do SQL Azure](https://azure.microsoft.com/services/sql-database/) service é previsões de saudação toostore usado (gerenciado pelo Azure Data Factory) recebidas por Olá service de aprendizado de máquina do Azure que será consumido no hello [Power BI](https://powerbi.microsoft.com) painel.

## <a name="data-consumption"></a>**Consumo de dados**
### <a name="power-bi"></a>Power BI
Olá [Power BI](https://powerbi.microsoft.com) service é usado tooshow um painel que contém as agregações e alertas fornecidas pelo Olá [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) serviço, bem como as previsões de regra armazenados em [SQL Azure Banco de dados](https://azure.microsoft.com/services/sql-database/) que foram produzidas usando Olá [aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/) serviço. Para obter instruções sobre como toobuild hello o painel do Power BI para este modelo de solução, consulte a seção de toohello abaixo.

## <a name="how-toobring-in-your-own-data"></a>**Como toobring em seus próprios dados**
Esta seção descreve como toobring tooAzure seus próprios dados e áreas que exigiria alterações de dados de saudação trazer para essa arquitetura.

É improvável que qualquer conjunto de dados que você coloque corresponderia a saudação de conjunto de dados usado pelo Olá [o conjunto de dados de simulação do Turbofan mecanismo degradação](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan) usado para esse modelo de solução. Noções básicas sobre seus dados e os requisitos serão fundamental como modificar esse modelo toowork com seus próprios dados. Se esse for o primeiro toohello de exposição service de aprendizado de máquina do Azure, você pode obter uma introdução tooit usando o exemplo hello [como toocreate sua primeira experiência](machine-learning-create-experiment.md).

Olá seções a seguir sobre seções de saudação do modelo de saudação que exigem modificações quando um novo conjunto de dados é apresentado.

### <a name="azure-event-hub"></a>Hub de Eventos do Azure
Olá serviço Hub de eventos do Azure é muito genérico, de modo que os dados podem ser publicados toohello hub no formato CSV ou JSON. Não há processamento especial ocorre em Olá Hub de eventos do Azure, mas é importante entender dados de saudação são alimentados nele.

Este documento descreve como tooingest seus dados, mas você pode facilmente enviar eventos ou dados tooan Hub de eventos do Azure usando Olá da API do Hub de eventos.

### <a name="azure-stream-analytics"></a>Stream Analytics do Azure
Olá serviço Azure Stream Analytics é usado tooprovide próximo a análise em tempo real lendo de fluxos de dados e gerando o número de tooany de dados de fontes.

Para Olá manutenção preditiva para o modelo de solução aeroespacial, a consulta do Stream Analytics do Azure consiste em quatro subconsultas, cada consumir eventos de saudação serviço Hub de eventos do Azure e ter saídas em quatro locais distintos. Essas saídas consistem em três conjuntos de dados do Power BI e em um local do Armazenamento do Azure.

consulta do Stream Analytics do Azure Olá pode ser encontrada:

* Fazer logon no portal do Azure de saudação
* Localizando trabalhos do Stream Analytics Olá ![ícone de análise de fluxo](media/cortana-analytics-technical-guide-predictive-maintenance/icon-stream-analytics.png) que foram gerados quando a implantação da solução hello (*, por exemplo,*, **maintenancesa02asapbi** e **maintenancesa02asablob** para a solução de manutenção preditiva)
* Seleção
  
  * ***ENTRADAS*** tooview Olá entrada da consulta
  * ***CONSULTA*** tooview Olá consulta
  * ***GERA*** tooview Olá saídas diferentes

Informações sobre a construção de consulta do Stream Analytics do Azure podem ser encontradas no hello [referência de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) no MSDN.

Nesta solução, consultas de saudação saída três conjuntos de dados com informações de análise em tempo real sobre Olá entrada dados fluxo tooa painel do Power BI que é fornecido como parte desse modelo de solução quase. Porque não há conhecimento implícito sobre o formato de dados de entrada de hello, essas consultas precisaria toobe alterado com base no seu formato de dados.

consulta Olá no trabalho do Stream Analytics da segunda Olá **maintenancesa02asablob** simplesmente gera todos os [Hub de eventos](https://azure.microsoft.com/services/event-hubs/) eventos [armazenamento do Azure](https://azure.microsoft.com/services/storage/) e, portanto, não requer nenhuma alteração independentemente de seu formato de dados como Olá informações de evento completa são transmitidas toostorage.

### <a name="azure-data-factory"></a>Fábrica de dados do Azure
Olá [do Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) orquestrada pelo serviço movimentação hello e processamento de dados. Em manutenção preditiva para dados de saudação do modelo de solução da fábrica é composta de três [pipelines](../data-factory/data-factory-create-pipelines.md) que mover e processar dados hello usando diversas tecnologias.  Você pode acessar sua fábrica de dados abrindo o nó de fábrica de dados Olá Olá na parte inferior de saudação do diagrama de modelo de solução Olá criado com a implantação de saudação de solução de saudação. Isso levará você toohello fábrica de dados em seu portal do Azure. Se você encontrar erros em seus conjuntos de dados, você pode ignorar os conforme forem devido a fábrica toodata que está sendo implantada antes de gerador de dados Olá foi iniciado. Esses erros não impedem o funcionamento do seu data factory.

![Erros do conjunto de dados do Data Factory](media/cortana-analytics-technical-guide-predictive-maintenance/data-factory-dataset-error.png)

Esta seção discute Olá necessário [pipelines](../data-factory/data-factory-create-pipelines.md) e [atividades](../data-factory/data-factory-create-pipelines.md) contidos em Olá [do Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/). Abaixo está o modo de exibição de diagrama de saudação de solução de saudação.

![Fábrica de dados do Azure](media/cortana-analytics-technical-guide-predictive-maintenance/azure-data-factory.png)

Dois pipelines de saudação desta fábrica contêm [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts que são usado toopartition e dados agregados de saudação. Quando observado, scripts Olá estará localizados em Olá [armazenamento do Azure](https://azure.microsoft.com/services/storage/) conta criada durante a instalação. A localização deles será: maintenancesascript\\\\script\\\\hive\\\\ (ou https://[nome da solução].blob.core.windows.net/maintenancesascript).

Semelhante toohello [Azure Stream Analytics](#azure-stream-analytics-1) consultas, o [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) scripts tem conhecimento implícito sobre o formato de dados de entrada de saudação, essas consultas precisaria toobe alterado com base em seu formato de dados e [recurso engenharia](machine-learning-feature-selection-and-engineering.md) requisitos.

#### <a name="aggregateflightinfopipeline"></a>*AggregateFlightInfoPipeline*
Isso [pipeline](../data-factory/data-factory-create-pipelines.md) contém uma única atividade - um [HDInsightHive](../data-factory/data-factory-hive-activity.md) atividade usando um [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) que executa um [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) Coloque os dados de saudação do script toopartition [armazenamento do Azure](https://azure.microsoft.com/services/storage/) durante o [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) trabalho.

O script do [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) para essa tarefa de particionamento é ***AggregateFlightInfo.hql***

#### <a name="mlscoringpipeline"></a>*MLScoringPipeline*
Isso [pipeline](../data-factory/data-factory-create-pipelines.md) contém várias atividades e cujo resultado final é Olá pontuada de previsões de saudação [aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/) experimento associado a esse modelo de solução.

Olá atividades contidas neste são:

* [HDInsightHive](../data-factory/data-factory-hive-activity.md) atividade usando um [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) que executa um [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) tooperform agregações de script e recursos de engenharia necessária para Olá [Azure Aprendizado de máquina](https://azure.microsoft.com/services/machine-learning/) experiências.
  O script do [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) para essa tarefa de particionamento é ***PrepareMLInput.hql***.
* [Cópia](https://msdn.microsoft.com/library/azure/dn835035.aspx) atividade que move os resultados de saudação do [HDInsightHive](../data-factory/data-factory-hive-activity.md) tooa de atividade único [armazenamento do Azure](https://azure.microsoft.com/services/storage/) blob que pode ser acessado pelo [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) atividade.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) atividade que chama Olá [aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/) experimento que resulta em resultados de saudação sejam colocados em um único [armazenamento do Azure](https://azure.microsoft.com/services/storage/) blob.

#### <a name="copyscoredresultpipeline"></a>*CopyScoredResultPipeline*
Isso [pipeline](../data-factory/data-factory-create-pipelines.md) contém uma única atividade - um [cópia](https://msdn.microsoft.com/library/azure/dn835035.aspx) atividade que move os resultados de saudação do hello [aprendizado de máquina do Azure](#azure-machine-learning) experiências do *** MLScoringPipeline*** toohello [banco de dados do SQL Azure](https://azure.microsoft.com/services/sql-database/) que foi provisionado como parte da instalação do modelo de solução.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Olá [aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/) experimento usado para este modelo de solução fornece Olá restantes útil vida (regra) de um mecanismo de aeronave. experiência de saudação é consumido de conjunto de dados toohello específico e, portanto, exigirá modificação ou substituição de dados toohello específico que são colocados no.

Para obter informações sobre como Olá experiência de aprendizado de máquina do Azure foi criada, consulte [manutenção preditiva: etapa 1 de 3, preparação de dados e de engenharia de recurso](http://gallery.cortanaanalytics.com/Experiment/Predictive-Maintenance-Step-1-of-3-data-preparation-and-feature-engineering-2).

## <a name="monitor-progress"></a>**Monitorar o progresso**
 Quando Olá gerador de dados é iniciado, pipeline hello começa tooget serializado e hello diferentes componentes de sua solução iniciar iniciar em ação comandos a seguir Olá emitidos por Olá fábrica de dados. Há duas maneiras que você pode monitorar o pipeline de saudação.

1. Um trabalho do Stream Analytics Olá grava Olá entrada dados tooblob um armazenamento bruto. Se você clicar no componente de armazenamento de Blob de sua solução de tela hello você solução Olá implantado com êxito e, em seguida, clique em Abrir no painel direito da saudação, levará você toohello [portal de gerenciamento](https://portal.azure.com/). No portal, clique em Blobs. No painel de Avançar hello, você verá uma lista de contêineres. Clique em **maintenancesadata**. No painel de Avançar hello, você verá Olá **rawdata** pasta. Pasta de dados brutos hello, você verá pastas com nomes como hora = 17, horas = 18 etc. Se você ver essas pastas, indica que dados brutos de saudação são com êxito sendo gerados no seu computador e armazenados no armazenamento de blob. Você deve ver arquivos csv que devem ter tamanhos finitos em MB nessas pastas.
2. Olá última etapa do pipeline de saudação é toowrite dados (por exemplo, as previsões do aprendizado de máquina) no banco de dados SQL. Você pode ter toowait um máximo de três horas para Olá dados tooappear no banco de dados do SQL. Uma maneira toomonitor a quantidade de dados está disponível no banco de dados SQL é por meio de [portal do azure](https://manage.windowsazure.com/). No painel esquerdo do hello Localize bancos de dados SQL ![ícone SQL](media/cortana-analytics-technical-guide-predictive-maintenance/icon-SQL-databases.png) e clique nele. Em seguida, localize o banco de dados **pmaintenancedb** e clique nele. Na próxima página na parte inferior do Olá Olá, clique em gerenciar
   
    ![Ícone Gerenciar](media/cortana-analytics-technical-guide-predictive-maintenance/icon-manage.png).
   
    Aqui, você pode clicar em nova consulta e consultar Olá número de linhas (por exemplo, selecione count(*) de PMResult). À medida que o banco de dados cresce, o número de saudação de linhas na tabela de saudação aumentará.

## <a name="power-bi-dashboard"></a>**Painel do Power BI**
### <a name="overview"></a>Visão geral
Esta seção descreve como tooset o Power BI painel toovisualize seus dados em tempo real do Azure Stream Analytics (afunilamento), bem como a previsão de lote os resultados de aprendizado de máquina do Azure (caminho frio).

### <a name="setup-cold-path-dashboard"></a>Painel de caminho frio de instalação
No pipeline de dados frios caminho hello, meta essencial Olá é tooget a regra de previsão (vida útil restante) de cada mecanismo aeronave após a conclusão de um voo (ciclo). resultado da previsão Olá é atualizado a cada três horas para prever os mecanismos de aeronave Olá terminar um voo durante a saudação últimos 3 horas.

Power BI se conecta o banco de dados do SQL Azure tooan como sua fonte de dados, onde são armazenados os resultados de previsão. Observação: 1) ao implantar sua solução, uma previsão real será exibido no banco de dados de saudação em 3 horas.
arquivo pbix Olá que acompanha o download do gerador de saudação contém alguns dados de propagação para que você pode criar o painel do Power BI Olá imediatamente. 2) nessa etapa, pré-requisito Olá é toodownload e instale o software livre de saudação [Power BI desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/).

Olá etapas a seguir irá guiá-lo no como de arquivos tooconnect pbix de saudação à saudação do banco de dados do SQL era lançado em tempo de saudação de implantação de solução que contém dados (*, por exemplo,*. resultados da previsão) para visualização.

1. Obtenha as credenciais de banco de dados de saudação.
   
   Você precisará **nome do servidor, o nome do banco de dados, o nome de usuário e senha de banco de dados** antes de mover toonext etapas. Aqui estão Olá etapas tooguide você como toofind-los.
   
   * Quando **'Banco de Dados SQL do Azure'** ficar verde no diagrama do modelo da solução, clique nele e em **'Abrir'**.
   * Você verá uma nova guia/janela do navegador que exibe o saudação página do portal do Azure. Clique em **'Grupos de recursos'** no painel esquerdo da saudação.
   * Selecionar assinatura Olá que você está usando para implantar a solução hello e, em seguida, selecione **' YourSolutionName\_ResourceGroup'**.
   * No pop-novo Olá out painel, clique em Olá ![ícone SQL](media/cortana-analytics-technical-guide-predictive-maintenance/icon-sql.png) tooaccess ícone seu banco de dados. O nome do banco de dados está próximo toohello esse ícone (*, por exemplo,*, **'pmaintenancedb'**) e hello **nome do servidor de banco de dados** está listada na propriedade de nome do servidor de saudação e deve ser semelhante muito**YourSoutionName.database.windows.net**.
   * O banco de dados **nome de usuário** e **senha** são Olá mesmo Olá nome de usuário e senha registrada anteriormente durante a implantação da solução de saudação.
2. Atualize a fonte de dados de saudação do arquivo de relatório de caminho frios Olá com o Power BI Desktop.
   
   * Na pasta de saudação em seu computador onde você baixou e descompactou o gerador de arquivo, clique duas vezes o **PowerBI\\PredictiveMaintenanceAerospace.pbix** arquivo. Se você vir as mensagens de aviso quando você abrir o arquivo hello, ignorá-las. Na parte superior de saudação do arquivo hello, clique em **editar consultas**.
     
     ![Editar Consultas](media/cortana-analytics-technical-guide-predictive-maintenance/edit-queries.png)
   * Você verá duas tabelas, **RemainingUsefulLife** e **PMResult**. Selecione Olá primeira tabela e clique em ![ícone de configurações de consulta](media/cortana-analytics-technical-guide-predictive-maintenance/icon-query-settings.png) Avançar muito**'Source'** em **'Etapas aplicadas'** em Olá direito **'Configurações de consulta'**painel. Ignore as mensagens de aviso que aparecerem.
   * Olá pop-out de janela, substitua **'Server'** e **'Database'** com seus próprios nomes de servidor e banco de dados e clique **'Okey'**. Para o nome do servidor, certifique-se de especificar a porta 1433 hello (**YourSoutionName.database.windows.net, 1433**). Deixe o campo de banco de dados hello como **pmaintenancedb**. Ignore mensagens de aviso de saudação que aparecem na tela hello.
   * No pop-Olá próxima janela, você verá duas opções no painel esquerdo da saudação (**Windows** e **banco de dados**). Clique em **'Database'**, preencha o **'Username'** e **'Senha'** (Olá nome de usuário e a senha inseridas quando você primeiro implantou solução hello e criado um Azure SQL database). Em ***selecione qual nível tooapply essas configurações***, marque a opção de nível de banco de dados. Clique em **'Conectar'**.
   * Clique na segunda tabela de saudação **PMResult** , em seguida, clique em ![ícone de navegação](media/cortana-analytics-technical-guide-predictive-maintenance/icon-navigation.png) Avançar muito**'Source'** em **'Etapas aplicadas'** em saudação à direita **'Configurações de consulta'** do painel e atualize o servidor de saudação e nomes de banco de dados como Olá acima etapas e clique Okey.
   * Uma vez página anterior toohello back interativa, feche a janela de saudação. Será exibida uma mensagem - clique em **Aplicar**. Por fim, clique em Olá **salvar** botão toosave alterações de saudação. O arquivo do Power BI agora estabeleceu servidor toohello de conexão. Se suas visualizações estiverem vazias, verifique se que você limpar todos os dados de saudação seleções Olá em Olá visualizações toovisualize Olá borracha ícone no canto superior direito de saudação de legendas de saudação. Use Olá atualização botão tooreflect novos dados em visualizações de saudação. Inicialmente, você só verá Olá semente dados em suas visualizações como fábrica de dados Olá é agendado toorefresh cada três horas. Depois de 3 horas, você verá novas previsões refletidas nas visualizações, quando você atualizar os dados de saudação.
3. (Opcional) Publicar o painel do caminho frios Olá muito[Power BI online](http://www.powerbi.com/). Observe que esta etapa precisa de uma conta do Power BI (ou de uma conta do Office 365).
   
   * Clique em **'Publicar'** e depois de alguns minutos uma janela aparece exibindo "Publicando tooPower BI sucesso!" com uma marca de seleção verde. Clique o link da saudação abaixo "Abrir PredictiveMaintenanceAerospace.pbix no Power BI". toofind obter instruções, consulte [publicar por meio do Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * toocreate um novo painel: clique Olá  **+**  entrar próximo toothe **painéis** seção no painel esquerdo da saudação. Insira o nome de hello "Demonstração de manutenção preditiva" para esse novo painel.
   * Depois de abrir o relatório de saudação, clique em ![ícone de PINO](media/cortana-analytics-technical-guide-predictive-maintenance/icon-pin.png) toopin todas as visualizações tooyour painel. toofind obter instruções, consulte [fixar um painel do Power BI de tooa lado a lado de um relatório](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     Acesse a página do painel toohello e ajustar o tamanho de saudação e o local de suas visualizações e editar seus títulos. toofind instruções detalhadas sobre como tooedit seus blocos, consulte [editar um bloco, redimensionar, mover, renomear, fixar, excluir, Adicionar hiperlink](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Aqui está um exemplo de painel com alguns tooit de visualizações fixadas caminho frios.  Dependendo de quanto tempo você executa o gerador de dados, os números em visualizações de saudação podem ser diferentes.
     <br/>
     ![Exibição final](media/cortana-analytics-technical-guide-predictive-maintenance/final-view.png)
     <br/>
   * tooschedule atualização de dados hello, passe o mouse sobre Olá **PredictiveMaintenanceAerospace** conjunto de dados, clique em ![ícone de reticências](media/cortana-analytics-technical-guide-predictive-maintenance/icon-elipsis.png) e, em seguida, escolha **agendar atualização**.
     <br/>
     **Observação:** se você vir Massagem um aviso, clique em **Editar credenciais** e verifique se suas credenciais de banco de dados são Olá mesmo daqueles descritos na etapa 1.
     <br/>
     ![Agendar atualização](media/cortana-analytics-technical-guide-predictive-maintenance/schedule-refresh.png)
     <br/>
   * Expanda Olá **agendar atualização** seção. Ative "manter os dados atualizados".
     <br/>
   * Agendar a atualização de saudação com base em suas necessidades. toofind obter mais informações, consulte [de atualização de dados no Power BI](https://support.powerbi.com/knowledgebase/articles/474669-data-refresh-in-power-bi).

### <a name="setup-hot-path-dashboard"></a>Painel de afunilamento de instalação
Olá etapas a seguir irá guiá-lo como toovisualize em tempo real de saída de dados de análise de fluxo de trabalhos que foram gerados em tempo de saudação da implantação da solução. Um [Power BI online](http://www.powerbi.com/) conta é necessário tooperform Olá etapas a seguir. Se não tiver uma conta, você poderá [criar uma](https://powerbi.microsoft.com/pricing).

1. Adicione a saída do Power BI ao Stream Analytics (ASA).
   
   * Você precisará de instruções Olá toofollow [Stream Analytics do Azure e Power BI: um painel de análise em tempo real para visibilidade em tempo real do fluxo de dados](../stream-analytics/stream-analytics-power-bi-dashboard.md) tooset a saída de saudação do seu trabalho do Stream Analytics do Azure como a potência Painel BI.
   * consulta ASA Hello tem três saídas que são **aircraftmonitor**, **aircraftalert**, e **flightsbyhour**. Você pode exibir a consulta Olá clicando na guia de consulta. Tooeach correspondente dessas tabelas, você precisará tooadd tooASA uma saída. Quando você adiciona a primeira saída de hello (*, por exemplo,* **aircraftmonitor**) Verifique se Olá **Alias de saída**, **nome do conjunto de dados** e  **Nome da tabela** são Olá mesmo (**aircraftmonitor**). Olá Repita etapas tooadd saídas para **aircraftalert**, e **flightsbyhour**. Depois de adicionar todas as três tabelas de saída e Olá ASA trabalho iniciado, você deve receber uma mensagem de confirmação (*, por exemplo,*, "Iniciar análise de fluxo de trabalho maintenancesa02asapbi bem-sucedida").
2. Faça logon no muito[online para o Power BI](http://www.powerbi.com)
   
   * Em Olá seção de conjuntos de dados do painel da esquerda no meu espaço de trabalho, o ***DATASET*** nomes **aircraftmonitor**, **aircraftalert**, e **flightsbyhour**devem aparecer. Isso é hello fluxo de dados enviados por push do Stream Analytics do Azure no conjunto de dados Olá de anterior step.hello **flightsbyhour** poderá não aparecer no hello como Olá outros dois conjuntos de dados devido a natureza toohello de consultas SQL Olá a mesma hora ele. No entanto, ele deve aparecer após uma hora.
   * Verifique se Olá ***visualizações*** painel está aberto e é exibido no lado direito da tela hello.
3. Depois que você tiver Olá dados que fluem para o Power BI, você pode iniciar visualizando Olá fluxo de dados. Abaixo está que um exemplo de painel com algumas visualizações de afunilamento fixado tooit. É possível criar outros blocos de painel com base em conjuntos de dados apropriados. Dependendo de quanto tempo você executa o gerador de dados, os números em visualizações de saudação podem ser diferentes.

    ![Exibição Painel](media\cortana-analytics-technical-guide-predictive-maintenance\dashboard-view.png)

1. Aqui estão alguns toocreate de etapas um dos blocos de saudação acima – hello "exibição frota de Sensor 11 vs. limite 48,26":
   
   * Clique em conjunto de dados **aircraftmonitor** na seção de conjuntos de dados do painel da esquerda de saudação.
   * Clique em Olá **gráfico de linhas** ícone.
   * Clique em **processadas** em Olá **campos** painel para que ela mostra sob "Eixo" hello **visualizações** painel.
   * Clique em "s11" e em "s11\_alert" para que ambos sejam exibidos em "Valores". Clica Olá pequena seta Avançar muito**s11** e **s11\_alerta**, altere "Sum" muito "Médio".
   * Clique em **salvar** Olá superior e nome do relatório hello "aircraftmonitor". O relatório chamado "aircraftmonitor" será mostrado em Olá **relatórios** seção Olá **navegador** painel Olá esquerda.
   * Clique em Olá **Pin Visual** ícone no canto superior direito de saudação do gráfico de linhas. Uma janela de "Pin tooDashboard" poderá aparecer para escolher um painel. Selecione "Demonstração de manutenção preditiva" e clique em "Fixar".
   * Focalize o mouse Olá esse bloco no painel de saudação, clique em hello "" Editar em toochange de canto superior direito da saudação seu título muito "Fleet exibição de Sensor 11 vs. Limite 48,26" e o subtítulo muito""Médio" em fleet ao longo do tempo.

## <a name="how-toodelete-your-solution"></a>**Como toodelete sua solução**
Certifique-se de que você interrompa o gerador de dados hello quando usando ativamente a solução de saudação como executar gerador de dados Olá incorrerá em custos mais altos. Exclua solução Olá se não estiver usando. A exclusão de sua solução excluirá todos os componentes de saudação provisionados em sua assinatura quando você implantou a solução de saudação. solução de saudação do toodelete clique em seu nome da solução no painel esquerdo de saudação do modelo de solução de saudação e clique em Excluir.

## <a name="cost-estimation-tools"></a>**Ferramentas de estimativa de custo**
Olá duas ferramentas a seguir estão disponível toohelp você entender melhor os custos totais envolvido na execução Olá manutenção preditiva para o modelo de solução aeroespacial em sua assinatura:

* [Ferramenta Calculadora de Preço do Microsoft Azure (online)](https://azure.microsoft.com/pricing/calculator/)
* [Ferramenta Calculadora de Preço do Microsoft Azure (área de trabalho)](http://www.microsoft.com/download/details.aspx?id=43376)

