---
title: "Dimensionamento programático do Azure Service Fabric | Microsoft Docs"
description: "Dimensionar um cluster do Azure Service Fabric para expandi-lo ou reduzi-lo por meio de programação de acordo com gatilhos personalizados"
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: mikerou
ms.openlocfilehash: 46b0b62f92abbac57bc27bbcdd5821eafedf5519
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="be0be-103">Dimensionar um cluster do Service Fabric por meio de programação</span><span class="sxs-lookup"><span data-stu-id="be0be-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="be0be-104">Os conceitos básicos do dimensionamento de um cluster do Azure Service Fabric são abordados na documentação sobre [dimensionamento de cluster](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="be0be-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="be0be-105">Esse artigo aborda como clusters do Service Fabric são criados em cima de conjuntos de dimensionamento de máquinas virtuais e podem ser dimensionados manualmente ou com regras de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="be0be-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="be0be-106">Este documento examina métodos programáticos de coordenação das operações de dimensionamento do Azure para cenários mais avançados.</span><span class="sxs-lookup"><span data-stu-id="be0be-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="be0be-107">Razões para um dimensionamento programático</span><span class="sxs-lookup"><span data-stu-id="be0be-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="be0be-108">Em muitos cenários, o dimensionamento manual ou por meio de regras de dimensionamento automático é uma boas solução.</span><span class="sxs-lookup"><span data-stu-id="be0be-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="be0be-109">Em outros cenários, no entanto, ele pode não ser adequado.</span><span class="sxs-lookup"><span data-stu-id="be0be-109">In other scenarios, though, they may not be the right fit.</span></span> <span data-ttu-id="be0be-110">As desvantagens desses métodos incluem:</span><span class="sxs-lookup"><span data-stu-id="be0be-110">Potential drawbacks to these approaches include:</span></span>

