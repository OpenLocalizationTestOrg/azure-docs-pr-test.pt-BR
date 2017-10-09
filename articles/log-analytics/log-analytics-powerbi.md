---
title: "tooPower de dados de análise de Log aaaExport BI | Microsoft Docs"
description: "O Power BI é um serviço de análise de negócios baseado em nuvem da Microsoft que fornece relatórios e visualizações avançadas para análise de diferentes conjuntos de dados.  Análise de log continuamente pode exportar dados do repositório do OMS Olá no Power BI para que você possa aproveitar suas visualizações e ferramentas de análise.  Este artigo descreve como tooconfigure as consultas de análise de Log que exportar tooPower BI automaticamente em intervalos regulares."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 4822f99677e5d1080c72e95cda410da81615bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="export-log-analytics-data-toopower-bi"></a>Exportar dados de análise de Log tooPower BI

>[!NOTE]
> Se o seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), em seguida, esse processo de exportação de dados de análise de Log tooPower BI deixarão de funcionar.  Todas as agendas existentes criadas antes da atualização serão desabilitadas. 
>
> Após a atualização, usa a análise de Log do Azure Olá mesma plataforma como o Application Insights e usar Olá mesmo processo tooPower de consultas de análise de Log tooexport BI como [tooexport de processo de saudação do Application Insights consultas tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).  Você pode exportar consulta hello usando o console de análise de saudação conforme descrito no artigo, ou você pode selecionar Olá **Power BI** botão na parte superior de saudação da tela hello no portal de pesquisa de Log de saudação.



O [Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) é um serviço de análise de negócios baseado em nuvem da Microsoft que fornece relatórios e visualizações avançadas para análise de diferentes conjuntos de dados.  Análise de log automaticamente pode exportar dados do repositório do OMS Olá no Power BI para que você possa aproveitar suas visualizações e ferramentas de análise.

Quando você configurar o Power BI com análise de Log, você pode criar consultas de log que exportar seus conjuntos de dados de toocorresponding resultados no Power BI.  exportação e consulta Olá continua tooautomatically executado em um agendamento que definem o conjunto de dados tookeep Olá backup toodate com dados mais recentes de saudação coletados pela análise de Log.

