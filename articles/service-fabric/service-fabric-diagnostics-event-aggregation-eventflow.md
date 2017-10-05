---
title: "Agregação de Eventos do Service Fabric do Azure com EventFlow | Microsoft Docs"
description: "Saiba mais sobre a agregação e a coleta de eventos utilizando EventFlow para monitoramento e diagnóstico de clusters do Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 90d26a77b749e70de3a7d910f15820653e2ef39b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="1ea83-103">Agregação e coleta de eventos usando EventFlow</span><span class="sxs-lookup"><span data-stu-id="1ea83-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="1ea83-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) pode encaminhar eventos de um nó a um ou mais destinos de monitoramentos.</span><span class="sxs-lookup"><span data-stu-id="1ea83-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node to one or more monitoring destinations.</span></span> <span data-ttu-id="1ea83-105">Como ele está incluído como um pacote NuGet em seu projeto de serviço, o código e a configuração do EventFlow viajam com o serviço, eliminando o problema de configuração por nó mencionado anteriormente sobre o Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ea83-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with the service, eliminating the per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="1ea83-106">O EventFlow é executado em seu processo de serviço e conecta-se diretamente às saídas configuradas.</span><span class="sxs-lookup"><span data-stu-id="1ea83-106">EventFlow runs within your service process, and connects directly to the configured outputs.</span></span> <span data-ttu-id="1ea83-107">Devido a essa conexão direta, o EventFlow funciona para o Azure, o contêiner e as implantações de serviço locais.</span><span class="sxs-lookup"><span data-stu-id="1ea83-107">Because of the direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="1ea83-108">Tenha cuidado se você executar EventFlow em cenários de alta densidade, como em um contêiner, pois cada pipeline EventFlow faz uma conexão externa.</span><span class="sxs-lookup"><span data-stu-id="1ea83-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="1ea83-109">Então, se você hospedar vários processos, obterá várias conexões de saída!</span><span class="sxs-lookup"><span data-stu-id="1ea83-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="1ea83-110">Isso não é tanto uma preocupação para aplicativos de Service Fabric, porque todas as réplicas de um `ServiceType` são executadas no mesmo processo e isso limita o número de conexões de saída.</span><span class="sxs-lookup"><span data-stu-id="1ea83-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in the same process, and this limits the number of outbound connections.</span></span> <span data-ttu-id="1ea83-111">O EventFlow também oferece a filtragem de eventos e, portanto, somente os eventos que correspondem ao filtro especificado são enviadas.</span><span class="sxs-lookup"><span data-stu-id="1ea83-111">EventFlow also offers event filtering, so that only the events that match the specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="1ea83-112">Configuração do EventFlow</span><span class="sxs-lookup"><span data-stu-id="1ea83-112">Setting up EventFlow</span></span>

