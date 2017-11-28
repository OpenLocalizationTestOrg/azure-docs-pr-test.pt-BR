---
title: "Exemplo de script do Azure PowerShell – Criar uma VM de um instantâneo | Microsoft Docs"
description: "Exemplo de script do Azure PowerShell – Criar uma VM de um instantâneo"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 63d108bbfd0f58f8a40bf1c7c8649e3a1f7ed288
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="06a04-103">Criar uma máquina virtual de um instantâneo com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="06a04-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="06a04-104">Esse script cria uma máquina virtual de um instantâneo de um disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="06a04-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="06a04-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="06a04-105">Sample script</span></span>

<span data-ttu-id="06a04-106">[!code-powershell[principal](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Criar VM por meio de um disco de sistema operacional gerenciado")]</span><span class="sxs-lookup"><span data-stu-id="06a04-106">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="06a04-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="06a04-107">Clean up deployment</span></span> 

<span data-ttu-id="06a04-108">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="06a04-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="06a04-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="06a04-109">Script explanation</span></span>

<span data-ttu-id="06a04-110">Esse script usa os seguintes comandos para obter as propriedades de instantâneo, criar um disco gerenciado de um instantâneo e criar uma VM.</span><span class="sxs-lookup"><span data-stu-id="06a04-110">This script uses the following commands to get snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="06a04-111">Cada item em que a tabela contém links para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="06a04-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="06a04-112">Command</span><span class="sxs-lookup"><span data-stu-id="06a04-112">Command</span></span> | <span data-ttu-id="06a04-113">Observações</span><span class="sxs-lookup"><span data-stu-id="06a04-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="06a04-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="06a04-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="06a04-115">Obtém um instantâneo usando o nome do instantâneo.</span><span class="sxs-lookup"><span data-stu-id="06a04-115">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="06a04-116">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="06a04-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="06a04-117">Cria uma configuração de disco.</span><span class="sxs-lookup"><span data-stu-id="06a04-117">Creates a disk configuration.</span></span> <span data-ttu-id="06a04-118">Essa configuração é usada com o processo de criação de disco.</span><span class="sxs-lookup"><span data-stu-id="06a04-118">This configuration is used with the disk creation process.</span></span> |
| [<span data-ttu-id="06a04-119">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="06a04-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="06a04-120">Cria um disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="06a04-120">Creates a managed disk.</span></span> |
| [<span data-ttu-id="06a04-121">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="06a04-121">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="06a04-122">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="06a04-122">Creates a VM configuration.</span></span> <span data-ttu-id="06a04-123">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="06a04-123">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="06a04-124">A configuração é usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="06a04-124">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="06a04-125">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="06a04-125">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="06a04-126">Anexa o disco gerenciado como disco do sistema operacional à máquina virtual</span><span class="sxs-lookup"><span data-stu-id="06a04-126">Attaches the managed disk as OS disk to the virtual machine</span></span> |
| [<span data-ttu-id="06a04-127">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="06a04-127">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="06a04-128">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="06a04-128">Creates a public IP address.</span></span> |
| [<span data-ttu-id="06a04-129">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="06a04-129">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="06a04-130">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="06a04-130">Creates a network interface.</span></span> |
| [<span data-ttu-id="06a04-131">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="06a04-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="06a04-132">Cria uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="06a04-132">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="06a04-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06a04-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="06a04-134">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="06a04-134">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="06a04-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="06a04-135">Next steps</span></span>

<span data-ttu-id="06a04-136">Para obter mais informações sobre o módulo do Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="06a04-136">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="06a04-137">Amostras de script do PowerShell da máquina virtual adicionais podem ser encontrados na [documentação da VM Windows do Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06a04-137">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>