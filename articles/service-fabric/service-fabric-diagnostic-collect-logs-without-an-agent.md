---
title: "logs de aaaCollect diretamente de uma malha de serviço do Azure processo do serviço | Microsoft Azure"
description: "Descreve os aplicativos podem enviar logs diretamente local central tooa, como informações de aplicativo do Azure ou Elasticsearch, sem depender de agente de diagnóstico do Azure do Service Fabric."
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
ms.openlocfilehash: d0681a2a6aaa76028d7cb469c31c006f24bbe954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="d17ac-103">Coletar logs diretamente de um processo do serviço Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d17ac-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="d17ac-104">Coleta de logs no processo</span><span class="sxs-lookup"><span data-stu-id="d17ac-104">In-process log collection</span></span>
<span data-ttu-id="d17ac-105">Coletar o aplicativo registra em log usando [extensão de diagnóstico do Azure](service-fabric-diagnostics-how-to-setup-wad.md) é uma boa opção para **Azure Service Fabric** serviços se Olá conjunto de log origens e destinos é pequeno, não altere muitas vezes e há é um mapeamento direto entre as origens de saudação e seus destinos.</span><span class="sxs-lookup"><span data-stu-id="d17ac-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if hello set of log sources and destinations is small, does not change often, and there is a straightforward mapping between hello sources and their destinations.</span></span> <span data-ttu-id="d17ac-106">Caso contrário, uma alternativa é toohave serviços enviar os logs diretamente local central tooa.</span><span class="sxs-lookup"><span data-stu-id="d17ac-106">If not, an alternative is toohave services send their logs directly tooa central location.</span></span> <span data-ttu-id="d17ac-107">Esse processo é conhecido como **coleta de logs no processo** e tem várias vantagens potenciais:</span><span class="sxs-lookup"><span data-stu-id="d17ac-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="d17ac-108">*Fácil Configuração e implantação*</span><span class="sxs-lookup"><span data-stu-id="d17ac-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="d17ac-109">configuração de saudação da coleta de dados de diagnóstico é apenas parte da configuração do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="d17ac-109">hello configuration of diagnostic data collection is just part of hello service configuration.</span></span> <span data-ttu-id="d17ac-110">É fácil tooalways manter "sincronizado" com hello-rest do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d17ac-110">It is easy tooalways keep it "in sync" with hello rest of hello application.</span></span>
    * <span data-ttu-id="d17ac-111">A configuração por aplicativo ou por serviço é facilmente realizável.</span><span class="sxs-lookup"><span data-stu-id="d17ac-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="d17ac-112">Coleta de log com base em agente normalmente requer uma implantação separada e a configuração do agente de diagnóstico hello, que é uma tarefa administrativa adicional e uma fonte de erros em potencial.</span><span class="sxs-lookup"><span data-stu-id="d17ac-112">Agent-based log collection usually requires a separate deployment and configuration of hello diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="d17ac-113">Geralmente, há apenas uma instância do agente de saudação permitido por máquina virtual (nó) e configuração do agente Olá é compartilhada entre todos os aplicativos e serviços em execução nesse nó.</span><span class="sxs-lookup"><span data-stu-id="d17ac-113">Often there is only one instance of hello agent allowed per virtual machine (node) and hello agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="d17ac-114">*Flexibilidade*</span><span class="sxs-lookup"><span data-stu-id="d17ac-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="d17ac-115">aplicativo Hello pode enviar dados Olá sempre que ele precisa toogo, enquanto há uma biblioteca de cliente que oferece suporte ao sistema de armazenamento de dados Olá direcionado.</span><span class="sxs-lookup"><span data-stu-id="d17ac-115">hello application can send hello data wherever it needs toogo, as long as there is a client library that supports hello targeted data storage system.</span></span> <span data-ttu-id="d17ac-116">Novos destinos podem ser adicionados conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="d17ac-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="d17ac-117">Regras de captura complexa, filtragem e agregação de dados podem ser implementadas.</span><span class="sxs-lookup"><span data-stu-id="d17ac-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="d17ac-118">Coleta de log com base em agente geralmente é limitada pelo Coletores de dados de saudação que Olá agent dá suporte a.</span><span class="sxs-lookup"><span data-stu-id="d17ac-118">Agent-based log collection is often limited by hello data sinks that hello agent supports.</span></span> <span data-ttu-id="d17ac-119">Alguns agentes são extensíveis.</span><span class="sxs-lookup"><span data-stu-id="d17ac-119">Some agents are extensible.</span></span>

