---
title: aaaMonitor uso com o Application Insights e a integridade de seu aplicativo
description: "Introdução ao Application Insights. Analise o uso, disponibilidade e desempenho de seu local ou aplicativos do Microsoft Azure."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a>Monitore o desempenho em aplicativos da web


Certifique-se de que seu aplicativo está sendo bem executado, e saiba rapidamente sobre quaisquer falhas. [Application Insights] [ start] será informam sobre quaisquer problemas de desempenho e exceções e causas raiz de ajudam você a localiza e diagnosticar hello.

O Application Insights pode monitorar serviços e aplicativos Web Java e ASP.NET e serviços WCF. Eles podem ser hospedados localmente, em máquinas virtuais ou como sites do Microsoft Azure. 

No lado do cliente hello, Application Insights pode levar a telemetria de páginas da web e uma ampla variedade de dispositivos, incluindo iOS, Android e aplicativos da Windows Store.

>[!Note]
> Disponibilizamos uma nova experiência para encontrar páginas de desempenho lento em seu aplicativo Web. Se você não tiver acesso tooit, habilitá-lo ao configurar as opções de visualização com hello [folha de visualização](app-insights-previews.md). Leia sobre essa nova experiência em [localizar e corrigir afunilamentos de desempenho com investigações de desempenho interativa Olá](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).

## <a name="setup"></a>Configurar o monitoramento de desempenho
Se você ainda não adicionou tooyour Application Insights (ou seja, se ele não tem applicationinsights. config) do projeto, escolha uma destas maneiras tooget iniciado:

* [Aplicativos Web ASP.NET](app-insights-asp-net.md)
  * [Adicionar monitoramento de exceção](app-insights-asp-net-exceptions.md)
  * [Adicionar monitoramento de dependência](app-insights-monitor-performance-live-website-now.md)
* [Aplicativos Web J2EE](app-insights-java-get-started.md)
  * [Adicionar monitoramento de dependência](app-insights-java-agent.md)

