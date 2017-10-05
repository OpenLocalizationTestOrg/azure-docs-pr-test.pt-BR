---
title: "Mover uma VM (Clássico) ou uma instância de função de Serviços de Nuvem para uma sub-rede diferente - Azure PowerShell | Microsoft Docs"
description: "Aprenda a mover VMs (Clássico) e instâncias de função de Serviços de Nuvem para uma sub-rede diferente usando o PowerShell."
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
ms.openlocfilehash: b094f8338394ef2e84cad3070936d715411326a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-to-a-different-subnet-using-powershell"></a><span data-ttu-id="4e18a-103">Mover uma VM (Clássico) ou uma instância de função de Serviços de Nuvem para uma sub-rede diferente usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e18a-103">Move a VM (Classic) or Cloud Services role instance to a different subnet using PowerShell</span></span>
<span data-ttu-id="4e18a-104">Você pode usar o PowerShell para mover suas VMs (Clássico) de uma sub-rede para outra na mesma rede virtual (VNet).</span><span class="sxs-lookup"><span data-stu-id="4e18a-104">You can use PowerShell to move your VMs (Classic) from one subnet to another in the same virtual network (VNet).</span></span> <span data-ttu-id="4e18a-105">As instâncias de função podem ser movidas editando o arquivo CSCFG em vez de usar o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e18a-105">Role instances can be moved by editing the CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="4e18a-106">Este artigo explica como mover VMs implantadas somente por meio do modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="4e18a-106">This article explains how to move VMs deployed through the classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="4e18a-107">Por que transferir VMs para outra sub-rede?</span><span class="sxs-lookup"><span data-stu-id="4e18a-107">Why move VMs to another subnet?</span></span> <span data-ttu-id="4e18a-108">A migração de sub-rede é útil quando a sub-rede antiga é muito pequena e não pode ser expandida devido às VMs existentes em execução nessa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="4e18a-108">Subnet migration is useful when the older subnet is too small and cannot be expanded due to existing running VMs in that subnet.</span></span> <span data-ttu-id="4e18a-109">Nesse caso, você pode criar uma nova sub-rede maior e migrar as máquinas virtuais para a nova sub-rede. Após a conclusão da migração, você pode excluir a sub-rede antiga vazia.</span><span class="sxs-lookup"><span data-stu-id="4e18a-109">In that case, you can create a new, larger subnet and migrate the VMs to the new subnet, then after migration is complete, you can delete the old empty subnet.</span></span>

## <a name="how-to-move-a-vm-to-another-subnet"></a><span data-ttu-id="4e18a-110">Como mover uma VM para outra sub-rede</span><span class="sxs-lookup"><span data-stu-id="4e18a-110">How to move a VM to another subnet</span></span>
<span data-ttu-id="4e18a-111">Para mover uma VM, execute o cmdlet Set-AzureSubnet PowerShell usando o exemplo abaixo como um modelo.</span><span class="sxs-lookup"><span data-stu-id="4e18a-111">To move a VM, run the Set-AzureSubnet PowerShell cmdlet, using the example below as a template.</span></span> <span data-ttu-id="4e18a-112">No exemplo a seguir, transferimos TestVM da sub-rede atual para Subnet-2.</span><span class="sxs-lookup"><span data-stu-id="4e18a-112">In the example below, we are moving TestVM from its present subnet, to Subnet-2.</span></span> <span data-ttu-id="4e18a-113">Não deixe de editar o exemplo para refletir o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="4e18a-113">Be sure to edit the example to reflect your environment.</span></span> <span data-ttu-id="4e18a-114">Observe que sempre que você executar o cmdlet Update-AzureVM como parte de um procedimento, ele reiniciará a sua VM como parte do processo de atualização.</span><span class="sxs-lookup"><span data-stu-id="4e18a-114">Note that whenever you run the Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of the update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="4e18a-115">Se você especificou um IP privado interno estático para a sua VM, terá que desmarcar essa configuração antes de poder mover a máquina virtual para uma nova sub-rede.</span><span class="sxs-lookup"><span data-stu-id="4e18a-115">If you specified a static internal private IP for your VM, you'll have to clear that setting before you can move the VM to a new subnet.</span></span> <span data-ttu-id="4e18a-116">Nesse caso, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4e18a-116">In that case, use the following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="to-move-a-role-instance-to-another-subnet"></a><span data-ttu-id="4e18a-117">Para mover uma instância de função para outra sub-rede</span><span class="sxs-lookup"><span data-stu-id="4e18a-117">To move a role instance to another subnet</span></span>
<span data-ttu-id="4e18a-118">Para mover uma instância de função, edite o arquivo CSCFG.</span><span class="sxs-lookup"><span data-stu-id="4e18a-118">To move a role instance, edit the CSCFG file.</span></span> <span data-ttu-id="4e18a-119">No exemplo a seguir, transferimos "Role0" na rede virtual *VNETName* da sub-rede atual para *Subnet-2*.</span><span class="sxs-lookup"><span data-stu-id="4e18a-119">In the example below, we are moving "Role0" in virtual network *VNETName* from its present subnet to *Subnet-2*.</span></span> <span data-ttu-id="4e18a-120">Como a instância de função já foi implantada, você só alterará o nome da sub-rede = Subnet-2.</span><span class="sxs-lookup"><span data-stu-id="4e18a-120">Because the role instance was already deployed, you'll just change the Subnet name = Subnet-2.</span></span> <span data-ttu-id="4e18a-121">Não deixe de editar o exemplo para refletir o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="4e18a-121">Be sure to edit the example to reflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
