---
title: "Monitorar um aplicativo Web ASP.NET dinâmico com o Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: d07a0c81f89100c378456bbea8dca1c009cc8d77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="43f6b-104">Instrumentar aplicativos Web no tempo de execução com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="43f6b-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="43f6b-105">Você pode instrumentar um aplicativo Web ativo com o Application Insights do Azure, sem a necessidade de modificar ou reimplantar o código.</span><span class="sxs-lookup"><span data-stu-id="43f6b-105">You can instrument a live web app with Azure Application Insights, without having to modify or redeploy your code.</span></span> <span data-ttu-id="43f6b-106">Se os seus aplicativos forem hospedados por um servidor IIS local, instale o Monitor de Status.</span><span class="sxs-lookup"><span data-stu-id="43f6b-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="43f6b-107">Se forem aplicativos Web do Azure ou estiverem sendo executados em uma VM do Azure, ative o monitoramento do Application Insights no painel de controle do Azure.</span><span class="sxs-lookup"><span data-stu-id="43f6b-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from the Azure control panel.</span></span> <span data-ttu-id="43f6b-108">(Também há artigos separados sobre como instrumentar os [aplicativos Web J2EE dinâmicos](app-insights-java-live.md) e os [Serviços de Nuvem do Azure](app-insights-cloudservices.md).) É necessário ter uma assinatura do [Microsoft Azure](http://azure.com) .</span><span class="sxs-lookup"><span data-stu-id="43f6b-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![gráficos de exemplo](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="43f6b-110">Você tem a opção de três rotas para aplicar o Application Insights nos aplicativos Web .NET:</span><span class="sxs-lookup"><span data-stu-id="43f6b-110">You have a choice of three routes to apply Application Insights to your .NET web applications:</span></span>

* <span data-ttu-id="43f6b-111">**Tempo de compilação:** [Adicionar o SDK do Application Insights][greenbrown] ao código do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="43f6b-111">**Build time:** [Add the Application Insights SDK][greenbrown] to your web app code.</span></span>
* <span data-ttu-id="43f6b-112">**Tempo de execução:** instrumente seu aplicativo Web no servidor, conforme descrito abaixo, sem recompilar e reimplantar o código.</span><span class="sxs-lookup"><span data-stu-id="43f6b-112">**Run time:** Instrument your web app on the server, as described below, without rebuilding and redeploying the code.</span></span>
* <span data-ttu-id="43f6b-113">**Ambos:** crie o SDK em seu código de aplicativo Web e também aplique as extensões de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="43f6b-113">**Both:** Build the SDK into your web app code, and also apply the run-time extensions.</span></span> <span data-ttu-id="43f6b-114">Obtenha o melhor de ambas as opções.</span><span class="sxs-lookup"><span data-stu-id="43f6b-114">Get the best of both options.</span></span>

<span data-ttu-id="43f6b-115">Aqui está um resumo do que você tem com cada rota:</span><span class="sxs-lookup"><span data-stu-id="43f6b-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="43f6b-116">Tempo de compilação</span><span class="sxs-lookup"><span data-stu-id="43f6b-116">Build time</span></span> | <span data-ttu-id="43f6b-117">Tempo de execução</span><span class="sxs-lookup"><span data-stu-id="43f6b-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="43f6b-118">Solicitações e exceções</span><span class="sxs-lookup"><span data-stu-id="43f6b-118">Requests & exceptions</span></span> |<span data-ttu-id="43f6b-119">Sim</span><span class="sxs-lookup"><span data-stu-id="43f6b-119">Yes</span></span> |<span data-ttu-id="43f6b-120">Sim</span><span class="sxs-lookup"><span data-stu-id="43f6b-120">Yes</span></span> |
| [<span data-ttu-id="43f6b-121">Exceções mais detalhadas</span><span class="sxs-lookup"><span data-stu-id="43f6b-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="43f6b-122">Sim</span><span class="sxs-lookup"><span data-stu-id="43f6b-122">Yes</span></span> |
| [<span data-ttu-id="43f6b-123">Diagnóstico de dependência</span><span class="sxs-lookup"><span data-stu-id="43f6b-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="43f6b-124">No .NET 4.6+, mas menos detalhes</span><span class="sxs-lookup"><span data-stu-id="43f6b-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="43f6b-125">Sim, detalhes completos: códigos de resultado, texto do comando SQL, verbo HTTP</span><span class="sxs-lookup"><span data-stu-id="43f6b-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="43f6b-126">Contadores de desempenho do sistema</span><span class="sxs-lookup"><span data-stu-id="43f6b-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="43f6b-127">Sim</span><span class="sxs-lookup"><span data-stu-id="43f6b-127">Yes</span></span> |<span data-ttu-id="43f6b-128">Sim</span><span class="sxs-lookup"><span data-stu-id="43f6b-128">Yes</span></span> |
| <span data-ttu-id="43f6b-129">[API de telemetria personalizada][api]</span><span class="sxs-lookup"><span data-stu-id="43f6b-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="43f6b-130">Sim</span><span class="sxs-lookup"><span data-stu-id="43f6b-130">Yes</span></span> |<span data-ttu-id="43f6b-131">Não</span><span class="sxs-lookup"><span data-stu-id="43f6b-131">No</span></span> |
| [<span data-ttu-id="43f6b-132">Integração do log de rastreamento</span><span class="sxs-lookup"><span data-stu-id="43f6b-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="43f6b-133">Sim</span><span class="sxs-lookup"><span data-stu-id="43f6b-133">Yes</span></span> |<span data-ttu-id="43f6b-134">Não</span><span class="sxs-lookup"><span data-stu-id="43f6b-134">No</span></span> |
| [<span data-ttu-id="43f6b-135">Exibição da página e dados do usuário</span><span class="sxs-lookup"><span data-stu-id="43f6b-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="43f6b-136">Sim</span><span class="sxs-lookup"><span data-stu-id="43f6b-136">Yes</span></span> |<span data-ttu-id="43f6b-137">Não</span><span class="sxs-lookup"><span data-stu-id="43f6b-137">No</span></span> |
| <span data-ttu-id="43f6b-138">É necessário recompilar o código</span><span class="sxs-lookup"><span data-stu-id="43f6b-138">Need to rebuild code</span></span> |<span data-ttu-id="43f6b-139">Sim</span><span class="sxs-lookup"><span data-stu-id="43f6b-139">Yes</span></span> | <span data-ttu-id="43f6b-140">Não</span><span class="sxs-lookup"><span data-stu-id="43f6b-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="43f6b-141">Monitorar um aplicativo da web ao vivo</span><span class="sxs-lookup"><span data-stu-id="43f6b-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="43f6b-142">Se seu aplicativo for executado como um serviço Web do Azure, veja como ativar o monitoramento:</span><span class="sxs-lookup"><span data-stu-id="43f6b-142">If your application is running as an Azure web service, here's how to switch on monitoring:</span></span>

* <span data-ttu-id="43f6b-143">Selecione o Application Insights no painel de controle do aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="43f6b-143">Select Application Insights on the app's control panel in Azure.</span></span>

    ![Configurar o Application Insights para um aplicativo Web do Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="43f6b-145">Quando a página de resumo do Application Insights for aberta, clique no link na parte inferior para abrir o recurso Application Insights completo.</span><span class="sxs-lookup"><span data-stu-id="43f6b-145">When the Application Insights summary page opens, click the link at the bottom to open the full Application Insights resource.</span></span>

    ![Clique até o Application Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="43f6b-147">[Monitoramento de aplicativos de nuvem e a VM](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="43f6b-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="43f6b-148">Habilitar o monitoramento do lado do cliente no Azure</span><span class="sxs-lookup"><span data-stu-id="43f6b-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="43f6b-149">Se você tiver habilitado o Application Insights no Azure, você poderá adicionar telemetria de usuário e exibição de página.</span><span class="sxs-lookup"><span data-stu-id="43f6b-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="43f6b-150">Selecione Configurações > Configurações do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="43f6b-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="43f6b-151">Em configurações do aplicativo, adicione um novo par de chave/valor:</span><span class="sxs-lookup"><span data-stu-id="43f6b-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="43f6b-152">Chave: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="43f6b-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="43f6b-153">Valor: `true`</span><span class="sxs-lookup"><span data-stu-id="43f6b-153">Value: `true`</span></span>
3. <span data-ttu-id="43f6b-154">**Salve** as configurações e **Reinicie** seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43f6b-154">**Save** the settings and **Restart** your app.</span></span>

<span data-ttu-id="43f6b-155">O SDK JavaScript do Application Insights agora é injetado em cada página da Web.</span><span class="sxs-lookup"><span data-stu-id="43f6b-155">The Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="43f6b-156">Monitorar um aplicativo de web IIS ao vivo</span><span class="sxs-lookup"><span data-stu-id="43f6b-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="43f6b-157">Se seu aplicativo estiver hospedado em um servidor do IIS, habilite o Application Insights usando o Monitor de Status.</span><span class="sxs-lookup"><span data-stu-id="43f6b-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="43f6b-158">No servidor Web IIS, entre com as credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="43f6b-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="43f6b-159">Se Application Insights Status Monitor ainda não estiver instalado, baixe e execute o [instalador do Status Monitor](http://go.microsoft.com/fwlink/?LinkId=506648) (ou execute o [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) e procure nele o Application Insights Status Monitor).</span><span class="sxs-lookup"><span data-stu-id="43f6b-159">If Application Insights Status Monitor is not already installed, download and run the [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="43f6b-160">No Monitor de Status, selecione o aplicativo Web ou o site que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="43f6b-160">In Status Monitor, select the installed web application or website that you want to monitor.</span></span> <span data-ttu-id="43f6b-161">Entre com suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="43f6b-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="43f6b-162">Configure o recurso onde você deseja ver os resultados no portal do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="43f6b-162">Configure the resource where you want to see the results in the Application Insights portal.</span></span> <span data-ttu-id="43f6b-163">(Normalmente, é melhor criar um novo recurso.</span><span class="sxs-lookup"><span data-stu-id="43f6b-163">(Normally, it's best to create a new resource.</span></span> <span data-ttu-id="43f6b-164">Selecione um recurso existente se você já tiver [testes da web][availability] ou [monitoramento de cliente][client] para esse aplicativo).</span><span class="sxs-lookup"><span data-stu-id="43f6b-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![Escolha um aplicativo e um recurso.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="43f6b-166">Reinicie o IIS.</span><span class="sxs-lookup"><span data-stu-id="43f6b-166">Restart IIS.</span></span>

    ![Escolha Reiniciar na parte superior da caixa de diálogo.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="43f6b-168">O serviço Web é interrompido por um período curto.</span><span class="sxs-lookup"><span data-stu-id="43f6b-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="43f6b-169">Personalizar opções de monitoramento</span><span class="sxs-lookup"><span data-stu-id="43f6b-169">Customize monitoring options</span></span>

<span data-ttu-id="43f6b-170">Habilitar o Application Insights adiciona DLLs e applicationinsights.config ao seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="43f6b-170">Enabling Application Insights adds DLLs and ApplicationInsights.config to your web app.</span></span> <span data-ttu-id="43f6b-171">Você pode [editar o arquivo .config](app-insights-configuration-with-applicationinsights-config.md) para alterar algumas opções.</span><span class="sxs-lookup"><span data-stu-id="43f6b-171">You can [edit the .config file](app-insights-configuration-with-applicationinsights-config.md) to change some of the options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="43f6b-172">Quando você publicar novamente seu aplicativo, habilite novamente o Application Insights</span><span class="sxs-lookup"><span data-stu-id="43f6b-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="43f6b-173">Antes de publicar novamente seu aplicativo, considere [adicionar Application Insights ao código no Visual Studio][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="43f6b-173">Before you re-publish your app, consider [adding Application Insights to the code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="43f6b-174">Você obterá uma telemetria mais detalhada e a capacidade de escrever telemetria personalizada.</span><span class="sxs-lookup"><span data-stu-id="43f6b-174">You'll get more detailed telemetry and the ability to write custom telemetry.</span></span>

<span data-ttu-id="43f6b-175">Se você deseja publicar novamente sem adicionar Application Insights no código, lembre-se de que o processo de implantação pode excluir as DLLs e applicationinsights.config do site publicado.</span><span class="sxs-lookup"><span data-stu-id="43f6b-175">If you want to re-publish without adding Application Insights to the code, be aware that the deployment process may delete the DLLs and ApplicationInsights.config from the published web site.</span></span> <span data-ttu-id="43f6b-176">Portanto:</span><span class="sxs-lookup"><span data-stu-id="43f6b-176">Therefore:</span></span>

1. <span data-ttu-id="43f6b-177">Se você tiver editado applicationinsights.config, faça uma cópia dele antes de publicar seu aplicativo novamente.</span><span class="sxs-lookup"><span data-stu-id="43f6b-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="43f6b-178">Republique seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43f6b-178">Republish your app.</span></span>
3. <span data-ttu-id="43f6b-179">Habilite novamente o monitoramento do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="43f6b-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="43f6b-180">(Use o método apropriado: o painel de controle do aplicativo Web do Azure ou o Monitor de Status em um host do IIS).</span><span class="sxs-lookup"><span data-stu-id="43f6b-180">(Use the appropriate method: either the Azure web app control panel, or the Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="43f6b-181">Reaplique as edições realizadas no arquivo .config.</span><span class="sxs-lookup"><span data-stu-id="43f6b-181">Reinstate any edits you performed on the .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="43f6b-182">Solução de problemas de configuração de tempo de execução do Application Insights</span><span class="sxs-lookup"><span data-stu-id="43f6b-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="43f6b-183">Não consegue se conectar?</span><span class="sxs-lookup"><span data-stu-id="43f6b-183">Can't connect?</span></span> <span data-ttu-id="43f6b-184">Sem telemetria?</span><span class="sxs-lookup"><span data-stu-id="43f6b-184">No telemetry?</span></span>

* <span data-ttu-id="43f6b-185">Abra [as portas de saída necessárias](app-insights-ip-addresses.md#outgoing-ports) no firewall de seu servidor para permitir o funcionamento do Status Monitor.</span><span class="sxs-lookup"><span data-stu-id="43f6b-185">Open [the necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall to allow Status Monitor to work.</span></span>

* <span data-ttu-id="43f6b-186">Abra o Monitor de Status e selecione seu aplicativo no painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="43f6b-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="43f6b-187">Verifique se há mensagens de diagnóstico para este aplicativo na seção "Configuração de notificações":</span><span class="sxs-lookup"><span data-stu-id="43f6b-187">Check if there are any diagnostics messages for this application in the "Configuration notifications" section:</span></span>

  ![Abra a folha de Desempenho para ver as solicitações, tempos de resposta, dependências e outros dados](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="43f6b-189">No servidor, se você encontrar uma mensagem sobre "permissões insuficientes", tente fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="43f6b-189">On the server, if you see a message about "insufficient permissions", try the following:</span></span>
  * <span data-ttu-id="43f6b-190">No Gerenciador do IIS, selecione o pool de aplicativos, abra **Configurações Avançadas** e no **Modelo de Processo**, anote a identidade.</span><span class="sxs-lookup"><span data-stu-id="43f6b-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note the identity.</span></span>
  * <span data-ttu-id="43f6b-191">No painel de controle de gerenciamento do computador, adicione essa identidade ao grupo Usuários do Monitor de Desempenho.</span><span class="sxs-lookup"><span data-stu-id="43f6b-191">In Computer management control panel, add this identity to the Performance Monitor Users group.</span></span>
* <span data-ttu-id="43f6b-192">Se você tiver o MMA/SCOM (Systems Center Operations Manager) instalado em seu servidor, algumas versões poderão entrar em conflito.</span><span class="sxs-lookup"><span data-stu-id="43f6b-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="43f6b-193">Desinstale o SCOM e o Monitor de Status e reinstale as versões mais recentes.</span><span class="sxs-lookup"><span data-stu-id="43f6b-193">Uninstall both SCOM and Status Monitor, and re-install the latest versions.</span></span>
* <span data-ttu-id="43f6b-194">Consulte [Solução de problemas][qna].</span><span class="sxs-lookup"><span data-stu-id="43f6b-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="43f6b-195">Requisitos do Sistema</span><span class="sxs-lookup"><span data-stu-id="43f6b-195">System Requirements</span></span>
<span data-ttu-id="43f6b-196">Suporte de sistema operacional para Application Insights Status Monitor no servidor:</span><span class="sxs-lookup"><span data-stu-id="43f6b-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="43f6b-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="43f6b-197">Windows Server 2008</span></span>
* <span data-ttu-id="43f6b-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="43f6b-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="43f6b-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="43f6b-199">Windows Server 2012</span></span>
* <span data-ttu-id="43f6b-200">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="43f6b-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="43f6b-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="43f6b-201">Windows Server 2016</span></span>

<span data-ttu-id="43f6b-202">com o SP mais recente e o .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="43f6b-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="43f6b-203">No lado do cliente, Windows 7, 8, 8.1 e 10, novamente com o .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="43f6b-203">On the client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="43f6b-204">Suporte ao IIS: IIS 7, 7,5, 8 e 8.5 (o IIS é obrigatório)</span><span class="sxs-lookup"><span data-stu-id="43f6b-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="43f6b-205">Automação com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="43f6b-205">Automation with PowerShell</span></span>
<span data-ttu-id="43f6b-206">Você pode iniciar e interromper o monitoramento usando o PowerShell no servidor IIS.</span><span class="sxs-lookup"><span data-stu-id="43f6b-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="43f6b-207">Primeiro, importe o módulo do Application Insights:</span><span class="sxs-lookup"><span data-stu-id="43f6b-207">First import the Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="43f6b-208">Saiba quais aplicativos estão sendo monitorados:</span><span class="sxs-lookup"><span data-stu-id="43f6b-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="43f6b-209">`-Name` (Opcional) O nome de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="43f6b-209">`-Name` (Optional) The name of a web app.</span></span>
* <span data-ttu-id="43f6b-210">Exibe o status de monitoramento do Application Insights para cada aplicativo Web (ou o aplicativo nomeado) nesse servidor IIS.</span><span class="sxs-lookup"><span data-stu-id="43f6b-210">Displays the Application Insights monitoring status for each web app (or the named app) in this IIS server.</span></span>
* <span data-ttu-id="43f6b-211">Retorna `ApplicationInsightsApplication` para cada aplicativo:</span><span class="sxs-lookup"><span data-stu-id="43f6b-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="43f6b-212">`SdkState==EnabledAfterDeployment`: o aplicativo está sendo monitorado e foi instrumentado em tempo de execução, pela ferramenta Monitor de Status ou pelo `Start-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="43f6b-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by the Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="43f6b-213">`SdkState==Disabled`: o aplicativo não é instrumentado para o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="43f6b-213">`SdkState==Disabled`: The app is not instrumented for Application Insights.</span></span> <span data-ttu-id="43f6b-214">Ele nunca foi instrumentado ou o monitoramento em tempo de execução foi desabilitado com a ferramenta Monitor de Status ou com o `Stop-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="43f6b-214">Either it was never instrumented, or run-time monitoring was disabled with the Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="43f6b-215">`SdkState==EnabledByCodeInstrumentation`: o aplicativo foi instrumentado por meio da adição do SDK ao código-fonte.</span><span class="sxs-lookup"><span data-stu-id="43f6b-215">`SdkState==EnabledByCodeInstrumentation`: The app was instrumented by adding the SDK to the source code.</span></span> <span data-ttu-id="43f6b-216">Seu SDK não pode ser atualizado ou interrompido.</span><span class="sxs-lookup"><span data-stu-id="43f6b-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="43f6b-217">`SdkVersion` mostra a versão em uso para o monitoramento do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43f6b-217">`SdkVersion` shows the version in use for monitoring this app.</span></span>
  * <span data-ttu-id="43f6b-218">`LatestAvailableSdkVersion`mostra a versão atualmente disponível na galeria do NuGet.</span><span class="sxs-lookup"><span data-stu-id="43f6b-218">`LatestAvailableSdkVersion`shows the version currently available on the NuGet gallery.</span></span> <span data-ttu-id="43f6b-219">Para atualizar o aplicativo para esta versão, use `Update-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="43f6b-219">To upgrade the app to this version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="43f6b-220">`-Name` O nome do aplicativo no IIS</span><span class="sxs-lookup"><span data-stu-id="43f6b-220">`-Name` The name of the app in IIS</span></span>
* <span data-ttu-id="43f6b-221">`-InstrumentationKey` O ikey do recurso Application Insights em que você deseja que os resultados sejam exibidos.</span><span class="sxs-lookup"><span data-stu-id="43f6b-221">`-InstrumentationKey` The ikey of the Application Insights resource where you want the results to be displayed.</span></span>
* <span data-ttu-id="43f6b-222">Este cmdlet afeta apenas os aplicativos que ainda não estão instrumentados - ou seja, SdkState==NotInstrumented.</span><span class="sxs-lookup"><span data-stu-id="43f6b-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="43f6b-223">O cmdlet não afeta um aplicativo que já é instrumentado.</span><span class="sxs-lookup"><span data-stu-id="43f6b-223">The cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="43f6b-224">Não importa se o aplicativo tiver sido instrumentado no momento da compilação por meio da adição do SDK ao código, ou em tempo de execução por meio de um uso anterior desse cmdlet.</span><span class="sxs-lookup"><span data-stu-id="43f6b-224">It does not matter whether the app was instrumented at build time by adding the SDK to the code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="43f6b-225">A versão do SDK usada para instrumentar o aplicativo é a versão baixada mais recentemente para este servidor.</span><span class="sxs-lookup"><span data-stu-id="43f6b-225">The SDK version used to instrument the app is the version that was most recently downloaded to this server.</span></span>

    <span data-ttu-id="43f6b-226">Para baixar a versão mais recente, use Update-ApplicationInsightsVersion.</span><span class="sxs-lookup"><span data-stu-id="43f6b-226">To download the latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="43f6b-227">Retorna `ApplicationInsightsApplication` se há êxito.</span><span class="sxs-lookup"><span data-stu-id="43f6b-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="43f6b-228">Se ele falhar, registrará em log um rastreamento para stderr.</span><span class="sxs-lookup"><span data-stu-id="43f6b-228">If it fails, it logs a trace to stderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="43f6b-229">`-Name` O nome de um aplicativo no IIS</span><span class="sxs-lookup"><span data-stu-id="43f6b-229">`-Name` The name of an app in IIS</span></span>
* <span data-ttu-id="43f6b-230">`-All` Para o monitoramento de todos os aplicativos desse servidor IIS para o qual `SdkState==EnabledAfterDeployment`</span><span class="sxs-lookup"><span data-stu-id="43f6b-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="43f6b-231">Para o monitoramento de aplicativos especificados e remove a instrumentação.</span><span class="sxs-lookup"><span data-stu-id="43f6b-231">Stops monitoring the specified apps and removes instrumentation.</span></span> <span data-ttu-id="43f6b-232">Ele só funciona para aplicativos que foram instrumentados em tempo de execução usando a ferramenta Monitoramento de Status ou Start-ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="43f6b-232">It only works for apps that have been instrumented at run-time using the Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="43f6b-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="43f6b-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="43f6b-234">Retorna ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="43f6b-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="43f6b-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="43f6b-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="43f6b-236">`-Name`: o nome de um aplicativo Web no IIS.</span><span class="sxs-lookup"><span data-stu-id="43f6b-236">`-Name`: The name of a web app in IIS.</span></span>
* <span data-ttu-id="43f6b-237">`-InstrumentationKey` (Opcional.) Use isso para alterar o recurso para o qual a telemetria do aplicativo é enviada.</span><span class="sxs-lookup"><span data-stu-id="43f6b-237">`-InstrumentationKey` (Optional.) Use this to change the resource to which the app's telemetry is sent.</span></span>
* <span data-ttu-id="43f6b-238">Este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="43f6b-238">This cmdlet:</span></span>
  * <span data-ttu-id="43f6b-239">Atualiza o aplicativo nomeado para a versão do SDK baixado mais recentemente para esta máquina.</span><span class="sxs-lookup"><span data-stu-id="43f6b-239">Upgrades the named app to the version of the SDK most recently downloaded to this machine.</span></span> <span data-ttu-id="43f6b-240">(Só funciona se `SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="43f6b-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="43f6b-241">Se você fornecer uma chave de instrumentação, o aplicativo nomeado será reconfigurado para enviar telemetria para o recurso com essa chave.</span><span class="sxs-lookup"><span data-stu-id="43f6b-241">If you provide an instrumentation key, the named app is reconfigured to send telemetry to the resource with that key.</span></span> <span data-ttu-id="43f6b-242">(Funciona se `SdkState != Disabled`)</span><span class="sxs-lookup"><span data-stu-id="43f6b-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="43f6b-243">Baixa o SDK mais recente do Application Insights para o servidor.</span><span class="sxs-lookup"><span data-stu-id="43f6b-243">Downloads the latest Application Insights SDK to the server.</span></span>

## <span data-ttu-id="43f6b-244"><a name="questions"></a>Perguntas sobre o Status Monitor</span><span class="sxs-lookup"><span data-stu-id="43f6b-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="43f6b-245">O que é o Status Monitor?</span><span class="sxs-lookup"><span data-stu-id="43f6b-245">What is Status Monitor?</span></span>

<span data-ttu-id="43f6b-246">Um aplicativo de desktop instalado no servidor web IIS.</span><span class="sxs-lookup"><span data-stu-id="43f6b-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="43f6b-247">Ele ajuda você instrumentar e configurar aplicativos web.</span><span class="sxs-lookup"><span data-stu-id="43f6b-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="43f6b-248">Quando eu devo usar o Status Monitor?</span><span class="sxs-lookup"><span data-stu-id="43f6b-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="43f6b-249">Para instrumentar qualquer aplicativo web em execução no servidor IIS - mesmo se ele já esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="43f6b-249">To instrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="43f6b-250">Para habilitar a telemetria adicional para aplicativos web que foram [compilados com o SDK do Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="43f6b-250">To enable additional telemetry for web apps that have been [built with the Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="43f6b-251">Eu posso fechá-lo depois de ser executado?</span><span class="sxs-lookup"><span data-stu-id="43f6b-251">Can I close it after it runs?</span></span>

<span data-ttu-id="43f6b-252">Sim.</span><span class="sxs-lookup"><span data-stu-id="43f6b-252">Yes.</span></span> <span data-ttu-id="43f6b-253">Depois dele instrumentar os sites selecionados, você pode fechá-lo.</span><span class="sxs-lookup"><span data-stu-id="43f6b-253">After it has instrumented the websites you select, you can close it.</span></span>

<span data-ttu-id="43f6b-254">Ele não coleta telemetria por si só.</span><span class="sxs-lookup"><span data-stu-id="43f6b-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="43f6b-255">Ele apenas configura os aplicativos web e define algumas permissões.</span><span class="sxs-lookup"><span data-stu-id="43f6b-255">It just configures the web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="43f6b-256">O que o Status Monitor faz?</span><span class="sxs-lookup"><span data-stu-id="43f6b-256">What does Status Monitor do?</span></span>

<span data-ttu-id="43f6b-257">Quando você seleciona um aplicativo web para o Status Monitor para instrumentar:</span><span class="sxs-lookup"><span data-stu-id="43f6b-257">When you select a web app for Status Monitor to instrument:</span></span>

* <span data-ttu-id="43f6b-258">Baixa e coloca os assemblies do Application Insights e o arquivo .config na pasta de binários do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="43f6b-258">Downloads and places the Application Insights assemblies and .config file in the web app's binaries folder.</span></span>
* <span data-ttu-id="43f6b-259">Modifica `web.config` para adicionar o módulo de rastreamento de HTTP do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="43f6b-259">Modifies `web.config` to add the Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="43f6b-260">Permite a criação de perfil do CLR para coletar chamadas de dependência.</span><span class="sxs-lookup"><span data-stu-id="43f6b-260">Enables CLR profiling to collect dependency calls.</span></span>

### <a name="do-i-need-to-run-status-monitor-whenever-i-update-the-app"></a><span data-ttu-id="43f6b-261">É necessário executar o Status Monitor sempre que eu atualizar o aplicativo?</span><span class="sxs-lookup"><span data-stu-id="43f6b-261">Do I need to run Status Monitor whenever I update the app?</span></span>

<span data-ttu-id="43f6b-262">Não ocorre se você reimplantar incrementalmente.</span><span class="sxs-lookup"><span data-stu-id="43f6b-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="43f6b-263">Se você selecionar a opção "Excluir arquivos existentes" no processo de publicação, você precisará executar novamente o Status Monitor para configurar o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="43f6b-263">If you select the 'delete existing files' option in the publish process, you would need to re-run Status Monitor to configure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="43f6b-264">Qual telemetria é coletada?</span><span class="sxs-lookup"><span data-stu-id="43f6b-264">What telemetry is collected?</span></span>

<span data-ttu-id="43f6b-265">Para aplicativos que você instrumenta apenas em tempo de execução usando o Status Monitor:</span><span class="sxs-lookup"><span data-stu-id="43f6b-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="43f6b-266">Solicitações HTTP</span><span class="sxs-lookup"><span data-stu-id="43f6b-266">HTTP requests</span></span>
* <span data-ttu-id="43f6b-267">Chamadas para dependências</span><span class="sxs-lookup"><span data-stu-id="43f6b-267">Calls to dependencies</span></span>
* <span data-ttu-id="43f6b-268">Exceções</span><span class="sxs-lookup"><span data-stu-id="43f6b-268">Exceptions</span></span>
* <span data-ttu-id="43f6b-269">Contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="43f6b-269">Performance counters</span></span>

<span data-ttu-id="43f6b-270">Para aplicativos já instrumentados em tempo de compilação:</span><span class="sxs-lookup"><span data-stu-id="43f6b-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="43f6b-271">Contadores de processo.</span><span class="sxs-lookup"><span data-stu-id="43f6b-271">Process counters.</span></span>
 * <span data-ttu-id="43f6b-272">Chamadas de dependência (.NET 4.5); valores de retorno em chamadas de dependência (.NET 4.6).</span><span class="sxs-lookup"><span data-stu-id="43f6b-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="43f6b-273">Exceção dos valores do rastreamento de pilha.</span><span class="sxs-lookup"><span data-stu-id="43f6b-273">Exception stack trace values.</span></span>

[<span data-ttu-id="43f6b-274">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="43f6b-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="43f6b-275">Vídeo</span><span class="sxs-lookup"><span data-stu-id="43f6b-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="43f6b-276"><a name="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="43f6b-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="43f6b-277">Exiba sua telemetria:</span><span class="sxs-lookup"><span data-stu-id="43f6b-277">View your telemetry:</span></span>

* <span data-ttu-id="43f6b-278">[Explore as métricas](app-insights-metrics-explorer.md) para monitorar o desempenho e o uso</span><span class="sxs-lookup"><span data-stu-id="43f6b-278">[Explore metrics](app-insights-metrics-explorer.md) to monitor performance and usage</span></span>
* <span data-ttu-id="43f6b-279">[Pesquise eventos e logs][diagnostic] para diagnosticar problemas</span><span class="sxs-lookup"><span data-stu-id="43f6b-279">[Search events and logs][diagnostic] to diagnose problems</span></span>
* <span data-ttu-id="43f6b-280">[Analise](app-insights-analytics.md) para obter mais consultas avançadas</span><span class="sxs-lookup"><span data-stu-id="43f6b-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="43f6b-281">Crie painéis</span><span class="sxs-lookup"><span data-stu-id="43f6b-281">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="43f6b-282">Adicione mais telemetria:</span><span class="sxs-lookup"><span data-stu-id="43f6b-282">Add more telemetry:</span></span>

* <span data-ttu-id="43f6b-283">[Crie testes na Web][availability] para ter a certeza de que seu site continua ativo.</span><span class="sxs-lookup"><span data-stu-id="43f6b-283">[Create web tests][availability] to make sure your site stays live.</span></span>
* <span data-ttu-id="43f6b-284">[Adicione telemetria de cliente Web][usage] para ver exceções de código de página Web e permitir que você insira rastreamento de chamadas.</span><span class="sxs-lookup"><span data-stu-id="43f6b-284">[Add web client telemetry][usage] to see exceptions from web page code and to let you insert trace calls.</span></span>
* <span data-ttu-id="43f6b-285">[Adicione SDK do Application Insights ao seu código][greenbrown] para que você possa inserir o rastreamento de chamadas de log</span><span class="sxs-lookup"><span data-stu-id="43f6b-285">[Add Application Insights SDK to your code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
