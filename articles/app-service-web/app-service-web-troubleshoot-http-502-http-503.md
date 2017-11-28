---
title: "gateway incorreto de aaaFix 502, 503 serviço indisponíveis erros | Microsoft Docs"
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
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="b3da8-104">Solucionar problemas de erros HTTP de "502 Gateway Incorreto" e "503 Serviço Indisponível" em seus Aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="b3da8-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="b3da8-105">"502 Gateway Incorreto" e "503 Serviço Indisponível" são os erros comuns em seu aplicativo Web hospedado no [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="b3da8-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="b3da8-106">Este artigo ajuda você a solucionar esses erros.</span><span class="sxs-lookup"><span data-stu-id="b3da8-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="b3da8-107">Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [hello Azure MSDN e Olá fóruns de estouro de pilha](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="b3da8-107">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="b3da8-108">Como alternativa, você também pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3da8-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="b3da8-109">Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e clique em **suporte**.</span><span class="sxs-lookup"><span data-stu-id="b3da8-109">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="b3da8-110">Sintoma</span><span class="sxs-lookup"><span data-stu-id="b3da8-110">Symptom</span></span>
<span data-ttu-id="b3da8-111">Quando você procurar o aplicativo web de toohello, ele retorna um HTTP um HTTP ou erro de "502 Gateway incorreto" erro "503 serviço não disponível".</span><span class="sxs-lookup"><span data-stu-id="b3da8-111">When you browse toohello web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="b3da8-112">Causa</span><span class="sxs-lookup"><span data-stu-id="b3da8-112">Cause</span></span>
<span data-ttu-id="b3da8-113">Esse problema geralmente é causado por questões no nível de aplicativo, como:</span><span class="sxs-lookup"><span data-stu-id="b3da8-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="b3da8-114">solicitações demorando muito</span><span class="sxs-lookup"><span data-stu-id="b3da8-114">requests taking a long time</span></span>
* <span data-ttu-id="b3da8-115">aplicativo usando muita memória/CPU</span><span class="sxs-lookup"><span data-stu-id="b3da8-115">application using high memory/CPU</span></span>
* <span data-ttu-id="b3da8-116">aplicativo falha devido a exceção tooan.</span><span class="sxs-lookup"><span data-stu-id="b3da8-116">application crashing due tooan exception.</span></span>

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="b3da8-117">Solução de problemas de erros de "503 Serviço indisponível" e etapas toosolve "502 gateway incorreto"</span><span class="sxs-lookup"><span data-stu-id="b3da8-117">Troubleshooting steps toosolve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="b3da8-118">A solução de problemas pode ser dividida em três tarefas distintas, em ordem sequencial:</span><span class="sxs-lookup"><span data-stu-id="b3da8-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="b3da8-119">Observar e monitorar o comportamento do aplicativo</span><span class="sxs-lookup"><span data-stu-id="b3da8-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="b3da8-120">Coletar dados</span><span class="sxs-lookup"><span data-stu-id="b3da8-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="b3da8-121">Reduzir o problema de saudação</span><span class="sxs-lookup"><span data-stu-id="b3da8-121">Mitigate hello issue</span></span>](#mitigate)

<span data-ttu-id="b3da8-122">[Os Aplicativos Web do Serviço de Aplicativo](/services/app-service/web/) oferecem várias opções em cada etapa.</span><span class="sxs-lookup"><span data-stu-id="b3da8-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="b3da8-123">1. Observar e monitorar o comportamento do aplicativo</span><span class="sxs-lookup"><span data-stu-id="b3da8-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="b3da8-124">Controlar a integridade do serviço</span><span class="sxs-lookup"><span data-stu-id="b3da8-124">Track Service health</span></span>
<span data-ttu-id="b3da8-125">O Microsoft Azure publica sempre que há uma degradação no desempenho ou interrupção do serviço.</span><span class="sxs-lookup"><span data-stu-id="b3da8-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="b3da8-126">Você pode acompanhar a integridade de saudação do serviço de saudação em Olá [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b3da8-126">You can track hello health of hello service on hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="b3da8-127">Para obter mais informações, confira [Controlar a integridade do serviço](../monitoring-and-diagnostics/insights-service-health.md).</span><span class="sxs-lookup"><span data-stu-id="b3da8-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="b3da8-128">Monitorar seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="b3da8-128">Monitor your web app</span></span>
<span data-ttu-id="b3da8-129">Essa opção permite que você toofind out se seu aplicativo estiver com problemas.</span><span class="sxs-lookup"><span data-stu-id="b3da8-129">This option enables you toofind out if your application is having any issues.</span></span> <span data-ttu-id="b3da8-130">Na folha do seu aplicativo web, clique em Olá **solicitações e erros** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="b3da8-130">In your web app’s blade, click hello **Requests and errors** tile.</span></span> <span data-ttu-id="b3da8-131">Olá **métrica** folha mostrará todas as métricas de saudação, você pode adicionar.</span><span class="sxs-lookup"><span data-stu-id="b3da8-131">hello **Metric** blade will show you all hello metrics you can add.</span></span>

