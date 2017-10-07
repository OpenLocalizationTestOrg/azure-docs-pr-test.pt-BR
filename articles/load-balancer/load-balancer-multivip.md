---
title: "aaaMutiple VIPs para um serviço de nuvem"
description: "Visão geral de multiVIP e como tooset vários VIPs em um serviço de nuvem"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a>Configurar vários VIPs para um serviço de nuvem

Você pode acessar os serviços de nuvem do Azure sobre Olá Internet pública usando um endereço IP fornecida pelo Azure. Este endereço IP público é chamado tooas um VIP (IP virtual) pois ela está vinculada toohello Azure balanceador de carga e não Olá instâncias de máquina Virtual (VM) no serviço de nuvem hello. Você pode acessar qualquer instância VM dentro de um serviço de nuvem usando um único VIP.

No entanto, há situações em que talvez seja necessário mais de um VIP como um toohello de ponto de entrada mesmo serviço de nuvem. Por exemplo, o serviço de nuvem pode hospedar vários sites que exigem conectividade SSL usando Olá porta padrão 443, como cada site é hospedado por um cliente diferente ou locatário. Nesse cenário, você precisa toohave um diferente endereço IP público para cada site. Olá diagrama abaixo ilustra uma hospedagem web multilocatária típico com uma necessidade SSL vários certificados em Olá mesmo porta pública.

![Cenário SSL de vários VIPs](./media/load-balancer-multivip/Figure1.png)

No exemplo hello acima, a saudação de uso todos os VIPs mesma porta pública (443) e o tráfego é redirecionado tooone ou mais carga equilibradas VMs em uma porta privada exclusiva para o endereço IP interno de Olá Olá do serviço de nuvem hospedagem todos os sites de saudação.

> [!NOTE]
> Outra situação exigindo Olá use Olá vários VIPs está hospedando vários ouvintes de grupo de disponibilidade AlwaysOn do SQL no mesmo conjunto de máquinas virtuais de saudação.

VIPs são dinâmicos por padrão, o que significa que o endereço IP real Olá atribuído toohello serviço de nuvem pode mudar ao longo do tempo. tooprevent que aconteça, você poderá reservar um VIP para seu serviço. toolearn mais sobre o VIP reservado, consulte [IP público reservado](../virtual-network/virtual-networks-reserved-public-ip.md).

> [!NOTE]
> Consulte [Preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses/) para obter informações sobre preços em VIPs e IPs reservados.

Você pode usar o PowerShell tooverify Olá VIPs usados por seus serviços de nuvem, bem como adicionar e remover VIPs, associar um ponto de extremidade do VIP tooan e configurar o balanceamento de carga em um VIP específico.

## <a name="limitations"></a>Limitações

Neste momento, a funcionalidade de várias VIP é limitado toohello os seguintes cenários:

* **IaaS apenas**. Só é possível habilitar o Multi VIP para serviços de nuvem que contêm VMs. Não é possível usar o Multi VIP em cenários de PaaS com instâncias de função.
* **PowerShell apenas**. Só é possível gerenciar o Multi VIP usando o PowerShell.

Essas limitações são temporárias e podem ser alteradas a qualquer momento. Verifique se toorevisit essa página tooverify as alterações futuras.

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a>Como o serviço de nuvem tooa tooadd um VIP
serviço de tooyour tooadd um VIP, execute o hello comando PowerShell a seguir:

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

Este comando exibe uma toohello semelhante resultado exemplo a seguir:

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a>Como tooremove um VIP de um serviço de nuvem
Olá tooremove VIP adicionado tooyour serviço exemplo hello acima, Olá executar comandos do PowerShell a seguir:

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> Você só pode remover um VIP, se nenhum tooit de pontos de extremidade associados.


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a>Como as informações de tooretrieve VIP de um serviço de nuvem
Olá tooretrieve VIPs associado com um serviço de nuvem, executar Olá script do PowerShell a seguir:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

script Hello exibe um toohello semelhante resultado exemplo a seguir:

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

Neste exemplo, o serviço de nuvem Olá tem 3 VIPs:

* **Vip1** é Olá padrão VIP, você sabe que porque o valor Olá IsDnsProgrammedName é definido tootrue.
* **Vip2** e **Vip3** não são usados porque não têm endereços IP. Eles só serão usados se você associar um ponto de extremidade toohello VIP.

> [!NOTE]
> Sua assinatura só será cobrada por VIPs extras quando eles estiverem associados a um ponto de extremidade. Para obter mais informações sobre preços, consulte [Preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a>Como ponto de extremidade de tooan tooassociate um VIP

tooassociate um VIP em um nuvem serviço tooan ponto de extremidade, execute Olá comando PowerShell a seguir:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

comando Hello cria um ponto de extremidade chamado VIP vinculado toohello *Vip2* na porta *80*e o vincula toohello VM denominada *myVM1* em um serviço de nuvem chamado  *myService* usando *TCP* na porta *8080*.

configuração tooverify hello, executar Olá comando PowerShell a seguir:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

saída de Hello parece semelhante toohello exemplo a seguir:

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a>Como tooenable o balanceamento de carga em um VIP específico

Você pode associar um único VIP com várias máquinas virtuais para fins de balanceamento de carga. Por exemplo, você tem um serviço de nuvem chamado *myService* e duas máquinas virtuais chamadas *myVM1* e *myVM2*. E o serviço de nuvem tem vários VIPs, um deles chamado *Vip2*. Se você quiser que todo o tráfego tooport de tooensure *81* na *Vip2* é equilibrada entre *myVM1* e *myVM2* na porta *8181* , execute hello script do PowerShell a seguir:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

Você também pode atualizar o balanceador de carga toouse um VIP diferente. Por exemplo, se você executar Olá comando PowerShell a seguir, você alterará conjunto toouse um VIP denominado Vip1 de balanceamento de carga de saudação:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a>Próximas etapas

[Log Analytics para o Azure Load Balancer](load-balancer-monitor-log.md)

[Visão geral do balanceador de carga para a Internet](load-balancer-internet-overview.md)

[Introdução ao balanceador de carga para a Internet](load-balancer-get-started-internet-arm-ps.md)

[Visão geral da Rede Virtual](../virtual-network/virtual-networks-overview.md)

[APIs REST com IP Reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx)
