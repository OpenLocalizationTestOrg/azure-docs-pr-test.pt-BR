---
title: "Coletar logs diretamente de um processo de serviço do Azure Service Fabric | Microsoft Azure"
description: "Descreve como os aplicativos do Service Fabric podem enviar logs diretamente para um local central, como o Azure Application Insights ou o Elasticsearch, sem depender de agentes do Diagnóstico do Azure."
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: rwike77
editor: 
ms.assetid: ab92c99b-1edd-4677-8c28-4e591d909b47
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/18/2017
ms.author: karolz
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: b7d2541928f4248750417a77d99033c8b4354dcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="219f9-103">Coletar logs diretamente de um processo do serviço Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="219f9-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="219f9-104">Coleta de logs no processo</span><span class="sxs-lookup"><span data-stu-id="219f9-104">In-process log collection</span></span>
<span data-ttu-id="219f9-105">Coletar logs de aplicativo usando a [extensão do Diagnóstico do Azure](service-fabric-diagnostics-how-to-setup-wad.md) será uma boa opção para serviços do **Azure Service Fabric** se o conjunto de origens e destinos de log for pequeno, não forem alterados com frequência e se houver um mapeamento direto entre as origens e seus destinos.</span><span class="sxs-lookup"><span data-stu-id="219f9-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if the set of log sources and destinations is small, does not change often, and there is a straightforward mapping between the sources and their destinations.</span></span> <span data-ttu-id="219f9-106">Caso contrário, uma alternativa é fazer com que os serviços enviem seus logs diretamente para um local central.</span><span class="sxs-lookup"><span data-stu-id="219f9-106">If not, an alternative is to have services send their logs directly to a central location.</span></span> <span data-ttu-id="219f9-107">Esse processo é conhecido como **coleta de logs no processo** e tem várias vantagens potenciais:</span><span class="sxs-lookup"><span data-stu-id="219f9-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="219f9-108">*Fácil Configuração e implantação*</span><span class="sxs-lookup"><span data-stu-id="219f9-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="219f9-109">A configuração de coleta de dados de diagnóstico é apenas uma parte da configuração do serviço.</span><span class="sxs-lookup"><span data-stu-id="219f9-109">The configuration of diagnostic data collection is just part of the service configuration.</span></span> <span data-ttu-id="219f9-110">É fácil sempre mantê-la "sincronizada" com o restante do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="219f9-110">It is easy to always keep it "in sync" with the rest of the application.</span></span>
    * <span data-ttu-id="219f9-111">A configuração por aplicativo ou por serviço é facilmente realizável.</span><span class="sxs-lookup"><span data-stu-id="219f9-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="219f9-112">A coleta de logs baseada em agentes normalmente requer a implantação e a configuração separadas do agente de diagnóstico, que é uma tarefa administrativa extra e uma possível fonte de erros.</span><span class="sxs-lookup"><span data-stu-id="219f9-112">Agent-based log collection usually requires a separate deployment and configuration of the diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="219f9-113">Geralmente, há apenas uma instância do agente permitido por máquina virtual (nó) e a configuração do agente é compartilhada entre todos os aplicativos e serviços em execução nesse nó.</span><span class="sxs-lookup"><span data-stu-id="219f9-113">Often there is only one instance of the agent allowed per virtual machine (node) and the agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="219f9-114">*Flexibilidade*</span><span class="sxs-lookup"><span data-stu-id="219f9-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="219f9-115">O aplicativo pode enviar os dados sempre que eles forem necessários, desde que exista uma biblioteca de cliente que ofereça suporte ao sistema de armazenamento de dados de destino.</span><span class="sxs-lookup"><span data-stu-id="219f9-115">The application can send the data wherever it needs to go, as long as there is a client library that supports the targeted data storage system.</span></span> <span data-ttu-id="219f9-116">Novos destinos podem ser adicionados conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="219f9-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="219f9-117">Regras de captura complexa, filtragem e agregação de dados podem ser implementadas.</span><span class="sxs-lookup"><span data-stu-id="219f9-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="219f9-118">Coleta de log do agente geralmente é limitada pelos Coletores de dados que suporta o agente.</span><span class="sxs-lookup"><span data-stu-id="219f9-118">Agent-based log collection is often limited by the data sinks that the agent supports.</span></span> <span data-ttu-id="219f9-119">Alguns agentes são extensíveis.</span><span class="sxs-lookup"><span data-stu-id="219f9-119">Some agents are extensible.</span></span>

