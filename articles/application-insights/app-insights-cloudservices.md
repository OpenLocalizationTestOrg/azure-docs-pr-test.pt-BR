---
title: "aaaApplication Insights para serviços de nuvem do Azure | Microsoft Docs"
description: "Monitorar suas funções da Web e de trabalho com eficiência com o Application Insights"
services: application-insights
documentationcenter: 
keywords: "WAD2AI, Diagnóstico do Azure"
author: CFreemanwa
manager: carmonm
editor: alancameronwills
ms.assetid: 5c7a5b34-329e-42b7-9330-9dcbb9ff1f88
ms.service: application-insights
ms.devlang: na
ms.tgt_pltfrm: ibiza
ms.topic: get-started-article
ms.workload: tbd
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 6956ce423eea1e2cf387bd98250bae32d9501ed0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-azure-cloud-services"></a>Application Insights para Serviços de Nuvem do Azure
[Os aplicativos do serviço de nuvem do Microsoft Azure](https://azure.microsoft.com/services/cloud-services/) podem ser monitorados pelo [Application Insights][start] para ver a disponibilidade, desempenho, falhas e uso combinando os dados dos SDKs do Application Insights com os dados de [Diagnóstico do Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) em seus Serviços de Nuvem. Feedback Olá que obter sobre desempenho hello e a eficácia do seu aplicativo em Olá curinga, você pode fazer escolhas informadas sobre a direção de saudação do design de saudação em cada ciclo de vida de desenvolvimento.

![Exemplo](./media/app-insights-cloudservices/sample.png)

## <a name="before-you-start"></a>Antes de começar
Você precisará de:

* Uma assinatura do [Microsoft Azure](http://azure.com). Entre com uma conta da Microsoft, que você pode ter para o Windows, XBox Live ou outros serviços de nuvem da Microsoft. 
* Ferramentas do Microsoft Azure 2.9 ou posteriores
* Developer Analytics Tools 7.10 ou posteriores

## <a name="quick-start"></a>Início rápido
Olá toomonitor de maneira mais rápida e fácil que seu serviço de nuvem com o Application Insights é toochoose opção quando você publica seu tooAzure de serviço.

![Exemplo](./media/app-insights-cloudservices/azure-cloud-application-insights.png)

Este instrumentos opção contadores de seu aplicativo em tempo de execução fornecendo toda a telemetria Olá precisar toomonitor solicitações, exceções e suas dependências em sua função web como o desempenho de suas funções de trabalho. Qualquer rastreamentos de diagnóstico gerados pelo seu aplicativo também são enviados tooApplication Insights.

Se isso for tudo o que você precisa, você está pronto! As próximas etapas são [exibição das métricas do seu aplicativo](app-insights-metrics-explorer.md), [consulta de seus dados com o Analytics](app-insights-analytics.md) e talvez a configuração de um [painel](app-insights-dashboards.md). Talvez você queira tooset backup [testes de disponibilidade](app-insights-monitor-web-app-availability.md) e [adicionar as páginas de código tooyour web](app-insights-javascript.md) toomonitor desempenho no navegador de saudação.

Mas você também pode obter mais opções:

* Enviar dados de diferentes componentes e recursos de tooseparate de configurações de compilação.
* Adicione telemetria personalizada do seu aplicativo.

Se essas opções são de interesse tooyou, continue a leitura.

## <a name="sample-application-instrumented-with-application-insights"></a>Aplicativo de exemplo instrumentado com o Application Insights
Dê uma olhada no [aplicativo de exemplo](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) no qual Application Insights é adicionado tooa serviço de nuvem com duas funções de trabalho hospedadas no Azure. 

Os itens a seguir informa como tooadapt seu próprio serviço de nuvem do projeto no hello mesma maneira.

## <a name="plan-resources-and-resource-groups"></a>Planejar recursos e grupos de recursos
Telemetria de saudação do seu aplicativo é armazenada, analisada e exibida em um recurso do Azure do tipo do Application Insights. 

Cada recurso pertence tooa grupo de recursos. Grupos de recursos são usados para gerenciar custos, para conceder acesso a membros de tooteam e toodeploy atualizações em uma única transação coordenada. Por exemplo, você poderia [gravar um script toodeploy](../azure-resource-manager/resource-group-template-deploy.md) um serviço de nuvem do Azure e seus recursos em uma operação de monitoramento do Application Insights.

### <a name="resources-for-components"></a>Recursos para componentes
Olá recomendado é de esquema toocreate um recurso separado para cada componente do aplicativo - ou seja, cada função web e função de trabalho. Você pode analisar cada componente separadamente, mas pode criar um [painel](app-insights-dashboards.md) que reúne gráficos-chave Olá de todos os componentes de hello, para que você possa comparar e monitorá-los juntos. 

Um esquema alternativo é toosend telemetria de saudação do toohello de mais de uma função mesmo recurso, mas [adicionar um item de telemetria de tooeach de propriedade de dimensão](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer) que identifica sua função de origem. Nesse esquema, gráficos de métricas, como exceções normalmente mostram uma agregação de contagens de saudação do hello diferentes funções, mas você pode segmentar gráfico Olá pelo identificador de função hello quando necessário. Pesquisas também podem ser filtradas por Olá mesma dimensão. Essa alternativa torna mais fácil tooview tudo no hello ao mesmo tempo, mas também pode causar confusão toosome entre as funções hello.

Telemetria de navegador geralmente está incluída no hello mesmo recurso como sua função do servidor web.

Colocar recursos do Application Insights Olá para diferentes componentes de saudação em um grupo de recursos. Isso torna fácil toomanage-los juntos. 

### <a name="separating-development-test-and-production"></a>A separação de desenvolvimento, teste e produção
Se você estiver desenvolvendo eventos personalizados para o próximo recurso enquanto a versão anterior do hello está ao vivo, você deseja toosend Olá desenvolvimento telemetria tooa Application Insights recurso separado. Caso contrário, será difícil toofind sua telemetria de teste entre todos Olá tráfego do site ao vivo hello.

tooavoid nessa situação, criar recursos separados para cada configuração de compilação ou 'carimbo' (desenvolvimento, teste, produção,...) do seu sistema. Colocar recursos Olá para cada configuração de compilação em um grupo de recursos separado. 

toosend Olá telemetria toohello os recursos adequados, você pode configurar Olá SDK do Application Insights para que ele escolhe uma chave de instrumentação diferentes dependendo da configuração de compilação de saudação. 

## <a name="create-an-application-insights-resource-for-each-role"></a>Criar um recurso do Application Insights para cada função
Se você decidir toocreate um recurso separado para cada função - talvez um separado é definido para cada configuração de build - e é mais fácil toocreate-los todos no portal do Application Insights de saudação. (Se você criar recursos muito, você pode [automatizar o processo de saudação](app-insights-powershell.md).

1. Em Olá [portal do Azure][portal], criar um novo recurso do Application Insights. Para o tipo de aplicativo, escolha o aplicativo ASP.NET. 

    ![Clique em Novo, Application Insights](./media/app-insights-cloudservices/01-new.png)
2. Observe que recurso é identificado por uma Chave de Instrumentação. Talvez seja necessário isso mais tarde, se você quiser toomanually configure ou verifique a configuração de saudação do hello SDK.

    ![Clique em propriedades, selecione a chave de saudação e pressione ctrl + C](./media/app-insights-cloudservices/02-props.png) 

## <a name="set-up-azure-diagnostics-for-each-role"></a>Configurar o diagnóstico do Azure para cada função
Defina essa opção toomonitor seu aplicativo com o Application Insights. Para funções web, isso fornece monitoramento de desempenho, alertas e diagnóstico, bem como análise de uso. Para outras funções, você pode pesquisar e monitorar o diagnóstico do Azure, como reinicialização, contadores de desempenho e chamadas tooSystem.Diagnostics.Trace. 

1. No Gerenciador de soluções do Visual Studio, em &lt;YourCloudService&gt;, funções, abra as propriedades de saudação de cada função.
2. Em **configuração**, defina **enviar dados de diagnóstico tooApplication Insights** e selecione Olá recurso Application Insights apropriado que você criou anteriormente.

Se você tiver decidido toouse um recurso do Application Insights separado para cada configuração de compilação, selecione configuração Olá primeiro.

![Nas propriedades de saudação de cada função do Azure, configurar o Application Insights](./media/app-insights-cloudservices/configure-azure-diagnostics.png)

Isso tem efeito de saudação de inserção suas chaves de instrumentação do Application Insights Olá arquivos denominados `ServiceConfiguration.*.cscfg`. ([Exemplo de código](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/AzureEmailService/ServiceConfiguration.Cloud.cscfg)).

Se desejar que o nível de saudação toovary de informações de diagnóstico enviadas tooApplication Insights, você pode fazer isso [editando Olá `.cscfg` arquivos diretamente](app-insights-azure-diagnostics.md).

## <a name="sdk"></a>Instalar Olá SDK em cada projeto
Essa opção adiciona Olá capacidade tooadd comercial personalizada telemetria tooany função, para uma análise mais próxima de como seu aplicativo é usado e executa.

No Visual Studio, configure Olá SDK do Application Insights para cada projeto de aplicativo de nuvem.

1. **Funções Web**: clique com botão direito hello e escolha **configurar o Application Insights** ou **Adicionar > telemetria do Application Insights**.

2. **Funções de trabalho**: 
 * Clique com botão direito hello e selecione **gerenciar pacotes Nuget**.
 * Adicione [Application Insights para Windows Servers](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/).

    ![Pesquise “Application Insights”](./media/app-insights-cloudservices/04-ai-nuget.png)

3. Configure Olá SDK toosend dados toohello recurso do Application Insights.

    Em uma função de inicialização adequado, defina chave de instrumentação de saudação da configuração Olá no arquivo. cscfg de saudação:
 
    ```C#
   
     TelemetryConfiguration.Active.InstrumentationKey = RoleEnvironment.GetConfigurationSettingValue("APPINSIGHTS_INSTRUMENTATIONKEY");
    ```
   
    Faça isso para cada função em seu aplicativo. Consulte exemplos de saudação:
   
   * [Função Web](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Global.asax.cs#L27)
   * [Função de trabalho](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L232)
   * [Para páginas da Web](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Views/Shared/_Layout.cshtml#L13) 
4. Conjunto Olá applicationinsights. config arquivo toobe sempre copiadas toohello diretório de saída. 
   
    (No arquivo. config de saudação, você verá mensagens para que você tooplace Olá instrumentação chave existe. No entanto, para aplicativos em nuvem é melhor tooset do arquivo. cscfg de saudação. Isso garante que função hello é identificada corretamente no portal de saudação).

#### <a name="run-and-publish-hello-app"></a>Executar e publicar o aplicativo hello
Execute o aplicativo e entre no Azure. Recursos do Application Insights Olá abertos que você criou, e você verá os pontos de dados individuais que aparecem em [pesquisa](app-insights-diagnostic-search.md), e os dados agregados em [Explorer métrica](app-insights-metrics-explorer.md). 

Adicionar mais telemetria - consulte Olá seções abaixo - e, em seguida, publicar seu aplicativo tooget ao vivo de diagnóstico e uso de comentários. 

#### <a name="no-data"></a>Não há dados?
* Olá abrir [pesquisa] [ diagnostic] lado a lado, eventos de toosee individuais.
* Use o aplicativo hello, páginas diferentes de abertura para que ele gera algumas telemetria.
* Aguarde alguns segundos e clique em Atualizar.
* Consulte [Solução de problemas][qna].

## <a name="view-azure-diagnostic-events"></a>Exibir eventos de Diagnóstico do Azure
Onde Olá toofind [diagnóstico do Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) informações no Application Insights:

* Os contadores de desempenho são exibidos como métricas personalizadas. 
* Os logs de eventos do Windows são mostrados como eventos de rastreamentos e personalizados.
* Logs do aplicativo, logs de ETW e todos os logs de infraestrutura de diagnóstico são exibidos como rastreamentos.

contadores de desempenho de toosee e contagens de eventos, abra [Metrics Explorer](app-insights-metrics-explorer.md) e adicionar um novo gráfico:

![Dados de diagnóstico do Azure](./media/app-insights-cloudservices/23-wad.png)

Use [pesquisa](app-insights-diagnostic-search.md) ou um [consulta analítica](app-insights-analytics-tour.md) toosearch em Olá vários logs enviados pelo diagnóstico do Azure de rastreamento. Por exemplo, suponha que você tem uma exceção sem tratamento que causou uma função toocrash e reciclagem. Essas informações seriam mostradas em Olá aplicativo canal de Log de eventos Windows. Você pode usar pesquisa toolook em Olá erro de Log de eventos do Windows e obter o rastreamento de pilha completos Olá para exceção hello. Que ajudarão você a encontrar a causa raiz de saudação do problema de saudação.

![Pesquisa de diagnóstico do Azure](./media/app-insights-cloudservices/25-wad.png)

## <a name="more-telemetry"></a>Mais telemetria
Olá seções a seguir mostram como tooget a telemetria adicionais em diferentes aspectos do seu aplicativo.

## <a name="track-requests-from-worker-roles"></a>Acompanhar as solicitações das funções de trabalho
Em funções da web, Olá solicitações módulo automaticamente coleta dados sobre solicitações HTTP. Consulte Olá [MVCWebRole de exemplo](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole) para obter exemplos de como você pode substituir o comportamento de coleção saudação padrão. 

Você pode capturar o desempenho Olá das funções de tooworker chamadas rastreando-los no hello mesma maneira que as solicitações HTTP. No Application Insights, o tipo de telemetria de solicitação Olá mede uma unidade de trabalho nomeada do lado do servidor que pode ser atingiu o tempo e pode independentemente tenha êxito ou falha. Enquanto as solicitações HTTP são capturadas automaticamente pelo Olá SDK, você pode inserir suas próprias funções de tooworker código tootrack solicitações.

Consulte Olá dois exemplo trabalho funções tooreport instrumentado solicitações: [WorkerRoleA](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleA) e [WorkerRoleB](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleB)

## <a name="exceptions"></a>Exceções
Consulte [Monitoramento de exceções no Application Insights](app-insights-asp-net-exceptions.md) para obter informações sobre como você pode coletar exceções sem tratamento de diferentes tipos de aplicativos Web.

função de web de exemplo Hello tem controladores MVC5 e API Web 2. Olá Olá duas exceções sem tratamento são capturadas com hello manipuladores a seguir:

* Configuração do [AiHandleErrorAttribute](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiHandleErrorAttribute.cs) [aqui](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/FilterConfig.cs#L12) para controladores MVC5
* Configuração do [AiWebApiExceptionLogger](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiWebApiExceptionLogger.cs) [aqui](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/WebApiConfig.cs#L25) para controladores da API Web 2

Funções de trabalho, há duas maneiras tootrack exceções:

* TrackException(ex)
* Se você tiver adicionado o pacote NuGet de ouvinte de rastreamento do hello Application Insights, você pode usar **Trace** toolog exceções. [Exemplo de código.](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L107)

## <a name="performance-counters"></a>Contadores de desempenho
Olá contadores a seguir é coletado por padrão:

    * \Process(??APP_WIN32_PROC??)\% Tempo do Processador
    * \Memória\Bytes Disponíveis
    * \.Exceções NET CLR (?. APP_CLR_PROC?)\# de exceções lançadas / s
    * \Processo(??APP_WIN32_PROC??)\Bytes Privados
    * \Processo(??APP_WIN32_PROC??)\Bytes de dados de ES/s
    * \Processador(_Total)\% Tempo do processador

Para funções web, esses contadores também são coletados:

    * \Aplicativos ASP.NET(??APP_W3SVC_PROC??)\Solicitções/S
    * \Aplicativos ASP.NET (?. APP_W3SVC_PROC?)\Tempo de Execução de Solicitação
    * \Aplicativos ASP.NET (?. APP_W3SVC_PROC?)\Solicitações na Fila do Aplicativo

É possível especificar contadores de desempenho adicionais, personalizados ou do Windows editando ApplicationInsights.config, [como neste exemplo](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/ApplicationInsights.config#L14).

  ![Contadores de desempenho](./media/app-insights-cloudservices/OLfMo2f.png)

## <a name="correlated-telemetry-for-worker-roles"></a>Telemetria correlacionada para funções de trabalho
É uma experiência avançada de diagnóstica, quando você pode ver quais led tooa falha ou a solicitação de alta latência. Com as funções da web, Olá entre que SDK configura automaticamente a correlação telemetria relacionada. Funções de trabalho, você pode usar um inicializador de telemetria personalizada tooset um atributo de contexto Operation.Id comum para todos os tooachieve de telemetria Olá isso. Isso permite que você toosee se o problema do hello latência/falha foi causado devido a dependência de tooa ou seu código em um relance! 

Faça assim:

* Definir a Id de correlação de saudação em um CallContext conforme mostrado [aqui](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L36). Nesse caso, estamos usando Olá ID da solicitação como id de correlação de saudação
* Adicione uma implementação personalizada de TelemetryInitializer, tooset Olá Operation.Id toohello correlationId definido acima. Há um exemplo aqui: [ItemCorrelationTelemetryInitializer](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/Telemetry/ItemCorrelationTelemetryInitializer.cs#L13)
* Adicione o inicializador de telemetria personalizada de saudação. Você pode fazer isso no arquivo applicationinsights. config de hello, ou no código conforme mostrado [aqui](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L233)

É isso! experiência do portal Hello está já conectada toohelp que você ver todos os respectivos telemetria rapidamente:

![Telemetria correlacionada](./media/app-insights-cloudservices/bHxuUhd.png)

## <a name="client-telemetry"></a>Telemetria do cliente
[Adicionar Olá páginas de web do SDK de JavaScript tooyour] [ client] tooget baseados em navegador telemetria como contagens de exibição de página, tempos de carregamento de página, as exceções de script e toolet você escrever telemetria personalizada em seus scripts de página.

## <a name="availability-tests"></a>Testes de disponibilidade
[Configurar testes da web] [ availability] toomake-se de que seu aplicativo permanece em tempo real e responsivo.

## <a name="display-everything-together"></a>Exibir tudo juntos
tooget uma visão geral do sistema, você pode colocar chave Olá gráficos de monitoramento juntos em um [painel](app-insights-dashboards.md). Por exemplo, você pode fixar solicitação hello e contagens de falha de cada função. 

Se o sistema usa outros serviços do Azure, como o Stream Analytics, inclua seus gráficos de monitoramento também. 

Se você tiver um aplicativo móvel do cliente, insira alguns eventos personalizados do código toosend em operações de chave de usuário e criar um [HockeyApp ponte](app-insights-hockeyapp-bridge-app.md). Criar consultas em [análise](app-insights-analytics.md) toodisplay Olá contagens dos eventos e fixá-los toohello painel.

## <a name="example"></a>Exemplo
[exemplo Hello](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) monitora um serviço que tem uma função web e duas funções de trabalho.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Exceção "método não encontrado" em execução nos Serviços de Nuvem do Azure
Você compilou para .NET 4.6? O 4.6 não tem suporte automático nas funções dos Serviços de Nuvem do Azure. [Instale o 4.6 em cada função](../cloud-services/cloud-services-dotnet-install-dotnet.md) antes de executar seu aplicativo.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Próximas etapas
* [Configurar o envio de informações de tooApplication de diagnóstico do Azure](app-insights-azure-diagnostics.md)
* [Automatizar a criação de recursos do Application Insights](app-insights-powershell.md)
* [Automatizar o diagnóstico do Azure](app-insights-powershell-azure-diagnostics.md)
* [Funções do Azure](https://github.com/christopheranderson/azure-functions-app-insights-sample)

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[azure]: app-insights-azure.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[netlogs]: app-insights-asp-net-trace-logs.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md 
