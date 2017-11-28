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
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a><span data-ttu-id="31841-103">Mover uma VM (clássico) ou os serviços de nuvem função instância tooa sub-rede diferente usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="31841-103">Move a VM (Classic) or Cloud Services role instance tooa different subnet using PowerShell</span></span>
<span data-ttu-id="31841-104">Você pode usar PowerShell toomove suas VMs (clássico) de uma sub-rede tooanother Olá mesma rede virtual (VNet).</span><span class="sxs-lookup"><span data-stu-id="31841-104">You can use PowerShell toomove your VMs (Classic) from one subnet tooanother in hello same virtual network (VNet).</span></span> <span data-ttu-id="31841-105">Instâncias de função podem ser movidas por edição Olá CSCFG arquivo, em vez de usar o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31841-105">Role instances can be moved by editing hello CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="31841-106">Este artigo explica como toomove VMs implantadas por meio do modelo de implantação clássico Olá somente.</span><span class="sxs-lookup"><span data-stu-id="31841-106">This article explains how toomove VMs deployed through hello classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="31841-107">Por que transferir VMs tooanother sub-rede?</span><span class="sxs-lookup"><span data-stu-id="31841-107">Why move VMs tooanother subnet?</span></span> <span data-ttu-id="31841-108">Migração de sub-rede é útil quando sub-rede antiga Olá é muito pequeno e não pode ser expandido devido tooexisting VMs em execução nessa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="31841-108">Subnet migration is useful when hello older subnet is too small and cannot be expanded due tooexisting running VMs in that subnet.</span></span> <span data-ttu-id="31841-109">Nesse caso, você pode criar uma nova sub-rede maior e migrar Olá VMs toohello nova subrede, em seguida, após a conclusão da migração, você pode excluir a sub-rede vazio antigo de saudação.</span><span class="sxs-lookup"><span data-stu-id="31841-109">In that case, you can create a new, larger subnet and migrate hello VMs toohello new subnet, then after migration is complete, you can delete hello old empty subnet.</span></span>

## <a name="how-toomove-a-vm-tooanother-subnet"></a><span data-ttu-id="31841-110">Como toomove tooanother uma subrede VM</span><span class="sxs-lookup"><span data-stu-id="31841-110">How toomove a VM tooanother subnet</span></span>
<span data-ttu-id="31841-111">toomove uma VM, execute o cmdlet do PowerShell do conjunto AzureSubnet de saudação, usando o exemplo hello abaixo como um modelo.</span><span class="sxs-lookup"><span data-stu-id="31841-111">toomove a VM, run hello Set-AzureSubnet PowerShell cmdlet, using hello example below as a template.</span></span> <span data-ttu-id="31841-112">O exemplo hello abaixo, vamos mudar TestVM da sua sub-rede atual, tooSubnet-2.</span><span class="sxs-lookup"><span data-stu-id="31841-112">In hello example below, we are moving TestVM from its present subnet, tooSubnet-2.</span></span> <span data-ttu-id="31841-113">Ser tooreflect de exemplo de hello tooedit-se de que seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="31841-113">Be sure tooedit hello example tooreflect your environment.</span></span> <span data-ttu-id="31841-114">Observe que sempre que você executar o cmdlet Update-AzureVM de saudação como parte de um procedimento, ele reiniciará sua VM como parte do processo de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="31841-114">Note that whenever you run hello Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of hello update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="31841-115">Se você tiver especificado um privada endereço IP interno estático para sua VM, você terá tooclear essa configuração antes de você pode mover Olá tooa nova subrede VM.</span><span class="sxs-lookup"><span data-stu-id="31841-115">If you specified a static internal private IP for your VM, you'll have tooclear that setting before you can move hello VM tooa new subnet.</span></span> <span data-ttu-id="31841-116">Nesse caso, use o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="31841-116">In that case, use hello following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a><span data-ttu-id="31841-117">toomove uma sub-rede de tooanother de instância de função</span><span class="sxs-lookup"><span data-stu-id="31841-117">toomove a role instance tooanother subnet</span></span>
<span data-ttu-id="31841-118">toomove uma instância de função, edite o arquivo CSCFG de saudação.</span><span class="sxs-lookup"><span data-stu-id="31841-118">toomove a role instance, edit hello CSCFG file.</span></span> <span data-ttu-id="31841-119">O exemplo hello abaixo, vamos mudar "Role0" na rede virtual *VNETName* de sua sub-rede presente muito*Subnet-2*.</span><span class="sxs-lookup"><span data-stu-id="31841-119">In hello example below, we are moving "Role0" in virtual network *VNETName* from its present subnet too*Subnet-2*.</span></span> <span data-ttu-id="31841-120">Porque a instância de função hello já foi implantada, você só alterará o nome de sub-rede hello = Subnet-2.</span><span class="sxs-lookup"><span data-stu-id="31841-120">Because hello role instance was already deployed, you'll just change hello Subnet name = Subnet-2.</span></span> <span data-ttu-id="31841-121">Ser tooreflect de exemplo de hello tooedit-se de que seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="31841-121">Be sure tooedit hello example tooreflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
