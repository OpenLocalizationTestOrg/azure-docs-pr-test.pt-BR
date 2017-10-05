---
title: Criar um conjunto de disponibilidade de VM no Azure | Microsoft Docs
description: "Saiba como criar um conjunto de disponibilidade gerenciado ou não gerenciado para suas máquinas virtuais usando o Azure PowerShell ou o portal no modelo de implantação do Resource Manager."
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
ms.openlocfilehash: e813ade8e105169f21138ed8a8eafda1ff39f42e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="78d0f-104">Aumentar a disponibilidade da VM criando um conjunto de disponibilidade do Azure</span><span class="sxs-lookup"><span data-stu-id="78d0f-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="78d0f-105">Os conjuntos de disponibilidade fornecem redundância ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="78d0f-105">Availability sets provide redundancy to your application.</span></span> <span data-ttu-id="78d0f-106">Recomendamos o agrupamento de uma ou mais máquinas virtuais em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="78d0f-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="78d0f-107">Essa configuração garante que durante um evento de manutenção planejada ou não planejada, pelo menos uma máquina virtual estará disponível e atenderá os 99,95% SLA do Azure.</span><span class="sxs-lookup"><span data-stu-id="78d0f-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet the 99.95% Azure SLA.</span></span> <span data-ttu-id="78d0f-108">Para saber mais, confira [SLA para máquinas virtuais](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="78d0f-108">For more information, see the [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78d0f-109">A VM deve ser criada no mesmo grupo de recursos que o grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="78d0f-109">VMs must be created in the same resource group as the availability set.</span></span>
> 

