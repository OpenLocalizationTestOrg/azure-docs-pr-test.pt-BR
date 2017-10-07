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
# <a name="scale-a-service-fabric-cluster-programmatically"></a>Dimensionar um cluster do Service Fabric por meio de programação 

Os conceitos básicos do dimensionamento de um cluster do Azure Service Fabric são abordados na documentação sobre [dimensionamento de cluster](./service-fabric-cluster-scale-up-down.md). Esse artigo aborda como clusters do Service Fabric são criados em cima de conjuntos de dimensionamento de máquinas virtuais e podem ser dimensionados manualmente ou com regras de dimensionamento automático. Este documento examina métodos programáticos de coordenação das operações de dimensionamento do Azure para cenários mais avançados. 

## <a name="reasons-for-programmatic-scaling"></a>Razões para um dimensionamento programático
Em muitos cenários, o dimensionamento manual ou por meio de regras de dimensionamento automático é uma boas solução. Em outros cenários, no entanto, eles podem não estar Olá ajustar à direita. Possíveis desvantagens toothese abordagens incluem:

- Dimensionamento manualmente requer toolog no e explicitamente as operações de dimensionamento de solicitação. Se as operações de dimensionamento são necessárias com frequência ou em momentos imprevisíveis, essa abordagem não pode ser uma boa solução.
- Quando as regras de dimensionamento automático removem uma instância de um conjunto de escala de máquinas virtuais, elas não remove automaticamente conhecimento do nó do cluster do Service Fabric Olá associado, a menos que o tipo de nó Olá tem um nível de durabilidade de prata ou ouro. Como as regras de dimensionamento automático funcionam ao definir o nível de escala de saudação (em vez de em Olá nível de malha do serviço), regras de dimensionamento automático podem remover nós do Service Fabric sem sendo desligado normalmente. Essa remoção de nó sem maiores cuidados deixará um estado do nó do Service Fabric “fantasma” de rastro após as operações de redução horizontal. Uma pessoa (ou um serviço) necessário tooperiodically Limpar estado do nó removido no cluster do Service Fabric hello.
  - Observe que um tipo de nó com um nível de durabilidade Ouro ou Prata limpará os nós removidos automaticamente.  
- Embora haja [várias métricas](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) com suporte pelas regras de dimensionamento automático, o conjunto ainda é limitado. Se seu cenário exigir dimensionamento com base em alguma métrica não abordada no conjunto, as regras de dimensionamento automático podem não ser uma boa opção.

Com base nessas limitações, talvez você queira tooimplement mais automática escala modelos personalizados. 

## <a name="scaling-apis"></a>Dimensionando APIs
APIs do Azure existem que permitem que aplicativos tooprogrammatically funcionem com conjuntos de escala de máquina virtual e clusters de malha do serviço. Se as opções de dimensionamento automático existentes não funcionam para seu cenário, essas APIs o tornam possível tooimplement lógica personalizada de escala. 

Uma abordagem tooimplementing isso 'Início-feitas' dimensionamento automático funcionalidade é tooadd um novo serviço sem monitoração de estado toohello Service Fabric application toomanage operações de dimensionamento. Dentro do serviço Olá `RunAsync` método, um conjunto de gatilhos pode determinar se a escala é necessária (incluindo verificando parâmetros, como o tamanho máximo do cluster e dimensionamento cooldowns).   

Olá API usada para interações de conjunto de escala de máquina virtual (ambos toocheck Olá atual de número de instâncias de máquina virtual e toomodify-lo) é hello [biblioteca de computação de gerenciamento do Azure fluente](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/). biblioteca de computação fluente Olá fornece uma API de fácil de usar para interagir com conjuntos de escala de máquina virtual.

usar toointeract com cluster do Service Fabric hello, [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).

Obviamente, Olá dimensionamento código não precisa toorun como um serviço em Olá cluster toobe expandida. Ambos `IAzure` e `FabricClient` podem se conectar recursos do Azure tootheir associado remotamente, Olá dimensionando serviço pode ser facilmente um aplicativo de console ou executando o aplicativo de malha do serviço de hello fora de serviço do Windows. 

