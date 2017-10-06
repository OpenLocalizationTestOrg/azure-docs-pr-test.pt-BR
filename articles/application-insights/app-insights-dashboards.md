---
title: "aaaDashboards e navegação no hello Azure Application Insights | Microsoft Docs"
description: "Crie exibições de suas consultas e gráficos principais do APM."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a>Painéis no portal do Application Insights hello e navegação
Depois de ter [configurar o Application Insights no seu projeto](app-insights-overview.md), dados de telemetria sobre desempenho e uso de seu aplicativo aparecerá no recurso do Application Insights do seu projeto no hello [portal do Azure](https://portal.azure.com).

## <a name="find-your-telemetry"></a>Encontrar sua telemetria
Entrar toohello [portal do Azure](https://portal.azure.com) e navegue de recurso do Application Insights toohello que você criou para seu aplicativo.

![Clique em Procurar, selecione Application Insights e seu aplicativo.](./media/app-insights-dashboards/00-start.png)

folha de visão geral de saudação (página) para seu aplicativo mostra um resumo dos principais métricas diagnóstico saudação do seu aplicativo e é um gateway toohello outros recursos do portal de saudação.

![Principais rotas tooview sua Telemetria](./media/app-insights-dashboards/010-oview.png)

Você pode personalizar qualquer um dos gráficos hello e grades e fixá-los tooa painel. Dessa forma, você pode reunir telemetria chave Olá de aplicativos diferentes em um painel central.

## <a name="dashboards"></a>Painéis
Olá primeiro você ver depois que você entra no toohello [portal do Microsoft Azure](https://portal.azure.com) é um painel. Aqui você pode reunir gráficos Olá que são mais importante tooyou em todos os seus recursos do Azure, incluindo a telemetria de [Azure Application Insights](app-insights-overview.md).

![Um painel personalizado.](./media/app-insights-dashboards/31.png)

1. **Navegue recursos toospecific** como seu aplicativo no Application Insights: barra à esquerda do uso hello.
2. **Painel atual retorno toohello**, ou alternar exibições recente tooother: Use Olá lista suspensa na parte superior esquerda.
3. **Alternar painéis**: Use Olá lista suspensa no título do painel Olá
4. **Criar, editar e compartilhar painéis** na barra de ferramentas do painel hello.
5. **Editar o painel Olá**: focalize um bloco e, em seguida, use a parte superior da barra toomove, personalizar ou removê-lo.

## <a name="add-tooa-dashboard"></a>Adicionar painel tooa
Quando você está procurando em uma folha ou conjunto de gráficos que é especialmente interessante, você pode fixar uma cópia desse painel toohello. Você o verá da próxima vez que retornar.

![toopin um gráfico, passe o mouse sobre ele e, em seguida, clique em "..." no cabeçalho de saudação.](./media/app-insights-dashboards/33.png)

1. Fixar toodashboard do gráfico. Uma cópia do gráfico de saudação aparece no painel de saudação.
2. PIN Olá folha inteira toohello painel - ele é exibido no painel de saudação como um bloco que você pode clicar.
3. Clique em Painel do canto superior esquerdo tooreturn toohello atual hello. Em seguida, você pode usar o hello menu suspenso tooreturn toohello modo de exibição atual.

Observe que os gráficos são agrupados em blocos: um bloco pode conter mais de um gráfico. Fixar o dashboard do hello bloco inteiro toohello.

gráfico de saudação é atualizado automaticamente com uma frequência que depende do intervalo de tempo do gráfico de saudação:

* Tempo de intervalo de hora too1: atualizar a cada 5 minutos
* Intervalo de tempo de 1 a 24 horas: atualizar a cada 15 minutos
* Intervalo de tempo acima de 24 horas: (intervalo de tempo)/60.

### <a name="pin-any-query-in-analytics"></a>Fixar qualquer consulta no Analytics
Você também pode [fixar análise](app-insights-analytics-using.md#pin-to-dashboard) gráficos tooa [compartilhado](#share-dashboards-with-your-team) painel. Isso permite que você tooadd gráficos de qualquer consulta arbitrário juntamente com métricas padrão de saudação. 

Os resultados são automaticamente recalculados a cada hora. Clique o ícone de atualização de Olá Olá gráfico toorecalculate imediatamente. (Atualizar do navegador não é recalculado.)

## <a name="adjust-a-tile-on-hello-dashboard"></a>Ajustar um bloco no painel de saudação
Após um bloco no painel hello, você pode ajustá-lo.

![Passe o mouse sobre um gráfico em ordem tooedit-lo.](./media/app-insights-dashboards/36.png)

1. Adicione um bloco de toohello do gráfico.
2. Definir a métrica hello, agrupar por dimensão e estilo (tabela, gráfico) de um gráfico.
3. Percorra Olá diagrama toozoom Clique em Olá desfazer botão tooreset Olá timespan; definir as propriedades de filtro de gráficos Olá no bloco de saudação.
4. Defina o título do bloco.

Blocos fixados de folhas do Metric Explorer têm mais opções de edição que aqueles fixados de uma folha de Visão Geral.

Olá original lado a lado que você fixou não é afetada por suas edições.

## <a name="switch-between-dashboards"></a>Alternar entre painéis
É possível salvar mais de um painel e alternar entre eles. Quando você fixa um gráfico ou folha, elas são adicionadas toohello do painel atual.

![tooswitch entre os painéis, clique em Painel de controle e selecione um painel salvo. toocreate e salvar um novo painel, clique em novo. toorearrange, clique em Editar.](./media/app-insights-dashboards/32.png)

Por exemplo, você pode ter um painel de exibição de tela inteira na sala de equipe hello e outro para desenvolvimento geral.

No painel hello, uma folha é exibido como um bloco: clique em toogo toohello folha. Um gráfico de replica gráfico Olá em seu local original.

![Clique em uma folha de saudação do bloco tooopen representa](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a>Compartilhar painéis
Quando você tiver criado um painel, poderá compartilhá-lo com outros usuários.

![No cabeçalho do painel de saudação, clique em compartilhamento](./media/app-insights-dashboards/41.png)

Saiba mais sobre [Funções e controle de acesso](app-insights-resources-roles-access-control.md).

## <a name="app-navigation"></a>Navegação do aplicativo
folha de visão geral de saudação é Olá gateway toomore informações de seu aplicativo.

* **Qualquer bloco ou gráfico** - clique em qualquer bloco ou gráfico toosee mais detalhes sobre o que é exibido.

### <a name="overview-blade-buttons"></a>Botões da folha Visão geral
![Barra de navegação superior da folha Visão geral](./media/app-insights-dashboards/app-overview-top-nav.png)

* [**Metrics Explorer**](app-insights-metrics-explorer.md) -crie seus próprios gráficos de desempenho e de uso.
* [**Pesquisa**](app-insights-diagnostic-search.md) - para investigar instâncias específicas de eventos, como solicitações, exceções ou log de rastreamento.
* [**Analytics**](app-insights-analytics.md) - consultas poderosas em sua telemetria.
* **Intervalo de tempo** -ajustar o intervalo de saudação exibido por todos os gráficos de saudação na folha de saudação.
* **Excluir** -excluir recurso do Application Insights Olá para este aplicativo. Você deve também remover pacotes do Application Insights Olá do código do aplicativo, ou editar Olá [chave de instrumentação](app-insights-create-new-resource.md#copy-the-instrumentation-key) em seu recurso de Application Insights diferente de tooa do aplicativo toodirect telemetria.

### <a name="essentials-tab"></a>Guia Conceitos Básicos
* [Chave de instrumentação](app-insights-create-new-resource.md#copy-the-instrumentation-key) -identifica esse recurso de aplicativo.
* Preço - disponibilize as funcionalidades disponíveis e defina volumes.

### <a name="app-navigation-bar"></a>Barra de navegação do aplicativo
![Barra de navegação à esquerda](./media/app-insights-dashboards/app-left-nav-bar.png)

* **Visão geral do** -toohello retorno folha de visão geral do aplicativo.
* **Log de atividades** -alertas e eventos administrativos do Azure.
* [**Controle de acesso** ](app-insights-resources-roles-access-control.md) -fornecem membros de tooteam de acesso e outros.
* [**Marcas** ](../azure-resource-manager/resource-group-using-tags.md) -Use marcas toogroup seu aplicativo com outras pessoas.

INVESTIGAR

* [**Mapa de aplicativo** ](app-insights-app-map.md) -mapa ativo mostrando componentes de saudação do seu aplicativo, derivado de informações de dependência de saudação.
* [**Detecção Inteligente**](app-insights-proactive-diagnostics.md) - Examine os alertas de desempenho recentes.
* [**Live Stream**](app-insights-live-stream.md) - um conjunto fixo de métricas quase instantâneas, úteis ao implantar um novo build ou depurar.
* [**Disponibilidade / testes na Web** ](app-insights-monitor-web-app-availability.md) -enviar solicitações regular tooyour aplicativo web em torno de saudação world.*
* [**Falhas e desempenho** ](app-insights-web-monitor-performance.md) -exceções, taxas de falha e resposta vezes para solicitações tooyour aplicativo e para solicitações de seu aplicativo muito[dependências](app-insights-asp-net-dependencies.md).
* [**Desempenho**](app-insights-web-monitor-performance.md) - tempo de resposta, tempos de resposta de dependência.
* [Servidores](app-insights-web-monitor-performance.md) - contadores de desempenho. Disponível se você [instalar o Status Monitor](app-insights-monitor-performance-live-website-now.md).
* **Navegador** - exibição de página e desempenho do AJAX. Disponível se você [instrumentar suas páginas da Web](app-insights-javascript.md).
* **Uso** - contagens de sessão, usuário e exibição de página. Disponível se você [instrumentar suas páginas da Web](app-insights-javascript.md).

CONFIGURAR

* **Introdução** - tutorial embutido.
* **Propriedades** - chave de instrumentação, assinatura e ID de recurso.
* [Alertas](app-insights-alerts.md) - configuração do alerta de métrica.
* [A exportação contínua](app-insights-export-telemetry.md) -configurar a exportação do armazenamento de tooAzure de telemetria.
* [Teste de desempenho](app-insights-monitor-web-app-availability.md#performance-tests) - configure uma carga sintética no seu site.
* [Cota e preço](app-insights-pricing.md) e [amostragem de ingestão](app-insights-sampling.md).
* **Acesso à API** -criar [versão anotações](app-insights-annotations.md) e Olá API de acesso a dados.
* [**Itens de trabalho** ](app-insights-diagnostic-search.md#create-work-item) -conectar-se o trabalho tooa sistema de controle para que você possa criar bugs durante a inspeção de telemetria.

CONFIGURAÇÕES

* [**Bloqueios**](../azure-resource-manager/resource-group-lock-resources.md) - bloqueie recursos do Azure
* [**Script de automação** ](app-insights-powershell.md) -exportar uma definição de saudação recursos do Azure para que você pode usá-lo como um recurso novo do modelo toocreate.


## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Próximas etapas

|  |  |
| --- | --- |
| [Metrics explorer](app-insights-metrics-explorer.md)<br/>Métricas de filtro e de segmento |![Exemplo de pesquisa](./media/app-insights-dashboards/64.png) |
| [Pesquisa de diagnóstico](app-insights-diagnostic-search.md)<br/>Localize e inspecione eventos, eventos relacionados e crie bugs |![Exemplo de pesquisa](./media/app-insights-dashboards/61.png) |
| [Analytics](app-insights-analytics.md)<br/>Linguagem de consulta poderosa |![Exemplo de pesquisa](./media/app-insights-dashboards/63.png) |
