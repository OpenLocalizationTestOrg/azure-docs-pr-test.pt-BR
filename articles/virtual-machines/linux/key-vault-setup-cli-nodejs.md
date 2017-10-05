---
title: Configurar o Key Vault para VMs do Linux com o CLI do Azure 1.0 | Microsoft Docs
description: "Como configurar o Key Vault para uso com uma máquina virtual do Azure Resource Manager com a CLI do Azure 1.0."
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
ms.openlocfilehash: fed612a354d45f34619f2a66bd40d78740c43ac7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-the-azure-cli-10"></a><span data-ttu-id="7393e-103">Configurar o Key Vault para máquinas virtuais no Azure Resource Manager com a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="7393e-103">Set up Key Vault for virtual machines in Azure Resource Manager with the Azure CLI 1.0</span></span>
<span data-ttu-id="7393e-104">Na pilha do Azure Resource Manager, os certificados/segredos são modelados como recursos que são fornecidos pelo provedor de recursos do Key Vault.</span><span class="sxs-lookup"><span data-stu-id="7393e-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="7393e-105">Para saber mais sobre o Cofre de Chaves do Azure, consulte [O que é o Cofre de Chaves do Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="7393e-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="7393e-106">Para que um Cofre de Chaves seja usado com máquinas virtuais do Azure Resource Manager, a propriedade *EnabledForDeployment* no Cofre de Chaves deverá ser definida como true.</span><span class="sxs-lookup"><span data-stu-id="7393e-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the *EnabledForDeployment* property on Key Vault must be set to true.</span></span> <span data-ttu-id="7393e-107">Você pode fazer isso em vários clientes.</span><span class="sxs-lookup"><span data-stu-id="7393e-107">You can do this in various clients.</span></span> <span data-ttu-id="7393e-108">Este artigo mostra como configurar o Key Vault para uso com as máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="7393e-108">This article shows you how to set up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="7393e-109">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="7393e-109">CLI versions to complete the task</span></span>
<span data-ttu-id="7393e-110">Você pode concluir a tarefa usando uma das seguintes versões da CLI</span><span class="sxs-lookup"><span data-stu-id="7393e-110">You can complete the task using one of the following CLI versions</span></span>

- <span data-ttu-id="7393e-111">[CLI 1.0 do Azure](#quick-commands) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos (este artigo)</span><span class="sxs-lookup"><span data-stu-id="7393e-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="7393e-112">[CLI do Azure 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – nossa próxima geração de CLI para o modelo de implantação do resource manager</span><span class="sxs-lookup"><span data-stu-id="7393e-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="use-cli-10-to-set-up-key-vault"></a><span data-ttu-id="7393e-113">Usar a CLI 1.0 para configurar o Key Vault</span><span class="sxs-lookup"><span data-stu-id="7393e-113">Use CLI 1.0 to set up Key Vault</span></span>
<span data-ttu-id="7393e-114">Para criar um cofre de chaves usando a CLI (interface de linha de comando), consulte [Gerenciar Cofre da Chave usando a CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="7393e-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="7393e-115">Para a CLI 1.0, você precisa criar o Key Vault antes de atribuir a política de implantação.</span><span class="sxs-lookup"><span data-stu-id="7393e-115">For CLI 1.0, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="7393e-116">Você pode atribuir a diretiva usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7393e-116">You can then assign the policy by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="7393e-117">Usar modelos para configurar o Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="7393e-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="7393e-118">Ao usar um modelo, você precisa definir a propriedade `enabledForDeployment` como `true` para o recurso de Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="7393e-118">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

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

<span data-ttu-id="7393e-119">Para saber outras opções que você pode configurar ao criar um cofre de chaves usando modelos, consulte [Criar um cofre de chave](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="7393e-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
