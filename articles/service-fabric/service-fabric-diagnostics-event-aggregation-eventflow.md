---
title: "Agregação de eventos do serviço de malha com EventFlow de aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: c0141d3ed72d835139250af3589e298fd22d8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="38613-103">Agregação e coleta de eventos usando EventFlow</span><span class="sxs-lookup"><span data-stu-id="38613-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="38613-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) pode encaminhar eventos de um nó tooone ou mais destinos de monitoramentos.</span><span class="sxs-lookup"><span data-stu-id="38613-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node tooone or more monitoring destinations.</span></span> <span data-ttu-id="38613-105">Porque ele está incluído como um pacote do NuGet em seu projeto de serviço, configuração e código EventFlow viajam com serviço hello, eliminando o problema de configuração por nó Olá mencionado anteriormente sobre o diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="38613-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with hello service, eliminating hello per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="38613-106">EventFlow é executado em seu processo de serviço e se conecta diretamente saídas toohello configurado.</span><span class="sxs-lookup"><span data-stu-id="38613-106">EventFlow runs within your service process, and connects directly toohello configured outputs.</span></span> <span data-ttu-id="38613-107">Devido à conexão direta de Olá, EventFlow funciona para o Azure, contêiner e implantações de serviço local.</span><span class="sxs-lookup"><span data-stu-id="38613-107">Because of hello direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="38613-108">Tenha cuidado se você executar EventFlow em cenários de alta densidade, como em um contêiner, pois cada pipeline EventFlow faz uma conexão externa.</span><span class="sxs-lookup"><span data-stu-id="38613-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="38613-109">Então, se você hospedar vários processos, obterá várias conexões de saída!</span><span class="sxs-lookup"><span data-stu-id="38613-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="38613-110">Isso não é uma preocupação quanto para aplicativos do Service Fabric, porque todas as réplicas de um `ServiceType` executar no hello mesmo processo, e isso limita o número de saudação de conexões de saída.</span><span class="sxs-lookup"><span data-stu-id="38613-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in hello same process, and this limits hello number of outbound connections.</span></span> <span data-ttu-id="38613-111">EventFlow também oferece filtragem de eventos, para que somente os eventos de saudação que correspondem ao filtro especificado Olá são enviados.</span><span class="sxs-lookup"><span data-stu-id="38613-111">EventFlow also offers event filtering, so that only hello events that match hello specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="38613-112">Configuração do EventFlow</span><span class="sxs-lookup"><span data-stu-id="38613-112">Setting up EventFlow</span></span>

