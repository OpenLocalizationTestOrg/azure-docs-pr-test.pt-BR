---
title: aaaApplication telemetria Insights no CodeLens do Visual Studio | Microsoft Docs
description: "Acesse rapidamente a solicitação do Application Insights e a telemetria de exceções com o CodeLens no Visual Studio."
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 93559e44-23cb-4b9d-8425-60f7f0d0a82c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: e812aa48f2a67eea860e7ecde341855763bb8a8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a>Telemetria do Application Insights no Visual Studio CodeLens
Métodos no código de saudação do seu aplicativo web podem ser anotados com a telemetria sobre exceções de tempo de execução e tempos de resposta de solicitação. Se você instalar [Azure Application Insights](app-insights-overview.md) em seu aplicativo, telemetria Olá aparece no Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) -Olá anotações na parte superior de saudação de cada função em que você está acostumado tooseeing úteis informações como o número de saudação da função de saudação locais são referenciadas ou Olá última pessoa que editou.

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> Application Insights no CodeLens está disponível no Visual Studio 2015 atualização 3 e posterior ou com a versão mais recente de saudação do [extensão de ferramentas de análise do desenvolvedor](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a). CodeLens está disponível em Olá edições Enterprise e Professional do Visual Studio.
> 
> 

## <a name="where-toofind-application-insights-data"></a>Onde toofind dados do Application Insights
Procure a telemetria do Application Insights em indicadores de CodeLens Olá dos métodos de solicitação público de saudação do seu aplicativo web. Os indicadores do CodeLens são mostrados acima do método e outras declarações no código do C# e do Visual Basic. Se os dados do Application Insights estiverem disponíveis para um método, você verá indicadores para solicitações e exceções, como "100 solicitações, falha de 1%" ou "10 exceções". Clique em um indicador do CodeLens para obter mais detalhes. 

> [!TIP]
> Solicitação do Application Insights e indicadores de exceção podem levar alguns segundos extras tooload depois outros indicadores CodeLens aparecem.
> 
> 

## <a name="exceptions-in-codelens"></a>Exceções em CodeLens
![TBD](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

indicador de CodeLens exceção Olá mostra o número de saudação de exceções que ocorreram no hello últimas 24 horas da saudação 15 a maioria das exceções que ocorrem com frequência em seu aplicativo durante esse período, durante o processamento de solicitação de saudação servido pelo método hello.

toosee mais detalhes, clique em indicador de CodeLens Olá exceções:

* alteração da porcentagem de saudação no número de exceções de saudação últimas 24 horas relativo toohello anterior de 24 horas
* Escolha **vá toocode** toonavigate toohello código-fonte para a função hello gerar exceção Olá
* Escolha **pesquisa** tooquery Olá de todas as instâncias dessa exceção que ocorreram nas últimas 24 horas
* Escolha **tendência** tooview uma visualização de tendência para ocorrências dessa exceção na Olá últimas 24 horas
* Escolha **exibir todas as exceções nesse aplicativo** tooquery Olá de todas as exceções que ocorreram nas últimas 24 horas
* Escolha **explorar as tendências de exceção** tooview uma visualização de tendência para todas as exceções que ocorreram no hello últimas 24 horas. 

> [!TIP]
> Se você vir "0 exceções" em CodeLens, mas você sabe que deve haver exceções, verifique toomake se o recurso do Application Insights à direita de saudação é selecionado na CodeLens. tooselect outro recurso, clique com botão direito no seu projeto no Gerenciador de soluções do hello e escolha **Application Insights > Escolher fonte de telemetria**. CodeLens é mostrada apenas para Olá 15 a maioria das exceções que ocorrem com frequência em seu aplicativo em Olá últimas 24 horas, portanto, se uma exceção é Olá frequentemente mais de 16 ou menos, você verá "0 exceções." Exceções de modos de exibição do ASP.NET não podem aparecer em métodos de saudação do controlador que gerou os modos de exibição.
> 
> [!TIP]
> Se vir "? exceções"em CodeLens, você precisa tooassociate que sua conta do Azure com o Visual Studio ou suas credenciais de conta do Azure pode ter expirado. Em ambos os casos, clique em "? exceções"e escolha **adicionar uma conta...**  tooenter suas credenciais.
> 
> 

## <a name="requests-in-codelens"></a>Solicitações no CodeLens
![TBD](./media/app-insights-visual-studio-codelens/codelens-requests.png)

Hello solicitação mostra de indicador CodeLens Olá número de HTTP solicitações que foram atendidas por um método no hello após 24 horas, além de porcentagem Olá dessas solicitações que falharam.

toosee mais detalhes, clique em Olá solicitações CodeLens indicador:

* Olá alterações no número de solicitações, solicitações com falha e tempos de resposta médio absoluto e percentual sobre Olá após 24 horas em comparação comparadas toohello anteriores a 24 horas
* confiabilidade de saudação do método hello, calculado como Olá porcentagem de solicitações que não falhou em Olá últimas 24 horas
* Escolha **pesquisa** solicitações ou solicitações com falha tooquery todos Olá solicitações (falhas) que ocorreram em Olá últimas 24 horas
* Escolha **tendência** tooview uma visualização de tendência para solicitações, solicitações com falha ou médio de resposta vezes em Olá últimas 24 horas.
* Escolha o nome de saudação do hello recurso do Application Insights no canto superior esquerdo de saudação da exibição de detalhes do hello CodeLens toochange qual recurso é a origem de saudação para dados de CodeLens.

## <a name="next"></a>Próximas etapas
|  |  |
| --- | --- |
| **[Trabalhando com o Application Insights no Visual Studio](app-insights-visual-studio.md)**<br/>Pesquisar telemetria, ver dados em CodeLens e configurar o Application Insights. Tudo no Visual Studio. |![Clique com botão direito hello e escolha o Application Insights, pesquisa](./media/app-insights-visual-studio-codelens/34.png) |
| **[Adicionar mais dados](app-insights-asp-net-more.md)**<br/>Monitorar o uso, a disponibilidade, as dependências e as exceções. Integrar rastreamentos de estruturas de logs. Escrever telemetria personalizada. |![Visual Studio](./media/app-insights-visual-studio-codelens/64.png) |
| **[Trabalhando com o portal do Application Insights Olá](app-insights-dashboards.md)**<br/>Painéis, poderosas ferramentas de diagnóstico e análise, alertas, um mapa de dependências em tempo real de seu aplicativo e a exportação de telemetria. |![Visual Studio](./media/app-insights-visual-studio-codelens/62.png) |

