---
title: "aaaAzure exemplo de Script CLI - implantar Olá pilha LAMP em um conjunto de escala de Load-Balanced monitoramente Machin | Microsoft Docs"
description: "Use uma saudação de toodeploy de extensão do script personalizado pilha LAMP em uma carga = escala de VM com balanceamento definido no Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="7e3aa-103">Implantar a pilha de LÂMPADA Olá em um conjunto de escala de VM com balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="7e3aa-103">Deploy hello LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="7e3aa-104">Este exemplo cria um conjunto de escala de máquinas virtuais e aplica uma extensão que executa uma pilha de LÂMPADA do script personalizado toodeploy Olá em cada máquina virtual no conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-104">This example creates a virtual machine scale set and applies an extension that runs a custom script toodeploy hello LAMP stack on each virtual machine in hello scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="7e3aa-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="7e3aa-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a><span data-ttu-id="7e3aa-106">Connect</span><span class="sxs-lookup"><span data-stu-id="7e3aa-106">Connect</span></span>

<span data-ttu-id="7e3aa-107">Use este toosee código como tooconnect tooyour VMs e a escala definidas.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-107">Use this code toosee how tooconnect tooyour VMs and your scale set.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7e3aa-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="7e3aa-108">Clean up deployment</span></span> 

<span data-ttu-id="7e3aa-109">Execute Olá grupo de recursos do comando tooremove hello, conjunto de escala hello e VMs e todos os recursos relacionados a seguir.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-109">Run hello following command tooremove hello resource group, hello scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="7e3aa-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="7e3aa-110">Script explanation</span></span>

<span data-ttu-id="7e3aa-111">Esse script usa Olá comandos toocreate um grupo de recursos, máquina virtual, o conjunto de disponibilidade, balanceador de carga e todos os recursos relacionados a seguir.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-111">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="7e3aa-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7e3aa-113">Command</span><span class="sxs-lookup"><span data-stu-id="7e3aa-113">Command</span></span> | <span data-ttu-id="7e3aa-114">Observações</span><span class="sxs-lookup"><span data-stu-id="7e3aa-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7e3aa-115">az group create</span><span class="sxs-lookup"><span data-stu-id="7e3aa-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7e3aa-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7e3aa-117">az vmss create</span><span class="sxs-lookup"><span data-stu-id="7e3aa-117">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="7e3aa-118">Criar um conjunto de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="7e3aa-118">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="7e3aa-119">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="7e3aa-119">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="7e3aa-120">Adicionar um ponto de extremidade com balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="7e3aa-120">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="7e3aa-121">az vmss extension set</span><span class="sxs-lookup"><span data-stu-id="7e3aa-121">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="7e3aa-122">Criar extensão Olá que executa o script personalizado Olá na implantação de uma VM</span><span class="sxs-lookup"><span data-stu-id="7e3aa-122">Create hello extension that runs hello custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="7e3aa-123">az vmss update-instances</span><span class="sxs-lookup"><span data-stu-id="7e3aa-123">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="7e3aa-124">Executar script personalizado Olá em instâncias de VM Olá que foram implantadas antes da aplicação extensão Olá toohello conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-124">Run hello custom script on hello VM instances that were deployed before hello extension was applied toohello scale set.</span></span> |
| [<span data-ttu-id="7e3aa-125">az vmss scale</span><span class="sxs-lookup"><span data-stu-id="7e3aa-125">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="7e3aa-126">Escala verticalmente escala Olá definir, adicionando mais instâncias VM.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-126">Scale up hello scale set by adding more VM instances.</span></span> <span data-ttu-id="7e3aa-127">script personalizado Olá é executado sobre estas configurações quando eles são implantados.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-127">hello custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="7e3aa-128">az network public-ip list</span><span class="sxs-lookup"><span data-stu-id="7e3aa-128">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="7e3aa-129">Obter endereços IP de saudação do hello VMs criadas pelo exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-129">Get hello IP addresses of hello VMs created by hello sample.</span></span> |
| [<span data-ttu-id="7e3aa-130">az network lb show</span><span class="sxs-lookup"><span data-stu-id="7e3aa-130">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="7e3aa-131">Obtenha o back-end e front-end Olá portas usadas pelo Balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-131">Get hello frontend and backend ports used by hello load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7e3aa-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7e3aa-132">Next steps</span></span>

<span data-ttu-id="7e3aa-133">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7e3aa-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7e3aa-134">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7e3aa-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
