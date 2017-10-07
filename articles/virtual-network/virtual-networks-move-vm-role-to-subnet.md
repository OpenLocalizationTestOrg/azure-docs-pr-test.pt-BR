---
title: "aaaMove uma VM (clássico) ou serviços de nuvem função instância tooa diferente subnet - PowerShell do Azure | Microsoft Docs"
description: "Saiba como toomove (clássico) de máquinas virtuais e instâncias de função de serviços de nuvem tooa sub-rede diferente usando o PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8d2de56f42a91be4a665414ea9641ffd46588fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a>Mover uma VM (clássico) ou os serviços de nuvem função instância tooa sub-rede diferente usando o PowerShell
Você pode usar PowerShell toomove suas VMs (clássico) de uma sub-rede tooanother Olá mesma rede virtual (VNet). Instâncias de função podem ser movidas por edição Olá CSCFG arquivo, em vez de usar o PowerShell.

> [!NOTE]
> Este artigo explica como toomove VMs implantadas por meio do modelo de implantação clássico Olá somente.
> 
> 

Por que transferir VMs tooanother sub-rede? Migração de sub-rede é útil quando sub-rede antiga Olá é muito pequeno e não pode ser expandido devido tooexisting VMs em execução nessa sub-rede. Nesse caso, você pode criar uma nova sub-rede maior e migrar Olá VMs toohello nova subrede, em seguida, após a conclusão da migração, você pode excluir a sub-rede vazio antigo de saudação.

## <a name="how-toomove-a-vm-tooanother-subnet"></a>Como toomove tooanother uma subrede VM
toomove uma VM, execute o cmdlet do PowerShell do conjunto AzureSubnet de saudação, usando o exemplo hello abaixo como um modelo. O exemplo hello abaixo, vamos mudar TestVM da sua sub-rede atual, tooSubnet-2. Ser tooreflect de exemplo de hello tooedit-se de que seu ambiente. Observe que sempre que você executar o cmdlet Update-AzureVM de saudação como parte de um procedimento, ele reiniciará sua VM como parte do processo de atualização de saudação.

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

Se você tiver especificado um privada endereço IP interno estático para sua VM, você terá tooclear essa configuração antes de você pode mover Olá tooa nova subrede VM. Nesse caso, use o seguinte hello:

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a>toomove uma sub-rede de tooanother de instância de função
toomove uma instância de função, edite o arquivo CSCFG de saudação. O exemplo hello abaixo, vamos mudar "Role0" na rede virtual *VNETName* de sua sub-rede presente muito*Subnet-2*. Porque a instância de função hello já foi implantada, você só alterará o nome de sub-rede hello = Subnet-2. Ser tooreflect de exemplo de hello tooedit-se de que seu ambiente.

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
