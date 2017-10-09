---
title: aaaSet o Cofre de chaves do Azure para VMs do Linux | Microsoft Docs
description: "Como tooset o Cofre de chaves para uso com uma máquina virtual de Gerenciador de recursos do Azure com hello 2.0 do CLI."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a><span data-ttu-id="b92bb-103">Como tooset o Cofre de chaves para máquinas virtuais com hello 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b92bb-103">How tooset up Key Vault for virtual machines with hello Azure CLI 2.0</span></span>

<span data-ttu-id="b92bb-104">Na pilha do Gerenciador de recursos do Azure hello, segredos/certificados são modelados como recursos que são fornecidos pelo Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="b92bb-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="b92bb-105">toolearn mais sobre o Cofre de chaves do Azure, consulte [o que é o Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="b92bb-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="b92bb-106">Em ordem para o Cofre de chaves toobe usado com máquinas virtuais do Gerenciador de recursos do Azure, Olá *EnabledForDeployment* propriedade no cofre de chaves deve ser definida como tootrue.</span><span class="sxs-lookup"><span data-stu-id="b92bb-106">In order for Key Vault toobe used with Azure Resource Manager VMs, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="b92bb-107">Este artigo mostra como tooset o Cofre de chaves para uso com máquinas virtuais do Azure (VMs) usando Olá 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="b92bb-107">This article shows you how tooset up Key Vault for use with Azure virtual machines (VMs) using hello Azure CLI 2.0.</span></span> <span data-ttu-id="b92bb-108">Você também pode executar essas etapas com hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b92bb-108">You can also perform these steps with hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b92bb-109">tooperform essas etapas, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b92bb-109">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="b92bb-110">Criar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="b92bb-110">Create a Key Vault</span></span>
<span data-ttu-id="b92bb-111">Criar um cofre de chaves e atribuir a política de implantação de saudação com [keyvault az criar](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="b92bb-111">Create a key vault and assign hello deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="b92bb-112">Olá, exemplo a seguir cria um cofre de chaves chamado `myKeyVault` em Olá `myResourceGroup` grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="b92bb-112">hello following example creates a key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="b92bb-113">Atualizar um Key Vault para uso com VMs</span><span class="sxs-lookup"><span data-stu-id="b92bb-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="b92bb-114">Definir a diretiva de implantação de saudação em um cofre de chave existente com [atualização de keyvault az](/cli/azure/keyvault#update).</span><span class="sxs-lookup"><span data-stu-id="b92bb-114">Set hello deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="b92bb-115">as seguintes atualizações Olá Olá Cofre de chaves chamado `myKeyVault` em Olá `myResourceGroup` grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="b92bb-115">hello following updates hello key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="b92bb-116">Usar modelos tooset o Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="b92bb-116">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="b92bb-117">Quando você usa um modelo, você precisa Olá tooset `enabledForDeployment` propriedade muito`true` para o recurso de Cofre de chaves de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b92bb-117">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource as follows:</span></span>

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="b92bb-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b92bb-118">Next steps</span></span>
<span data-ttu-id="b92bb-119">Para obter outras opções que você pode definir ao criar um Key Vault usando modelos, consulte [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/) (Criar um Key Vault).</span><span class="sxs-lookup"><span data-stu-id="b92bb-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
