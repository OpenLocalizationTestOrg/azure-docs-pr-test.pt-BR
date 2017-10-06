---
title: "aaaSmart detecção - anomalias falha, no Application Insights | Microsoft Docs"
description: "Alerta toounusual alterações na taxa de saudação do aplicativo de web tooyour solicitações com falha e fornece a análise de diagnóstico. Nenhuma configuração é necessária."
services: application-insights
documentationcenter: 
author: yorac
manager: carmonm
ms.assetid: ea2a28ed-4cd9-4006-bd5a-d4c76f4ec20b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: bwren
ms.openlocfilehash: dfd178ca9546294be91f27b0c1b846d519539b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection---failure-anomalies"></a>Detecção Inteligente - anomalias de falha
[Application Insights](app-insights-overview.md) automaticamente notifica quase em tempo real se seu aplicativo web passa por um aumento anormal na taxa de saudação de solicitações com falha. Ele detecta um aumento incomuns na taxa de saudação de solicitações HTTP ou chamadas de dependência são relatadas como falha. Para solicitações, solicitações com falha geralmente são aqueles com códigos de resposta de 400 ou superior. toohelp triagem e diagnosticar o problema hello, uma análise das características de saudação do hello falhas e telemetrias relacionadas é fornecida na notificação de saudação. Também há portal do Application Insights links toohello para diagnóstico mais detalhado. Olá recurso não precisa de nenhuma instalação nem a configuração, pois ele usa o aprendizado de máquina taxa de falha normal algoritmos toopredict hello.

