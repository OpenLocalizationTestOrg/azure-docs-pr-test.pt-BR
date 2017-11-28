---
title: aaaMove uma VM do Linux no Azure | Microsoft Docs
description: "Mova uma VM do Linux tooanother assinatura do Azure ou o grupo de recursos no modelo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a><span data-ttu-id="70493-103">Mover um VM do Linux tooanother assinatura ou grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="70493-103">Move a Linux VM tooanother subscription or resource group</span></span>
<span data-ttu-id="70493-104">Este artigo orienta como toomove uma VM do Linux entre grupos de recursos ou assinaturas.</span><span class="sxs-lookup"><span data-stu-id="70493-104">This article walks you through how toomove a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="70493-105">Mover uma VM entre as assinaturas pode ser úteis se você tiver criado uma VM em uma assinatura pessoal e agora deseja toomove-assinatura tooyour da empresa.</span><span class="sxs-lookup"><span data-stu-id="70493-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want toomove it tooyour company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="70493-106">No momento, não é possível mover o Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="70493-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="70493-107">Novas IDs de recurso são criados como parte da movimentação de saudação.</span><span class="sxs-lookup"><span data-stu-id="70493-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="70493-108">Após hello VM tiver sido movida, você precisará tooupdate suas ferramentas e scripts toouse Olá novas IDs de recurso.</span><span class="sxs-lookup"><span data-stu-id="70493-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a><span data-ttu-id="70493-109">Use Olá CLI do Azure toomove uma VM</span><span class="sxs-lookup"><span data-stu-id="70493-109">Use hello Azure CLI toomove a VM</span></span>
<span data-ttu-id="70493-110">toosuccessfully mover uma máquina virtual, é necessário toomove Olá VM e todos os seus recursos de suporte.</span><span class="sxs-lookup"><span data-stu-id="70493-110">toosuccessfully move a VM, you need toomove hello VM and all its supporting resources.</span></span> <span data-ttu-id="70493-111">Saudação de uso **Mostrar de grupo do azure** comando toolist todos os recursos de saudação em um grupo de recursos e suas IDs.</span><span class="sxs-lookup"><span data-stu-id="70493-111">Use hello **azure group show** command toolist all hello resources in a resource group and their IDs.</span></span> <span data-ttu-id="70493-112">Ele ajuda a saída de hello toopipe este tooa do arquivo de comando para que você pode copiar e colar Olá IDs em comandos posteriores.</span><span class="sxs-lookup"><span data-stu-id="70493-112">It helps toopipe hello output of this command tooa file so you can copy and paste hello IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="70493-113">toomove uma máquina virtual e seu grupo de recursos de tooanother de recursos, use Olá **mover recursos do azure** comando CLI.</span><span class="sxs-lookup"><span data-stu-id="70493-113">toomove a VM and its resources tooanother resource group, use hello **azure resource move** CLI command.</span></span> <span data-ttu-id="70493-114">saudação de exemplo a seguir mostra como toomove uma máquina virtual e os recursos mais comuns do hello requer.</span><span class="sxs-lookup"><span data-stu-id="70493-114">hello following example shows how toomove a VM and hello most common resources it requires.</span></span> <span data-ttu-id="70493-115">Usamos Olá **-i** parâmetro e passar uma separada por vírgulas lista (sem espaços) de IDs para Olá toomove de recursos.</span><span class="sxs-lookup"><span data-stu-id="70493-115">We use hello **-i** parameter and pass in a comma-separated list (without spaces) of IDs for hello resources toomove.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="70493-116">Se você quiser toomove Olá VM e sua assinatura de recursos diferentes de tooa, adicione Olá **– destino subscriptionId &#60; destinationSubscriptionID &#62;** assinatura de destino do parâmetro toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="70493-116">If you want toomove hello VM and its resources tooa different subscription, add hello **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter toospecify hello destination subscription.</span></span>

<span data-ttu-id="70493-117">Se você estiver trabalhando de saudação de Prompt de comando em um computador Windows, é necessário tooadd um  **$**  na frente dos nomes de variável hello quando você declará-los.</span><span class="sxs-lookup"><span data-stu-id="70493-117">If you are working from hello Command Prompt on a Windows computer, you need tooadd a **$** in front of hello variable names when you declare them.</span></span> <span data-ttu-id="70493-118">Isso não é necessário no Linux.</span><span class="sxs-lookup"><span data-stu-id="70493-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="70493-119">Você será solicitado tooconfirm que você deseja toomove Olá o recurso especificado.</span><span class="sxs-lookup"><span data-stu-id="70493-119">You are asked tooconfirm that you want toomove hello specified resource.</span></span> <span data-ttu-id="70493-120">Tipo **Y** tooconfirm que você deseja que os recursos de saudação do toomove.</span><span class="sxs-lookup"><span data-stu-id="70493-120">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="70493-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70493-121">Next steps</span></span>
<span data-ttu-id="70493-122">Você pode mover vários tipos diferentes de recursos entre grupos de recursos e assinaturas.</span><span class="sxs-lookup"><span data-stu-id="70493-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="70493-123">Para obter mais informações, consulte [Mover grupo de recursos toonew de recursos ou assinatura](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="70493-123">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