<span data-ttu-id="38613-113">EventFlow binários estão disponíveis como um conjunto de pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="38613-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="38613-114">tooadd EventFlow tooa projeto do serviço do Service Fabric, clique com botão direito Olá no hello Gerenciador de soluções e escolha "Pacotes de gerenciar NuGet".</span><span class="sxs-lookup"><span data-stu-id="38613-114">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="38613-115">Alternar o guia de "Procurar" toohello e procure "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="38613-115">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Pacotes do EventFlow NuGet no Gerenciador de pacotes do NuGet do Visual Studio da interface do usuário](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="38613-117">Você verá uma lista de vários pacotes, rotulados como "Entradas" e "Saídas".</span><span class="sxs-lookup"><span data-stu-id="38613-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="38613-118">O EventFlow dá suporte a vários provedores de log e analisadores diferentes.</span><span class="sxs-lookup"><span data-stu-id="38613-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="38613-119">serviço de saudação hospedagem EventFlow deve incluir pacotes apropriados dependendo da origem de saudação e de destino para os logs de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="38613-119">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="38613-120">Além do pacote ServiceFabric core toohello, também é necessário pelo menos uma entrada e saída configurada.</span><span class="sxs-lookup"><span data-stu-id="38613-120">In addition toohello core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="38613-121">Para o exemplo, você pode adicionar Olá pacotes toosent EventSource eventos tooApplication informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="38613-121">For exmaple, you can add hello following packages toosent EventSource events tooApplication Insights:</span></span>

* <span data-ttu-id="38613-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource`toocapture dados de classe de EventSource do serviço hello e de EventSources padrão como *serviços do Microsoft-ServiceFabric* e *ServiceFabric-Microsoft-atores*)</span><span class="sxs-lookup"><span data-stu-id="38613-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="38613-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(vamos toosend Olá logs tooan Azure Application Insights recurso)</span><span class="sxs-lookup"><span data-stu-id="38613-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going toosend hello logs tooan Azure Application Insights resource)</span></span>
* <span data-ttu-id="38613-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(permite a inicialização do pipeline de EventFlow Olá da configuração de serviço do Service Fabric e reporta os problemas com o envio de dados de diagnóstico como relatórios de integridade da malha do serviço)</span><span class="sxs-lookup"><span data-stu-id="38613-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="38613-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource`o pacote requer tootarget de projeto de serviço de saudação do .NET Framework 4.6 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="38613-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="38613-126">Verifique se que você configurou o framework de destino apropriado Olá nas propriedades do projeto antes de instalar este pacote.</span><span class="sxs-lookup"><span data-stu-id="38613-126">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="38613-127">Depois que todos os hello pacotes estão instalados, Olá próxima etapa é tooconfigure e habilitar EventFlow no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="38613-127">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="38613-128">Configurar e habilitar a coleta de logs</span><span class="sxs-lookup"><span data-stu-id="38613-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="38613-129">pipeline de EventFlow Olá responsável pelo envio de logs de saudação é criada de uma especificação armazenada em um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="38613-129">hello EventFlow pipeline responsible for sending hello logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="38613-130">Olá `Microsoft.Diagnostics.EventFlow.ServiceFabric` pacote instala um arquivo de configuração inicial do EventFlow em `PackageRoot\Config` pasta de solução, chamada `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="38613-130">hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="38613-131">Esse arquivo de configuração precisa toobe modificado toocapture dados do serviço de padrão de saudação `EventSource` classe e outras entradas tooconfigure e enviar dados toohello apropriado local.</span><span class="sxs-lookup"><span data-stu-id="38613-131">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class, and any other inputs you want tooconfigure, and send data toohello appropriate place.</span></span>

