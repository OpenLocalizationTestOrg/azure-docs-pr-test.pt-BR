---
title: "aaaConvert toomicroservices de aplicativos de serviços de nuvem do Azure | Microsoft Docs"
description: "Este guia compara da Web de serviços de nuvem e funções de trabalho e do Service Fabric serviços sem estado toohelp migram de serviços de nuvem tooService malha."
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
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a><span data-ttu-id="93895-103">Guia tooconverting serviços Web e funções de trabalho tooService malha sem monitoração de estado</span><span class="sxs-lookup"><span data-stu-id="93895-103">Guide tooconverting Web and Worker Roles tooService Fabric stateless services</span></span>
<span data-ttu-id="93895-104">Este artigo descreve como toomigrate sua nuvem serviços Web e funções de trabalho tooService malha sem monitoração de estado dos serviços.</span><span class="sxs-lookup"><span data-stu-id="93895-104">This article describes how toomigrate your Cloud Services Web and Worker Roles tooService Fabric stateless services.</span></span> <span data-ttu-id="93895-105">Este é o caminho de migração mais simples saudação do serviços de nuvem tooService malha de aplicativos cuja arquitetura geral será aproximadamente toostay Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="93895-105">This is hello simplest migration path from Cloud Services tooService Fabric for applications whose overall architecture is going toostay roughly hello same.</span></span>

## <a name="cloud-service-project-tooservice-fabric-application-project"></a><span data-ttu-id="93895-106">O projeto de aplicativo do serviço project tooService malha de nuvem</span><span class="sxs-lookup"><span data-stu-id="93895-106">Cloud Service project tooService Fabric application project</span></span>
 <span data-ttu-id="93895-107">Um projeto de serviço de nuvem e um projeto de aplicativo do Service Fabric têm uma estrutura semelhante e ambas as unidade de implantação Olá representam de seu aplicativo - ou seja, eles cada definem Olá completo pacote toorun implantado seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="93895-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent hello deployment unit for your application - that is, they each define hello complete package that is deployed toorun your application.</span></span> <span data-ttu-id="93895-108">Um projeto de Serviço de Nuvem contém uma ou mais funções de trabalho ou Web.</span><span class="sxs-lookup"><span data-stu-id="93895-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="93895-109">Da mesma forma, um projeto de aplicativo Service Fabric contém um ou mais serviços.</span><span class="sxs-lookup"><span data-stu-id="93895-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="93895-110">diferença de saudação é que Casais de projeto de serviço de nuvem Olá Olá a implantação de aplicativos com uma implantação de VM e, portanto, contém as definições de configuração da VM, enquanto o projeto de aplicativo do Service Fabric Olá define apenas um aplicativo que será implantado tooa o conjunto de máquinas virtuais existentes em um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="93895-110">hello difference is that hello Cloud Service project couples hello application deployment with a VM deployment and thus contains VM configuration settings in it, whereas hello Service Fabric Application project only defines an application that will be deployed tooa set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="93895-111">cluster do Service Fabric Olá em si é implantado apenas uma vez, por meio de um modelo do Gerenciador de recursos ou através de saudação portal do Azure e o Service Fabric vários aplicativos podem ser implantados tooit.</span><span class="sxs-lookup"><span data-stu-id="93895-111">hello Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through hello Azure portal, and multiple Service Fabric applications can be deployed tooit.</span></span>

![Comparação de projeto dos Serviços de Nuvem e do Service Fabric][3]

## <a name="worker-role-toostateless-service"></a><span data-ttu-id="93895-113">Serviço de toostateless de função de trabalho</span><span class="sxs-lookup"><span data-stu-id="93895-113">Worker Role toostateless service</span></span>
<span data-ttu-id="93895-114">Conceitualmente, uma função de trabalho representa uma carga de trabalho sem monitoração de estado, que significa que todas as instâncias de carga de trabalho de saudação é idêntica e solicitações podem ser roteado tooany instância a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="93895-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of hello workload is identical and requests can be routed tooany instance at any time.</span></span> <span data-ttu-id="93895-115">Cada instância não é solicitação anterior de saudação tooremember esperado.</span><span class="sxs-lookup"><span data-stu-id="93895-115">Each instance is not expected tooremember hello previous request.</span></span> <span data-ttu-id="93895-116">Estado de carga de trabalho Olá opera em é gerenciado por um armazenamento de estado externo, como o armazenamento de tabela do Azure ou banco de dados de documento do Azure.</span><span class="sxs-lookup"><span data-stu-id="93895-116">State that hello workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="93895-117">No Service Fabric, esse tipo de carga de trabalho é representado por um serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="93895-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="93895-118">Olá mais simples abordagem toomigrating um tooService de função de trabalho malha pode ser feita pela conversão tooa de código da função de trabalho sem monitoração de estado do serviço.</span><span class="sxs-lookup"><span data-stu-id="93895-118">hello simplest approach toomigrating a Worker Role tooService Fabric can be done by converting Worker Role code tooa Stateless Service.</span></span>

