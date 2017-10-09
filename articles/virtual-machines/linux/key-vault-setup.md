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
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a>Como tooset o Cofre de chaves para máquinas virtuais com hello 2.0 do CLI do Azure

Na pilha do Gerenciador de recursos do Azure hello, segredos/certificados são modelados como recursos que são fornecidos pelo Cofre de chaves. toolearn mais sobre o Cofre de chaves do Azure, consulte [o que é o Azure Key Vault?](../../key-vault/key-vault-whatis.md) Em ordem para o Cofre de chaves toobe usado com máquinas virtuais do Gerenciador de recursos do Azure, Olá *EnabledForDeployment* propriedade no cofre de chaves deve ser definida como tootrue. Este artigo mostra como tooset o Cofre de chaves para uso com máquinas virtuais do Azure (VMs) usando Olá 2.0 do CLI do Azure. Você também pode executar essas etapas com hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

tooperform essas etapas, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).

## <a name="create-a-key-vault"></a>Criar um cofre de chaves
Criar um cofre de chaves e atribuir a política de implantação de saudação com [keyvault az criar](/cli/azure/keyvault#create). Olá, exemplo a seguir cria um cofre de chaves chamado `myKeyVault` em Olá `myResourceGroup` grupo de recursos:

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a>Atualizar um Key Vault para uso com VMs
Definir a diretiva de implantação de saudação em um cofre de chave existente com [atualização de keyvault az](/cli/azure/keyvault#update). as seguintes atualizações Olá Olá Cofre de chaves chamado `myKeyVault` em Olá `myResourceGroup` grupo de recursos:

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a>Usar modelos tooset o Cofre de chaves
Quando você usa um modelo, você precisa Olá tooset `enabledForDeployment` propriedade muito`true` para o recurso de Cofre de chaves de saudação da seguinte maneira:

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

## <a name="next-steps"></a>Próximas etapas
Para obter outras opções que você pode definir ao criar um Key Vault usando modelos, consulte [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/) (Criar um Key Vault).
