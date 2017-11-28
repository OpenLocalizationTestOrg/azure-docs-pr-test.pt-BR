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
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="f1148-103">Configurar o Cofre de Chaves para máquinas virtuais no Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f1148-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="f1148-104">Na pilha do Gerenciador de recursos do Azure, segredos/certificados são modelados como recursos que são fornecidos pelo provedor de recursos de saudação do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="f1148-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="f1148-105">toolearn mais sobre o Cofre de chaves, consulte [o que é o Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="f1148-105">toolearn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="f1148-106">Em ordem para o Cofre de chaves toobe usado com máquinas virtuais do Gerenciador de recursos do Azure, Olá **EnabledForDeployment** propriedade no cofre de chaves deve ser definida como tootrue.</span><span class="sxs-lookup"><span data-stu-id="f1148-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello **EnabledForDeployment** property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="f1148-107">Você pode fazer isso em vários clientes.</span><span class="sxs-lookup"><span data-stu-id="f1148-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="f1148-108">necessidades de Cofre de chaves Olá toobe criado no hello mesma assinatura e local como Olá a máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="f1148-108">hello Key Vault needs toobe created in hello same subscription and location as hello Virtual Machine.</span></span>
>
>

## <a name="use-powershell-tooset-up-key-vault"></a><span data-ttu-id="f1148-109">Use o PowerShell tooset o Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="f1148-109">Use PowerShell tooset up Key Vault</span></span>
<span data-ttu-id="f1148-110">toocreate um cofre de chaves usando o PowerShell, consulte [Introdução ao Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span><span class="sxs-lookup"><span data-stu-id="f1148-110">toocreate a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="f1148-111">Para novos cofres de chaves, você pode usar este cmdlet do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f1148-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="f1148-112">Para cofres de chaves existentes, você pode usar este cmdlet do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f1148-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a><span data-ttu-id="f1148-113">Nós CLI tooset o Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="f1148-113">Us CLI tooset up Key Vault</span></span>
<span data-ttu-id="f1148-114">toocreate um cofre de chaves usando a interface de linha de comando da saudação (CLI), consulte [Gerenciar cofre de chaves usando a CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="f1148-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="f1148-115">Para CLI, você deve ter um cofre de chaves toocreate Olá antes de atribuir a política de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1148-115">For CLI, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="f1148-116">Você pode fazer isso usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f1148-116">You can do this by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="f1148-117">Usar modelos tooset o Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="f1148-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="f1148-118">Ao usar um modelo, você precisa Olá tooset `enabledForDeployment` propriedade muito`true` para Olá recurso de Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="f1148-118">While you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="f1148-119">Para saber outras opções que você pode configurar ao criar um cofre de chaves usando modelos, consulte [Criar um cofre de chave](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="f1148-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