<span data-ttu-id="b3da8-132">Algumas das métricas de saudação que você pode querer toomonitor de seu aplicativo web são</span><span class="sxs-lookup"><span data-stu-id="b3da8-132">Some of hello metrics that you might want toomonitor for your web app are</span></span>

* <span data-ttu-id="b3da8-133">Conjunto de trabalho de memória média</span><span class="sxs-lookup"><span data-stu-id="b3da8-133">Average memory working set</span></span>
* <span data-ttu-id="b3da8-134">Tempo médio de resposta</span><span class="sxs-lookup"><span data-stu-id="b3da8-134">Average response time</span></span>
* <span data-ttu-id="b3da8-135">Tempo de CPU</span><span class="sxs-lookup"><span data-stu-id="b3da8-135">CPU time</span></span>
* <span data-ttu-id="b3da8-136">Conjunto de trabalho de memória</span><span class="sxs-lookup"><span data-stu-id="b3da8-136">Memory working set</span></span>
* <span data-ttu-id="b3da8-137">Solicitações</span><span class="sxs-lookup"><span data-stu-id="b3da8-137">Requests</span></span>

![monitorar aplicativo Web para solucionar problemas de erros HTTP de 502 Gateway Incorreto e 503 Serviço Indisponível](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="b3da8-139">Para obter mais informações, confira:</span><span class="sxs-lookup"><span data-stu-id="b3da8-139">For more information, see:</span></span>

* [<span data-ttu-id="b3da8-140">Monitorar aplicativos Web no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="b3da8-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="b3da8-141">Receber notificações de alerta</span><span class="sxs-lookup"><span data-stu-id="b3da8-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="b3da8-142">2. Coletar dados</span><span class="sxs-lookup"><span data-stu-id="b3da8-142">2. Collect data</span></span>
#### <a name="use-hello-azure-app-service-support-portal"></a><span data-ttu-id="b3da8-143">Use Olá Portal de suporte do serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="b3da8-143">Use hello Azure App Service Support Portal</span></span>
<span data-ttu-id="b3da8-144">Os aplicativos Web fornece Olá capacidade tootroubleshoot problemas relacionados tooyour web aplicativo examinando HTTP logs, logs de eventos, os despejos de processo e muito mais.</span><span class="sxs-lookup"><span data-stu-id="b3da8-144">Web Apps provides you with hello ability tootroubleshoot issues related tooyour web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="b3da8-145">Você pode acessar todas essas informações usando nosso portal de Suporte em **http://&lt;nome do aplicativo>.scm.azurewebsites.net/Support**</span><span class="sxs-lookup"><span data-stu-id="b3da8-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="b3da8-146">portal de suporte de serviço de aplicativo do Azure Olá fornece três guias separadas toosupport Olá três etapas de um cenário de solução de problemas comuns:</span><span class="sxs-lookup"><span data-stu-id="b3da8-146">hello Azure App Service Support portal provides you with three separate tabs toosupport hello three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="b3da8-147">Observar o comportamento atual</span><span class="sxs-lookup"><span data-stu-id="b3da8-147">Observe current behavior</span></span>
2. <span data-ttu-id="b3da8-148">Analisar a coleta de informações de diagnóstico e executando Olá analisadores internos</span><span class="sxs-lookup"><span data-stu-id="b3da8-148">Analyze by collecting diagnostics information and running hello built-in analyzers</span></span>
3. <span data-ttu-id="b3da8-149">Atenuar</span><span class="sxs-lookup"><span data-stu-id="b3da8-149">Mitigate</span></span>

<span data-ttu-id="b3da8-150">Se o problema de saudação estiver ocorrendo no momento, clique em **analisar** > **diagnóstico** > **diagnosticar agora** toocreate uma sessão de diagnóstico para você, que coletará HTTP logs, logs do Visualizador de eventos, PHP, logs de erros do PHP e despejos de processam o relatório de memória.</span><span class="sxs-lookup"><span data-stu-id="b3da8-150">If hello issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** toocreate a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="b3da8-151">Depois de saudação os dados são coletados, também será executar uma análise em dados de saudação e fornecer um relatório HTML.</span><span class="sxs-lookup"><span data-stu-id="b3da8-151">Once hello data is collected, it will also run an analysis on hello data and provide you with an HTML report.</span></span>

<span data-ttu-id="b3da8-152">Caso você deseje dados de saudação toodownload, por padrão, ele seria armazenado na pasta de D:\home\data\DaaS hello.</span><span class="sxs-lookup"><span data-stu-id="b3da8-152">In case you want toodownload hello data, by default, it would be stored in hello D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="b3da8-153">Para obter mais informações sobre o portal de suporte de serviço de aplicativo do Azure hello, consulte [tooSupport de novas atualizações a extensão de Site para sites do Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="b3da8-153">For more information on hello Azure App Service Support portal, see [New Updates tooSupport Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-hello-kudu-debug-console"></a><span data-ttu-id="b3da8-154">Use Olá Kudu Console de depuração</span><span class="sxs-lookup"><span data-stu-id="b3da8-154">Use hello Kudu Debug Console</span></span>
<span data-ttu-id="b3da8-155">Aplicativos Web vêm com um console de depuração que você pode usar para depuração, exploração, carregamento de arquivos, bem como para pontos de extremidade JSON para obter informações sobre seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="b3da8-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="b3da8-156">Isso é chamado hello *Kudu Console* ou hello *SCM painel* para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="b3da8-156">This is called hello *Kudu Console* or hello *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="b3da8-157">Você pode acessar este painel, vai toohello link **https://&lt;nome do aplicativo >.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="b3da8-157">You can access this dashboard by going toohello link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="b3da8-158">Algumas das coisas Olá Kudu oferece são:</span><span class="sxs-lookup"><span data-stu-id="b3da8-158">Some of hello things that Kudu provides are:</span></span>

* <span data-ttu-id="b3da8-159">configurações de ambiente para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="b3da8-159">environment settings for your application</span></span>
* <span data-ttu-id="b3da8-160">fluxo de logs</span><span class="sxs-lookup"><span data-stu-id="b3da8-160">log stream</span></span>
* <span data-ttu-id="b3da8-161">despejos de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="b3da8-161">diagnostic dump</span></span>
* <span data-ttu-id="b3da8-162">console de depuração no qual você pode executar os cmdlets do Powershell e os comandos básicos de DOS.</span><span class="sxs-lookup"><span data-stu-id="b3da8-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="b3da8-163">Outro recurso útil de Kudu é que, no caso de seu aplicativo está gerando exceções de primeira chance, você pode usar o Kudu e despejos de memória do hello SysInternals ferramenta Procdump toocreate.</span><span class="sxs-lookup"><span data-stu-id="b3da8-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and hello SysInternals tool Procdump toocreate memory dumps.</span></span> <span data-ttu-id="b3da8-164">Esses despejos de memória são instantâneos do processo de saudação e podem geralmente ajudá-lo a solucionar problemas mais complexos com seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="b3da8-164">These memory dumps are snapshots of hello process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="b3da8-165">Para saber mais sobre recursos disponíveis no Kudu, consulte [Ferramentas online de Sites do Azure que você deve conhecer](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span><span class="sxs-lookup"><span data-stu-id="b3da8-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a><span data-ttu-id="b3da8-166">3. Reduzir o problema de saudação</span><span class="sxs-lookup"><span data-stu-id="b3da8-166">3. Mitigate hello issue</span></span>
#### <a name="scale-hello-web-app"></a><span data-ttu-id="b3da8-167">Escala Olá web app</span><span class="sxs-lookup"><span data-stu-id="b3da8-167">Scale hello web app</span></span>
<span data-ttu-id="b3da8-168">No serviço de aplicativo do Azure, para aumentar o desempenho e a taxa de transferência, você pode ajustar a escala de saudação em que você estiver executando o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b3da8-168">In Azure App Service, for increased performance and throughput,  you can adjust hello scale at which you are running your application.</span></span> <span data-ttu-id="b3da8-169">Dimensionamento de um aplicativo web envolve duas ações relacionadas: alterando sua tooa de plano de serviço de aplicativo maior preço e determinadas configurações após a troca de toohello maior preço.</span><span class="sxs-lookup"><span data-stu-id="b3da8-169">Scaling up a web app involves two related actions: changing your App Service plan tooa higher pricing tier, and configuring certain settings after you have switched toohello higher pricing tier.</span></span>

<span data-ttu-id="b3da8-170">Para saber mais sobre como escalar, consulte [Escalar um aplicativo Web no Serviço de Aplicativo do Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="b3da8-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="b3da8-171">Além disso, você pode escolher toorun seu aplicativo em mais de uma instância.</span><span class="sxs-lookup"><span data-stu-id="b3da8-171">Additionally, you can choose toorun your application on more than one instance .</span></span> <span data-ttu-id="b3da8-172">Isso não apenas fornece mais capacidade de processamento, como também oferece alguma quantidade de tolerância a falhas.</span><span class="sxs-lookup"><span data-stu-id="b3da8-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="b3da8-173">Se hello processo falhar em uma instância, hello outra instância ainda continuará atender solicitações.</span><span class="sxs-lookup"><span data-stu-id="b3da8-173">If hello process goes down on one instance, hello other instance will still continue serving requests.</span></span>

<span data-ttu-id="b3da8-174">Você pode definir Olá dimensionamento toobe Manual ou automático.</span><span class="sxs-lookup"><span data-stu-id="b3da8-174">You can set hello scaling toobe Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="b3da8-175">Usar AutoHeal</span><span class="sxs-lookup"><span data-stu-id="b3da8-175">Use AutoHeal</span></span>
<span data-ttu-id="b3da8-176">O AutoHeal recicla o processo do operador de saudação para seu aplicativo com base nas configurações que você escolha (como as alterações de configuração, solicitações, limites de memória ou tempo de saudação necessário tooexecute uma solicitação).</span><span class="sxs-lookup"><span data-stu-id="b3da8-176">AutoHeal recycles hello worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or hello time needed tooexecute a request).</span></span> <span data-ttu-id="b3da8-177">A maioria do tempo de saudação Reciclar processos do hello são Olá toorecover de maneira mais rápida de um problema.</span><span class="sxs-lookup"><span data-stu-id="b3da8-177">Most of hello time, recycle hello process is hello fastest way toorecover from a problem.</span></span> <span data-ttu-id="b3da8-178">Embora você sempre pode reiniciar aplicativo web de saudação do diretamente dentro de saudação Portal do Azure, AutoHeal fará automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="b3da8-178">Though you can always restart hello web app from directly within hello Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="b3da8-179">Você só precisa toodo é adicionar alguns gatilhos no Web. config de raiz de saudação para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="b3da8-179">All you need toodo is add some triggers in hello root web.config for your web app.</span></span> <span data-ttu-id="b3da8-180">Observe que essas configurações funcionaria em Olá mesma forma, mesmo que seu aplicativo não é um .net.</span><span class="sxs-lookup"><span data-stu-id="b3da8-180">Note that these settings would work in hello same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="b3da8-181">Para saber mais, consulte [AutoHeal em sites do Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="b3da8-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-hello-web-app"></a><span data-ttu-id="b3da8-182">Reiniciar o aplicativo web de saudação</span><span class="sxs-lookup"><span data-stu-id="b3da8-182">Restart hello web app</span></span>
<span data-ttu-id="b3da8-183">Isso geralmente é Olá toorecover de maneira mais simples de problemas ocasionais.</span><span class="sxs-lookup"><span data-stu-id="b3da8-183">This is often hello simplest way toorecover from one-time issues.</span></span> <span data-ttu-id="b3da8-184">Em Olá [Portal do Azure](https://portal.azure.com/), na folha do seu aplicativo web, você tem Olá opções toostop ou reiniciar o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b3da8-184">On hello [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have hello options toostop or restart your app.</span></span>

 ![Reinicie os erros do aplicativo toosolve HTTP 502 gateway incorreto e 503 serviço não disponível](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="b3da8-186">Você também pode gerenciar seu aplicativo Web usando o Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="b3da8-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="b3da8-187">Para obter mais informações, consulte [Usando o PowerShell do Azure com o Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b3da8-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

