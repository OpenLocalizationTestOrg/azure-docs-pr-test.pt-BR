---
title: "aaaScale uma malha do serviço de cluster ou | Microsoft Docs"
description: "Dimensione um cluster do Service Fabric in ou out toomatch demanda definindo regras de dimensionamento automático para cada conjunto de escala de máquina do nó Virtual/tipo. Adicionar ou remover nós tooa malha do serviço cluster"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: aeb76f63-7303-4753-9c64-46146340b83d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 37cfeaf80edc016cf6de017d1c2dc6fbcb8acc2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-in-or-out-using-auto-scale-rules"></a>Escalar ou reduzir horizontalmente um cluster do Service Fabric usando regras de autoescala
Conjuntos de escala de máquinas virtuais são um recurso de computação do Azure que você pode usar toodeploy e gerenciar uma coleção de máquinas virtuais como um conjunto. Cada tipo de nó definido em um cluster do Service Fabric está configurado como um conjunto de dimensionamento de máquinas virtuais separado. Cada tipo de nó pode ser escalado ou reduzido horizontalmente de forma independente, ter conjuntos diferentes de portas abertas e métricas de capacidade diferentes. Leia mais sobre isso em Olá [nodetypes Service Fabric](service-fabric-cluster-nodetypes.md) documento. Como tipos de nós do Service Fabric Olá no cluster são feitos de conjuntos de escala de máquinas virtuais em Olá back-end, você precisa tooset as regras de dimensionamento automático para cada conjunto de escala de máquina do nó Virtual/tipo.

> [!NOTE]
> Sua assinatura deve ter suficiente tooadd núcleos Olá novas VMs que compõem esse cluster. Não há nenhuma validação de modelo no momento, para que você obtenha uma falha de tempo de implantação, se qualquer um dos limites de cota de saudação são atingidos.
> 
> 

## <a name="choose-hello-node-typevirtual-machine-scale-set-tooscale"></a>Escolha Olá nó tipo/Virtual escala de máquina conjunto tooscale
No momento, você não toospecify capaz de regras de dimensionamento automático Olá para conjuntos de escala de máquinas virtuais usando o portal de hello, então vamos usar tipos de nós do Azure PowerShell (1.0 +) toolist hello e, em seguida, adicione toothem de regras de dimensionamento automático.

lista de saudação tooget da máquina Virtual conjunto de escala que compõem o cluster, execute Olá cmdlets a seguir:

```powershell
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Compute/VirtualMachineScaleSets

Get-AzureRmVmss -ResourceGroupName <RGname> -VMScaleSetName <Virtual Machine scale set name>
```

## <a name="set-auto-scale-rules-for-hello-node-typevirtual-machine-scale-set"></a>Definir regras de dimensionamento automático para o conjunto de escala de máquina do hello nó tipo/Virtual
Se o cluster tiver vários tipos de nós, repita que isso para cada tipos de nó/escala de máquina Virtual define que você deseja tooscale (entrada ou saída). Considera número Olá da conta de nós que você deve ter antes de configurar o dimensionamento automático. número mínimo de saudação de nós que você deve ter para o tipo de nó primário Olá é orientado por nível de confiabilidade Olá escolhido. Leia mais sobre os [níveis de confiabilidade](service-fabric-cluster-capacity.md).

> [!NOTE]
> Redução tooless de tipo de nó primário Olá que o número mínimo de saudação fazer cluster Olá instável ou colocá-lo para baixo. Isso pode resultar em perda de dados para seus aplicativos e serviços de sistema de saudação.
> 
> 

No momento recurso de dimensionamento automático Olá não é orientado por cargas de saudação que seus aplicativos podem relatar tooService malha. Portanto em Olá esse tempo AutoEscala que você obter puramente é orientada por contadores de desempenho de saudação que são emitidas por cada uma das instâncias de conjunto de escala de máquina Virtual de saudação.  

Siga estas instruções [tooset o dimensionamento automático para cada conjunto de escala de máquina Virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview.md).

> [!NOTE]
> Em uma escala para baixo do cenário, a menos que o tipo de nó tem um nível de durabilidade de ouro ou prata precisar Olá toocall [cmdlet Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/azure/mt125993.aspx) com o nome de nó apropriado hello.
> 
> 

