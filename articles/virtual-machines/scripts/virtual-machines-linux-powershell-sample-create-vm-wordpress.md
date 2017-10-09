---
title: aaaAzure exemplo de Script do PowerShell - WordPress | Microsoft Docs
description: "Amostra de Script do Azure PowerShell – WordPress"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b011726a772bb4d13fcfcba088eac4d0305967c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-vm-with-powershell"></a><span data-ttu-id="61ce8-103">Criar uma VM do WordPress com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="61ce8-103">Create a WordPress VM with PowerShell</span></span>

<span data-ttu-id="61ce8-104">Esse script cria uma máquina virtual e usa Olá Máquina Virtual do Azure script personalizado extensão tooinstall WordPress.</span><span class="sxs-lookup"><span data-stu-id="61ce8-104">This script creates a virtual machine and uses hello Azure Virtual Machine custom script extension tooinstall WordPress.</span></span> <span data-ttu-id="61ce8-105">Após script hello em execução, você pode acessar o site de configuração do WordPress Olá em `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="61ce8-105">After running hello script, you can access hello WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="61ce8-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="61ce8-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "Create VM WordPress")]

## <a name="clean-up-deployment"></a><span data-ttu-id="61ce8-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="61ce8-107">Clean up deployment</span></span> 

<span data-ttu-id="61ce8-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="61ce8-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="61ce8-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="61ce8-109">Script explanation</span></span>

<span data-ttu-id="61ce8-110">Esse script usa Olá implantação de saudação toocreate comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="61ce8-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="61ce8-111">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="61ce8-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="61ce8-112">Command</span><span class="sxs-lookup"><span data-stu-id="61ce8-112">Command</span></span> | <span data-ttu-id="61ce8-113">Observações</span><span class="sxs-lookup"><span data-stu-id="61ce8-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="61ce8-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="61ce8-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="61ce8-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="61ce8-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="61ce8-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="61ce8-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="61ce8-117">Cria uma configuração de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="61ce8-117">Creates a subnet configuration.</span></span> <span data-ttu-id="61ce8-118">Essa configuração é usada com o processo de criação de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="61ce8-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="61ce8-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="61ce8-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="61ce8-120">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="61ce8-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="61ce8-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="61ce8-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="61ce8-122">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="61ce8-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="61ce8-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="61ce8-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="61ce8-124">Cria uma configuração de regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="61ce8-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="61ce8-125">Essa configuração é usada toocreate uma regra NSG quando Olá NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="61ce8-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="61ce8-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="61ce8-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="61ce8-127">Cria um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="61ce8-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="61ce8-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="61ce8-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="61ce8-129">Obtém informações de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="61ce8-129">Gets subnet information.</span></span> <span data-ttu-id="61ce8-130">Essas informações são usadas ao criar um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="61ce8-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="61ce8-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="61ce8-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="61ce8-132">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="61ce8-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="61ce8-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="61ce8-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="61ce8-134">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="61ce8-134">Creates a VM configuration.</span></span> <span data-ttu-id="61ce8-135">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="61ce8-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="61ce8-136">Olá configuração será usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="61ce8-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="61ce8-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="61ce8-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="61ce8-138">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="61ce8-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="61ce8-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="61ce8-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="61ce8-140">Adicione a máquina virtual do hello extensão de Script personalizado toohello, que chama um script tooinstall WordPress.</span><span class="sxs-lookup"><span data-stu-id="61ce8-140">Add hello Custom Script Extension toohello virtual machine, which invokes a script tooinstall WordPress.</span></span> |
|[<span data-ttu-id="61ce8-141">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="61ce8-141">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="61ce8-142">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="61ce8-142">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="61ce8-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="61ce8-143">Next steps</span></span>

<span data-ttu-id="61ce8-144">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="61ce8-144">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="61ce8-145">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="61ce8-145">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
