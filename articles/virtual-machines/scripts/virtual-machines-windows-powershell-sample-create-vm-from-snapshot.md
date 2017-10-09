---
title: "aaaAzure exemplo de Script do PowerShell - criar uma máquina virtual de um instantâneo | Microsoft Docs"
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
ms.openlocfilehash: 89c65171b55bff0582c4a26df0b0f29f556845fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="2fd0c-103">Criar uma máquina virtual de um instantâneo com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd0c-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="2fd0c-104">Esse script cria uma máquina virtual de um instantâneo de um disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="2fd0c-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2fd0c-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="2fd0c-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2fd0c-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="2fd0c-106">Clean up deployment</span></span> 

<span data-ttu-id="2fd0c-107">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="2fd0c-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2fd0c-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="2fd0c-108">Script explanation</span></span>

<span data-ttu-id="2fd0c-109">Esse script usa Olá comandos tooget propriedades de instantâneo, crie um disco gerenciado de instantâneo e criar uma máquina virtual a seguir.</span><span class="sxs-lookup"><span data-stu-id="2fd0c-109">This script uses hello following commands tooget snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="2fd0c-110">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="2fd0c-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2fd0c-111">Command</span><span class="sxs-lookup"><span data-stu-id="2fd0c-111">Command</span></span> | <span data-ttu-id="2fd0c-112">Observações</span><span class="sxs-lookup"><span data-stu-id="2fd0c-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2fd0c-113">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="2fd0c-113">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="2fd0c-114">Obtém um instantâneo usando o nome do instantâneo.</span><span class="sxs-lookup"><span data-stu-id="2fd0c-114">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="2fd0c-115">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="2fd0c-115">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="2fd0c-116">Cria uma configuração de disco.</span><span class="sxs-lookup"><span data-stu-id="2fd0c-116">Creates a disk configuration.</span></span> <span data-ttu-id="2fd0c-117">Essa configuração é usada com o processo de criação de disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fd0c-117">This configuration is used with hello disk creation process.</span></span> |
| [<span data-ttu-id="2fd0c-118">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="2fd0c-118">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="2fd0c-119">Cria um disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="2fd0c-119">Creates a managed disk.</span></span> |
| [<span data-ttu-id="2fd0c-120">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="2fd0c-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="2fd0c-121">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="2fd0c-121">Creates a VM configuration.</span></span> <span data-ttu-id="2fd0c-122">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="2fd0c-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="2fd0c-123">Olá configuração será usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="2fd0c-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="2fd0c-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="2fd0c-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="2fd0c-125">Anexa um disco gerenciado hello como máquina virtual do sistema operacional em disco toohello</span><span class="sxs-lookup"><span data-stu-id="2fd0c-125">Attaches hello managed disk as OS disk toohello virtual machine</span></span> |
| [<span data-ttu-id="2fd0c-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="2fd0c-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="2fd0c-127">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="2fd0c-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="2fd0c-128">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="2fd0c-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="2fd0c-129">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="2fd0c-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="2fd0c-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="2fd0c-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="2fd0c-131">Cria uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2fd0c-131">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="2fd0c-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2fd0c-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="2fd0c-133">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="2fd0c-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2fd0c-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2fd0c-134">Next steps</span></span>

<span data-ttu-id="2fd0c-135">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2fd0c-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2fd0c-136">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2fd0c-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
