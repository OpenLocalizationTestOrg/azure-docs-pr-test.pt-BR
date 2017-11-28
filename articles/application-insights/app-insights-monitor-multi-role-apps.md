---
title: "aaaAzure Application Insights oferecem suporte para vários componentes, microservices e contêineres | Microsoft Docs"
description: "Monitoramento de aplicativos que consistem em vários componentes ou funções para desempenho e uso."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="a8cd1-103">Monitore aplicativos de vários componentes com o Application Insights (visualização)</span><span class="sxs-lookup"><span data-stu-id="a8cd1-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="a8cd1-104">Você pode monitorar aplicativos que consistem em vários componentes, funções ou serviços de servidor com [Application Insights do Azure](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8cd1-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="a8cd1-105">integridade de saudação de componentes de saudação e relações de saudação entre eles são exibidos em um mapa de aplicativo único.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-105">hello health of hello components and hello relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="a8cd1-106">Você pode rastrear a operações individuais por meio de vários componentes com correlação automática de HTTP.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="a8cd1-107">Os diagnósticos do contêiner podem ser integrados e correlacionados à telemetria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="a8cd1-108">Use um único recurso do Application Insights para todos os componentes de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-108">Use a single Application Insights resource for all hello components of your application.</span></span> 

![Mapa de aplicativos de vários componentes](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="a8cd1-110">Podemos usar 'componente' toomean aqui qualquer parte do funcionamento de um aplicativo grande.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-110">We use 'component' here toomean any functioning part of a large application.</span></span> <span data-ttu-id="a8cd1-111">Por exemplo, um aplicativo comercial comum pode consistir em código de cliente em execução em navegadores da web, falando tooone ou mais serviços de aplicativo web, que por sua vez usam novamente terminar serviços.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-111">For example, a typical business application may consist of client code running in web browsers, talking tooone or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="a8cd1-112">Componentes de servidor podem ser hospedado no local na nuvem hello, ou podem ser funções da web e de trabalho do Azure ou podem ser executado em contêineres como Docker ou do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-112">Server components may be hosted on-premises on in hello cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="a8cd1-113">Compartilhamento um único recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="a8cd1-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="a8cd1-114">Olá, técnica chave aqui é toosend telemetria de cada componente em seu aplicativo toohello mesmo recurso Application Insights, mas use Olá `cloud_RoleName` componentes toodistinguish de propriedade quando necessário.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-114">hello key technique here is toosend telemetry from every component in your application toohello same Application Insights resource, but use hello `cloud_RoleName` property toodistinguish components when necessary.</span></span> <span data-ttu-id="a8cd1-115">Olá SDK do Application Insights adiciona Olá `cloud_RoleName` componentes de telemetria toohello propriedade emitir.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-115">hello Application Insights SDK adds hello `cloud_RoleName` property toohello telemetry components emit.</span></span> <span data-ttu-id="a8cd1-116">Por exemplo, a saudação SDK adicionará um nome de site da web ou serviço toohello de nome de função `cloud_RoleName` propriedade.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-116">For example, hello SDK will add a web site name, or service role name toohello `cloud_RoleName` property.</span></span> <span data-ttu-id="a8cd1-117">Você pode substituir esse valor com um telemetryinitializer.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="a8cd1-118">Olá mapa de aplicativo usa Olá `cloud_RoleName` componentes de saudação propriedade tooidentify no mapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-118">hello Application Map uses hello `cloud_RoleName` property tooidentify hello components on hello map.</span></span>

<span data-ttu-id="a8cd1-119">Para obter mais informações sobre como substituir Olá `cloud_RoleName` consulte propriedade [adicionar propriedades: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="a8cd1-119">For more information about how do override hello `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="a8cd1-120">Em alguns casos, isso pode não ser apropriado e, talvez você prefira toouse de recursos separados para diferentes grupos de componentes.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-120">In some cases, this may not be appropriate, and you may prefer toouse separate resources for different groups of components.</span></span> <span data-ttu-id="a8cd1-121">Por exemplo, talvez seja necessário toouse diferentes recursos de gerenciamento ou fins de cobrança.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-121">For example, you might need toouse different resources for management or billing purposes.</span></span> <span data-ttu-id="a8cd1-122">Usar recursos separados significa que você não vir todos os componentes de saudação exibidos em um mapa de aplicativo único; e se você não pode consultar em componentes [análise](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="a8cd1-122">Using separate resources means that you don't see all hello components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="a8cd1-123">Você também tem tooset recursos separados de saudação.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-123">You also have tooset up hello separate resources.</span></span>

<span data-ttu-id="a8cd1-124">Com essa limitação, vamos supor que no restante deste documento hello que você deseja toosend dados de recurso do Application Insights tooone de vários componentes.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-124">With that caveat, we'll assume in hello rest of this document that you want toosend data from multiple components tooone Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="a8cd1-125">Configurar aplicativos de vários componentes</span><span class="sxs-lookup"><span data-stu-id="a8cd1-125">Configure multi-component applications</span></span>

<span data-ttu-id="a8cd1-126">mapa de um aplicativo de vários componente tooget, é necessário tooachieve essas metas:</span><span class="sxs-lookup"><span data-stu-id="a8cd1-126">tooget a multi-component application map, you need tooachieve these goals:</span></span>

* <span data-ttu-id="a8cd1-127">**Instalar a pré-versão mais recente de Olá** pacote do Application Insights em cada componente do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-127">**Install hello latest pre-release** Application Insights package in each component of hello application.</span></span> 
* <span data-ttu-id="a8cd1-128">**Compartilhar um único recurso do Application Insights** para todos os componentes do aplicativo de hello.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-128">**Share a single Application Insights resource** for all hello components of your application.</span></span>
* <span data-ttu-id="a8cd1-129">**Habilitar mapa de aplicativos de várias funções** na folha de visualizações de saudação.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-129">**Enable Multi-role Application Map** in hello Previews blade.</span></span>

<span data-ttu-id="a8cd1-130">Configure cada componente do seu aplicativo usando o método apropriado de saudação para seu tipo.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-130">Configure each component of your application using hello appropriate method for its type.</span></span> <span data-ttu-id="a8cd1-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span><span class="sxs-lookup"><span data-stu-id="a8cd1-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-hello-latest-pre-release-package"></a><span data-ttu-id="a8cd1-132">1. Instalar o pacote de pré-lançamento mais recente Olá</span><span class="sxs-lookup"><span data-stu-id="a8cd1-132">1. Install hello latest pre-release package</span></span>

<span data-ttu-id="a8cd1-133">Atualizar ou instalar pacotes do Application Insights Olá no projeto Olá para cada componente do servidor.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-133">Update or install hello Appication Insights packages in hello project for each server component.</span></span> <span data-ttu-id="a8cd1-134">Se você estiver usando o Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="a8cd1-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="a8cd1-135">Clique o botão direito do mouse no projeto e selecione **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="a8cd1-136">Selecione **Incluir pré-lançamento**.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="a8cd1-137">Se pacotes do Application Insights aparecerem nas atualizações, selecione-os.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="a8cd1-138">Caso contrário, procurar e instalar o pacote de saudação apropriado:</span><span class="sxs-lookup"><span data-stu-id="a8cd1-138">Otherwise, browse for and install hello appropriate package:</span></span>
    
    * <span data-ttu-id="a8cd1-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="a8cd1-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="a8cd1-140">Microsoft.ApplicationInsights.ServiceFabric – para componentes em execução como executáveis de convidado e executando um aplicativo do Service Fabric em contêineres do Docker</span><span class="sxs-lookup"><span data-stu-id="a8cd1-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="a8cd1-141">Microsoft.ApplicationInsights.ServiceFabric.Native - para serviços confiáveis em aplicativos no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a8cd1-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="a8cd1-142">Microsoft.ApplicationInsights.Kubernetes para componentes em execução no Docker e nos Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a8cd1-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="a8cd1-143">2. Compartilhamento de um único recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="a8cd1-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="a8cd1-144">No Visual Studio, clique o botão direito do mouse em um projeto e selecione **Configurar o Application Insights** ou **Application Insights > Configuração**.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="a8cd1-145">Para o primeiro projeto de Olá, use Olá Assistente toocreate um recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-145">For hello first project, use hello wizard toocreate an Application Insights resource.</span></span> <span data-ttu-id="a8cd1-146">Para projetos subsequentes, selecione Olá mesmo recurso.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-146">For subsequent projects, select hello same resource.</span></span>
* <span data-ttu-id="a8cd1-147">Se não houver nenhum menu do Application Insights, configure manualmente:</span><span class="sxs-lookup"><span data-stu-id="a8cd1-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="a8cd1-148">Em [portal do Azure](https://portal,azure.com), abrir o recurso do Application Insights Olá você já criou para outro componente.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-148">In [Azure portal](https://portal,azure.com), open hello Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="a8cd1-149">Na folha de visão geral de saudação, guia Olá abrir menu suspenso do Essentials e Olá cópia **chave de instrumentação.**</span><span class="sxs-lookup"><span data-stu-id="a8cd1-149">In hello Overview blade, open hello Essentials drop-down tab, and copy hello **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="a8cd1-150">No seu projeto, abra ApplicationInsights.config e insira: `<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="a8cd1-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Copiar Olá instrumentação chave toohello. config arquivo](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="a8cd1-152">3. Habilitação do mapa de aplicativo de várias funções</span><span class="sxs-lookup"><span data-stu-id="a8cd1-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="a8cd1-153">No portal do Azure de Olá, abra o recurso de saudação para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-153">In hello Azure portal, open hello resource for your application.</span></span> <span data-ttu-id="a8cd1-154">Na folha de visualizações hello, habilitar *mapa de aplicativos de várias funções*.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-154">In hello Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="a8cd1-155">4. Habilitação das métricas de Docker (opcional)</span><span class="sxs-lookup"><span data-stu-id="a8cd1-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="a8cd1-156">Se um componente é executado em um Docker hospedado em uma VM do Windows Azure, você pode coletar métricas adicionais de contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from hello container.</span></span> <span data-ttu-id="a8cd1-157">Insira isso no seu arquivo de configuração de [diagnóstico do Azure](../monitoring-and-diagnostics/azure-diagnostics.md):</span><span class="sxs-lookup"><span data-stu-id="a8cd1-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a><span data-ttu-id="a8cd1-158">Usar cloud_RoleName tooseparate componentes</span><span class="sxs-lookup"><span data-stu-id="a8cd1-158">Use cloud_RoleName tooseparate components</span></span>

<span data-ttu-id="a8cd1-159">Olá `cloud_RoleName` propriedade é telemetria tooall anexado.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-159">hello `cloud_RoleName` property is attached tooall telemetry.</span></span> <span data-ttu-id="a8cd1-160">Ele identifica o componente de saudação - Olá função ou um serviço - que se origina a telemetria de saudação.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-160">It identifies hello component - hello role or service - that originates hello telemetry.</span></span> <span data-ttu-id="a8cd1-161">(É não Olá mesmo como cloud_RoleInstance, que separa idênticas funções que são executados em paralelo em vários processos do servidor ou computadores.)</span><span class="sxs-lookup"><span data-stu-id="a8cd1-161">(It is not hello same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="a8cd1-162">No portal de saudação, você pode filtrar ou segmentar sua telemetria usando essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-162">In hello portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="a8cd1-163">Neste exemplo, folha de falhas de saudação é filtrado tooshow apenas informações do serviço de front-end web Olá, filtragem de falhas de back-end de API do CRM Olá:</span><span class="sxs-lookup"><span data-stu-id="a8cd1-163">In this example, hello Failures blade is filtered tooshow just information from hello front-end web service, filtering out failures from hello CRM API backend:</span></span>

![Gráfico de métricas segmentado por nome de função de nuvem](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="a8cd1-165">Rastrear operações entre componentes</span><span class="sxs-lookup"><span data-stu-id="a8cd1-165">Trace operations between components</span></span>

<span data-ttu-id="a8cd1-166">Você pode rastrear a partir de um componente tooanother, chamadas de saudação feitas durante o processamento de uma operação individual.</span><span class="sxs-lookup"><span data-stu-id="a8cd1-166">You can trace from one component tooanother, hello calls made while processing an individual operation.</span></span>


![Mostrar telemetria para operação](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="a8cd1-168">Clique em lista correlacionados de tooa de telemetria para esta operação no servidor de front-end web hello e na API de back-end de saudação:</span><span class="sxs-lookup"><span data-stu-id="a8cd1-168">Click through tooa correlated list of telemetry for this operation across hello front-end web server and hello back-end API:</span></span>

![Pesquisar entre os componentes](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="a8cd1-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a8cd1-170">Next steps</span></span>

* [<span data-ttu-id="a8cd1-171">Separação da telemetria de desenvolvimento, teste e produção</span><span class="sxs-lookup"><span data-stu-id="a8cd1-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