![Função de trabalho tooStateless serviço][4]

## <a name="web-role-toostateless-service"></a><span data-ttu-id="93895-120">Função toostateless serviço Web</span><span class="sxs-lookup"><span data-stu-id="93895-120">Web Role toostateless service</span></span>
<span data-ttu-id="93895-121">TooWorker semelhante função, uma função Web também representa uma carga de trabalho sem monitoração de estado, e portanto conceitualmente muito pode ser mapeado tooa serviço sem monitoração de estado do serviço de malha.</span><span class="sxs-lookup"><span data-stu-id="93895-121">Similar tooWorker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped tooa Service Fabric stateless service.</span></span> <span data-ttu-id="93895-122">No entanto, diferentemente das funções Web, o Service Fabric não dá suporte a IIS.</span><span class="sxs-lookup"><span data-stu-id="93895-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="93895-123">toomigrate um aplicativo web de um serviço sem monitoração de estado de tooa de função Web requer primeiro framework web tooa móvel que pode ser auto-hospedado e não dependem de IIS ou System. Web, como o ASP.NET Core 1.</span><span class="sxs-lookup"><span data-stu-id="93895-123">toomigrate a web application from a Web Role tooa stateless service requires first moving tooa web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="93895-124">**Aplicativo**</span><span class="sxs-lookup"><span data-stu-id="93895-124">**Application**</span></span> | <span data-ttu-id="93895-125">**Com suporte**</span><span class="sxs-lookup"><span data-stu-id="93895-125">**Supported**</span></span> | <span data-ttu-id="93895-126">**Caminho de migração**</span><span class="sxs-lookup"><span data-stu-id="93895-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="93895-127">Web Forms do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="93895-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="93895-128">Não</span><span class="sxs-lookup"><span data-stu-id="93895-128">No</span></span> |<span data-ttu-id="93895-129">Converter tooASP.NET principal 1 MVC</span><span class="sxs-lookup"><span data-stu-id="93895-129">Convert tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="93895-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="93895-130">ASP.NET MVC</span></span> |<span data-ttu-id="93895-131">Com migração</span><span class="sxs-lookup"><span data-stu-id="93895-131">With Migration</span></span> |<span data-ttu-id="93895-132">Atualização tooASP.NET principal 1 MVC</span><span class="sxs-lookup"><span data-stu-id="93895-132">Upgrade tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="93895-133">API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="93895-133">ASP.NET Web API</span></span> |<span data-ttu-id="93895-134">Com migração</span><span class="sxs-lookup"><span data-stu-id="93895-134">With Migration</span></span> |<span data-ttu-id="93895-135">Usar o servidor auto-hospedado ou o ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="93895-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="93895-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="93895-136">ASP.NET Core 1</span></span> |<span data-ttu-id="93895-137">Sim</span><span class="sxs-lookup"><span data-stu-id="93895-137">Yes</span></span> |<span data-ttu-id="93895-138">N/D</span><span class="sxs-lookup"><span data-stu-id="93895-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="93895-139">API de ponto de entrada e ciclo de vida</span><span class="sxs-lookup"><span data-stu-id="93895-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="93895-140">As APIs de função de trabalho e do Service Fabric oferecem pontos de entrada semelhantes:</span><span class="sxs-lookup"><span data-stu-id="93895-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="93895-141">**Ponto de entrada**</span><span class="sxs-lookup"><span data-stu-id="93895-141">**Entry Point**</span></span> | <span data-ttu-id="93895-142">**Função de trabalho**</span><span class="sxs-lookup"><span data-stu-id="93895-142">**Worker Role**</span></span> | <span data-ttu-id="93895-143">**Serviço Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="93895-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="93895-144">Processando</span><span class="sxs-lookup"><span data-stu-id="93895-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="93895-145">Iniciar VM</span><span class="sxs-lookup"><span data-stu-id="93895-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="93895-146">N/D</span><span class="sxs-lookup"><span data-stu-id="93895-146">N/A</span></span> |
| <span data-ttu-id="93895-147">Parar VM</span><span class="sxs-lookup"><span data-stu-id="93895-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="93895-148">N/D</span><span class="sxs-lookup"><span data-stu-id="93895-148">N/A</span></span> |
| <span data-ttu-id="93895-149">Abrir escuta para solicitações de cliente</span><span class="sxs-lookup"><span data-stu-id="93895-149">Open listener for client requests</span></span> |<span data-ttu-id="93895-150">N/D</span><span class="sxs-lookup"><span data-stu-id="93895-150">N/A</span></span> |<ul><li> <span data-ttu-id="93895-151">`CreateServiceInstanceListener()` para serviços sem estado</span><span class="sxs-lookup"><span data-stu-id="93895-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="93895-152">`CreateServiceReplicaListener()` para serviços com estado</span><span class="sxs-lookup"><span data-stu-id="93895-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="93895-153">Função de trabalho</span><span class="sxs-lookup"><span data-stu-id="93895-153">Worker Role</span></span>
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

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="93895-154">Serviço sem estado do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="93895-154">Service Fabric Stateless Service</span></span>
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

