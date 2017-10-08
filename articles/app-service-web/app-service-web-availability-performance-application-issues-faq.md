---
title: desempenho aaaApplication perguntas frequentes para aplicativos web do Azure | Microsoft Docs
description: "Obtenha respostas toofrequently perguntas frequentes sobre disponibilidade, desempenho e problemas de aplicativo no recurso de aplicativos Web de saudação do serviço de aplicativo do Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 7f2383743079e4c630fd548b0efd9993029afe11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-faqs-for-web-apps-in-azure"></a>Perguntas frequentes do desempenho do aplicativo para Aplicativos Web no Azure

Este artigo possui respostas toofrequently perguntas frequentes (FAQs) sobre problemas de desempenho do aplicativo para Olá [recurso de aplicativos Web do serviço de aplicativo do Azure](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-is-my-app-slow"></a>Por que o meu aplicativo está lento?

Vários fatores podem contribuir tooslow o desempenho do aplicativo. Para obter as etapas detalhadas de solução de problemas, consulte [Solucionar problemas de desempenho lento do aplicativo Web](app-service-web-troubleshoot-performance-degradation.md).

## <a name="how-do-i-troubleshoot-a-high-cpu-consumption-scenario"></a>Como solucionar problemas de um cenário de alto consumo de CPU?

Em alguns cenários de alto consumo de CPU, seu aplicativo pode exigir realmente mais recursos de computação. Nesse caso, considere a possibilidade de dimensionamento tooa mais alto nível de serviço para que o aplicativo hello obtém todos os recursos de saudação precisa. Outras vezes, o alto consumo de CPU pode ser causado por um loop ou uma prática de codificação incorretos. Obter informações sobre o que está causando o aumento de consumo da CPU é um processo de duas partes. Primeiro, crie um despejo de processo e, em seguida, analisar o despejo de processo hello. Para obter mais informações, consulte [Capturar e analisar um arquivo de despejo para alto consumo de CPU para aplicativos Web](https://blogs.msdn.microsoft.com/asiatech/2016/01/20/how-to-capture-dump-when-intermittent-high-cpu-happens-on-azure-web-app/).

## <a name="how-do-i-troubleshoot-a-high-memory-consumption-scenario"></a>Como solucionar problemas de um cenário de alto consumo de memória?

Em alguns cenários de alto consumo de memória, seu aplicativo pode exigir realmente mais recursos de computação. Nesse caso, considere a possibilidade de dimensionamento tooa mais alto nível de serviço para que o aplicativo hello obtém todos os recursos de saudação precisa. Outras vezes, um bug no código Olá pode causar um vazamento de memória. Uma prática de codificação também pode aumentar o consumo de memória. Obter informações sobre o que está causando o aumento de consumo da memória é um processo de duas partes. Primeiro, crie um despejo de processo e, em seguida, analisar o despejo de processo hello. Diagnóstico de falha de saudação Galeria de extensões de Site do Azure pode executar com eficiência ambas as seguintes etapas. Para obter mais informações, consulte [Capturar e analisar um arquivo de despejo de memória alta intermitente para aplicativos Web](https://blogs.msdn.microsoft.com/asiatech/2016/02/02/how-to-capture-and-analyze-dump-for-intermittent-high-memory-on-azure-web-app/).

## <a name="how-do-i-automate-app-service-web-apps-by-using-powershell"></a>Como automatizar a Aplicativos Web do Serviço de Aplicativo usando o PowerShell?

Você pode usar toomanage de cmdlets do PowerShell e manter os aplicativos do serviço de aplicativo web. Em nossa postagem do blog [automatizar os aplicativos web hospedados no serviço de aplicativo do Azure usando o PowerShell](https://blogs.msdn.microsoft.com/puneetgupta/2016/03/21/automating-webapps-hosted-in-azure-app-service-through-powershell-arm-way/), descrevemos como tarefas comuns de tooautomate toouse de cmdlets do PowerShell com base no Gerenciador de recursos do Azure. postagem do blog Olá também tem o código de exemplo para várias tarefas de gerenciamento de aplicativos web. Para obter descrições e sintaxe para todos os cmdlets de aplicativos Web do Serviço de Aplicativo, consulte [AzureRM.Websites](https://docs.microsoft.com/powershell/module/azurerm.websites/?view=azurermps-4.0.0).

## <a name="how-do-i-view-my-web-apps-event-logs"></a>Como exibir os logs de eventos do aplicativo web?

logs de eventos do aplicativo web tooview:

1. Entrar tooyour [site Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. No menu de saudação, selecione **Console depuração** > **CMD**.
3. Selecione Olá **LogFiles** pasta.
4. tooview logs de eventos, selecione o ícone de lápis Olá Avançar muito**eventlog.xml**.
5. logs de saudação toodownload, executados o cmdlet do PowerShell Olá `Save-AzureWebSiteLog -Name webappname`.

## <a name="how-do-i-capture-a-user-mode-memory-dump-of-my-web-app"></a>Como capturar um despejo de memória do modo de usuário do meu aplicativo web?

toocapture um despejo de memória do modo de usuário de seu aplicativo web:

1. Entrar tooyour [site Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. Selecione Olá **Process Explorer** menu.
3. Saudação de atalho **w3wp.exe** processo ou seu trabalho Web.
4. Selecione **Baixar o despejo de memória** > **Despejo completo**.

## <a name="how-do-i-view-process-level-info-for-my-web-app"></a>Como exibir informações de nível de processo para meu aplicativo web?

Você tem duas opções para exibir as informações de nível de processo para seu aplicativo web:

*   Em Olá portal do Azure:
    1. Olá abrir **Process Explorer** para o aplicativo web de saudação.
    2. detalhes de saudação toosee, selecione Olá **w3wp.exe** processo.
*   No console do Kudu hello:
    1. Entrar tooyour [site Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
    2. Selecione Olá **Process Explorer** menu.
    3. Para Olá **w3wp.exe** processo, selecione **propriedades**.

## <a name="when-i-browse-toomy-app-i-see-error-403---this-web-app-is-stopped-how-do-i-resolve-this"></a>Ao navegar toomy aplicativo, vejo "Erro 403 - este aplicativo web foi interrompido." Como resolver isso?

Três condições podem causar esse erro:

* aplicativo web de saudação atingiu um limite de cobrança e seu site foi desabilitado.
* aplicativo web de saudação foi interrompido no portal de saudação.
* aplicativo web de saudação atingiu um limite de cota de recursos que pode ser aplicadas tooa gratuito ou compartilhado plano do serviço de escala.

toosee o que está causando o erro hello e problema de saudação tooresolve, Olá siga as etapas em [aplicativos Web: "Erro 403 – este aplicativo web for interrompido"](https://blogs.msdn.microsoft.com/waws/2016/01/05/azure-web-apps-error-403-this-web-app-is-stopped/).

## <a name="where-can-i-learn-more-about-quotas-and-limits-for-various-app-service-plans"></a>Onde posso obter mais informações sobre cotas e limites de vários planos do Serviço de Aplicativo?

Para obter informações sobre cotas e limites, consulte [limites de Serviço de Aplicativo](../azure-subscription-service-limits.md#app-service-limits). 

## <a name="how-do-i-decrease-hello-response-time-for-hello-first-request-after-idle-time"></a>Como diminuir o tempo de resposta Olá para solicitação primeiro Olá após o tempo ocioso?

Por padrão, os aplicativos Web serão descarregados se estiverem ociosos por um período de tempo definido. Dessa forma, o sistema Olá pode conservar recursos. desvantagem de saudação é que hello resposta toohello primeira solicitação depois de aplicativo da web de saudação é descarregado é maior, tooallow Olá tooload de aplicativo web e começar a servir as respostas. Em planos de serviço básico e padrão, você pode ativar Olá **AlwaysOn** configuração tookeep Olá aplicativo sempre carregado. Isso elimina tempos de carregamento após o aplicativo hello está ocioso. Olá toochange **AlwaysOn** configuração:

1. No hello portal do Azure, vá tooyour web app.
2. Selecione **Configurações do aplicativo**.
3. Para **Sempre Ativo**, selecione **On**.

## <a name="how-do-i-turned-on-failed-request-tracing"></a>Como ativar o rastreamento de solicitação com falha?

tooturn no rastreamento de solicitação com falha:

1. No hello portal do Azure, vá tooyour web app.
3. Selecione **Todas as configurações** > **Logs de diagnóstico**.
4. Para **Rastreamento de solicitação com falha**, selecione **On**.
5. Selecione **Salvar**.
6. Na folha de saudação do aplicativo web, selecione **ferramentas**.
7. Selecione **Visual Studio Online**.
8. Se a configuração de saudação não é **na**, selecione **em**.
9. Selecione **Ir**.
10. Selecione **Web.config**.
11. No System. webServer, adicione essa configuração (toocapture uma URL específica):

    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*api*" />
    <add path="*api*">
    <traceAreas>
    <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
12. problemas de desempenho lento tootroubleshoot, adicione essa configuração (se Olá solicitação de captura está demorando mais de 30 segundos):
    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*" />
    <add path="*">
    <traceAreas> <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions timeTaken="00:00:30" statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
13. Olá toodownload falha rastreamentos de solicitação, em Olá [portal](https://portal.azure.com), vá tooyour site.
15. Selecione **Ferramentas** > **Kudu** > **Go**.
18. No menu de saudação, selecione **Console depuração** > **CMD**.
19. Selecione Olá **LogFiles** pasta e, em seguida, selecione Olá pasta com um nome que começa com **W3SVC**.
20. arquivo de XML toosee hello, o ícone de lápis Olá select.

## <a name="i-see-hello-message-worker-process-requested-recycle-due-toopercent-memory-limit-how-do-i-address-this-issue"></a>Vejo a mensagem de saudação "reciclagem do processo de trabalho solicitou too'Percent devido memória ' limite." Como posso solucionar esse problema?

Olá disponível quantidade máxima de memória para um processo de 32 bits (mesmo em um sistema operacional de 64 bits) é 2 GB. Por padrão, o processo de trabalho de saudação é definido too32 bits no serviço de aplicativo (para compatibilidade com aplicativos web herdada).

Considere a possibilidade de processos too64 bits para que você pode tirar proveito da saudação mais memória disponível em sua função Web Worker. Isso dispara uma reinicialização do aplicativo web, portanto agende adequadamente.

Observe também que um ambiente de 64 bits requer um plano de serviço básico ou padrão. Planos gratuito ou compartilhado são sempre executados em um ambiente de 32 bits.

Para obter mais informações, consulte [Configurar aplicativos web no Serviço de Aplicativo](https://docs.microsoft.com/azure/app-service-web/web-sites-configure).

## <a name="why-does-my-request-time-out-after-240-seconds"></a>Por que minha solicitação atinge o tempo limite depois de 240 segundos?

O Azure Load Balancer tem uma configuração de tempo limite de ociosidade padrão de quatro minutos. Isso geralmente é um limite de tempo de resposta razoável para uma solicitação da web. Se seu aplicativo web requer o processamento em segundo plano, é recomendável usar o Azure WebJobs. aplicativo da web do Azure de saudação pode chamar WebJobs e ser notificado quando o processamento em segundo plano é concluído. Você pode escolher entre vários métodos para usar WebJobs, inclusive filas e gatilhos.

O WebJobs foi projetado para processamento em segundo plano. Você pode fazer quantos processamentos em segundo plano desejar em um WebJob. Para obter mais informações sobre WebJobs, consulte [Executar tarefas em segundo plano com o WebJobs](https://docs.microsoft.com/azure/app-service-web/web-sites-create-web-jobs).

## <a name="aspnet-core-applications-that-are-hosted-in-app-service-sometimes-stop-responding-how-do-i-fix-this-issue"></a>Aplicativos ASP.NET Core que são hospedados no Serviço de Aplicativo, às vezes, param de responder. Como faço para corrigir esse problema?

Um problema conhecido com um anteriores [versão Kestrel](https://github.com/aspnet/KestrelHttpServer/issues/1182) pode fazer com que um aplicativo do ASP.NET Core 1.0 que está hospedado no serviço de aplicativo toointermittently parar respondendo. Você também pode ver esta mensagem: "hello especificado aplicativo CGI encontrou um processo de saudação servidor encerrada erro e hello".

Esse problema foi corrigido no Kestrel versão 1.0.2. Esta versão está incluída no hello atualização do ASP.NET Core 1.0.3. tooresolve esse problema, certifique-se de atualizar sua dependências de aplicativo toouse Kestrel 1.0.2. Como alternativa, você pode usar uma das duas soluções alternativas são descritas na postagem do blog Olá [problemas de desempenho lento do ASP.NET Core 1.0 em aplicativos do serviço de aplicativo da web](https://blogs.msdn.microsoft.com/waws/2016/12/11/asp-net-core-slow-perf-issues-on-azure-websites).


## <a name="i-cant-find-my-log-files-in-hello-file-structure-of-my-web-app-how-can-i-find-them"></a>Não é possível localizar Meus arquivos de log na estrutura de arquivos de saudação do meu aplicativo web. Como posso encontrá-los?

Se você usar o recurso de Cache Local de saudação do serviço de aplicativo, estrutura de pastas de saudação do hello arquivos de log e as pastas de dados para a instância do serviço de aplicativo são afetadas. Quando o Cache Local é usado, as subpastas são criadas no armazenamento de saudação arquivos de log e as pastas de dados. uso de subpastas Olá Olá nomenclatura padrão "identificador exclusivo" + o carimbo de data / hora. Cada subpasta corresponde tooa instância VM na qual Olá aplicativo web está em execução ou foi executada.

toodetermine se você estiver usando o Cache Local, verifique o seu serviço de aplicativo **configurações de aplicativo** guia. Se o Cache Local está sendo usado, Olá configuração do aplicativo `WEBSITE_LOCAL_CACHE_OPTION` está definido muito`Always`. Para obter mais informações sobre o Cache Local, consulte Olá [visão geral do Cache Local do serviço de aplicativo](https://docs.microsoft.com/azure/app-service/app-service-local-cache).

Se você não estiver usando o Cache Local e estiver enfrentando esse problema, envie uma solicitação de suporte.

## <a name="i-see-hello-message-an-attempt-was-made-tooaccess-a-socket-in-a-way-forbidden-by-its-access-permissions-how-do-i-resolve-this"></a>Vejo a mensagem de saudação "uma tentativa foi feita tooaccess um soquete de uma maneira proibida pelas permissões de acesso." Como resolver isso?

Esse erro normalmente ocorre se as conexões TCP de saída Olá na instância VM Olá são esgotadas. No serviço de aplicativo, os limites são aplicados para o número máximo de saudação de conexões de saída que podem ser feitas para cada instância VM. Para obter mais informações, consulte [limites numéricos entre-VM](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#cross-vm-numerical-limits).

Esse erro também pode ocorrer se você tentar tooaccess um endereço local do seu aplicativo. Para obter mais informações, consulte [Solicitações de endereço local](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#local-address-requests).

Para obter mais informações sobre conexões de saída em seu aplicativo web, consulte Olá postagem de blog sobre [saída conexões tooAzure sites](http://www.freekpaans.nl/2015/08/starving-outgoing-connections-on-windows-azure-web-sites/).

## <a name="how-do-i-use-visual-studio-tooremote-debug-my-app-service-web-app"></a>Como usar depuração do Visual Studio tooremote meu aplicativo do serviço de aplicativo web?

Para obter instruções detalhadas que mostra como toodebug seu aplicativo web usando o Visual Studio, consulte [remoto depurar seu aplicativo do serviço de aplicativo web](https://blogs.msdn.microsoft.com/benjaminperkins/2016/09/22/remote-debug-your-azure-app-service-web-app/).
