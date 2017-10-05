---
title: "Converta os aplicativos de Serviços de Nuvem do Azure aos microsserviços | Microsoft Docs"
description: "Este guia compara as funções de trabalho e Web dos Serviços de Nuvem e os serviços sem estado do Service Fabric para ajudar a migrar dos Serviços de Nuvem para o Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4ab1f83e88b262b1752300b2786340d9abca8154
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="guide-to-converting-web-and-worker-roles-to-service-fabric-stateless-services"></a><span data-ttu-id="f362a-103">Guia de conversão de funções de trabalho e Web em serviços sem estado do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f362a-103">Guide to converting Web and Worker Roles to Service Fabric stateless services</span></span>
<span data-ttu-id="f362a-104">Este artigo descreve como migrar suas funções de trabalho e Web dos Serviços de Nuvem para serviços sem estado do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f362a-104">This article describes how to migrate your Cloud Services Web and Worker Roles to Service Fabric stateless services.</span></span> <span data-ttu-id="f362a-105">Esse é o caminho mais simples de migração dos Serviços de Nuvem para o Service Fabric, no caso de aplicativos cuja arquitetura geral permanecerá basicamente igual.</span><span class="sxs-lookup"><span data-stu-id="f362a-105">This is the simplest migration path from Cloud Services to Service Fabric for applications whose overall architecture is going to stay roughly the same.</span></span>

## <a name="cloud-service-project-to-service-fabric-application-project"></a><span data-ttu-id="f362a-106">Projeto de Serviço de Nuvem para projeto de aplicativo Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f362a-106">Cloud Service project to Service Fabric application project</span></span>
 <span data-ttu-id="f362a-107">Um projeto de Serviço de Nuvem e um projeto de aplicativo Service Fabric têm uma estrutura semelhante, e ambos representam a unidade de implantação de seu aplicativo, ou seja, cada um define o pacote completo que é implantado para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f362a-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent the deployment unit for your application - that is, they each define the complete package that is deployed to run your application.</span></span> <span data-ttu-id="f362a-108">Um projeto de Serviço de Nuvem contém uma ou mais funções de trabalho ou Web.</span><span class="sxs-lookup"><span data-stu-id="f362a-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="f362a-109">Da mesma forma, um projeto de aplicativo Service Fabric contém um ou mais serviços.</span><span class="sxs-lookup"><span data-stu-id="f362a-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="f362a-110">A diferença é que o projeto de Serviço de Nuvem associa a implantação do aplicativo a uma implantação de VM e, portanto, contém as definições de configuração da VM, enquanto o projeto de aplicativo Service Fabric define apenas um aplicativo que será implantado em um conjunto de máquinas virtuais existentes em um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f362a-110">The difference is that the Cloud Service project couples the application deployment with a VM deployment and thus contains VM configuration settings in it, whereas the Service Fabric Application project only defines an application that will be deployed to a set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="f362a-111">O cluster do Service Fabric em si só é implantado uma vez, por meio de um modelo do Resource Manager ou por meio do portal do Azure, e vários aplicativos do Service Fabric podem ser implantados nele.</span><span class="sxs-lookup"><span data-stu-id="f362a-111">The Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through the Azure portal, and multiple Service Fabric applications can be deployed to it.</span></span>

![Comparação de projeto dos Serviços de Nuvem e do Service Fabric][3]

## <a name="worker-role-to-stateless-service"></a><span data-ttu-id="f362a-113">Função de trabalho para serviço sem estado</span><span class="sxs-lookup"><span data-stu-id="f362a-113">Worker Role to stateless service</span></span>
<span data-ttu-id="f362a-114">Conceitualmente, uma função de trabalho representa uma carga de trabalho sem estado, o que significa que cada instância da carga de trabalho é idêntica e as solicitações podem ser roteadas para qualquer instância a qualquer hora.</span><span class="sxs-lookup"><span data-stu-id="f362a-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of the workload is identical and requests can be routed to any instance at any time.</span></span> <span data-ttu-id="f362a-115">Não se espera que as instâncias lembrem da solicitação anterior.</span><span class="sxs-lookup"><span data-stu-id="f362a-115">Each instance is not expected to remember the previous request.</span></span> <span data-ttu-id="f362a-116">O estado em que a carga de trabalho opera é gerenciado por um armazenamento de estado externo, como o Armazenamento de Tabelas do Azure ou o Banco de Dados de Documentos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f362a-116">State that the workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="f362a-117">No Service Fabric, esse tipo de carga de trabalho é representado por um serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="f362a-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="f362a-118">A abordagem mais simples para migrar uma função de trabalho para o Service Fabric pode ser feita pela conversão de um código de função de trabalho em um serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="f362a-118">The simplest approach to migrating a Worker Role to Service Fabric can be done by converting Worker Role code to a Stateless Service.</span></span>

