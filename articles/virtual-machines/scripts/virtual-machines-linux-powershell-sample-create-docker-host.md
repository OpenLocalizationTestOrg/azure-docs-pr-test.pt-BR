---
title: aaaAzure exemplo de Script do PowerShell - Docker | Microsoft Docs
description: "Amostra de Script do Azure PowerShell – Docker"
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
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 556093d3cfaecda352ff52cce96728fc0e723a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-host-with-powershell"></a><span data-ttu-id="bc66f-103">Criar um host do Docker com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc66f-103">Create a Docker host with PowerShell</span></span>

<span data-ttu-id="bc66f-104">Esse script cria uma máquina virtual com o Docker habilitado e inicia um contêiner que executa o NGINX.</span><span class="sxs-lookup"><span data-stu-id="bc66f-104">This script creates a virtual machine with Docker enabled and starts a container running NGINX.</span></span> <span data-ttu-id="bc66f-105">Depois de executar o script hello, você pode acessar o servidor de web NGINX Olá através de Olá FQDN do hello máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc66f-105">After running hello script, you can access hello NGINX web server through hello FQDN of hello Azure virtual machine.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="bc66f-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="bc66f-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-docker-host/create-docker-host.ps1 "Create Docker host")]

## <a name="clean-up-deployment"></a><span data-ttu-id="bc66f-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="bc66f-107">Clean up deployment</span></span> 

<span data-ttu-id="bc66f-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="bc66f-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="bc66f-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="bc66f-109">Script explanation</span></span>

<span data-ttu-id="bc66f-110">Esse script usa Olá implantação de saudação toocreate comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="bc66f-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="bc66f-111">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="bc66f-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="bc66f-112">Command</span><span class="sxs-lookup"><span data-stu-id="bc66f-112">Command</span></span> | <span data-ttu-id="bc66f-113">Observações</span><span class="sxs-lookup"><span data-stu-id="bc66f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bc66f-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bc66f-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="bc66f-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="bc66f-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bc66f-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="bc66f-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="bc66f-117">Cria uma configuração de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="bc66f-117">Creates a subnet configuration.</span></span> <span data-ttu-id="bc66f-118">Essa configuração é usada com o processo de criação de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="bc66f-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="bc66f-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="bc66f-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="bc66f-120">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="bc66f-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="bc66f-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="bc66f-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="bc66f-122">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="bc66f-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="bc66f-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="bc66f-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="bc66f-124">Cria uma configuração de regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="bc66f-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="bc66f-125">Essa configuração é usada toocreate uma regra NSG quando Olá NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="bc66f-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="bc66f-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="bc66f-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="bc66f-127">Cria um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="bc66f-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="bc66f-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="bc66f-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="bc66f-129">Obtém informações de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="bc66f-129">Gets subnet information.</span></span> <span data-ttu-id="bc66f-130">Essas informações são usadas ao criar um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="bc66f-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="bc66f-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="bc66f-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="bc66f-132">Cria um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="bc66f-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="bc66f-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="bc66f-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="bc66f-134">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="bc66f-134">Creates a VM configuration.</span></span> <span data-ttu-id="bc66f-135">Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="bc66f-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="bc66f-136">Olá configuração será usada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="bc66f-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="bc66f-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="bc66f-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="bc66f-138">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bc66f-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="bc66f-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="bc66f-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="bc66f-140">Adicione uma máquina virtual de toohello de extensão VM.</span><span class="sxs-lookup"><span data-stu-id="bc66f-140">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="bc66f-141">Neste exemplo, hello extensão Docker é usado tooconfigure Docker e executar um contêiner de Docker NGINX.</span><span class="sxs-lookup"><span data-stu-id="bc66f-141">In this sample, hello Docker extension is used tooconfigure Docker and run an NGINX Docker container.</span></span> |
|[<span data-ttu-id="bc66f-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bc66f-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="bc66f-143">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="bc66f-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bc66f-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bc66f-144">Next steps</span></span>

<span data-ttu-id="bc66f-145">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bc66f-145">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="bc66f-146">Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bc66f-146">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
