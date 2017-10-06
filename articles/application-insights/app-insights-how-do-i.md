---
title: "aaaHow fazer … em informações de aplicativo do Azure | Microsoft Docs"
description: Perguntas Frequentes no Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a>Como ... no Application Insights?
## <a name="get-an-email-when-"></a>Receber um email quando...
### <a name="email-if-my-site-goes-down"></a>Enviar emails se meu site ficar inativo
Definir um [teste da Web de disponibilidade](app-insights-monitor-web-app-availability.md).

### <a name="email-if-my-site-is-overloaded"></a>Enviar emails de meu site estiver sobrecarregado
Definir um [alerta](app-insights-alerts.md) para **Tempo de resposta do servidor**. Um limite entre 1 e 2 segundos deve funcionar.

![](./media/app-insights-how-do-i/030-server.png)

Seu aplicativo também pode mostrar sinais de sobrecarga retornando códigos de falha. Definir um alerta para **Solicitações com falha**.

Se você quiser tooset um alerta em **exceções servidor**, talvez seja necessário toodo [alguma configuração adicional](app-insights-asp-net-exceptions.md) dados de pedidos toosee.

### <a name="email-on-exceptions"></a>Exceções de email
1. [Configurar monitoramento de exceção](app-insights-asp-net-exceptions.md)
2. [Definir um alerta](app-insights-alerts.md) em Olá exceção contagem métrica

### <a name="email-on-an-event-in-my-app"></a>Enviar emails sobre um evento em meu aplicativo
Vamos supor que você gostaria que tooget um email quando ocorrer um evento específico. O Application Insights não oferece esse recurso diretamente, mas pode [enviar um alerta quando uma métrica ultrapassar um limite](app-insights-alerts.md).

