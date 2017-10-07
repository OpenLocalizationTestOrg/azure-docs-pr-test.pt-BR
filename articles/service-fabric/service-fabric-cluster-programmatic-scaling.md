---
title: "aaaAzure dimensionamento programático do serviço de malha | Microsoft Docs"
description: Dimensionar um cluster do Service Fabric do Azure ou programaticamente, de acordo com toocustom gatilhos
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
ms.openlocfilehash: a0c6499b1a143a173006248cf8a15380632637e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="ffad8-103">Dimensionar um cluster do Service Fabric por meio de programação</span><span class="sxs-lookup"><span data-stu-id="ffad8-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="ffad8-104">Os conceitos básicos do dimensionamento de um cluster do Azure Service Fabric são abordados na documentação sobre [dimensionamento de cluster](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="ffad8-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="ffad8-105">Esse artigo aborda como clusters do Service Fabric são criados em cima de conjuntos de dimensionamento de máquinas virtuais e podem ser dimensionados manualmente ou com regras de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="ffad8-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="ffad8-106">Este documento examina métodos programáticos de coordenação das operações de dimensionamento do Azure para cenários mais avançados.</span><span class="sxs-lookup"><span data-stu-id="ffad8-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="ffad8-107">Razões para um dimensionamento programático</span><span class="sxs-lookup"><span data-stu-id="ffad8-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="ffad8-108">Em muitos cenários, o dimensionamento manual ou por meio de regras de dimensionamento automático é uma boas solução.</span><span class="sxs-lookup"><span data-stu-id="ffad8-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="ffad8-109">Em outros cenários, no entanto, eles podem não estar Olá ajustar à direita.</span><span class="sxs-lookup"><span data-stu-id="ffad8-109">In other scenarios, though, they may not be hello right fit.</span></span> <span data-ttu-id="ffad8-110">Possíveis desvantagens toothese abordagens incluem:</span><span class="sxs-lookup"><span data-stu-id="ffad8-110">Potential drawbacks toothese approaches include:</span></span>

