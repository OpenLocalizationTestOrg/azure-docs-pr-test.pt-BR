---
title: aaaDeploy modelo do Azure com o token SAS e a CLI do Azure | Microsoft Docs
description: "Use o Gerenciador de recursos do Azure e a CLI do Azure toodeploy tooAzure de recursos de um modelo que está protegido com token SAS."
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
ms.openlocfilehash: 59c64616d6e1f5e456d88a72854d0ed99e1bdc0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a><span data-ttu-id="85b76-103">Implantar o modelo particular do Resource Manager com a CLI do Azure e o token SAS</span><span class="sxs-lookup"><span data-stu-id="85b76-103">Deploy private Resource Manager template with SAS token and Azure CLI</span></span>

<span data-ttu-id="85b76-104">Quando o modelo estiver em uma conta de armazenamento, você pode restringir o modelo de toohello de acesso e fornecer um token de assinatura (SAS) de acesso compartilhado durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="85b76-104">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="85b76-105">Este tópico explica como toouse PowerShell do Azure com o Gerenciador de recursos modelos tooprovide um token SAS durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="85b76-105">This topic explains how toouse Azure PowerShell with Resource Manager templates tooprovide a SAS token during deployment.</span></span> 

## <a name="add-private-template-toostorage-account"></a><span data-ttu-id="85b76-106">Adicionar modelo particular toostorage conta</span><span class="sxs-lookup"><span data-stu-id="85b76-106">Add private template toostorage account</span></span>

<span data-ttu-id="85b76-107">Você pode adicionar sua conta de armazenamento tooa modelos e vincular toothem durante a implantação com um token SAS.</span><span class="sxs-lookup"><span data-stu-id="85b76-107">You can add your templates tooa storage account and link toothem during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85b76-108">Seguindo as etapas de saudação abaixo, o blob de saudação que contém o modelo de saudação é proprietário da conta Olá tooonly acessível.</span><span class="sxs-lookup"><span data-stu-id="85b76-108">By following hello steps below, hello blob containing hello template is accessible tooonly hello account owner.</span></span> <span data-ttu-id="85b76-109">No entanto, quando você cria um token SAS para blob hello, blob Olá é tooanyone acessível com esse URI.</span><span class="sxs-lookup"><span data-stu-id="85b76-109">However, when you create a SAS token for hello blob, hello blob is accessible tooanyone with that URI.</span></span> <span data-ttu-id="85b76-110">Se outro usuário interceptar Olá URI, esse usuário será capaz de tooaccess modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="85b76-110">If another user intercepts hello URI, that user is able tooaccess hello template.</span></span> <span data-ttu-id="85b76-111">Usar um token SAS é uma boa maneira de limitar o acesso tooyour modelos, mas você não deve incluir dados confidenciais, como senhas diretamente no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="85b76-111">Using a SAS token is a good way of limiting access tooyour templates, but you should not include sensitive data like passwords directly in hello template.</span></span>
> 
> 

<span data-ttu-id="85b76-112">Olá exemplo a seguir configura um contêiner de conta de armazenamento privado e carrega um modelo:</span><span class="sxs-lookup"><span data-stu-id="85b76-112">hello following example sets up a private storage account container and uploads a template:</span></span>
   
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

### <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="85b76-113">Forneça um token SAS durante a implantação</span><span class="sxs-lookup"><span data-stu-id="85b76-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="85b76-114">toodeploy um modelo particular em uma conta de armazenamento, gerar um token SAS e incluí-lo em hello URI para o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="85b76-114">toodeploy a private template in a storage account, generate a SAS token and include it in hello URI for hello template.</span></span> <span data-ttu-id="85b76-115">Defina tooallow de tempo de expiração Olá suficiente implantação toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="85b76-115">Set hello expiry time tooallow enough time toocomplete hello deployment.</span></span>
   
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

<span data-ttu-id="85b76-116">Para ver um exemplo de como usar um token SAS com modelos vinculados, consulte [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="85b76-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="85b76-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="85b76-117">Next steps</span></span>
* <span data-ttu-id="85b76-118">Para modelos de toodeploying uma introdução, consulte [implantar recursos com modelos do Gerenciador de recursos e o Azure PowerShell](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="85b76-118">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="85b76-119">Para um script de exemplo completo que implanta um modelo, veja [Implantar o script de modelo do Resource Manager](resource-manager-samples-cli-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="85b76-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md)</span></span>
* <span data-ttu-id="85b76-120">parâmetros de toodefine no modelo, consulte [criar modelos](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="85b76-120">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="85b76-121">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="85b76-121">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
