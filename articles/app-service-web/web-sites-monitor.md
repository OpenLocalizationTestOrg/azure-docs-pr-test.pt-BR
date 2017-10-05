---
title: "Monitorar aplicativos no Serviço de Aplicativo do Azure | Microsoft Docs"
description: "Saiba como monitorar Aplicativos no Serviço de Aplicativo do Azure usando o Portal do Azure."
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 25d3776920d683fffedcd8ac6ed0e84dfe875974
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="bd668-103">Como monitorar aplicativos Web no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="bd668-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="bd668-104">O [Serviço de Aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714) fornece a funcionalidade de monitoramento no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bd668-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in the [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="bd668-105">Isso inclui a capacidade de examinar **cotas** e **métricas** para um aplicativo, bem como o Plano do Serviço de Aplicativo, configurar **alertas** e até mesmo **dimensionar** automaticamente de acordo com essas métricas.</span><span class="sxs-lookup"><span data-stu-id="bd668-105">This includes the ability to review **quotas** and **metrics** for an app as well as the App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="bd668-106">Noções básicas sobre cotas e métricas</span><span class="sxs-lookup"><span data-stu-id="bd668-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="bd668-107">Cotas</span><span class="sxs-lookup"><span data-stu-id="bd668-107">Quotas</span></span>
<span data-ttu-id="bd668-108">Aplicativos hospedados no Serviço de Aplicativo estão sujeitos a determinados *limites* de recursos que eles podem usar.</span><span class="sxs-lookup"><span data-stu-id="bd668-108">Applications hosted in App Service are subject to certain *limits* on the resources they can use.</span></span> <span data-ttu-id="bd668-109">Os limites são definidos pelo **Plano do Serviço de Aplicativo** associado ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd668-109">The limits are defined by the **App Service plan** associated with the app.</span></span>

<span data-ttu-id="bd668-110">Se o aplicativo estiver hospedado em um plano **Gratuito** ou **Compartilhado**, os limites de uso dos recursos que o aplicativo pode usar são definidos por **Cotas**.</span><span class="sxs-lookup"><span data-stu-id="bd668-110">If the application is hosted in a **Free** or **Shared** plan, then the limits on the resources the app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="bd668-111">Se o aplicativo estiver hospedado em um plano **Básico**, **Standard** ou **Premium**, os limites de uso dos recursos que podem usar são definidos pelo **tamanho** (Pequeno, Médio, Grande) e **contagem de instâncias** (1, 2, 3,...) do **Plano do Serviço de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="bd668-111">If the application is hosted in a **Basic**, **Standard** or **Premium** plan, then the limits on the resources they can use are set by the **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of the **App Service plan**.</span></span>

<span data-ttu-id="bd668-112">**Cotas** para aplicativos **Gratuitos** ou **Compartilhados** são:</span><span class="sxs-lookup"><span data-stu-id="bd668-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="bd668-113">**CPU(Curto)**</span><span class="sxs-lookup"><span data-stu-id="bd668-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="bd668-114">Quantidade de CPU permitida para esse aplicativo em um intervalo de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="bd668-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="bd668-115">Essa cota é definida novamente a cada cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="bd668-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="bd668-116">**CPU(dia)**</span><span class="sxs-lookup"><span data-stu-id="bd668-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="bd668-117">Quantidade total de CPU permitida para esse aplicativo em um dia.</span><span class="sxs-lookup"><span data-stu-id="bd668-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="bd668-118">Essa cota é definida novamente a cada 24 horas, à meia-noite UTC.</span><span class="sxs-lookup"><span data-stu-id="bd668-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="bd668-119">**Memória**</span><span class="sxs-lookup"><span data-stu-id="bd668-119">**Memory**</span></span>
  * <span data-ttu-id="bd668-120">Quantidade total de memória permitida para esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd668-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="bd668-121">**Largura de banda**</span><span class="sxs-lookup"><span data-stu-id="bd668-121">**Bandwidth**</span></span>
  * <span data-ttu-id="bd668-122">Quantidade total de largura de banda de saída permitida para esse aplicativo em um dia.</span><span class="sxs-lookup"><span data-stu-id="bd668-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="bd668-123">Essa cota é definida novamente a cada 24 horas, à meia-noite UTC.</span><span class="sxs-lookup"><span data-stu-id="bd668-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="bd668-124">**Sistema de arquivos**</span><span class="sxs-lookup"><span data-stu-id="bd668-124">**Filesystem**</span></span>
  * <span data-ttu-id="bd668-125">Quantidade total de armazenamento permitida.</span><span class="sxs-lookup"><span data-stu-id="bd668-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="bd668-126">A única cota aplicável aos aplicativos hospedados no plano **Básico**, **Standard** e **Premium** é **Sistema de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="bd668-126">The only quota applicable to apps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="bd668-127">Para saber mais sobre cotas, limites e recursos específicos disponíveis para SKUs de Serviço de Aplicativo diferentes, confira: [Limites do serviço de assinatura do Azure](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="bd668-127">More information about the specific quotas, limits and features available to the different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="bd668-128">Aplicação de cota</span><span class="sxs-lookup"><span data-stu-id="bd668-128">Quota Enforcement</span></span>