![Função de trabalho para serviço sem estado][4]

## <a name="web-role-to-stateless-service"></a><span data-ttu-id="f362a-120">Função Web para serviço sem estado</span><span class="sxs-lookup"><span data-stu-id="f362a-120">Web Role to stateless service</span></span>
<span data-ttu-id="f362a-121">Semelhante à função de trabalho, uma função Web também representa uma carga de trabalho sem estado e, assim, conceitualmente, ele também pode ser mapeado para um serviço sem estado do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f362a-121">Similar to Worker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped to a Service Fabric stateless service.</span></span> <span data-ttu-id="f362a-122">No entanto, diferentemente das funções Web, o Service Fabric não dá suporte a IIS.</span><span class="sxs-lookup"><span data-stu-id="f362a-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="f362a-123">A migração de um aplicativo Web de uma função Web para um serviço sem estado requer primeiro a mudança para uma estrutura Web que pode ser auto-hospedada e não depende de IIS ou System.Web, como o ASP.NET Core 1.</span><span class="sxs-lookup"><span data-stu-id="f362a-123">To migrate a web application from a Web Role to a stateless service requires first moving to a web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="f362a-124">**Aplicativo**</span><span class="sxs-lookup"><span data-stu-id="f362a-124">**Application**</span></span> | <span data-ttu-id="f362a-125">**Com suporte**</span><span class="sxs-lookup"><span data-stu-id="f362a-125">**Supported**</span></span> | <span data-ttu-id="f362a-126">**Caminho de migração**</span><span class="sxs-lookup"><span data-stu-id="f362a-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f362a-127">Web Forms do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f362a-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="f362a-128">Não</span><span class="sxs-lookup"><span data-stu-id="f362a-128">No</span></span> |<span data-ttu-id="f362a-129">Converter em MVC do ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="f362a-129">Convert to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="f362a-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f362a-130">ASP.NET MVC</span></span> |<span data-ttu-id="f362a-131">Com migração</span><span class="sxs-lookup"><span data-stu-id="f362a-131">With Migration</span></span> |<span data-ttu-id="f362a-132">Atualizar para o ASP.NET Core 1 MVC</span><span class="sxs-lookup"><span data-stu-id="f362a-132">Upgrade to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="f362a-133">API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f362a-133">ASP.NET Web API</span></span> |<span data-ttu-id="f362a-134">Com migração</span><span class="sxs-lookup"><span data-stu-id="f362a-134">With Migration</span></span> |<span data-ttu-id="f362a-135">Usar o servidor auto-hospedado ou o ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="f362a-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="f362a-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="f362a-136">ASP.NET Core 1</span></span> |<span data-ttu-id="f362a-137">Sim</span><span class="sxs-lookup"><span data-stu-id="f362a-137">Yes</span></span> |<span data-ttu-id="f362a-138">N/D</span><span class="sxs-lookup"><span data-stu-id="f362a-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="f362a-139">API de ponto de entrada e ciclo de vida</span><span class="sxs-lookup"><span data-stu-id="f362a-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="f362a-140">As APIs de função de trabalho e do Service Fabric oferecem pontos de entrada semelhantes:</span><span class="sxs-lookup"><span data-stu-id="f362a-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="f362a-141">**Ponto de entrada**</span><span class="sxs-lookup"><span data-stu-id="f362a-141">**Entry Point**</span></span> | <span data-ttu-id="f362a-142">**Função de trabalho**</span><span class="sxs-lookup"><span data-stu-id="f362a-142">**Worker Role**</span></span> | <span data-ttu-id="f362a-143">**Serviço Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="f362a-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f362a-144">Processando</span><span class="sxs-lookup"><span data-stu-id="f362a-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="f362a-145">Iniciar VM</span><span class="sxs-lookup"><span data-stu-id="f362a-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="f362a-146">N/D</span><span class="sxs-lookup"><span data-stu-id="f362a-146">N/A</span></span> |
| <span data-ttu-id="f362a-147">Parar VM</span><span class="sxs-lookup"><span data-stu-id="f362a-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="f362a-148">N/D</span><span class="sxs-lookup"><span data-stu-id="f362a-148">N/A</span></span> |
| <span data-ttu-id="f362a-149">Abrir escuta para solicitações de cliente</span><span class="sxs-lookup"><span data-stu-id="f362a-149">Open listener for client requests</span></span> |<span data-ttu-id="f362a-150">N/D</span><span class="sxs-lookup"><span data-stu-id="f362a-150">N/A</span></span> |<ul><li> <span data-ttu-id="f362a-151">`CreateServiceInstanceListener()` para serviços sem estado</span><span class="sxs-lookup"><span data-stu-id="f362a-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="f362a-152">`CreateServiceReplicaListener()` para serviços com estado</span><span class="sxs-lookup"><span data-stu-id="f362a-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="f362a-153">Função de trabalho</span><span class="sxs-lookup"><span data-stu-id="f362a-153">Worker Role</span></span>
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="f362a-154">Serviço sem estado do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f362a-154">Service Fabric Stateless Service</span></span>
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