* <span data-ttu-id="219f9-120">*Acesso a dados de aplicativos internos e contexto*</span><span class="sxs-lookup"><span data-stu-id="219f9-120">*Access to internal application data and context*</span></span>
   
    * <span data-ttu-id="219f9-121">O subsistema de diagnóstico em execução dentro do processo de serviço/do aplicativo pode facilmente aumentar os rastreamentos com informações contextuais.</span><span class="sxs-lookup"><span data-stu-id="219f9-121">The diagnostic subsystem running inside the application/service process can easily augment the traces with contextual information.</span></span>
    * <span data-ttu-id="219f9-122">Com a coleta de logs baseada em agentes, os dados devem ser enviados a um agente por meio de um mecanismo de comunicação entre processos, como Rastreamento de Eventos para Windows.</span><span class="sxs-lookup"><span data-stu-id="219f9-122">With agent-based log collection, the data must be sent to an agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="219f9-123">Esse mecanismo pode impor limitações adicionais.</span><span class="sxs-lookup"><span data-stu-id="219f9-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="219f9-124">É possível combinar e aproveitar ambos os métodos de coleta.</span><span class="sxs-lookup"><span data-stu-id="219f9-124">It is possible to combine and benefit from both collection methods.</span></span> <span data-ttu-id="219f9-125">Na verdade, essa pode ser a melhor solução para muitos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="219f9-125">Indeed, it might be the best solution for many applications.</span></span> <span data-ttu-id="219f9-126">Coleção com base em agente é uma solução natural para coletar logs relacionados para o cluster inteiro e nós de cluster individuais.</span><span class="sxs-lookup"><span data-stu-id="219f9-126">Agent-based collection is a natural solution for collecting logs related to the whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="219f9-127">Ele é muito mais confiável maneira, que coleta de log em processo para diagnosticar problemas de inicialização do serviço e falhas.</span><span class="sxs-lookup"><span data-stu-id="219f9-127">It is much more reliable way, than in-process log collection, to diagnose service startup problems and crashes.</span></span> <span data-ttu-id="219f9-128">Além disso, com vários serviços em execução dentro de um cluster de Service Fabric, cada serviço fazer sua própria coleção de log em processo resulta em várias conexões de saída do cluster.</span><span class="sxs-lookup"><span data-stu-id="219f9-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from the cluster.</span></span> <span data-ttu-id="219f9-129">Grande número de conexões de saída é uma sobrecarga para o subsistema de rede e o destino de log.</span><span class="sxs-lookup"><span data-stu-id="219f9-129">Large number of outgoing connections is taxing both for the network subsystem and for the log destination.</span></span> <span data-ttu-id="219f9-130">Um agente como [ **diagnóstico do Azure** ](../cloud-services/cloud-services-dotnet-diagnostics.md) pode coletar dados de vários serviços e enviar dados por meio de algumas conexões, melhorando a taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="219f9-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="219f9-131">Neste artigo, mostramos como configurar uma coleção no processo log usando [ **biblioteca de código-fonte aberto EventFlow**](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="219f9-131">In this article, we show how to set up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="219f9-132">Outras bibliotecas que podem ser usadas para a mesma finalidade, mas EventFlow tem a vantagem de ter foi projetado especificamente para coleta de log em processo e para dar suporte a serviços de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="219f9-132">Other libraries might be used for the same purpose, but EventFlow has the benefit of having been designed specifically for in-process log collection and to support Service Fabric services.</span></span> <span data-ttu-id="219f9-133">Usamos [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) como o destino de log.</span><span class="sxs-lookup"><span data-stu-id="219f9-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as the log destination.</span></span> <span data-ttu-id="219f9-134">Outros destinos, como [ **Hubs de eventos** ](https://azure.microsoft.com/services/event-hubs/) ou [ **Elasticsearch** ](https://www.elastic.co/products/elasticsearch) também têm suporte.</span><span class="sxs-lookup"><span data-stu-id="219f9-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="219f9-135">É apenas uma questão de instalar o pacote do NuGet apropriado e configurando o destino no arquivo de configuração EventFlow.</span><span class="sxs-lookup"><span data-stu-id="219f9-135">It is just a question of installing appropriate NuGet package and configuring the destination in the EventFlow configuration file.</span></span> <span data-ttu-id="219f9-136">Para obter mais informações sobre destinos de log diferente do Application Insights, consulte [EventFlow documentação](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="219f9-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-to-a-service-fabric-service-project"></a><span data-ttu-id="219f9-137">Adição da biblioteca EventFlow a um projeto de serviço do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="219f9-137">Adding EventFlow library to a Service Fabric service project</span></span>
<span data-ttu-id="219f9-138">EventFlow binários estão disponíveis como um conjunto de pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="219f9-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="219f9-139">Para adicionar EventFlow a um projeto de serviço do Service Fabric, clique com botão direito do mouse no projeto no Gerenciador de Soluções e escolha "Gerenciar pacotes NuGet."</span><span class="sxs-lookup"><span data-stu-id="219f9-139">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="219f9-140">Alternar para a guia "Procurar" e pesquise por "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="219f9-140">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Pacotes do EventFlow NuGet no Gerenciador de pacotes do NuGet do Visual Studio da interface do usuário][1]