## <a name="credential-management"></a>Gerenciamento de credenciais
Um desafio de escrever um dimensionamento de toohandle de serviço é que o serviço de saudação deve ser recursos de conjunto de escala tooaccess capaz de máquina virtual sem um logon interativo. Acessando Olá malha do serviço de cluster é fácil se Olá dimensionando serviço está modificando seu próprio aplicativo de malha do serviço, mas as credenciais são necessárias tooaccess Olá conjunto de escala. toolog no, você pode usar um [entidade de serviço](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) criado com hello [Azure CLI 2.0](https://github.com/azure/azure-cli).

Uma entidade de serviço pode ser criada com hello etapas a seguir:

1. Faça logon no toohello CLI do Azure (`az login`) como um usuário com a escala de máquinas virtuais toohello acesso definido
2. Criar serviço Olá principal com`az ad sp create-for-rbac`
    1. Anote Olá appId (chamado de ID do cliente em outro lugar), nome, senha e locatário para uso posterior.
    2. Você também precisará da sua ID de assinatura, que pode ser exibida com `az account list`

Olá computação fluente biblioteca pode fazer logon usando essas credenciais da seguinte maneira (Observe que os tipos de Azure fluente core como `IAzure` no hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) pacote):

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

Depois da conexão, a contagem de instâncias do conjunto de dimensionamento pode ser consultada por meio de `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.

## <a name="scaling-out"></a>Expansão
Usando Olá fluente SDK de computação do Azure, instâncias podem ser adicionadas a escala de máquinas virtuais toohello com apenas algumas chamadas-

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

Como alternativa, o tamanho do conjunto de dimensionamento de máquinas virtuais também pode ser gerenciado com os cmdlets do PowerShell. [`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)pode recuperar o objeto de conjunto de escala de máquina virtual de saudação. capacidade atual Hello será armazenada no hello `.sku.capacity` propriedade. Depois de alterar Olá capacidade toohello valor desejado, escala de máquinas virtuais Olá definida no Azure pode ser atualizada com hello [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) comando.

Como adicionar conjunto de uma escala de instância ao adicionar um nó manualmente, deve ser todos os toostart necessário que inclui um novo nó de malha do serviço porque o modelo de conjunto de escala de saudação extensões tooautomatically adicionar novo cluster de malha do serviço de toohello de instâncias. 

## <a name="scaling-in"></a>Redução horizontal

O dimensionamento em é semelhante tooscaling-out. conjunto de escala de máquina virtual Olá alterações são praticamente Olá mesmo. Mas, como discutido anteriormente, o Service Fabric apenas limpa automaticamente nós removidos com uma durabilidade Ouro ou Prata. Portanto, Olá Bronze durabilidade escala no caso, é necessário toointeract com hello Service Fabric cluster tooshut para baixo Olá nó toobe removido e, em seguida, tooremove seu estado.

Preparando o nó de saudação para desligamento envolve a localização Olá nó toobe removido (Olá nó adicionado mais recentemente) e desativá-lo. No caso de nós sem propagação, os nós mais recentes podem ser encontrados comparando `NodeInstanceId`. 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

Lembre-se que *semente* nós não parecem tooalways seguem a convenção de saudação que maior IDs de instância são removidas primeiro.

Depois de saudação nó toobe removido for encontrado, ele pode ser desativado e removido usando Olá mesmo `FabricClient` instância e hello `IAzure` instância anteriores.

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

Com a expansão, os cmdlets do PowerShell para modificar a capacidade do conjunto de dimensionamento de máquinas virtuais também pode ser usada aqui se uma abordagem de script for preferível. Depois que a instância de máquina virtual de saudação for removida, o estado do nó do Service Fabric pode ser removido.

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a>Possíveis desvantagens

Conforme demonstrado no hello anterior trechos de código, criar seu próprio serviço de dimensionamento fornece mais alto grau de saudação de controle e personalização em seu aplicativo do dimensionamento de comportamento. Isso pode ser útil para cenários que exigem controle preciso sobre quando ou como um aplicativo pode ser expandido ou reduzido horizontalmente. No entanto, esse controle é fornecido ao custo de uma maior complexidade do código. Usando essa abordagem significa que você precisa tooown dimensionamento de código, que não é simples.

Como você deve abordar o dimensionamento do Service Fabric depende de seu cenário. Se a escala é incomum, Olá capacidade tooadd ou remover nós manualmente provavelmente será suficiente. Para cenários mais complexos, regras de dimensionamento automático e SDKs expondo Olá capacidade tooscale programaticamente oferecem alternativas poderosas.

## <a name="next-steps"></a>Próximas etapas

tooget começaram a implementar sua própria lógica de dimensionamento automático, se familiarizar com hello APIs úteis e conceitos a seguir:

- [Dimensionar manualmente ou com regras de dimensionamento automático](./service-fabric-cluster-scale-up-down.md)
- [Bibliotecas do Gerenciamento do Azure para .NET fluentes](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (útil para interagir com conjuntos de dimensionamento de máquinas virtuais subjacentes a um cluster do Service Fabric)
- [System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (útil para interagir com um cluster do Service Fabric e seus nós)