<span data-ttu-id="bd668-129">Se, durante o uso, um aplicativo exceder a cota **CPU (curto)**, **CPU (dia)** ou **largura de banda**, o aplicativo será interrompido até que a cota seja redefinida.</span><span class="sxs-lookup"><span data-stu-id="bd668-129">If an application in its usage exceeds the **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then the application will be stopped until the quota re-sets.</span></span> <span data-ttu-id="bd668-130">Durante esse tempo, todas as solicitações de entrada resultarão em um **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="bd668-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="bd668-131">Se a cota **memória** do aplicativo for excedida, o aplicativo será reiniciado.</span><span class="sxs-lookup"><span data-stu-id="bd668-131">If the application **memory** quota is exceeded, then the application will be re-started.</span></span>

<span data-ttu-id="bd668-132">Se a cota **Sistema de arquivos** for excedida, qualquer operação falhará, incluindo a gravação em logs.</span><span class="sxs-lookup"><span data-stu-id="bd668-132">If the **Filesystem** quota is exceeded, then any write operation will fail, this includes writing to logs.</span></span>

<span data-ttu-id="bd668-133">As cotas podem ser aumentadas ou removidas de seu aplicativo pela atualização de seu Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd668-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="bd668-134">Métricas</span><span class="sxs-lookup"><span data-stu-id="bd668-134">Metrics</span></span>
<span data-ttu-id="bd668-135">**Métricas** fornecem informações sobre o aplicativo, ou sobre o comportamento do Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd668-135">**Metrics** provide information about the app, or App Service plan's behavior.</span></span>

<span data-ttu-id="bd668-136">Para um **Aplicativo**, as métricas disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="bd668-136">For an **Application**, the available metrics are:</span></span>

* <span data-ttu-id="bd668-137">**Tempo Médio de Resposta**</span><span class="sxs-lookup"><span data-stu-id="bd668-137">**Average Response Time**</span></span>
  * <span data-ttu-id="bd668-138">O tempo médio necessário para o aplicativo atender às solicitações em ms.</span><span class="sxs-lookup"><span data-stu-id="bd668-138">The average time taken for the app to serve requests in ms.</span></span>
* <span data-ttu-id="bd668-139">**Conjunto de trabalho de memória média**</span><span class="sxs-lookup"><span data-stu-id="bd668-139">**Average memory working set**</span></span>
  * <span data-ttu-id="bd668-140">A quantidade média de memória em MiBs usada pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd668-140">The average amount of memory in MiBs used by the app.</span></span>
* <span data-ttu-id="bd668-141">**Tempo de CPU**</span><span class="sxs-lookup"><span data-stu-id="bd668-141">**CPU Time**</span></span>
  * <span data-ttu-id="bd668-142">A quantidade de CPU em segundos consumida pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd668-142">The amount of CPU in seconds consumed by the app.</span></span> <span data-ttu-id="bd668-143">Para saber mais sobre essa métrica, consulte: [Tempo de CPU versus percentual de CPU](#cpu-time-vs-cpu-percentage)</span><span class="sxs-lookup"><span data-stu-id="bd668-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="bd668-144">**Entrada de Dados**</span><span class="sxs-lookup"><span data-stu-id="bd668-144">**Data In**</span></span>
  * <span data-ttu-id="bd668-145">A quantidade de largura de banda de entrada consumida pelo aplicativo em MiBs.</span><span class="sxs-lookup"><span data-stu-id="bd668-145">The amount of incoming bandwidth consumed by the app in MiBs.</span></span>
