---
title: aaaAzure exemplo de Script CLI - criptografar uma VM do Linux | Microsoft Docs
description: "Amostra de script da CLI do Azure – Criptografar uma VM Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 1e455da4a8ea6d75b6d0d74b338d2e4d84973413
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="53c0a-103">Criptografar uma máquina virtual Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="53c0a-103">Encrypt a Linux virtual machine in Azure</span></span>

<span data-ttu-id="53c0a-104">Esse script cria um Azure Key Vault seguro, chaves de criptografia, uma entidade de serviço do Azure Active Directory e uma VM (máquina virtual) Linux.</span><span class="sxs-lookup"><span data-stu-id="53c0a-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Linux virtual machine (VM).</span></span> <span data-ttu-id="53c0a-105">Olá VM é criptografada usando a chave de criptografia de saudação do Cofre de chaves e credenciais de serviço principal.</span><span class="sxs-lookup"><span data-stu-id="53c0a-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="53c0a-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="53c0a-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="53c0a-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="53c0a-107">Clean up deployment</span></span> 

<span data-ttu-id="53c0a-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="53c0a-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="53c0a-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="53c0a-109">Script explanation</span></span>

<span data-ttu-id="53c0a-110">Esse script usa Olá toocreate comandos a seguir uma recurso grupo, o Cofre de chaves do Azure, serviço principal, máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="53c0a-110">This script uses hello following commands toocreate a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="53c0a-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="53c0a-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="53c0a-112">Command</span><span class="sxs-lookup"><span data-stu-id="53c0a-112">Command</span></span> | <span data-ttu-id="53c0a-113">Observações</span><span class="sxs-lookup"><span data-stu-id="53c0a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="53c0a-114">az group create</span><span class="sxs-lookup"><span data-stu-id="53c0a-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="53c0a-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="53c0a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="53c0a-116">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="53c0a-116">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="53c0a-117">Cria um cofre de chaves do Azure toostore proteger os dados, como chaves de criptografia.</span><span class="sxs-lookup"><span data-stu-id="53c0a-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="53c0a-118">az keyvault key create</span><span class="sxs-lookup"><span data-stu-id="53c0a-118">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="53c0a-119">Cria uma chave de criptografia no Key Vault.</span><span class="sxs-lookup"><span data-stu-id="53c0a-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="53c0a-120">az ad sp create-for-rbac</span><span class="sxs-lookup"><span data-stu-id="53c0a-120">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="53c0a-121">Cria um serviço do Active Directory do Azure toosecurely principal autenticar e controlar o acesso tooencryption chaves.</span><span class="sxs-lookup"><span data-stu-id="53c0a-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="53c0a-122">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="53c0a-122">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="53c0a-123">Define permissões na Olá Cofre de chaves toogrant chaves de tooencryption Olá serviço principal de acesso.</span><span class="sxs-lookup"><span data-stu-id="53c0a-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="53c0a-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="53c0a-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="53c0a-125">Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="53c0a-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="53c0a-126">Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="53c0a-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="53c0a-127">az vm encryption enable</span><span class="sxs-lookup"><span data-stu-id="53c0a-127">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="53c0a-128">Habilita a criptografia em uma VM usando credenciais do serviço principal do hello e chave de criptografia.</span><span class="sxs-lookup"><span data-stu-id="53c0a-128">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="53c0a-129">az vm encryption show</span><span class="sxs-lookup"><span data-stu-id="53c0a-129">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="53c0a-130">Mostra o status de saudação do hello processo de criptografia de VM.</span><span class="sxs-lookup"><span data-stu-id="53c0a-130">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="53c0a-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="53c0a-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="53c0a-132">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="53c0a-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="53c0a-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="53c0a-133">Next steps</span></span>

<span data-ttu-id="53c0a-134">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="53c0a-134">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="53c0a-135">Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="53c0a-135">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
