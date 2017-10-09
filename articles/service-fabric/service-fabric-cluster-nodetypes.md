---
title: "aaaService malha tipos de nó e conjuntos de escala de VM | Microsoft Docs"
description: "Descreve como os tipos de nós do Service Fabric se relacionam tooVM conjuntos de escala e como tooremote conecte-se a instância de conjunto de escala de tooa ou um nó de cluster."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a>relação de saudação entre tipos de nós do Service Fabric e conjuntos de escala de máquinas virtuais
Conjuntos de escala de máquinas virtuais são um recurso de computação do Azure, você pode usar toodeploy e gerenciar uma coleção de máquinas virtuais como um conjunto. Cada tipo de nó definido em um cluster do Service Fabric é configurado como um Conjunto de Escala de VM separado. Cada tipo de nó pode ser escalado verticalmente para cima ou para baixo de forma independente, tem conjuntos diferentes de portas abertas e pode ter métricas de capacidade diferente.

Olá captura de tela a seguir mostra um cluster que tem dois tipos de nó: front-end e back-end.  Cada tipo de nó tem cinco nós.

![Captura de tela de um cluster com dois tipos de nó][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a>Mapeamento de conjunto de escala de VM toonodes de instâncias
Como você pode ver acima, Olá conjunto de escala de VM iniciar instâncias de instância 0 e, em seguida, aumenta. Olá numeração é refletido nos nomes de saudação. Por exemplo, BackEnd_0 é instância 0 da saudação conjunto de escala de VM back-end. Esse conjunto de escala da VM específico tem cinco instâncias, chamadas BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 e BackEnd_4.

Quando você escala um conjunto de escala de VM verticalmente, uma nova instância é criada. Olá novo conjunto de escala de VM nome da instância normalmente é nome do conjunto de escala de VM Olá + próximo número de instância hello. Em nosso exemplo, é BackEnd_5.

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a>Mapeamento de VM carregar o conjunto de escala balanceadores tooeach nó tipo VM conjunto de escala
Se você tiver implantado o cluster do portal de saudação ou ter usado o modelo de Gerenciador de recursos do exemplo hello fornecemos, em seguida, quando você obter uma lista de todos os recursos em um grupo de recursos, em seguida, você verá balanceadores de carga Olá para cada tipo de conjunto de escala de VM ou nó.

Olá nome seria algo como: **LB -&lt;nome de NodeType&gt;**. Por exemplo, LB-sfcluster4doc-0, conforme mostrado nesta captura de tela:

![Recursos][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a>Conexão remota tooa instância de conjunto de escala de VM ou um nó de cluster
Cada tipo de Nó definido em um cluster é configurado como um Conjunto de Escala de VM separado.  Significa Olá tipos de nó pode ser dimensionada para cima ou independentemente e podem ser feitas de SKUs de VM diferente. Ao contrário de única instância VMs, instâncias de conjunto de escala de VM Olá não obtém um endereço IP virtual de seus próprios. Para que ele possa ser um pouco difícil quando você estiver procurando um IP endereço e porta que você pode usar tooremote conectarem instância específica do tooa.

Aqui estão Olá etapas que você pode seguir toodiscovê-los.

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a>Etapa 1: Localizar o endereço IP virtual Olá para o tipo de nó hello e, em seguida, regras de NAT de entrada para RDP
Em ordem tooget, é necessária tooget Olá NAT de entrada regras valores que foram definidos como parte da definição de recurso Olá para **Microsoft.Network/loadBalancers**.

No portal de hello, navegue até toohello folha de Balanceador de carga e, em seguida, **configurações**.

![LBBlade][LBBlade]

Em **Configurações**, clique em **Regras NAT de entrada**. Agora fornece Olá endereço IP e porta que você pode usar tooremote conectar toohello primeira instância do conjunto de escala de VM. Olá captura de tela abaixo, é **104.42.106.156** e **3389**

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a>Etapa 2: Descobrir porta Olá que você pode usar tooremote conectar toohello conjunto de escala de VM instância/nó específico
No início deste documento, eu falou sobre como instâncias de conjunto de escala de VM Olá mapeiam toohello nós. Usaremos esse toofigure porta exata Olá de saída.

Olá portas são alocadas em ordem crescente da instância de conjunto de escala de VM hello. portanto em meu exemplo de saudação tipo de nó de front-end, portas de Olá para cada um dos cinco instâncias de saudação são seguinte hello. Você agora precisa toodo Olá mesmo mapeamento para a instância do conjunto de escala de VM.

| **Instância do Conjunto de Escala de VM** | **Porta** |
| --- | --- |
| FrontEnd_0 |3389 |
| FrontEnd_1 |3390 |
| FrontEnd_2 |3391 |
| FrontEnd_3 |3392 |
| FrontEnd_4 |3393 |
| FrontEnd_5 |3394 |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a>Etapa 3: Instância de conjunto de escala específica toohello de conexão remota
Na captura de tela de saudação abaixo uso Conexão de área de trabalho remota tooconnect toohello FrontEnd_1:

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a>Como valores do intervalo de saudação toochange porta do RDP
### <a name="before-cluster-deployment"></a>Antes da implantação de cluster
Quando você estiver configurando o cluster hello usando um modelo do Gerenciador de recursos, você pode especificar o intervalo de saudação em Olá **inboundNatPools**.

Vá para consultar a definição de recurso toohello **Microsoft.Network/loadBalancers**. Em que você encontrar descrição Olá para **inboundNatPools**.  Substituir saudação *frontendPortRangeStart* e *frontendPortRangeEnd* valores.

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a>Depois da implantação de cluster
Isso é um pouco mais envolvido e pode resultar em VMs Olá recicladas. Agora, você terá tooset novos valores usando o PowerShell do Azure. Verifique se o Azure PowerShell versão 1.0 ou posterior está instalado em seu computador. Se você não tiver feito isso antes, sugiro que você siga etapas Olá descritas em [como tooinstall e configurar o Azure PowerShell.](/powershell/azure/overview)

Entre tooyour conta do Azure. Se o comando do PowerShell falhar por algum motivo, verifique se o Azure PowerShell foi instalado corretamente.

```
Login-AzureRmAccount
```

Executar Olá tooget detalhes no balanceador de carga a seguir e consulte valores hello para descrição Olá para **inboundNatPools**:

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

Agora definido *frontendPortRangeEnd* e *frontendPortRangeStart* toohello valores desejados.

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a>Próximas etapas
* [Visão geral do recurso de "Implantar em qualquer lugar" hello e uma comparação com clusters gerenciado do Azure](service-fabric-deploy-anywhere.md)
* [Segurança de cluster](service-fabric-cluster-security.md)
* [ SDK do Service Fabric e introdução](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
