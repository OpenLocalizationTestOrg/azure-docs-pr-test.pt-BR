---
title: aplicativo com o Azure Insights de aplicativo da web aaaMonitor um ASP.NET ao vivo | Microsoft Docs
description: "Monitore o desempenho do site sem implantá-lo novamente. Funciona com aplicativos web ASP.NET hospedado no local, em máquinas virtuais ou no Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="bb995-104">Instrumentar aplicativos Web no tempo de execução com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="bb995-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="bb995-105">Você pode instrumentar um aplicativo web em tempo real com informações de aplicativo do Azure, sem ter que toomodify ou reimplantar seu código.</span><span class="sxs-lookup"><span data-stu-id="bb995-105">You can instrument a live web app with Azure Application Insights, without having toomodify or redeploy your code.</span></span> <span data-ttu-id="bb995-106">Se os seus aplicativos forem hospedados por um servidor IIS local, instale o Monitor de Status.</span><span class="sxs-lookup"><span data-stu-id="bb995-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="bb995-107">Caso de aplicativos web do Azure ou executados em uma VM do Azure, você pode alternar no monitoramento do Application Insights hello Azure no painel de controle.</span><span class="sxs-lookup"><span data-stu-id="bb995-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from hello Azure control panel.</span></span> <span data-ttu-id="bb995-108">(Também há artigos separados sobre como instrumentar os [aplicativos Web J2EE dinâmicos](app-insights-java-live.md) e os [Serviços de Nuvem do Azure](app-insights-cloudservices.md).) É necessário ter uma assinatura do [Microsoft Azure](http://azure.com) .</span><span class="sxs-lookup"><span data-stu-id="bb995-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![gráficos de exemplo](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="bb995-110">Você tem a opção de três rotas tooapply Application Insights tooyour .NET web aplicativos:</span><span class="sxs-lookup"><span data-stu-id="bb995-110">You have a choice of three routes tooapply Application Insights tooyour .NET web applications:</span></span>

* <span data-ttu-id="bb995-111">**Tempo de compilação:** [Olá adicionar SDK do Application Insights] [ greenbrown] tooyour código de aplicativo de web.</span><span class="sxs-lookup"><span data-stu-id="bb995-111">**Build time:** [Add hello Application Insights SDK][greenbrown] tooyour web app code.</span></span>
* <span data-ttu-id="bb995-112">**Tempo de execução:** instrumentar seu aplicativo web no servidor de saudação, conforme descrito abaixo, sem recompilar e reimplantar o código de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb995-112">**Run time:** Instrument your web app on hello server, as described below, without rebuilding and redeploying hello code.</span></span>
* <span data-ttu-id="bb995-113">**Ambos:** criar hello SDK em seu código de aplicativo web e também se aplicam a extensões de tempo de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb995-113">**Both:** Build hello SDK into your web app code, and also apply hello run-time extensions.</span></span> <span data-ttu-id="bb995-114">Olá obter o melhor de ambas as opções.</span><span class="sxs-lookup"><span data-stu-id="bb995-114">Get hello best of both options.</span></span>

<span data-ttu-id="bb995-115">Aqui está um resumo do que você tem com cada rota:</span><span class="sxs-lookup"><span data-stu-id="bb995-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="bb995-116">Tempo de compilação</span><span class="sxs-lookup"><span data-stu-id="bb995-116">Build time</span></span> | <span data-ttu-id="bb995-117">Tempo de execução</span><span class="sxs-lookup"><span data-stu-id="bb995-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb995-118">Solicitações e exceções</span><span class="sxs-lookup"><span data-stu-id="bb995-118">Requests & exceptions</span></span> |<span data-ttu-id="bb995-119">Sim</span><span class="sxs-lookup"><span data-stu-id="bb995-119">Yes</span></span> |<span data-ttu-id="bb995-120">Sim</span><span class="sxs-lookup"><span data-stu-id="bb995-120">Yes</span></span> |
| [<span data-ttu-id="bb995-121">Exceções mais detalhadas</span><span class="sxs-lookup"><span data-stu-id="bb995-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="bb995-122">Sim</span><span class="sxs-lookup"><span data-stu-id="bb995-122">Yes</span></span> |
| [<span data-ttu-id="bb995-123">Diagnóstico de dependência</span><span class="sxs-lookup"><span data-stu-id="bb995-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="bb995-124">No .NET 4.6+, mas menos detalhes</span><span class="sxs-lookup"><span data-stu-id="bb995-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="bb995-125">Sim, detalhes completos: códigos de resultado, texto do comando SQL, verbo HTTP</span><span class="sxs-lookup"><span data-stu-id="bb995-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="bb995-126">Contadores de desempenho do sistema</span><span class="sxs-lookup"><span data-stu-id="bb995-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="bb995-127">Sim</span><span class="sxs-lookup"><span data-stu-id="bb995-127">Yes</span></span> |<span data-ttu-id="bb995-128">Sim</span><span class="sxs-lookup"><span data-stu-id="bb995-128">Yes</span></span> |
| <span data-ttu-id="bb995-129">[API de telemetria personalizada][api]</span><span class="sxs-lookup"><span data-stu-id="bb995-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="bb995-130">Sim</span><span class="sxs-lookup"><span data-stu-id="bb995-130">Yes</span></span> |<span data-ttu-id="bb995-131">Não</span><span class="sxs-lookup"><span data-stu-id="bb995-131">No</span></span> |
| [<span data-ttu-id="bb995-132">Integração do log de rastreamento</span><span class="sxs-lookup"><span data-stu-id="bb995-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="bb995-133">Sim</span><span class="sxs-lookup"><span data-stu-id="bb995-133">Yes</span></span> |<span data-ttu-id="bb995-134">Não</span><span class="sxs-lookup"><span data-stu-id="bb995-134">No</span></span> |
| [<span data-ttu-id="bb995-135">Exibição da página e dados do usuário</span><span class="sxs-lookup"><span data-stu-id="bb995-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="bb995-136">Sim</span><span class="sxs-lookup"><span data-stu-id="bb995-136">Yes</span></span> |<span data-ttu-id="bb995-137">Não</span><span class="sxs-lookup"><span data-stu-id="bb995-137">No</span></span> |
| <span data-ttu-id="bb995-138">Código de toorebuild necessário</span><span class="sxs-lookup"><span data-stu-id="bb995-138">Need toorebuild code</span></span> |<span data-ttu-id="bb995-139">Sim</span><span class="sxs-lookup"><span data-stu-id="bb995-139">Yes</span></span> | <span data-ttu-id="bb995-140">Não</span><span class="sxs-lookup"><span data-stu-id="bb995-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="bb995-141">Monitorar um aplicativo da web ao vivo</span><span class="sxs-lookup"><span data-stu-id="bb995-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="bb995-142">Se seu aplicativo é executado como um serviço de web do Azure, aqui como tooswitch no monitoramento:</span><span class="sxs-lookup"><span data-stu-id="bb995-142">If your application is running as an Azure web service, here's how tooswitch on monitoring:</span></span>

* <span data-ttu-id="bb995-143">Selecione o Application Insights no painel de controle de saudação do aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="bb995-143">Select Application Insights on hello app's control panel in Azure.</span></span>

    ![Configurar o Application Insights para um aplicativo Web do Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="bb995-145">Quando abre a página Resumo do Application Insights hello, clique o link de saudação na Olá inferior tooopen Olá completo recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bb995-145">When hello Application Insights summary page opens, click hello link at hello bottom tooopen hello full Application Insights resource.</span></span>

    ![Clique nas tooApplication Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="bb995-147">[Monitoramento de aplicativos de nuvem e a VM](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="bb995-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="bb995-148">Habilitar o monitoramento do lado do cliente no Azure</span><span class="sxs-lookup"><span data-stu-id="bb995-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="bb995-149">Se você tiver habilitado o Application Insights no Azure, você poderá adicionar telemetria de usuário e exibição de página.</span><span class="sxs-lookup"><span data-stu-id="bb995-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="bb995-150">Selecione Configurações > Configurações do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="bb995-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="bb995-151">Em configurações do aplicativo, adicione um novo par de chave/valor:</span><span class="sxs-lookup"><span data-stu-id="bb995-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="bb995-152">Chave: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="bb995-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="bb995-153">Valor: `true`</span><span class="sxs-lookup"><span data-stu-id="bb995-153">Value: `true`</span></span>
3. <span data-ttu-id="bb995-154">**Salvar** Olá configurações e **reiniciar** seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bb995-154">**Save** hello settings and **Restart** your app.</span></span>

<span data-ttu-id="bb995-155">Olá SDK de JavaScript do Application Insights agora é injetado em cada página da web.</span><span class="sxs-lookup"><span data-stu-id="bb995-155">hello Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="bb995-156">Monitorar um aplicativo de web IIS ao vivo</span><span class="sxs-lookup"><span data-stu-id="bb995-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="bb995-157">Se seu aplicativo estiver hospedado em um servidor do IIS, habilite o Application Insights usando o Monitor de Status.</span><span class="sxs-lookup"><span data-stu-id="bb995-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="bb995-158">No servidor Web IIS, entre com as credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="bb995-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="bb995-159">Se o Application Insights Status Monitor não estiver instalado, baixe e execute Olá [instalador do Monitor de Status](http://go.microsoft.com/fwlink/?LinkId=506648) (ou execute [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) e procure nele Application Insights Status Monitor).</span><span class="sxs-lookup"><span data-stu-id="bb995-159">If Application Insights Status Monitor is not already installed, download and run hello [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="bb995-160">No Monitor de Status, selecione o aplicativo hello instalado ou o site que você deseja toomonitor.</span><span class="sxs-lookup"><span data-stu-id="bb995-160">In Status Monitor, select hello installed web application or website that you want toomonitor.</span></span> <span data-ttu-id="bb995-161">Entre com suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb995-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="bb995-162">Configure o recurso de saudação onde você deseja que os resultados de saudação toosee no portal do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="bb995-162">Configure hello resource where you want toosee hello results in hello Application Insights portal.</span></span> <span data-ttu-id="bb995-163">(Normalmente, é melhor toocreate um novo recurso.</span><span class="sxs-lookup"><span data-stu-id="bb995-163">(Normally, it's best toocreate a new resource.</span></span> <span data-ttu-id="bb995-164">Selecione um recurso existente se você já tiver [testes da web][availability] ou [monitoramento de cliente][client] para esse aplicativo).</span><span class="sxs-lookup"><span data-stu-id="bb995-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![Escolha um aplicativo e um recurso.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="bb995-166">Reinicie o IIS.</span><span class="sxs-lookup"><span data-stu-id="bb995-166">Restart IIS.</span></span>

    ![Escolha reiniciar na parte superior de saudação da caixa de diálogo de saudação.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="bb995-168">O serviço Web é interrompido por um período curto.</span><span class="sxs-lookup"><span data-stu-id="bb995-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="bb995-169">Personalizar opções de monitoramento</span><span class="sxs-lookup"><span data-stu-id="bb995-169">Customize monitoring options</span></span>

<span data-ttu-id="bb995-170">A habilitação do Application Insights adiciona DLLs e Applicationinsights tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="bb995-170">Enabling Application Insights adds DLLs and ApplicationInsights.config tooyour web app.</span></span> <span data-ttu-id="bb995-171">Você pode [editar o arquivo. config de saudação](app-insights-configuration-with-applicationinsights-config.md) toochange algumas das opções de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb995-171">You can [edit hello .config file](app-insights-configuration-with-applicationinsights-config.md) toochange some of hello options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="bb995-172">Quando você publicar novamente seu aplicativo, habilite novamente o Application Insights</span><span class="sxs-lookup"><span data-stu-id="bb995-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="bb995-173">Antes de publicar seu aplicativo novamente, considere [adicionando o código de toohello do Application Insights no Visual Studio][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="bb995-173">Before you re-publish your app, consider [adding Application Insights toohello code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="bb995-174">Você obterá mais detalhada de telemetria e telemetria personalizada de toowrite de capacidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb995-174">You'll get more detailed telemetry and hello ability toowrite custom telemetry.</span></span>

<span data-ttu-id="bb995-175">Se você quiser toore-publicar sem adicionar Application Insights toohello código, lembre-se de que o processo de implantação Olá pode excluir Olá DLLs e applicationinsights. config de saudação publicado o site da web.</span><span class="sxs-lookup"><span data-stu-id="bb995-175">If you want toore-publish without adding Application Insights toohello code, be aware that hello deployment process may delete hello DLLs and ApplicationInsights.config from hello published web site.</span></span> <span data-ttu-id="bb995-176">Portanto:</span><span class="sxs-lookup"><span data-stu-id="bb995-176">Therefore:</span></span>

1. <span data-ttu-id="bb995-177">Se você tiver editado applicationinsights.config, faça uma cópia dele antes de publicar seu aplicativo novamente.</span><span class="sxs-lookup"><span data-stu-id="bb995-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="bb995-178">Republique seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bb995-178">Republish your app.</span></span>
3. <span data-ttu-id="bb995-179">Habilite novamente o monitoramento do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bb995-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="bb995-180">(Use o método apropriado de saudação: painel de controle de aplicativo web do Azure Olá ou Olá Monitor de Status em um host IIS.)</span><span class="sxs-lookup"><span data-stu-id="bb995-180">(Use hello appropriate method: either hello Azure web app control panel, or hello Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="bb995-181">Reaplicar as edições realizadas no arquivo. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb995-181">Reinstate any edits you performed on hello .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="bb995-182">Solução de problemas de configuração de tempo de execução do Application Insights</span><span class="sxs-lookup"><span data-stu-id="bb995-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="bb995-183">Não consegue se conectar?</span><span class="sxs-lookup"><span data-stu-id="bb995-183">Can't connect?</span></span> <span data-ttu-id="bb995-184">Sem telemetria?</span><span class="sxs-lookup"><span data-stu-id="bb995-184">No telemetry?</span></span>

* <span data-ttu-id="bb995-185">Abra [Olá portas de saída necessário](app-insights-ip-addresses.md#outgoing-ports) no toowork de Monitor de Status de tooallow de firewall do servidor.</span><span class="sxs-lookup"><span data-stu-id="bb995-185">Open [hello necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall tooallow Status Monitor toowork.</span></span>

* <span data-ttu-id="bb995-186">Abra o Monitor de Status e selecione seu aplicativo no painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="bb995-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="bb995-187">Verifique se há mensagens de diagnóstico para este aplicativo no hello seção "Configuração de notificações":</span><span class="sxs-lookup"><span data-stu-id="bb995-187">Check if there are any diagnostics messages for this application in hello "Configuration notifications" section:</span></span>

  ![Abra a solicitação de toosee Olá desempenho folha, tempo de resposta, dependências e outros dados](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="bb995-189">No servidor de saudação, se você vir uma mensagem sobre "permissões insuficientes", tente seguir hello:</span><span class="sxs-lookup"><span data-stu-id="bb995-189">On hello server, if you see a message about "insufficient permissions", try hello following:</span></span>
  * <span data-ttu-id="bb995-190">No Gerenciador do IIS, selecione o pool de aplicativos, abra **configurações avançadas**e, em **modelo de processo** Observe identidade hello.</span><span class="sxs-lookup"><span data-stu-id="bb995-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note hello identity.</span></span>
  * <span data-ttu-id="bb995-191">No painel de controle de gerenciamento do computador, adicione esse grupo de usuários de Monitor de desempenho de toohello de identidade.</span><span class="sxs-lookup"><span data-stu-id="bb995-191">In Computer management control panel, add this identity toohello Performance Monitor Users group.</span></span>
* <span data-ttu-id="bb995-192">Se você tiver o MMA/SCOM (Systems Center Operations Manager) instalado em seu servidor, algumas versões poderão entrar em conflito.</span><span class="sxs-lookup"><span data-stu-id="bb995-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="bb995-193">Desinstalar o SCOM e o Monitor de Status e reinstale em versões mais recentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb995-193">Uninstall both SCOM and Status Monitor, and re-install hello latest versions.</span></span>
* <span data-ttu-id="bb995-194">Consulte [Solução de problemas][qna].</span><span class="sxs-lookup"><span data-stu-id="bb995-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="bb995-195">Requisitos do Sistema</span><span class="sxs-lookup"><span data-stu-id="bb995-195">System Requirements</span></span>
<span data-ttu-id="bb995-196">Suporte de sistema operacional para Application Insights Status Monitor no servidor:</span><span class="sxs-lookup"><span data-stu-id="bb995-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="bb995-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="bb995-197">Windows Server 2008</span></span>
* <span data-ttu-id="bb995-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="bb995-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="bb995-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="bb995-199">Windows Server 2012</span></span>
* <span data-ttu-id="bb995-200">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="bb995-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="bb995-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="bb995-201">Windows Server 2016</span></span>

<span data-ttu-id="bb995-202">com o SP mais recente e o .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="bb995-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="bb995-203">No lado do cliente Olá: Windows 7, 8, 8.1 e 10, novamente com o .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="bb995-203">On hello client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="bb995-204">Suporte ao IIS: IIS 7, 7,5, 8 e 8.5 (o IIS é obrigatório)</span><span class="sxs-lookup"><span data-stu-id="bb995-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="bb995-205">Automação com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb995-205">Automation with PowerShell</span></span>
<span data-ttu-id="bb995-206">Você pode iniciar e interromper o monitoramento usando o PowerShell no servidor IIS.</span><span class="sxs-lookup"><span data-stu-id="bb995-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="bb995-207">Primeiro importe o módulo do Application Insights hello:</span><span class="sxs-lookup"><span data-stu-id="bb995-207">First import hello Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="bb995-208">Saiba quais aplicativos estão sendo monitorados:</span><span class="sxs-lookup"><span data-stu-id="bb995-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="bb995-209">`-Name`Nome da saudação (opcional) de um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="bb995-209">`-Name` (Optional) hello name of a web app.</span></span>
* <span data-ttu-id="bb995-210">Exibe Olá status de monitoramento do Application Insights para cada aplicativo web (ou Olá denominado aplicativo) neste servidor IIS.</span><span class="sxs-lookup"><span data-stu-id="bb995-210">Displays hello Application Insights monitoring status for each web app (or hello named app) in this IIS server.</span></span>
* <span data-ttu-id="bb995-211">Retorna `ApplicationInsightsApplication` para cada aplicativo:</span><span class="sxs-lookup"><span data-stu-id="bb995-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="bb995-212">`SdkState==EnabledAfterDeployment`: O aplicativo está sendo monitorado e foi instrumentado em tempo de execução, pela ferramenta de Monitor de Status de hello, ou por `Start-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="bb995-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by hello Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="bb995-213">`SdkState==Disabled`: aplicativo hello não está instrumentado para o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bb995-213">`SdkState==Disabled`: hello app is not instrumented for Application Insights.</span></span> <span data-ttu-id="bb995-214">Ele nunca foi instrumentado, tanto o monitoramento de tempo de execução foi desabilitado com a ferramenta de Monitor de Status de saudação ou com `Stop-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="bb995-214">Either it was never instrumented, or run-time monitoring was disabled with hello Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="bb995-215">`SdkState==EnabledByCodeInstrumentation`: aplicativo hello foi instrumentado, adicionando o código-fonte toohello Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="bb995-215">`SdkState==EnabledByCodeInstrumentation`: hello app was instrumented by adding hello SDK toohello source code.</span></span> <span data-ttu-id="bb995-216">Seu SDK não pode ser atualizado ou interrompido.</span><span class="sxs-lookup"><span data-stu-id="bb995-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="bb995-217">`SdkVersion`mostra a versão de saudação em uso para este aplicativo de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="bb995-217">`SdkVersion` shows hello version in use for monitoring this app.</span></span>
  * <span data-ttu-id="bb995-218">`LatestAvailableSdkVersion`mostra a versão de hello atualmente disponível na Galeria do NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="bb995-218">`LatestAvailableSdkVersion`shows hello version currently available on hello NuGet gallery.</span></span> <span data-ttu-id="bb995-219">tooupgrade Olá aplicativo toothis a versão `Update-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="bb995-219">tooupgrade hello app toothis version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="bb995-220">`-Name`nome de saudação do aplicativo hello no IIS</span><span class="sxs-lookup"><span data-stu-id="bb995-220">`-Name` hello name of hello app in IIS</span></span>
* <span data-ttu-id="bb995-221">`-InstrumentationKey`Olá ikey de saudação recurso do Application Insights onde você deseja Olá resultados toobe exibida.</span><span class="sxs-lookup"><span data-stu-id="bb995-221">`-InstrumentationKey` hello ikey of hello Application Insights resource where you want hello results toobe displayed.</span></span>
* <span data-ttu-id="bb995-222">Este cmdlet afeta apenas os aplicativos que ainda não estão instrumentados - ou seja, SdkState==NotInstrumented.</span><span class="sxs-lookup"><span data-stu-id="bb995-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="bb995-223">Olá cmdlet não afeta um aplicativo que já está instrumentado.</span><span class="sxs-lookup"><span data-stu-id="bb995-223">hello cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="bb995-224">Não importa se o aplicativo hello foi instrumentado no momento da compilação, adicionando Olá SDK toohello código, ou em tempo de execução por um uso anterior deste cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bb995-224">It does not matter whether hello app was instrumented at build time by adding hello SDK toohello code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="bb995-225">Olá SDK versão usada tooinstrument Olá aplicativo é versão hello mais recentemente baixado toothis server.</span><span class="sxs-lookup"><span data-stu-id="bb995-225">hello SDK version used tooinstrument hello app is hello version that was most recently downloaded toothis server.</span></span>

    <span data-ttu-id="bb995-226">versão mais recente do toodownload hello, use ApplicationInsightsVersion de atualização.</span><span class="sxs-lookup"><span data-stu-id="bb995-226">toodownload hello latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="bb995-227">Retorna `ApplicationInsightsApplication` se há êxito.</span><span class="sxs-lookup"><span data-stu-id="bb995-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="bb995-228">Se ele falhar, ele registra um toostderr de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="bb995-228">If it fails, it logs a trace toostderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="bb995-229">`-Name`nome de saudação de um aplicativo no IIS</span><span class="sxs-lookup"><span data-stu-id="bb995-229">`-Name` hello name of an app in IIS</span></span>
* <span data-ttu-id="bb995-230">`-All` Para o monitoramento de todos os aplicativos desse servidor IIS para o qual `SdkState==EnabledAfterDeployment`</span><span class="sxs-lookup"><span data-stu-id="bb995-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="bb995-231">Interrompe o monitoramento Olá determinados aplicativos e remove a instrumentação.</span><span class="sxs-lookup"><span data-stu-id="bb995-231">Stops monitoring hello specified apps and removes instrumentation.</span></span> <span data-ttu-id="bb995-232">Ele só funciona para aplicativos que foram instrumentados em tempo de execução usando Olá, ferramenta de monitoramento de Status ou ApplicationInsightsApplication de início.</span><span class="sxs-lookup"><span data-stu-id="bb995-232">It only works for apps that have been instrumented at run-time using hello Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="bb995-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="bb995-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="bb995-234">Retorna ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="bb995-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="bb995-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="bb995-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="bb995-236">`-Name`: nome de saudação de um aplicativo web no IIS.</span><span class="sxs-lookup"><span data-stu-id="bb995-236">`-Name`: hello name of a web app in IIS.</span></span>
* <span data-ttu-id="bb995-237">`-InstrumentationKey` (Opcional.) Use que este toochange Olá recurso toowhich Olá telemetria do aplicativo é enviada.</span><span class="sxs-lookup"><span data-stu-id="bb995-237">`-InstrumentationKey` (Optional.) Use this toochange hello resource toowhich hello app's telemetry is sent.</span></span>
* <span data-ttu-id="bb995-238">Este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bb995-238">This cmdlet:</span></span>
  * <span data-ttu-id="bb995-239">Olá atualizações chamado toohello do aplicativo versão do SDK do hello mais recentemente baixado toothis máquina.</span><span class="sxs-lookup"><span data-stu-id="bb995-239">Upgrades hello named app toohello version of hello SDK most recently downloaded toothis machine.</span></span> <span data-ttu-id="bb995-240">(Só funciona se `SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="bb995-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="bb995-241">Se você fornecer uma chave de instrumentação, Olá denominado aplicativo é reconfigurado toosend telemetria toohello recursos com essa chave.</span><span class="sxs-lookup"><span data-stu-id="bb995-241">If you provide an instrumentation key, hello named app is reconfigured toosend telemetry toohello resource with that key.</span></span> <span data-ttu-id="bb995-242">(Funciona se `SdkState != Disabled`)</span><span class="sxs-lookup"><span data-stu-id="bb995-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="bb995-243">Faz o download do servidor de toohello do SDK do Application Insights mais recente hello.</span><span class="sxs-lookup"><span data-stu-id="bb995-243">Downloads hello latest Application Insights SDK toohello server.</span></span>

## <span data-ttu-id="bb995-244"><a name="questions"></a>Perguntas sobre o Status Monitor</span><span class="sxs-lookup"><span data-stu-id="bb995-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="bb995-245">O que é o Status Monitor?</span><span class="sxs-lookup"><span data-stu-id="bb995-245">What is Status Monitor?</span></span>

<span data-ttu-id="bb995-246">Um aplicativo de desktop instalado no servidor web IIS.</span><span class="sxs-lookup"><span data-stu-id="bb995-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="bb995-247">Ele ajuda você instrumentar e configurar aplicativos web.</span><span class="sxs-lookup"><span data-stu-id="bb995-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="bb995-248">Quando eu devo usar o Status Monitor?</span><span class="sxs-lookup"><span data-stu-id="bb995-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="bb995-249">tooinstrument qualquer aplicativo da web que está em execução no servidor IIS - mesmo se ele já está em execução.</span><span class="sxs-lookup"><span data-stu-id="bb995-249">tooinstrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="bb995-250">tooenable a telemetria adicional para aplicativos web que foram [criados com hello SDK do Application Insights](app-insights-asp-net.md) em tempo de compilação.</span><span class="sxs-lookup"><span data-stu-id="bb995-250">tooenable additional telemetry for web apps that have been [built with hello Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="bb995-251">Eu posso fechá-lo depois de ser executado?</span><span class="sxs-lookup"><span data-stu-id="bb995-251">Can I close it after it runs?</span></span>

<span data-ttu-id="bb995-252">Sim.</span><span class="sxs-lookup"><span data-stu-id="bb995-252">Yes.</span></span> <span data-ttu-id="bb995-253">Depois que ele foi instrumentado sites Olá que você selecionar, você pode fechá-lo.</span><span class="sxs-lookup"><span data-stu-id="bb995-253">After it has instrumented hello websites you select, you can close it.</span></span>

<span data-ttu-id="bb995-254">Ele não coleta telemetria por si só.</span><span class="sxs-lookup"><span data-stu-id="bb995-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="bb995-255">Ele apenas configura os aplicativos web hello e define algumas permissões.</span><span class="sxs-lookup"><span data-stu-id="bb995-255">It just configures hello web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="bb995-256">O que o Status Monitor faz?</span><span class="sxs-lookup"><span data-stu-id="bb995-256">What does Status Monitor do?</span></span>

<span data-ttu-id="bb995-257">Quando você seleciona um aplicativo web para o Monitor de Status tooinstrument:</span><span class="sxs-lookup"><span data-stu-id="bb995-257">When you select a web app for Status Monitor tooinstrument:</span></span>

* <span data-ttu-id="bb995-258">Baixa e coloca os assemblies do Application Insights hello e arquivo. config na pasta de binários do aplicativo da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb995-258">Downloads and places hello Application Insights assemblies and .config file in hello web app's binaries folder.</span></span>
* <span data-ttu-id="bb995-259">Modifica `web.config` módulo de controle de aplicativo Insights HTTP tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="bb995-259">Modifies `web.config` tooadd hello Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="bb995-260">Habilita o CLR toocollect chamadas de dependência de criação de perfil.</span><span class="sxs-lookup"><span data-stu-id="bb995-260">Enables CLR profiling toocollect dependency calls.</span></span>

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a><span data-ttu-id="bb995-261">É necessário o Monitor de Status de toorun sempre que atualiza o aplicativo hello?</span><span class="sxs-lookup"><span data-stu-id="bb995-261">Do I need toorun Status Monitor whenever I update hello app?</span></span>

<span data-ttu-id="bb995-262">Não ocorre se você reimplantar incrementalmente.</span><span class="sxs-lookup"><span data-stu-id="bb995-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="bb995-263">Se você selecionar a opção de 'Excluir os arquivos existentes' de saudação em Olá processo de publicação, você deve executar toore Status Monitor tooconfigure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bb995-263">If you select hello 'delete existing files' option in hello publish process, you would need toore-run Status Monitor tooconfigure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="bb995-264">Qual telemetria é coletada?</span><span class="sxs-lookup"><span data-stu-id="bb995-264">What telemetry is collected?</span></span>

<span data-ttu-id="bb995-265">Para aplicativos que você instrumenta apenas em tempo de execução usando o Status Monitor:</span><span class="sxs-lookup"><span data-stu-id="bb995-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="bb995-266">Solicitações HTTP</span><span class="sxs-lookup"><span data-stu-id="bb995-266">HTTP requests</span></span>
* <span data-ttu-id="bb995-267">Chamadas toodependencies</span><span class="sxs-lookup"><span data-stu-id="bb995-267">Calls toodependencies</span></span>
* <span data-ttu-id="bb995-268">Exceções</span><span class="sxs-lookup"><span data-stu-id="bb995-268">Exceptions</span></span>
* <span data-ttu-id="bb995-269">Contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="bb995-269">Performance counters</span></span>

<span data-ttu-id="bb995-270">Para aplicativos já instrumentados em tempo de compilação:</span><span class="sxs-lookup"><span data-stu-id="bb995-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="bb995-271">Contadores de processo.</span><span class="sxs-lookup"><span data-stu-id="bb995-271">Process counters.</span></span>
 * <span data-ttu-id="bb995-272">Chamadas de dependência (.NET 4.5); valores de retorno em chamadas de dependência (.NET 4.6).</span><span class="sxs-lookup"><span data-stu-id="bb995-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="bb995-273">Exceção dos valores do rastreamento de pilha.</span><span class="sxs-lookup"><span data-stu-id="bb995-273">Exception stack trace values.</span></span>

[<span data-ttu-id="bb995-274">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="bb995-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="bb995-275">Vídeo</span><span class="sxs-lookup"><span data-stu-id="bb995-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="bb995-276"><a name="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb995-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="bb995-277">Exiba sua telemetria:</span><span class="sxs-lookup"><span data-stu-id="bb995-277">View your telemetry:</span></span>

* <span data-ttu-id="bb995-278">[Explorar as métricas](app-insights-metrics-explorer.md) toomonitor desempenho e uso</span><span class="sxs-lookup"><span data-stu-id="bb995-278">[Explore metrics](app-insights-metrics-explorer.md) toomonitor performance and usage</span></span>
* <span data-ttu-id="bb995-279">[Pesquisar eventos e logs de] [ diagnostic] toodiagnose problemas</span><span class="sxs-lookup"><span data-stu-id="bb995-279">[Search events and logs][diagnostic] toodiagnose problems</span></span>
* <span data-ttu-id="bb995-280">[Analise](app-insights-analytics.md) para obter mais consultas avançadas</span><span class="sxs-lookup"><span data-stu-id="bb995-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="bb995-281">Crie painéis</span><span class="sxs-lookup"><span data-stu-id="bb995-281">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="bb995-282">Adicione mais telemetria:</span><span class="sxs-lookup"><span data-stu-id="bb995-282">Add more telemetry:</span></span>

* <span data-ttu-id="bb995-283">[Criar testes da web] [ availability] toomake-se de que o site permanece ativo.</span><span class="sxs-lookup"><span data-stu-id="bb995-283">[Create web tests][availability] toomake sure your site stays live.</span></span>
* <span data-ttu-id="bb995-284">[Adicionar telemetria do cliente web] [ usage] toosee exceções do código de página da web e toolet inserir chamadas de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="bb995-284">[Add web client telemetry][usage] toosee exceptions from web page code and toolet you insert trace calls.</span></span>
* <span data-ttu-id="bb995-285">[Adicione o código do SDK do Application Insights tooyour] [ greenbrown] para que você pode inserir o rastreamento e chamadas de log</span><span class="sxs-lookup"><span data-stu-id="bb995-285">[Add Application Insights SDK tooyour code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