<span data-ttu-id="f362a-155">Ambos têm uma substituição de "Executar" principal para começar o processamento.</span><span class="sxs-lookup"><span data-stu-id="f362a-155">Both have a primary "Run" override in which to begin processing.</span></span> <span data-ttu-id="f362a-156">Os serviços do Service Fabric combinam `Run`, `Start` e `Stop` em um único ponto de entrada, `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="f362a-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="f362a-157">O serviço deve começar a trabalhar quando `RunAsync` inicia e deve parar de funcionar quando o CancellationToken do método `RunAsync` é sinalizado.</span><span class="sxs-lookup"><span data-stu-id="f362a-157">Your service should begin working when `RunAsync` starts, and should stop working when the `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="f362a-158">Há várias diferenças importantes entre o ciclo de vida e a vida útil das funções de trabalho e do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="f362a-158">There are several key differences between the lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="f362a-159">**Ciclo de vida:** a maior diferença é que uma função de trabalho é uma máquina virtual e, portanto, o ciclo de vida está ligado à VM, o que inclui eventos quando a VM inicia e para.</span><span class="sxs-lookup"><span data-stu-id="f362a-159">**Lifecycle:** The biggest difference is that a Worker Role is a VM and so its lifecycle is tied to the VM, which includes events for when the VM starts and stops.</span></span> <span data-ttu-id="f362a-160">Um serviço do Service Fabric tem um ciclo de vida que é separado do ciclo de vida da VM; portanto, ele não inclui eventos quando a VM ou computador host inicia e para, pois eles não estão relacionados.</span><span class="sxs-lookup"><span data-stu-id="f362a-160">A Service Fabric service has a lifecycle that is separate from the VM lifecycle, so it does not include events for when the host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="f362a-161">**Tempo de vida:** uma instância de função de trabalho será reciclada se o método `Run` sair.</span><span class="sxs-lookup"><span data-stu-id="f362a-161">**Lifetime:** A Worker Role instance will recycle if the `Run` method exits.</span></span> <span data-ttu-id="f362a-162">O método `RunAsync` em um serviço do Service Fabric, no entanto, pode executar até a conclusão, e a instância do serviço permanecerá ativa.</span><span class="sxs-lookup"><span data-stu-id="f362a-162">The `RunAsync` method in a Service Fabric service however can run to completion and the service instance will stay up.</span></span> 

<span data-ttu-id="f362a-163">O Service Fabric fornece um ponto de entrada de configuração opcional de comunicação para serviços que escutam solicitações de cliente.</span><span class="sxs-lookup"><span data-stu-id="f362a-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="f362a-164">O RunAsync e o ponto de entrada de comunicação são substituições opcionais nos serviços do Service Fabric. Seu serviço pode optar por escutar somente as solicitações do cliente ou somente executar um loop de processamento, ou ambos, motivo pelo qual o método RunAsync pode sair sem reiniciar a instância do serviço, pois ele pode continuar a escutar solicitações de cliente.</span><span class="sxs-lookup"><span data-stu-id="f362a-164">Both the RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose to only listen to client requests, or only run a processing loop, or both - which is why the RunAsync method is allowed to exit without restarting the service instance, because it may continue to listen for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="f362a-165">API de aplicativo e ambiente</span><span class="sxs-lookup"><span data-stu-id="f362a-165">Application API and environment</span></span>
<span data-ttu-id="f362a-166">A API do ambiente dos Serviços de Nuvem fornece informações e funcionalidade para a instância atual da VM, bem como informações sobre outras instâncias de função VM.</span><span class="sxs-lookup"><span data-stu-id="f362a-166">The Cloud Services environment API provides information and functionality for the current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="f362a-167">O Service Fabric fornece informações relacionadas ao tempo de execução e algumas informações sobre o nó em que o serviço está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="f362a-167">Service Fabric provides information related to its runtime and some information about the node a service is currently running on.</span></span> 