* <span data-ttu-id="bd668-146">**Saída de dados**</span><span class="sxs-lookup"><span data-stu-id="bd668-146">**Data Out**</span></span>
  * <span data-ttu-id="bd668-147">A quantidade de largura de banda de saída consumida pelo aplicativo em MiBs.</span><span class="sxs-lookup"><span data-stu-id="bd668-147">The amount of outgoing bandwidth consumed by the app in MiBs.</span></span>
* <span data-ttu-id="bd668-148">**Http 2xx**</span><span class="sxs-lookup"><span data-stu-id="bd668-148">**Http 2xx**</span></span>
  * <span data-ttu-id="bd668-149">Contagem de solicitações que resultam em um código de status http > = 200, mas < 300.</span><span class="sxs-lookup"><span data-stu-id="bd668-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="bd668-150">**Http 3xx**</span><span class="sxs-lookup"><span data-stu-id="bd668-150">**Http 3xx**</span></span>
  * <span data-ttu-id="bd668-151">Contagem de solicitações que resultam em um código de status http > = 300, mas < 400.</span><span class="sxs-lookup"><span data-stu-id="bd668-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="bd668-152">**Http 401**</span><span class="sxs-lookup"><span data-stu-id="bd668-152">**Http 401**</span></span>
  * <span data-ttu-id="bd668-153">Contagem de solicitações que resultam em um código de status HTTP 401.</span><span class="sxs-lookup"><span data-stu-id="bd668-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="bd668-154">**Http 403**</span><span class="sxs-lookup"><span data-stu-id="bd668-154">**Http 403**</span></span>
  * <span data-ttu-id="bd668-155">Contagem de solicitações que resultam em um código de status HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="bd668-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="bd668-156">**Http 404**</span><span class="sxs-lookup"><span data-stu-id="bd668-156">**Http 404**</span></span>
  * <span data-ttu-id="bd668-157">Contagem de solicitações que resultam em um código de status HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="bd668-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="bd668-158">**Http 406**</span><span class="sxs-lookup"><span data-stu-id="bd668-158">**Http 406**</span></span>
  * <span data-ttu-id="bd668-159">Contagem de solicitações que resultam em um código de status HTTP 406.</span><span class="sxs-lookup"><span data-stu-id="bd668-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="bd668-160">**Http 4xx**</span><span class="sxs-lookup"><span data-stu-id="bd668-160">**Http 4xx**</span></span>
  * <span data-ttu-id="bd668-161">Contagem de solicitações que resultam em um código de status http > = 400, mas < 500.</span><span class="sxs-lookup"><span data-stu-id="bd668-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="bd668-162">**Erros do Servidor Http**</span><span class="sxs-lookup"><span data-stu-id="bd668-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="bd668-163">Contagem de solicitações que resultam em um código de status http > = 500, mas < 600.</span><span class="sxs-lookup"><span data-stu-id="bd668-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="bd668-164">**Conjunto de trabalho de memória**</span><span class="sxs-lookup"><span data-stu-id="bd668-164">**Memory working set**</span></span>
  * <span data-ttu-id="bd668-165">Quantidade atual de memória usada pelo aplicativo em MiBs.</span><span class="sxs-lookup"><span data-stu-id="bd668-165">Current amount of memory used by the app in MiBs.</span></span>
* <span data-ttu-id="bd668-166">**Solicitações**</span><span class="sxs-lookup"><span data-stu-id="bd668-166">**Requests**</span></span>
  * <span data-ttu-id="bd668-167">Número total de solicitações, independentemente de seu código de status HTTP resultante.</span><span class="sxs-lookup"><span data-stu-id="bd668-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="bd668-168">Para um **Plano do Serviço de Aplicativo**, as métricas disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="bd668-168">For an **App Service plan**, the available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="bd668-169">As métricas do Plano do Serviço de Aplicativo só estão disponíveis para os planos no SKU **Básico**, **Standard** e **Premium**.</span><span class="sxs-lookup"><span data-stu-id="bd668-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="bd668-170">**Porcentagem de CPU**</span><span class="sxs-lookup"><span data-stu-id="bd668-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="bd668-171">A média de CPU usada em todas as instâncias do plano.</span><span class="sxs-lookup"><span data-stu-id="bd668-171">The average CPU used across all instances of the plan.</span></span>
