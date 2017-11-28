---
title: Exemplo de script do Azure PowerShell- Criar uma VM anexando um disco gerenciado como disco do sistema operacional | Microsoft Docs
description: Exemplo de script do Azure PowerShell- Criar uma VM anexando um disco gerenciado como disco do sistema operacional
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
ms.openlocfilehash: ec532811e94647c8a04b9faf9474f6749969f83e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="a69a0-103">Criar uma máquina virtual usando um disco de sistema operacional gerenciado existente com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a69a0-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="a69a0-104">Esse script cria uma máquina virtual anexando um disco gerenciado existente como disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="a69a0-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="a69a0-105">Use esse script em cenários anteriores:</span><span class="sxs-lookup"><span data-stu-id="a69a0-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="a69a0-106">Criar uma VM de um disco de sistema operacional gerenciado existente que foi copiado de um disco gerenciado em uma assinatura diferente</span><span class="sxs-lookup"><span data-stu-id="a69a0-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="a69a0-107">Criar uma VM de um disco gerenciado existente que foi criado de um arquivo VHD especializado</span><span class="sxs-lookup"><span data-stu-id="a69a0-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="a69a0-108">Criar uma VM de um disco do sistema operacional gerenciado existente que foi criado de um instantâneo</span><span class="sxs-lookup"><span data-stu-id="a69a0-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a69a0-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="a69a0-109">Sample script</span></span>

<span data-ttu-id="a69a0-110">[!code-powershell[principal](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Criar VM por meio do instantâneo")]</span><span class="sxs-lookup"><span data-stu-id="a69a0-110">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a69a0-111">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="a69a0-111">Clean up deployment</span></span> 

<span data-ttu-id="a69a0-112">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="a69a0-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a69a0-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="a69a0-113">Script explanation</span></span>

<span data-ttu-id="a69a0-114">Esse script usa os seguintes comandos para obter as propriedades do disco gerenciado, anexar um disco gerenciado em uma nova VM e criar uma VM.</span><span class="sxs-lookup"><span data-stu-id="a69a0-114">This script uses the following commands to get managed disk properties, attach a managed disk to a new VM and create a VM.</span></span> <span data-ttu-id="a69a0-115">Cada item em que a tabela contém links para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="a69a0-115">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a69a0-116">Command</span><span class="sxs-lookup"><span data-stu-id="a69a0-116">Command</span></span> | <span data-ttu-id="a69a0-117">Observações</span><span class="sxs-lookup"><span data-stu-id="a69a0-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a69a0-118">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="a69a0-118">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="a69a0-119">Obtém o objeto de disco com base no nome e no grupo de recursos de um disco.</span><span class="sxs-lookup"><span data-stu-id="a69a0-119">Gets disk object based on the name and the resource group of a disk.</span></span> <span data-ttu-id="a69a0-120">A propriedade de ID do objeto de disco retornado é usada para anexar o disco a uma nova VM</span><span class="sxs-lookup"><span data-stu-id="a69a0-120">Id property of the returned disk object is used to attach the disk to a new VM</span></span> |
| [<span data-ttu-id="a69a0-121">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="a69a0-121">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="a69a0-122">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="a69a0-122">Creates a VM configuration.</span></span> <span data-ttu-id="a69a0-123">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="a69a0-123">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="a69a0-124">A configuração é usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="a69a0-124">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="a69a0-125">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="a69a0-125">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="a69a0-126">Anexa um disco gerenciado usando a propriedade de ID do disco como disco do sistema operacional a uma nova máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a69a0-126">Attaches a managed disk using the Id property of the disk as OS disk to a new virtual machine</span></span> |
| [<span data-ttu-id="a69a0-127">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="a69a0-127">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="a69a0-128">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="a69a0-128">Creates a public IP address.</span></span> |
| [<span data-ttu-id="a69a0-129">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="a69a0-129">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="a69a0-130">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="a69a0-130">Creates a network interface.</span></span> |
| [<span data-ttu-id="a69a0-131">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="a69a0-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="a69a0-132">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a69a0-132">Create a virtual machine.</span></span> |
|[<span data-ttu-id="a69a0-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a69a0-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="a69a0-134">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="a69a0-134">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a69a0-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a69a0-135">Next steps</span></span>

<span data-ttu-id="a69a0-136">Para obter mais informações sobre o módulo do Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a69a0-136">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a69a0-137">Amostras de script do PowerShell da máquina virtual adicionais podem ser encontrados na [documentação da VM Windows do Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a69a0-137">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>