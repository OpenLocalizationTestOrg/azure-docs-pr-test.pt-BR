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
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a><span data-ttu-id="8ccac-103">Configurar o Cofre de chaves para as máquinas virtuais no Gerenciador de recursos do Azure com hello 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8ccac-103">Set up Key Vault for virtual machines in Azure Resource Manager with hello Azure CLI 1.0</span></span>
<span data-ttu-id="8ccac-104">Na pilha do Gerenciador de recursos do Azure hello, segredos/certificados são modelados como recursos que são fornecidos pelo provedor de recursos de saudação do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="8ccac-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="8ccac-105">toolearn mais sobre o Cofre de chaves do Azure, consulte [o que é o Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="8ccac-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="8ccac-106">Em ordem para o Cofre de chaves toobe usado com máquinas virtuais do Gerenciador de recursos do Azure, Olá *EnabledForDeployment* propriedade no cofre de chaves deve ser definida como tootrue.</span><span class="sxs-lookup"><span data-stu-id="8ccac-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="8ccac-107">Você pode fazer isso em vários clientes.</span><span class="sxs-lookup"><span data-stu-id="8ccac-107">You can do this in various clients.</span></span> <span data-ttu-id="8ccac-108">Este artigo mostra como tooset o Cofre de chaves para uso com as máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ccac-108">This article shows you how tooset up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="8ccac-109">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="8ccac-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="8ccac-110">Você pode concluir tarefa hello usando uma saudação seguir versões da CLI</span><span class="sxs-lookup"><span data-stu-id="8ccac-110">You can complete hello task using one of hello following CLI versions</span></span>

- <span data-ttu-id="8ccac-111">[1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="8ccac-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="8ccac-112">[2.0 do CLI do Azure](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="8ccac-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="use-cli-10-tooset-up-key-vault"></a><span data-ttu-id="8ccac-113">Usar CLI 1.0 tooset o Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="8ccac-113">Use CLI 1.0 tooset up Key Vault</span></span>
<span data-ttu-id="8ccac-114">toocreate um cofre de chaves usando a interface de linha de comando da saudação (CLI), consulte [Gerenciar cofre de chaves usando a CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="8ccac-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="8ccac-115">CLI 1.0, você deve ter um cofre de chaves toocreate Olá antes de atribuir a política de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ccac-115">For CLI 1.0, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="8ccac-116">Você pode atribuir política hello usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ccac-116">You can then assign hello policy by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="8ccac-117">Usar modelos tooset o Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="8ccac-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="8ccac-118">Quando você usa um modelo, você precisa Olá tooset `enabledForDeployment` propriedade muito`true` para Olá recurso de Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="8ccac-118">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="8ccac-119">Para saber outras opções que você pode configurar ao criar um cofre de chaves usando modelos, consulte [Criar um cofre de chave](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="8ccac-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
