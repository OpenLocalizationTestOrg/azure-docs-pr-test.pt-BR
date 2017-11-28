---
title: "aaaMove um recurso de máquina virtual do Windows no Azure | Microsoft Docs"
description: "Mova uma máquina virtual do Windows tooanother assinatura do Azure ou o grupo de recursos no modelo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 859e78dce9acf1168780d4ee8e9f6dac0e3c11cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a><span data-ttu-id="f621d-103">Mover uma máquina virtual do Windows tooanother assinatura do Azure ou o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f621d-103">Move a Windows VM tooanother Azure subscription or resource group</span></span>
<span data-ttu-id="f621d-104">Este artigo orienta como toomove uma VM do Windows entre grupos de recursos ou assinaturas.</span><span class="sxs-lookup"><span data-stu-id="f621d-104">This article walks you through how toomove a Windows VM between resource groups or subscriptions.</span></span> <span data-ttu-id="f621d-105">Mover entre assinaturas pode ser úteis se você criou uma VM em uma assinatura pessoal e agora deseja toomove-toocontinue de assinatura da empresa tooyour seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="f621d-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want toomove it tooyour company's subscription toocontinue your work.</span></span>

> [!IMPORTANT]
><span data-ttu-id="f621d-106">No momento, não é possível mover o Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="f621d-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="f621d-107">Novas IDs de recurso são criados como parte da movimentação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f621d-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="f621d-108">Após hello VM tiver sido movida, você precisará tooupdate suas ferramentas e scripts toouse Olá novas IDs de recurso.</span><span class="sxs-lookup"><span data-stu-id="f621d-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a><span data-ttu-id="f621d-109">Use o Powershell toomove uma VM</span><span class="sxs-lookup"><span data-stu-id="f621d-109">Use Powershell toomove a VM</span></span>
<span data-ttu-id="f621d-110">toomove um grupo de recursos de tooanother da máquina virtual, você precisa toomake-se de que você mova também todos os recursos dependentes hello.</span><span class="sxs-lookup"><span data-stu-id="f621d-110">toomove a virtual machine tooanother resource group, you need toomake sure that you also move all of hello dependent resources.</span></span> <span data-ttu-id="f621d-111">toouse Olá Move-AzureRMResource cmdlet, que você precisa que o nome do recurso hello e Olá tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="f621d-111">toouse hello Move-AzureRMResource cmdlet, you need hello resource name and hello type of resource.</span></span> <span data-ttu-id="f621d-112">Você pode obter ambos Olá Find-AzureRMResource cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f621d-112">You can get both from hello Find-AzureRMResource cmdlet.</span></span>

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


<span data-ttu-id="f621d-113">toomove uma VM que precisamos toomove vários recursos.</span><span class="sxs-lookup"><span data-stu-id="f621d-113">toomove a VM we need toomove multiple resources.</span></span> <span data-ttu-id="f621d-114">Podemos criar variáveis separadas para cada recurso e depois listá-las.</span><span class="sxs-lookup"><span data-stu-id="f621d-114">We can just create separate variables for each resource and then list them.</span></span> <span data-ttu-id="f621d-115">Este exemplo inclui a maioria dos recursos básicos de saudação para uma VM, mas você pode adicionar mais conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f621d-115">This example includes most of hello basic resources for a VM, but you can add more as needed.</span></span>

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

<span data-ttu-id="f621d-116">toomove Olá assinatura de recursos de toodifferent, incluir Olá **- DestinationSubscriptionId** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="f621d-116">toomove hello resources toodifferent subscription, include hello **-DestinationSubscriptionId** parameter.</span></span> 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



<span data-ttu-id="f621d-117">Você será solicitado tooconfirm que você deseja toomove Olá especificado recursos.</span><span class="sxs-lookup"><span data-stu-id="f621d-117">You will be asked tooconfirm that you want toomove hello specified resources.</span></span> <span data-ttu-id="f621d-118">Tipo **Y** tooconfirm que você deseja que os recursos de saudação do toomove.</span><span class="sxs-lookup"><span data-stu-id="f621d-118">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f621d-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f621d-119">Next steps</span></span>
<span data-ttu-id="f621d-120">Você pode mover vários tipos diferentes de recursos entre grupos de recursos e assinaturas.</span><span class="sxs-lookup"><span data-stu-id="f621d-120">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="f621d-121">Para obter mais informações, consulte [Mover grupo de recursos toonew de recursos ou assinatura](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="f621d-121">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