Esse recurso funciona para aplicativos web Java e ASP.NET, hospedados na nuvem hello, ou em seus próprios servidores. Ele também funciona para qualquer aplicativo que gere telemetria de solicitação ou de dependência - por exemplo, se você tiver uma função de trabalho que chame [TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) ou [TrackDependency()](app-insights-api-custom-events-metrics.md#trackdependency).

Depois de configurar o [Application Insights para seu projeto](app-insights-overview.md), e desde que o aplicativo gera uma determinada quantidade mínima de telemetria, inteligente detecção de anomalias de falha leva 24 horas comportamento normal do toolearn saudação do seu aplicativo, antes que ele está ligado e podem enviar alertas.

Veja a seguir um exemplo do alerta.

![Exemplo de alerta de detecção inteligente mostrando a análise de cluster sobre a falha](./media/app-insights-proactive-failure-diagnostics/013.png)

> [!NOTE]
> Por padrão, você receberá uma mensagem com formato mais curto que esse exemplo. Mas você pode [formato detalhado do comutador toothis](#configure-alerts).
>
>

Observe o que ele diz:

* taxa de falhas de saudação comparados toonormal o comportamento do aplicativo.
* Quantos usuários são afetados – para saber quanto tooworry.
* Um padrão de característica associado a saudação falhas. Neste exemplo, há um código de resposta específico, o nome da solicitação (operação) e a versão do aplicativo. Que informa imediatamente onde toostart procurando em seu código. Outras possibilidades poderiam ser um navegador ou um sistema operacional cliente específico.
* exceção Hello, rastreamentos de log e falha de dependência (bancos de dados ou outros componentes externos) que aparecem toobe associado Olá caracterizam falhas.
* Vincula diretamente toorelevant pesquisas na telemetria Olá no Application Insights.

## <a name="benefits-of-smart-detection"></a>Benefícios da Detecção Inteligente
Os [alertas de métrica](app-insights-alerts.md) comuns mostram que pode haver um problema. Mas detecção inteligente inicia o trabalho de diagnóstico Olá para você, executando muitos analysis Olá você teria toodo por conta própria. Obtém Olá resultados claramente empacotados, ajudando você a tooget rapidamente toohello raiz do problema de saudação.

## <a name="how-it-works"></a>Como funciona
Detecção inteligente monitora telemetria Olá recebida de seu aplicativo e nas taxas de falha de saudação específico. Essa regra conta o número de saudação de solicitações para o qual Olá `Successful request` propriedade é false, e número de saudação de dependência chama para quais Olá `Successful call` propriedade é false. Para solicitações, por padrão, `Successful request == (resultCode < 400)` (a menos que você tenha escrito código personalizado muito[filtro](app-insights-api-filtering-sampling.md#filtering) ou gerar seu próprio [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest) chamadas). 

O desempenho do aplicativo tem um padrão típico de comportamento. Algumas solicitações ou chamadas de dependência será mais propensa toofailure que outros; e hello taxa geral de falhas pode subir como a carga aumenta. Detecção inteligente usa essas anomalias toofind do aprendizado de máquina.

Como telemetria de volta no Application Insights de seu aplicativo web, detecção inteligente compara o comportamento atual Olá com padrões Olá vistos pela Olá alguns dias anteriores. Se for observado um aumento anormal na taxa de falha em comparação com o desempenho anterior, uma análise será disparada.

Quando uma análise é disparada, o serviço Olá realiza uma análise de cluster na solicitação com falha de Olá, tootry tooidentify um padrão de valores que caracterizam falhas hello. O exemplo hello acima, análise de saudação descobriu que a maioria das falhas são sobre um código de resultado específico, nome da solicitação, o host de URL do servidor e instância de função. Por outro lado, a análise Olá descobriu que propriedade do sistema operacional de cliente Olá é distribuída por vários valores, e portanto ele não está listado.

Quando o serviço está instrumentado com essas chamadas de telemetria, analyser Olá procura uma exceção e uma falha de dependência que estão associadas a solicitações em cluster Olá identificados, junto com um exemplo de quaisquer logs de rastreamento associados a esses solicitações.

análise resultante Olá é enviado tooyou como alerta, a menos que você o configurou para não.

Como Olá [alertas que você definir manualmente](app-insights-alerts.md), você pode inspecionar o estado de saudação do alerta hello e configurá-lo na folha de alertas de saudação do recurso do Application Insights. Mas, ao contrário de outros alertas, você não precise tooset backup ou configurar a detecção inteligente. Se quiser, você pode desabilitá-lo ou alterar o endereço de email de destino.

## <a name="configure-alerts"></a>Configurar alertas
Desabilitar a detecção inteligente, alterar Olá destinatários de email, criar um webhook ou aceitar toomore detalhada mensagens de alerta.

Abra a página de alertas de saudação. Falha de anomalias está incluído junto com todos os alertas que você configurou manualmente, e você pode ver se ele está em estado de alerta de saudação.

![Na página de visão geral de saudação, clique em bloco de alertas. Ou em qualquer página Métricas, clique no botão Alertas.](./media/app-insights-proactive-failure-diagnostics/021.png)

Clique em tooconfigure alerta Olá-lo.

![Configuração](./media/app-insights-proactive-failure-diagnostics/032.png)

Observe que você pode desabilitar a Detecção Inteligente, mas não excluí-la (nem criar outra).

#### <a name="detailed-alerts"></a>Alertas detalhados
Se você selecionar "Obter diagnósticos mais detalhados" email Olá conterá mais informações de diagnóstico. Às vezes, você estará toodiagnose capaz de problema de saudação apenas por meio de dados de saudação no email de saudação.

Não há o risco de pequeno hello mais detalhada de alerta pode conter informações confidenciais, porque ela inclui mensagens de exceção e rastreamento. No entanto, isso aconteceria apenas se seu código permitisse informações confidenciais nessas mensagens.

## <a name="triaging-and-diagnosing-an-alert"></a>Triagem e diagnóstico de um alerta
Um alerta indica que um aumento anormal na taxa de solicitação com falha Olá foi detectado. É provável que haja algum problema com seu aplicativo ou seu ambiente.

De porcentagem de saudação de solicitações e o número de usuários afetados, você pode decidir como urgente problema de saudação é. O exemplo hello acima, taxa de falhas de saudação do 22.5% compara com uma taxa normal de % 1, indica que algo ruim está em andamento. Em Olá outro lado, somente 11 usuários foram afetados. Se fosse seu aplicativo, seria possível tooassess a gravidade é.

Em muitos casos, será capaz de toodiagnose problema de Olá rapidamente usando o nome da solicitação hello, exceção, dados de rastreamento e de falha de dependência fornecidos.

Há alguns outros indícios. Por exemplo, taxa de falha de dependência Olá neste exemplo é Olá mesmas Olá taxa de exceções (% 89.3). Isso sugere que exceção Olá surge diretamente da falha de dependência Olá - dando a você uma ideia clara de onde toostart procurando em seu código.

tooinvestigate Além disso, Olá links em cada seção terão reta tooa [página Pesquisa](app-insights-diagnostic-search.md) filtrados solicitações relevantes toohello, exceções, dependências ou rastreamentos. Ou você pode abrir Olá [portal do Azure](https://portal.azure.com), navegue recurso do Application Insights toohello para seu aplicativo e abra a folha de falhas de saudação.

Neste exemplo, clicando em link de saudação 'Exibir dependência falhas detalhes' abre a folha de pesquisa do hello Application Insights. Ele mostra a instrução SQL Olá que tem um exemplo de causas Olá: foram fornecidos em campos obrigatórios de nulos e não passou na validação durante a saudação operação de gravação.

![Pesquisa de diagnóstico](./media/app-insights-proactive-failure-diagnostics/051.png)

## <a name="review-recent-alerts"></a>Exame dos alertas recentes

Clique em **detecção inteligente** tooget toohello mais recente alerta:

![Resumo de alertas](./media/app-insights-proactive-failure-diagnostics/070.png)


## <a name="whats-hello-difference-"></a>Qual é a diferença de saudação...
A Detecção Inteligente de anomalias de falha complementa outros recursos distintos, mas parecidos, do Application Insights.

* Os [Alertas de Métrica](app-insights-alerts.md) são definidos por você e podem monitorar uma ampla variedade de métricas, como a ocupação da CPU, as taxas de solicitação, os tempos de carregamento de página e assim por diante. Você pode usar toowarn você, por exemplo, se você precisar de mais recursos tooadd. Por outro lado, inteligente detecção de anomalias de falha abrange toonotify um pequeno intervalo de métricas críticas (atualmente apenas com falha taxa de solicitação), projetado que você em quase em tempo real de maneira quando aumenta significativamente a taxa de solicitação com falha do seu aplicativo web em comparação com tooweb do aplicativo comportamento normal.

    Detecção inteligente ajusta automaticamente o seu limite de condições de tooprevailing de resposta.

    Detecção inteligente inicia o trabalho de diagnóstico Olá para você.
* [Detecção de anomalias de desempenho de Smart](app-insights-proactive-performance-diagnostics.md) também usa inteligência toodiscover incomum padrões suas métricas de máquina, e é necessária nenhuma configuração por você. Mas diferentemente inteligente detecção de anomalias de falha, finalidade Olá inteligente detecção de anomalias de desempenho é toofind segmentos de sua coleção de uso que pode ser servida mal - por exemplo, por páginas específicas em um tipo de navegador específico. análise de saudação é executada diariamente e se nenhum resultado for encontrado, é provável toobe muito menos urgente que um alerta. Por outro lado, análise de saudação de anomalias de falha é executada continuamente na telemetria a entrada, e você será notificado dentro de minutos se as taxas de falha do servidor são maiores do que o esperado.

## <a name="if-you-receive-a-smart-detection-alert"></a>Se você receber um alerta de Detecção Inteligente
*Por que eu recebei esse alerta?*

* Foi detectado um aumento anormal em solicitações com falha taxa comparada toohello normal linha de base de saudação anterior período. Após a análise de falhas de saudação e telemetria associada, achamos que há um problema que você deve examinar.

*Notificação de saudação significa que tenho definitivamente um problema?*

* Tentamos tooalert na interrupção do aplicativo ou degradação, mas só você possa entender totalmente os semântica hello e impacto Olá no aplicativo hello ou usuários.

*Então, vocês examinam os meus dados?*

* Não. serviço de saudação é totalmente automático. Obter somente as notificações de saudação. Os dados são [privados](app-insights-data-retention-privacy.md).

*É necessário toosubscribe toothis alerta?*

* Não. Cada aplicativo que envia uma solicitação telemetria tem regra de alerta de detecção inteligente hello.

*Pode cancelar a assinatura ou receber as notificações de saudação enviadas toomy colegas?*

* Sim, as regras de alerta, clique em tooconfigure de regra de detecção inteligente Olá-lo. Você pode desabilitar alerta hello, ou alterar destinatários de alerta de saudação.

*Perdi email hello. Onde posso encontrar notificações Olá no portal de Olá?*

* Olá logs de atividade. No Azure, abrir o recurso do Application Insights Olá para seu aplicativo, selecione os logs de atividade.

*Alguns dos Olá alertas sobre problemas conhecidos e não quero tooreceive-los.*

* Nós temos a supressão de alerta em nossa lista de pendências.

## <a name="next-steps"></a>Próximas etapas
Essas ferramentas de diagnóstico ajudam a inspecionar a telemetria de saudação do seu aplicativo:

* [Metrics explorer](app-insights-metrics-explorer.md)
* [Gerenciador de pesquisas](app-insights-diagnostic-search.md)
* [Analytics - linguagem de consulta poderosa](app-insights-analytics-tour.md)

As detecções inteligentes são totalmente automáticas. Mas você queria tooset alguns alertas mais?

* [Alertas de métrica configurados manualmente](app-insights-alerts.md)
* [Testes de disponibilidade na Web](app-insights-monitor-web-app-availability.md)