<span data-ttu-id="219f9-142">O serviço que hospeda EventFlow deve incluir pacotes apropriados dependendo da origem e destino para os logs de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="219f9-142">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="219f9-143">Adicione os seguintes pacotes:</span><span class="sxs-lookup"><span data-stu-id="219f9-143">Add the following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="219f9-144">(para capturar dados de classe do EventSource do serviço e de EventSources padrão como *Microsoft-ServiceFabric-Services* e *Microsoft-ServiceFabric-Actors*)</span><span class="sxs-lookup"><span data-stu-id="219f9-144">(to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="219f9-145">(vamos enviar os logs para um recurso do Azure Application Insights)</span><span class="sxs-lookup"><span data-stu-id="219f9-145">(we are going to send the logs to an Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="219f9-146">(permite a inicialização do pipeline EventFlow da configuração do serviço Service Fabric e relata quaisquer problemas com o envio de dados de diagnóstico como relatórios de integridade do Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="219f9-146">(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="219f9-147">O pacote `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` requer que o projeto de serviço tenha como destino o .NET Framework 4.6 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="219f9-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="219f9-148">Certifique-se de que definir a estrutura de destino apropriada nas propriedades do projeto antes de instalar este pacote.</span><span class="sxs-lookup"><span data-stu-id="219f9-148">Make sure you set the appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="219f9-149">Depois que todos os pacotes são instalados, a próxima etapa é configurar e habilitar EventFlow no serviço.</span><span class="sxs-lookup"><span data-stu-id="219f9-149">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="219f9-150">Configurar e habilitar a coleta de logs</span><span class="sxs-lookup"><span data-stu-id="219f9-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="219f9-151">O pipeline de EventFlow, responsável pelo envio de logs, é criado de uma especificação armazenada em um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="219f9-151">EventFlow pipeline, responsible for sending the logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="219f9-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric`pacote instala um arquivo de configuração inicial do EventFlow em `PackageRoot\Config` pasta da solução.</span><span class="sxs-lookup"><span data-stu-id="219f9-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="219f9-153">O nome do arquivo é `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="219f9-153">The file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="219f9-154">Esse arquivo de configuração precisa ser modificado para capturar dados do serviço padrão `EventSource` classe e enviar dados ao serviço Application Insights.</span><span class="sxs-lookup"><span data-stu-id="219f9-154">This configuration file needs to be modified to capture data from the default service `EventSource` class and send data to Application Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="219f9-155">Vamos supor que você esteja familiarizado com o seviço **Azure Application Insights** e que tenha um recurso Application Insights que planeja usar para monitorar seu serviço do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="219f9-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan to use to monitor your Service Fabric service.</span></span> <span data-ttu-id="219f9-156">Se você precisar de mais informações, veja [Criar um recurso do Application Insights](../application-insights/app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="219f9-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="219f9-157">Abra o `eventFlowConfig.json` no editor de arquivo e altere seu conteúdo conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="219f9-157">Open the `eventFlowConfig.json` file in the editor and change its content as shown below.</span></span> <span data-ttu-id="219f9-158">Substitua o nome da ServiceEventSource e a chave de instrumentação do Application Insights de acordo com comentários.</span><span class="sxs-lookup"><span data-stu-id="219f9-158">Make sure to replace the ServiceEventSource name and Application Insights instrumentation key according to comments.</span></span> 

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

> [!NOTE]
> <span data-ttu-id="219f9-159">O nome da ServiceEventSource do serviço é o valor da propriedade Nome do `EventSourceAttribute` aplicado à classe ServiceEventSource.</span><span class="sxs-lookup"><span data-stu-id="219f9-159">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="219f9-160">Isso é especificado no arquivo `ServiceEventSource.cs`, que faz parte do código do serviço.</span><span class="sxs-lookup"><span data-stu-id="219f9-160">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="219f9-161">Por exemplo, no trecho de código a seguir, o nome do ServiceEventSource é *MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="219f9-161">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="219f9-162">Observe que o arquivo `eventFlowConfig.json` faz parte do pacote de configuração de serviço.</span><span class="sxs-lookup"><span data-stu-id="219f9-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="219f9-163">As alterações feitas neste arquivo podem ser incluídas em atualizações completo - ou apenas da configuração do serviço, sujeito a verificações de integridade de atualização do Service Fabric e a reversão automática se houver falha na atualização.</span><span class="sxs-lookup"><span data-stu-id="219f9-163">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="219f9-164">Para saber mais, confira [Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="219f9-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="219f9-165">A etapa final é criar uma instância de pipeline de EventFlow no código de inicialização do serviço, localizado em `Program.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="219f9-165">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="219f9-166">No exemplo a seguir relacionados EventFlow adições são marcadas com comentários começando com `****`:</span><span class="sxs-lookup"><span data-stu-id="219f9-166">In the following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

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

<span data-ttu-id="219f9-167">O nome passado como o parâmetro do método `CreatePipeline` do `ServiceFabricDiagnosticsPipelineFactory` é o nome da *entidade de integridade* que representa o pipeline de coleta de logs de EventFlow.</span><span class="sxs-lookup"><span data-stu-id="219f9-167">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="219f9-168">Esse nome será usado se EventFlow encontrar um erro e o reportar por meio do subsistema de integridade do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="219f9-168">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="219f9-169">Verificação</span><span class="sxs-lookup"><span data-stu-id="219f9-169">Verification</span></span>
<span data-ttu-id="219f9-170">Inicie o serviço e observe a depuração janela saída no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="219f9-170">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="219f9-171">Depois que o serviço for iniciado, você deverá começar a ver evidências de que o serviço está enviando registros de "Application Insights Telemetry".</span><span class="sxs-lookup"><span data-stu-id="219f9-171">After the service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="219f9-172">Abra um navegador da Web e vá até seu recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="219f9-172">Open a web browser and navigate go to your Application Insights resource.</span></span> <span data-ttu-id="219f9-173">Abra a guia "Pesquisar" (na parte superior da folha padrão "Visão geral").</span><span class="sxs-lookup"><span data-stu-id="219f9-173">Open "Search" tab (at the top of the default "Overview" blade).</span></span> <span data-ttu-id="219f9-174">Após um pequeno atraso, deve ser possível ver os rastreamentos no portal do Application Insights:</span><span class="sxs-lookup"><span data-stu-id="219f9-174">After a short delay you should start seeing your traces in the Application Insights portal:</span></span>

![Portal do Application Insights mostrando logs de um aplicativo do Service Fabric][2]

## <a name="next-steps"></a><span data-ttu-id="219f9-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="219f9-176">Next steps</span></span>
* [<span data-ttu-id="219f9-177">Saiba mais sobre o diagnóstico e monitoramento de um serviço da Malha de Serviço</span><span class="sxs-lookup"><span data-stu-id="219f9-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="219f9-178">Documentação de EventFlow</span><span class="sxs-lookup"><span data-stu-id="219f9-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