<span data-ttu-id="93895-155">Têm uma substituição de "Executar" primário em que o processamento toobegin.</span><span class="sxs-lookup"><span data-stu-id="93895-155">Both have a primary "Run" override in which toobegin processing.</span></span> <span data-ttu-id="93895-156">Os serviços do Service Fabric combinam `Run`, `Start` e `Stop` em um único ponto de entrada, `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="93895-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="93895-157">O serviço deve começar a trabalhar quando `RunAsync` inicia e deve parar de funcionar quando hello `RunAsync` CancellationToken do método é sinalizado.</span><span class="sxs-lookup"><span data-stu-id="93895-157">Your service should begin working when `RunAsync` starts, and should stop working when hello `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="93895-158">Há várias diferenças importantes entre o ciclo de vida de saudação e tempo de vida de serviços de funções de trabalho e serviço de malha:</span><span class="sxs-lookup"><span data-stu-id="93895-158">There are several key differences between hello lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="93895-159">**Ciclo de vida:** Olá maior diferença é que uma função de trabalho é uma VM e portanto o ciclo de vida é toohello empatado VM, que inclui eventos de ao Olá VM inícios e paradas.</span><span class="sxs-lookup"><span data-stu-id="93895-159">**Lifecycle:** hello biggest difference is that a Worker Role is a VM and so its lifecycle is tied toohello VM, which includes events for when hello VM starts and stops.</span></span> <span data-ttu-id="93895-160">Um serviço de malha do serviço tem um ciclo de vida que é separado do ciclo de vida VM hello, portanto, não inclui eventos para quando o hello host VM ou máquina é iniciado e parar, pois eles não estão relacionados.</span><span class="sxs-lookup"><span data-stu-id="93895-160">A Service Fabric service has a lifecycle that is separate from hello VM lifecycle, so it does not include events for when hello host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="93895-161">**Tempo de vida:** uma instância de função de trabalho reciclará se hello `Run` sai do método.</span><span class="sxs-lookup"><span data-stu-id="93895-161">**Lifetime:** A Worker Role instance will recycle if hello `Run` method exits.</span></span> <span data-ttu-id="93895-162">Olá `RunAsync` método em um serviço do Service Fabric Entretanto pode executar toocompletion e instância de serviço Olá permaneçam em.</span><span class="sxs-lookup"><span data-stu-id="93895-162">hello `RunAsync` method in a Service Fabric service however can run toocompletion and hello service instance will stay up.</span></span> 

