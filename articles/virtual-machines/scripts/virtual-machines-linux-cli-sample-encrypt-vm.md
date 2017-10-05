---
title: "Amostra de script da CLI do Azure – Criptografar uma VM Linux | Microsoft Docs"
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
ms.openlocfilehash: 9388bce04e37d049301521f808cd8494c327e335
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="13df8-103">Criptografar uma máquina virtual Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="13df8-103">Encrypt a Linux virtual machine in Azure</span></span>

<span data-ttu-id="13df8-104">Esse script cria um Azure Key Vault seguro, chaves de criptografia, uma entidade de serviço do Azure Active Directory e uma VM (máquina virtual) Linux.</span><span class="sxs-lookup"><span data-stu-id="13df8-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Linux virtual machine (VM).</span></span> <span data-ttu-id="13df8-105">A VM é então criptografada usando a chave de criptografia do Key Vault e as credenciais da entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="13df8-105">The VM is then encrypted using the encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="13df8-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="13df8-106">Sample script</span></span>

<span data-ttu-id="13df8-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Criptografar discos de VM")]</span><span class="sxs-lookup"><span data-stu-id="13df8-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="13df8-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="13df8-108">Clean up deployment</span></span> 

<span data-ttu-id="13df8-109">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="13df8-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="13df8-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="13df8-110">Script explanation</span></span>

<span data-ttu-id="13df8-111">Esse script usa os comandos a seguir para criar um grupo de recursos, um Azure Key Vault, uma entidade de serviço, uma máquina virtual e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="13df8-111">This script uses the following commands to create a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="13df8-112">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="13df8-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="13df8-113">Command</span><span class="sxs-lookup"><span data-stu-id="13df8-113">Command</span></span> | <span data-ttu-id="13df8-114">Observações</span><span class="sxs-lookup"><span data-stu-id="13df8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="13df8-115">az group create</span><span class="sxs-lookup"><span data-stu-id="13df8-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="13df8-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="13df8-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="13df8-117">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="13df8-117">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="13df8-118">Cria um Azure Key Vault para armazenar dados seguros, como chaves de criptografia.</span><span class="sxs-lookup"><span data-stu-id="13df8-118">Creates an Azure Key Vault to store secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="13df8-119">az keyvault key create</span><span class="sxs-lookup"><span data-stu-id="13df8-119">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="13df8-120">Cria uma chave de criptografia no Key Vault.</span><span class="sxs-lookup"><span data-stu-id="13df8-120">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="13df8-121">az ad sp create-for-rbac</span><span class="sxs-lookup"><span data-stu-id="13df8-121">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="13df8-122">Cria uma entidade de serviço do Azure Active Directory para autenticar com segurança e controlar o acesso às chaves de criptografia.</span><span class="sxs-lookup"><span data-stu-id="13df8-122">Creates an Azure Active Directory service principal to securely authenticate and control access to encryption keys.</span></span> |
| [<span data-ttu-id="13df8-123">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="13df8-123">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="13df8-124">Define as permissões no Key Vault para conceder à entidade de serviço o acesso às chaves de criptografia.</span><span class="sxs-lookup"><span data-stu-id="13df8-124">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> |
| [<span data-ttu-id="13df8-125">az vm create</span><span class="sxs-lookup"><span data-stu-id="13df8-125">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="13df8-126">Cria a máquina virtual e a conecta a placa de rede, a rede virtual, a sub-rede e o NSG.</span><span class="sxs-lookup"><span data-stu-id="13df8-126">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="13df8-127">Este comando também especifica a imagem de máquina virtual a ser usada e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="13df8-127">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="13df8-128">az vm encryption enable</span><span class="sxs-lookup"><span data-stu-id="13df8-128">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="13df8-129">Habilita a criptografia em uma VM usando as credenciais da entidade de serviço e a chave de criptografia.</span><span class="sxs-lookup"><span data-stu-id="13df8-129">Enables encryption on a VM using the service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="13df8-130">az vm encryption show</span><span class="sxs-lookup"><span data-stu-id="13df8-130">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="13df8-131">Mostra o status do processo de criptografia da VM.</span><span class="sxs-lookup"><span data-stu-id="13df8-131">Shows the status of the VM encryption process.</span></span> |
| [<span data-ttu-id="13df8-132">az group delete</span><span class="sxs-lookup"><span data-stu-id="13df8-132">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="13df8-133">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="13df8-133">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="13df8-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="13df8-134">Next steps</span></span>

<span data-ttu-id="13df8-135">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="13df8-135">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="13df8-136">Os exemplos de script da CLI de máquina virtual adicionais podem ser encontrados na [documentação da VM Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="13df8-136">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
