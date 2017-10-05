---
title: "Suporte do Application Insights do Azure para vários componentes, microsserviços e contêineres | Microsoft Docs"
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
ms.openlocfilehash: ca1bb8ee886c4b4e69be9dd653d6a52b874e1f5a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="c8d76-103">Monitore aplicativos de vários componentes com o Application Insights (visualização)</span><span class="sxs-lookup"><span data-stu-id="c8d76-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="c8d76-104">Você pode monitorar aplicativos que consistem em vários componentes, funções ou serviços de servidor com [Application Insights do Azure](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c8d76-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="c8d76-105">A integridade dos componentes e as relações entre eles são exibidas em um mapa de aplicativo único.</span><span class="sxs-lookup"><span data-stu-id="c8d76-105">The health of the components and the relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="c8d76-106">Você pode rastrear a operações individuais por meio de vários componentes com correlação automática de HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8d76-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="c8d76-107">Os diagnósticos do contêiner podem ser integrados e correlacionados à telemetria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="c8d76-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="c8d76-108">Use um único recurso do Application Insights para todos os componentes do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c8d76-108">Use a single Application Insights resource for all the components of your application.</span></span> 

![Mapa de aplicativos de vários componentes](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="c8d76-110">Usamos 'componente' aqui para indicar qualquer parte funcional de um aplicativo grande.</span><span class="sxs-lookup"><span data-stu-id="c8d76-110">We use 'component' here to mean any functioning part of a large application.</span></span> <span data-ttu-id="c8d76-111">Por exemplo, um aplicativo de negócios típico pode consistir em código do cliente em execução em navegadores da Web, conversando com um ou mais serviços de aplicativos Web, que, por sua vez, usam serviços de back-end.</span><span class="sxs-lookup"><span data-stu-id="c8d76-111">For example, a typical business application may consist of client code running in web browsers, talking to one or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="c8d76-112">Os componentes de servidor podem ser hospedados no local ou na nuvem, podem ser funções da Web e de trabalho do Azure ou podem ser executados em contêineres como Docker ou Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c8d76-112">Server components may be hosted on-premises on in the cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="c8d76-113">Compartilhamento um único recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="c8d76-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="c8d76-114">A principal técnica aqui é enviar telemetria de cada componente em seu aplicativo para o mesmo recurso do Application Insights, mas usar a propriedade `cloud_RoleName` para distinguir os componentes quando necessário.</span><span class="sxs-lookup"><span data-stu-id="c8d76-114">The key technique here is to send telemetry from every component in your application to the same Application Insights resource, but use the `cloud_RoleName` property to distinguish components when necessary.</span></span> <span data-ttu-id="c8d76-115">O SDK do Application Insights adiciona a propriedade `cloud_RoleName` para a emissão dos componentes de telemetria.</span><span class="sxs-lookup"><span data-stu-id="c8d76-115">The Application Insights SDK adds the `cloud_RoleName` property to the telemetry components emit.</span></span> <span data-ttu-id="c8d76-116">Por exemplo, o SDK adicionará um nome do site ou nome de função de serviço para a propriedade `cloud_RoleName`.</span><span class="sxs-lookup"><span data-stu-id="c8d76-116">For example, the SDK will add a web site name, or service role name to the `cloud_RoleName` property.</span></span> <span data-ttu-id="c8d76-117">Você pode substituir esse valor com um telemetryinitializer.</span><span class="sxs-lookup"><span data-stu-id="c8d76-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="c8d76-118">O mapa de aplicativo usa a propriedade `cloud_RoleName` para identificar os componentes no mapa.</span><span class="sxs-lookup"><span data-stu-id="c8d76-118">The Application Map uses the `cloud_RoleName` property to identify the components on the map.</span></span>

<span data-ttu-id="c8d76-119">Para obter mais informações sobre como substituir a propriedade `cloud_RoleName` consulte [Adicionar propriedades: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="c8d76-119">For more information about how do override the `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="c8d76-120">Em alguns casos, isso pode não ser apropriado e talvez você prefira usar recursos separados para diferentes grupos de componentes.</span><span class="sxs-lookup"><span data-stu-id="c8d76-120">In some cases, this may not be appropriate, and you may prefer to use separate resources for different groups of components.</span></span> <span data-ttu-id="c8d76-121">Por exemplo, talvez seja necessário usar recursos diferentes para fins de cobranças ou gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="c8d76-121">For example, you might need to use different resources for management or billing purposes.</span></span> <span data-ttu-id="c8d76-122">O uso de recursos separados significa que você não vê todos os componentes exibidos em um mapa de aplicativo único e não pode consultar componentes na [Análise](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="c8d76-122">Using separate resources means that you don't see all the components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="c8d76-123">Você também precisa configurar os recursos separados.</span><span class="sxs-lookup"><span data-stu-id="c8d76-123">You also have to set up the separate resources.</span></span>

<span data-ttu-id="c8d76-124">Com essa limitação, vamos supor no restante desse documento que você quer enviar dados de vários componentes para um recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c8d76-124">With that caveat, we'll assume in the rest of this document that you want to send data from multiple components to one Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="c8d76-125">Configurar aplicativos de vários componentes</span><span class="sxs-lookup"><span data-stu-id="c8d76-125">Configure multi-component applications</span></span>

<span data-ttu-id="c8d76-126">Para obter um mapa de aplicativo de vários componentes, você cumprir os seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="c8d76-126">To get a multi-component application map, you need to achieve these goals:</span></span>

* <span data-ttu-id="c8d76-127">**Instalar a versão de pré-lançamento mais recente** do pacote Application Insights em cada componente do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c8d76-127">**Install the latest pre-release** Application Insights package in each component of the application.</span></span> 
* <span data-ttu-id="c8d76-128">**Compartilhar um único recurso do Application Insights** para todas as funções do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c8d76-128">**Share a single Application Insights resource** for all the components of your application.</span></span>
* <span data-ttu-id="c8d76-129">**Habilitar o mapa de aplicativo de várias funções** na folha de visualizações.</span><span class="sxs-lookup"><span data-stu-id="c8d76-129">**Enable Multi-role Application Map** in the Previews blade.</span></span>

<span data-ttu-id="c8d76-130">Configurar cada componente do aplicativo usando o método apropriado para seu tipo.</span><span class="sxs-lookup"><span data-stu-id="c8d76-130">Configure each component of your application using the appropriate method for its type.</span></span> <span data-ttu-id="c8d76-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span><span class="sxs-lookup"><span data-stu-id="c8d76-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-the-latest-pre-release-package"></a><span data-ttu-id="c8d76-132">1. Instalação do pacote de pré-lançamento mais recente</span><span class="sxs-lookup"><span data-stu-id="c8d76-132">1. Install the latest pre-release package</span></span>

<span data-ttu-id="c8d76-133">Como atualizar ou instalar os pacotes do Application Insights no projeto para cada componente de servidor.</span><span class="sxs-lookup"><span data-stu-id="c8d76-133">Update or install the Appication Insights packages in the project for each server component.</span></span> <span data-ttu-id="c8d76-134">Se você estiver usando o Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="c8d76-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="c8d76-135">Clique o botão direito do mouse no projeto e selecione **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c8d76-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="c8d76-136">Selecione **Incluir pré-lançamento**.</span><span class="sxs-lookup"><span data-stu-id="c8d76-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="c8d76-137">Se pacotes do Application Insights aparecerem nas atualizações, selecione-os.</span><span class="sxs-lookup"><span data-stu-id="c8d76-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="c8d76-138">Caso contrário, procure e instale o pacote apropriado:</span><span class="sxs-lookup"><span data-stu-id="c8d76-138">Otherwise, browse for and install the appropriate package:</span></span>
    
    * <span data-ttu-id="c8d76-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c8d76-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="c8d76-140">Microsoft.ApplicationInsights.ServiceFabric – para componentes em execução como executáveis de convidado e executando um aplicativo do Service Fabric em contêineres do Docker</span><span class="sxs-lookup"><span data-stu-id="c8d76-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="c8d76-141">Microsoft.ApplicationInsights.ServiceFabric.Native - para serviços confiáveis em aplicativos no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c8d76-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="c8d76-142">Microsoft.ApplicationInsights.Kubernetes para componentes em execução no Docker e nos Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c8d76-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="c8d76-143">2. Compartilhamento de um único recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="c8d76-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="c8d76-144">No Visual Studio, clique o botão direito do mouse em um projeto e selecione **Configurar o Application Insights** ou **Application Insights > Configuração**.</span><span class="sxs-lookup"><span data-stu-id="c8d76-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="c8d76-145">Para o primeiro projeto, use o assistente para criar um recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c8d76-145">For the first project, use the wizard to create an Application Insights resource.</span></span> <span data-ttu-id="c8d76-146">Para projetos subsequentes, selecione o mesmo recurso.</span><span class="sxs-lookup"><span data-stu-id="c8d76-146">For subsequent projects, select the same resource.</span></span>
* <span data-ttu-id="c8d76-147">Se não houver nenhum menu do Application Insights, configure manualmente:</span><span class="sxs-lookup"><span data-stu-id="c8d76-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="c8d76-148">No [Portal do Azure](https://portal,azure.com), abra o recurso do Application Insights já criado para outro componente.</span><span class="sxs-lookup"><span data-stu-id="c8d76-148">In [Azure portal](https://portal,azure.com), open the Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="c8d76-149">Na folha de Visão geral, abra a guia suspensa Essentials e copie a **Chave de instrumentação.**</span><span class="sxs-lookup"><span data-stu-id="c8d76-149">In the Overview blade, open the Essentials drop-down tab, and copy the **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="c8d76-150">No seu projeto, abra ApplicationInsights.config e insira: `<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="c8d76-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Copie a chave de instrumentação para o arquivo .config](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="c8d76-152">3. Habilitação do mapa de aplicativo de várias funções</span><span class="sxs-lookup"><span data-stu-id="c8d76-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="c8d76-153">No portal do Azure, abra o recurso do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c8d76-153">In the Azure portal, open the resource for your application.</span></span> <span data-ttu-id="c8d76-154">Na folha de visualizações, habilite o *Mapa de Aplicativo de Várias Funções*.</span><span class="sxs-lookup"><span data-stu-id="c8d76-154">In the Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="c8d76-155">4. Habilitação das métricas de Docker (opcional)</span><span class="sxs-lookup"><span data-stu-id="c8d76-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="c8d76-156">Se um componente é executado no Docker hospedado em uma VM Windows do Azure, você pode coletar métricas adicionais do contêiner.</span><span class="sxs-lookup"><span data-stu-id="c8d76-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from the container.</span></span> <span data-ttu-id="c8d76-157">Insira isso no seu arquivo de configuração de [diagnóstico do Azure](../monitoring-and-diagnostics/azure-diagnostics.md):</span><span class="sxs-lookup"><span data-stu-id="c8d76-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

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

## <a name="use-cloudrolename-to-separate-components"></a><span data-ttu-id="c8d76-158">Usar cloud_RoleName para separar componentes</span><span class="sxs-lookup"><span data-stu-id="c8d76-158">Use cloud_RoleName to separate components</span></span>

<span data-ttu-id="c8d76-159">A propriedade `cloud_RoleName` está conectada a todas as telemetrias.</span><span class="sxs-lookup"><span data-stu-id="c8d76-159">The `cloud_RoleName` property is attached to all telemetry.</span></span> <span data-ttu-id="c8d76-160">Identifica o componente (a função ou o serviço) que origina a telemetria.</span><span class="sxs-lookup"><span data-stu-id="c8d76-160">It identifies the component - the role or service - that originates the telemetry.</span></span> <span data-ttu-id="c8d76-161">(Não é igual a cloud_RoleInstance, que separa funções idênticas executadas em paralelo em vários processos do servidor ou computadores.)</span><span class="sxs-lookup"><span data-stu-id="c8d76-161">(It is not the same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="c8d76-162">No portal, você pode filtrar ou segmentar a sua telemetria usando essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="c8d76-162">In the portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="c8d76-163">Neste exemplo, a folha de falhas é filtrada para mostrar apenas as informações do serviço Web do front-end, a filtragem de falhas de back-end da API do CRM:</span><span class="sxs-lookup"><span data-stu-id="c8d76-163">In this example, the Failures blade is filtered to show just information from the front-end web service, filtering out failures from the CRM API backend:</span></span>

![Gráfico de métricas segmentado por nome de função de nuvem](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="c8d76-165">Rastrear operações entre componentes</span><span class="sxs-lookup"><span data-stu-id="c8d76-165">Trace operations between components</span></span>

<span data-ttu-id="c8d76-166">Você pode rastrear, de um componente para outro, as chamadas feitas durante o processamento de uma operação individual.</span><span class="sxs-lookup"><span data-stu-id="c8d76-166">You can trace from one component to another, the calls made while processing an individual operation.</span></span>


![Mostrar telemetria para operação](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="c8d76-168">Clique em uma lista correlacionada de telemetria para esta operação entre o servidor web de front-end e a API de back-end:</span><span class="sxs-lookup"><span data-stu-id="c8d76-168">Click through to a correlated list of telemetry for this operation across the front-end web server and the back-end API:</span></span>

![Pesquisar entre os componentes](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="c8d76-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c8d76-170">Next steps</span></span>

* [<span data-ttu-id="c8d76-171">Separação da telemetria de desenvolvimento, teste e produção</span><span class="sxs-lookup"><span data-stu-id="c8d76-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