## <a name="manually-add-vms-tooa-node-typevirtual-machine-scale-set"></a>Adicionar manualmente as VMs tooa nó tipo/Virtual conjunto de escalas da máquina
Siga Olá/instruções de exemplo no hello [Galeria de modelos de início rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange número de saudação de VMs em cada Nodetype. 

> [!NOTE]
> A adição de VMs leva tempo, portanto, não haverá Olá adições toobe instantânea. Para planejar a capacidade de tooadd bem em tempo, tooallow para mais de 10 minutos antes de saudação de capacidade de VM está disponível para réplicas Olá / serviço tooget instâncias colocado.
> 
> 

## <a name="manually-remove-vms-from-hello-primary-node-typevirtual-machine-scale-set"></a>Remova manualmente as VMs do conjunto de escala de máquina do hello nó primário tipo/Virtual
> [!NOTE]
> Serviços de sistema de malha de serviço Olá são executados no tipo de nó primário Olá no cluster. Menor que o nível de confiabilidade Olá garante para nunca deve desligar ou reduzir o número de saudação de instâncias em que tipos de nó. Consulte também[Olá detalhes em níveis de confiabilidade aqui](service-fabric-cluster-capacity.md). 
> 
> 

Você precisa tooexecute uma instância VM as etapas a seguir Olá por vez. Isso permite que serviços do sistema hello (e seus serviços com monitoração de estado) toobe desligar normalmente na instância VM de saudação você está removendo e novas réplicas criadas em outros nós.

1. Executar [ServiceFabricNode desabilitar](https://msdn.microsoft.com/library/mt125852.aspx) com nó de saudação do propósito 'RemoveNode' toodisable for tooremove (instância maior Olá nesse tipo de nó).
2. Executar [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake-se de que esse nó Olá realmente tem transição toodisabled. Caso contrário, aguarde até que o nó hello está desabilitado. Não tenha pressa nesta etapa.
3. Siga Olá/instruções de exemplo no hello [Galeria de modelos de início rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange Olá diversas VMs em uma unidade em que Nodetype. Olá instância removida é hello mais alto VM. 
4. Repita as etapas 1 a 3, conforme necessário, mas nunca reduzir o número de saudação de instâncias no hello tipos de nó principal menor que garante que nível de confiabilidade hello. Consulte também[Olá detalhes em níveis de confiabilidade aqui](service-fabric-cluster-capacity.md). 

## <a name="manually-remove-vms-from-hello-non-primary-node-typevirtual-machine-scale-set"></a>Remova manualmente VMs a saudação não primário nó tipo/Virtual conjunto de escalas da máquina
> [!NOTE]
> Para um serviço com monitoração de estado, é necessário um determinado número de nós toobe sempre backup toomaintain disponibilidade e preservar o estado do serviço. No hello mínimo, você precisa de número de saudação de nós toohello igual destino réplica Definir contagem de partição de saudação/serviço. 
> 
> 

Você precisa Olá Olá uma instância VM etapas a seguir em vez de executar. Isso permite que serviços do sistema hello (e seus serviços com monitoração de estado) toobe desligar normalmente em Olá instância VM que você está removendo e novas réplicas criada onde else.

1. Executar [ServiceFabricNode desabilitar](https://msdn.microsoft.com/library/mt125852.aspx) com nó de saudação do propósito 'RemoveNode' toodisable for tooremove (instância maior Olá nesse tipo de nó).
2. Executar [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake-se de que esse nó Olá realmente tem transição toodisabled. Se não Aguarde até que o nó hello está desabilitado. Não tenha pressa nesta etapa.
3. Siga Olá/instruções de exemplo no hello [Galeria de modelos de início rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange Olá diversas VMs em uma unidade em que Nodetype. Isso removerá instância de VM hello mais alta. 
4. Repita as etapas 1 a 3, conforme necessário, mas nunca reduzir o número de saudação de instâncias no hello tipos de nó principal menor que garante que nível de confiabilidade hello. Consulte também[Olá detalhes em níveis de confiabilidade aqui](service-fabric-cluster-capacity.md).

## <a name="behaviors-you-may-observe-in-service-fabric-explorer"></a>Comportamentos que podem ser observados no Service Fabric Explorer
Quando você expandir uma saudação cluster Service Fabric Explorer refletirá o número de saudação de nós (instâncias do conjunto de escala de máquina Virtual) que fazem parte do cluster de saudação.  No entanto, quando você dimensionar um cluster para baixo, você verá instância VM nó Olá removido exibida em um estado não íntegro, a menos que você chame [ServiceFabricNodeState remover cmd](https://msdn.microsoft.com/library/mt125993.aspx) com o nome de nó apropriado hello.   

Aqui está a explicação Olá para esse comportamento.

nós listados no Gerenciador do Service Fabric Hello são um reflexo de quais serviços do sistema do Service Fabric hello (FM especificamente) conhece o número de saudação de nós Olá cluster tinha/tem. Quando você escala Olá escala de máquina Virtual definida para baixo, Olá VM foi excluído, mas o serviço do sistema FM ainda considera nó hello (que foi mapeada toohello VM que foi excluída) voltará. Portanto Service Fabric Explorer continua toodisplay nó (embora o estado de integridade Olá pode ser desconhecido ou erro).

Toomake ordem-se de que um nó é removido quando uma máquina virtual é removida, você tem duas opções:

1) Escolha um nível de durabilidade de ouro ou prata (disponível em breve) para tipos de nós de saudação do cluster, que lhe Olá integração de infraestrutura. Que, em seguida, removerá automaticamente nós de saudação do nosso estado do sistema de serviços (FM) quando você reduzir.
Consulte também[Olá detalhes sobre os níveis de durabilidade aqui](service-fabric-cluster-capacity.md)

2) Depois que a instância VM Olá foi reduzida, você precisa Olá toocall [cmdlet Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/mt125993.aspx).

> [!NOTE]
> Clusters de malha serviço exigem um determinado número de nós toobe backup em todos os Olá tempo na ordem toomaintain disponibilidade e preservar o estado - tooas chamado "mantêm o quórum." Portanto, é normalmente unsafe tooshut todas as máquinas de saudação em cluster hello, a menos que você tiver executado pela primeira vez um [backup completo do estado do seu](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Próximas etapas
Saudação de leitura após tooalso Saiba mais sobre planejamento de capacidade do cluster, atualizando um cluster e particionamento de serviços:

* [Planejar a capacidade do cluster](service-fabric-cluster-capacity.md)
* [Atualizações do cluster](service-fabric-cluster-upgrade.md)
* [Serviços com estado de partição para escala máxima](service-fabric-concepts-partitioning.md)

<!--Image references-->
[BrowseServiceFabricClusterResource]: ./media/service-fabric-cluster-scale-up-down/BrowseServiceFabricClusterResource.png
[ClusterResources]: ./media/service-fabric-cluster-scale-up-down/ClusterResources.png
