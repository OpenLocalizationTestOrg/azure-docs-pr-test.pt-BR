---
title: aaaDependency controle no Azure Application Insights | Microsoft Docs
description: Analise o uso, disponibilidade e desempenho de seu local ou um aplicativo Web do Microsoft Azure com o Application Insights.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a>Configurar o Application Insights: acompanhamento de dependências
Um *dependência* é um componente externo que é chamado por seu aplicativo. Normalmente, ele é um serviço chamado usando HTTP, um banco de dados ou um sistema de arquivos. O [Application Insights](app-insights-overview.md) mede por quanto tempo o aplicativo aguarda dependências e com que frequência uma chamada de dependência falha. Você pode investigar chamadas específicas e relacioná-los toorequests e exceções.

![gráficos de exemplo](./media/app-insights-asp-net-dependencies/10-intro.png)

monitor de dependência de caixa Olá atualmente relata chamadas toothese tipos de dependências:

* Servidor
  * Bancos de dados SQL
  * Serviços Web ASP.NET e WCF que usam associações baseadas em HTTP
  * Chamadas HTTP locais ou remotas
  * Azure Cosmos DB, tabela, Armazenamento de Blobs e fila
* Páginas da Web
  * Chamadas AJAX

O monitoramento funciona com o uso da [instrumentação de código de byte](https://msdn.microsoft.com/library/z9z62c29.aspx) nos métodos selecionados. A sobrecarga de desempenho é mínima.

Você também pode escrever seu próprios SDK chamadas toomonitor outras dependências, ambos no código de cliente e servidor hello, usando Olá [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

## <a name="set-up-dependency-monitoring"></a>Configurar o monitoramento de dependência
Informações de dependência parcial são coletadas automaticamente pelo Olá [SDK do Application Insights](app-insights-asp-net.md). tooget completa dos dados, instale o agente de apropriada de Olá para o servidor de host de saudação.

| Plataforma | Instalar |
| --- | --- |
| Servidor IIS |O [instalar o Monitor de Status em seu servidor](app-insights-monitor-performance-live-website-now.md) ou [atualizar a estrutura de too.NET aplicativo 4.6 ou posterior](http://go.microsoft.com/fwlink/?LinkId=528259) e instalar Olá [SDK do Application Insights](app-insights-asp-net.md) em seu aplicativo. |
| Aplicativo Web do Azure |No painel de controle de aplicativo web, [folha do Application Insights Olá aberto no painel de controle de aplicativo web](app-insights-azure-web-apps.md) e escolha a instalação se solicitado. |
| Serviço de Nuvem do Azure |[Usar tarefa de inicialização](app-insights-cloudservices.md) ou [Instalar o .NET Framework 4.6 +](../cloud-services/cloud-services-dotnet-install-dotnet.md) |

## <a name="where-toofind-dependency-data"></a>Onde os dados de dependência de toofind
* O [Mapa de Aplicativo](#application-map) visualiza as dependências entre seu aplicativo e os componentes de vizinhança.
* As [folhas de desempenho, de navegador e de falha](#performance-and-blades) mostram dados de dependência de servidor.
* A [folha de navegadores](#ajax-calls) mostra chamadas AJAX de navegadores dos usuários.
* [Clique em por meio de solicitações com falha ou lentas](#diagnose-slow-requests) toocheck sua dependência chama.
* [Análise de](#analytics) pode ser usado tooquery dados de dependência.

## <a name="application-map"></a>Mapa de aplicativo
Mapa de aplicativo atua como um toodiscovering de auxílio visual dependências entre componentes de saudação do seu aplicativo. Ele é gerado automaticamente da telemetria de saudação do seu aplicativo. Este exemplo mostra chamadas AJAX de scripts de navegador hello e chamadas REST do servidor de saudação serviços externos de tootwo de aplicativo.

![Mapa de aplicativo](./media/app-insights-asp-net-dependencies/08.png)

* **Navegue nas caixas Olá** toorelevant dependência e outros gráficos.
* **Mapa de saudação do PIN** toohello [painel](app-insights-dashboards.md), onde ele será totalmente funcional.

[Saiba mais](app-insights-app-map.md).

## <a name="performance-and-failure-blades"></a>Folhas de falha e de desempenho
folha de desempenho Olá mostra a duração de saudação de chamadas de dependência feitas pelo aplicativo do servidor de saudação. Há um gráfico de resumo e uma tabela segmentadas por chamada.

![Gráficos de dependência de folha de desempenho](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

Clique nos gráficos de resumo de saudação ou Olá tabela itens toosearch bruto ocorrências dessas chamadas.

![Instâncias de chamada de dependência](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

**Contagens de falha** são mostrados em Olá **falhas** folha. Uma falha é qualquer código de retorno não está no intervalo de saudação 200-399, ou desconhecido.

> [!NOTE]
> **Falhas de 100%?** - Isso provavelmente indica que você está apenas obtendo dados de dependência parcial. É necessário muito[configurar dependência monitoramento plataforma apropriada tooyour](#set-up-dependency-monitoring).
>
>

## <a name="ajax-calls"></a>Chamadas AJAX
folha de navegadores Olá mostra a duração de saudação e taxa de falha de AJAX chama de [JavaScript nas páginas da web](app-insights-javascript.md). Elas são mostradas como Dependências.

## <a name="diagnosis"></a> Diagnosticar solicitações lentas
Cada evento de solicitação associado com chamadas de dependência hello, Olá exceções e outros eventos que são rastreados enquanto seu aplicativo está processando a solicitação. Portanto, se algumas solicitações são com baixo desempenho, você pode descobrir se ela é devido as respostas tooslow uma dependência.

Vamos examinar um exemplo disso.

### <a name="tracing-from-requests-toodependencies"></a>Rastreamento de solicitações toodependencies
Abra a folha de desempenho de saudação e examine a grade de saudação de solicitações:

![Lista de solicitações com contagens e médias](./media/app-insights-asp-net-dependencies/02-reqs.png)

superior Olá um está demorando muito. Vamos ver se podemos pode descobrir onde o tempo de saudação é gasto.

Clique em eventos de solicitação individual de toosee essa linha:

![Lista de ocorrências de solicitação](./media/app-insights-asp-net-dependencies/03-instances.png)

Clique em qualquer tooinspect de instância de execução longa ainda mais e role para baixo toohello dependência remoto chamadas relacionadas toothis solicitação:

![Localizar chamadas tooRemote dependências, identifique a duração incomuns](./media/app-insights-asp-net-dependencies/04-dependencies.png)

Parece que a maioria das Olá tempo atendendo a que essa solicitação foi gasta em um serviço local de tooa de chamada.

Selecione essa linha tooget obter mais informações:

![Clique nas que responsável de saudação tooidentify dependência remoto](./media/app-insights-asp-net-dependencies/05-detail.png)

Parece que este é onde está o problema de saudação. Nós já é identificar o problema de saudação, portanto agora simplesmente necessário toofind out por essa chamada está demorando muito tempo.

### <a name="request-timeline"></a>Linha do tempo da solicitação
Em outro caso, não há nenhuma chamada de dependência que seja tão longa. Mas, alternando o modo de exibição de tempo de toohello, podemos ver onde o atraso de saudação ocorreu no nosso processamento interno:

![Localizar chamadas tooRemote dependências, identifique a duração incomuns](./media/app-insights-asp-net-dependencies/04-1.png)

Parece toobe uma grande diferença após a primeira chamada de dependência hello, portanto deve observarmos nossa toosee código por que isto é.

### <a name="profile-your-live-site"></a>Perfil de seu site ativo

Não sabe onde o tempo de saudação vai? Olá [criador de perfil do Application Insights](app-insights-profiler.md) rastreamentos HTTP chama o site ao vivo tooyour e mostra quais funções em seu código levaram tempo mais longo de saudação.

## <a name="failed-requests"></a>Solicitações falhas
Solicitações com falha também podem ser associadas com toodependencies de chamadas com falha. Novamente, estamos pode clicar tootrack problema hello.

![Clique em gráfico de solicitações com falha Olá](./media/app-insights-asp-net-dependencies/06-fail.png)

Clique nas tooan ocorrência de uma solicitação com falha e examinar seus eventos associados.

![Clique em um tipo de solicitação, clique em Olá instância tooget tooa exibição diferente dos Olá a mesma instância, clique em detalhes da exceção tooget.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a>Análise
Você pode rastrear dependências em Olá [linguagem de consulta de análise de Log](https://docs.loganalytics.io/). Veja alguns exemplos.

* Localize todas as chamadas com falha de dependência:

```

    dependencies | where success != "True" | take 10
```

* Localize as chamadas AJAX:

```

    dependencies | where client_Type == "Browser" | take 10
```

* Localize as chamadas de dependência associadas a solicitações:

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* Localize as chamadas do AJAX associadas a exibições de página:

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a>Acompanhamento de dependência personalizado
módulo de controle de dependência padrão Olá descobre automaticamente as dependências externas, como bancos de dados e APIs REST. Mas talvez você queira toobe alguns componentes adicionais tratado no hello mesma maneira.

Você pode escrever código que envia informações de dependência usando Olá mesmo [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) que é usado pelos módulos de saudação padrão.

Por exemplo, se você compilar seu código com um assembly que não gravar por conta própria, você poderia tempo tooit de chamadas Olá todos os, toofind out que contribuição faz resposta tooyour vezes. toohave esses dados exibidos em gráficos de dependência Olá no Application Insights, enviá-lo usando `TrackDependency`.

```C#

            var startTime = DateTime.UtcNow;
            var timer = System.Diagnostics.Stopwatch.StartNew();
            try
            {
                success = dependency.Call();
            }
            finally
            {
                timer.Stop();
                telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
            }
```

Se você quiser tooswitch fora do módulo de controle de dependência padrão hello, remover Olá referência tooDependencyTrackingTelemetryModule em [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md).

## <a name="troubleshooting"></a>Solucionar problemas
*O sinalizador de êxito da dependência sempre mostra true ou false.*

*Consulta SQL não mostrada por completo.*

* Atualize a versão mais recente toohello de saudação SDK. Se sua versão do .NET for inferior à 4.6:
  * Host de IIS: instalar [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) nos servidores de host de saudação.
  * Aplicativo web do Azure: Abra Application Insights guia no painel de controle de aplicativo de web hello e instale o Application Insights.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Próximas etapas
* [Exceções](app-insights-asp-net-exceptions.md)
* [Dados do usuário e da página](app-insights-javascript.md)
* [Disponibilidade](app-insights-monitor-web-app-availability.md)