| <span data-ttu-id="f362a-168">**Tarefa de ambiente**</span><span class="sxs-lookup"><span data-stu-id="f362a-168">**Environment Task**</span></span> | <span data-ttu-id="f362a-169">**Serviços de Nuvem**</span><span class="sxs-lookup"><span data-stu-id="f362a-169">**Cloud Services**</span></span> | <span data-ttu-id="f362a-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="f362a-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f362a-171">Notificação de alteração e Definições de Configuração</span><span class="sxs-lookup"><span data-stu-id="f362a-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="f362a-172">Armazenamento local</span><span class="sxs-lookup"><span data-stu-id="f362a-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="f362a-173">Informações de ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="f362a-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="f362a-174">Instância atual: `RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="f362a-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="f362a-175">Outras funções e instância: `RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="f362a-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="f362a-176">`NodeContext` para o endereço do nó atual</span><span class="sxs-lookup"><span data-stu-id="f362a-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="f362a-177">`FabricClient` e `ServicePartitionResolver` para descoberta de ponto de extremidade de serviço</span><span class="sxs-lookup"><span data-stu-id="f362a-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="f362a-178">Ambiente de emulação</span><span class="sxs-lookup"><span data-stu-id="f362a-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="f362a-179">N/D</span><span class="sxs-lookup"><span data-stu-id="f362a-179">N/A</span></span> |
| <span data-ttu-id="f362a-180">Eventos de alteração simultânea</span><span class="sxs-lookup"><span data-stu-id="f362a-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="f362a-181">N/D</span><span class="sxs-lookup"><span data-stu-id="f362a-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="f362a-182">Definições de configuração</span><span class="sxs-lookup"><span data-stu-id="f362a-182">Configuration settings</span></span>
<span data-ttu-id="f362a-183">As definições de configuração nos Serviços de Nuvem são definidas para uma função VM e se aplicam a todas as instâncias dessa função VM.</span><span class="sxs-lookup"><span data-stu-id="f362a-183">Configuration settings in Cloud Services are set for a VM role and apply to all instances of that VM role.</span></span> <span data-ttu-id="f362a-184">Essas configurações são pares chave-valor definidos nos arquivos ServiceConfiguration.*.cscfg e podem ser acessadas diretamente por meio do RoleEnvironment.</span><span class="sxs-lookup"><span data-stu-id="f362a-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="f362a-185">No Service Fabric, as configurações se aplicam individualmente a cada serviço e a cada aplicativo, em vez de a uma VM, já que uma máquina virtual pode hospedar vários serviços e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f362a-185">In Service Fabric, settings apply individually to each service and to each application, rather than to a VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="f362a-186">Um serviço é composto de três pacotes:</span><span class="sxs-lookup"><span data-stu-id="f362a-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="f362a-187">**Código:** contém os executáveis de serviço, binários, DLLs e outros arquivos de que um serviço precisa para executar.</span><span class="sxs-lookup"><span data-stu-id="f362a-187">**Code:** contains the service executables, binaries, DLLs, and any other files a service needs to run.</span></span>
* <span data-ttu-id="f362a-188">**Config:** todos os arquivos de configuração e configurações de um serviço.</span><span class="sxs-lookup"><span data-stu-id="f362a-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="f362a-189">**Dados:** arquivos de dados estáticos associados ao serviço.</span><span class="sxs-lookup"><span data-stu-id="f362a-189">**Data:** static data files associated with the service.</span></span>

