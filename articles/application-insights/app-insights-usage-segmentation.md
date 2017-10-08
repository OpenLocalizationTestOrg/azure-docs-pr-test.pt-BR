---
title: "análise de aaaUser, sessão e eventos no Azure Application Insights | Documentos da Microsoft"
description: "Análise demográfica dos usuários de seu aplicativo Web."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a>Análise de usuários, sessões e eventos no Application Insights

Descubra quando as pessoas usam seu aplicativo Web, em quais páginas elas estão mais interessadas, onde os usuários estão localizados e quais navegadores e sistemas operacionais eles usam. Analisar a telemetria de negócios e de uso com o [Application Insights do Azure](app-insights-overview.md).

## <a name="get-started"></a>Introdução

Se você ainda não vir dados Olá usuários, sessões ou folhas de eventos no portal do Application Insights hello, [Saiba como tooget iniciada com ferramentas de uso de saudação](app-insights-usage-overview.md).

## <a name="hello-users-sessions-and-events-segmentation-tool"></a>ferramenta de segmentação de usuários, sessões e eventos de saudação

Três usam folhas de uso de Olá Olá mesma ferramenta tooslice e dos dados da telemetria do seu aplicativo web de três perspectivas diferentes. Filtrando e dividir os dados Olá, você pode revelar informações sobre o uso de saudação relativo de diferentes páginas e recursos.

* **Ferramenta de Usuários**: quantas pessoas usaram seu aplicativo e seus recursos.  Os usuários são contados usando IDs anônimas armazenadas em cookies do navegador. Uma única pessoa que usar diferentes navegadores ou computadores será contada como mais de um usuário.
* **Ferramenta de Sessões**: quantas sessões de atividade do usuário incluíram determinadas páginas e recursos de seu aplicativo. Uma sessão é contada após meia hora de inatividade do usuário ou após 24 horas contínuas de uso.
* **Ferramenta de Eventos**: com que frequência determinadas páginas e recursos de seu aplicativo são usados. Uma exibição de página é contada quando um navegador carrega uma página do seu aplicativo, desde que você a tenha [instrumentado](app-insights-javascript.md). 

    Um evento personalizado representa uma ocorrência de algo que esteja acontecendo em seu aplicativo, geralmente uma interação do usuário como um botão, clique em ou Olá conclusão de uma tarefa. Inserir código em seu aplicativo muito[gerar eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent).

![Ferramenta de uso](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a>Consultar determinados usuários 

Explore a diferentes grupos de usuários, ajustando as opções de consulta Olá na parte superior de saudação da ferramenta de usuários hello: 

* Quem usou: escolha exibições de página e eventos personalizados. 
* Durante: escolha um intervalo de tempo. 
* : Escolha como toobucket Olá dados, por um período de tempo ou por outra propriedade, como navegador ou uma cidade. 
* Dividir por: Escolha uma propriedade de dados Olá toosplit ou segmento. 
* Adicionar filtros: Limite Olá consultar toocertain usuários, sessões ou eventos com base em suas propriedades, como navegador ou uma cidade. 
 
## <a name="saving-and-sharing-reports"></a>Salvar e compartilhar relatórios 
Você pode salvar os relatórios de usuários, ou privada tooyou apenas na seção de meus relatórios hello, ou compartilhados com qualquer outra pessoa com acesso toothis recurso do Application Insights Olá seção relatórios compartilhados.  
 
Ao salvar um relatório ou editar suas propriedades, escolha "Atual intervalo de tempo relativo" toosave que um relatório será continuamente atualizada dados, voltando alguma quantidade fixa de tempo.  
 
Escolha "Atual intervalo de tempo absoluto" toosave um relatório com um conjunto fixo de dados. Tenha em mente que os dados no Application Insights são armazenados somente por 90 dias, portanto, se mais de 90 dias passaram desde um relatório com um intervalo de tempo absoluto foi salvo, relatório Olá aparecerá vazio. 
 
## <a name="example-instances"></a>Instâncias de exemplo

Olá seção de instâncias de exemplo mostra informações sobre uma série de eventos que correspondem a consulta atual hello, sessões ou usuários individuais. Considerar e explorar os comportamentos de saudação de indivíduos, na inclusão tooaggregates, podem fornecer informações sobre como as pessoas usam, na verdade, seu aplicativo. 
 
## <a name="insights"></a>Insights 

barra lateral de Insights Olá mostra grandes clusters de usuários que compartilham propriedades comuns. Esses clusters podem revelar tendências surpreendentes de como as pessoas usam seu aplicativo. Por exemplo, se 40% de uso de saudação do seu aplicativo todos vêm de pessoas que usam um único recurso.  


## <a name="next-steps"></a>Próximas etapas
- uso de tooenable experiências, comece a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [exibições de página](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Se você já enviar eventos personalizados ou modos de exibição de página, explorar Olá uso ferramentas toolearn como os usuários usar seu serviço.
    - [Funis](usage-funnels.md)
    - [Retenção](app-insights-usage-retention.md)
    - [Fluxos de Usuário](app-insights-usage-flows.md)
    - [Pastas de trabalho](app-insights-usage-workbooks.md)
    - [Adicionar contexto de usuário](app-insights-usage-send-user-context.md)

