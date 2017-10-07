---
title: "aaaSet a chave de cofre para máquinas virtuais do Windows no Gerenciador de recursos do Azure | Microsoft Docs"
description: "Como tooset o Cofre de chaves para uso com uma máquina virtual do Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a>Configurar o Cofre de Chaves para máquinas virtuais no Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

Na pilha do Gerenciador de recursos do Azure, segredos/certificados são modelados como recursos que são fornecidos pelo provedor de recursos de saudação do Cofre de chaves. toolearn mais sobre o Cofre de chaves, consulte [o que é o Azure Key Vault?](../../key-vault/key-vault-whatis.md)

> [!NOTE]
> 1. Em ordem para o Cofre de chaves toobe usado com máquinas virtuais do Gerenciador de recursos do Azure, Olá **EnabledForDeployment** propriedade no cofre de chaves deve ser definida como tootrue. Você pode fazer isso em vários clientes.
> 2. necessidades de Cofre de chaves Olá toobe criado no hello mesma assinatura e local como Olá a máquina Virtual.
>
>

## <a name="use-powershell-tooset-up-key-vault"></a>Use o PowerShell tooset o Cofre de chaves
toocreate um cofre de chaves usando o PowerShell, consulte [Introdução ao Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).

Para novos cofres de chaves, você pode usar este cmdlet do PowerShell:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

Para cofres de chaves existentes, você pode usar este cmdlet do PowerShell:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a>Nós CLI tooset o Cofre de chaves
toocreate um cofre de chaves usando a interface de linha de comando da saudação (CLI), consulte [Gerenciar cofre de chaves usando a CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

Para CLI, você deve ter um cofre de chaves toocreate Olá antes de atribuir a política de implantação de saudação. Você pode fazer isso usando o comando a seguir de saudação:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>Usar modelos tooset o Cofre de chaves
Ao usar um modelo, você precisa Olá tooset `enabledForDeployment` propriedade muito`true` para Olá recurso de Cofre de chaves.

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
