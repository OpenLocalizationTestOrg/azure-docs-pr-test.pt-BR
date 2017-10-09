---
title: "aaaAzure exemplo de Script do PowerShell - criar uma máquina virtual, anexando um disco gerenciado como disco do sistema operacional | Microsoft Docs"
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
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="b9a71-103">Criar uma máquina virtual usando um disco de sistema operacional gerenciado existente com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a71-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="b9a71-104">Esse script cria uma máquina virtual anexando um disco gerenciado existente como disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="b9a71-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="b9a71-105">Use esse script em cenários anteriores:</span><span class="sxs-lookup"><span data-stu-id="b9a71-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="b9a71-106">Criar uma VM de um disco de sistema operacional gerenciado existente que foi copiado de um disco gerenciado em uma assinatura diferente</span><span class="sxs-lookup"><span data-stu-id="b9a71-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="b9a71-107">Criar uma VM de um disco gerenciado existente que foi criado de um arquivo VHD especializado</span><span class="sxs-lookup"><span data-stu-id="b9a71-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="b9a71-108">Criar uma VM de um disco do sistema operacional gerenciado existente que foi criado de um instantâneo</span><span class="sxs-lookup"><span data-stu-id="b9a71-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b9a71-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="b9a71-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b9a71-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="b9a71-110">Clean up deployment</span></span> 

<span data-ttu-id="b9a71-111">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9a71-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b9a71-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="b9a71-112">Script explanation</span></span>

<span data-ttu-id="b9a71-113">Esse script usa Olá comandos tooget gerenciado disco propriedades a seguir, anexar um disco gerenciado tooa nova VM e criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b9a71-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="b9a71-114">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="b9a71-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b9a71-115">Command</span><span class="sxs-lookup"><span data-stu-id="b9a71-115">Command</span></span> | <span data-ttu-id="b9a71-116">Observações</span><span class="sxs-lookup"><span data-stu-id="b9a71-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b9a71-117">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="b9a71-117">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="b9a71-118">Obtém o objeto de disco com base no nome hello e o grupo de recursos de saudação de um disco.</span><span class="sxs-lookup"><span data-stu-id="b9a71-118">Gets disk object based on hello name and hello resource group of a disk.</span></span> <span data-ttu-id="b9a71-119">Propriedade de ID de saudação retornado de objeto de disco é usado tooattach Olá disco tooa nova VM</span><span class="sxs-lookup"><span data-stu-id="b9a71-119">Id property of hello returned disk object is used tooattach hello disk tooa new VM</span></span> |
| [<span data-ttu-id="b9a71-120">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="b9a71-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="b9a71-121">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="b9a71-121">Creates a VM configuration.</span></span> <span data-ttu-id="b9a71-122">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="b9a71-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="b9a71-123">Olá configuração será usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="b9a71-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="b9a71-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="b9a71-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="b9a71-125">Anexa um disco gerenciado usando a propriedade de Id de saudação do disco hello como OS disco tooa nova máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b9a71-125">Attaches a managed disk using hello Id property of hello disk as OS disk tooa new virtual machine</span></span> |
| [<span data-ttu-id="b9a71-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="b9a71-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="b9a71-127">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="b9a71-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="b9a71-128">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="b9a71-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="b9a71-129">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="b9a71-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="b9a71-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="b9a71-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="b9a71-131">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b9a71-131">Create a virtual machine.</span></span> |
|[<span data-ttu-id="b9a71-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b9a71-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b9a71-133">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="b9a71-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b9a71-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b9a71-134">Next steps</span></span>

<span data-ttu-id="b9a71-135">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b9a71-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b9a71-136">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b9a71-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
