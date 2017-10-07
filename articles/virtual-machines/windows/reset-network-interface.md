---
title: interface de rede tooreset aaaHow para VM do Windows Azure | Microsoft Docs
description: Mostra como tooreset interface de rede de VM do Windows Azure
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
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="cc463-103">Como tooreset interface de rede de VM do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="cc463-103">How tooreset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="cc463-104">Não é possível conectar tooMicrosoft Windows Máquina Virtual (VM) do Azure depois de desabilitar o padrão de saudação de rede (NIC) ou manualmente define um endereço IP estático para a NIC hello.</span><span class="sxs-lookup"><span data-stu-id="cc463-104">You cannot connect tooMicrosoft Azure Windows Virtual Machine (VM) after you disable hello default Network Interface (NIC) or manually sets a static IP for hello NIC.</span></span> <span data-ttu-id="cc463-105">Este artigo mostra como tooreset Olá interface de rede de VM do Windows Azure, que resolverá o problema de conexão remota hello.</span><span class="sxs-lookup"><span data-stu-id="cc463-105">This article shows how tooreset hello network interface for Azure Windows VM, which will resolve hello remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="cc463-106">Redefinir o adaptador de rede</span><span class="sxs-lookup"><span data-stu-id="cc463-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="cc463-107">Para VMs Clássicas</span><span class="sxs-lookup"><span data-stu-id="cc463-107">For Classic VMs</span></span>

<span data-ttu-id="cc463-108">rede tooreset interface, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="cc463-108">tooreset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="cc463-109">Vá toohello [portal do Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cc463-109">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="cc463-110">Selecione **Máquinas Virtuais (Clássicas)**.</span><span class="sxs-lookup"><span data-stu-id="cc463-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="cc463-111">Selecione Olá afetados Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="cc463-111">Select hello affected Virtual Machine.</span></span>
4.  <span data-ttu-id="cc463-112">Selecione **Endereços IP**.</span><span class="sxs-lookup"><span data-stu-id="cc463-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="cc463-113">Se hello **atribuição de IP privado** não é **estático**, alterá-la muito**estático**.</span><span class="sxs-lookup"><span data-stu-id="cc463-113">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
6.  <span data-ttu-id="cc463-114">Saudação de alteração **endereço IP** tooanother endereço IP que está disponível no hello sub-rede.</span><span class="sxs-lookup"><span data-stu-id="cc463-114">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
7.  <span data-ttu-id="cc463-115">Selecione Salvar.</span><span class="sxs-lookup"><span data-stu-id="cc463-115">Select Save.</span></span>
8.  <span data-ttu-id="cc463-116">máquina virtual de saudação reiniciará tooinitialize Olá novo NIC toohello sistema.</span><span class="sxs-lookup"><span data-stu-id="cc463-116">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
9.  <span data-ttu-id="cc463-117">Tente tooRDP tooyour máquina.</span><span class="sxs-lookup"><span data-stu-id="cc463-117">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="cc463-118">Se for bem-sucedido, você pode alterar Olá toohello voltar de endereço de IP privado original se você quiser.</span><span class="sxs-lookup"><span data-stu-id="cc463-118">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="cc463-119">Caso contrário, você poderá mantê-lo.</span><span class="sxs-lookup"><span data-stu-id="cc463-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="cc463-120">Para as VMs implantadas no modelo de Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="cc463-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="cc463-121">Vá toohello [portal do Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cc463-121">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="cc463-122">Selecione Olá afetados Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="cc463-122">Select hello affected Virtual Machine.</span></span>
3.  <span data-ttu-id="cc463-123">Selecione **Adaptadores de Rede**.</span><span class="sxs-lookup"><span data-stu-id="cc463-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="cc463-124">Selecione Olá associado à Interface de rede com sua máquina</span><span class="sxs-lookup"><span data-stu-id="cc463-124">Select hello Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="cc463-125">Selecione **Configurações de IP**.</span><span class="sxs-lookup"><span data-stu-id="cc463-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="cc463-126">Selecione IP hello.</span><span class="sxs-lookup"><span data-stu-id="cc463-126">Select hello IP.</span></span> 
7.  <span data-ttu-id="cc463-127">Se hello **atribuição de IP privado** não é **estático**, alterá-la muito**estático**.</span><span class="sxs-lookup"><span data-stu-id="cc463-127">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
8.  <span data-ttu-id="cc463-128">Saudação de alteração **endereço IP** tooanother endereço IP que está disponível no hello sub-rede.</span><span class="sxs-lookup"><span data-stu-id="cc463-128">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
9. <span data-ttu-id="cc463-129">máquina virtual de saudação reiniciará tooinitialize Olá novo NIC toohello sistema.</span><span class="sxs-lookup"><span data-stu-id="cc463-129">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
10. <span data-ttu-id="cc463-130">Tente tooRDP tooyour máquina.</span><span class="sxs-lookup"><span data-stu-id="cc463-130">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="cc463-131">Se for bem-sucedido, você pode alterar Olá toohello voltar de endereço de IP privado original se você quiser.</span><span class="sxs-lookup"><span data-stu-id="cc463-131">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="cc463-132">Caso contrário, você poderá mantê-lo.</span><span class="sxs-lookup"><span data-stu-id="cc463-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-hello-unavailable-nics"></a><span data-ttu-id="cc463-133">Excluir Olá NICs indisponíveis</span><span class="sxs-lookup"><span data-stu-id="cc463-133">Delete hello unavailable NICs</span></span>
<span data-ttu-id="cc463-134">Depois que você pode máquina toohello de área de trabalho remota, você deve excluir Olá antigo NICs tooavoid Olá problema em potencial:</span><span class="sxs-lookup"><span data-stu-id="cc463-134">After you can remote desktop toohello machine, you must delete hello old NICs tooavoid hello potential problem:</span></span>

1.  <span data-ttu-id="cc463-135">Abra o Gerenciador de Dispositivos.</span><span class="sxs-lookup"><span data-stu-id="cc463-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="cc463-136">Selecione **Exibir** > **Mostrar dispositivos ocultos**.</span><span class="sxs-lookup"><span data-stu-id="cc463-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="cc463-137">Selecione **Adaptadores de Rede**.</span><span class="sxs-lookup"><span data-stu-id="cc463-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="cc463-138">Verifique se há adaptadores Olá nomeadas como "Adaptador de rede do Microsoft Hyper-V".</span><span class="sxs-lookup"><span data-stu-id="cc463-138">Check for hello adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="cc463-139">Talvez você veja um adaptador não disponível que está esmaecido. Clique com botão direito adaptador hello e, em seguida, selecione Desinstalar.</span><span class="sxs-lookup"><span data-stu-id="cc463-139">You might see an unavailable adapter that is grayed out. Right-click hello adapter and then select Uninstall.</span></span>

    ![imagem de saudação do hello NIC](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="cc463-141">Desinstale somente os adaptadores indisponível Olá com nome hello "Adaptador de rede do Microsoft Hyper-V".</span><span class="sxs-lookup"><span data-stu-id="cc463-141">Only uninstall hello unavailable adapters that have hello name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="cc463-142">Se você desinstalar qualquer Olá outros adaptadores ocultados, isso pode causar problemas adicionais.</span><span class="sxs-lookup"><span data-stu-id="cc463-142">If you uninstall any of hello other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="cc463-143">Agora todos os adaptadores não disponíveis deverão ser limpos do sistema.</span><span class="sxs-lookup"><span data-stu-id="cc463-143">Now all unavailable adapter should be cleared out from your system.</span></span>