* <span data-ttu-id="bd668-172">**Porcentagem de Memória**</span><span class="sxs-lookup"><span data-stu-id="bd668-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="bd668-173">A média de memória usada em todas as instâncias do plano.</span><span class="sxs-lookup"><span data-stu-id="bd668-173">The average memory used across all instances of the plan.</span></span>
* <span data-ttu-id="bd668-174">**Entrada de Dados**</span><span class="sxs-lookup"><span data-stu-id="bd668-174">**Data In**</span></span>
  * <span data-ttu-id="bd668-175">A média de largura de banda de entrada usada em todas as instâncias do plano.</span><span class="sxs-lookup"><span data-stu-id="bd668-175">The average incoming bandwidth used across all instances of the plan.</span></span>
* <span data-ttu-id="bd668-176">**Saída de dados**</span><span class="sxs-lookup"><span data-stu-id="bd668-176">**Data Out**</span></span>
  * <span data-ttu-id="bd668-177">A média de largura de banda de saída usada em todas as instâncias do plano.</span><span class="sxs-lookup"><span data-stu-id="bd668-177">The average outgoing bandwidth used across all instances of the plan.</span></span>
* <span data-ttu-id="bd668-178">**Tamanho da fila do disco**</span><span class="sxs-lookup"><span data-stu-id="bd668-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="bd668-179">O número médio de solicitações de leitura e gravação enfileiradas no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bd668-179">The average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="bd668-180">Um tamanho grande de fila de disco é uma indicação de um aplicativo que pode estar lento devido ao excesso de E/S de disco.</span><span class="sxs-lookup"><span data-stu-id="bd668-180">A high disk queue length is an indication of an application that might be slowing down due to excessive disk I/O.</span></span>
* <span data-ttu-id="bd668-181">**Tamanho da Fila de Http**</span><span class="sxs-lookup"><span data-stu-id="bd668-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="bd668-182">O número médio de solicitações HTTP que tiveram de esperar na fila antes de serem atendidas.</span><span class="sxs-lookup"><span data-stu-id="bd668-182">The average number of HTTP requests that had to sit on the queue before being fulfilled.</span></span> <span data-ttu-id="bd668-183">Um tamanho de fila HTTP alto ou crescente é um sintoma de um plano sob carga pesada.</span><span class="sxs-lookup"><span data-stu-id="bd668-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="bd668-184">Tempo de CPU versus porcentagem de CPU</span><span class="sxs-lookup"><span data-stu-id="bd668-184">CPU time vs CPU percentage</span></span>
<!-- To do: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="bd668-185">Há duas métricas que refletem o uso da CPU.</span><span class="sxs-lookup"><span data-stu-id="bd668-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="bd668-186">**Tempo de CPU** e **Percentual de CPU**</span><span class="sxs-lookup"><span data-stu-id="bd668-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="bd668-187">**Tempo de CPU** é útil para aplicativos hospedados nos planos **Gratuito** ou **Compartilhado** desde que uma de suas cotas seja definida em minutos de CPU usados pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd668-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by the app.</span></span>

<span data-ttu-id="bd668-188">O **percentual de CPU**, por outro lado, é útil para aplicativos hospedados em planos **Básico**, **Standard** e **Premium**, já que podem ser expandidos e essa métrica é uma boa indicação do uso geral em todas as instâncias.</span><span class="sxs-lookup"><span data-stu-id="bd668-188">**CPU percentage** on the other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of the overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="bd668-189">Granularidade de Métricas e a Política de Retenção</span><span class="sxs-lookup"><span data-stu-id="bd668-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="bd668-190">As métricas de um aplicativo e de um Plano do Serviço de Aplicativo são registradas e agregadas pelo serviço com as seguintes granularidades e políticas de retenção:</span><span class="sxs-lookup"><span data-stu-id="bd668-190">Metrics for an application and app service plan are logged and aggregated by the service with the following granularities and retention policies:</span></span>

