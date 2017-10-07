---
title: Definir aaaCreate uma disponibilidade VM no Azure | Microsoft Docs
description: "Saiba como definir toocreate uma disponibilidade gerenciada ou não gerenciado de disponibilidade definida para suas máquinas virtuais usando o Azure PowerShell ou Olá portal no modelo de implantação do Gerenciador de recursos de saudação."
keywords: conjunto de disponibilidade
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="3d83f-104">Aumentar a disponibilidade da VM criando um conjunto de disponibilidade do Azure</span><span class="sxs-lookup"><span data-stu-id="3d83f-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="3d83f-105">Conjuntos de disponibilidade fornecem aplicativos de tooyour de redundância.</span><span class="sxs-lookup"><span data-stu-id="3d83f-105">Availability sets provide redundancy tooyour application.</span></span> <span data-ttu-id="3d83f-106">Recomendamos o agrupamento de uma ou mais máquinas virtuais em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3d83f-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="3d83f-107">Essa configuração garante que durante a um evento de manutenção planejada ou não planejada, pelo menos uma máquina virtual será Olá disponível e atender 99,95% do SLA do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d83f-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet hello 99.95% Azure SLA.</span></span> <span data-ttu-id="3d83f-108">Para obter mais informações, consulte Olá [SLA para máquinas virtuais](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="3d83f-108">For more information, see hello [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d83f-109">Máquinas virtuais devem ser criados no hello mesmo grupo de recursos como conjunto de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d83f-109">VMs must be created in hello same resource group as hello availability set.</span></span>
> 