<span data-ttu-id="f362a-190">Cada um desses pacotes pode ter controle de versão e atualização independentes.</span><span class="sxs-lookup"><span data-stu-id="f362a-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="f362a-191">De forma semelhante aos Serviços de Nuvem, um pacote de configuração pode ser acessado programaticamente por uma API e há eventos disponíveis para notificar o serviço sobre alterações no pacote de configuração.</span><span class="sxs-lookup"><span data-stu-id="f362a-191">Similar to Cloud Services, a config package can be accessed programmatically through an API and events are available to notify the service of a config package change.</span></span> <span data-ttu-id="f362a-192">Um arquivo Settings.xml pode ser usado para configuração de chave-valor e acesso programático semelhante à seção de configurações do aplicativo de um arquivo App.config.</span><span class="sxs-lookup"><span data-stu-id="f362a-192">A Settings.xml file can be used for key-value configuration and programmatic access similar to the app settings section of an App.config file.</span></span> <span data-ttu-id="f362a-193">No entanto, ao contrário dos Serviços de Nuvem, um pacote de configuração do Service Fabric pode conter arquivos de configuração em qualquer formato, seja XML, JSON, YAML ou formato binário personalizado.</span><span class="sxs-lookup"><span data-stu-id="f362a-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="f362a-194">Acessando configuração</span><span class="sxs-lookup"><span data-stu-id="f362a-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="f362a-195">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="f362a-195">Cloud Services</span></span>
<span data-ttu-id="f362a-196">As definições de configuração do ServiceConfiguration.*.cscfg podem ser acessadas por meio do `RoleEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="f362a-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="f362a-197">Essas configurações estão disponíveis globalmente para todas as instâncias de função na mesma implantação do Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="f362a-197">These settings are globally available to all role instances in the same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="f362a-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f362a-198">Service Fabric</span></span>
<span data-ttu-id="f362a-199">Cada serviço tem seu próprio pacote de configuração individual.</span><span class="sxs-lookup"><span data-stu-id="f362a-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="f362a-200">Não há nenhum mecanismo interno para as configurações globais que possa ser acessado por todos os aplicativos em um cluster.</span><span class="sxs-lookup"><span data-stu-id="f362a-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="f362a-201">Ao usar o arquivo de configuração especial Settings.xml do Service Fabric em um pacote de configuração, os valores em Settings.xml podem ser substituídos no nível do aplicativo, possibilitando definições de configuração no nível do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f362a-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at the application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="f362a-202">As definições de configuração são acessadas em cada instância de serviço por meio do `CodePackageActivationContext`do serviço.</span><span class="sxs-lookup"><span data-stu-id="f362a-202">Configuration settings are accesses within each service instance through the service's `CodePackageActivationContext`.</span></span>

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a><span data-ttu-id="f362a-203">Eventos de atualização de configuração</span><span class="sxs-lookup"><span data-stu-id="f362a-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="f362a-204">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="f362a-204">Cloud Services</span></span>
<span data-ttu-id="f362a-205">O evento `RoleEnvironment.Changed` é usado para notificar a todas as instâncias de função quando ocorre uma alteração no ambiente, como uma alteração de configuração.</span><span class="sxs-lookup"><span data-stu-id="f362a-205">The `RoleEnvironment.Changed` event is used to notify all role instances when a change occurs in the environment, such as a configuration change.</span></span> <span data-ttu-id="f362a-206">Isso é usado para consumir as atualizações da configuração sem reciclar instâncias de função ou reiniciar um processo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f362a-206">This is used to consume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get the list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="f362a-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f362a-207">Service Fabric</span></span>
<span data-ttu-id="f362a-208">Cada um dos três tipos de pacote em um serviço, Código, Configuração e Dados, tem eventos que notificam uma instância de serviço quando um pacote é atualizado, adicionado ou removido.</span><span class="sxs-lookup"><span data-stu-id="f362a-208">Each of the three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="f362a-209">Um serviço pode conter vários pacotes de cada tipo.</span><span class="sxs-lookup"><span data-stu-id="f362a-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="f362a-210">Por exemplo, um serviço pode ter vários pacotes de configuração, cada um deles com controle de versão e atualização individuais.</span><span class="sxs-lookup"><span data-stu-id="f362a-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="f362a-211">Esses eventos estão disponíveis para consumir alterações nos pacotes de serviço sem reiniciar a instância do serviço.</span><span class="sxs-lookup"><span data-stu-id="f362a-211">These events are available to consume changes in service packages without restarting the service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="f362a-212">Tarefas de inicialização</span><span class="sxs-lookup"><span data-stu-id="f362a-212">Startup tasks</span></span>
<span data-ttu-id="f362a-213">As tarefas de inicialização são ações executadas antes de um aplicativo ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="f362a-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="f362a-214">Uma tarefa de inicialização normalmente é usada para executar scripts de instalação usando privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="f362a-214">A startup task is typically used to run setup scripts using elevated privileges.</span></span> <span data-ttu-id="f362a-215">Os Serviços de Nuvem e o Service Fabric dão suporte a tarefas de inicialização.</span><span class="sxs-lookup"><span data-stu-id="f362a-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="f362a-216">A principal diferença é que nos Serviços de Nuvem, uma tarefa de inicialização está vinculada a uma VM porque faz parte de uma instância de função, enquanto que no Service Fabric uma tarefa de inicialização está associada a um serviço, que não está vinculado a nenhuma máquina virtual específica.</span><span class="sxs-lookup"><span data-stu-id="f362a-216">The main difference is that in Cloud Services, a startup task is tied to a VM because it is part of a role instance, whereas in Service Fabric a startup task is tied to a service, which is not tied to any particular VM.</span></span>

| <span data-ttu-id="f362a-217">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="f362a-217">Cloud Services</span></span> | <span data-ttu-id="f362a-218">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f362a-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f362a-219">Configuração local</span><span class="sxs-lookup"><span data-stu-id="f362a-219">Configuration location</span></span> |<span data-ttu-id="f362a-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="f362a-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="f362a-221">Privilégios</span><span class="sxs-lookup"><span data-stu-id="f362a-221">Privileges</span></span> |<span data-ttu-id="f362a-222">"limitados" ou "elevados"</span><span class="sxs-lookup"><span data-stu-id="f362a-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="f362a-223">Sequenciamento</span><span class="sxs-lookup"><span data-stu-id="f362a-223">Sequencing</span></span> |<span data-ttu-id="f362a-224">"simples", "em segundo plano", "primeiro plano"</span><span class="sxs-lookup"><span data-stu-id="f362a-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="f362a-225">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="f362a-225">Cloud Services</span></span>
<span data-ttu-id="f362a-226">Nos Serviços de Nuvem, um ponto de entrada de inicialização é configurado por função em ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="f362a-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a><span data-ttu-id="f362a-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f362a-227">Service Fabric</span></span>
<span data-ttu-id="f362a-228">No Service Fabric, um ponto de entrada de inicialização é configurado por serviço em ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="f362a-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a><span data-ttu-id="f362a-229">Uma observação sobre o ambiente de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="f362a-229">A note about development environment</span></span>
<span data-ttu-id="f362a-230">Os Serviços de Nuvem e o Service Fabric são integrados com o Visual Studio com modelos de projeto e suporte para depuração, configuração e implantação localmente e no Azure.</span><span class="sxs-lookup"><span data-stu-id="f362a-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and to Azure.</span></span> <span data-ttu-id="f362a-231">Os Serviços de Nuvem e o Service Fabric também fornecem um ambiente de tempo de execução de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="f362a-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="f362a-232">A diferença é que enquanto o tempo de execução do desenvolvimento do Serviço de Nuvem emula o ambiente do Azure no qual ele é executado, o Service Fabric não usa um emulador; ele usa o tempo de execução do Service Fabric completo.</span><span class="sxs-lookup"><span data-stu-id="f362a-232">The difference is that while the Cloud Service development runtime emulates the Azure environment on which it runs, Service Fabric does not use an emulator - it uses the complete Service Fabric runtime.</span></span> <span data-ttu-id="f362a-233">O ambiente do Service Fabric executado em sua máquina de desenvolvimento local é o mesmo ambiente executado na produção.</span><span class="sxs-lookup"><span data-stu-id="f362a-233">The Service Fabric environment you run on your local development machine is the same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f362a-234">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f362a-234">Next steps</span></span>
<span data-ttu-id="f362a-235">Leia mais sobre os Reliable Services do Service Fabric e as diferenças fundamentais entre os Serviços de Nuvem e a arquitetura de aplicativos Service Fabric para entender como tirar proveito do conjunto completo de recursos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f362a-235">Read more about Service Fabric Reliable Services and the fundamental differences between Cloud Services and Service Fabric application architecture to understand how to take advantage of the full set of Service Fabric features.</span></span>

* [<span data-ttu-id="f362a-236">Introdução aos Reliable Services do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f362a-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="f362a-237">Guia conceitual sobre as diferenças entre os Serviços de Nuvem e o Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f362a-237">Conceptual guide to the differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