- <span data-ttu-id="be0be-111">O dimensionamento manual requer que você faça logon e solicite as operações de dimensionamento explicitamente.</span><span class="sxs-lookup"><span data-stu-id="be0be-111">Manually scaling requires you to log in and explicitly request scaling operations.</span></span> <span data-ttu-id="be0be-112">Se as operações de dimensionamento são necessárias com frequência ou em momentos imprevisíveis, essa abordagem não pode ser uma boa solução.</span><span class="sxs-lookup"><span data-stu-id="be0be-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="be0be-113">Quando as regras de dimensionamento automático removem uma instância de um conjunto de dimensionamento de máquinas virtuais, elas não removem o conhecimento do nó do cluster do Service Fabric associado, a menos que o tipo de nó tenha um nível de durabilidade de Prata ou Ouro.</span><span class="sxs-lookup"><span data-stu-id="be0be-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from the associated Service Fabric cluster unless the node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="be0be-114">Como as regras de dimensionamento automático funcionam no nível do conjunto de dimensionamento (em vez do nível do Service Fabric), elas podem remover nós do Service Fabric sem desligá-lo normalmente.</span><span class="sxs-lookup"><span data-stu-id="be0be-114">Because auto-scale rules work at the scale set level (rather than at the Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="be0be-115">Essa remoção de nó sem maiores cuidados deixará um estado do nó do Service Fabric “fantasma” de rastro após as operações de redução horizontal.</span><span class="sxs-lookup"><span data-stu-id="be0be-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="be0be-116">Uma pessoa (ou um serviço) precisaria limpar periodicamente o estado do nó removido no cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="be0be-116">An individual (or a service) would need to periodically clean up removed node state in the Service Fabric cluster.</span></span>
  - <span data-ttu-id="be0be-117">Observe que um tipo de nó com um nível de durabilidade Ouro ou Prata limpará os nós removidos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="be0be-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="be0be-118">Embora haja [várias métricas](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) com suporte pelas regras de dimensionamento automático, o conjunto ainda é limitado.</span><span class="sxs-lookup"><span data-stu-id="be0be-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="be0be-119">Se seu cenário exigir dimensionamento com base em alguma métrica não abordada no conjunto, as regras de dimensionamento automático podem não ser uma boa opção.</span><span class="sxs-lookup"><span data-stu-id="be0be-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="be0be-120">Com base nessas limitações, convém implementar mais modelos de dimensionamento personalizados.</span><span class="sxs-lookup"><span data-stu-id="be0be-120">Based on these limitations, you may wish to implement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="be0be-121">Dimensionando APIs</span><span class="sxs-lookup"><span data-stu-id="be0be-121">Scaling APIs</span></span>
<span data-ttu-id="be0be-122">Existem APIs do Azure que permitem aos aplicativos trabalhar com conjuntos de dimensionamento de máquinas virtuais e clusters do Service Fabric por meio de programação.</span><span class="sxs-lookup"><span data-stu-id="be0be-122">Azure APIs exist which allow applications to programmatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="be0be-123">Se as opções de dimensionamento automático existentes não funcionam em seu cenário, essas APIs possibilitam a implementação de lógica de dimensionamento personalizada.</span><span class="sxs-lookup"><span data-stu-id="be0be-123">If existing auto-scale options don't work for your scenario, these APIs make it possible to implement custom scaling logic.</span></span> 

<span data-ttu-id="be0be-124">Uma abordagem para implementar essa funcionalidade de dimensionamento automático “caseira” é adicionar um novo serviço sem estado ao aplicativo do Service Fabric para gerenciar operações de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="be0be-124">One approach to implementing this 'home-made' auto-scaling functionality is to add a new stateless service to the Service Fabric application to manage scaling operations.</span></span> <span data-ttu-id="be0be-125">No método `RunAsync` do serviço, um conjunto de disparadores pode determinar se o dimensionamento é necessário (inclusive verificando parâmetros como o tamanho máximo do cluster e o dimensionamento de cooldowns).</span><span class="sxs-lookup"><span data-stu-id="be0be-125">Within the service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="be0be-126">A API usada para interações de conjunto de dimensionamento de máquinas virtuais (tanto para verificar o número atual de instâncias da máquina virtual quanto para modificá-lo) é a [biblioteca de computação do Gerenciamento do Azure fluente](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span><span class="sxs-lookup"><span data-stu-id="be0be-126">The API used for virtual machine scale set interactions (both to check the current number of virtual machine instances and to modify it) is the [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="be0be-127">A biblioteca de computação fluente fornece uma API fácil de usar para interagir com conjuntos de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="be0be-127">The fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="be0be-128">Para interagir com o próprio cluster do Service Fabric, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="be0be-128">To interact with the Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="be0be-129">É claro que o código de dimensionamento não precisa ser executado como um serviço no cluster para ser dimensionado.</span><span class="sxs-lookup"><span data-stu-id="be0be-129">Of course, the scaling code doesn't need to run as a service in the cluster to be scaled.</span></span> <span data-ttu-id="be0be-130">Tanto o `IAzure` quanto o `FabricClient` podem se conectar aos recursos do Azure associados remotamente e, portanto, o serviço de dimensionamento pode facilmente ser um aplicativo de console ou serviço do Windows executado de fora do aplicativo do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="be0be-130">Both `IAzure` and `FabricClient` can connect to their associated Azure resources remotely, so the scaling service could easily be a console application or Windows service running from outside the Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="be0be-131">Gerenciamento de credenciais</span><span class="sxs-lookup"><span data-stu-id="be0be-131">Credential management</span></span>
<span data-ttu-id="be0be-132">Um desafio de se escrever um serviço para manipular o dimensionamento é que o serviço deve ser capaz de acessar recursos do conjunto de dimensionamento de máquinas virtuais sem um logon interativo.</span><span class="sxs-lookup"><span data-stu-id="be0be-132">One challenge of writing a service to handle scaling is that the service must be able to access virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="be0be-133">O acesso ao cluster do Service Fabric é fácil se o serviço de dimensionamento está modificando seu próprio aplicativo do Service Fabric, mas as credenciais são exigidas para acessar o conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="be0be-133">Accessing the Service Fabric cluster is easy if the scaling service is modifying its own Service Fabric application, but credentials are needed to access the scale set.</span></span> <span data-ttu-id="be0be-134">Para fazer logon, você pode usar uma [entidade de serviço](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) criada com a [CLI do Azure 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="be0be-134">To log in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with the [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="be0be-135">Uma entidade de serviço pode ser criada com as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="be0be-135">A service principal can be created with the following steps:</span></span>

1. <span data-ttu-id="be0be-136">Faça logon na CLI do Azure (`az login`) como um usuário com acesso ao conjunto de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="be0be-136">Log in to the Azure CLI (`az login`) as a user with access to the virtual machine scale set</span></span>
2. <span data-ttu-id="be0be-137">Crie a entidade de serviço com `az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="be0be-137">Create the service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="be0be-138">Anote o appId (chamado de ‘ID do cliente’ em outros lugares), o nome, a senha e o locatário para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="be0be-138">Make note of the appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="be0be-139">Você também precisará da sua ID de assinatura, que pode ser exibida com `az account list`</span><span class="sxs-lookup"><span data-stu-id="be0be-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="be0be-140">A biblioteca de computação fluente pode fazer logon usando essas credenciais da seguinte maneira (observe que os tipos de núcleo fluente do Azure como `IAzure` estão no pacote [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/)):</span><span class="sxs-lookup"><span data-stu-id="be0be-140">The fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in the [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

```C#
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed to login to Azure");
}
```

<span data-ttu-id="be0be-141">Depois da conexão, a contagem de instâncias do conjunto de dimensionamento pode ser consultada por meio de `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="be0be-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="be0be-142">Expansão</span><span class="sxs-lookup"><span data-stu-id="be0be-142">Scaling out</span></span>
<span data-ttu-id="be0be-143">Usando o SDK de computação do Azure fluente, instâncias podem ser adicionadas ao conjunto de dimensionamento de máquinas virtuais com apenas algumas chamadas-</span><span class="sxs-lookup"><span data-stu-id="be0be-143">Using the fluent Azure compute SDK, instances can be added to the virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="be0be-144">Como alternativa, o tamanho do conjunto de dimensionamento de máquinas virtuais também pode ser gerenciado com os cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be0be-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="be0be-145">O [`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) pode recuperar o objeto do conjunto de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="be0be-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve the virtual machine scale set object.</span></span> <span data-ttu-id="be0be-146">A capacidade atual será armazenada na propriedade `.sku.capacity`.</span><span class="sxs-lookup"><span data-stu-id="be0be-146">The current capacity will be stored in the `.sku.capacity` property.</span></span> <span data-ttu-id="be0be-147">Depois de alterar a capacidade para o valor desejado, o conjunto de dimensionamento de máquinas virtuais do Azure pode ser atualizado com o comando [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="be0be-147">After changing the capacity to the desired value, the virtual machine scale set in Azure can be updated with the [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="be0be-148">Assim como na adição de um nó manual, a adição de uma instância de conjunto de dimensionamento deve ser suficiente para iniciar um novo nó do Service Fabric, pois o modelo do conjunto de dimensionamento inclui extensões para unir novas instâncias de cluster do Service Fabric automaticamente.</span><span class="sxs-lookup"><span data-stu-id="be0be-148">As when adding a node manually, adding a scale set instance should be all that's needed to start a new Service Fabric node since the scale set template includes extensions to automatically join new instances to the Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="be0be-149">Redução horizontal</span><span class="sxs-lookup"><span data-stu-id="be0be-149">Scaling in</span></span>

<span data-ttu-id="be0be-150">A redução horizontal é semelhante à expansão.</span><span class="sxs-lookup"><span data-stu-id="be0be-150">Scaling in is similar to scaling out.</span></span> <span data-ttu-id="be0be-151">As alterações do conjunto de dimensionamento de máquinas virtuais são praticamente as mesmas.</span><span class="sxs-lookup"><span data-stu-id="be0be-151">The actual virtual machine scale set changes are practically the same.</span></span> <span data-ttu-id="be0be-152">Mas, como discutido anteriormente, o Service Fabric apenas limpa automaticamente nós removidos com uma durabilidade Ouro ou Prata.</span><span class="sxs-lookup"><span data-stu-id="be0be-152">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="be0be-153">Assim, no caso de durabilidade Bronze, é necessário interagir com o cluster do Service Fabric para desligar o nó a ser removido e remover seu estado.</span><span class="sxs-lookup"><span data-stu-id="be0be-153">So, in the Bronze-durability scale-in case, it's necessary to interact with the Service Fabric cluster to shut down the node to be removed and then to remove its state.</span></span>

<span data-ttu-id="be0be-154">A preparação do nó para desligamento envolve localizar o nó a ser removido (o nó adicionado mais recentemente) e desativá-lo.</span><span class="sxs-lookup"><span data-stu-id="be0be-154">Preparing the node for shutdown involves finding the node to be removed (the most recently added node) and deactivating it.</span></span> <span data-ttu-id="be0be-155">No caso de nós sem propagação, os nós mais recentes podem ser encontrados comparando `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="be0be-155">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="be0be-156">Lembre-se de que os nós de *propagação* nem sempre parecem seguir a convenção de que as IDs de instâncias maiores são removidas primeiro.</span><span class="sxs-lookup"><span data-stu-id="be0be-156">Be aware that *seed* nodes don't seem to always follow the convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="be0be-157">Depois que o nó a ser removido é encontrado, ele podem ser desativado e removido usando a mesma instância `FabricClient` e a instância `IAzure` anterior.</span><span class="sxs-lookup"><span data-stu-id="be0be-157">Once the node to be removed is found, it can be deactivated and removed using the same `FabricClient` instance and the `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove the node from the Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up to a timeout) for the node to gracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

<span data-ttu-id="be0be-158">Com a expansão, os cmdlets do PowerShell para modificar a capacidade do conjunto de dimensionamento de máquinas virtuais também pode ser usada aqui se uma abordagem de script for preferível.</span><span class="sxs-lookup"><span data-stu-id="be0be-158">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="be0be-159">Depois que a instância da máquina virtual é removida, o estado do nó do Service Fabric pode ser removido.</span><span class="sxs-lookup"><span data-stu-id="be0be-159">Once the virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="be0be-160">Possíveis desvantagens</span><span class="sxs-lookup"><span data-stu-id="be0be-160">Potential drawbacks</span></span>

<span data-ttu-id="be0be-161">Conforme demonstrado nos trechos de código anteriores, a criação do seu próprio serviço de dimensionamento fornece o mais alto grau de controle e personalização do comportamento de dimensionamento do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="be0be-161">As demonstrated in the preceding code snippets, creating your own scaling service provides the highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="be0be-162">Isso pode ser útil para cenários que exigem controle preciso sobre quando ou como um aplicativo pode ser expandido ou reduzido horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="be0be-162">This can be useful for scenarios requiring precise control over when or how an application scales in or out.</span></span> <span data-ttu-id="be0be-163">No entanto, esse controle é fornecido ao custo de uma maior complexidade do código.</span><span class="sxs-lookup"><span data-stu-id="be0be-163">However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="be0be-164">O uso dessa abordagem significa que você precisa possuir código de dimensionamento, o que não é simples.</span><span class="sxs-lookup"><span data-stu-id="be0be-164">Using this approach means that you need to own scaling code, which is non-trivial.</span></span>

<span data-ttu-id="be0be-165">Como você deve abordar o dimensionamento do Service Fabric depende de seu cenário.</span><span class="sxs-lookup"><span data-stu-id="be0be-165">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="be0be-166">Se o dimensionamento for incomum, a capacidade de adicionar ou remover nós manualmente provavelmente será suficiente.</span><span class="sxs-lookup"><span data-stu-id="be0be-166">If scaling is uncommon, the ability to add or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="be0be-167">Para cenários mais complexos, as regras de dimensionamento automático e os SDKs que expõem a capacidade de dimensionamento programático oferecem alternativas poderosas.</span><span class="sxs-lookup"><span data-stu-id="be0be-167">For more complex scenarios, auto-scale rules and SDKs exposing the ability to scale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be0be-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="be0be-168">Next steps</span></span>

<span data-ttu-id="be0be-169">Para começar a implementar sua própria lógica de dimensionamento automático, familiarize-se com as APIs úteis e os conceitos abaixo:</span><span class="sxs-lookup"><span data-stu-id="be0be-169">To get started implementing your own auto-scaling logic, familiarize yourself with the following concepts and useful APIs:</span></span>

- [<span data-ttu-id="be0be-170">Dimensionar manualmente ou com regras de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="be0be-170">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="be0be-171">[Bibliotecas do Gerenciamento do Azure para .NET fluentes](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (útil para interagir com conjuntos de dimensionamento de máquinas virtuais subjacentes a um cluster do Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="be0be-171">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="be0be-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (útil para interagir com um cluster do Service Fabric e seus nós)</span><span class="sxs-lookup"><span data-stu-id="be0be-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