<span data-ttu-id="3d83f-110">Se você quiser que sua parte de toobe VM de um conjunto de disponibilidade, você precisa de disponibilidade de saudação do toocreate definir primeiro ou enquanto você estiver criando sua primeira VM no conjunto de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d83f-110">If you want your VM toobe part of an availability set, you need toocreate hello availability set first or while you are creating your first VM in hello set.</span></span> <span data-ttu-id="3d83f-111">Se a VM estiver usando discos gerenciados, o conjunto de disponibilidade de saudação deve ser criado como um conjunto de disponibilidade gerenciada.</span><span class="sxs-lookup"><span data-stu-id="3d83f-111">If your VM will be using Managed Disks, hello availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="3d83f-112">Para obter mais informações sobre como criar e usar conjuntos de disponibilidade, consulte [gerenciar Olá disponibilidade das máquinas virtuais](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3d83f-112">For more information about creating and using availability sets, see [Manage hello availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="3d83f-113">Use Olá portal toocreate um conjunto antes de criar suas VMs de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="3d83f-113">Use hello portal toocreate an availability set before creating your VMs</span></span>
1. <span data-ttu-id="3d83f-114">No menu de hub hello, clique em **procurar** e selecione **conjuntos de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="3d83f-114">In hello hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="3d83f-115">Em Olá **folha de conjuntos de disponibilidade**, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3d83f-115">On hello **Availability sets blade**, click **Add**.</span></span>
   
    ![Captura de tela que mostra Olá adicionar botão para criar um novo conjunto de disponibilidade.](./media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="3d83f-117">Em Olá **criar conjunto de disponibilidade** folha, informações de saudação completa para o conjunto.</span><span class="sxs-lookup"><span data-stu-id="3d83f-117">On hello **Create availability set** blade, complete hello information for your set.</span></span>
   
    ![Captura de tela que mostra Olá informações que você precisa tooenter toocreate Olá disponibilidade definida.](./media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="3d83f-119">**Nome** -nome hello deve ser 1-80 caracteres compostas de números, letras, pontos, sublinhados e traços.</span><span class="sxs-lookup"><span data-stu-id="3d83f-119">**Name** - hello name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="3d83f-120">Olá primeiro caractere deve ser uma letra ou número.</span><span class="sxs-lookup"><span data-stu-id="3d83f-120">hello first character must be a letter or number.</span></span> <span data-ttu-id="3d83f-121">último caractere do Hello deve ser uma letra, número ou sublinhado.</span><span class="sxs-lookup"><span data-stu-id="3d83f-121">hello last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="3d83f-122">**Domínios de falha** -domínios de falha definem o grupo de saudação de máquinas virtuais que compartilham um comutador de origem e de rede de alimentação comum.</span><span class="sxs-lookup"><span data-stu-id="3d83f-122">**Fault domains** - fault domains define hello group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="3d83f-123">Por padrão, Olá VMs estiverem separadas em domínios de falha de toothree e podem ser alterado toobetween 1 e 3.</span><span class="sxs-lookup"><span data-stu-id="3d83f-123">By default, hello VMs  are separated across up toothree fault domains and can be changed toobetween 1 and 3.</span></span>
   * <span data-ttu-id="3d83f-124">**Atualizar domínios** - cinco domínios de atualização são atribuídos por padrão, e isso pode ser definido toobetween 1 e 20.</span><span class="sxs-lookup"><span data-stu-id="3d83f-124">**Update domains** -  five update domains are assigned by default and this can be set toobetween 1 and 20.</span></span> <span data-ttu-id="3d83f-125">Domínios de atualização indicam grupos de máquinas virtuais e o hardware físico subjacente que pode ser reinicializado no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="3d83f-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="3d83f-126">Por exemplo, se especificamos atualização cinco domínios, quando mais de cinco máquinas virtuais são configuradas em um único conjunto de disponibilidade, máquina virtual da sexta hello serão colocados no hello mesmo domínio de atualização como máquina virtual da primeira hello, hello sétima em Olá mesmo UD como máquina virtual da segunda Olá e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="3d83f-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, hello sixth virtual machine will be placed into hello same update domain as hello first virtual machine, hello seventh in hello same UD as hello second virtual machine, and so on.</span></span> <span data-ttu-id="3d83f-127">ordem de saudação de reinicializações de saudação não pode ser sequencial, mas somente uma atualização de domínio será reinicializado por vez.</span><span class="sxs-lookup"><span data-stu-id="3d83f-127">hello order of hello reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="3d83f-128">**Assinatura** -selecione Olá toouse de assinatura, se você tiver mais de um.</span><span class="sxs-lookup"><span data-stu-id="3d83f-128">**Subscription** - select hello subscription toouse if you have more than one.</span></span>
   * <span data-ttu-id="3d83f-129">**Grupo de recursos** -selecione um grupo de recursos existente clicando em seta hello e selecionando um grupo de recursos de saudação lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="3d83f-129">**Resource group** - select an existing resource group by clicking hello arrow and selecting a resource group from hello drop down.</span></span> <span data-ttu-id="3d83f-130">Você também pode criar um novo grupo de recursos digitando um nome.</span><span class="sxs-lookup"><span data-stu-id="3d83f-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="3d83f-131">Olá nome pode conter nenhum dos seguintes caracteres de saudação: letras, números, pontos, traços, sublinhados e abertura ou parêntese de fechamento.</span><span class="sxs-lookup"><span data-stu-id="3d83f-131">hello name can contain any of hello following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="3d83f-132">Olá nome não pode terminar em um período.</span><span class="sxs-lookup"><span data-stu-id="3d83f-132">hello name cannot end in a period.</span></span> <span data-ttu-id="3d83f-133">Todas Olá VMs no grupo de disponibilidade Olá precisam toobe criado no hello mesmo grupo de recursos Olá conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3d83f-133">All of hello VMs in hello availability group need toobe created in hello same resource group as hello availability set.</span></span>
   * <span data-ttu-id="3d83f-134">**Local** -selecione um local na lista suspensa hello.</span><span class="sxs-lookup"><span data-stu-id="3d83f-134">**Location** - select a location from hello drop-down.</span></span>
   * <span data-ttu-id="3d83f-135">**Gerenciado** - selecione *Sim* toocreate uma disponibilidade gerenciada definida toouse com máquinas virtuais que usam discos gerenciados para o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3d83f-135">**Managed** - select *Yes* toocreate a managed availability set toouse with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="3d83f-136">Selecione **não** se Olá VMs no conjunto de saudação usa discos de não gerenciados em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3d83f-136">Select **No** if hello VMs that will be in hello set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="3d83f-137">Quando você terminar de inserir informações de saudação, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="3d83f-137">When you are done entering hello information, click **Create**.</span></span> 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a><span data-ttu-id="3d83f-138">Use Olá toocreate portal uma máquina virtual e uma disponibilidade definidos no hello mesmo tempo</span><span class="sxs-lookup"><span data-stu-id="3d83f-138">Use hello portal toocreate a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="3d83f-139">Se você estiver criando uma nova VM usando o portal de saudação, você também pode criar uma novo conjunto de disponibilidade para Olá VM enquanto você cria Olá primeira VM no conjunto de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d83f-139">If you are creating a new VM using hello portal, you can also create a new availability set for hello VM while you create hello first VM in hello set.</span></span> <span data-ttu-id="3d83f-140">Se você escolher toouse gerenciados discos para sua VM, será criado um conjunto de disponibilidade gerenciada.</span><span class="sxs-lookup"><span data-stu-id="3d83f-140">If you choose toouse Managed Disks for your VM, a managed availability set will be created.</span></span>

![Captura de tela que mostra o processo de Olá para criar uma nova disponibilidade definida durante a criação de saudação VM.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a><span data-ttu-id="3d83f-142">Adicionar uma nova VM tooan existente conjunto de disponibilidade no portal de saudação</span><span class="sxs-lookup"><span data-stu-id="3d83f-142">Add a new VM tooan existing availability set in hello portal</span></span>
<span data-ttu-id="3d83f-143">Para cada VM adicional que você criar que deve pertencer no conjunto de saudação, certifique-se de que você a crie em Olá mesmo **grupo de recursos** e, em seguida, selecione Olá disponibilidade existente, definida na etapa 3.</span><span class="sxs-lookup"><span data-stu-id="3d83f-143">For each additional VM that you create that should belong in hello set, make sure that you create it in hello same **resource group** and then select hello existing availability set in Step 3.</span></span> 

![Captura de tela mostrando como tooselect um grupo de disponibilidade configurado toouse para sua VM.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a><span data-ttu-id="3d83f-145">Use o PowerShell toocreate uma disponibilidade definida</span><span class="sxs-lookup"><span data-stu-id="3d83f-145">Use PowerShell toocreate an availability set</span></span>
<span data-ttu-id="3d83f-146">Este exemplo cria um conjunto nomeada de disponibilidade **myAvailabilitySet** em Olá **myResourceGroup** grupo de recursos em Olá **Oeste dos EUA** local.</span><span class="sxs-lookup"><span data-stu-id="3d83f-146">This example creates an availability set named **myAvailabilitySet** in hello **myResourceGroup** resource group in hello **West US** location.</span></span> <span data-ttu-id="3d83f-147">Isso deve toobe feito antes de criar hello primeira VM que estarão no conjunto de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d83f-147">This needs toobe done before you create hello first VM that will be in hello set.</span></span>

<span data-ttu-id="3d83f-148">Antes de começar, certifique-se de que você tem a versão mais recente Olá de saudação módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3d83f-148">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="3d83f-149">Executar Olá tooinstall de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="3d83f-149">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="3d83f-150">Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="3d83f-150">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


<span data-ttu-id="3d83f-151">Se você estiver usando Managed Disks para suas VMs, digite:</span><span class="sxs-lookup"><span data-stu-id="3d83f-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="3d83f-152">Se você estiver usando suas próprias contas de armazenamento para suas VMs, digite:</span><span class="sxs-lookup"><span data-stu-id="3d83f-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="3d83f-153">Para obter mais informações, consulte [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="3d83f-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3d83f-154">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="3d83f-154">Troubleshooting</span></span>
* <span data-ttu-id="3d83f-155">Quando você cria uma máquina virtual, se conjunto de disponibilidade de saudação desejado não estiver na lista suspensa de saudação no portal de saudação você pode criá-lo em outro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3d83f-155">When you create a VM, if hello availability set you want isn't in hello drop-down list in hello portal you may have created it in a different resource group.</span></span> <span data-ttu-id="3d83f-156">Se você não souber o grupo de recursos de saudação de disponibilidade do seu conjunto, acesse o menu de hub toohello e clique em Procurar > toosee define uma lista de sua disponibilidade e quais grupos de recursos que pertençam a conjuntos de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3d83f-156">If you don't know hello resource group for your availability set, go toohello hub menu and click Browse > Availability sets toosee a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d83f-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3d83f-157">Next steps</span></span>
<span data-ttu-id="3d83f-158">Adicionar armazenamento adicional tooyour VM adicionando mais [disco de dados](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3d83f-158">Add additional storage tooyour VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

