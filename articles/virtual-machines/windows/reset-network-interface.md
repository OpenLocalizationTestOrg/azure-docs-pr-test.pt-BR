---
title: Como redefinir o adaptador de rede de uma VM Windows do Azure | Microsoft Docs
description: Mostra como redefinir o adaptador de rede de uma VM Windows do Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 220e426be20086841854d89831f6c9d67529867f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="e138e-103">Como redefinir o adaptador de rede de uma VM Windows do Azure</span><span class="sxs-lookup"><span data-stu-id="e138e-103">How to reset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="e138e-104">Você não consegue se conectar à VM (Máquina Virtual) Windows do Microsoft Azure depois de desabilitar a NIC (Adaptador de Rede) padrão ou definir um IP estático manualmente para a NIC.</span><span class="sxs-lookup"><span data-stu-id="e138e-104">You cannot connect to Microsoft Azure Windows Virtual Machine (VM) after you disable the default Network Interface (NIC) or manually sets a static IP for the NIC.</span></span> <span data-ttu-id="e138e-105">Este artigo mostra como redefinir o adaptador de rede de uma VM Windows do Azure, o que resolverá o problema de conexão remota.</span><span class="sxs-lookup"><span data-stu-id="e138e-105">This article shows how to reset the network interface for Azure Windows VM, which will resolve the remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="e138e-106">Redefinir o adaptador de rede</span><span class="sxs-lookup"><span data-stu-id="e138e-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="e138e-107">Para VMs Clássicas</span><span class="sxs-lookup"><span data-stu-id="e138e-107">For Classic VMs</span></span>

