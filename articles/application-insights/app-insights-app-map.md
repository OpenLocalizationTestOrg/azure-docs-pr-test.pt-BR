---
title: aaaApplication mapa no Azure Application Insights | Microsoft Docs
description: "Uma apresentação visual de dependências de saudação entre componentes de aplicativo, rotulado com KPIs e alertas."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a>Mapa de Aplicativos no Application Insights
Em [Azure Application Insights](app-insights-overview.md), mapa de aplicativo é um layout visual de relações de dependência de saudação de componentes do seu aplicativo. Cada componente mostra KPIs como toohelp de carga, desempenho, falhas e alertas, você descobrir qualquer componente causando um problema de desempenho ou falha. Você pode clicar por meio de qualquer componente toomore detalhadas de diagnóstico, como eventos do Application Insights. Se seu aplicativo usa os serviços do Azure, você também pode clicar tooAzure diagnóstico, como as recomendações do Orientador de banco de dados SQL.

Como outros gráficos, você pode fixar um toohello de mapa de aplicativo do painel do Azure, onde ela será totalmente funcional. 

## <a name="open-hello-application-map"></a>Mapa de aplicativo hello aberto
Olá abrir o mapa da folha de visão geral de saudação para seu aplicativo:

![abrir mapa de aplicativos](./media/app-insights-app-map/01.png)

![mapa de aplicativos](./media/app-insights-app-map/02.png)

mapa de saudação mostra:

* Testes de disponibilidade
* Componente do lado do cliente (monitorado com hello SDK de JavaScript)
* Componente do lado do servidor
* Dependências de componentes de cliente e servidor de saudação

Você pode expandir e recolher grupos de link de dependência:

![recolher](./media/app-insights-app-map/03.png)

Se você tiver muitas dependências de um tipo (SQL, HTTP, etc.), elas poderão aparecer agrupadas. 

![dependências agrupadas](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a>Identificar problemas
Cada nó tem indicadores de desempenho relevantes, como taxas de falha de carga e desempenho Olá para esse componente. 

Ícones de aviso destacam possíveis problemas. Um aviso laranja significa que existem falhas em solicitações, exibições de página ou chamadas de dependência. Vermelho significa uma taxa de falha acima de 5%. Se você quiser tooadjust esses limites, abra Opções.

![ícones de falha](./media/app-insights-app-map/04.png)

Alertas ativos também aparecem: 

![alertas ativos](./media/app-insights-app-map/05.png)

Se você usa o SQL Azure, há um ícone que mostra quando há recomendações sobre como melhorar o desempenho. 

![Recomendações do Azure](./media/app-insights-app-map/06.png)

Clique em qualquer ícone tooget mais detalhes:

![Recomendações do Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a>Clique para Diagnóstico
Cada um de nós de saudação no mapa de saudação oferece destino de cliques para diagnóstico. Opções de saudação variam dependendo do tipo de saudação do nó de saudação.

![opções de servidor](./media/app-insights-app-map/09.png)

Para componentes que são hospedadas no Azure, as opções de saudação incluem toothem links diretos.

## <a name="filters-and-time-range"></a>Filtros e o intervalo de tempo
Por padrão, o mapa de Olá resume todos os dados de saudação disponíveis para Olá escolhido o intervalo de tempo. Mas você pode filtrar nomes de operação específica somente tooinclude ou dependências.

* Nome da operação: isso inclui tipos de solicitação do lado servidor e exibições de página. Com essa opção, a saudação mapa mostra Olá KPI no nó de servidor/cliente Olá Olá selecionada apenas para operações. Ele mostra dependências Olá chamadas no contexto de saudação dessas operações específicas.
* Nome de base de dependência: Isso inclui Olá AJAX navegador dependências e do lado do servidor. Se o relatório de telemetria de dependência personalizada com hello TrackDependency API, elas também aparecerão aqui. Você pode selecionar Olá dependências tooshow no mapa de saudação. Atualmente esta seleção não filtrar solicitações do lado do servidor de saudação ou exibições saudação do cliente.

![Definir filtros](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a>Salvar filtros
filtros de saudação toosave você aplicou, Olá pin filtrados exibição para um [painel](app-insights-dashboards.md).

![PIN toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a>Painel de erros
Quando você clica em um nó no mapa Olá, um painel de erro é exibido no lado direito de saudação resumindo falhas para esse nó. As falhas são agrupadas primeiro segundo a ID da operação e, em seguida, segundo a ID do problema.

![Painel de erros](./media/app-insights-app-map/error-pane.png)

Clicando em uma falha de usa a instância mais recente toohello essa falha.

## <a name="resource-health"></a>Integridade de recursos
Para alguns tipos de recurso, integridade de recursos é exibida na parte superior de saudação do painel de erro hello. Por exemplo, clicando em um nó do SQL mostrará integridade de banco de dados de saudação e todos os alertas que tenham disparado.

![Integridade de recursos](./media/app-insights-app-map/resource-health.png)

Você pode clicar em métricas de visão geral padrão de tooview Olá recursos nome para esse recurso.

## <a name="end-to-end-system-app-maps"></a>Mapas de aplicativos do sistema de ponta a ponta

*Requer o SDK versão 2.3 ou superior*

Se seu aplicativo tiver vários componentes - por exemplo, um serviço back-end além de aplicativo da web de toohello - em seguida, você pode mostrá-los todos no mapa de um aplicativo integrado.

![Definir filtros](./media/app-insights-app-map/multi-component-app-map.png)

mapa de aplicativo Hello localiza nós de servidor seguindo qualquer chamada de dependência HTTP feita entre os servidores com hello que Application Insights SDK instalado. Cada recurso do Application Insights será considerado toocontain um servidor.

### <a name="multi-role-app-map-preview"></a>Mapa do aplicativo com várias funções (versão prévia)

recurso de mapa de aplicativo de várias funções de visualização Olá permite toouse Olá aplicativo mapa com vários servidores de envio de dados toohello mesmo recurso Application Insights / chave de instrumentação. Servidores no mapa de saudação são segmentadas por propriedade de cloud_RoleName Olá em itens de telemetria. Definir *mapa de aplicativos de várias funções* muito*na* de Olá visualizações folha tooenable essa configuração.

Essa abordagem pode ser desejável em um aplicativo de microsserviços ou em outros cenários onde você deseja toocorrelate eventos em vários servidores em um único recurso do Application Insights.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a>Comentários
Forneça comentários por meio da opção de comentários do portal de saudação.

![Imagem de MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a>Próximas etapas

* [Portal do Azure](https://portal.azure.com)
