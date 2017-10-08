---
title: "aaaLive fluxo de métricas com métricas personalizadas e diagnósticos no Azure Application Insights | Microsoft Docs"
description: "Monitore seu aplicativo Web em tempo real usando métrica personalizada e diagnostique problemas com um feed em tempo real de falhas, rastreamentos e eventos."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a>Live Metrics Stream: monitorar e diagnosticar com latência de um segundo 

Teste o coração de pulsação de saudação do seu aplicativo web em tempo real, em produção usando o fluxo ao vivo de métricas de [Application Insights](app-insights-overview.md). Selecionar e filtrar toowatch de contadores de desempenho e métricas em tempo real, sem qualquer serviço de tooyour interferência no. Inspecione os rastreamentos de pilha de exceções e solicitações de amostra com falha. Juntamente com [Criador de perfil](app-insights-profiler.md), [Depurador de instantâneo](app-insights-snapshot-debugger.md) e [testes de desempenho](app-insights-monitor-web-app-availability.md#performance-tests), o Live Metrics Stream fornece uma ferramenta de diagnóstico poderosa e não invasiva para seu site ao vivo.

Com o Live Metrics Stream, você pode:

* Valide uma correção enquanto ela é liberado, observando as contagens de falha e desempenho.
* Assista o efeito de saudação de cargas de teste e diagnosticar problemas em tempo real. 
* Se concentrar em sessões de teste específica ou filtrar problemas conhecidos, selecionando e métricas Olá deseja toowatch de filtragem.
* Obter rastreamentos de exceção quando eles ocorrerem.
* Experiência com filtros toofind Olá KPIs mais relevantes.
* Monitore qualquer contador de desempenho do Windows em tempo real.
* Facilmente identificar um servidor que está tendo problemas e filtrar todos os Olá KPI/live feed toojust nesse servidor.

[![Vídeo do Live Metrics Stream](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)

Transmissão ao vivo de métricas está disponível em aplicativos ASP.NET executados localmente ou na nuvem de saudação. 

## <a name="get-started"></a>Introdução

1. Se você ainda não [instalou o Application Insights](app-insights-asp-net.md) no aplicativo Web ASP.NET ou [aplicativo do Windows Server](app-insights-windows-services.md), faça isso agora. 
2. **Versão mais recente da atualização toohello** do pacote do Application Insights hello. No Visual Studio, clique com o botão direito do mouse em seu projeto e escolha **Gerenciar pacotes Nuget**. Olá abrir **atualizações** guia seleção **incluir pré-lançamento**e selecionar todos os pacotes de Microsoft.ApplicationInsights.* hello.

    Reimplante o aplicativo.

3. Em Olá [portal do Azure](https://portal.azure.com), abra o recurso do Application Insights Olá para seu aplicativo e, em seguida, abrir o fluxo ao vivo.

4. [Canal de controle seguro Olá](#secure-the-control-channel) se você pode usar dados confidenciais, como nomes de clientes em seus filtros.


![Na folha de visão geral de saudação, clique em fluxo ao vivo](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a>Não há dados? Verificar o firewall de servidor

Verificar Olá [portas de saída para transmissão ao vivo de métricas](app-insights-ip-addresses.md#outgoing-ports) estão abertas no firewall Olá dos seus servidores. 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a>Como o Live Metrics Stream difere do Metrics Explorer e Analytics?

| |Live Stream | Metrics Explorer e Analytics |
|---|---|---|
|Latência|Dados exibidos em um segundo|Agregado ao longo de minutos|
|Nenhuma retenção|Persiste os dados enquanto ele está em um gráfico de saudação e é descartado|[Dados retidos por 90 dias](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|Sob demanda|Os dados são transmitidos enquanto você abre o Live Metrics|Os dados são enviados sempre que Olá SDK está instalado e habilitado|
|Grátis|Não há nenhum custo para dados do Live Stream|Entidade muito[preços](app-insights-pricing.md)
|amostragem|Todas as métricas e os contadores selecionados são transmitidos. Há amostras de falhas e rastreamentos de pilha. TelemetryProcessors não são aplicados.|Os eventos podem ter [amostras](app-insights-api-filtering-sampling.md)|
|Canal de controle|Sinais de controle de filtro são enviados toohello SDK. Recomendamos que você [proteja este canal](#secure-channel).|A comunicação é unidirecional toohello portal|


## <a name="select-and-filter-your-metrics"></a>Selecionar e filtrar suas métricas

(Disponível em clássico aplicativos ASP.NET com hello SDK mais recente.)

Você pode monitorar o KPI personalizado ao vivo aplicando filtros arbitrários em qualquer telemetria do Application Insights do portal de saudação. Clique em controle de filtro de saudação que mostra quando você passar o mouse qualquer um dos gráficos de saudação. Olá gráfico a seguir é uma contagem de solicitação personalizada KPI com filtros em atributos de URL e a duração de plotagem. Valide os filtros com hello seção de visualização de fluxo que mostra um feed de telemetria que corresponde aos critérios de saudação especificado em qualquer ponto no tempo. 

![KPI de solicitação personalizado](./media/app-insights-live-stream/live-stream-filteredMetric.png)

Você pode monitorar um valor diferente da Contagem. Opções de saudação dependem de tipo de saudação do fluxo, o que pode ser qualquer telemetria do Application Insights: solicitações, dependências, exceções, rastreamentos, eventos ou métricas. Ela pode ser sua própria [medida personalizada](app-insights-api-custom-events-metrics.md#properties):

![Opções de valor](./media/app-insights-live-stream/live-stream-valueoptions.png)

Além disso tooApplication telemetria Insights, você também pode monitorar qualquer contador de desempenho do Windows que a seleção de opções de fluxo de saudação e fornecendo o nome Olá Olá do contador de desempenho.

Métricas em tempo real são agregadas em dois pontos: localmente em cada servidor e, em seguida, em todos os servidores. Você pode alterar o padrão, Olá selecionando outras opções no hello respectivos suspensos.

## <a name="sample-telemetry-custom-live-diagnostic-events"></a>Telemetria de exemplo: eventos de diagnóstico em tempo real personalizados
Por padrão, o feed Olá de eventos mostra exemplos de solicitações com falha e chamadas de dependência, exceções, eventos e rastreamentos. Clique em critérios Olá filtro ícone toosee Olá aplicada em qualquer ponto no tempo. 

![Feed em tempo real padrão](./media/app-insights-live-stream/live-stream-eventsdefault.png)

Como com métricas, você pode especificar qualquer tooany critérios arbitrário de tipos de telemetria do Application Insights hello. Neste exemplo, estamos selecionando falhas, rastreamentos e eventos de solicitação específicos. Também estamos selecionando todas as exceções e falhas de dependência.

![Feed em tempo real personalizado](./media/app-insights-live-stream/live-stream-events.png)

Observação: No momento, para critérios baseada em mensagem de exceção use mensagem de exceção mais externo hello. Em Olá anterior como exemplo, toofilter out a exceção benignas Olá com a mensagem de exceção interna (segue hello "< –" delimitador) "cliente de saudação desconectado." use um critério de que a mensagem não contém "Erro ao ler o conteúdo da solicitação".

Consulte os detalhes de saudação de um item no hello live feed clicando nele. Você pode pausar Olá feed clicando **pausar** simplesmente rolando para baixo ou clicar em um item. Feed dinâmica será retomado quando você rola toohello back superior, ou clicando o contador de saudação de itens coletados enquanto ele estava em pausa.

![Amostra de falhas em tempo real](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a>Filtrar por instância do servidor

Se você quiser toomonitor uma instância de função de servidor específico, você pode filtrar por servidor.

![Amostra de falhas em tempo real](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a>Requisitos do SDK
O Fluxo de métricas em tempo real personalizado está disponível com a versão 2.4.0-beta2 ou mais recente do [SDK do Application Insights para Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). Lembre-se a opção de "Incluir pré-lançamento" tooselect do Gerenciador de pacotes do NuGet.

## <a name="secure-hello-control-channel"></a>Proteger o canal de controle de saudação
critérios de filtros personalizados Olá especificados são enviados toohello back componente de métricas em tempo real em Olá SDK do Application Insights. filtros de saudação possam conter informações confidenciais, como customerIDs. Você pode fazer com que o canal de saudação seguro com uma chave de segredo de API além toohello chave de instrumentação.
### <a name="create-an-api-key"></a>Criar uma chave de API

![Criar chave de API](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a>Adicionar tooConfiguration de chave de API
No arquivo applicationinsights. config de hello, adicione Olá AuthenticationApiKey toohello QuickPulseTelemetryModule:
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
Ou, no código, defina-Olá QuickPulseTelemetryModule:

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

No entanto, se você reconhece e confia em que todos os Olá servidores conectados, você pode tentar filtros personalizados de saudação sem canal Olá autenticado. Essa opção está disponível por seis meses. Essa substituição é necessária uma vez a cada nova sessão ou quando um novo servidor ficar online.

![Opções de autenticação das métricas em tempo real](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
>É altamente recomendável que você configure o canal Olá autenticado antes de inserir informações potencialmente confidenciais como CustomerID Olá critérios de filtro.
>

## <a name="generating-a-performance-test-load"></a>Geração de uma carga de teste de desempenho

Se você quiser toowatch efeito de saudação carga aumentar, folha de teste de desempenho do uso hello. Ele simula solicitações de vários usuários simultâneos. Ele pode ser executado ou "testes manuais" (ping testes) de uma única URL, ou pode executar um [teste de desempenho web de várias etapas](app-insights-monitor-web-app-availability.md#multi-step-web-tests) que você carregue (em Olá mesma forma como uma disponibilidade de teste).

> [!TIP]
> Depois de criar o teste de desempenho Olá, abra o teste hello e Olá folha de transmissão ao vivo em janelas separadas. Você pode ver quando Olá enfileiradas inicia de teste de desempenho e a transmissão ao vivo inspecionar a saudação simultaneamente.
>


## <a name="troubleshooting"></a>Solucionar problemas

Não há dados? Se seu aplicativo estiver em uma rede protegida: o Fluxo de métricas em tempo real usará endereços IP diferentes de outras Application Insights Telemetries. Certifique-se de que [esses endereços IP](app-insights-ip-addresses.md) estejam abertos em seu firewall.



## <a name="next-steps"></a>Próximas etapas
* [Monitorando o uso com o Application Insights](app-insights-web-track-usage.md)
* [Usando a Pesquisa de diagnóstico](app-insights-diagnostic-search.md)
* [Criador de perfil](app-insights-profiler.md)
* [Depurador instantâneo](app-insights-snapshot-debugger.md)