- <span data-ttu-id="ffad8-111">Dimensionamento manualmente requer toolog no e explicitamente as operações de dimensionamento de solicitação.</span><span class="sxs-lookup"><span data-stu-id="ffad8-111">Manually scaling requires you toolog in and explicitly request scaling operations.</span></span> <span data-ttu-id="ffad8-112">Se as operações de dimensionamento são necessárias com frequência ou em momentos imprevisíveis, essa abordagem não pode ser uma boa solução.</span><span class="sxs-lookup"><span data-stu-id="ffad8-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="ffad8-113">Quando as regras de dimensionamento automático removem uma instância de um conjunto de escala de máquinas virtuais, elas não remove automaticamente conhecimento do nó do cluster do Service Fabric Olá associado, a menos que o tipo de nó Olá tem um nível de durabilidade de prata ou ouro.</span><span class="sxs-lookup"><span data-stu-id="ffad8-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from hello associated Service Fabric cluster unless hello node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="ffad8-114">Como as regras de dimensionamento automático funcionam ao definir o nível de escala de saudação (em vez de em Olá nível de malha do serviço), regras de dimensionamento automático podem remover nós do Service Fabric sem sendo desligado normalmente.</span><span class="sxs-lookup"><span data-stu-id="ffad8-114">Because auto-scale rules work at hello scale set level (rather than at hello Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="ffad8-115">Essa remoção de nó sem maiores cuidados deixará um estado do nó do Service Fabric “fantasma” de rastro após as operações de redução horizontal.</span><span class="sxs-lookup"><span data-stu-id="ffad8-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="ffad8-116">Uma pessoa (ou um serviço) necessário tooperiodically Limpar estado do nó removido no cluster do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="ffad8-116">An individual (or a service) would need tooperiodically clean up removed node state in hello Service Fabric cluster.</span></span>
  - <span data-ttu-id="ffad8-117">Observe que um tipo de nó com um nível de durabilidade Ouro ou Prata limpará os nós removidos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ffad8-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="ffad8-118">Embora haja [várias métricas](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) com suporte pelas regras de dimensionamento automático, o conjunto ainda é limitado.</span><span class="sxs-lookup"><span data-stu-id="ffad8-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="ffad8-119">Se seu cenário exigir dimensionamento com base em alguma métrica não abordada no conjunto, as regras de dimensionamento automático podem não ser uma boa opção.</span><span class="sxs-lookup"><span data-stu-id="ffad8-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="ffad8-120">Com base nessas limitações, talvez você queira tooimplement mais automática escala modelos personalizados.</span><span class="sxs-lookup"><span data-stu-id="ffad8-120">Based on these limitations, you may wish tooimplement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="ffad8-121">Dimensionando APIs</span><span class="sxs-lookup"><span data-stu-id="ffad8-121">Scaling APIs</span></span>
<span data-ttu-id="ffad8-122">APIs do Azure existem que permitem que aplicativos tooprogrammatically funcionem com conjuntos de escala de máquina virtual e clusters de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="ffad8-122">Azure APIs exist which allow applications tooprogrammatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="ffad8-123">Se as opções de dimensionamento automático existentes não funcionam para seu cenário, essas APIs o tornam possível tooimplement lógica personalizada de escala.</span><span class="sxs-lookup"><span data-stu-id="ffad8-123">If existing auto-scale options don't work for your scenario, these APIs make it possible tooimplement custom scaling logic.</span></span> 

<span data-ttu-id="ffad8-124">Uma abordagem tooimplementing isso 'Início-feitas' dimensionamento automático funcionalidade é tooadd um novo serviço sem monitoração de estado toohello Service Fabric application toomanage operações de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="ffad8-124">One approach tooimplementing this 'home-made' auto-scaling functionality is tooadd a new stateless service toohello Service Fabric application toomanage scaling operations.</span></span> <span data-ttu-id="ffad8-125">Dentro do serviço Olá `RunAsync` método, um conjunto de gatilhos pode determinar se a escala é necessária (incluindo verificando parâmetros, como o tamanho máximo do cluster e dimensionamento cooldowns).</span><span class="sxs-lookup"><span data-stu-id="ffad8-125">Within hello service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="ffad8-126">Olá API usada para interações de conjunto de escala de máquina virtual (ambos toocheck Olá atual de número de instâncias de máquina virtual e toomodify-lo) é hello [biblioteca de computação de gerenciamento do Azure fluente](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span><span class="sxs-lookup"><span data-stu-id="ffad8-126">hello API used for virtual machine scale set interactions (both toocheck hello current number of virtual machine instances and toomodify it) is hello [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="ffad8-127">biblioteca de computação fluente Olá fornece uma API de fácil de usar para interagir com conjuntos de escala de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ffad8-127">hello fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="ffad8-128">usar toointeract com cluster do Service Fabric hello, [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="ffad8-128">toointeract with hello Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="ffad8-129">Obviamente, Olá dimensionamento código não precisa toorun como um serviço em Olá cluster toobe expandida.</span><span class="sxs-lookup"><span data-stu-id="ffad8-129">Of course, hello scaling code doesn't need toorun as a service in hello cluster toobe scaled.</span></span> <span data-ttu-id="ffad8-130">Ambos `IAzure` e `FabricClient` podem se conectar recursos do Azure tootheir associado remotamente, Olá dimensionando serviço pode ser facilmente um aplicativo de console ou executando o aplicativo de malha do serviço de hello fora de serviço do Windows.</span><span class="sxs-lookup"><span data-stu-id="ffad8-130">Both `IAzure` and `FabricClient` can connect tootheir associated Azure resources remotely, so hello scaling service could easily be a console application or Windows service running from outside hello Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="ffad8-131">Gerenciamento de credenciais</span><span class="sxs-lookup"><span data-stu-id="ffad8-131">Credential management</span></span>
<span data-ttu-id="ffad8-132">Um desafio de escrever um dimensionamento de toohandle de serviço é que o serviço de saudação deve ser recursos de conjunto de escala tooaccess capaz de máquina virtual sem um logon interativo.</span><span class="sxs-lookup"><span data-stu-id="ffad8-132">One challenge of writing a service toohandle scaling is that hello service must be able tooaccess virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="ffad8-133">Acessando Olá malha do serviço de cluster é fácil se Olá dimensionando serviço está modificando seu próprio aplicativo de malha do serviço, mas as credenciais são necessárias tooaccess Olá conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="ffad8-133">Accessing hello Service Fabric cluster is easy if hello scaling service is modifying its own Service Fabric application, but credentials are needed tooaccess hello scale set.</span></span> <span data-ttu-id="ffad8-134">toolog no, você pode usar um [entidade de serviço](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) criado com hello [Azure CLI 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ffad8-134">toolog in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with hello [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="ffad8-135">Uma entidade de serviço pode ser criada com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffad8-135">A service principal can be created with hello following steps:</span></span>

1. <span data-ttu-id="ffad8-136">Faça logon no toohello CLI do Azure (`az login`) como um usuário com a escala de máquinas virtuais toohello acesso definido</span><span class="sxs-lookup"><span data-stu-id="ffad8-136">Log in toohello Azure CLI (`az login`) as a user with access toohello virtual machine scale set</span></span>
2. <span data-ttu-id="ffad8-137">Criar serviço Olá principal com`az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="ffad8-137">Create hello service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="ffad8-138">Anote Olá appId (chamado de ID do cliente em outro lugar), nome, senha e locatário para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="ffad8-138">Make note of hello appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="ffad8-139">Você também precisará da sua ID de assinatura, que pode ser exibida com `az account list`</span><span class="sxs-lookup"><span data-stu-id="ffad8-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="ffad8-140">Olá computação fluente biblioteca pode fazer logon usando essas credenciais da seguinte maneira (Observe que os tipos de Azure fluente core como `IAzure` no hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) pacote):</span><span class="sxs-lookup"><span data-stu-id="ffad8-140">hello fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

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
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed toologin tooAzure");
}
```

<span data-ttu-id="ffad8-141">Depois da conexão, a contagem de instâncias do conjunto de dimensionamento pode ser consultada por meio de `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="ffad8-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="ffad8-142">Expansão</span><span class="sxs-lookup"><span data-stu-id="ffad8-142">Scaling out</span></span>
<span data-ttu-id="ffad8-143">Usando Olá fluente SDK de computação do Azure, instâncias podem ser adicionadas a escala de máquinas virtuais toohello com apenas algumas chamadas-</span><span class="sxs-lookup"><span data-stu-id="ffad8-143">Using hello fluent Azure compute SDK, instances can be added toohello virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="ffad8-144">Como alternativa, o tamanho do conjunto de dimensionamento de máquinas virtuais também pode ser gerenciado com os cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ffad8-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="ffad8-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)pode recuperar o objeto de conjunto de escala de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffad8-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve hello virtual machine scale set object.</span></span> <span data-ttu-id="ffad8-146">capacidade atual Hello será armazenada no hello `.sku.capacity` propriedade.</span><span class="sxs-lookup"><span data-stu-id="ffad8-146">hello current capacity will be stored in hello `.sku.capacity` property.</span></span> <span data-ttu-id="ffad8-147">Depois de alterar Olá capacidade toohello valor desejado, escala de máquinas virtuais Olá definida no Azure pode ser atualizada com hello [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) comando.</span><span class="sxs-lookup"><span data-stu-id="ffad8-147">After changing hello capacity toohello desired value, hello virtual machine scale set in Azure can be updated with hello [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="ffad8-148">Como adicionar conjunto de uma escala de instância ao adicionar um nó manualmente, deve ser todos os toostart necessário que inclui um novo nó de malha do serviço porque o modelo de conjunto de escala de saudação extensões tooautomatically adicionar novo cluster de malha do serviço de toohello de instâncias.</span><span class="sxs-lookup"><span data-stu-id="ffad8-148">As when adding a node manually, adding a scale set instance should be all that's needed toostart a new Service Fabric node since hello scale set template includes extensions tooautomatically join new instances toohello Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="ffad8-149">Redução horizontal</span><span class="sxs-lookup"><span data-stu-id="ffad8-149">Scaling in</span></span>

<span data-ttu-id="ffad8-150">O dimensionamento em é semelhante tooscaling-out. conjunto de escala de máquina virtual Olá alterações são praticamente Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="ffad8-150">Scaling in is similar tooscaling out. hello actual virtual machine scale set changes are practically hello same.</span></span> <span data-ttu-id="ffad8-151">Mas, como discutido anteriormente, o Service Fabric apenas limpa automaticamente nós removidos com uma durabilidade Ouro ou Prata.</span><span class="sxs-lookup"><span data-stu-id="ffad8-151">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="ffad8-152">Portanto, Olá Bronze durabilidade escala no caso, é necessário toointeract com hello Service Fabric cluster tooshut para baixo Olá nó toobe removido e, em seguida, tooremove seu estado.</span><span class="sxs-lookup"><span data-stu-id="ffad8-152">So, in hello Bronze-durability scale-in case, it's necessary toointeract with hello Service Fabric cluster tooshut down hello node toobe removed and then tooremove its state.</span></span>

<span data-ttu-id="ffad8-153">Preparando o nó de saudação para desligamento envolve a localização Olá nó toobe removido (Olá nó adicionado mais recentemente) e desativá-lo.</span><span class="sxs-lookup"><span data-stu-id="ffad8-153">Preparing hello node for shutdown involves finding hello node toobe removed (hello most recently added node) and deactivating it.</span></span> <span data-ttu-id="ffad8-154">No caso de nós sem propagação, os nós mais recentes podem ser encontrados comparando `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="ffad8-154">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="ffad8-155">Lembre-se que *semente* nós não parecem tooalways seguem a convenção de saudação que maior IDs de instância são removidas primeiro.</span><span class="sxs-lookup"><span data-stu-id="ffad8-155">Be aware that *seed* nodes don't seem tooalways follow hello convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="ffad8-156">Depois de saudação nó toobe removido for encontrado, ele pode ser desativado e removido usando Olá mesmo `FabricClient` instância e hello `IAzure` instância anteriores.</span><span class="sxs-lookup"><span data-stu-id="ffad8-156">Once hello node toobe removed is found, it can be deactivated and removed using hello same `FabricClient` instance and hello `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove hello node from hello Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up tooa timeout) for hello node toogracefully shutdown
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

<span data-ttu-id="ffad8-157">Com a expansão, os cmdlets do PowerShell para modificar a capacidade do conjunto de dimensionamento de máquinas virtuais também pode ser usada aqui se uma abordagem de script for preferível.</span><span class="sxs-lookup"><span data-stu-id="ffad8-157">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="ffad8-158">Depois que a instância de máquina virtual de saudação for removida, o estado do nó do Service Fabric pode ser removido.</span><span class="sxs-lookup"><span data-stu-id="ffad8-158">Once hello virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="ffad8-159">Possíveis desvantagens</span><span class="sxs-lookup"><span data-stu-id="ffad8-159">Potential drawbacks</span></span>

<span data-ttu-id="ffad8-160">Conforme demonstrado no hello anterior trechos de código, criar seu próprio serviço de dimensionamento fornece mais alto grau de saudação de controle e personalização em seu aplicativo do dimensionamento de comportamento.</span><span class="sxs-lookup"><span data-stu-id="ffad8-160">As demonstrated in hello preceding code snippets, creating your own scaling service provides hello highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="ffad8-161">Isso pode ser útil para cenários que exigem controle preciso sobre quando ou como um aplicativo pode ser expandido ou reduzido horizontalmente. No entanto, esse controle é fornecido ao custo de uma maior complexidade do código.</span><span class="sxs-lookup"><span data-stu-id="ffad8-161">This can be useful for scenarios requiring precise control over when or how an application scales in or out. However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="ffad8-162">Usando essa abordagem significa que você precisa tooown dimensionamento de código, que não é simples.</span><span class="sxs-lookup"><span data-stu-id="ffad8-162">Using this approach means that you need tooown scaling code, which is non-trivial.</span></span>

<span data-ttu-id="ffad8-163">Como você deve abordar o dimensionamento do Service Fabric depende de seu cenário.</span><span class="sxs-lookup"><span data-stu-id="ffad8-163">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="ffad8-164">Se a escala é incomum, Olá capacidade tooadd ou remover nós manualmente provavelmente será suficiente.</span><span class="sxs-lookup"><span data-stu-id="ffad8-164">If scaling is uncommon, hello ability tooadd or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="ffad8-165">Para cenários mais complexos, regras de dimensionamento automático e SDKs expondo Olá capacidade tooscale programaticamente oferecem alternativas poderosas.</span><span class="sxs-lookup"><span data-stu-id="ffad8-165">For more complex scenarios, auto-scale rules and SDKs exposing hello ability tooscale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffad8-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ffad8-166">Next steps</span></span>

<span data-ttu-id="ffad8-167">tooget começaram a implementar sua própria lógica de dimensionamento automático, se familiarizar com hello APIs úteis e conceitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffad8-167">tooget started implementing your own auto-scaling logic, familiarize yourself with hello following concepts and useful APIs:</span></span>

- [<span data-ttu-id="ffad8-168">Dimensionar manualmente ou com regras de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="ffad8-168">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="ffad8-169">[Bibliotecas do Gerenciamento do Azure para .NET fluentes](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (útil para interagir com conjuntos de dimensionamento de máquinas virtuais subjacentes a um cluster do Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="ffad8-169">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="ffad8-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (útil para interagir com um cluster do Service Fabric e seus nós)</span><span class="sxs-lookup"><span data-stu-id="ffad8-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