Alertas podem ser definidos com base em [métricas personalizadas](app-insights-api-custom-events-metrics.md#trackmetric), mas não em eventos personalizados. Grave algumas tooincrease código uma métrica quando ocorre o evento de saudação:

    telemetry.TrackMetric("Alarm", 10);

ou:

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

Como os alertas têm dois estados, você tem toosend um valor baixo quando você considera o alerta Olá toohave foi encerrado:

    telemetry.TrackMetric("Alarm", 0.5);

Criar um gráfico em [explorer métrica](app-insights-metrics-explorer.md) toosee o alarme:

![](./media/app-insights-how-do-i/010-alarm.png)

Agora, defina toofire um alerta quando a métrica de saudação fica acima de um valor médio por um curto período:

![](./media/app-insights-how-do-i/020-threshold.png)

Definir Olá média toohello período mínimo.

Você receberá emails quando a métrica de saudação fica acima e abaixo do limite de saudação.

Tooconsider alguns pontos:

* Um alerta tem dois estados ("alerta" e "íntegro"). estado de saudação é avaliado somente quando uma métrica é recebida.
* Um email é enviado apenas quando o estado de saudação é alterado. Isso é porque você tem toosend métricas de alta e baixa-valor.
* alerta tooevaluate Olá média Olá é assumida de valores hello recebida Olá que precedem o período. Isso ocorre sempre que uma métrica é recebida, portanto emails podem ser enviados com mais frequência do que o período Olá definido.
* Desde que os emails são enviados na "alerta" e "Íntegro", talvez você queira tooconsider pensando novamente seu evento única como uma condição de dois estados. Por exemplo, em vez de um evento de "trabalho concluído", ter uma condição de "trabalho em andamento", onde você recebe emails no início de saudação e no final de um trabalho.

### <a name="set-up-alerts-automatically"></a>Configurar alertas automaticamente
[Use o PowerShell toocreate novos alertas](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a>Use o PowerShell tooManage Application Insights
* [Criar novos recursos](app-insights-powershell-script-create-resource.md)
* [Criar novos alertas](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a>Telemetria separada de versões diferentes

* Várias funções em um aplicativo: use um único recurso do Application Insights e filtre cloud_Rolename. [Saiba mais](app-insights-monitor-multi-role-apps.md)
* Separação de desenvolvimento, teste e versões de lançamento: usar recursos diferentes do Application Insights. Obter chaves de instrumentação de saudação do Web. config. [Saiba mais](app-insights-separate-resources.md)
* Relatando versões de build: adicionar uma propriedade usando um inicializador de telemetria. [Saiba mais](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a>Monitorar servidores de back-end e aplicativos de desktop
[Módulo de SDK do Windows Server Olá Use](app-insights-windows-desktop.md).

## <a name="visualize-data"></a>Visualizar dados
#### <a name="dashboard-with-metrics-from-multiple-apps"></a>Painel com métricas de vários aplicativos
* No [Metrics Explorer](app-insights-metrics-explorer.md), personalize o gráfico e salve-o como um favorito. Fixe-toohello do painel do Azure.

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a>Painel com dados de outras fontes e Application Insights
* [Exportar telemetria tooPower BI](app-insights-export-power-bi.md).

Ou

* Use o SharePoint como seu painel e exiba dados em web parts do SharePoint. [Use a exportação contínua e análise de fluxo tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).  Usar banco de dados do PowerView tooexamine hello e criar uma web part do SharePoint para PowerView.

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a>Filtrar usuários anônimos ou autenticados
Se os usuários se conectar, você pode definir Olá [autenticado a id de usuário](app-insights-api-custom-events-metrics.md#authenticated-users). (Isso não ocorre automaticamente.)

Você pode:

* Pesquisar IDs de usuário específicos

![](./media/app-insights-how-do-i/110-search.png)

* Filtrar usuários de autenticado ou anônimo tooeither métricas

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a>Modificar valores ou nomes de propriedade
Crie um [filtro](app-insights-api-filtering-sampling.md#filtering). Isso permite modificar ou filtrar telemetria antes de ser enviada de seu aplicativo tooApplication Insights.

## <a name="list-specific-users-and-their-usage"></a>Listar usuários específicos e seu uso
Se você quiser apenas muito[pesquisa para usuários específicos](#search-specific-users), você pode definir Olá [autenticado a id de usuário](app-insights-api-custom-events-metrics.md#authenticated-users).

Se você quiser uma lista de usuários com os dados como, por exemplo, quais páginas eles exibem e com qual frequência eles fazem logon, você terá duas opções:

* [Id do conjunto de usuário autenticado](app-insights-api-custom-events-metrics.md#authenticated-users), [Exportar banco de dados tooa](app-insights-code-sample-export-sql-stream-analytics.md) e uso adequado ferramentas tooanalyze seus dados de usuário.
* Se você tiver somente um pequeno número de usuários, envie eventos personalizados ou métricas, usando dados de saudação de interesse como Olá valor de métrica ou o nome do evento e a id de usuário de saudação de configuração como uma propriedade. modos de exibição de página tooanalyze, substitua saudação padrão JavaScript trackPageView de chamada. tooanalyze telemetria do lado do servidor, use uma telemetria inicializador tooadd Olá id tooall server telemetria do usuário. Você pode, em seguida, as métricas de filtro e de segmento e pesquisas na id de usuário de saudação.

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a>Reduzir o tráfego de tooApplication meu aplicativo Insights
* Em [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), desabilite quaisquer módulos que não é necessário, tal coletor de contador de desempenho de saudação.
* Use [amostragem e filtragem](app-insights-api-filtering-sampling.md) em Olá SDK.
* Nas páginas da web, limite o número de saudação de chamadas Ajax relatados para cada modo de exibição de página. No trecho de script hello após `instrumentationKey:...` , insira: `,maxAjaxCallsPerView:3` (ou um número adequado).
* Se você estiver usando [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), agregação de saudação de lotes de valores da métrica de computação antes de enviar os resultados de saudação. Há uma sobrecarga de TrackMetric() que possibilita isso.

Saiba mais sobre [preços e cotas](app-insights-pricing.md).

## <a name="disable-telemetry"></a>Desabilitar telemetria
muito**dinamicamente parar e iniciar** Olá coleta e transmissão de telemetria do servidor de saudação:

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



muito**desabilitar os coletores padrão selecionados** - por exemplo, contadores de desempenho, as solicitações HTTP ou dependências - exclua ou comente linhas relevantes Olá [Applicationinsights](app-insights-api-custom-events-metrics.md). Você pode fazer isso, por exemplo, se você quiser toosend seus próprios dados TrackRequest.

## <a name="view-system-performance-counters"></a>Exibir contadores de desempenho do sistema
Entre Olá métricas, que você pode exibir no metrics explorer são um conjunto de contadores de desempenho do sistema. Há uma folha predefinida intitulada **Servidores** que exibe vários deles.

![Abra o recurso Application Insights e clique em Servidores](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a>Se você não vir dados do contador de desempenho
* **Servidor IIS** em seu próprio computador ou em uma VM. [Instalar Monitor de Status](app-insights-monitor-performance-live-website-now.md).
* **Site do Azure** - ainda não há suporte para contadores de desempenho. Há várias métricas, que você pode obter como parte do painel de controle do site do Azure hello.
* **Servidor Unix** - [Instalar collectd](app-insights-java-collectd.md)

### <a name="toodisplay-more-performance-counters"></a>toodisplay mais contadores de desempenho
* Primeiro, [adicionar um novo gráfico](app-insights-metrics-explorer.md) e veja se Olá contador em Olá básica definido que oferecemos.
* Caso contrário, [adicionar Olá contador toohello conjunto coletado pelo módulo do contador de desempenho de saudação](app-insights-performance-counters.md).
