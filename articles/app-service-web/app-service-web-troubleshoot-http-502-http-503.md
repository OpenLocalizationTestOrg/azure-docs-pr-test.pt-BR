---
title: "Corrigir os erros 502 Gateway Incorreto e 503 Serviço Indisponíveis | Microsoft Docs"
description: "Solucionar problemas dos erros \"502 Gateway Incorreto\" e \"503 Serviço Indisponível\" no seu aplicativo Web hospedado no Serviço de Aplicativo do Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "502 Gateway Incorreto, 503 Serviço Indisponível, erro 503, erro 502"
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 397a6aaf7dc27adfa0fc0e722b8a2be5cc1d75f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="2502f-104">Solucionar problemas de erros HTTP de "502 Gateway Incorreto" e "503 Serviço Indisponível" em seus Aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="2502f-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="2502f-105">"502 Gateway Incorreto" e "503 Serviço Indisponível" são os erros comuns em seu aplicativo Web hospedado no [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="2502f-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="2502f-106">Este artigo ajuda você a solucionar esses erros.</span><span class="sxs-lookup"><span data-stu-id="2502f-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="2502f-107">Se você precisar de mais ajuda em qualquer momento neste artigo, você pode contatar os especialistas do Azure nos [fóruns do Azure MSDN e Excedente de Pilha](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="2502f-107">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="2502f-108">Como alternativa, você também pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="2502f-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="2502f-109">Acesse o [site de Suporte do Azure](https://azure.microsoft.com/support/options/) e clique em **Obter Suporte**.</span><span class="sxs-lookup"><span data-stu-id="2502f-109">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="2502f-110">Sintoma</span><span class="sxs-lookup"><span data-stu-id="2502f-110">Symptom</span></span>
<span data-ttu-id="2502f-111">Quando você navega até o aplicativo Web, ele retorna um erro de HTTP “502 Gateway Incorreto” ou um “503 Serviço Indisponível”.</span><span class="sxs-lookup"><span data-stu-id="2502f-111">When you browse to the web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="2502f-112">Causa</span><span class="sxs-lookup"><span data-stu-id="2502f-112">Cause</span></span>
<span data-ttu-id="2502f-113">Esse problema geralmente é causado por questões no nível de aplicativo, como:</span><span class="sxs-lookup"><span data-stu-id="2502f-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="2502f-114">solicitações demorando muito</span><span class="sxs-lookup"><span data-stu-id="2502f-114">requests taking a long time</span></span>
* <span data-ttu-id="2502f-115">aplicativo usando muita memória/CPU</span><span class="sxs-lookup"><span data-stu-id="2502f-115">application using high memory/CPU</span></span>
* <span data-ttu-id="2502f-116">aplicativo falhando devido a uma exceção.</span><span class="sxs-lookup"><span data-stu-id="2502f-116">application crashing due to an exception.</span></span>

## <a name="troubleshooting-steps-to-solve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="2502f-117">Etapas de solução de problemas para resolver erros de "502 Gateway Incorreto" e "503 Serviço Indisponível"</span><span class="sxs-lookup"><span data-stu-id="2502f-117">Troubleshooting steps to solve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="2502f-118">A solução de problemas pode ser dividida em três tarefas distintas, em ordem sequencial:</span><span class="sxs-lookup"><span data-stu-id="2502f-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="2502f-119">Observar e monitorar o comportamento do aplicativo</span><span class="sxs-lookup"><span data-stu-id="2502f-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="2502f-120">Coletar dados</span><span class="sxs-lookup"><span data-stu-id="2502f-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="2502f-121">Atenuar o problema</span><span class="sxs-lookup"><span data-stu-id="2502f-121">Mitigate the issue</span></span>](#mitigate)

<span data-ttu-id="2502f-122">[Os Aplicativos Web do Serviço de Aplicativo](/services/app-service/web/) oferecem várias opções em cada etapa.</span><span class="sxs-lookup"><span data-stu-id="2502f-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="2502f-123">1. Observar e monitorar o comportamento do aplicativo</span><span class="sxs-lookup"><span data-stu-id="2502f-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="2502f-124">Controlar a integridade do serviço</span><span class="sxs-lookup"><span data-stu-id="2502f-124">Track Service health</span></span>
<span data-ttu-id="2502f-125">O Microsoft Azure publica sempre que há uma degradação no desempenho ou interrupção do serviço.</span><span class="sxs-lookup"><span data-stu-id="2502f-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="2502f-126">Você pode controlar a integridade do serviço no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2502f-126">You can track the health of the service on the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="2502f-127">Para obter mais informações, confira [Controlar a integridade do serviço](../monitoring-and-diagnostics/insights-service-health.md).</span><span class="sxs-lookup"><span data-stu-id="2502f-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="2502f-128">Monitorar seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="2502f-128">Monitor your web app</span></span>
<span data-ttu-id="2502f-129">Essa opção permite que você descubra se seu aplicativo está com problemas.</span><span class="sxs-lookup"><span data-stu-id="2502f-129">This option enables you to find out if your application is having any issues.</span></span> <span data-ttu-id="2502f-130">Na folha de seu aplicativo Web, clique no bloco **Solicitações e erros** .</span><span class="sxs-lookup"><span data-stu-id="2502f-130">In your web app’s blade, click the **Requests and errors** tile.</span></span> <span data-ttu-id="2502f-131">A folha **Métrica** mostrará todas as métricas que você pode adicionar.</span><span class="sxs-lookup"><span data-stu-id="2502f-131">The **Metric** blade will show you all the metrics you can add.</span></span>

<span data-ttu-id="2502f-132">Algumas das métricas que deseja monitorar para seu aplicativo Web são</span><span class="sxs-lookup"><span data-stu-id="2502f-132">Some of the metrics that you might want to monitor for your web app are</span></span>

* <span data-ttu-id="2502f-133">Conjunto de trabalho de memória média</span><span class="sxs-lookup"><span data-stu-id="2502f-133">Average memory working set</span></span>
* <span data-ttu-id="2502f-134">Tempo médio de resposta</span><span class="sxs-lookup"><span data-stu-id="2502f-134">Average response time</span></span>
* <span data-ttu-id="2502f-135">Tempo de CPU</span><span class="sxs-lookup"><span data-stu-id="2502f-135">CPU time</span></span>
* <span data-ttu-id="2502f-136">Conjunto de trabalho de memória</span><span class="sxs-lookup"><span data-stu-id="2502f-136">Memory working set</span></span>
* <span data-ttu-id="2502f-137">Solicitações</span><span class="sxs-lookup"><span data-stu-id="2502f-137">Requests</span></span>

![monitorar aplicativo Web para solucionar problemas de erros HTTP de 502 Gateway Incorreto e 503 Serviço Indisponível](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="2502f-139">Para obter mais informações, confira:</span><span class="sxs-lookup"><span data-stu-id="2502f-139">For more information, see:</span></span>

* [<span data-ttu-id="2502f-140">Monitorar aplicativos Web no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="2502f-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="2502f-141">Receber notificações de alerta</span><span class="sxs-lookup"><span data-stu-id="2502f-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="2502f-142">2. Coletar dados</span><span class="sxs-lookup"><span data-stu-id="2502f-142">2. Collect data</span></span>
#### <a name="use-the-azure-app-service-support-portal"></a><span data-ttu-id="2502f-143">Usar o Portal de Suporte do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="2502f-143">Use the Azure App Service Support Portal</span></span>
<span data-ttu-id="2502f-144">Os Aplicativos Web fornecem a capacidade de solucionar problemas relacionados ao seu aplicativo Web examinando logs de HTTP, logs de eventos, despejos de processo e muito mais.</span><span class="sxs-lookup"><span data-stu-id="2502f-144">Web Apps provides you with the ability to troubleshoot issues related to your web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="2502f-145">Você pode acessar todas essas informações usando nosso portal de Suporte em **http://&lt;nome do aplicativo>.scm.azurewebsites.net/Support**</span><span class="sxs-lookup"><span data-stu-id="2502f-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="2502f-146">O portal de Suporte do Serviço de Aplicativo do Azure fornece três guias separadas para dar suporte às três etapas de um cenário de solução de problemas comum:</span><span class="sxs-lookup"><span data-stu-id="2502f-146">The Azure App Service Support portal provides you with three separate tabs to support the three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="2502f-147">Observar o comportamento atual</span><span class="sxs-lookup"><span data-stu-id="2502f-147">Observe current behavior</span></span>
2. <span data-ttu-id="2502f-148">Analisar por meio da coleta das informações de diagnóstico e da execução dos analisadores internos</span><span class="sxs-lookup"><span data-stu-id="2502f-148">Analyze by collecting diagnostics information and running the built-in analyzers</span></span>
3. <span data-ttu-id="2502f-149">Atenuar</span><span class="sxs-lookup"><span data-stu-id="2502f-149">Mitigate</span></span>

<span data-ttu-id="2502f-150">Se o problema estiver ocorrendo no momento, clique em **Analisar** > **Diagnóstico** > **Diagnosticar Agora** para criar uma sessão de diagnóstico para você, que coletará logs de HTTP, logs do visualizador de eventos, despejos de memória, logs de erros de PHP e relatórios de processo de PHP.</span><span class="sxs-lookup"><span data-stu-id="2502f-150">If the issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** to create a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="2502f-151">Depois que os dados são coletados, ele também executará uma análise dos dados e fornecerá um relatório HTML.</span><span class="sxs-lookup"><span data-stu-id="2502f-151">Once the data is collected, it will also run an analysis on the data and provide you with an HTML report.</span></span>

<span data-ttu-id="2502f-152">Caso queira baixar os dados, por padrão, estariam armazenados na pasta D:\home\data\DaaS.</span><span class="sxs-lookup"><span data-stu-id="2502f-152">In case you want to download the data, by default, it would be stored in the D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="2502f-153">Para saber mais sobre o portal de Suporte do Serviço de Aplicativo do Azure, consulte [Novas atualizações para suporte de extensão de sites para sites do Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="2502f-153">For more information on the Azure App Service Support portal, see [New Updates to Support Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-the-kudu-debug-console"></a><span data-ttu-id="2502f-154">Usar o Console de Depuração Kudu</span><span class="sxs-lookup"><span data-stu-id="2502f-154">Use the Kudu Debug Console</span></span>
<span data-ttu-id="2502f-155">Aplicativos Web vêm com um console de depuração que você pode usar para depuração, exploração, carregamento de arquivos, bem como para pontos de extremidade JSON para obter informações sobre seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="2502f-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="2502f-156">Chama-se *Console Kudu* ou *Painel SCM* de seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="2502f-156">This is called the *Kudu Console* or the *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="2502f-157">Você pode acessar este painel acessando o link **https://&lt;Nome do aplicativo>.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="2502f-157">You can access this dashboard by going to the link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="2502f-158">Estas são algumas das coisas que o Kudu fornece:</span><span class="sxs-lookup"><span data-stu-id="2502f-158">Some of the things that Kudu provides are:</span></span>

* <span data-ttu-id="2502f-159">configurações de ambiente para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="2502f-159">environment settings for your application</span></span>
* <span data-ttu-id="2502f-160">fluxo de logs</span><span class="sxs-lookup"><span data-stu-id="2502f-160">log stream</span></span>
* <span data-ttu-id="2502f-161">despejos de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="2502f-161">diagnostic dump</span></span>
* <span data-ttu-id="2502f-162">console de depuração no qual você pode executar os cmdlets do Powershell e os comandos básicos de DOS.</span><span class="sxs-lookup"><span data-stu-id="2502f-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="2502f-163">Outro recurso útil do Kudu é que, caso seu aplicativo esteja lançando exceções de primeira chance, você pode usar o Kudu e o despejo de processo da ferramenta SysInternals para criar despejos de memória.</span><span class="sxs-lookup"><span data-stu-id="2502f-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and the SysInternals tool Procdump to create memory dumps.</span></span> <span data-ttu-id="2502f-164">Esses despejos de memória são instantâneos do processo e podem frequentemente ajudá-lo a solucionar problemas mais complexos com seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="2502f-164">These memory dumps are snapshots of the process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="2502f-165">Para saber mais sobre recursos disponíveis no Kudu, consulte [Ferramentas online de Sites do Azure que você deve conhecer](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span><span class="sxs-lookup"><span data-stu-id="2502f-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-the-issue"></a><span data-ttu-id="2502f-166">3. Atenuar o problema</span><span class="sxs-lookup"><span data-stu-id="2502f-166">3. Mitigate the issue</span></span>
#### <a name="scale-the-web-app"></a><span data-ttu-id="2502f-167">Escalar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="2502f-167">Scale the web app</span></span>
<span data-ttu-id="2502f-168">No Serviço de Aplicativo do Azure, para um melhor desempenho e taxa de transferência, você pode ajustar a escala na qual você está executando seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2502f-168">In Azure App Service, for increased performance and throughput,  you can adjust the scale at which you are running your application.</span></span> <span data-ttu-id="2502f-169">Escalar verticalmente aplicativos Web envolve duas ações relacionadas: alterar seu plano do Serviço de Aplicativo para um tipo de preço mais alto e configurar determinadas configurações depois de ter mudado para o tipo de preço mais alto.</span><span class="sxs-lookup"><span data-stu-id="2502f-169">Scaling up a web app involves two related actions: changing your App Service plan to a higher pricing tier, and configuring certain settings after you have switched to the higher pricing tier.</span></span>

<span data-ttu-id="2502f-170">Para saber mais sobre como escalar, consulte [Escalar um aplicativo Web no Serviço de Aplicativo do Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="2502f-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="2502f-171">Além disso, você pode optar por executar o aplicativo em mais de uma instância.</span><span class="sxs-lookup"><span data-stu-id="2502f-171">Additionally, you can choose to run your application on more than one instance .</span></span> <span data-ttu-id="2502f-172">Isso não apenas fornece mais capacidade de processamento, como também oferece alguma quantidade de tolerância a falhas.</span><span class="sxs-lookup"><span data-stu-id="2502f-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="2502f-173">Se o processo falhar em uma instância, a outra instância ainda continuará atendendo a solicitações.</span><span class="sxs-lookup"><span data-stu-id="2502f-173">If the process goes down on one instance, the other instance will still continue serving requests.</span></span>

<span data-ttu-id="2502f-174">Você pode definir a escala para ser Manual ou Automática.</span><span class="sxs-lookup"><span data-stu-id="2502f-174">You can set the scaling to be Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="2502f-175">Usar AutoHeal</span><span class="sxs-lookup"><span data-stu-id="2502f-175">Use AutoHeal</span></span>
<span data-ttu-id="2502f-176">O AutoHeal recicla o processo de trabalho para seu aplicativo com base nas configurações que você escolher (como alterações de configuração, solicitações, limites baseados na memória ou o tempo necessário para executar uma solicitação).</span><span class="sxs-lookup"><span data-stu-id="2502f-176">AutoHeal recycles the worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or the time needed to execute a request).</span></span> <span data-ttu-id="2502f-177">Na maioria das vezes, reciclar o processo é a maneira mais rápida de resolver um problema.</span><span class="sxs-lookup"><span data-stu-id="2502f-177">Most of the time, recycle the process is the fastest way to recover from a problem.</span></span> <span data-ttu-id="2502f-178">Embora você possa sempre reiniciar o aplicativo Web diretamente no Portal do Azure, o AutoHeal fará isso automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2502f-178">Though you can always restart the web app from directly within the Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="2502f-179">Tudo que você precisa fazer é adicionar alguns gatilhos na raiz web.config de seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="2502f-179">All you need to do is add some triggers in the root web.config for your web app.</span></span> <span data-ttu-id="2502f-180">Observe que essas configurações devem funcionar da mesma forma ainda que seu aplicativo não seja um .Net.</span><span class="sxs-lookup"><span data-stu-id="2502f-180">Note that these settings would work in the same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="2502f-181">Para saber mais, consulte [AutoHeal em sites do Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="2502f-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-the-web-app"></a><span data-ttu-id="2502f-182">Reiniciar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="2502f-182">Restart the web app</span></span>
<span data-ttu-id="2502f-183">Esta é geralmente a maneira mais simples de se recuperar de problemas de uso únicos.</span><span class="sxs-lookup"><span data-stu-id="2502f-183">This is often the simplest way to recover from one-time issues.</span></span> <span data-ttu-id="2502f-184">No [Portal do Azure](https://portal.azure.com/), na folha de seu aplicativo Web, existem as opções para parar ou reiniciar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2502f-184">On the [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have the options to stop or restart your app.</span></span>

 ![reiniciar o aplicativo para solucionar os erros HTTP de 502 Gateway Incorreto e 503 Serviço Indisponível](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="2502f-186">Você também pode gerenciar seu aplicativo Web usando o Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="2502f-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="2502f-187">Para obter mais informações, consulte [Usando o PowerShell do Azure com o Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2502f-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