![Análise de log tooPower BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a>Agendas do Power BI
Um *Power BI agenda* inclui uma pesquisa de log que exporta um conjunto de dados de saudação do OMS repositório tooa correspondente conjunto de dados no Power BI e uma agenda que define a frequência na qual a pesquisa é executada tookeep Olá dataset atual.

campos de saudação no conjunto de dados Olá corresponderá propriedades Olá Olá registros retornados pela pesquisa de log de saudação.  Se pesquisa Olá retorna registros de tipos diferentes Olá conjunto de dados incluirá todas propriedades saudação de cada um dos Olá incluem tipos de registro.  

> [!NOTE]
> É um toouse de prática recomendada uma consulta de pesquisa de log que retorna dados brutos como tooperforming contrário qualquer consolidação usando comandos como [medida](log-analytics-search-reference.md#measure).  Você pode executar qualquer agregação e cálculos no Power BI dos dados brutos de saudação.
>
>

## <a name="connecting-oms-workspace-toopower-bi"></a>Conectar-se tooPower de espaço de trabalho do OMS BI
Antes de você pode exportar de análise de Log tooPower BI, você deve se conectar a sua conta da tooyour de espaço de trabalho do OMS Power BI usando Olá procedimento a seguir.  

1. No console do OMS Olá clique Olá **configurações** lado a lado.
2. Selecione **Contas**.
3. Em Olá **informações de espaço de trabalho** seção clique **conectar tooPower conta BI**.
4. Insira as credenciais de saudação para sua conta do Power BI.

## <a name="create-a-power-bi-schedule"></a>Criar uma agenda do Power BI
Crie uma agenda de BI de energia para cada conjunto de dados usando Olá procedimento a seguir.

1. No console do OMS Olá clique Olá **pesquisa de Log** lado a lado.
2. Digite uma nova consulta ou selecione uma pesquisa salva que retorna Olá dados que você deseja tooexport muito**Power BI**.  
3. Clique em Olá **Power BI** botão na parte superior da saudação de saudação do hello página tooopen **Power BI** caixa de diálogo.
4. Fornecer informações de saudação em Olá seguinte tabela e clique em **salvar**.

| Propriedade | Descrição |
|:--- |:--- |
| Nome |Nome tooidentify Olá agendar quando você exibir a lista de saudação de agendas do Power BI. |
| Pesquisa Salva |Olá toorun de pesquisa de log.  Você pode selecionar a consulta atual hello ou selecione uma pesquisa salva existente na caixa de lista suspensa de saudação. |
| Agenda |Frequência Olá toorun salvo pesquisar e exportar o conjunto de dados do toohello Power BI.  Olá valor deve ser entre 15 minutos e 24 horas. |
| Nome do conjunto de dados |nome de saudação do conjunto de dados Olá no Power BI.  Ele será criado se ele não existir e atualizado se existir. |

## <a name="viewing-and-removing-power-bi-schedules"></a>Exibir e remover agendas do Power BI
Exiba a lista de saudação do existente agendas do Power BI com hello procedimento a seguir.

1. No console do OMS Olá clique Olá **configurações** lado a lado.
2. Selecione **Power BI**.

Além disso toohello detalhes de saudação agendar, número de saudação de vezes que Olá agenda está em execução Olá semana passada e status de saudação da última sincronização de saudação são exibidos.  Se a sincronização de saudação encontrou erros, você pode clicar em Olá link toorun uma pesquisa de log de registros com detalhes do erro de saudação.

Você pode remover uma agenda clicando-se em Olá **X** em Olá **Remover coluna**.  É possível desabilitar um agendamento selecionando **Desativado**.  toomodify uma agenda você deve removê-lo e recriá-la com novas configurações de saudação.

![Agendas do Power BI](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a>Passo a passo de exemplo
Hello seção a seguir apresenta um exemplo de criação de uma agenda do Power BI e usando seu conjunto de dados toocreate um relatório simples.  Neste exemplo, todos os dados de desempenho para um conjunto de computadores é exportado tooPower BI e, em seguida, um gráfico de linha é criado toodisplay utilização do processador.

### <a name="create-log-search"></a>Criar pesquisa de log
Vamos começar criando uma pesquisa de log de dados de saudação que desejamos toosend toohello dataset.  Neste exemplo, usaremos uma consulta que retorna todos os dados de desempenho de computadores com um nome que começa com *srv*.  

![Agendas do Power BI](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a>Criar a pesquisa do Power BI
Olá, clicamos **Power BI** botão caixa de diálogo tooopen Olá Power BI e fornecer informações de saudação necessária.  Podemos deseja toorun essa pesquisa uma vez por hora e criar um conjunto de dados chamado *Contoso Perf*.  Como já temos Olá pesquisa aberto que cria dados de saudação queremos, mantemos padrão Olá *usar consulta de pesquisa atual* para **pesquisa salva**.

![Pesquisa do Power BI](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a>Verifique a pesquisa do Power BI
tooverify que criamos agenda Olá corretamente, vemos que a lista de saudação do Power BI pesquisas em Olá **configurações** bloco no painel do OMS hello.  Aguarde alguns minutos e atualize essa exibição até que informa que a sincronização de saudação foi executada.

![Pesquisa do Power BI](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-hello-dataset-in-power-bi"></a>Verifique se a saudação de conjunto de dados no Power BI
Registramos em nossa conta na [powerbi.microsoft.com](http://powerbi.microsoft.com/) e role muito**conjuntos de dados** na parte inferior de saudação do painel esquerdo do hello.  Podemos ver que Olá *Contoso Perf* conjunto de dados está listado, indicando que o nosso exportação foi executada com êxito.

![Conjunto de dados do Power BI](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a>Criar um relatório com base no conjunto de dados
Selecionamos Olá **Contoso Perf** conjunto de dados e, em seguida, clique em **resultados** em Olá **campos** painel Olá tooview direita Olá os campos que fazem parte deste conjunto de dados.  toocreate uma utilização do processador de mostrando do gráfico de linha para cada computador, podemos executar Olá ações a seguir.

1. Selecione a visualização de gráfico de linha de saudação.
2. Arraste **ObjectName** muito**filtro de nível de relatório** e verificar **processador**.
3. Arraste **CounterName** muito**filtro de nível de relatório** e verificar **% tempo do processador**.
4. Arraste **CounterValue** muito**valores**.
5. Arraste **computador** muito**legenda**.
6. Arraste **TimeGenerated** muito**eixo**.

Podemos ver que um gráfico de linhas resultante que Olá é exibido com os dados de saudação do nosso conjunto de dados.

![Gráfico de linha do Power BI](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-hello-report"></a>Salvar relatório Olá
Podemos salvar relatório Olá clicando em hello botão na parte superior de saudação da tela hello e valide que agora está listado na seção de relatórios de saudação no painel esquerdo da saudação.

![Relatórios do Power BI](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) toobuild consultas que podem ser exportados tooPower BI.
* Saiba mais sobre [Power BI](http://powerbi.microsoft.com) toobuild visualizações com base em exportações de análise de Log.
