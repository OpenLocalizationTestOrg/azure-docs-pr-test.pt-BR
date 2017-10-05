---
title: Monitorar um aplicativo Web | Microsoft Docs
description: Saiba como configurar o Monitoramento em seu aplicativo Web
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: 29df824062d00e01b786533033097948c008588f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="71236-103">Monitorar o Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="71236-103">Monitor App Service</span></span>
<span data-ttu-id="71236-104">Este tutorial orienta você por meio de monitoramento do aplicativo e usar as ferramentas de plataforma interno para resolver problemas quando eles ocorrerem.</span><span class="sxs-lookup"><span data-stu-id="71236-104">This tutorial walks you through monitoring your app and using the built-in platform tools to solve problems when they occur.</span></span>

<span data-ttu-id="71236-105">Cada seção deste documento será um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="71236-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="71236-106">Usando os recursos juntos permitem que você:</span><span class="sxs-lookup"><span data-stu-id="71236-106">Using the features together let you:</span></span>
- <span data-ttu-id="71236-107">Identificar um problema em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71236-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="71236-108">Determinando quando o problema é causado por seu código ou a plataforma.</span><span class="sxs-lookup"><span data-stu-id="71236-108">Determining when the issue is caused by your code or the platform.</span></span>
- <span data-ttu-id="71236-109">Restrinja a origem do problema em seu código.</span><span class="sxs-lookup"><span data-stu-id="71236-109">Narrow down the source of the problem in your code.</span></span>
- <span data-ttu-id="71236-110">Depure e corrija o problema.</span><span class="sxs-lookup"><span data-stu-id="71236-110">Debugging and fixing the issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="71236-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="71236-111">Before you begin</span></span>
- <span data-ttu-id="71236-112">Você precisa de um aplicativo Web para monitorar e seguir as etapas destacadas.</span><span class="sxs-lookup"><span data-stu-id="71236-112">You need a Web App to monitor and follow the outlined steps.</span></span>
    - <span data-ttu-id="71236-113">É possível criar um aplicativo seguindo as etapas descritas no tutorial [Criar um aplicativo ASP.NET no Azure com Banco de dados SQL](app-service-web-tutorial-dotnet-sqldatabase.md).</span><span class="sxs-lookup"><span data-stu-id="71236-113">You can create an application following the steps described in the [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="71236-114">Caso queira testar a **Depuração Remota** do seu aplicativo, você precisará do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71236-114">If you want to try out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="71236-115">Se ainda não tiver o Visual Studio 2017 instalado, é possível baixar e usar o [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/) gratuito.</span><span class="sxs-lookup"><span data-stu-id="71236-115">If you don’t already have Visual Studio 2017 installed, you can download and use the free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="71236-116">Verifique se você habilitou o **desenvolvimento do Azure** durante a instalação do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71236-116">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

## <span data-ttu-id="71236-117"><a name="metrics"></a>Etapa 1 - Métricas de exibição</span><span class="sxs-lookup"><span data-stu-id="71236-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="71236-118">**Métricas** são úteis para entender:</span><span class="sxs-lookup"><span data-stu-id="71236-118">**Metrics** are useful to understand:</span></span>
- <span data-ttu-id="71236-119">Integridade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="71236-119">Application health</span></span>
- <span data-ttu-id="71236-120">Desempenho do apliativo</span><span class="sxs-lookup"><span data-stu-id="71236-120">App performance</span></span>
- <span data-ttu-id="71236-121">Consumo de recursos</span><span class="sxs-lookup"><span data-stu-id="71236-121">Resource consumption</span></span>

<span data-ttu-id="71236-122">Ao investigar um problema de aplicativo, revisar as métricas é um bom lugar para começar.</span><span class="sxs-lookup"><span data-stu-id="71236-122">When investigating an application issue, reviewing metrics is a good place to start.</span></span> <span data-ttu-id="71236-123">O portal do Azure tem uma maneira rápida para inspecionar visualmente as métricas de seu aplicativo, usando o **Azure Monitor**.</span><span class="sxs-lookup"><span data-stu-id="71236-123">Azure portal has a quick way to visually inspect the metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="71236-124">Métricas fornecem uma exibição histórica entre várias agregações chave para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71236-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="71236-125">Para qualquer aplicativo hospedado no serviço de aplicativo, será necessário monitorar o aplicativo Web e o plano de Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71236-125">For any app hosted in app service, you should monitor both the Web App and the App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="71236-126">Um plano do Serviço de Aplicativo representa a coleção de recursos físicos usados para hospedar seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="71236-126">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="71236-127">Todos os aplicativos atribuídos a um plano do Serviço de Aplicativo compartilham os recursos definidos por ele, permitindo que você economize ao hospedar vários aplicativos.</span><span class="sxs-lookup"><span data-stu-id="71236-127">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="71236-128">Os Planos do Serviço de Aplicativo definem:</span><span class="sxs-lookup"><span data-stu-id="71236-128">App Service plans define:</span></span>
> * <span data-ttu-id="71236-129">Região: Norte da Europa, Leste dos EUA, Sudeste da Ásia, etc.</span><span class="sxs-lookup"><span data-stu-id="71236-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="71236-130">Tamanho da instância: Pequeno, médio, grande, etc.</span><span class="sxs-lookup"><span data-stu-id="71236-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="71236-131">Contagem da Escala: uma, duas ou três instâncias, etc.</span><span class="sxs-lookup"><span data-stu-id="71236-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="71236-132">SKU: Gratuito, Compartilhado, Básico, Standard, Premium, etc.</span><span class="sxs-lookup"><span data-stu-id="71236-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="71236-133">Para revisar as métricas para seu aplicativo Web, vá para a folha **Visão geral** do aplicativo que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="71236-133">To review metrics for your Web App, go to the **Overview** blade of the app you want to monitor.</span></span> <span data-ttu-id="71236-134">A partir daqui, você pode exibir um gráfico de métricas do seu aplicativo como um **bloco de monitoramento**.</span><span class="sxs-lookup"><span data-stu-id="71236-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="71236-135">Clique no bloco para editar e configurar as métricas e o intervalo de tempo a serem exibidos.</span><span class="sxs-lookup"><span data-stu-id="71236-135">Click the tile to edit and configure what metrics to view and the time range to display.</span></span>

<span data-ttu-id="71236-136">Por padrão a folha de recursos fornece uma exibição para as solicitações do aplicativo e os erros de última hora.</span><span class="sxs-lookup"><span data-stu-id="71236-136">By default the resource blade provides a view for the Application Requests and errors for the last hour.</span></span>
<span data-ttu-id="71236-137">![Monitorar o aplicativo](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="71236-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="71236-138">Como você pode ver no exemplo, temos um aplicativo que está gerando muitos **erros do servidor HTTP**.</span><span class="sxs-lookup"><span data-stu-id="71236-138">As you can see in the example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="71236-139">Alto volume de erros é a indicação primeiro precisamos investigar esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71236-139">The high volume of errors is the first indication we need to investigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="71236-140">Saiba mais sobre o Azure Monitor com os seguintes links:</span><span class="sxs-lookup"><span data-stu-id="71236-140">Learn more about Azure Monitor with the following links:</span></span>
> - [<span data-ttu-id="71236-141">Introdução ao Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="71236-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="71236-142">Métricas do Azure</span><span class="sxs-lookup"><span data-stu-id="71236-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="71236-143">Métricas compatíveis com o Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="71236-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="71236-144">Painéis do Azure</span><span class="sxs-lookup"><span data-stu-id="71236-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="71236-145"><a name="alerts"></a>Etapa 2 - Configurar Alertas</span><span class="sxs-lookup"><span data-stu-id="71236-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="71236-146">**Alertas** podem ser configurados para serem acionados com condições específicas para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71236-146">**Alerts** can be configured to trigger on specific conditions for your app.</span></span>

<span data-ttu-id="71236-147">Em [etapa 1 - visualizar métricas](#metrics), vimos que o aplicativo tinha um grande número de erros.</span><span class="sxs-lookup"><span data-stu-id="71236-147">In [Step 1 - View metrics](#metrics), we saw that the application had a high number of errors.</span></span>

<span data-ttu-id="71236-148">Permite configurar um alerta para ser notificado automaticamente quando ocorrem erros.</span><span class="sxs-lookup"><span data-stu-id="71236-148">Lets configure an alert to automatically get notified when errors occur.</span></span> <span data-ttu-id="71236-149">Nesse caso, queremos que o alerta para enviar e email sempre que o número de erros HTTP 50 X fica acima de um determinado limite.</span><span class="sxs-lookup"><span data-stu-id="71236-149">In this case, we want the alert to send and e-mail every time the number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="71236-150">Para criar um alerta, navegue até **monitoramento** > **alertas** e clique em **[+] Adicionar alerta**.</span><span class="sxs-lookup"><span data-stu-id="71236-150">To create an alert, navigate to **Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Alertas](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="71236-152">Forneça valores para a configuração de alertas:</span><span class="sxs-lookup"><span data-stu-id="71236-152">Provide values for the Alert configuration:</span></span>
- <span data-ttu-id="71236-153">**Recurso:** o site para monitorar com o alerta.</span><span class="sxs-lookup"><span data-stu-id="71236-153">**Resource:** The site to monitor with the alert.</span></span>
- <span data-ttu-id="71236-154">**Nome:** um nome para o alerta, nesse caso: *HTTP alta 50 X*.</span><span class="sxs-lookup"><span data-stu-id="71236-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="71236-155">**Descrição:** explicação de texto sem formatação do que esse alerta está observando.</span><span class="sxs-lookup"><span data-stu-id="71236-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="71236-156">**Alerta sobre:** alertas podem examinar eventos ou métricas, para este exemplo Estamos analisando as métricas.</span><span class="sxs-lookup"><span data-stu-id="71236-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="71236-157">**Métrica:** que métrica para monitorar, nesse caso: *erros do servidor HTTP*.</span><span class="sxs-lookup"><span data-stu-id="71236-157">**Metric:** What metric to monitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="71236-158">**Condição:** quando um alerta, selecione nesse caso o *maior* opção.</span><span class="sxs-lookup"><span data-stu-id="71236-158">**Condition:** When to alert, in this case select the *greater than* option.</span></span>
- <span data-ttu-id="71236-159">**Limite:** o que é o valor a ser procurado, nesse caso: *400*.</span><span class="sxs-lookup"><span data-stu-id="71236-159">**Threshold:** What is value to look for, in this case: *400*.</span></span>
- <span data-ttu-id="71236-160">**Período:** alertas operam sobre o valor médio de uma métrica.</span><span class="sxs-lookup"><span data-stu-id="71236-160">**Period:** Alerts operate over the average value of a metric.</span></span> <span data-ttu-id="71236-161">Períodos menores geram alertas mais importantes.</span><span class="sxs-lookup"><span data-stu-id="71236-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="71236-162">Neste caso temos *5 minutos*.</span><span class="sxs-lookup"><span data-stu-id="71236-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="71236-163">**Os proprietários e colaboradores de e-mail:** nesse caso: *Habilitado*.</span><span class="sxs-lookup"><span data-stu-id="71236-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="71236-164">Agora que o alerta foi criado um email é enviado sempre que o aplicativo fica acima do limite configurado.</span><span class="sxs-lookup"><span data-stu-id="71236-164">Now that the alert is created an email is sent every time the app goes over the configured threshold.</span></span> <span data-ttu-id="71236-165">Alertas ativos também podem ser analisados no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="71236-165">Active alerts can also be reviewed in the Azure portal.</span></span>

![Acionado alertas](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="71236-167">Saiba mais sobre Alertas do Azure com os seguintes links:</span><span class="sxs-lookup"><span data-stu-id="71236-167">Learn more about Azure Alerts with the following links:</span></span>
> - [<span data-ttu-id="71236-168">O que são alertas no Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="71236-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="71236-169">Executar uma Ação com Base nas Métricas</span><span class="sxs-lookup"><span data-stu-id="71236-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="71236-170">Criar alertas de métricas</span><span class="sxs-lookup"><span data-stu-id="71236-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="71236-171"><a name="companion"></a> Etapa 3 - Complemento do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="71236-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="71236-172">O **Complemento do Serviço de Aplicativo** oferece uma maneira conveniente para monitorar o aplicativo com uma experiência nativa no dispositivo móvel (iOS ou Android).</span><span class="sxs-lookup"><span data-stu-id="71236-172">**App Service companion** offers a convenient way to monitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="71236-173">Use o Complemento do Serviço de Aplicativo para:</span><span class="sxs-lookup"><span data-stu-id="71236-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="71236-174">Analisar as métricas de aplicativo</span><span class="sxs-lookup"><span data-stu-id="71236-174">Review application metrics</span></span>
- <span data-ttu-id="71236-175">Analisar e agir sobre alertas de aplicativos e recomendações</span><span class="sxs-lookup"><span data-stu-id="71236-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="71236-176">Executar a solução de problemas básicos (procurar, iniciar, parar, reiniciar o aplicativo)</span><span class="sxs-lookup"><span data-stu-id="71236-176">Perform basic troubleshooting (browse, start, stop, restart the app)</span></span>
- <span data-ttu-id="71236-177">Recebe notificações por push para eventos críticos.</span><span class="sxs-lookup"><span data-stu-id="71236-177">Get push notifications for critical events.</span></span>

![Complemento do Serviço de Aplicativo](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="71236-179">[![Loja de Aplicativos do Complemento do Serviço de Aplicativo](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Google Play do Complemento do Serviço de Aplicativo ](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="71236-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="71236-180">É possível instalar o complemento do Serviço de Aplicativo pela [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) ou pelo [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="71236-180">You can install App Service companion from the [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="71236-181"><a name="diagnose"></a> Etapa 4 - Diagnosticar e resolver problemas</span><span class="sxs-lookup"><span data-stu-id="71236-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="71236-182">**Diagnosticar e resolver problemas** ajuda a separar questões de aplicativo forma a problemas de plataforma.</span><span class="sxs-lookup"><span data-stu-id="71236-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="71236-183">Ele também pode sugerir possíveis atenuações para deixar seu aplicativo Web para íntegro.</span><span class="sxs-lookup"><span data-stu-id="71236-183">It can also suggest possible mitigations to get your Web App back to healthy.</span></span>

![Diagnosticar e Resolver Problemas](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="71236-185">Continuar com as etapas anteriores do formulário de exemplo, podemos ver que o aplicativo tenha sido com disponível problemas.</span><span class="sxs-lookup"><span data-stu-id="71236-185">Continuing with the example form previous steps, we can see that the application has been having availably issues.</span></span> <span data-ttu-id="71236-186">Por outro lado, a disponibilidade de plataforma não foi movida de 100%.</span><span class="sxs-lookup"><span data-stu-id="71236-186">In contrast, the platform availability has not moved from 100%.</span></span>

<span data-ttu-id="71236-187">Quando o aplicativo está tendo problemas e a plataforma permaneça em funcionamento, é uma indicação clara de que estamos lidando com um problema de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71236-187">When the app is having issue and the platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="71236-188"><a name="logging"></a> Etapa 5 - Registrar em Log</span><span class="sxs-lookup"><span data-stu-id="71236-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="71236-189">Agora que podemos ter limitados as falhas para um problema de aplicativo, podemos ver os logs de aplicativo e servidor para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="71236-189">Now that we have narrowed down the failures to an application issue, we can look at the application and server logs to get more information.</span></span>

<span data-ttu-id="71236-190">O registro em log permite coletar ambos os logs do **Diagnóstico de Aplicativos** e do **Diagnóstico de Servidor Web** para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="71236-190">Logging allows you to collect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="71236-191">Diagnóstico de Aplicativos</span><span class="sxs-lookup"><span data-stu-id="71236-191">Application Diagnostics</span></span>
<span data-ttu-id="71236-192">O diagnóstico de aplicativo permite capturar rastreamentos produzidos pelo aplicativo em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="71236-192">Application diagnostics allows you to capture traces produced by the application at runtime.</span></span>

<span data-ttu-id="71236-193">Adicionar rastreamento para seu aplicativo muito melhora a capacidade de depurar e problemas de Pinpoint.</span><span class="sxs-lookup"><span data-stu-id="71236-193">Adding tracing to your application greatly improves your ability to debug and pin-point issues.</span></span>

<span data-ttu-id="71236-194">No ASP.NET, é possível registrar rastreamentos de aplicativo usando [System.Diagnostics.Trace clase](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) para gerar eventos que são capturados pela infraestrutura de log.</span><span class="sxs-lookup"><span data-stu-id="71236-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) to generate events that are captured by the log infrastructure.</span></span> <span data-ttu-id="71236-195">Você também pode especificar a severidade do rastreamento para filtragem mais fácil.</span><span class="sxs-lookup"><span data-stu-id="71236-195">You can also specify the severity of the trace for easier filtering.</span></span>

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
<span data-ttu-id="71236-196">Para habilitar o log de aplicativo, vá para **monitoramento** > **Logs de diagnóstico** e habilitar o log de aplicativo usando a alterna.</span><span class="sxs-lookup"><span data-stu-id="71236-196">To enable Application logging Go to **Monitoring** > **Diagnostic Logs** and Enable Application Logging using the toggles.</span></span>

![Monitorar o aplicativo](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="71236-198">Os Logs de Aplicativo podem ser armazenados em um sistema de arquivos do Aplicativo Web ou enviados para armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="71236-198">Application logs can be stored to your Web App's file system or pushed out to blob storage.</span></span> <span data-ttu-id="71236-199">Para cenários de produção, é recomendável usar o armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="71236-199">For production scenarios, it's recommended to use blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71236-200">Habilitar o registro no log tem um impacto sobre o desempenho do aplicativo e a utilização de recursos.</span><span class="sxs-lookup"><span data-stu-id="71236-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="71236-201">Para cenários de produção, logs de erros são recomendados.</span><span class="sxs-lookup"><span data-stu-id="71236-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="71236-202">Somente habilite o registro no log mais detalhado quando investigar problemas.</span><span class="sxs-lookup"><span data-stu-id="71236-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="71236-203">Diagnóstico de Servidor Web</span><span class="sxs-lookup"><span data-stu-id="71236-203">Web Server Diagnostics</span></span>
<span data-ttu-id="71236-204">Logs do servidor Web são gerados, mesmo que seu aplicativo não é instrumentado.</span><span class="sxs-lookup"><span data-stu-id="71236-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="71236-205">O Serviço de Aplicativo pode coletar três tipos diferentes de logs do servidor:</span><span class="sxs-lookup"><span data-stu-id="71236-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="71236-206">**Log do Servidor Web**</span><span class="sxs-lookup"><span data-stu-id="71236-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="71236-207">Informações sobre transações HTTP usando o [formato do arquivo de log estendido do W3C](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="71236-207">Information about HTTP transactions using the [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="71236-208">Útil ao determinar métricas globais do site como o número de solicitações processadas ou a quantidade de solicitações de um endereço IP específico.</span><span class="sxs-lookup"><span data-stu-id="71236-208">Useful when determining overall site metrics such as the number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="71236-209">**Logs de Erros Detalhados**</span><span class="sxs-lookup"><span data-stu-id="71236-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="71236-210">Informações detalhadas de erros para códigos de status HTTP que indiquem uma falha (código de status 400 ou superior).</span><span class="sxs-lookup"><span data-stu-id="71236-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="71236-211">Saiba mais sobre o log de erro detalhado</span><span class="sxs-lookup"><span data-stu-id="71236-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="71236-212">**Rastreamento de Solicitações com Falha**</span><span class="sxs-lookup"><span data-stu-id="71236-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="71236-213">Informações detalhadas sobre solicitações com falha, incluindo um rastreamento dos componentes IIS usados para processar a solicitação e o tempo levado em cada componente.</span><span class="sxs-lookup"><span data-stu-id="71236-213">Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span></span>
    - <span data-ttu-id="71236-214">O logs de solicitações com falha são úteis ao tentar isolar a causa de um erro HTTP específico.</span><span class="sxs-lookup"><span data-stu-id="71236-214">Failed request logs are useful when trying to isolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="71236-215">Saiba mais sobre falha de solicitação de rastreamento</span><span class="sxs-lookup"><span data-stu-id="71236-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="71236-216">Para habilitar o Log de Servidor:</span><span class="sxs-lookup"><span data-stu-id="71236-216">To enable Server logging:</span></span>
- <span data-ttu-id="71236-217">vá para **Monitoramento** > **Logs de Diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="71236-217">go to **Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="71236-218">Habilite os diferentes tipos de Diagnóstico de Servidor Web usando as alternâncias.</span><span class="sxs-lookup"><span data-stu-id="71236-218">Enable the different types of Web Server Diagnostics using the toggles.</span></span>

![Monitorar o aplicativo](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="71236-220">Habilitar o registro no log tem um impacto sobre o desempenho do aplicativo e a utilização de recursos.</span><span class="sxs-lookup"><span data-stu-id="71236-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="71236-221">Para Cenários de Produção, os Logs de Erros são recomendados, Somente habilite o registro no log mais detalhado quando investigar problemas.</span><span class="sxs-lookup"><span data-stu-id="71236-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="71236-222">Acessar Logs</span><span class="sxs-lookup"><span data-stu-id="71236-222">Accessing Logs</span></span>
<span data-ttu-id="71236-223">Os logs armazenados no armazenamento de blobs são acessados usando o Gerenciador de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="71236-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="71236-224">Os logs armazenados no sistema de arquivos do aplicativo Web são acessados por meio de FTP nos seguintes caminhos:</span><span class="sxs-lookup"><span data-stu-id="71236-224">Logs stored in the Web App's filesystem are accessed through FTP under the following paths:</span></span>

- <span data-ttu-id="71236-225">**Logs de aplicativos** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="71236-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="71236-226">Essa pasta contém um ou mais arquivos de texto que contêm informações produzidas pelo log do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71236-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="71236-227">**Falha de solicitação de rastreamento** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="71236-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="71236-228">Esta pasta contém um arquivo XSL e um ou mais arquivos XML.</span><span class="sxs-lookup"><span data-stu-id="71236-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="71236-229">**Logs de erro detalhadas** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="71236-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="71236-230">Esta pasta contém um ou mais arquivos .htm com informações abrangentes sobre erros HTTP gerados pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71236-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="71236-231">**Logs do Web Server** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="71236-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="71236-232">Esta pasta contém um ou mais arquivos de texto formatados usando o formato do arquivo de log estendido do W3C.</span><span class="sxs-lookup"><span data-stu-id="71236-232">This folder contains one or more text files formatted using the W3C extended log file format.</span></span>

## <span data-ttu-id="71236-233"><a name="streaming"></a> Etapa 6 - Streaming de Log</span><span class="sxs-lookup"><span data-stu-id="71236-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="71236-234">Logs de streaming são convenientes durante a depuração de um aplicativo uma vez que ele economiza tempo em comparação comparado [acessar os logs de](#Accessing-Logs) por meio de FTP.</span><span class="sxs-lookup"><span data-stu-id="71236-234">Streaming logs are convenient when debugging an application since it saves time compared to [accessing the logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="71236-235">O Serviço de Aplicativo pode fazer streaming de **Logs do Aplicativo** e **Logs do Servidor Web** conforme eles são gerados.</span><span class="sxs-lookup"><span data-stu-id="71236-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="71236-236">Antes de tentar fazer streaming de logs certifique-se de que você habilitou a coleta de logs, conforme descrito na seção [Registrar em Log](#logging).</span><span class="sxs-lookup"><span data-stu-id="71236-236">Before trying to stream logs, make sure you have enabled collecting logs as described in the [Logging](#logging) section.</span></span>

<span data-ttu-id="71236-237">Para transmitir logs, vá para **monitoramento**> **fluxo de Log**.</span><span class="sxs-lookup"><span data-stu-id="71236-237">To stream logs, go to **Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="71236-238">Selecione **Logs do Aplicativo** ou **Logs do Servidor Web**, dependendo de quais informações você está procurando.</span><span class="sxs-lookup"><span data-stu-id="71236-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="71236-239">A partir daqui, também será possível pausar, reiniciar e limpar o buffer.</span><span class="sxs-lookup"><span data-stu-id="71236-239">From here, you can also pause, restart, and clear the buffer.</span></span>

![Logs de streaming](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="71236-241">Os logs são gerados apenas quando há tráfego no aplicativo, também é possível aumentar o nível de detalhes dos logs para obter mais eventos ou informações.</span><span class="sxs-lookup"><span data-stu-id="71236-241">Logs are only generated when there is traffic on the app, you can also increase the verbosity of logs to get more events or information.</span></span>

## <span data-ttu-id="71236-242"><a name="remote"></a> Etapa 7 - Depuração Remota</span><span class="sxs-lookup"><span data-stu-id="71236-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="71236-243">Após você ter pin pontas a origem dos problemas de aplicativos, use **depuração remota** para percorrer o código.</span><span class="sxs-lookup"><span data-stu-id="71236-243">Once you have pin-pointed the source of the applications problems, use **Remote Debugging** to walk through the code.</span></span>

<span data-ttu-id="71236-244">A Depuração remota permite anexar um depurador ao seu aplicativo Web em execução na nuvem.</span><span class="sxs-lookup"><span data-stu-id="71236-244">Remote debugging lets you attach a debugger to your Web App running in the cloud.</span></span> <span data-ttu-id="71236-245">É possível pode definir pontos de interrupção, manipular a memória diretamente, percorrer o código e até mesmo alterar o caminho do código, exatamente como para um aplicativo executado localmente.</span><span class="sxs-lookup"><span data-stu-id="71236-245">You can set breakpoints, manipulate memory directly, step through code, and even change the code path just like you do for an app running locally.</span></span>

<span data-ttu-id="71236-246">Para anexar o depurador ao seu aplicativo em execução na nuvem:</span><span class="sxs-lookup"><span data-stu-id="71236-246">To attach the debugger to your app running in the cloud:</span></span>

- <span data-ttu-id="71236-247">Usando o Visual Studio 2017, abra a solução para o aplicativo que deseja depurar</span><span class="sxs-lookup"><span data-stu-id="71236-247">Using Visual Studio 2017, open the solution for the app you want to debug</span></span>
- <span data-ttu-id="71236-248">Defina alguns pontos de interrupção, exatamente como faria para desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="71236-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="71236-249">Abra o **cloud explorer** (ctr + /, ctrl + x).</span><span class="sxs-lookup"><span data-stu-id="71236-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="71236-250">Faça logon com suas credenciais do Azure, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="71236-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="71236-251">Localize o aplicativo que deseja depurar</span><span class="sxs-lookup"><span data-stu-id="71236-251">Find the app you want to debug</span></span>
- <span data-ttu-id="71236-252">Selecione **Anexar Depurador** do painel **Ações**.</span><span class="sxs-lookup"><span data-stu-id="71236-252">Select **Attach Debugger** form the **Actions** pane.</span></span>

![Depuração Remota](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="71236-254">O Visual Studio configura seu aplicativo para depuração remota e inicia uma janela do navegador que navega até o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71236-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates to your app.</span></span> <span data-ttu-id="71236-255">Navegue pelo aplicativo para disparar pontos de interrupção e percorrer o código.</span><span class="sxs-lookup"><span data-stu-id="71236-255">Browse through your app to trigger break points and step through the code.</span></span>

> [!WARNING]
> <span data-ttu-id="71236-256">A execução em modo de depuração em produção não é recomendada.</span><span class="sxs-lookup"><span data-stu-id="71236-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="71236-257">Se o aplicativo de produção não for dimensionado para várias instâncias de servidor, a depuração impedirá que o servidor Web responda a outras solicitações.</span><span class="sxs-lookup"><span data-stu-id="71236-257">If your production app is not scaled out to multiple server instances, debugging prevent the web server from responding to other requests.</span></span> <span data-ttu-id="71236-258">Para solucionar problemas de produção, os melhores recursos são [configurar o registro em log](#logging) e [Application Insight](#insights).</span><span class="sxs-lookup"><span data-stu-id="71236-258">For troubleshooting production problems, your best resource is to [configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="71236-259"><a name="explorer"></a> Etapa 8 - Gerenciador de Processos</span><span class="sxs-lookup"><span data-stu-id="71236-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="71236-260">Quando seu aplicativo é dimensionado para mais de uma instância, **o process explorer** pode ajudar a identificar problemas específicos da instância.</span><span class="sxs-lookup"><span data-stu-id="71236-260">When your application is scaled out to more than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="71236-261">Use **Gerenciador de Processos** para:</span><span class="sxs-lookup"><span data-stu-id="71236-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="71236-262">Enumere todos os processos entre diferentes instâncias do seu plano de Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71236-262">Enumerate all the processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="71236-263">Analise detalhadamente e exiba os identificadores e módulos associados a cada processo.</span><span class="sxs-lookup"><span data-stu-id="71236-263">Drill down and view the handles and modules associated with each process.</span></span>
- <span data-ttu-id="71236-264">Exibir CPU, Conjunto de trabalho e contagem de Threads no nível de processo para ajudá-lo a identificar processos sem controle</span><span class="sxs-lookup"><span data-stu-id="71236-264">View CPU, Working Set, and Thread count at the process level to help you identify runaway processes</span></span>
- <span data-ttu-id="71236-265">Localize identificadores de arquivos abertos e, até mesmo, encerre uma instância de processo específico.</span><span class="sxs-lookup"><span data-stu-id="71236-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="71236-266">O Gerenciador de Processos pode estar em **Monitoramento** > **Explorador de Processos**.</span><span class="sxs-lookup"><span data-stu-id="71236-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Gerenciador de Processos](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="71236-268"><a name="insights"></a> Etapa 9 - Application Insights</span><span class="sxs-lookup"><span data-stu-id="71236-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="71236-269">O **Application Insights** fornece perfil de aplicativo e recursos avançados de monitoramento para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71236-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="71236-270">Use o Insights de Aplicativos para detectar e diagnosticar exceções e problemas de desempenho no Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="71236-270">Use Application Insights to detect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="71236-271">É possível habilitar o Application Insights para seu aplicativo Web em **Monitoramento** > **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="71236-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="71236-272">O Application Insights pode solicitar a instalação da extensão de site do Application Insights para iniciar a coleta de dados.</span><span class="sxs-lookup"><span data-stu-id="71236-272">Application Insights might prompt you to install the Application Insights site extension to start collecting data.</span></span> <span data-ttu-id="71236-273">Instalar a extensão de site causa o reinício do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71236-273">Installing the site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="71236-275">O Application Insights possui um avançado conjunto de recursos, para saber mais siga os links incluídos na seção [Próximas etapas](#next).</span><span class="sxs-lookup"><span data-stu-id="71236-275">Application Insights has a rich feature set, to learn more, follow the links included in the [Next Steps](#next) section.</span></span>

## <span data-ttu-id="71236-276"><a name="next"></a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="71236-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="71236-277">O que é o Application Insights</span><span class="sxs-lookup"><span data-stu-id="71236-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="71236-278">Monitorar o desempenho do aplicativo Web do Azure com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="71236-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="71236-279">Monitorar a disponibilidade e capacidade de resposta de qualquer site da Web com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="71236-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
