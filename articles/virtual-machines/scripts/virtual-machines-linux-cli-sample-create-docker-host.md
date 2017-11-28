---
title: aaaAzure exemplo de Script CLI - criar um host Docker | Microsoft Docs
description: Exemplo de script da CLI do Azure - Criar um host de Docker
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7df2561c428ff5d3ab0a0d53c8e046781996be77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="d34b5-103">Criar uma máquina virtual com o Docker</span><span class="sxs-lookup"><span data-stu-id="d34b5-103">Create a VM with Docker</span></span>

<span data-ttu-id="d34b5-104">Esse script cria uma máquina virtual com o Docker habilitado e inicia um contêiner do Docker que executa o NGINX.</span><span class="sxs-lookup"><span data-stu-id="d34b5-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="d34b5-105">Depois de executar o script hello, você pode acessar o servidor de web NGINX Olá através de Olá FQDN do hello máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="d34b5-105">After running hello script, you can access hello NGINX web server through hello FQDN of hello Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d34b5-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="d34b5-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d34b5-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="d34b5-107">Clean up deployment</span></span> 

<span data-ttu-id="d34b5-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="d34b5-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d34b5-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="d34b5-109">Script explanation</span></span>

<span data-ttu-id="d34b5-110">Esse script usa Olá implantação de saudação toocreate comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="d34b5-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="d34b5-111">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="d34b5-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d34b5-112">Command</span><span class="sxs-lookup"><span data-stu-id="d34b5-112">Command</span></span> | <span data-ttu-id="d34b5-113">Observações</span><span class="sxs-lookup"><span data-stu-id="d34b5-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d34b5-114">az group create</span><span class="sxs-lookup"><span data-stu-id="d34b5-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d34b5-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="d34b5-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d34b5-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="d34b5-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="d34b5-117">Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="d34b5-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="d34b5-118">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="d34b5-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="d34b5-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="d34b5-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="d34b5-120">Cria um tooallow de regra de grupo de segurança de rede o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="d34b5-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="d34b5-121">Neste exemplo, a porta 80 está aberta para tráfego HTTP.</span><span class="sxs-lookup"><span data-stu-id="d34b5-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="d34b5-122">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="d34b5-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d34b5-123">Adiciona e executa uma extensão de máquina virtual tooa VM.</span><span class="sxs-lookup"><span data-stu-id="d34b5-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="d34b5-124">Neste exemplo, Olá extensão da VM Docker é tooconfigure usado um host Docker.</span><span class="sxs-lookup"><span data-stu-id="d34b5-124">In this sample, hello Docker VM extension is used tooconfigure a Docker host.</span></span>|
| [<span data-ttu-id="d34b5-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="d34b5-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d34b5-126">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="d34b5-126">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d34b5-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d34b5-127">Next steps</span></span>

<span data-ttu-id="d34b5-128">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d34b5-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d34b5-129">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d34b5-129">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