* <span data-ttu-id="d17ac-120">*Contexto e acessar dados de aplicativo toointernal*</span><span class="sxs-lookup"><span data-stu-id="d17ac-120">*Access toointernal application data and context*</span></span>
   
    * <span data-ttu-id="d17ac-121">subsistema de diagnóstico Olá em execução no processo de aplicativo/serviço Olá facilmente pode aumentar rastreamentos Olá com informações contextuais.</span><span class="sxs-lookup"><span data-stu-id="d17ac-121">hello diagnostic subsystem running inside hello application/service process can easily augment hello traces with contextual information.</span></span>
    * <span data-ttu-id="d17ac-122">Com a coleção de log com base em agente dados saudação devem ser enviados tooan agent por meio de um mecanismo de comunicação entre processos, como o rastreamento de eventos do Windows.</span><span class="sxs-lookup"><span data-stu-id="d17ac-122">With agent-based log collection, hello data must be sent tooan agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="d17ac-123">Esse mecanismo pode impor limitações adicionais.</span><span class="sxs-lookup"><span data-stu-id="d17ac-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="d17ac-124">É possível toocombine e se beneficiam de ambos os métodos de coleção.</span><span class="sxs-lookup"><span data-stu-id="d17ac-124">It is possible toocombine and benefit from both collection methods.</span></span> <span data-ttu-id="d17ac-125">Na verdade, talvez seja melhor solução Olá para muitos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d17ac-125">Indeed, it might be hello best solution for many applications.</span></span> <span data-ttu-id="d17ac-126">Coleção com base em agente é uma solução natural para coletar o cluster inteiro de toohello relacionados de logs e nós de cluster individuais.</span><span class="sxs-lookup"><span data-stu-id="d17ac-126">Agent-based collection is a natural solution for collecting logs related toohello whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="d17ac-127">É uma maneira muito mais confiável, que coleta de log em processo, problemas de inicialização do serviço de toodiagnose e falhas.</span><span class="sxs-lookup"><span data-stu-id="d17ac-127">It is much more reliable way, than in-process log collection, toodiagnose service startup problems and crashes.</span></span> <span data-ttu-id="d17ac-128">Além disso, com muitos serviços em execução dentro de um cluster do Service Fabric, cada serviço fazer sua própria coleção de log em processo resulta em várias conexões de saída do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d17ac-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from hello cluster.</span></span> <span data-ttu-id="d17ac-129">Grande número de conexões de saída é uma sobrecarga para o subsistema de rede hello e de destino de log hello.</span><span class="sxs-lookup"><span data-stu-id="d17ac-129">Large number of outgoing connections is taxing both for hello network subsystem and for hello log destination.</span></span> <span data-ttu-id="d17ac-130">Um agente como [ **diagnóstico do Azure** ](../cloud-services/cloud-services-dotnet-diagnostics.md) pode coletar dados de vários serviços e enviar dados por meio de algumas conexões, melhorando a taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="d17ac-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="d17ac-131">Neste artigo, mostramos como tooset um processo de-log coleção usando [ **biblioteca de código-fonte aberto EventFlow**](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="d17ac-131">In this article, we show how tooset up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="d17ac-132">Outras bibliotecas podem ser usadas para Olá mesmo propósito, mas EventFlow tem benefício de saudação de projetados especificamente para em processo log coleta e toosupport serviços do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d17ac-132">Other libraries might be used for hello same purpose, but EventFlow has hello benefit of having been designed specifically for in-process log collection and toosupport Service Fabric services.</span></span> <span data-ttu-id="d17ac-133">Usamos [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) como destino de log hello.</span><span class="sxs-lookup"><span data-stu-id="d17ac-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as hello log destination.</span></span> <span data-ttu-id="d17ac-134">Outros destinos, como [ **Hubs de eventos** ](https://azure.microsoft.com/services/event-hubs/) ou [ **Elasticsearch** ](https://www.elastic.co/products/elasticsearch) também têm suporte.</span><span class="sxs-lookup"><span data-stu-id="d17ac-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="d17ac-135">É apenas uma questão de instalar o pacote do NuGet apropriado e configurando o destino de Olá no arquivo de configuração EventFlow Olá.</span><span class="sxs-lookup"><span data-stu-id="d17ac-135">It is just a question of installing appropriate NuGet package and configuring hello destination in hello EventFlow configuration file.</span></span> <span data-ttu-id="d17ac-136">Para obter mais informações sobre destinos de log diferente do Application Insights, consulte [EventFlow documentação](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="d17ac-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a><span data-ttu-id="d17ac-137">Adicionar projeto de serviço EventFlow biblioteca tooa Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d17ac-137">Adding EventFlow library tooa Service Fabric service project</span></span>
<span data-ttu-id="d17ac-138">EventFlow binários estão disponíveis como um conjunto de pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="d17ac-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="d17ac-139">tooadd EventFlow tooa projeto do serviço do Service Fabric, clique com botão direito Olá no hello Gerenciador de soluções e escolha "Pacotes de gerenciar NuGet".</span><span class="sxs-lookup"><span data-stu-id="d17ac-139">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="d17ac-140">Alternar o guia de "Procurar" toohello e procure "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="d17ac-140">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Pacotes do EventFlow NuGet no Gerenciador de pacotes do NuGet do Visual Studio da interface do usuário][1]