<span data-ttu-id="38613-132">Aqui está um exemplo *eventFlowConfig.json* com base em pacotes do NuGet Olá mencionados acima:</span><span class="sxs-lookup"><span data-stu-id="38613-132">Here is a sample *eventFlowConfig.json* based on hello NuGet packages mentioned above:</span></span>
```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace hello following value with your service's ServiceEventSource name)
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
      // (replace hello following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

<span data-ttu-id="38613-133">nome de saudação do ServiceEventSource do serviço é o valor de saudação do hello propriedade Name de saudação `EventSourceAttribute` aplicada toohello ServiceEventSource classe.</span><span class="sxs-lookup"><span data-stu-id="38613-133">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="38613-134">Ele é especificado em Olá `ServiceEventSource.cs` arquivo, que faz parte do código de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="38613-134">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="38613-135">Por exemplo, em Olá seguir Olá nome do trecho de saudação ServiceEventSource é *MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="38613-135">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="38613-136">Observe que o arquivo `eventFlowConfig.json` faz parte do pacote de configuração de serviço.</span><span class="sxs-lookup"><span data-stu-id="38613-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="38613-137">Arquivo de toothis de alterações pode ser incluído no completo ou configuração-somente atualizações de serviço hello, assunto tooService malha atualização verificações de integridade e reversão automática se houver falha na atualização.</span><span class="sxs-lookup"><span data-stu-id="38613-137">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="38613-138">Para saber mais, confira [Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="38613-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="38613-139">Olá *filtros* seção de configuração de saudação permite que você toofurther personalizar informações Olá contínuo toogo por meio de saudação EventFlow pipeline toohello saídas, permitindo que você toodrop incluir determinadas informações ou alterar Olá estrutura de dados de evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="38613-139">hello *filters* section of hello config allows you toofurther customize hello information that is going toogo through hello EventFlow pipeline toohello outputs, allowing you toodrop or include certain information, or change hello structure of hello event data.</span></span> <span data-ttu-id="38613-140">Para saber mais sobre filtragem, confira [Filtros EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).</span><span class="sxs-lookup"><span data-stu-id="38613-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="38613-141">Olá última etapa é o pipeline de EventFlow tooinstantiate no código de inicialização do serviço, localizado em `Program.cs` arquivo:</span><span class="sxs-lookup"><span data-stu-id="38613-141">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

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
        /// This is hello entry point of hello service host process.
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

<span data-ttu-id="38613-142">nome Hello passado como parâmetro de saudação do hello `CreatePipeline` método hello `ServiceFabricDiagnosticsPipelineFactory` é nome de saudação do hello *entidade integridade* que representa o pipeline de coleta de log Olá EventFlow.</span><span class="sxs-lookup"><span data-stu-id="38613-142">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="38613-143">Esse nome é usado se encontrar EventFlow e erro e reporta isso por meio de saudação subsistema de integridade da malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="38613-143">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a><span data-ttu-id="38613-144">Usando as configurações de malha do serviço e aplicativo parâmetros tooin eventFlowConfig</span><span class="sxs-lookup"><span data-stu-id="38613-144">Using Service Fabric settings and application parameters tooin eventFlowConfig</span></span>

<span data-ttu-id="38613-145">EventFlow oferece suporte a configurações de malha do serviço e aplicativo incorretos tooconfigure EventFlow.</span><span class="sxs-lookup"><span data-stu-id="38613-145">EventFlow supports using Service Fabric settings and application paremeters tooconfigure EventFlow settings.</span></span> <span data-ttu-id="38613-146">Você pode consultar os parâmetros de configuração de malha tooService usando essa sintaxe especial para valores:</span><span class="sxs-lookup"><span data-stu-id="38613-146">You can refer tooService Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="38613-147">`<section-name>`é o nome de saudação de saudação seção de configuração de malha do serviço, e `<setting-name>` é a configuração Olá fornecendo valor Olá que serão usada tooconfigure uma configuração de EventFlow.</span><span class="sxs-lookup"><span data-stu-id="38613-147">`<section-name>` is hello name of hello Service Fabric configuration section, and `<setting-name>` is hello configuration setting providing hello value that will be used tooconfigure an EventFlow setting.</span></span> <span data-ttu-id="38613-148">tooread mais informações sobre como toodo, ir muito[suporte para parâmetros de aplicativos e configurações do Service Fabric](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span><span class="sxs-lookup"><span data-stu-id="38613-148">tooread more about how toodo this, go too[Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="38613-149">Verificação</span><span class="sxs-lookup"><span data-stu-id="38613-149">Verification</span></span>

<span data-ttu-id="38613-150">Iniciar o serviço e observar Olá depuração janela de saída no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38613-150">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="38613-151">Depois de iniciado o serviço hello, você deve começar a ver evidências de que o serviço está enviando registros de saída toohello que você configurou.</span><span class="sxs-lookup"><span data-stu-id="38613-151">After hello service is started, you should start seeing evidence that your service is sending records toohello output that you have configured.</span></span> <span data-ttu-id="38613-152">Navegue tooyour plataforma de análise e à visualização do evento e confirme se os logs foram iniciados tooshow up (pode levar alguns minutos).</span><span class="sxs-lookup"><span data-stu-id="38613-152">Navigate tooyour event analysis and visualization platform and confirm that logs have started tooshow up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="38613-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="38613-153">Next steps</span></span>

* [<span data-ttu-id="38613-154">Visualização e Análise de Eventos com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="38613-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="38613-155">Visualização com o OMS e Análise de Eventos</span><span class="sxs-lookup"><span data-stu-id="38613-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="38613-156">Documentação de EventFlow</span><span class="sxs-lookup"><span data-stu-id="38613-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)