<span data-ttu-id="93895-163">O Service Fabric fornece um ponto de entrada de configuração opcional de comunicação para serviços que escutam solicitações de cliente.</span><span class="sxs-lookup"><span data-stu-id="93895-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="93895-164">Olá RunAsync e o ponto de entrada de comunicação são substituições opcionais nos serviços do Service Fabric - seu serviço pode escolher tooonly escutar solicitações de tooclient, ou apenas executar um loop de processamento, ou ambos - motivo pelo qual Olá método RunAsync é permitido tooexit sem reiniciar a instância de serviço Olá, porque ele pode continuar toolisten para solicitações de cliente.</span><span class="sxs-lookup"><span data-stu-id="93895-164">Both hello RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose tooonly listen tooclient requests, or only run a processing loop, or both - which is why hello RunAsync method is allowed tooexit without restarting hello service instance, because it may continue toolisten for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="93895-165">API de aplicativo e ambiente</span><span class="sxs-lookup"><span data-stu-id="93895-165">Application API and environment</span></span>
<span data-ttu-id="93895-166">ambiente de serviços de nuvem Olá API fornece informações e funcionalidade para a instância atual de VM hello, bem como informações sobre outras instâncias de função VM.</span><span class="sxs-lookup"><span data-stu-id="93895-166">hello Cloud Services environment API provides information and functionality for hello current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="93895-167">Service Fabric fornece informações relacionadas tooits tempo de execução e algumas informações sobre o nó de saudação um serviço no momento está executando.</span><span class="sxs-lookup"><span data-stu-id="93895-167">Service Fabric provides information related tooits runtime and some information about hello node a service is currently running on.</span></span> 

| <span data-ttu-id="93895-168">**Tarefa de ambiente**</span><span class="sxs-lookup"><span data-stu-id="93895-168">**Environment Task**</span></span> | <span data-ttu-id="93895-169">**Serviços de Nuvem**</span><span class="sxs-lookup"><span data-stu-id="93895-169">**Cloud Services**</span></span> | <span data-ttu-id="93895-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="93895-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="93895-171">Notificação de alteração e Definições de Configuração</span><span class="sxs-lookup"><span data-stu-id="93895-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="93895-172">Armazenamento local</span><span class="sxs-lookup"><span data-stu-id="93895-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="93895-173">Informações de ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="93895-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="93895-174">Instância atual: `RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="93895-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="93895-175">Outras funções e instância: `RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="93895-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="93895-176">`NodeContext` para o endereço do nó atual</span><span class="sxs-lookup"><span data-stu-id="93895-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="93895-177">`FabricClient` e `ServicePartitionResolver` para descoberta de ponto de extremidade de serviço</span><span class="sxs-lookup"><span data-stu-id="93895-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="93895-178">Ambiente de emulação</span><span class="sxs-lookup"><span data-stu-id="93895-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="93895-179">N/D</span><span class="sxs-lookup"><span data-stu-id="93895-179">N/A</span></span> |
| <span data-ttu-id="93895-180">Eventos de alteração simultânea</span><span class="sxs-lookup"><span data-stu-id="93895-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="93895-181">N/D</span><span class="sxs-lookup"><span data-stu-id="93895-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="93895-182">Definições de configuração</span><span class="sxs-lookup"><span data-stu-id="93895-182">Configuration settings</span></span>
<span data-ttu-id="93895-183">Definições de configuração em serviços de nuvem são definidas para uma função de VM e aplicam tooall instâncias dessa função VM.</span><span class="sxs-lookup"><span data-stu-id="93895-183">Configuration settings in Cloud Services are set for a VM role and apply tooall instances of that VM role.</span></span> <span data-ttu-id="93895-184">Essas configurações são pares chave-valor definidos nos arquivos ServiceConfiguration.*.cscfg e podem ser acessadas diretamente por meio do RoleEnvironment.</span><span class="sxs-lookup"><span data-stu-id="93895-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="93895-185">Na malha do serviço, configurações se aplicam individualmente tooeach serviço e aplicativo tooeach, em vez de tooa VM, como uma máquina virtual pode hospedar vários serviços e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="93895-185">In Service Fabric, settings apply individually tooeach service and tooeach application, rather than tooa VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="93895-186">Um serviço é composto de três pacotes:</span><span class="sxs-lookup"><span data-stu-id="93895-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="93895-187">**Código:** contém os executáveis de serviço hello, binários, DLLs e outros arquivos toorun precisa de um serviço.</span><span class="sxs-lookup"><span data-stu-id="93895-187">**Code:** contains hello service executables, binaries, DLLs, and any other files a service needs toorun.</span></span>
* <span data-ttu-id="93895-188">**Config:** todos os arquivos de configuração e configurações de um serviço.</span><span class="sxs-lookup"><span data-stu-id="93895-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="93895-189">**Dados:** arquivos de dados estáticos associados ao serviço hello.</span><span class="sxs-lookup"><span data-stu-id="93895-189">**Data:** static data files associated with hello service.</span></span>

<span data-ttu-id="93895-190">Cada um desses pacotes pode ter controle de versão e atualização independentes.</span><span class="sxs-lookup"><span data-stu-id="93895-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="93895-191">Serviços de tooCloud semelhante, um pacote de configuração podem ser acessados por meio de programação através de uma API e eventos são serviços de saudação toonotify disponíveis de uma alteração de pacote de configuração.</span><span class="sxs-lookup"><span data-stu-id="93895-191">Similar tooCloud Services, a config package can be accessed programmatically through an API and events are available toonotify hello service of a config package change.</span></span> <span data-ttu-id="93895-192">Um arquivo Settings.xml pode ser usado para configuração de chave-valor e o acesso programático semelhante toohello aplicativo seção configurações de um arquivo App. config.</span><span class="sxs-lookup"><span data-stu-id="93895-192">A Settings.xml file can be used for key-value configuration and programmatic access similar toohello app settings section of an App.config file.</span></span> <span data-ttu-id="93895-193">No entanto, ao contrário dos Serviços de Nuvem, um pacote de configuração do Service Fabric pode conter arquivos de configuração em qualquer formato, seja XML, JSON, YAML ou formato binário personalizado.</span><span class="sxs-lookup"><span data-stu-id="93895-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="93895-194">Acessando configuração</span><span class="sxs-lookup"><span data-stu-id="93895-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="93895-195">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="93895-195">Cloud Services</span></span>
<span data-ttu-id="93895-196">As definições de configuração do ServiceConfiguration.*.cscfg podem ser acessadas por meio do `RoleEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="93895-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="93895-197">Essas configurações são instâncias de função tooall globalmente disponíveis no hello mesma implantação do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="93895-197">These settings are globally available tooall role instances in hello same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="93895-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="93895-198">Service Fabric</span></span>
<span data-ttu-id="93895-199">Cada serviço tem seu próprio pacote de configuração individual.</span><span class="sxs-lookup"><span data-stu-id="93895-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="93895-200">Não há nenhum mecanismo interno para as configurações globais que possa ser acessado por todos os aplicativos em um cluster.</span><span class="sxs-lookup"><span data-stu-id="93895-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="93895-201">Ao usar especial Settings.xml configuração arquivo do Service Fabric dentro de um pacote de configuração, os valores em Settings.xml podem ser substituídos no nível de aplicativo hello, possibilitando a definições de configuração de nível de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="93895-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at hello application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="93895-202">Definições de configuração são acessos dentro de cada instância de serviço por meio do serviço Olá `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="93895-202">Configuration settings are accesses within each service instance through hello service's `CodePackageActivationContext`.</span></span>

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