<span data-ttu-id="1ea83-113">EventFlow binários estão disponíveis como um conjunto de pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="1ea83-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="1ea83-114">Para adicionar EventFlow a um projeto de serviço do Service Fabric, clique com botão direito do mouse no projeto no Gerenciador de Soluções e escolha "Gerenciar pacotes NuGet."</span><span class="sxs-lookup"><span data-stu-id="1ea83-114">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="1ea83-115">Alternar para a guia "Procurar" e pesquise por "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="1ea83-115">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Pacotes do EventFlow NuGet no Gerenciador de pacotes do NuGet do Visual Studio da interface do usuário](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="1ea83-117">Você verá uma lista de vários pacotes, rotulados como "Entradas" e "Saídas".</span><span class="sxs-lookup"><span data-stu-id="1ea83-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="1ea83-118">O EventFlow dá suporte a vários provedores de log e analisadores diferentes.</span><span class="sxs-lookup"><span data-stu-id="1ea83-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="1ea83-119">O serviço que hospeda EventFlow deve incluir pacotes apropriados dependendo da origem e destino para os logs de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ea83-119">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="1ea83-120">Além do pacote principal do Service Fabric, você também precisa de pelo menos uma Entrada e Saída configuradas.</span><span class="sxs-lookup"><span data-stu-id="1ea83-120">In addition to the core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="1ea83-121">Por exemplo, você pode adicionar os seguintes pacotes para eventos EventSource enviados ao Application Insights:</span><span class="sxs-lookup"><span data-stu-id="1ea83-121">For exmaple, you can add the following packages to sent EventSource events to Application Insights:</span></span>

* <span data-ttu-id="1ea83-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` para capturar dados de classe do EventSource do serviço e de EventSources padrão como *Microsoft-ServiceFabric-Services* e *Microsoft-ServiceFabric-Actors*)</span><span class="sxs-lookup"><span data-stu-id="1ea83-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="1ea83-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (vamos enviar os logs para um recurso do Azure Application Insights)</span><span class="sxs-lookup"><span data-stu-id="1ea83-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going to send the logs to an Azure Application Insights resource)</span></span>
* <span data-ttu-id="1ea83-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(habilita a inicialização do pipeline EventFlow da configuração do serviço Service Fabric e relata quaisquer problemas com o envio de dados de diagnóstico como relatórios de integridade do Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="1ea83-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="1ea83-125">O pacote `Microsoft.Diagnostics.EventFlow.Input.EventSource` requer que o projeto de serviço tenha como destino o .NET Framework 4.6 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="1ea83-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="1ea83-126">Certifique-se de que definir a estrutura de destino apropriada nas propriedades do projeto antes de instalar este pacote.</span><span class="sxs-lookup"><span data-stu-id="1ea83-126">Make sure you set the appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="1ea83-127">Depois que todos os pacotes são instalados, a próxima etapa é configurar e habilitar EventFlow no serviço.</span><span class="sxs-lookup"><span data-stu-id="1ea83-127">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="1ea83-128">Configurar e habilitar a coleta de logs</span><span class="sxs-lookup"><span data-stu-id="1ea83-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="1ea83-129">O pipeline de EventFlow, responsável pelo envio de logs, é criado de uma especificação armazenada em um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="1ea83-129">The EventFlow pipeline responsible for sending the logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="1ea83-130">O `Microsoft.Diagnostics.EventFlow.ServiceFabric`pacote instala um arquivo de configuração inicial do EventFlow em `PackageRoot\Config` pasta da solução, chamada `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="1ea83-130">The `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="1ea83-131">Esse arquivo de configuração precisa ser modificado para capturar dados da classe `EventSource` do serviço padrão e quaisquer outras entradas que você deseja configurar, bem como enviar dados ao local apropriado.</span><span class="sxs-lookup"><span data-stu-id="1ea83-131">This configuration file needs to be modified to capture data from the default service `EventSource` class, and any other inputs you want to configure, and send data to the appropriate place.</span></span>

<span data-ttu-id="1ea83-132">Aqui está um *eventFlowConfig.json* de exemplo com base nos pacotes NuGet mencionados acima:</span><span class="sxs-lookup"><span data-stu-id="1ea83-132">Here is a sample *eventFlowConfig.json* based on the NuGet packages mentioned above:</span></span>
```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace the following value with your service's ServiceEventSource name)
        { "providerName": "your-service-EventSource-name" }
      ]
    }
  ],
  "filters": [
    {
      "type": "drop",
      "include": "Level == Verbose"
    }
  ],
  "outputs": [
    {
      "type": "ApplicationInsights",
      // (replace the following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

<span data-ttu-id="1ea83-133">O nome da ServiceEventSource do serviço é o valor da propriedade Nome do `EventSourceAttribute` aplicado à classe ServiceEventSource.</span><span class="sxs-lookup"><span data-stu-id="1ea83-133">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="1ea83-134">Isso é especificado no arquivo `ServiceEventSource.cs`, que faz parte do código do serviço.</span><span class="sxs-lookup"><span data-stu-id="1ea83-134">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="1ea83-135">Por exemplo, no trecho de código a seguir, o nome do ServiceEventSource é *MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="1ea83-135">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="1ea83-136">Observe que o arquivo `eventFlowConfig.json` faz parte do pacote de configuração de serviço.</span><span class="sxs-lookup"><span data-stu-id="1ea83-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="1ea83-137">As alterações feitas neste arquivo podem ser incluídas em atualizações completo - ou apenas da configuração do serviço, sujeito a verificações de integridade de atualização do Service Fabric e a reversão automática se houver falha na atualização.</span><span class="sxs-lookup"><span data-stu-id="1ea83-137">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="1ea83-138">Para saber mais, confira [Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="1ea83-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="1ea83-139">A seção *Filtros* da configuração permite que você personalize as informações que passarão pelo pipeline EventFlow para as saídas, permitindo que você descarte ou inclua determinadas informações ou altere ainda mais a estrutura dos dados do evento.</span><span class="sxs-lookup"><span data-stu-id="1ea83-139">The *filters* section of the config allows you to further customize the information that is going to go through the EventFlow pipeline to the outputs, allowing you to drop or include certain information, or change the structure of the event data.</span></span> <span data-ttu-id="1ea83-140">Para saber mais sobre filtragem, confira [Filtros EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).</span><span class="sxs-lookup"><span data-stu-id="1ea83-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="1ea83-141">A etapa final é criar uma instância de pipeline de EventFlow no código de inicialização do serviço, localizado no arquivo `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="1ea83-141">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric;
using Microsoft.ServiceFabric.Services.Runtime;