<span data-ttu-id="d17ac-142">serviço de saudação hospedagem EventFlow deve incluir pacotes apropriados dependendo da origem de saudação e de destino para os logs de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d17ac-142">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="d17ac-143">Adicione Olá pacotes a seguir:</span><span class="sxs-lookup"><span data-stu-id="d17ac-143">Add hello following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="d17ac-144">(toocapture dados de classe de EventSource do serviço hello e de EventSources padrão como *serviços do Microsoft-ServiceFabric* e *ServiceFabric-Microsoft-atores*)</span><span class="sxs-lookup"><span data-stu-id="d17ac-144">(toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="d17ac-145">(vamos toosend Olá logs tooan Azure Application Insights recurso)</span><span class="sxs-lookup"><span data-stu-id="d17ac-145">(we are going toosend hello logs tooan Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="d17ac-146">(permite a inicialização do pipeline de EventFlow Olá da configuração de serviço do Service Fabric e reporta os problemas com o envio de dados de diagnóstico como relatórios de integridade da malha do serviço)</span><span class="sxs-lookup"><span data-stu-id="d17ac-146">(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="d17ac-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource`o pacote requer tootarget de projeto de serviço de saudação do .NET Framework 4.6 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="d17ac-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="d17ac-148">Verifique se que você configurou o framework de destino apropriado Olá nas propriedades do projeto antes de instalar este pacote.</span><span class="sxs-lookup"><span data-stu-id="d17ac-148">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="d17ac-149">Depois que todos os hello pacotes estão instalados, Olá próxima etapa é tooconfigure e habilitar EventFlow no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="d17ac-149">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="d17ac-150">Configurar e habilitar a coleta de logs</span><span class="sxs-lookup"><span data-stu-id="d17ac-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="d17ac-151">Pipeline EventFlow, responsável pelo envio de logs Olá, é criado a partir de uma especificação armazenada em um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="d17ac-151">EventFlow pipeline, responsible for sending hello logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="d17ac-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric`pacote instala um arquivo de configuração inicial do EventFlow em `PackageRoot\Config` pasta da solução.</span><span class="sxs-lookup"><span data-stu-id="d17ac-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="d17ac-153">nome do arquivo Hello é `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="d17ac-153">hello file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="d17ac-154">Esse arquivo de configuração precisa toobe modificado toocapture dados do serviço de padrão de saudação `EventSource` classe e envia dados tooApplication Insights service.</span><span class="sxs-lookup"><span data-stu-id="d17ac-154">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class and send data tooApplication Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="d17ac-155">Vamos supor que você esteja familiarizado com **Azure Application Insights** serviço e se você tem um recurso do Application Insights que você planeje toouse toomonitor seu serviço de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="d17ac-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan toouse toomonitor your Service Fabric service.</span></span> <span data-ttu-id="d17ac-156">Se você precisar de mais informações, veja [Criar um recurso do Application Insights](../application-insights/app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="d17ac-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="d17ac-157">Olá abrir `eventFlowConfig.json` no editor de saudação e alterar seu conteúdo, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="d17ac-157">Open hello `eventFlowConfig.json` file in hello editor and change its content as shown below.</span></span> <span data-ttu-id="d17ac-158">Certifique-se de nome de ServiceEventSource de saudação de tooreplace e a chave de instrumentação do Application Insights toocomments de acordo com.</span><span class="sxs-lookup"><span data-stu-id="d17ac-158">Make sure tooreplace hello ServiceEventSource name and Application Insights instrumentation key according toocomments.</span></span> 

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

> [!NOTE]
> <span data-ttu-id="d17ac-159">nome de saudação do ServiceEventSource do serviço é o valor de saudação do hello propriedade Name de saudação `EventSourceAttribute` aplicada toohello ServiceEventSource classe.</span><span class="sxs-lookup"><span data-stu-id="d17ac-159">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="d17ac-160">Ele é especificado em Olá `ServiceEventSource.cs` arquivo, que faz parte do código de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="d17ac-160">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="d17ac-161">Por exemplo, em Olá seguir Olá nome do trecho de saudação ServiceEventSource é *MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="d17ac-161">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="d17ac-162">Observe que o arquivo `eventFlowConfig.json` faz parte do pacote de configuração de serviço.</span><span class="sxs-lookup"><span data-stu-id="d17ac-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="d17ac-163">Arquivo de toothis de alterações pode ser incluído no completo ou configuração-somente atualizações de serviço hello, assunto tooService malha atualização verificações de integridade e reversão automática se houver falha na atualização.</span><span class="sxs-lookup"><span data-stu-id="d17ac-163">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="d17ac-164">Para saber mais, confira [Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="d17ac-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="d17ac-165">Olá última etapa é o pipeline de EventFlow tooinstantiate no código de inicialização do serviço, localizado em `Program.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="d17ac-165">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="d17ac-166">Em Olá adições a seguir exemplo EventFlow relacionadas são marcadas com comentários começando com `****`:</span><span class="sxs-lookup"><span data-stu-id="d17ac-166">In hello following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

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

<span data-ttu-id="d17ac-167">nome Hello passado como parâmetro de saudação do hello `CreatePipeline` método hello `ServiceFabricDiagnosticsPipelineFactory` é nome de saudação do hello *entidade integridade* que representa o pipeline de coleta de log Olá EventFlow.</span><span class="sxs-lookup"><span data-stu-id="d17ac-167">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="d17ac-168">Esse nome é usado se encontrar EventFlow e erro e reporta isso por meio de saudação subsistema de integridade da malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="d17ac-168">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="d17ac-169">Verificação</span><span class="sxs-lookup"><span data-stu-id="d17ac-169">Verification</span></span>
<span data-ttu-id="d17ac-170">Iniciar o serviço e observar Olá depuração janela de saída no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d17ac-170">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="d17ac-171">Depois de iniciado o serviço hello, você deve começar a ver evidências de que o serviço está enviando registros de "Telemetria do Application Insights".</span><span class="sxs-lookup"><span data-stu-id="d17ac-171">After hello service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="d17ac-172">Abra um navegador da web e navegue tooyour vá Application Insights recursos.</span><span class="sxs-lookup"><span data-stu-id="d17ac-172">Open a web browser and navigate go tooyour Application Insights resource.</span></span> <span data-ttu-id="d17ac-173">Abra a guia "Pesquisar" (na parte superior de saudação da folha de "Visão geral" hello padrão).</span><span class="sxs-lookup"><span data-stu-id="d17ac-173">Open "Search" tab (at hello top of hello default "Overview" blade).</span></span> <span data-ttu-id="d17ac-174">Após um pequeno atraso você deve começar a ver os rastreamentos no portal do Application Insights hello:</span><span class="sxs-lookup"><span data-stu-id="d17ac-174">After a short delay you should start seeing your traces in hello Application Insights portal:</span></span>

![Portal do Application Insights mostrando logs de um aplicativo do Service Fabric][2]

## <a name="next-steps"></a><span data-ttu-id="d17ac-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d17ac-176">Next steps</span></span>
* [<span data-ttu-id="d17ac-177">Saiba mais sobre o diagnóstico e monitoramento de um serviço da Malha de Serviço</span><span class="sxs-lookup"><span data-stu-id="d17ac-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="d17ac-178">Documentação de EventFlow</span><span class="sxs-lookup"><span data-stu-id="d17ac-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
