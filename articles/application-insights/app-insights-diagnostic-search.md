---
title: aaaUsing pesquisa no Azure Application Insights | Microsoft Docs
description: Pesquise e filtre telemetria bruta enviada pelo seu aplicativo Web.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a>Usar a Pesquisa no Application Insights
A pesquisa é um recurso do [Application Insights](app-insights-overview.md) usar toofind e explorar os itens de telemetria individuais, como modos de exibição de página, exceções ou solicitações de web. Você também pode exibir rastreamentos de log e eventos que você tenha codificado.

(Para consultas mais complexas sobre os dados, use o [Analytics](app-insights-analytics-tour.md).)

## <a name="where-do-you-see-search"></a>Onde você vê a Pesquisa?
### <a name="in-hello-azure-portal"></a>No portal do Azure de saudação
Você pode abrir pesquisa diagnóstica explicitamente na folha de visão geral das informações do aplicativo de saudação do seu aplicativo:

![Abra a pesquisa de diagnóstico](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

Ela também é aberta quando você clica em alguns gráficos e itens de grade. Nesse caso, os filtros são definidos previamente toofocus no tipo de saudação do item selecionado. 

Por exemplo, na folha de visão geral do hello, há um gráfico de barras de solicitações classificadas por tempo de resposta. Clique em um toosee de intervalo de desempenho por meio de uma lista de solicitações individuais em que o intervalo de tempo de resposta:

![Clique no desempenho de solicitação](./media/app-insights-diagnostic-search/07-open-from-filters.png)

saudação de corpo principal da pesquisa de diagnóstico é uma lista de itens de telemetria - solicitações ao servidor, página exibições, eventos personalizados que você codificou e assim por diante. Em Olá parte superior da lista de saudação é um gráfico de resumo mostra as contagens de eventos ao longo do tempo.

Clique em Atualizar tooget novos eventos.

### <a name="in-visual-studio"></a>No Visual Studio

No Visual Studio, há também uma janela da Pesquisa do Application Insights. É mais útil para exibir eventos de telemetria gerados pelo aplicativo hello que você está depurando. Mas ele também pode mostrar eventos Olá coletados do seu aplicativo publicado no hello portal do Azure.

Abra a janela de pesquisa de saudação no Visual Studio:

![O Visual Studio abre a pesquisa do Application Insights](./media/app-insights-diagnostic-search/32.png)

janela de pesquisa Olá tem portal do recursos semelhantes toohello da web:

![Janela de pesquisa do Visual Studio Application Insights](./media/app-insights-diagnostic-search/34.png)

Guia de faixa operação Hello está disponível quando você abrir uma solicitação ou um modo de exibição de página. Um ' operação ' é uma sequência de eventos que está associada à exibição única tooa solicitação ou página. Por exemplo, chamadas de dependência, exceções, logs de rastreamento e eventos personalizados podem fazer parte de uma única operação. Olá operação de controle guia mostra graficamente Olá tempo e a duração esses eventos em relação toohello o modo de exibição de solicitação ou página. 

## <a name="inspect-individual-items"></a>Inspecionar itens individuais
Selecione todos os campos de chave de toosee de item de telemetria e itens relacionados. Se você quiser toosee Olá todo o conjunto de campos, clique em "...". 

![Clique em Novo Item de trabalho, editar campos de hello e, em seguida, clique em Okey.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a>Filtrar tipos de evento
Abra a folha de filtro hello e escolher os tipos de evento Olá você deseja toosee. (Se, posteriormente, você deseja que os filtros de saudação toorestore com a qual você abriu a folha de saudação, clique em Redefinir.)

![Escolha o filtro e selecione os tipos de telemetria](./media/app-insights-diagnostic-search/02-filter-req.png)

os tipos de evento Olá são:

* **Controlar** - [Logs de diagnóstico](app-insights-asp-net-trace-logs.md), incluindo chamadas TrackTrace, log4Net, NLog e System.Diagnostic.Trace.
* **Solicitar** -Solicitações HTTP recebidas pelo seu aplicativo para servidores, incluindo páginas, scripts, imagens, arquivos de estilo e dados. Esses eventos são gráficos de visão geral usado toocreate Olá solicitação e resposta.
* **Exibição de página** - [telemetria enviada pelo cliente de web de saudação](app-insights-javascript.md), usado toocreate relatórios de modo de exibição de página. 
* **Evento personalizado** - se você inseriu chamadas tooTrackEvent() na ordem muito[monitorar o uso de](app-insights-api-custom-events-metrics.md), você pode pesquisar aqui.
* **Exceção** - não percebida [exceções no servidor de saudação](app-insights-asp-net-exceptions.md)e aqueles que você faça logon usando trackexception ().
* **Dependência** - [chamadas de seu aplicativo de servidor](app-insights-asp-net-dependencies.md) tooother os serviços, como bancos de dados ou APIs REST e chamadas AJAX de seu [código de cliente](app-insights-javascript.md).
* **Disponibilidade** ‑ Resultados de [testes de disponibilidade](app-insights-monitor-web-app-availability.md).

## <a name="filter-on-property-values"></a>Filtrar pelos valores de propriedade
Você pode filtrar eventos em valores de saudação de suas propriedades. propriedades disponíveis Olá dependem de tipos de evento de saudação selecionado. 

Por exemplo, escolha solicitações com um código de resposta específicos. 

![Expanda uma propriedade e escolha um valor](./media/app-insights-diagnostic-search/03-response500.png)

Não escolher nenhum valor de uma propriedade específica tem Olá mesmo efeito que escolher todos os valores. Ele desativará a filtragem nessa propriedade.

### <a name="narrow-your-search"></a>Reduzir o escopo de sua pesquisa
Observe que Olá contagens toohello à direita dos valores de filtro de saudação mostrar quantos ocorrências existe estão no conjunto atual de filtrado hello. 

Neste exemplo, é claro que a solicitação ' Rpt/funcionários' hello resulta na maioria dos erros de saudação '500':

![Expanda uma propriedade e escolha um valor](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a>Localizar eventos com hello mesma propriedade
Localizar Olá a todos os itens com hello mesmo valor da propriedade:

![Clique com o botão direito em uma propriedade](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a>Dados de saudação de pesquisa

> [!NOTE]
> toowrite consultas mais complexas, abra [ **análise** ](app-insights-analytics-tour.md) da parte superior da saudação da folha de pesquisa de saudação.
> 

Você pode pesquisar termos em qualquer um dos valores de propriedade hello. Isso será especialmente útil se você tiver gravado [eventos personalizados](app-insights-api-custom-events-metrics.md) com valores de propriedade. 

Talvez você queira tooset um intervalo de tempo, como pesquisas em um intervalo mais curto é mais rápido. 

![Abra a pesquisa de diagnóstico](./media/app-insights-diagnostic-search/appinsights-311search.png)

Pesquisar por palavras inteiras, não subcadeias de caracteres. Use caracteres especiais do tooenclose aspas.

| string | *não* é encontrada por | porém, pode ser encontrada por |
| --- | --- | --- |
| ControladorInicial.Sobre |inicial<br/>controlador<br/>obre | homecontroller<br/>sobre<br/>"homecontroller.about"|
|Estados Unidos|Uni<br/>dos|unidos<br/>estados<br/>estados AND unidos<br/>“estados unidos”

Aqui estão as expressões de pesquisa de saudação, que você pode usar:

| Exemplo de consulta | Efeito |
| --- | --- |
| `apple` |Localiza todos os eventos no intervalo de tempo de saudação cujos campos incluem palavras hello "apple" |
| `apple AND banana` |Encontrar eventos que contêm as duas palavras. Use "AND” em letras maiúsculas, e não "and". |
| `apple OR banana`<br/>`apple banana` |Encontrar eventos que contêm uma das duas palavras. Use "OR", e não "or".<br/>Forma abreviada. |
| `apple NOT banana` |Localize eventos que contêm uma palavra mas não Olá outros. |



## <a name="sampling"></a>amostragem
Se seu aplicativo gera muita telemetria (e você estiver usando Olá ASP.NET SDK versão 2.0.0-beta3 ou posterior), módulo de amostragem adaptável Olá automaticamente reduz o volume de saudação enviada toohello portal enviando apenas uma fração representativa de eventos. No entanto, eventos que são relacionada toohello mesma solicitação são selecionado ou desmarcado como um grupo, para que você possa navegar entre eventos relacionados. 

[Saiba mais sobre amostragem](app-insights-sampling.md).



## <a name="create-work-item"></a>Criar um item de trabalho
Você pode criar um bug no GitHub ou Visual Studio Team Services com detalhes de saudação de qualquer item de telemetria. 

![Clique em Novo Item de trabalho, editar campos de hello e, em seguida, clique em Okey.](./media/app-insights-diagnostic-search/42.png)

Hello primeira vez que você fizer isso, você será solicitado a tooconfigure tooyour um link do Team Services conta e de projeto.

![Preencher Olá URL do seu servidor do Team Services e o nome do projeto hello e, em seguida, clique em autorizar](./media/app-insights-diagnostic-search/41.png)

(Você também pode configurar o link de saudação na folha de itens de trabalho hello.)

## <a name="save-your-search"></a>Salvar sua pesquisa
Quando você definiu todos os filtros de saudação desejado, você pode salvar pesquisa hello como um favorito. Se você trabalha em uma conta organizacional, você pode escolher se tooshare-lo com outros membros da equipe.

![Clique em favorito, Olá nome do conjunto e clique em Salvar](./media/app-insights-diagnostic-search/08-favorite-save.png)

novamente, pesquisa de saudação toosee **folha de visão geral de toohello vá** e abrir favoritos:

![Bloco Favoritos](./media/app-insights-diagnostic-search/09-favorite-get.png)

Se você salvou com intervalo de tempo relativo, folha reaberto Olá tem dados mais recentes de saudação. Se você salvou com intervalo de tempo absoluto, você verá Olá mesmos dados toda vez. (Se 'Relativo' não está disponível quando você deseja toosave um favorito, clique o intervalo de tempo no cabeçalho de saudação e definir um intervalo de tempo que não é um intervalo personalizado).

## <a name="send-more-telemetry-tooapplication-insights"></a>Enviar telemetria mais tooApplication Insights
Telemetria de fora da caixa de toohello adição enviada pelo SDK do Application Insights, você pode:

* Capturar rastreamentos de log da sua estrutura de registros favorita no [.NET](app-insights-asp-net-trace-logs.md) ou [Java](app-insights-java-trace-logs.md). Isso significa que você pode pesquisar os rastreamentos de log e correlacioná-los com outros eventos, exceções e visualizações de página. 
* [Escrever código](app-insights-api-custom-events-metrics.md) toosend eventos personalizados, modos de exibição de página e as exceções. 

[Saiba como toosend registra e telemetria personalizada tooApplication Insights](app-insights-asp-net-trace-logs.md).

## <a name="questions"></a>Perguntas e respostas
### <a name="limits"></a>Que quantidade de dados é mantida?

Consulte Olá [resumo de limites](app-insights-pricing.md#limits-summary).

### <a name="how-can-i-see-post-data-in-my-server-requests"></a>Como consultar dados de POSTAGEM nas minhas solicitações de servidor?
Nós não registrar dados de POSTAGEM Olá automaticamente, mas você pode usar [TrackTrace ou log chama](app-insights-asp-net-trace-logs.md). Colocar os dados de POSTAGEM Olá no parâmetro de mensagem de saudação. Não é possível filtrar em uma mensagem de saudação no hello mesma forma, você pode filtrar em propriedades, mas o limite de tamanho de saudação é maior.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="add"></a>Próximas etapas
* [Escrever consultas complexas no Analytics](app-insights-analytics-tour.md)
* [Enviar logs e telemetria personalizada tooApplication Insights](app-insights-asp-net-trace-logs.md)
* [Configurar testes de disponibilidade e capacidade de resposta](app-insights-monitor-web-app-availability.md)
* [Solução de problemas](app-insights-troubleshoot-faq.md)