### <a name="configuration-update-events"></a><span data-ttu-id="93895-203">Eventos de atualização de configuração</span><span class="sxs-lookup"><span data-stu-id="93895-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="93895-204">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="93895-204">Cloud Services</span></span>
<span data-ttu-id="93895-205">Olá `RoleEnvironment.Changed` evento é usada toonotify todas as instâncias de função quando uma alteração ocorre em ambiente de saudação, como uma alteração de configuração.</span><span class="sxs-lookup"><span data-stu-id="93895-205">hello `RoleEnvironment.Changed` event is used toonotify all role instances when a change occurs in hello environment, such as a configuration change.</span></span> <span data-ttu-id="93895-206">Isso é usado tooconsume atualizações de configuração sem reciclar instâncias de função ou reiniciar um processo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="93895-206">This is used tooconsume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="93895-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="93895-207">Service Fabric</span></span>
<span data-ttu-id="93895-208">Cada um dos três tipos de pacote hello em um serviço de código, configuração e dados - ter eventos notificam uma instância de serviço quando um pacote é atualizado, adicionado ou removido.</span><span class="sxs-lookup"><span data-stu-id="93895-208">Each of hello three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="93895-209">Um serviço pode conter vários pacotes de cada tipo.</span><span class="sxs-lookup"><span data-stu-id="93895-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="93895-210">Por exemplo, um serviço pode ter vários pacotes de configuração, cada um deles com controle de versão e atualização individuais.</span><span class="sxs-lookup"><span data-stu-id="93895-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="93895-211">Esses eventos são alterações tooconsume disponíveis em pacotes de serviço sem reiniciar a instância do serviço hello.</span><span class="sxs-lookup"><span data-stu-id="93895-211">These events are available tooconsume changes in service packages without restarting hello service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="93895-212">Tarefas de inicialização</span><span class="sxs-lookup"><span data-stu-id="93895-212">Startup tasks</span></span>
<span data-ttu-id="93895-213">As tarefas de inicialização são ações executadas antes de um aplicativo ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="93895-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="93895-214">Uma tarefa de inicialização é normalmente usada toorun scripts de instalação usando privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="93895-214">A startup task is typically used toorun setup scripts using elevated privileges.</span></span> <span data-ttu-id="93895-215">Os Serviços de Nuvem e o Service Fabric dão suporte a tarefas de inicialização.</span><span class="sxs-lookup"><span data-stu-id="93895-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="93895-216">Olá principal diferença é que os serviços em nuvem, uma tarefa de inicialização é tooa empatado VM porque ela é parte de uma instância de função, enquanto na malha do serviço de uma tarefa de inicialização é serviço tooa associado, que não está associado tooany VM específica.</span><span class="sxs-lookup"><span data-stu-id="93895-216">hello main difference is that in Cloud Services, a startup task is tied tooa VM because it is part of a role instance, whereas in Service Fabric a startup task is tied tooa service, which is not tied tooany particular VM.</span></span>

