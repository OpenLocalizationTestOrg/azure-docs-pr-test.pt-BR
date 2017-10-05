---
title: "Versão prévia do Docker Compose do Azure Service Fabric"
description: "O Azure Service Fabric aceita o formato do Docker Compose para facilitar a orquestração dos contêineres existentes usando o Service Fabric. No momento, esse suporte está na versão prévia."
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
ms.openlocfilehash: e05d1a3d6111e3bbc34008226bcd1fdf35935450
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="a452d-104">Suporte ao aplicativo Docker Compose no Azure Service Fabric (Versão prévia)</span><span class="sxs-lookup"><span data-stu-id="a452d-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="a452d-105">O docker usa o arquivo [docker-compose.yml](https://docs.docker.com/compose) para definir aplicativos de vários contêineres.</span><span class="sxs-lookup"><span data-stu-id="a452d-105">Docker uses the [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="a452d-106">A fim de facilitar para os clientes familiarizados com o Docker orquestrarem aplicativos de contêiner existentes no Azure Service Fabric, incluímos o suporte da versão prévia para o Docker Compose nativamente na plataforma.</span><span class="sxs-lookup"><span data-stu-id="a452d-106">To make it easy for customers familiar with Docker to orchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in the platform.</span></span> <span data-ttu-id="a452d-107">O Service Fabric pode aceitar a versão 3 e posteriores de arquivos `docker-compose.yml`.</span><span class="sxs-lookup"><span data-stu-id="a452d-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="a452d-108">Como esse suporte está na versão prévia, há suporte para apenas um subconjunto de diretivas do Compose.</span><span class="sxs-lookup"><span data-stu-id="a452d-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="a452d-109">Por exemplo, não há suporte para atualizações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a452d-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="a452d-110">No entanto, você sempre pode remover e implantar aplicativos em vez de atualizá-los.</span><span class="sxs-lookup"><span data-stu-id="a452d-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="a452d-111">Para usar essa versão prévia, crie o cluster com a versão 5.7 ou superior do tempo de execução do Service Fabric por meio do portal do Azure junto com o SDK correspondente.</span><span class="sxs-lookup"><span data-stu-id="a452d-111">To use this preview, create your cluster with version 5.7 or greater of the Service Fabric runtime through the Azure portal along with the corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="a452d-112">Esse recurso está na versão prévia e não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="a452d-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="a452d-113">Implantar um arquivo do Docker Compose no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a452d-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="a452d-114">Os seguintes comandos criam um aplicativo do Service Fabric (chamado `fabric:/TestContainerApp` no exemplo anterior) que você pode monitorar e gerenciar da mesma forma que qualquer outro aplicativo do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a452d-114">The following commands create a Service Fabric application (named `fabric:/TestContainerApp` in the preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="a452d-115">Você pode usar o nome do aplicativo especificado para consultas de integridade.</span><span class="sxs-lookup"><span data-stu-id="a452d-115">You can use the specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="a452d-116">Usar o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a452d-116">Use PowerShell</span></span>

<span data-ttu-id="a452d-117">Crie um aplicativo do Compose do Service Fabric por meio de um arquivo docker-compose.yml, executando o seguinte comando no PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a452d-117">Create a Service Fabric Compose application from a docker-compose.yml file by running the following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="a452d-118">`RegistryUserName` e `RegistryPassword` se referem ao nome de usuário e senha de registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="a452d-118">`RegistryUserName` and `RegistryPassword` refer to the container registry username and password.</span></span> <span data-ttu-id="a452d-119">Depois de concluir o aplicativo, você pode verificar seu status usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a452d-119">After you've completed the application, you can check its status by using the following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="a452d-120">Para excluir o aplicativo do Compose por meio do PowerShell, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a452d-120">To delete the Compose application through PowerShell, use the following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="a452d-121">Usar a CLI do Azure Service Fabric (sfctl)</span><span class="sxs-lookup"><span data-stu-id="a452d-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="a452d-122">Como alternativa, você pode usar o seguinte comando da CLI do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="a452d-122">Alternatively, you can use the following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="a452d-123">Depois de criar o aplicativo, você pode verificar seu status usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a452d-123">After you've created the application, you can check its status by using the following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="a452d-124">Para excluir o aplicativo do Compose, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a452d-124">To delete the Compose application, use the following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="a452d-125">Diretivas do Compose com suporte</span><span class="sxs-lookup"><span data-stu-id="a452d-125">Supported Compose directives</span></span>

<span data-ttu-id="a452d-126">Esta versão prévia dá suporte a um subconjunto das opções de configuração do formato da versão 3 do Compose, incluindo os primitivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a452d-126">This preview supports a subset of the configuration options from the Compose version 3 format, including the following primitives:</span></span>

* <span data-ttu-id="a452d-127">Serviços > Implantar > Réplicas</span><span class="sxs-lookup"><span data-stu-id="a452d-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="a452d-128">Serviços > Implantar > Posicionamento > Restrições</span><span class="sxs-lookup"><span data-stu-id="a452d-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="a452d-129">Serviços > Implantar > Recursos > Limites</span><span class="sxs-lookup"><span data-stu-id="a452d-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="a452d-130">-cpu-shares</span><span class="sxs-lookup"><span data-stu-id="a452d-130">-cpu-shares</span></span>
    * <span data-ttu-id="a452d-131">-memory</span><span class="sxs-lookup"><span data-stu-id="a452d-131">-memory</span></span>
    * <span data-ttu-id="a452d-132">-memory-swap</span><span class="sxs-lookup"><span data-stu-id="a452d-132">-memory-swap</span></span>
* <span data-ttu-id="a452d-133">Serviços > Comandos</span><span class="sxs-lookup"><span data-stu-id="a452d-133">Services > Commands</span></span>
* <span data-ttu-id="a452d-134">Serviços > Ambiente</span><span class="sxs-lookup"><span data-stu-id="a452d-134">Services > Environment</span></span>
* <span data-ttu-id="a452d-135">Serviços > Portas</span><span class="sxs-lookup"><span data-stu-id="a452d-135">Services > Ports</span></span>
* <span data-ttu-id="a452d-136">Serviços > Imagem</span><span class="sxs-lookup"><span data-stu-id="a452d-136">Services > Image</span></span>
* <span data-ttu-id="a452d-137">Serviços > Isolamento (somente para Windows)</span><span class="sxs-lookup"><span data-stu-id="a452d-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="a452d-138">Serviços > Registro em log > Driver</span><span class="sxs-lookup"><span data-stu-id="a452d-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="a452d-139">Serviços > Registro em log > Driver > Opções</span><span class="sxs-lookup"><span data-stu-id="a452d-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="a452d-140">Volume e Implantar > Volume</span><span class="sxs-lookup"><span data-stu-id="a452d-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="a452d-141">Configure o cluster para impor limites de recursos, conforme descrito na [Governança de recursos do Service Fabric](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="a452d-141">Set up the cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="a452d-142">Todas as outras diretivas do Docker Compose não têm suporte nessa versão prévia.</span><span class="sxs-lookup"><span data-stu-id="a452d-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="a452d-143">Computação de ServiceDnsName</span><span class="sxs-lookup"><span data-stu-id="a452d-143">ServiceDnsName computation</span></span>

<span data-ttu-id="a452d-144">Se o nome do serviço que você especifica em um arquivo do Compose é um nome de domínio totalmente qualificado (isto é, contem um ponto, [.]), o nome DNS registrado pelo Service Fabric será `<ServiceName>` (incluindo o ponto).</span><span class="sxs-lookup"><span data-stu-id="a452d-144">If the service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), the DNS name registered by Service Fabric is `<ServiceName>` (including the dot).</span></span> <span data-ttu-id="a452d-145">Caso contrário, cada segmento de caminho no nome de aplicativo se tornará um rótulo de domínio no nome DNS do serviço com o primeiro segmento de caminho se tornando o rótulo de domínio primário.</span><span class="sxs-lookup"><span data-stu-id="a452d-145">If not, each path segment in the application name becomes a domain label in the service DNS name, with the first path segment becoming the top-level domain label.</span></span>

<span data-ttu-id="a452d-146">Por exemplo, se o nome especificado do aplicativo for `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` seria o nome DNS registrado.</span><span class="sxs-lookup"><span data-stu-id="a452d-146">For example, if the specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be the registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="a452d-147">Diferenças entre o modelo de aplicativo do Compose (definição de instância) e do Service Fabric (definição de tipo)</span><span class="sxs-lookup"><span data-stu-id="a452d-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="a452d-148">Um arquivo docker-compose.yml descreve um conjunto de contêineres implantável, incluindo suas propriedades e configurações.</span><span class="sxs-lookup"><span data-stu-id="a452d-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="a452d-149">Por exemplo, o arquivo pode conter variáveis de ambiente e portas.</span><span class="sxs-lookup"><span data-stu-id="a452d-149">For example, the file can contain environment variables and ports.</span></span> <span data-ttu-id="a452d-150">Você também pode especificar parâmetros de implantação, como restrições de posicionamento, limites de recursos e nomes DNS, no arquivo docker-compose.yml.</span><span class="sxs-lookup"><span data-stu-id="a452d-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in the docker-compose.yml file.</span></span>

<span data-ttu-id="a452d-151">O [modelo de aplicativo do Service Fabric](service-fabric-application-model.md) usa tipos de serviço e tipos de aplicativo, em que é possível ter várias instâncias de aplicativo do mesmo tipo.</span><span class="sxs-lookup"><span data-stu-id="a452d-151">The [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of the same type.</span></span> <span data-ttu-id="a452d-152">Por exemplo, você pode ter uma instância de aplicativo por cliente.</span><span class="sxs-lookup"><span data-stu-id="a452d-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="a452d-153">Esse modelo baseado em tipo dá suporte a várias versões do mesmo tipo de aplicativo que é registrado com o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="a452d-153">This type-based model supports multiple versions of the same application type that's registered with the runtime.</span></span>

<span data-ttu-id="a452d-154">Por exemplo, o cliente A pode ter um aplicativo instanciado com tipo 1.0 do AppTypeA e o cliente B pode ter outro aplicativo instanciado com o mesmo tipo e versão.</span><span class="sxs-lookup"><span data-stu-id="a452d-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with the same type and version.</span></span> <span data-ttu-id="a452d-155">Você define os tipos de aplicativos nos manifestos do aplicativo e especifica os parâmetros de nome e implantação do aplicativo ao criar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a452d-155">You define the application types in the application manifests, and you specify the application name and deployment parameters when you create the application.</span></span>

<span data-ttu-id="a452d-156">Embora esse modelo ofereça flexibilidade, também estamos planejando dar suporte a um modelo de implantação baseado em instâncias mais simples em que os tipos são implícitos no arquivo de manifesto.</span><span class="sxs-lookup"><span data-stu-id="a452d-156">Although this model offers flexibility, we are also planning to support a simpler, instance-based deployment model where types are implicit from the manifest file.</span></span> <span data-ttu-id="a452d-157">Nesse modelo, cada aplicativo obtém seu próprio manifesto independente.</span><span class="sxs-lookup"><span data-stu-id="a452d-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="a452d-158">Estamos fazendo a versão prévia desse esforço adicionando suporte para o docker-compose.yml, que é um formato de implantação baseado em instância.</span><span class="sxs-lookup"><span data-stu-id="a452d-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a452d-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a452d-159">Next steps</span></span>

* <span data-ttu-id="a452d-160">Leia sobre o [modelo de aplicativo do Service Fabric](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="a452d-160">Read up on the [Service Fabric application model](service-fabric-application-model.md)</span></span>
* [<span data-ttu-id="a452d-161">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a452d-161">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)