// **** EventFlow namespace
using Microsoft.Diagnostics.EventFlow.ServiceFabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is the entry point of the service host process.
        /// </summary>
        private static void Main()
        {
            try
            {
                // **** Instantiate log collection via EventFlow
                using (var diagnosticsPipeline = ServiceFabricDiagnosticPipelineFactory.CreatePipeline("MyApplication-MyService-DiagnosticsPipeline"))
                {

                    ServiceRuntime.RegisterServiceAsync("Stateless1Type",
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                    ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                    Thread.Sleep(Timeout.Infinite);
                }
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
                throw;
            }
        }
    }
}
```

<span data-ttu-id="1ea83-142">O nome passado como o parâmetro do método `CreatePipeline` do `ServiceFabricDiagnosticsPipelineFactory` é o nome da *entidade de integridade* que representa o pipeline de coleta de logs de EventFlow.</span><span class="sxs-lookup"><span data-stu-id="1ea83-142">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="1ea83-143">Esse nome será usado se EventFlow encontrar um erro e o reportar por meio do subsistema de integridade do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1ea83-143">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-to-in-eventflowconfig"></a><span data-ttu-id="1ea83-144">Usando configurações do Service Fabric e parâmetros de aplicativo em eventFlowConfig</span><span class="sxs-lookup"><span data-stu-id="1ea83-144">Using Service Fabric settings and application parameters to in eventFlowConfig</span></span>

<span data-ttu-id="1ea83-145">O EventFlow dá suporte ao uso de configurações do Service Fabric e parâmetros de aplicativo para definir configurações de EventFlow.</span><span class="sxs-lookup"><span data-stu-id="1ea83-145">EventFlow supports using Service Fabric settings and application paremeters to configure EventFlow settings.</span></span> <span data-ttu-id="1ea83-146">Você pode se referir aos parâmetros de configuração do Service Fabric usando essa sintaxe especial para valores:</span><span class="sxs-lookup"><span data-stu-id="1ea83-146">You can refer to Service Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="1ea83-147">`<section-name>` é o nome da seção de configuração do Service Fabric e `<setting-name>` é a configuração que fornece o valor que será usado para definir uma configuração de EventFlow.</span><span class="sxs-lookup"><span data-stu-id="1ea83-147">`<section-name>` is the name of the Service Fabric configuration section, and `<setting-name>` is the configuration setting providing the value that will be used to configure an EventFlow setting.</span></span> <span data-ttu-id="1ea83-148">Para ler mais sobre como fazer isso, acesse o [Suporte para parâmetros de aplicativo e configurações do Service Fabric](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span><span class="sxs-lookup"><span data-stu-id="1ea83-148">To read more about how to do this, go to [Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="1ea83-149">Verificação</span><span class="sxs-lookup"><span data-stu-id="1ea83-149">Verification</span></span>

<span data-ttu-id="1ea83-150">Inicie o serviço e observe a depuração janela saída no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ea83-150">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="1ea83-151">Depois que o serviço é iniciado, você deve começar a ver evidências de que ele está enviando registros para a saída que você configurou.</span><span class="sxs-lookup"><span data-stu-id="1ea83-151">After the service is started, you should start seeing evidence that your service is sending records to the output that you have configured.</span></span> <span data-ttu-id="1ea83-152">Navegue até a plataforma de análise e visualização de eventos e confirme se os logs começaram a ser mostrados (isso pode levar alguns minutos).</span><span class="sxs-lookup"><span data-stu-id="1ea83-152">Navigate to your event analysis and visualization platform and confirm that logs have started to show up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ea83-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1ea83-153">Next steps</span></span>

* [<span data-ttu-id="1ea83-154">Visualização e Análise de Eventos com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="1ea83-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="1ea83-155">Visualização com o OMS e Análise de Eventos</span><span class="sxs-lookup"><span data-stu-id="1ea83-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="1ea83-156">Documentação de EventFlow</span><span class="sxs-lookup"><span data-stu-id="1ea83-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)