<span data-ttu-id="e138e-108">Para redefinir o adaptador de rede, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="e138e-108">To reset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="e138e-109">Vá para o [Portal do Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e138e-109">Go to the [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="e138e-110">Selecione **Máquinas Virtuais (Clássicas)**.</span><span class="sxs-lookup"><span data-stu-id="e138e-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="e138e-111">Selecione a Máquina Virtual afetada.</span><span class="sxs-lookup"><span data-stu-id="e138e-111">Select the affected Virtual Machine.</span></span>
4.  <span data-ttu-id="e138e-112">Selecione **Endereços IP**.</span><span class="sxs-lookup"><span data-stu-id="e138e-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="e138e-113">Se a **Atribuição de IP privado** não for **Estática**, altere-a para **Estática**.</span><span class="sxs-lookup"><span data-stu-id="e138e-113">If the **Private IP assignment**  is not  **Static**, change it to **Static**.</span></span>
6.  <span data-ttu-id="e138e-114">Altere o **endereço IP** para outro endereço IP que está disponível na Sub-rede.</span><span class="sxs-lookup"><span data-stu-id="e138e-114">Change the **IP address** to another IP address that is available in the Subnet.</span></span>
7.  <span data-ttu-id="e138e-115">Selecione Salvar.</span><span class="sxs-lookup"><span data-stu-id="e138e-115">Select Save.</span></span>
8.  <span data-ttu-id="e138e-116">A máquina virtual será reiniciada para inicializar a nova NIC no sistema.</span><span class="sxs-lookup"><span data-stu-id="e138e-116">The virtual machine will restart to initialize the new NIC to the system.</span></span>
9.  <span data-ttu-id="e138e-117">Tente executar o RDP no computador.</span><span class="sxs-lookup"><span data-stu-id="e138e-117">Try to RDP to your machine.</span></span> <span data-ttu-id="e138e-118">Se for bem-sucedido, você poderá alterar o endereço IP Privado novamente para o original, se desejar.</span><span class="sxs-lookup"><span data-stu-id="e138e-118">If successful, you can change the Private IP address back to the original if you would like.</span></span> <span data-ttu-id="e138e-119">Caso contrário, você poderá mantê-lo.</span><span class="sxs-lookup"><span data-stu-id="e138e-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="e138e-120">Para as VMs implantadas no modelo de Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e138e-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="e138e-121">Vá para o [Portal do Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e138e-121">Go to the [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="e138e-122">Selecione a Máquina Virtual afetada.</span><span class="sxs-lookup"><span data-stu-id="e138e-122">Select the affected Virtual Machine.</span></span>
3.  <span data-ttu-id="e138e-123">Selecione **Adaptadores de Rede**.</span><span class="sxs-lookup"><span data-stu-id="e138e-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="e138e-124">Selecione o Adaptador de Rede associado ao computador</span><span class="sxs-lookup"><span data-stu-id="e138e-124">Select the Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="e138e-125">Selecione **Configurações de IP**.</span><span class="sxs-lookup"><span data-stu-id="e138e-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="e138e-126">Selecione o IP.</span><span class="sxs-lookup"><span data-stu-id="e138e-126">Select the IP.</span></span> 
7.  <span data-ttu-id="e138e-127">Se a **Atribuição de IP privado** não for **Estática**, altere-a para **Estática**.</span><span class="sxs-lookup"><span data-stu-id="e138e-127">If the **Private IP assignment**  is not  **Static**, change it to **Static**.</span></span>
8.  <span data-ttu-id="e138e-128">Altere o **endereço IP** para outro endereço IP que está disponível na Sub-rede.</span><span class="sxs-lookup"><span data-stu-id="e138e-128">Change the **IP address** to another IP address that is available in the Subnet.</span></span>
9. <span data-ttu-id="e138e-129">A máquina virtual será reiniciada para inicializar a nova NIC no sistema.</span><span class="sxs-lookup"><span data-stu-id="e138e-129">The virtual machine will restart to initialize the new NIC to the system.</span></span>
10. <span data-ttu-id="e138e-130">Tente executar o RDP no computador.</span><span class="sxs-lookup"><span data-stu-id="e138e-130">Try to RDP to your machine.</span></span> <span data-ttu-id="e138e-131">Se for bem-sucedido, você poderá alterar o endereço IP Privado novamente para o original, se desejar.</span><span class="sxs-lookup"><span data-stu-id="e138e-131">If successful, you can change the Private IP address back to the original if you would like.</span></span> <span data-ttu-id="e138e-132">Caso contrário, você poderá mantê-lo.</span><span class="sxs-lookup"><span data-stu-id="e138e-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-the-unavailable-nics"></a><span data-ttu-id="e138e-133">Excluir as NICs não disponíveis</span><span class="sxs-lookup"><span data-stu-id="e138e-133">Delete the unavailable NICs</span></span>
<span data-ttu-id="e138e-134">Depois que você conseguir conectar a área de trabalho remota ao computador, deverá excluir as NICs antigas para evitar o problema potencial:</span><span class="sxs-lookup"><span data-stu-id="e138e-134">After you can remote desktop to the machine, you must delete the old NICs to avoid the potential problem:</span></span>

1.  <span data-ttu-id="e138e-135">Abra o Gerenciador de Dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e138e-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="e138e-136">Selecione **Exibir** > **Mostrar dispositivos ocultos**.</span><span class="sxs-lookup"><span data-stu-id="e138e-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="e138e-137">Selecione **Adaptadores de Rede**.</span><span class="sxs-lookup"><span data-stu-id="e138e-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="e138e-138">Verifique os adaptadores nomeados como “Adaptador de Rede do Microsoft Hyper-V”.</span><span class="sxs-lookup"><span data-stu-id="e138e-138">Check for the adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="e138e-139">Talvez você veja um adaptador não disponível que está esmaecido.</span><span class="sxs-lookup"><span data-stu-id="e138e-139">You might see an unavailable adapter that is grayed out.</span></span> <span data-ttu-id="e138e-140">Clique com o botão direito do mouse no adaptador e, em seguida, selecione Desinstalar.</span><span class="sxs-lookup"><span data-stu-id="e138e-140">Right-click the adapter and then select Uninstall.</span></span>

    ![a imagem da NIC](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="e138e-142">Desinstale somente os adaptadores não disponíveis que têm o nome “Adaptador de Rede do Microsoft Hyper-V”.</span><span class="sxs-lookup"><span data-stu-id="e138e-142">Only uninstall the unavailable adapters that have the name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="e138e-143">Se você desinstalar um dos outros adaptadores ocultos, isso poderá causar outros problemas.</span><span class="sxs-lookup"><span data-stu-id="e138e-143">If you uninstall any of the other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="e138e-144">Agora todos os adaptadores não disponíveis deverão ser limpos do sistema.</span><span class="sxs-lookup"><span data-stu-id="e138e-144">Now all unavailable adapter should be cleared out from your system.</span></span>