| <span data-ttu-id="93895-217">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="93895-217">Cloud Services</span></span> | <span data-ttu-id="93895-218">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="93895-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="93895-219">Configuração local</span><span class="sxs-lookup"><span data-stu-id="93895-219">Configuration location</span></span> |<span data-ttu-id="93895-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="93895-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="93895-221">Privilégios</span><span class="sxs-lookup"><span data-stu-id="93895-221">Privileges</span></span> |<span data-ttu-id="93895-222">"limitados" ou "elevados"</span><span class="sxs-lookup"><span data-stu-id="93895-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="93895-223">Sequenciamento</span><span class="sxs-lookup"><span data-stu-id="93895-223">Sequencing</span></span> |<span data-ttu-id="93895-224">"simples", "em segundo plano", "primeiro plano"</span><span class="sxs-lookup"><span data-stu-id="93895-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="93895-225">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="93895-225">Cloud Services</span></span>
<span data-ttu-id="93895-226">Nos Serviços de Nuvem, um ponto de entrada de inicialização é configurado por função em ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="93895-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

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

### <a name="service-fabric"></a><span data-ttu-id="93895-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="93895-227">Service Fabric</span></span>
<span data-ttu-id="93895-228">No Service Fabric, um ponto de entrada de inicialização é configurado por serviço em ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="93895-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

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

## <a name="a-note-about-development-environment"></a><span data-ttu-id="93895-229">Uma observação sobre o ambiente de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="93895-229">A note about development environment</span></span>
<span data-ttu-id="93895-230">Serviços de nuvem e malha do serviço são integrados com o Visual Studio com suporte para depuração, configurar e implantar as localmente e modelos de projeto e tooAzure.</span><span class="sxs-lookup"><span data-stu-id="93895-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and tooAzure.</span></span> <span data-ttu-id="93895-231">Os Serviços de Nuvem e o Service Fabric também fornecem um ambiente de tempo de execução de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="93895-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="93895-232">Olá diferença é que enquanto o serviço de nuvem que emula o tempo de execução de desenvolvimento Olá Olá ambiente do Azure no qual ele é executado, Service Fabric não usa um emulador: usa Olá completa do Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="93895-232">hello difference is that while hello Cloud Service development runtime emulates hello Azure environment on which it runs, Service Fabric does not use an emulator - it uses hello complete Service Fabric runtime.</span></span> <span data-ttu-id="93895-233">Olá, é executado no computador de desenvolvimento local do ambiente do Service Fabric Olá mesmo ambiente que é executado em produção.</span><span class="sxs-lookup"><span data-stu-id="93895-233">hello Service Fabric environment you run on your local development machine is hello same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93895-234">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="93895-234">Next steps</span></span>
<span data-ttu-id="93895-235">Leia mais sobre serviços confiáveis do serviço de malha e diferenças fundamentais de saudação entre serviços de nuvem e toounderstand de arquitetura de aplicativo do Service Fabric como tootake aproveitar Olá completo conjunto de recursos de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="93895-235">Read more about Service Fabric Reliable Services and hello fundamental differences between Cloud Services and Service Fabric application architecture toounderstand how tootake advantage of hello full set of Service Fabric features.</span></span>

* [<span data-ttu-id="93895-236">Introdução aos Reliable Services do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="93895-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="93895-237">Diferenças de toohello guia conceitual entre os serviços de nuvem e do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="93895-237">Conceptual guide toohello differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
