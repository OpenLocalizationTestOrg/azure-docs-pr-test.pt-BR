---
title: aaaSet o Cofre de chaves para VMs do Linux com hello 1.0 da CLI do Azure | Microsoft Docs
description: "Como tooset o Cofre de chaves para uso com uma máquina virtual de Gerenciador de recursos do Azure com hello 1.0 da CLI do Azure."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 275022e4e7e26d7363784c289dd7512047c07bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a>Configurar o Cofre de chaves para as máquinas virtuais no Gerenciador de recursos do Azure com hello 1.0 da CLI do Azure
Na pilha do Gerenciador de recursos do Azure hello, segredos/certificados são modelados como recursos que são fornecidos pelo provedor de recursos de saudação do Cofre de chaves. toolearn mais sobre o Cofre de chaves do Azure, consulte [o que é o Azure Key Vault?](../../key-vault/key-vault-whatis.md) Em ordem para o Cofre de chaves toobe usado com máquinas virtuais do Gerenciador de recursos do Azure, Olá *EnabledForDeployment* propriedade no cofre de chaves deve ser definida como tootrue. Você pode fazer isso em vários clientes. Este artigo mostra como tooset o Cofre de chaves para uso com as máquinas virtuais do Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir tarefa hello usando uma saudação seguir versões da CLI

- [1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação

## <a name="use-cli-10-tooset-up-key-vault"></a>Usar CLI 1.0 tooset o Cofre de chaves
toocreate um cofre de chaves usando a interface de linha de comando da saudação (CLI), consulte [Gerenciar cofre de chaves usando a CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

CLI 1.0, você deve ter um cofre de chaves toocreate Olá antes de atribuir a política de implantação de saudação. Você pode atribuir política hello usando Olá comando a seguir:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>Usar modelos tooset o Cofre de chaves
Quando você usa um modelo, você precisa Olá tooset `enabledForDeployment` propriedade muito`true` para Olá recurso de Cofre de chaves.

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

Para saber outras opções que você pode configurar ao criar um cofre de chaves usando modelos, consulte [Criar um cofre de chave](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).