<span data-ttu-id="78d0f-110">Se você quiser que sua VM faça parte de um conjunto de disponibilidade, crie o conjunto de disponibilidade primeiro ou durante a criação da VM no conjunto.</span><span class="sxs-lookup"><span data-stu-id="78d0f-110">If you want your VM to be part of an availability set, you need to create the availability set first or while you are creating your first VM in the set.</span></span> <span data-ttu-id="78d0f-111">Se a VM for usar o Managed Disks, o conjunto de disponibilidade deverá ser criado como um conjunto de disponibilidade gerenciado.</span><span class="sxs-lookup"><span data-stu-id="78d0f-111">If your VM will be using Managed Disks, the availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="78d0f-112">Para obter mais informações sobre como criar e usar conjuntos de disponibilidade, confira [Gerenciar a disponibilidade de máquinas virtuais](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78d0f-112">For more information about creating and using availability sets, see [Manage the availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-the-portal-to-create-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="78d0f-113">Usar o portal para criar um conjunto de disponibilidade antes de criar suas VMs</span><span class="sxs-lookup"><span data-stu-id="78d0f-113">Use the portal to create an availability set before creating your VMs</span></span>
1. <span data-ttu-id="78d0f-114">No menu hub, clique em **Procurar** e selecione **Conjuntos de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="78d0f-114">In the hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="78d0f-115">Na **folha Conjuntos de disponibilidade**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="78d0f-115">On the **Availability sets blade**, click **Add**.</span></span>
   
    ![Captura de tela que mostra o botão de adição para criar um novo conjunto de disponibilidade.](./media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="78d0f-117">Na folha **Criar conjunto de disponibilidade** , preencha as informações para o conjunto.</span><span class="sxs-lookup"><span data-stu-id="78d0f-117">On the **Create availability set** blade, complete the information for your set.</span></span>
   
    ![Captura de tela que mostra as informações que você precisa inserir para criar o conjunto de disponibilidade.](./media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="78d0f-119">**Nome** : o nome deve ter de 1 a 80 caracteres compostos por números, letras, pontos, sublinhados e traços.</span><span class="sxs-lookup"><span data-stu-id="78d0f-119">**Name** - the name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="78d0f-120">O primeiro caractere deve ser uma letra ou um número.</span><span class="sxs-lookup"><span data-stu-id="78d0f-120">The first character must be a letter or number.</span></span> <span data-ttu-id="78d0f-121">O último caractere deve ser uma letra, um número ou um sublinhado.</span><span class="sxs-lookup"><span data-stu-id="78d0f-121">The last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="78d0f-122">**Domínios de falha** : os domínios de falha definem o grupo de máquinas virtuais que compartilham uma fonte de energia e um comutador de rede comuns.</span><span class="sxs-lookup"><span data-stu-id="78d0f-122">**Fault domains** - fault domains define the group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="78d0f-123">Por padrão, as VMs são separadas em até três domínios de falha e podem ser mudadas para entre 1 e 3.</span><span class="sxs-lookup"><span data-stu-id="78d0f-123">By default, the VMs  are separated across up to three fault domains and can be changed to between 1 and 3.</span></span>
   * <span data-ttu-id="78d0f-124">**Domínios de atualização** - cinco domínios de atualização são atribuídos por padrão e isso pode ser definido como entre 1 e 20.</span><span class="sxs-lookup"><span data-stu-id="78d0f-124">**Update domains** -  five update domains are assigned by default and this can be set to between 1 and 20.</span></span> <span data-ttu-id="78d0f-125">Os domínios de atualização indicam grupos de máquinas virtuais e hardware físico subjacente que podem ser reinicializados ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="78d0f-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="78d0f-126">Por exemplo, se especificarmos cinco domínios de atualização, quando mais do que cinco máquinas virtuais forem configuradas em um único conjunto de disponibilidade, a sexta máquina virtual será colocada no mesmo domínio de atualização que a primeira máquina virtual, a sétima no mesmo UD que a segunda e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="78d0f-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, the sixth virtual machine will be placed into the same update domain as the first virtual machine, the seventh in the same UD as the second virtual machine, and so on.</span></span> <span data-ttu-id="78d0f-127">A ordem da reinicialização poderá não ser sequencial, mas apenas um domínio de atualização será reinicializado por vez.</span><span class="sxs-lookup"><span data-stu-id="78d0f-127">The order of the reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="78d0f-128">**Assinatura** – selecione a assinatura a ser usada, caso tenha mais de uma.</span><span class="sxs-lookup"><span data-stu-id="78d0f-128">**Subscription** - select the subscription to use if you have more than one.</span></span>
   * <span data-ttu-id="78d0f-129">**Grupo de recursos** : selecione um grupo de recursos existente, clicando na seta e selecionando um grupo de recursos no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="78d0f-129">**Resource group** - select an existing resource group by clicking the arrow and selecting a resource group from the drop down.</span></span> <span data-ttu-id="78d0f-130">Você também pode criar um novo grupo de recursos digitando um nome.</span><span class="sxs-lookup"><span data-stu-id="78d0f-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="78d0f-131">O nome pode conter qualquer um dos seguintes caracteres: letras, números, pontos, traços, sublinhados e parênteses de abertura ou fechamento.</span><span class="sxs-lookup"><span data-stu-id="78d0f-131">The name can contain any of the following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="78d0f-132">O nome não pode terminar em um ponto.</span><span class="sxs-lookup"><span data-stu-id="78d0f-132">The name cannot end in a period.</span></span> <span data-ttu-id="78d0f-133">Todas as VMs no grupo de disponibilidade precisam ser criadas no mesmo grupo de recursos do conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="78d0f-133">All of the VMs in the availability group need to be created in the same resource group as the availability set.</span></span>
   * <span data-ttu-id="78d0f-134">**Localização** : selecione uma localização na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="78d0f-134">**Location** - select a location from the drop-down.</span></span>
   * <span data-ttu-id="78d0f-135">**Gerenciado** - selecione *Sim* para criar um conjunto de disponibilidade gerenciado para usar com VMs que usam o Managed Disks para armazenamento.</span><span class="sxs-lookup"><span data-stu-id="78d0f-135">**Managed** - select *Yes* to create a managed availability set to use with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="78d0f-136">Selecione **Não** se as VMs que estarão no conjunto usam discos não gerenciados em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="78d0f-136">Select **No** if the VMs that will be in the set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="78d0f-137">Quando terminar de inserir as informações, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="78d0f-137">When you are done entering the information, click **Create**.</span></span> 

## <a name="use-the-portal-to-create-a-virtual-machine-and-an-availability-set-at-the-same-time"></a><span data-ttu-id="78d0f-138">Usar o portal para criar uma máquina virtual e um conjunto de disponibilidade ao mesmo tempo</span><span class="sxs-lookup"><span data-stu-id="78d0f-138">Use the portal to create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="78d0f-139">Se estiver criando uma nova VM usando o portal, você também poderá criar um novo conjunto de disponibilidade para a nova VM enquanto cria a primeira VM no conjunto.</span><span class="sxs-lookup"><span data-stu-id="78d0f-139">If you are creating a new VM using the portal, you can also create a new availability set for the VM while you create the first VM in the set.</span></span> <span data-ttu-id="78d0f-140">Se você optar por usar o Managed Disks para sua VM, um conjunto de disponibilidade gerenciado será criado.</span><span class="sxs-lookup"><span data-stu-id="78d0f-140">If you choose to use Managed Disks for your VM, a managed availability set will be created.</span></span>

![Captura de tela que mostra o processo para criar um novo conjunto de disponibilidade ao criar a VM.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-to-an-existing-availability-set-in-the-portal"></a><span data-ttu-id="78d0f-142">Adicionar uma nova VM a um conjunto de disponibilidade existente no portal</span><span class="sxs-lookup"><span data-stu-id="78d0f-142">Add a new VM to an existing availability set in the portal</span></span>
<span data-ttu-id="78d0f-143">Para cada VM adicional que você criar e que deva pertencer ao conjunto, certifique-se de criá-la no mesmo **grupo de recursos** e selecione o conjunto de disponibilidade existente na Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="78d0f-143">For each additional VM that you create that should belong in the set, make sure that you create it in the same **resource group** and then select the existing availability set in Step 3.</span></span> 

![Captura de tela mostrando como selecionar um conjunto de disponibilidade existente para ser usado com sua VM.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-to-create-an-availability-set"></a><span data-ttu-id="78d0f-145">Usar o PowerShell para criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="78d0f-145">Use PowerShell to create an availability set</span></span>
<span data-ttu-id="78d0f-146">Este exemplo cria um conjunto de disponibilidade chamado **myAvailabilitySet** no grupo de recursos **myResourceGroup** na localização **Oeste dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="78d0f-146">This example creates an availability set named **myAvailabilitySet** in the **myResourceGroup** resource group in the **West US** location.</span></span> <span data-ttu-id="78d0f-147">Isso precisa ser feito antes de criar a primeira VM que estará no conjunto.</span><span class="sxs-lookup"><span data-stu-id="78d0f-147">This needs to be done before you create the first VM that will be in the set.</span></span>

<span data-ttu-id="78d0f-148">Antes de começar, verifique se você tem a versão mais recente do módulo AzureRM.Compute do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78d0f-148">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="78d0f-149">Execute o comando a seguir para instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="78d0f-149">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="78d0f-150">Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="78d0f-150">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


<span data-ttu-id="78d0f-151">Se você estiver usando Managed Disks para suas VMs, digite:</span><span class="sxs-lookup"><span data-stu-id="78d0f-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="78d0f-152">Se você estiver usando suas próprias contas de armazenamento para suas VMs, digite:</span><span class="sxs-lookup"><span data-stu-id="78d0f-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="78d0f-153">Para obter mais informações, consulte [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="78d0f-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="78d0f-154">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="78d0f-154">Troubleshooting</span></span>
* <span data-ttu-id="78d0f-155">Ao criar uma VM, se o conjunto de disponibilidade desejado não estiver na lista suspensa no portal, você poderá ter realizado a criação dele em um grupo de recursos diferente.</span><span class="sxs-lookup"><span data-stu-id="78d0f-155">When you create a VM, if the availability set you want isn't in the drop-down list in the portal you may have created it in a different resource group.</span></span> <span data-ttu-id="78d0f-156">Se você não souber o grupo de recursos para sua seu conjunto de disponibilidade, vá até o menu hub e clique em Procurar > Conjuntos de disponibilidade para ver uma lista dos seus conjuntos de disponibilidade e a quais grupos de recursos pertencem.</span><span class="sxs-lookup"><span data-stu-id="78d0f-156">If you don't know the resource group for your availability set, go to the hub menu and click Browse > Availability sets to see a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78d0f-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="78d0f-157">Next steps</span></span>
<span data-ttu-id="78d0f-158">Adicione armazenamento adicional à sua VM incluindo um [disco de dados](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)adicional.</span><span class="sxs-lookup"><span data-stu-id="78d0f-158">Add additional storage to your VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

