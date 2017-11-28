---
title: "aaaAzure compor visualização do Service Fabric Docker"
description: "Malha do Azure do serviço aceita Docker compor formato toomake-lo mais fácil contêineres existentes tooorchestrate usando o Service Fabric. No momento, esse suporte está na versão prévia."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="99282-104">Suporte ao aplicativo Docker Compose no Azure Service Fabric (Versão prévia)</span><span class="sxs-lookup"><span data-stu-id="99282-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="99282-105">Docker usa Olá [docker compose.yml](https://docs.docker.com/compose) arquivo para definir o contêiner de vários aplicativos.</span><span class="sxs-lookup"><span data-stu-id="99282-105">Docker uses hello [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="99282-106">toomake-fácil para os clientes familiarizados com o Docker tooorchestrate contêiner aplicativos existentes no Azure Service Fabric, incluímos suporte para compor Docker visualização nativamente na plataforma de saudação.</span><span class="sxs-lookup"><span data-stu-id="99282-106">toomake it easy for customers familiar with Docker tooorchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in hello platform.</span></span> <span data-ttu-id="99282-107">O Service Fabric pode aceitar a versão 3 e posteriores de arquivos `docker-compose.yml`.</span><span class="sxs-lookup"><span data-stu-id="99282-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="99282-108">Como esse suporte está na versão prévia, há suporte para apenas um subconjunto de diretivas do Compose.</span><span class="sxs-lookup"><span data-stu-id="99282-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="99282-109">Por exemplo, não há suporte para atualizações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99282-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="99282-110">No entanto, você sempre pode remover e implantar aplicativos em vez de atualizá-los.</span><span class="sxs-lookup"><span data-stu-id="99282-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="99282-111">toouse visualizar, criar o cluster com a versão 5.7 ou superior do tempo de execução do Service Fabric Olá por meio de saudação portal do Azure junto com hello correspondente SDK.</span><span class="sxs-lookup"><span data-stu-id="99282-111">toouse this preview, create your cluster with version 5.7 or greater of hello Service Fabric runtime through hello Azure portal along with hello corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="99282-112">Esse recurso está na versão prévia e não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="99282-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="99282-113">Implantar um arquivo do Docker Compose no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="99282-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="99282-114">Olá, comandos a seguir criam um aplicativo de malha do serviço (denominado `fabric:/TestContainerApp` em Olá anterior exemplo), que você pode monitorar e gerenciar como qualquer outro aplicativo de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="99282-114">hello following commands create a Service Fabric application (named `fabric:/TestContainerApp` in hello preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="99282-115">Você pode usar o nome do aplicativo especificado Olá para consultas de integridade.</span><span class="sxs-lookup"><span data-stu-id="99282-115">You can use hello specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="99282-116">Usar o PowerShell</span><span class="sxs-lookup"><span data-stu-id="99282-116">Use PowerShell</span></span>

<span data-ttu-id="99282-117">Crie um aplicativo de serviço compor de malha de um arquivo de docker compose.yml executando Olá comando do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="99282-117">Create a Service Fabric Compose application from a docker-compose.yml file by running hello following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="99282-118">`RegistryUserName`e `RegistryPassword` consulte toohello contêiner do registro username e password.</span><span class="sxs-lookup"><span data-stu-id="99282-118">`RegistryUserName` and `RegistryPassword` refer toohello container registry username and password.</span></span> <span data-ttu-id="99282-119">Depois que você tiver concluído o aplicativo hello, você pode verificar seu status usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="99282-119">After you've completed hello application, you can check its status by using hello following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="99282-120">toodelete Olá compor aplicativos por meio do PowerShell, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="99282-120">toodelete hello Compose application through PowerShell, use hello following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="99282-121">Usar a CLI do Azure Service Fabric (sfctl)</span><span class="sxs-lookup"><span data-stu-id="99282-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="99282-122">Como alternativa, você pode usar o hello CLI de malha do serviço de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="99282-122">Alternatively, you can use hello following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="99282-123">Depois que você criou um aplicativo hello, você pode verificar seu status usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="99282-123">After you've created hello application, you can check its status by using hello following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="99282-124">Olá toodelete compor aplicativos, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="99282-124">toodelete hello Compose application, use hello following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="99282-125">Diretivas do Compose com suporte</span><span class="sxs-lookup"><span data-stu-id="99282-125">Supported Compose directives</span></span>

<span data-ttu-id="99282-126">Esta visualização dá suporte a um subconjunto das opções de configuração de saudação do formato de versão 3 redigir hello, incluindo Olá primitivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="99282-126">This preview supports a subset of hello configuration options from hello Compose version 3 format, including hello following primitives:</span></span>

* <span data-ttu-id="99282-127">Serviços > Implantar > Réplicas</span><span class="sxs-lookup"><span data-stu-id="99282-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="99282-128">Serviços > Implantar > Posicionamento > Restrições</span><span class="sxs-lookup"><span data-stu-id="99282-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="99282-129">Serviços > Implantar > Recursos > Limites</span><span class="sxs-lookup"><span data-stu-id="99282-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="99282-130">-cpu-shares</span><span class="sxs-lookup"><span data-stu-id="99282-130">-cpu-shares</span></span>
    * <span data-ttu-id="99282-131">-memory</span><span class="sxs-lookup"><span data-stu-id="99282-131">-memory</span></span>
    * <span data-ttu-id="99282-132">-memory-swap</span><span class="sxs-lookup"><span data-stu-id="99282-132">-memory-swap</span></span>
* <span data-ttu-id="99282-133">Serviços > Comandos</span><span class="sxs-lookup"><span data-stu-id="99282-133">Services > Commands</span></span>
* <span data-ttu-id="99282-134">Serviços > Ambiente</span><span class="sxs-lookup"><span data-stu-id="99282-134">Services > Environment</span></span>
* <span data-ttu-id="99282-135">Serviços > Portas</span><span class="sxs-lookup"><span data-stu-id="99282-135">Services > Ports</span></span>
* <span data-ttu-id="99282-136">Serviços > Imagem</span><span class="sxs-lookup"><span data-stu-id="99282-136">Services > Image</span></span>
* <span data-ttu-id="99282-137">Serviços > Isolamento (somente para Windows)</span><span class="sxs-lookup"><span data-stu-id="99282-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="99282-138">Serviços > Registro em log > Driver</span><span class="sxs-lookup"><span data-stu-id="99282-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="99282-139">Serviços > Registro em log > Driver > Opções</span><span class="sxs-lookup"><span data-stu-id="99282-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="99282-140">Volume e Implantar > Volume</span><span class="sxs-lookup"><span data-stu-id="99282-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="99282-141">Configurar o cluster Olá para impor limites de recurso, conforme descrito em [governança de recursos de malha do serviço](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="99282-141">Set up hello cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="99282-142">Todas as outras diretivas do Docker Compose não têm suporte nessa versão prévia.</span><span class="sxs-lookup"><span data-stu-id="99282-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="99282-143">Computação de ServiceDnsName</span><span class="sxs-lookup"><span data-stu-id="99282-143">ServiceDnsName computation</span></span>

<span data-ttu-id="99282-144">Se o nome do serviço Olá que você especificar em um arquivo de composição é um nome de domínio totalmente qualificado (ou seja, ele contém um ponto [.]), nome DNS Olá registrado pelo Service Fabric é `<ServiceName>` (incluindo ponto Olá).</span><span class="sxs-lookup"><span data-stu-id="99282-144">If hello service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), hello DNS name registered by Service Fabric is `<ServiceName>` (including hello dot).</span></span> <span data-ttu-id="99282-145">Caso contrário, cada segmento de caminho no nome do aplicativo hello se torna um rótulo de domínio no nome DNS do serviço hello, com hello primeiro segmento de caminho se torne o rótulo de domínio de nível superior de saudação.</span><span class="sxs-lookup"><span data-stu-id="99282-145">If not, each path segment in hello application name becomes a domain label in hello service DNS name, with hello first path segment becoming hello top-level domain label.</span></span>

<span data-ttu-id="99282-146">Por exemplo, se Olá especificado o nome do aplicativo é `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` seria Olá nome DNS registrado.</span><span class="sxs-lookup"><span data-stu-id="99282-146">For example, if hello specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be hello registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="99282-147">Diferenças entre o modelo de aplicativo do Compose (definição de instância) e do Service Fabric (definição de tipo)</span><span class="sxs-lookup"><span data-stu-id="99282-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="99282-148">Um arquivo docker-compose.yml descreve um conjunto de contêineres implantável, incluindo suas propriedades e configurações.</span><span class="sxs-lookup"><span data-stu-id="99282-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="99282-149">Por exemplo, o arquivo hello pode conter variáveis de ambiente e portas.</span><span class="sxs-lookup"><span data-stu-id="99282-149">For example, hello file can contain environment variables and ports.</span></span> <span data-ttu-id="99282-150">Você também pode especificar parâmetros de implantação, como restrições de posicionamento, limites de recursos e nomes DNS, no arquivo de docker compose.yml hello.</span><span class="sxs-lookup"><span data-stu-id="99282-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in hello docker-compose.yml file.</span></span>

<span data-ttu-id="99282-151">Olá [o modelo de aplicativo do Service Fabric](service-fabric-application-model.md) usa tipos de serviço e aplicativo, onde você pode ter muitas instâncias de aplicativo do hello mesmo tipo.</span><span class="sxs-lookup"><span data-stu-id="99282-151">hello [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of hello same type.</span></span> <span data-ttu-id="99282-152">Por exemplo, você pode ter uma instância de aplicativo por cliente.</span><span class="sxs-lookup"><span data-stu-id="99282-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="99282-153">Esse modelo baseado em tipo oferece suporte a várias versões do hello mesmo tipo de aplicativo que está registrado com o tempo de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="99282-153">This type-based model supports multiple versions of hello same application type that's registered with hello runtime.</span></span>

<span data-ttu-id="99282-154">Por exemplo, o cliente pode ter um aplicativo instanciado com tipo 1.0 de AppTypeA e cliente B pode ter outro aplicativo instanciado com hello mesmo tipo e versão.</span><span class="sxs-lookup"><span data-stu-id="99282-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with hello same type and version.</span></span> <span data-ttu-id="99282-155">Definir tipos de aplicativo hello nos manifestos de aplicativo hello e você especificar parâmetros de nome e a implantação de aplicativo hello quando você cria o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="99282-155">You define hello application types in hello application manifests, and you specify hello application name and deployment parameters when you create hello application.</span></span>

<span data-ttu-id="99282-156">Embora esse modelo oferece flexibilidade, também planejamos toosupport um modelo de implantação mais simples, com base em instância onde os tipos são implícita do arquivo de manifesto hello.</span><span class="sxs-lookup"><span data-stu-id="99282-156">Although this model offers flexibility, we are also planning toosupport a simpler, instance-based deployment model where types are implicit from hello manifest file.</span></span> <span data-ttu-id="99282-157">Nesse modelo, cada aplicativo obtém seu próprio manifesto independente.</span><span class="sxs-lookup"><span data-stu-id="99282-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="99282-158">Estamos fazendo a versão prévia desse esforço adicionando suporte para o docker-compose.yml, que é um formato de implantação baseado em instância.</span><span class="sxs-lookup"><span data-stu-id="99282-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99282-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="99282-159">Next steps</span></span>

* <span data-ttu-id="99282-160">Leia sobre Olá [modelo de aplicativo do Service Fabric](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="99282-160">Read up on hello [Service Fabric application model](service-fabric-application-model.md)</span></span>
* [<span data-ttu-id="99282-161">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="99282-161">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)
