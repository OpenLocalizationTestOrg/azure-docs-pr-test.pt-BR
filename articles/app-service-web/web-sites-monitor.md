---
title: "aaaMonitor aplicativos no serviço de aplicativo do Azure | Microsoft Docs"
description: "Saiba como toomonitor aplicativos no serviço de aplicativo do Azure usando Olá Portal do Azure."
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
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="678e9-103">Como monitorar aplicativos Web no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="678e9-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="678e9-104">[Serviço de aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714) fornece funcionalidade interna de monitoramento no hello [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="678e9-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in hello [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="678e9-105">Isso inclui Olá capacidade tooreview **cotas** e **métricas** para um aplicativo, bem como Olá plano de serviço de aplicativo, configurando **alertas** e até mesmo **dimensionamento** automaticamente de acordo com essas métricas.</span><span class="sxs-lookup"><span data-stu-id="678e9-105">This includes hello ability tooreview **quotas** and **metrics** for an app as well as hello App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="678e9-106">Noções básicas sobre cotas e métricas</span><span class="sxs-lookup"><span data-stu-id="678e9-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="678e9-107">Cotas</span><span class="sxs-lookup"><span data-stu-id="678e9-107">Quotas</span></span>
<span data-ttu-id="678e9-108">Aplicativos hospedados no serviço de aplicativo são o assunto toocertain *limites* nos recursos que eles podem usar.</span><span class="sxs-lookup"><span data-stu-id="678e9-108">Applications hosted in App Service are subject toocertain *limits* on the resources they can use.</span></span> <span data-ttu-id="678e9-109">Olá limites são definidos por Olá **plano de serviço de aplicativo** associado ao aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="678e9-109">hello limits are defined by hello **App Service plan** associated with hello app.</span></span>

<span data-ttu-id="678e9-110">Se o aplicativo hello está hospedado em um **livre** ou **compartilhado** planejar, em seguida, limites de saudação em recursos Olá Olá aplicativo pode usar são definidos por **cotas**.</span><span class="sxs-lookup"><span data-stu-id="678e9-110">If hello application is hosted in a **Free** or **Shared** plan, then hello limits on hello resources hello app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="678e9-111">Se o aplicativo hello está hospedado em um **básica**, **padrão** ou **Premium** planejar, em seguida, limites de saudação em recursos Olá usarem são definidas pelas Olá **tamanho** (Pequeno, médio, grande) e **a contagem de instâncias** (1, 2, 3,...) do hello **plano de serviço de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="678e9-111">If hello application is hosted in a **Basic**, **Standard** or **Premium** plan, then hello limits on hello resources they can use are set by hello **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of hello **App Service plan**.</span></span>

<span data-ttu-id="678e9-112">**Cotas** para aplicativos **Gratuitos** ou **Compartilhados** são:</span><span class="sxs-lookup"><span data-stu-id="678e9-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="678e9-113">**CPU(Curto)**</span><span class="sxs-lookup"><span data-stu-id="678e9-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="678e9-114">Quantidade de CPU permitida para esse aplicativo em um intervalo de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="678e9-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="678e9-115">Essa cota é definida novamente a cada cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="678e9-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="678e9-116">**CPU(dia)**</span><span class="sxs-lookup"><span data-stu-id="678e9-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="678e9-117">Quantidade total de CPU permitida para esse aplicativo em um dia.</span><span class="sxs-lookup"><span data-stu-id="678e9-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="678e9-118">Essa cota é definida novamente a cada 24 horas, à meia-noite UTC.</span><span class="sxs-lookup"><span data-stu-id="678e9-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="678e9-119">**Memória**</span><span class="sxs-lookup"><span data-stu-id="678e9-119">**Memory**</span></span>
  * <span data-ttu-id="678e9-120">Quantidade total de memória permitida para esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="678e9-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="678e9-121">**Largura de banda**</span><span class="sxs-lookup"><span data-stu-id="678e9-121">**Bandwidth**</span></span>
  * <span data-ttu-id="678e9-122">Quantidade total de largura de banda de saída permitida para esse aplicativo em um dia.</span><span class="sxs-lookup"><span data-stu-id="678e9-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="678e9-123">Essa cota é definida novamente a cada 24 horas, à meia-noite UTC.</span><span class="sxs-lookup"><span data-stu-id="678e9-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="678e9-124">**Sistema de arquivos**</span><span class="sxs-lookup"><span data-stu-id="678e9-124">**Filesystem**</span></span>
  * <span data-ttu-id="678e9-125">Quantidade total de armazenamento permitida.</span><span class="sxs-lookup"><span data-stu-id="678e9-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="678e9-126">Olá somente cota aplicável tooapps hospedado em **básica**, **padrão** e **Premium** planos é **Filesystem**.</span><span class="sxs-lookup"><span data-stu-id="678e9-126">hello only quota applicable tooapps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="678e9-127">Para obter mais informações sobre cotas específicas hello, limites e recursos disponíveis para Olá diferentes SKUs do serviço de aplicativo podem ser encontradas aqui: [limites de serviço de assinatura do Azure](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="678e9-127">More information about hello specific quotas, limits and features available to hello different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="678e9-128">Aplicação de cota</span><span class="sxs-lookup"><span data-stu-id="678e9-128">Quota Enforcement</span></span>
<span data-ttu-id="678e9-129">Se um aplicativo em seu uso exceder Olá **CPU (curta)**, **CPU (dia)**, ou **largura de banda** cota, Olá aplicativo será interrompido até que a cota de saudação define novamente.</span><span class="sxs-lookup"><span data-stu-id="678e9-129">If an application in its usage exceeds hello **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then hello application will be stopped until hello quota re-sets.</span></span> <span data-ttu-id="678e9-130">Durante esse tempo, todas as solicitações de entrada resultarão em um **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="678e9-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="678e9-131">Se Olá aplicativo **memória** cota for excedida, aplicativo hello será reiniciado.</span><span class="sxs-lookup"><span data-stu-id="678e9-131">If hello application **memory** quota is exceeded, then hello application will be re-started.</span></span>

<span data-ttu-id="678e9-132">Se hello **Filesystem** cota for excedida, em seguida, qualquer operação irá falhar, isso inclui gravar toologs de gravação.</span><span class="sxs-lookup"><span data-stu-id="678e9-132">If hello **Filesystem** quota is exceeded, then any write operation will fail, this includes writing toologs.</span></span>

<span data-ttu-id="678e9-133">As cotas podem ser aumentadas ou removidas de seu aplicativo pela atualização de seu Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="678e9-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="678e9-134">Métricas</span><span class="sxs-lookup"><span data-stu-id="678e9-134">Metrics</span></span>
<span data-ttu-id="678e9-135">**Métricas** fornecem informações sobre o aplicativo hello ou o comportamento do plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="678e9-135">**Metrics** provide information about hello app, or App Service plan's behavior.</span></span>

<span data-ttu-id="678e9-136">Para uma **aplicativo**, métricas de saudação disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="678e9-136">For an **Application**, hello available metrics are:</span></span>

* <span data-ttu-id="678e9-137">**Tempo Médio de Resposta**</span><span class="sxs-lookup"><span data-stu-id="678e9-137">**Average Response Time**</span></span>
  * <span data-ttu-id="678e9-138">Olá tempo médio para solicitações de tooserve aplicativo hello em ms.</span><span class="sxs-lookup"><span data-stu-id="678e9-138">hello average time taken for hello app tooserve requests in ms.</span></span>
* <span data-ttu-id="678e9-139">**Conjunto de trabalho de memória média**</span><span class="sxs-lookup"><span data-stu-id="678e9-139">**Average memory working set**</span></span>
  * <span data-ttu-id="678e9-140">tempo médio de saudação de memória em MiBs usada pelo aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="678e9-140">hello average amount of memory in MiBs used by hello app.</span></span>
* <span data-ttu-id="678e9-141">**Tempo de CPU**</span><span class="sxs-lookup"><span data-stu-id="678e9-141">**CPU Time**</span></span>
  * <span data-ttu-id="678e9-142">quantidade de saudação da CPU em segundos consumidos por um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="678e9-142">hello amount of CPU in seconds consumed by hello app.</span></span> <span data-ttu-id="678e9-143">Para saber mais sobre essa métrica, consulte: [Tempo de CPU versus percentual de CPU](#cpu-time-vs-cpu-percentage)</span><span class="sxs-lookup"><span data-stu-id="678e9-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="678e9-144">**Entrada de Dados**</span><span class="sxs-lookup"><span data-stu-id="678e9-144">**Data In**</span></span>
  * <span data-ttu-id="678e9-145">quantidade de saudação de entrada largura de banda consumida pelo aplicativo hello em MiBs.</span><span class="sxs-lookup"><span data-stu-id="678e9-145">hello amount of incoming bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="678e9-146">**Saída de dados**</span><span class="sxs-lookup"><span data-stu-id="678e9-146">**Data Out**</span></span>
  * <span data-ttu-id="678e9-147">quantidade de saudação de saída de largura de banda consumida por um aplicativo hello MiBs.</span><span class="sxs-lookup"><span data-stu-id="678e9-147">hello amount of outgoing bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="678e9-148">**Http 2xx**</span><span class="sxs-lookup"><span data-stu-id="678e9-148">**Http 2xx**</span></span>
  * <span data-ttu-id="678e9-149">Contagem de solicitações que resultam em um código de status http > = 200, mas < 300.</span><span class="sxs-lookup"><span data-stu-id="678e9-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="678e9-150">**Http 3xx**</span><span class="sxs-lookup"><span data-stu-id="678e9-150">**Http 3xx**</span></span>
  * <span data-ttu-id="678e9-151">Contagem de solicitações que resultam em um código de status http > = 300, mas < 400.</span><span class="sxs-lookup"><span data-stu-id="678e9-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="678e9-152">**Http 401**</span><span class="sxs-lookup"><span data-stu-id="678e9-152">**Http 401**</span></span>
  * <span data-ttu-id="678e9-153">Contagem de solicitações que resultam em um código de status HTTP 401.</span><span class="sxs-lookup"><span data-stu-id="678e9-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="678e9-154">**Http 403**</span><span class="sxs-lookup"><span data-stu-id="678e9-154">**Http 403**</span></span>
  * <span data-ttu-id="678e9-155">Contagem de solicitações que resultam em um código de status HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="678e9-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="678e9-156">**Http 404**</span><span class="sxs-lookup"><span data-stu-id="678e9-156">**Http 404**</span></span>
  * <span data-ttu-id="678e9-157">Contagem de solicitações que resultam em um código de status HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="678e9-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="678e9-158">**Http 406**</span><span class="sxs-lookup"><span data-stu-id="678e9-158">**Http 406**</span></span>
  * <span data-ttu-id="678e9-159">Contagem de solicitações que resultam em um código de status HTTP 406.</span><span class="sxs-lookup"><span data-stu-id="678e9-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="678e9-160">**Http 4xx**</span><span class="sxs-lookup"><span data-stu-id="678e9-160">**Http 4xx**</span></span>
  * <span data-ttu-id="678e9-161">Contagem de solicitações que resultam em um código de status http > = 400, mas < 500.</span><span class="sxs-lookup"><span data-stu-id="678e9-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="678e9-162">**Erros do Servidor Http**</span><span class="sxs-lookup"><span data-stu-id="678e9-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="678e9-163">Contagem de solicitações que resultam em um código de status http > = 500, mas < 600.</span><span class="sxs-lookup"><span data-stu-id="678e9-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="678e9-164">**Conjunto de trabalho de memória**</span><span class="sxs-lookup"><span data-stu-id="678e9-164">**Memory working set**</span></span>
  * <span data-ttu-id="678e9-165">Quantidade de memória usada pelo aplicativo hello MiBs atual.</span><span class="sxs-lookup"><span data-stu-id="678e9-165">Current amount of memory used by hello app in MiBs.</span></span>
* <span data-ttu-id="678e9-166">**Solicitações**</span><span class="sxs-lookup"><span data-stu-id="678e9-166">**Requests**</span></span>
  * <span data-ttu-id="678e9-167">Número total de solicitações, independentemente de seu código de status HTTP resultante.</span><span class="sxs-lookup"><span data-stu-id="678e9-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="678e9-168">Para uma **plano de serviço de aplicativo**, métricas de saudação disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="678e9-168">For an **App Service plan**, hello available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="678e9-169">As métricas do Plano do Serviço de Aplicativo só estão disponíveis para os planos no SKU **Básico**, **Standard** e **Premium**.</span><span class="sxs-lookup"><span data-stu-id="678e9-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="678e9-170">**Porcentagem de CPU**</span><span class="sxs-lookup"><span data-stu-id="678e9-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="678e9-171">Olá média de CPU usada por todas as instâncias do plano de saudação.</span><span class="sxs-lookup"><span data-stu-id="678e9-171">hello average CPU used across all instances of hello plan.</span></span>
* <span data-ttu-id="678e9-172">**Porcentagem de Memória**</span><span class="sxs-lookup"><span data-stu-id="678e9-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="678e9-173">Olá média da memória usada em todas as instâncias do plano de saudação.</span><span class="sxs-lookup"><span data-stu-id="678e9-173">hello average memory used across all instances of hello plan.</span></span>
* <span data-ttu-id="678e9-174">**Entrada de Dados**</span><span class="sxs-lookup"><span data-stu-id="678e9-174">**Data In**</span></span>
  * <span data-ttu-id="678e9-175">Olá entrada largura de banda média usada em todas as instâncias do plano de saudação.</span><span class="sxs-lookup"><span data-stu-id="678e9-175">hello average incoming bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="678e9-176">**Saída de dados**</span><span class="sxs-lookup"><span data-stu-id="678e9-176">**Data Out**</span></span>
  * <span data-ttu-id="678e9-177">Média de saudação largura de banda usada em todas as instâncias do plano de saudação de saída.</span><span class="sxs-lookup"><span data-stu-id="678e9-177">hello average outgoing bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="678e9-178">**Tamanho da fila do disco**</span><span class="sxs-lookup"><span data-stu-id="678e9-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="678e9-179">número médio de saudação de ler e gravar solicitações enfileiradas no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="678e9-179">hello average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="678e9-180">Um comprimento de fila de disco alta é uma indicação de um aplicativo que pode ser lento devido a e/s de disco tooexcessive.</span><span class="sxs-lookup"><span data-stu-id="678e9-180">A high disk queue length is an indication of an application that might be slowing down due tooexcessive disk I/O.</span></span>
* <span data-ttu-id="678e9-181">**Tamanho da Fila de Http**</span><span class="sxs-lookup"><span data-stu-id="678e9-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="678e9-182">Olá média de solicitações HTTP que tinha toosit na fila de saudação antes que está sendo atendida.</span><span class="sxs-lookup"><span data-stu-id="678e9-182">hello average number of HTTP requests that had toosit on hello queue before being fulfilled.</span></span> <span data-ttu-id="678e9-183">Um tamanho de fila HTTP alto ou crescente é um sintoma de um plano sob carga pesada.</span><span class="sxs-lookup"><span data-stu-id="678e9-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="678e9-184">Tempo de CPU versus porcentagem de CPU</span><span class="sxs-lookup"><span data-stu-id="678e9-184">CPU time vs CPU percentage</span></span>
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="678e9-185">Há duas métricas que refletem o uso da CPU.</span><span class="sxs-lookup"><span data-stu-id="678e9-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="678e9-186">**Tempo de CPU** e **Percentual de CPU**</span><span class="sxs-lookup"><span data-stu-id="678e9-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="678e9-187">**Tempo de CPU** é útil para aplicativos hospedados em **livre** ou **compartilhado** planos como uma das suas cotas é definida em minutos de CPU usados pelo aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="678e9-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by hello app.</span></span>

<span data-ttu-id="678e9-188">**Porcentagem de CPU** em Olá outro lado é útil para aplicativos hospedados em **básica**, **padrão** e **premium** planos desde que eles podem ser expandidos e essa métrica é uma boa indicação da saudação uso geral em todas as instâncias.</span><span class="sxs-lookup"><span data-stu-id="678e9-188">**CPU percentage** on hello other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of hello overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="678e9-189">Granularidade de Métricas e a Política de Retenção</span><span class="sxs-lookup"><span data-stu-id="678e9-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="678e9-190">Métricas para um plano de serviço de aplicativo e de aplicativo são registradas e agregadas por serviço Olá com hello granularidades e políticas de retenção a seguir:</span><span class="sxs-lookup"><span data-stu-id="678e9-190">Metrics for an application and app service plan are logged and aggregated by hello service with hello following granularities and retention policies:</span></span>

* <span data-ttu-id="678e9-191">Métricas de granularidade de **minuto** são mantidas por **48 horas**</span><span class="sxs-lookup"><span data-stu-id="678e9-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="678e9-192">Métricas de granularidade de **hora** são mantidas por **30 dias**</span><span class="sxs-lookup"><span data-stu-id="678e9-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="678e9-193">Métricas de granularidade de **dia** são mantidas por **90 dias**</span><span class="sxs-lookup"><span data-stu-id="678e9-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a><span data-ttu-id="678e9-194">Monitoramento de métricas e cotas no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="678e9-194">Monitoring Quotas and Metrics in hello Azure Portal.</span></span>
<span data-ttu-id="678e9-195">Você pode examinar o status de saudação do hello diferente **cotas** e **métricas** afetar um aplicativo hello [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="678e9-195">You can review hello status of hello different **quotas** and **metrics** affecting an application in hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="678e9-196">![][quotas]
**Cotas** podem ser encontradas em Configurações >**Cotas**.</span><span class="sxs-lookup"><span data-stu-id="678e9-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="678e9-197">Olá UX permite que você examine: nome de cotas de saudação (1), (2) o intervalo de redefinição, (3) o limite atual e o valor atual (4).</span><span class="sxs-lookup"><span data-stu-id="678e9-197">hello UX allows you to review: (1) hello quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="678e9-198">![][metrics]
**Métricas** pode ser acessado diretamente na folha de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="678e9-198">![][metrics]
**Metrics** can be access directly from hello resource blade.</span></span> <span data-ttu-id="678e9-199">Você também pode personalizar o gráfico do hello: (1) **clique** nele e selecione (2) **Editar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="678e9-199">You can also customize hello chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="678e9-200">Aqui você pode alterar hello (3) **intervalo de tempo**, (4) **tipo de gráfico**e (5) **métricas** toodisplay.</span><span class="sxs-lookup"><span data-stu-id="678e9-200">From here you can change hello (3) **time range**, (4) **chart type**, and (5) **metrics** toodisplay.</span></span>  

<span data-ttu-id="678e9-201">Saiba mais sobre métricas aqui: [Monitorar as métricas do serviço](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="678e9-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="678e9-202">Alertas e dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="678e9-202">Alerts and Autoscale</span></span>
<span data-ttu-id="678e9-203">Métricas para um plano de aplicativo ou serviço de aplicativo pode ser vinculado tooalerts, toolearn mais sobre isso, consulte [receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="678e9-203">Metrics for an App or App Service plan can be hooked up tooalerts, toolearn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="678e9-204">Aplicativos do Serviço de Aplicativo hospedados em Planos do Serviço de Aplicativo Básico, Standard ou Premium oferecem suporte ao **Dimensionamento Automático**.</span><span class="sxs-lookup"><span data-stu-id="678e9-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="678e9-205">Isso permite que você regras tooconfigure que monitorar as métricas de plano de serviço de aplicativo e podem aumentar ou diminuir a contagem de instância Olá fornecer recursos adicionais conforme necessário, ou salvando money quando o aplicativo hello excesso de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="678e9-205">This allows you tooconfigure rules that monitor the App Service plan metrics and can increase or decrease hello instance count providing additional resources as needed, or saving money when hello application is over-provision.</span></span> <span data-ttu-id="678e9-206">Você pode aprender mais sobre AutoEscala aqui: [como tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) e aqui [as práticas recomendadas para dimensionamento automático do Monitor do Azure](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="678e9-206">You can learn more about auto scale here: [How tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="678e9-207">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="678e9-207">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="678e9-208">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="678e9-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="678e9-209">O que mudou</span><span class="sxs-lookup"><span data-stu-id="678e9-209">What's changed</span></span>
* <span data-ttu-id="678e9-210">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="678e9-210">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