## <a name="view"></a>Explorando métricas de desempenho
Em [Olá portal do Azure](https://portal.azure.com), procure o recurso do Application Insights toohello que você configurou para seu aplicativo. folha de visão geral de saudação mostra dados de desempenho básicos:

Clique em qualquer toosee gráfico mais detalhes e os resultados de toosee por um período maior. Por exemplo, clique em bloco de solicitações de saudação e, em seguida, selecione um intervalo de tempo:

![Clicar em toomore dados e selecione um intervalo de tempo](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

Clique em um gráfico toochoose quais métricas ele exibe, ou adicionar um novo gráfico e selecione suas métricas:

![Clique em métricas de toochoose um gráfico](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> **Desmarque todas as métricas de saudação** toosee Olá completo seleção disponível. métricas de saudação se encaixam em grupos; Quando qualquer membro de um grupo é selecionado, somente hello outros membros do grupo aparecem.

## <a name="metrics"></a>O que significa tudo isso? Blocos e relatórios de desempenho
Há várias métricas de desempenho que você pode obter. Vamos começar com aqueles que aparecem por padrão na folha de aplicativo hello.

### <a name="requests"></a>Solicitações
número de saudação de solicitações HTTP recebidas em um período especificado. Compare isso com resultados de saudação em outros toosee relatórios como o seu aplicativo se comporta como carga de saudação varia.

As solicitações HTTP incluem todas as solicitações GET ou POST para páginas, dados e imagens.

Clique em Olá bloco tooget contagens de URLs específicas.

### <a name="average-response-time"></a>Tempo médio de resposta
Tempo de saudação de medidas entre uma solicitação da web inserir sua resposta de aplicativo e hello está sendo retornada.

pontos Olá mostram a movimentação de uma média. Se houver muitas solicitações, pode haver alguns desvio da média de saudação sem um horário de pico óbvio ou ficarem no gráfico de saudação.

Procure por picos incomuns. Em geral, espera toorise de tempo de resposta com um aumento nas solicitações. Se o aumento de saudação desproporcional, seu aplicativo pode ser atingir um limite de recursos, como a capacidade de CPU ou saudação de um serviço que ele usa.

Clique em tempos de tooget Olá lado a lado para URLs específicas.

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a>Solicitações mais lentas
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

Mostra quais solicitações podem precisar de sintonização de desempenho.

### <a name="failed-requests"></a>Solicitações falhas
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

Uma contagem de solicitações que gerou exceções não capturadas.

Clique em Olá bloco toosee Olá detalhes de falhas específicas e selecione uma solicitação individual toosee seus detalhes. 

Somente uma amostra representativa de falhas é retida para inspeção individual.

### <a name="other-metrics"></a>Outras métricas
toosee que outras métricas, você pode exibir, clique em um gráfico e, em seguida, desmarque Olá métricas toosee Olá completo disponível definidos. Clique em (i) toosee definição de cada métrica.

![Desmarque todas as métricas toosee Olá todo o conjunto](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

Outras pessoas que não pode aparecer em qualquer Olá métrica desabilita a seleção Olá mesmo gráfico.

## <a name="set-alerts"></a>Definir alertas
toobe notificado por email sobre valores incomuns de alguma das métricas, adicionar um alerta. Você pode escolher os administradores de contas toohello de email Olá toosend ou toospecific endereços de email.

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

Defina outras propriedades do recurso de saudação antes de saudação. Não escolha a recursos de webtest Olá se você quiser tooset alertas em métricas de uso ou de desempenho.

Ser unidades de saudação toonote cuidado em que você for questionado tooenter valor de limite de saudação.

*Não vejo o botão de alerta de adicionar hello.* -Este é um toowhich de conta de grupo têm acesso somente leitura? Verifique com o administrador da conta hello.

## <a name="diagnosis"></a>Diagnosticando problemas
Aqui estão algumas dicas para localizar e diagnosticar problemas de desempenho:

* Configurar [testes na web] [ availability] toobe alertado se seu site é desativado ou responde lentamente ou incorretamente. 
* Compare contagem de solicitações de saudação com outra métricas toosee se falhas ou resposta lenta tooload relacionado.
* [Inserir e instruções de rastreamento de pesquisa] [ diagnostic] no seu código toohelp a identificar problemas.
* Monitore seu aplicativo Web em operação com o [Live Metrics Stream][livestream].
* Capturar o estado de saudação do seu aplicativo .net com [instantâneo depurador][snapshot].

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a>Encontrar e corrigir afunilamentos de desempenho com uma investigação de desempenho interativo

Você pode usar o hello novo Application Insights interativo investigação toolocate áreas de desempenho de seu aplicativo Web que estão prejudicando o desempenho geral. Você pode rapidamente localizar páginas específicas que estão diminuindo e usam Olá [ferramenta de criação de perfil](app-insights-profiler.md) toosee se não houver uma correlação entre essas páginas.

### <a name="create-a-list-of-slow-performing-pages"></a>Criar uma lista de páginas de desempenho lento 

Olá primeira etapa para localizar problemas de desempenho é tooget uma lista de saudação lenta de páginas de responder. Olá captura tela abaixo demonstra como usar o hello desempenho folha tooget uma lista de possíveis tooinvestigate páginas adicionais. Você pode ver rapidamente nesta página que houve um retardar no tempo de resposta de saudação do aplicativo hello em cerca de 6:00 PM e novamente em aproximadamente 10 PM. Você também pode ver que a operação de detalhes do cliente GET hello sofreu algum tempo executando operações com um tempo de resposta médio de 507.05 milissegundos. 

![Desempenho interativo do Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a>Fazer uma busca detalhada em páginas específicas

Depois de obter um instantâneo do desempenho do aplicativo, você pode obter mais detalhes sobre operações específicas de desempenho lento. Clique em qualquer operação em Olá lista toosee Olá detalhes conforme mostrado abaixo. Gráfico de saudação você pode ver se o desempenho de saudação foi baseado em uma dependência. Você também pode ver quantos Olá experientes de usuários vários tempos de resposta. 

![Folha Operações do Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a>Fazer uma busca detalhada em um período específico

Depois de identificar um ponto no tempo tooinvestigate, aprofunde ainda mais toolook em operações específicas de saudação que possam ter causado retardar de desempenho de saudação. Quando você clica em um ponto específico no tempo você obter detalhes de saudação da página Olá conforme mostrado abaixo. No hello exemplo abaixo, você pode ver operações Olá listadas para um determinado período de tempo junto com os códigos de resposta do servidor de saudação e a duração da operação de saudação. Você também tem Olá url para abrir um item de trabalho do TFS, se você precisar toosend essa equipe de desenvolvimento tooyour informações.

![Fração de tempo do Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a>Fazer uma busca detalhada em uma operação específica

Depois de identificar um ponto no tempo tooinvestigate, aprofunde ainda mais toolook em operações específicas de saudação que possam ter causado retardar de desempenho de saudação. Clique em uma operação de saudação listar toosee Olá detalhes da operação Olá conforme mostrado abaixo. Neste exemplo, que você pode ver que falha na operação de saudação e do Application Insights fornece detalhes de saudação do hello aplicativo hello de exceção gerou. Novamente, é possível criar um item de trabalho do TFS com facilidade nesta folha.

![Folha Operação do Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <a name="next"></a>Próximas etapas
[Testes na Web] [ availability] -solicitações da web enviaram tooyour aplicativo em intervalos regulares do mundo hello.

[Capturar e pesquisar rastreamentos de diagnóstico] [ diagnostic] - inserir chamadas de rastreamento e examinar os problemas de toopinpoint Olá resultados.

[Acompanhamento de uso][usage] – Saiba como as pessoas usam seu aplicativo.

[Solução de problemas][qna] – e P e R



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