* <span data-ttu-id="bd668-191">Métricas de granularidade de **minuto** são mantidas por **48 horas**</span><span class="sxs-lookup"><span data-stu-id="bd668-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="bd668-192">Métricas de granularidade de **hora** são mantidas por **30 dias**</span><span class="sxs-lookup"><span data-stu-id="bd668-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="bd668-193">Métricas de granularidade de **dia** são mantidas por **90 dias**</span><span class="sxs-lookup"><span data-stu-id="bd668-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-the-azure-portal"></a><span data-ttu-id="bd668-194">Monitoramento de cotas e métricas no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd668-194">Monitoring Quotas and Metrics in the Azure Portal.</span></span>
<span data-ttu-id="bd668-195">Você pode examinar o status das diferentes **cotas** e **métricas** que afetam um aplicativo no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bd668-195">You can review the status of the different **quotas** and **metrics** affecting an application in the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="bd668-196">![][quotas]
**Cotas** podem ser encontradas em Configurações >**Cotas**.</span><span class="sxs-lookup"><span data-stu-id="bd668-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="bd668-197">A experiência do usuário permite que você examine: (1) o nome das cotas, (2) o intervalo de redefinição, (3) o limite atual e (4) o valor atual.</span><span class="sxs-lookup"><span data-stu-id="bd668-197">The UX allows you to review: (1) the quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="bd668-198">![][metrics]
**Métricas** podem ser acessadas diretamente da folha do recurso.</span><span class="sxs-lookup"><span data-stu-id="bd668-198">![][metrics]
**Metrics** can be access directly from the resource blade.</span></span> <span data-ttu-id="bd668-199">Você também pode personalizar o gráfico da seguinte maneira: (1) **clique** nele e (2) selecione **editar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="bd668-199">You can also customize the chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="bd668-200">A partir daqui, você pode alterar (3) o **intervalo de tempo**, (4) o **tipo de gráfico** e (5) as **métricas** a serem exibidas.</span><span class="sxs-lookup"><span data-stu-id="bd668-200">From here you can change the (3) **time range**, (4) **chart type**, and (5) **metrics** to display.</span></span>  

<span data-ttu-id="bd668-201">Saiba mais sobre métricas aqui: [Monitorar as métricas do serviço](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="bd668-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="bd668-202">Alertas e dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="bd668-202">Alerts and Autoscale</span></span>
<span data-ttu-id="bd668-203">As métricas de um Aplicativo ou Plano do Serviço de Aplicativo podem ser conectadas a alertas, para saber mais sobre isso, consulte [Receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="bd668-203">Metrics for an App or App Service plan can be hooked up to alerts, to learn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="bd668-204">Aplicativos do Serviço de Aplicativo hospedados em Planos do Serviço de Aplicativo Básico, Standard ou Premium oferecem suporte ao **Dimensionamento Automático**.</span><span class="sxs-lookup"><span data-stu-id="bd668-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="bd668-205">Isso permite que você configure regras que monitoram as métricas do Plano do Serviço de Aplicativo e podem aumentar ou diminuir a contagem de instâncias, fornecendo recursos adicionais conforme o necessário, ou economizando dinheiro quando o aplicativo é provisionado de forma excessiva.</span><span class="sxs-lookup"><span data-stu-id="bd668-205">This allows you to configure rules that monitor the App Service plan metrics and can increase or decrease the instance count providing additional resources as needed, or saving money when the application is over-provision.</span></span> <span data-ttu-id="bd668-206">Saiba mais sobre o dimensionamento automático aqui: [Como dimensionar](../monitoring-and-diagnostics/insights-how-to-scale.md) e aqui [Práticas recomendadas para o dimensionamento automático do Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="bd668-206">You can learn more about auto scale here: [How to Scale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="bd668-207">Se desejar começar a usar o Serviço de Aplicativo do Azure antes de inscrever-se em uma conta do Azure, vá para [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd668-207">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="bd668-208">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="bd668-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="bd668-209">O que mudou</span><span class="sxs-lookup"><span data-stu-id="bd668-209">What's changed</span></span>
* <span data-ttu-id="bd668-210">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="bd668-210">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
