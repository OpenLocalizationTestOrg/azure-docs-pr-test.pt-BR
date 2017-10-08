---
title: um aplicativo Web de aaaMonitor | Microsoft Docs
description: Saiba como tooset o monitoramento em seu aplicativo Web
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="0027b-103">Monitorar o Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="0027b-103">Monitor App Service</span></span>
<span data-ttu-id="0027b-104">Este tutorial orienta você por seu aplicativo de monitoramento e usando os problemas de toosolve de ferramentas de plataforma interna hello quando eles ocorrerem.</span><span class="sxs-lookup"><span data-stu-id="0027b-104">This tutorial walks you through monitoring your app and using hello built-in platform tools toosolve problems when they occur.</span></span>

<span data-ttu-id="0027b-105">Cada seção deste documento será um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="0027b-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="0027b-106">Usar recursos de saudação juntos permitem que você:</span><span class="sxs-lookup"><span data-stu-id="0027b-106">Using hello features together let you:</span></span>
- <span data-ttu-id="0027b-107">Identificar um problema em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0027b-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="0027b-108">Determinando quando o problema de saudação é causado pela sua plataforma de código ou hello.</span><span class="sxs-lookup"><span data-stu-id="0027b-108">Determining when hello issue is caused by your code or hello platform.</span></span>
- <span data-ttu-id="0027b-109">Restrinja a origem de saudação de problema de saudação em seu código.</span><span class="sxs-lookup"><span data-stu-id="0027b-109">Narrow down hello source of hello problem in your code.</span></span>
- <span data-ttu-id="0027b-110">Depure e corrija o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="0027b-110">Debugging and fixing hello issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0027b-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="0027b-111">Before you begin</span></span>
- <span data-ttu-id="0027b-112">Você precisa de um aplicativo Web toomonitor e siga Olá descritas etapas.</span><span class="sxs-lookup"><span data-stu-id="0027b-112">You need a Web App toomonitor and follow hello outlined steps.</span></span>
    - <span data-ttu-id="0027b-113">Você pode criar um aplicativo hello etapas descritas Olá [criar um aplicativo ASP.NET no Azure com o banco de dados SQL](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="0027b-113">You can create an application following hello steps described in hello [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="0027b-114">Se você quiser tootry out **depuração remota** do seu aplicativo, você precisará do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0027b-114">If you want tootry out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="0027b-115">Se você ainda não tiver o Visual Studio de 2017 instalado, você pode baixar e usar Olá livre [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0027b-115">If you don’t already have Visual Studio 2017 installed, you can download and use hello free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="0027b-116">Certifique-se de que você habilite **desenvolvimento do Azure** durante a instalação do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="0027b-116">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

## <span data-ttu-id="0027b-117"><a name="metrics"></a>Etapa 1 - Métricas de exibição</span><span class="sxs-lookup"><span data-stu-id="0027b-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="0027b-118">**Métricas** são toounderstand úteis:</span><span class="sxs-lookup"><span data-stu-id="0027b-118">**Metrics** are useful toounderstand:</span></span>
- <span data-ttu-id="0027b-119">Integridade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="0027b-119">Application health</span></span>
- <span data-ttu-id="0027b-120">Desempenho do apliativo</span><span class="sxs-lookup"><span data-stu-id="0027b-120">App performance</span></span>
- <span data-ttu-id="0027b-121">Consumo de recursos</span><span class="sxs-lookup"><span data-stu-id="0027b-121">Resource consumption</span></span>

<span data-ttu-id="0027b-122">Ao investigar um problema de aplicativo, revisar as métricas é um bom lugar toostart.</span><span class="sxs-lookup"><span data-stu-id="0027b-122">When investigating an application issue, reviewing metrics is a good place toostart.</span></span> <span data-ttu-id="0027b-123">Portal do Azure tem uma maneira rápida toovisually inspecionar as métricas de saudação do seu aplicativo usando **Azure Monitor**.</span><span class="sxs-lookup"><span data-stu-id="0027b-123">Azure portal has a quick way toovisually inspect hello metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="0027b-124">Métricas fornecem uma exibição histórica entre várias agregações chave para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0027b-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="0027b-125">Para qualquer aplicativo hospedado no serviço de aplicativo, você deve monitorar Olá Web App e Olá plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0027b-125">For any app hosted in app service, you should monitor both hello Web App and hello App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="0027b-126">Um plano de serviço de aplicativo representa a coleção de saudação de recursos físicos usados toohost seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0027b-126">An App Service plan represents hello collection of physical resources used toohost your apps.</span></span> <span data-ttu-id="0027b-127">Todos os aplicativos tooan do serviço de aplicativo plano compartilhamento Olá recursos atribuídos definida por ela, permitindo que você toosave custo ao hospedar vários aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0027b-127">All applications assigned tooan App Service plan share hello resources defined by it allowing you toosave cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="0027b-128">Os Planos do Serviço de Aplicativo definem:</span><span class="sxs-lookup"><span data-stu-id="0027b-128">App Service plans define:</span></span>
> * <span data-ttu-id="0027b-129">Região: Norte da Europa, Leste dos EUA, Sudeste da Ásia, etc.</span><span class="sxs-lookup"><span data-stu-id="0027b-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="0027b-130">Tamanho da instância: Pequeno, médio, grande, etc.</span><span class="sxs-lookup"><span data-stu-id="0027b-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="0027b-131">Contagem da Escala: uma, duas ou três instâncias, etc.</span><span class="sxs-lookup"><span data-stu-id="0027b-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="0027b-132">SKU: Gratuito, Compartilhado, Básico, Standard, Premium, etc.</span><span class="sxs-lookup"><span data-stu-id="0027b-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="0027b-133">métricas de tooreview para seu aplicativo Web, vá toohello **visão geral** folha do aplicativo hello deseja toomonitor.</span><span class="sxs-lookup"><span data-stu-id="0027b-133">tooreview metrics for your Web App, go toohello **Overview** blade of hello app you want toomonitor.</span></span> <span data-ttu-id="0027b-134">A partir daqui, você pode exibir um gráfico de métricas do seu aplicativo como um **bloco de monitoramento**.</span><span class="sxs-lookup"><span data-stu-id="0027b-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="0027b-135">Clique em Olá bloco tooedit e configurar quais tooview de métricas e Olá toodisplay de intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="0027b-135">Click hello tile tooedit and configure what metrics tooview and hello time range toodisplay.</span></span>

<span data-ttu-id="0027b-136">Por folha de recursos de saudação padrão fornece uma exibição para Olá solicitações de aplicativos e erros de saudação última hora.</span><span class="sxs-lookup"><span data-stu-id="0027b-136">By default hello resource blade provides a view for hello Application Requests and errors for hello last hour.</span></span>
<span data-ttu-id="0027b-137">![Monitorar o aplicativo](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="0027b-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="0027b-138">Como você pode ver no exemplo hello, temos um aplicativo que está gerando muitos **erros de servidor HTTP**.</span><span class="sxs-lookup"><span data-stu-id="0027b-138">As you can see in hello example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="0027b-139">alto volume de saudação de erros é indicação de primeira Olá precisamos tooinvestigate este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0027b-139">hello high volume of errors is hello first indication we need tooinvestigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="0027b-140">Saiba mais sobre o Monitor do Azure com hello links a seguir:</span><span class="sxs-lookup"><span data-stu-id="0027b-140">Learn more about Azure Monitor with hello following links:</span></span>
> - [<span data-ttu-id="0027b-141">Introdução ao Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="0027b-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="0027b-142">Métricas do Azure</span><span class="sxs-lookup"><span data-stu-id="0027b-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="0027b-143">Métricas compatíveis com o Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="0027b-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="0027b-144">Painéis do Azure</span><span class="sxs-lookup"><span data-stu-id="0027b-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="0027b-145"><a name="alerts"></a>Etapa 2 - Configurar Alertas</span><span class="sxs-lookup"><span data-stu-id="0027b-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="0027b-146">**Alertas** pode ser configurado tootrigger em condições específicas para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0027b-146">**Alerts** can be configured tootrigger on specific conditions for your app.</span></span>

<span data-ttu-id="0027b-147">Em [etapa 1 - métricas de exibição](#metrics), vimos que o aplicativo hello tinha um grande número de erros.</span><span class="sxs-lookup"><span data-stu-id="0027b-147">In [Step 1 - View metrics](#metrics), we saw that hello application had a high number of errors.</span></span>

<span data-ttu-id="0027b-148">Permite configurar um alerta tooautomatically ser notificado quando ocorrerem erros.</span><span class="sxs-lookup"><span data-stu-id="0027b-148">Lets configure an alert tooautomatically get notified when errors occur.</span></span> <span data-ttu-id="0027b-149">Nesse caso, estamos deseja toosend alerta hello e enviar por email sempre que o número de saudação de erros HTTP 50 X passa por um certo limite.</span><span class="sxs-lookup"><span data-stu-id="0027b-149">In this case, we want hello alert toosend and e-mail every time hello number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="0027b-150">toocreate um alerta, navegue muito**monitoramento** > **alertas** e clique em **[+] adicionar alerta**.</span><span class="sxs-lookup"><span data-stu-id="0027b-150">toocreate an alert, navigate too**Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Alertas](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="0027b-152">Forneça valores para a configuração de alerta de saudação:</span><span class="sxs-lookup"><span data-stu-id="0027b-152">Provide values for hello Alert configuration:</span></span>
- <span data-ttu-id="0027b-153">**Recurso:** Olá toomonitor de site com o alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="0027b-153">**Resource:** hello site toomonitor with hello alert.</span></span>
- <span data-ttu-id="0027b-154">**Nome:** um nome para o alerta, nesse caso: *HTTP alta 50 X*.</span><span class="sxs-lookup"><span data-stu-id="0027b-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="0027b-155">**Descrição:** explicação de texto sem formatação do que esse alerta está observando.</span><span class="sxs-lookup"><span data-stu-id="0027b-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="0027b-156">**Alerta sobre:** alertas podem examinar eventos ou métricas, para este exemplo Estamos analisando as métricas.</span><span class="sxs-lookup"><span data-stu-id="0027b-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="0027b-157">**Métrica:** que toomonitor métrica, nesse caso: *erros de servidor HTTP*.</span><span class="sxs-lookup"><span data-stu-id="0027b-157">**Metric:** What metric toomonitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="0027b-158">**Condição:** quando tooalert, neste caso, selecione Olá *maior* opção.</span><span class="sxs-lookup"><span data-stu-id="0027b-158">**Condition:** When tooalert, in this case select hello *greater than* option.</span></span>
- <span data-ttu-id="0027b-159">**Limite:** o que é o valor toolook, nesse caso: *400*.</span><span class="sxs-lookup"><span data-stu-id="0027b-159">**Threshold:** What is value toolook for, in this case: *400*.</span></span>
- <span data-ttu-id="0027b-160">**Período:** alertas operam em valor médio de saudação de uma métrica.</span><span class="sxs-lookup"><span data-stu-id="0027b-160">**Period:** Alerts operate over hello average value of a metric.</span></span> <span data-ttu-id="0027b-161">Períodos menores geram alertas mais importantes.</span><span class="sxs-lookup"><span data-stu-id="0027b-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="0027b-162">Neste caso temos *5 minutos*.</span><span class="sxs-lookup"><span data-stu-id="0027b-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="0027b-163">**Os proprietários e colaboradores de e-mail:** nesse caso: *Habilitado*.</span><span class="sxs-lookup"><span data-stu-id="0027b-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="0027b-164">Agora que hello alerta é criado um email é enviado sempre hello aplicativo fica acima do limite de saudação configurada.</span><span class="sxs-lookup"><span data-stu-id="0027b-164">Now that hello alert is created an email is sent every time hello app goes over hello configured threshold.</span></span> <span data-ttu-id="0027b-165">Alertas ativos também podem ser examinados em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0027b-165">Active alerts can also be reviewed in hello Azure portal.</span></span>

![Acionado alertas](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="0027b-167">Saiba mais sobre alertas do Azure com hello links a seguir:</span><span class="sxs-lookup"><span data-stu-id="0027b-167">Learn more about Azure Alerts with hello following links:</span></span>
> - [<span data-ttu-id="0027b-168">O que são alertas no Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="0027b-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="0027b-169">Executar uma Ação com Base nas Métricas</span><span class="sxs-lookup"><span data-stu-id="0027b-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="0027b-170">Criar alertas de métricas</span><span class="sxs-lookup"><span data-stu-id="0027b-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="0027b-171"><a name="companion"></a> Etapa 3 - Complemento do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="0027b-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="0027b-172">**Complemento de serviço de aplicativo** oferece uma maneira conveniente toomonitor seu aplicativo com uma experiência nativo em seu dispositivo móvel (iOS ou Android).</span><span class="sxs-lookup"><span data-stu-id="0027b-172">**App Service companion** offers a convenient way toomonitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="0027b-173">Use o Complemento do Serviço de Aplicativo para:</span><span class="sxs-lookup"><span data-stu-id="0027b-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="0027b-174">Analisar as métricas de aplicativo</span><span class="sxs-lookup"><span data-stu-id="0027b-174">Review application metrics</span></span>
- <span data-ttu-id="0027b-175">Analisar e agir sobre alertas de aplicativos e recomendações</span><span class="sxs-lookup"><span data-stu-id="0027b-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="0027b-176">Executar a solução de problemas básicos (Procurar, iniciar, parar, reiniciar Olá aplicativo)</span><span class="sxs-lookup"><span data-stu-id="0027b-176">Perform basic troubleshooting (browse, start, stop, restart hello app)</span></span>
- <span data-ttu-id="0027b-177">Recebe notificações por push para eventos críticos.</span><span class="sxs-lookup"><span data-stu-id="0027b-177">Get push notifications for critical events.</span></span>

![Complemento do Serviço de Aplicativo](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="0027b-179">[![Loja de Aplicativos do Complemento do Serviço de Aplicativo](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Google Play do Complemento do Serviço de Aplicativo ](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="0027b-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="0027b-180">Você pode instalar o complemento de serviço de aplicativo do hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) ou [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="0027b-180">You can install App Service companion from hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="0027b-181"><a name="diagnose"></a> Etapa 4 - Diagnosticar e resolver problemas</span><span class="sxs-lookup"><span data-stu-id="0027b-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="0027b-182">**Diagnosticar e resolver problemas** ajuda a separar questões de aplicativo forma a problemas de plataforma.</span><span class="sxs-lookup"><span data-stu-id="0027b-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="0027b-183">Ele também pode sugerir possíveis atenuações tooget toohealthy de fundo seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0027b-183">It can also suggest possible mitigations tooget your Web App back toohealthy.</span></span>

![Diagnosticar e Resolver Problemas](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="0027b-185">Continuar com as etapas anteriores de formulário de exemplo de hello, podemos ver que aplicativo hello tem sido com disponibilidade problemas.</span><span class="sxs-lookup"><span data-stu-id="0027b-185">Continuing with hello example form previous steps, we can see that hello application has been having availably issues.</span></span> <span data-ttu-id="0027b-186">Por outro lado, a disponibilidade da plataforma de saudação não foi movida de 100%.</span><span class="sxs-lookup"><span data-stu-id="0027b-186">In contrast, hello platform availability has not moved from 100%.</span></span>

<span data-ttu-id="0027b-187">Quando o aplicativo hello está tendo o problema e hello plataforma permaneça em funcionamento, ele é uma indicação clara que estamos lidando com um problema de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0027b-187">When hello app is having issue and hello platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="0027b-188"><a name="logging"></a> Etapa 5 - Registrar em Log</span><span class="sxs-lookup"><span data-stu-id="0027b-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="0027b-189">Agora que já têm restringimos problema de aplicativo hello falhas tooan, podemos ver tooget de logs de aplicativo e servidor de saudação obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="0027b-189">Now that we have narrowed down hello failures tooan application issue, we can look at hello application and server logs tooget more information.</span></span>

<span data-ttu-id="0027b-190">O registro permite que ambos os toocollect **Application Diagnostics** e **diagnósticos do servidor Web** logs para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0027b-190">Logging allows you toocollect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="0027b-191">Diagnóstico de Aplicativos</span><span class="sxs-lookup"><span data-stu-id="0027b-191">Application Diagnostics</span></span>
<span data-ttu-id="0027b-192">O diagnóstico de aplicativo permite que você toocapture rastreamentos produzidos pelo aplicativo hello em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="0027b-192">Application diagnostics allows you toocapture traces produced by hello application at runtime.</span></span>

<span data-ttu-id="0027b-193">Adicionando rastreamento tooyour aplicativo melhora significativamente sua capacidade toodebug e problemas de ponto de pin.</span><span class="sxs-lookup"><span data-stu-id="0027b-193">Adding tracing tooyour application greatly improves your ability toodebug and pin-point issues.</span></span>

<span data-ttu-id="0027b-194">No ASP.NET, você pode registrar rastreamentos de aplicativo usando [classe Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate eventos que são capturados pela infraestrutura de log hello.</span><span class="sxs-lookup"><span data-stu-id="0027b-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate events that are captured by hello log infrastructure.</span></span> <span data-ttu-id="0027b-195">Você também pode especificar a severidade de saudação do rastreamento Olá para filtragem mais fácil.</span><span class="sxs-lookup"><span data-stu-id="0027b-195">You can also specify hello severity of hello trace for easier filtering.</span></span>

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
<span data-ttu-id="0027b-196">log de aplicativo tooenable ir muito**monitoramento** > **Logs de diagnóstico** e habilitar o log de aplicativo usando as alternâncias de saudação.</span><span class="sxs-lookup"><span data-stu-id="0027b-196">tooenable Application logging Go too**Monitoring** > **Diagnostic Logs** and Enable Application Logging using hello toggles.</span></span>

![Monitorar o aplicativo](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="0027b-198">Logs de aplicativo podem ser um sistema de arquivos do aplicativo da Web armazenado tooyour ou enviados por push tooblob armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0027b-198">Application logs can be stored tooyour Web App's file system or pushed out tooblob storage.</span></span> <span data-ttu-id="0027b-199">Para cenários de produção, é recomendado toouse armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="0027b-199">For production scenarios, it's recommended toouse blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0027b-200">Habilitar o registro no log tem um impacto sobre o desempenho do aplicativo e a utilização de recursos.</span><span class="sxs-lookup"><span data-stu-id="0027b-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="0027b-201">Para cenários de produção, logs de erros são recomendados.</span><span class="sxs-lookup"><span data-stu-id="0027b-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="0027b-202">Somente habilite o registro no log mais detalhado quando investigar problemas.</span><span class="sxs-lookup"><span data-stu-id="0027b-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="0027b-203">Diagnóstico de Servidor Web</span><span class="sxs-lookup"><span data-stu-id="0027b-203">Web Server Diagnostics</span></span>
<span data-ttu-id="0027b-204">Logs do servidor Web são gerados, mesmo que seu aplicativo não é instrumentado.</span><span class="sxs-lookup"><span data-stu-id="0027b-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="0027b-205">O Serviço de Aplicativo pode coletar três tipos diferentes de logs do servidor:</span><span class="sxs-lookup"><span data-stu-id="0027b-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="0027b-206">**Log do Servidor Web**</span><span class="sxs-lookup"><span data-stu-id="0027b-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="0027b-207">Informações sobre transações HTTP usando Olá [formato de arquivo de log estendido W3C](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="0027b-207">Information about HTTP transactions using hello [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="0027b-208">Útil ao determinar a métrica geral do site, como número de saudação de solicitações manipuladas ou quantas solicitações são de um endereço IP específico.</span><span class="sxs-lookup"><span data-stu-id="0027b-208">Useful when determining overall site metrics such as hello number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="0027b-209">**Logs de Erros Detalhados**</span><span class="sxs-lookup"><span data-stu-id="0027b-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="0027b-210">Informações detalhadas de erros para códigos de status HTTP que indiquem uma falha (código de status 400 ou superior).</span><span class="sxs-lookup"><span data-stu-id="0027b-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="0027b-211">Saiba mais sobre o log de erro detalhado</span><span class="sxs-lookup"><span data-stu-id="0027b-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="0027b-212">**Rastreamento de Solicitações com Falha**</span><span class="sxs-lookup"><span data-stu-id="0027b-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="0027b-213">Informações detalhadas sobre solicitações com falha, incluindo um rastreamento de componentes do IIS Olá usado tooprocess Olá Olá e solicitação de tempo em cada componente.</span><span class="sxs-lookup"><span data-stu-id="0027b-213">Detailed information on failed requests, including a trace of hello IIS components used tooprocess hello request and hello time taken in each component.</span></span>
    - <span data-ttu-id="0027b-214">Logs de solicitação com falha são úteis quando você tentar tooisolate o que está causando um erro HTTP específico.</span><span class="sxs-lookup"><span data-stu-id="0027b-214">Failed request logs are useful when trying tooisolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="0027b-215">Saiba mais sobre falha de solicitação de rastreamento</span><span class="sxs-lookup"><span data-stu-id="0027b-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="0027b-216">log do servidor tooenable:</span><span class="sxs-lookup"><span data-stu-id="0027b-216">tooenable Server logging:</span></span>
- <span data-ttu-id="0027b-217">Vá muito**monitoramento** > **Logs de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="0027b-217">go too**Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="0027b-218">Habilite tipos diferentes de saudação do diagnóstico de servidor da Web usando alternâncias de saudação.</span><span class="sxs-lookup"><span data-stu-id="0027b-218">Enable hello different types of Web Server Diagnostics using hello toggles.</span></span>

![Monitorar o aplicativo](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="0027b-220">Habilitar o registro no log tem um impacto sobre o desempenho do aplicativo e a utilização de recursos.</span><span class="sxs-lookup"><span data-stu-id="0027b-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="0027b-221">Para Cenários de Produção, os Logs de Erros são recomendados, Somente habilite o registro no log mais detalhado quando investigar problemas.</span><span class="sxs-lookup"><span data-stu-id="0027b-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="0027b-222">Acessar Logs</span><span class="sxs-lookup"><span data-stu-id="0027b-222">Accessing Logs</span></span>
<span data-ttu-id="0027b-223">Os logs armazenados no armazenamento de blobs são acessados usando o Gerenciador de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0027b-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="0027b-224">Logs armazenados no sistema de arquivos do aplicativo da Web hello são acessados por meio de FTP em Olá caminhos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0027b-224">Logs stored in hello Web App's filesystem are accessed through FTP under hello following paths:</span></span>

- <span data-ttu-id="0027b-225">**Logs de aplicativos** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="0027b-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="0027b-226">Essa pasta contém um ou mais arquivos de texto que contêm informações produzidas pelo log do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0027b-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="0027b-227">**Falha de solicitação de rastreamento** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="0027b-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="0027b-228">Esta pasta contém um arquivo XSL e um ou mais arquivos XML.</span><span class="sxs-lookup"><span data-stu-id="0027b-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="0027b-229">**Logs de erro detalhadas** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="0027b-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="0027b-230">Esta pasta contém um ou mais arquivos .htm com informações abrangentes sobre erros HTTP gerados pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0027b-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="0027b-231">**Logs do Web Server** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="0027b-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="0027b-232">Esta pasta contém um ou mais arquivos de texto formatados usando o formato de arquivo de log estendido W3C de saudação.</span><span class="sxs-lookup"><span data-stu-id="0027b-232">This folder contains one or more text files formatted using hello W3C extended log file format.</span></span>

## <span data-ttu-id="0027b-233"><a name="streaming"></a> Etapa 6 - Streaming de Log</span><span class="sxs-lookup"><span data-stu-id="0027b-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="0027b-234">Os logs de streaming são convenientes ao depurar um aplicativo desde que ele economiza tempo em comparação comparado muito[acessar logs de saudação](#Accessing-Logs) por meio de FTP.</span><span class="sxs-lookup"><span data-stu-id="0027b-234">Streaming logs are convenient when debugging an application since it saves time compared too[accessing hello logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="0027b-235">O Serviço de Aplicativo pode fazer streaming de **Logs do Aplicativo** e **Logs do Servidor Web** conforme eles são gerados.</span><span class="sxs-lookup"><span data-stu-id="0027b-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="0027b-236">Antes de tentar toostream logs, verifique se você habilitou coletar logs conforme descrito em Olá [log](#logging) seção.</span><span class="sxs-lookup"><span data-stu-id="0027b-236">Before trying toostream logs, make sure you have enabled collecting logs as described in hello [Logging](#logging) section.</span></span>

<span data-ttu-id="0027b-237">logs de toostream ir muito**monitoramento**> **fluxo de Log**.</span><span class="sxs-lookup"><span data-stu-id="0027b-237">toostream logs, go too**Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="0027b-238">Selecione **Logs do Aplicativo** ou **Logs do Servidor Web**, dependendo de quais informações você está procurando.</span><span class="sxs-lookup"><span data-stu-id="0027b-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="0027b-239">A partir daqui, também pausar, reiniciar e limpar o buffer de saudação.</span><span class="sxs-lookup"><span data-stu-id="0027b-239">From here, you can also pause, restart, and clear hello buffer.</span></span>

![Logs de streaming](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="0027b-241">Logs são gerados somente quando há tráfego no aplicativo hello, você também pode aumentar o nível de detalhes de saudação do tooget de logs mais informações ou eventos.</span><span class="sxs-lookup"><span data-stu-id="0027b-241">Logs are only generated when there is traffic on hello app, you can also increase hello verbosity of logs tooget more events or information.</span></span>

## <span data-ttu-id="0027b-242"><a name="remote"></a> Etapa 7 - Depuração Remota</span><span class="sxs-lookup"><span data-stu-id="0027b-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="0027b-243">Quando você tiver origem Olá apontada pin de problemas de aplicativos hello, usar **depuração remota** toowalk através do código de saudação.</span><span class="sxs-lookup"><span data-stu-id="0027b-243">Once you have pin-pointed hello source of hello applications problems, use **Remote Debugging** toowalk through hello code.</span></span>

<span data-ttu-id="0027b-244">Remota de depuração permite que você anexar um depurador tooyour aplicativo Web em execução na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="0027b-244">Remote debugging lets you attach a debugger tooyour Web App running in hello cloud.</span></span> <span data-ttu-id="0027b-245">Você pode definir pontos de interrupção, manipular memória diretamente, percorrer o código e até mesmo alterar o caminho de código Olá exatamente como faria para um aplicativo em execução localmente.</span><span class="sxs-lookup"><span data-stu-id="0027b-245">You can set breakpoints, manipulate memory directly, step through code, and even change hello code path just like you do for an app running locally.</span></span>

<span data-ttu-id="0027b-246">tooattach Olá depurador tooyour o aplicativo em execução na nuvem hello:</span><span class="sxs-lookup"><span data-stu-id="0027b-246">tooattach hello debugger tooyour app running in hello cloud:</span></span>

- <span data-ttu-id="0027b-247">Usando o Visual Studio de 2017, solução de saudação aberta para o aplicativo hello deseja toodebug</span><span class="sxs-lookup"><span data-stu-id="0027b-247">Using Visual Studio 2017, open hello solution for hello app you want toodebug</span></span>
- <span data-ttu-id="0027b-248">Defina alguns pontos de interrupção, exatamente como faria para desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="0027b-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="0027b-249">Abra o **cloud explorer** (ctr + /, ctrl + x).</span><span class="sxs-lookup"><span data-stu-id="0027b-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="0027b-250">Faça logon com suas credenciais do Azure, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="0027b-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="0027b-251">Localizar Olá aplicativo deseja toodebug</span><span class="sxs-lookup"><span data-stu-id="0027b-251">Find hello app you want toodebug</span></span>
- <span data-ttu-id="0027b-252">Selecione **Anexar depurador** Olá formulário **ações** painel.</span><span class="sxs-lookup"><span data-stu-id="0027b-252">Select **Attach Debugger** form hello **Actions** pane.</span></span>

![Depuração Remota](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="0027b-254">Visual Studio configura seu aplicativo para depuração remota e abre uma janela de navegador que navega tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0027b-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates tooyour app.</span></span> <span data-ttu-id="0027b-255">Navegue pelos seus pontos de interrupção do aplicativo tootrigger e percorrer o código de saudação.</span><span class="sxs-lookup"><span data-stu-id="0027b-255">Browse through your app tootrigger break points and step through hello code.</span></span>

> [!WARNING]
> <span data-ttu-id="0027b-256">A execução em modo de depuração em produção não é recomendada.</span><span class="sxs-lookup"><span data-stu-id="0027b-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="0027b-257">Se seu aplicativo de produção não é expandido toomultiple instâncias de servidor, depuração impedir o servidor web de saudação de solicitações de tooother está respondendo.</span><span class="sxs-lookup"><span data-stu-id="0027b-257">If your production app is not scaled out toomultiple server instances, debugging prevent hello web server from responding tooother requests.</span></span> <span data-ttu-id="0027b-258">Para solucionar problemas de produção, o melhor recurso é muito[configurar o log](#logging) e [Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="0027b-258">For troubleshooting production problems, your best resource is too[configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="0027b-259"><a name="explorer"></a> Etapa 8 - Gerenciador de Processos</span><span class="sxs-lookup"><span data-stu-id="0027b-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="0027b-260">Quando seu aplicativo é expandido toomore de uma instância, **Explorador de processos** pode ajudar a identificar problemas específicos da instância.</span><span class="sxs-lookup"><span data-stu-id="0027b-260">When your application is scaled out toomore than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="0027b-261">Use **Gerenciador de Processos** para:</span><span class="sxs-lookup"><span data-stu-id="0027b-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="0027b-262">Enumere todos os processos de saudação instâncias diferentes do seu plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0027b-262">Enumerate all hello processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="0027b-263">Fazer drill down e exiba Olá identificadores e módulos associados a cada processo.</span><span class="sxs-lookup"><span data-stu-id="0027b-263">Drill down and view hello handles and modules associated with each process.</span></span>
- <span data-ttu-id="0027b-264">Contagem de CPU do modo de exibição, o conjunto de trabalho e o Thread em Olá processar nível toohelp identificar processos sem controle</span><span class="sxs-lookup"><span data-stu-id="0027b-264">View CPU, Working Set, and Thread count at hello process level toohelp you identify runaway processes</span></span>
- <span data-ttu-id="0027b-265">Localize identificadores de arquivos abertos e, até mesmo, encerre uma instância de processo específico.</span><span class="sxs-lookup"><span data-stu-id="0027b-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="0027b-266">O Gerenciador de Processos pode estar em **Monitoramento** > **Explorador de Processos**.</span><span class="sxs-lookup"><span data-stu-id="0027b-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Gerenciador de Processos](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="0027b-268"><a name="insights"></a> Etapa 9 - Application Insights</span><span class="sxs-lookup"><span data-stu-id="0027b-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="0027b-269">O **Application Insights** fornece perfil de aplicativo e recursos avançados de monitoramento para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0027b-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="0027b-270">Use o Application Insights toodetect e diagnosticar exceções e problemas de desempenho em seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0027b-270">Use Application Insights toodetect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="0027b-271">É possível habilitar o Application Insights para seu aplicativo Web em **Monitoramento** > **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="0027b-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="0027b-272">Application Insights pode solicitar tooinstall Olá Application Insights site extensão toostart coleta de dados.</span><span class="sxs-lookup"><span data-stu-id="0027b-272">Application Insights might prompt you tooinstall hello Application Insights site extension toostart collecting data.</span></span> <span data-ttu-id="0027b-273">Instalação da extensão do site Olá faz com que uma reinicialização do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0027b-273">Installing hello site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="0027b-275">Application Insights tem um recurso avançado definido, toolearn mais, siga os links de saudação incluídos no hello [próximas etapas](#next) seção.</span><span class="sxs-lookup"><span data-stu-id="0027b-275">Application Insights has a rich feature set, toolearn more, follow hello links included in hello [Next Steps](#next) section.</span></span>

## <span data-ttu-id="0027b-276"><a name="next"></a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0027b-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="0027b-277">O que é o Application Insights</span><span class="sxs-lookup"><span data-stu-id="0027b-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="0027b-278">Monitorar o desempenho do aplicativo Web do Azure com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="0027b-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="0027b-279">Monitorar a disponibilidade e capacidade de resposta de qualquer site da Web com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="0027b-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
