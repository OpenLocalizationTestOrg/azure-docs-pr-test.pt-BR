---
title: Implantar o modelo do Azure com o token SAS e a CLI do Azure | Microsoft Docs
description: "Use o Azure Resource Manager e a CLI do Azure para implantar recursos para o Azure de um modelo que é protegido com o token SAS."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 22387aadd8f53a65efb76a29a9403c46a2c25954
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a><span data-ttu-id="f8f1d-103">Implantar o modelo particular do Resource Manager com a CLI do Azure e o token SAS</span><span class="sxs-lookup"><span data-stu-id="f8f1d-103">Deploy private Resource Manager template with SAS token and Azure CLI</span></span>

<span data-ttu-id="f8f1d-104">Quando seu modelo reside em uma conta de armazenamento, você pode restringir o acesso a ele e fornecer um token de SAS (Assinatura de Acesso Compartilhado) durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="f8f1d-105">Este tópico explica como usar o Azure PowerShell com modelos do Resource Manager para fornecer um token SAS durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span></span> 

## <a name="add-private-template-to-storage-account"></a><span data-ttu-id="f8f1d-106">Adicionar modelo privado à conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f8f1d-106">Add private template to storage account</span></span>

<span data-ttu-id="f8f1d-107">Você pode adicionar seus modelos a uma conta de armazenamento e vinculá-los durante a implantação com um token SAS.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8f1d-108">Seguindo as etapas abaixo, o blob que contém o modelo fica acessível somente para o proprietário da conta.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span></span> <span data-ttu-id="f8f1d-109">No entanto, quando você cria um token SAS para o blob, o blob fica acessível para qualquer pessoa com o URI.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span></span> <span data-ttu-id="f8f1d-110">Se outro usuário interceptar o URI, esse usuário será capaz de acessar o modelo.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-110">If another user intercepts the URI, that user is able to access the template.</span></span> <span data-ttu-id="f8f1d-111">Usar um token SAS é uma boa maneira de limitar o acesso aos seus modelos, mas você não deve incluir dados confidenciais como senhas diretamente no modelo.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span></span>
> 
> 

<span data-ttu-id="f8f1d-112">O seguinte exemplo configura um contêiner de conta de armazenamento privado e carrega um modelo:</span><span class="sxs-lookup"><span data-stu-id="f8f1d-112">The following example sets up a private storage account container and uploads a template:</span></span>
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="f8f1d-113">Forneça um token SAS durante a implantação</span><span class="sxs-lookup"><span data-stu-id="f8f1d-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="f8f1d-114">Para implantar um modelo privado em uma conta de armazenamento, gere um token SAS e inclua-o no URI para o modelo.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="f8f1d-115">Defina a hora de vencimento de forma a permitir que haja tempo suficiente para concluir a implantação.</span><span class="sxs-lookup"><span data-stu-id="f8f1d-115">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

<span data-ttu-id="f8f1d-116">Para ver um exemplo de como usar um token SAS com modelos vinculados, consulte [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f8f1d-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8f1d-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f8f1d-117">Next steps</span></span>
* <span data-ttu-id="f8f1d-118">Para obter uma introdução à implantação de modelos, veja [Implantar recursos com modelos do Resource Manager e o Azure PowerShell](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f8f1d-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="f8f1d-119">Para um script de exemplo completo que implanta um modelo, veja [Implantar o script de modelo do Resource Manager](resource-manager-samples-cli-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="f8f1d-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md)</span></span>
* <span data-ttu-id="f8f1d-120">Para definir os parâmetros no modelo, consulte [Criando modelos](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="f8f1d-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="f8f1d-121">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="f8f1d-121">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
