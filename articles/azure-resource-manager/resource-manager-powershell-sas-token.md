---
title: aaaDeploy modelo do Azure com o token SAS e PowerShell | Microsoft Docs
description: "Use o Gerenciador de recursos do Azure e o Azure PowerShell toodeploy tooAzure de recursos de um modelo que está protegido com o token SAS."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: b95e096591d6213f8ef79235c8cd85705c4b79ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a><span data-ttu-id="6cafd-103">Implantar o modelo particular do Resource Manager com o Azure PowerShell e o token SAS</span><span class="sxs-lookup"><span data-stu-id="6cafd-103">Deploy private Resource Manager template with SAS token and Azure PowerShell</span></span>

<span data-ttu-id="6cafd-104">Quando o modelo estiver em uma conta de armazenamento, você pode restringir o modelo de toohello de acesso e fornecer um token de assinatura (SAS) de acesso compartilhado durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="6cafd-104">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="6cafd-105">Este tópico explica como toouse PowerShell do Azure com o Gerenciador de recursos modelos tooprovide um token SAS durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="6cafd-105">This topic explains how toouse Azure PowerShell with Resource Manager templates tooprovide a SAS token during deployment.</span></span> 

## <a name="add-private-template-toostorage-account"></a><span data-ttu-id="6cafd-106">Adicionar modelo particular toostorage conta</span><span class="sxs-lookup"><span data-stu-id="6cafd-106">Add private template toostorage account</span></span>

<span data-ttu-id="6cafd-107">Você pode adicionar sua conta de armazenamento tooa modelos e vincular toothem durante a implantação com um token SAS.</span><span class="sxs-lookup"><span data-stu-id="6cafd-107">You can add your templates tooa storage account and link toothem during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6cafd-108">Seguindo as etapas de saudação abaixo, o blob de saudação que contém o modelo de saudação é proprietário da conta Olá tooonly acessível.</span><span class="sxs-lookup"><span data-stu-id="6cafd-108">By following hello steps below, hello blob containing hello template is accessible tooonly hello account owner.</span></span> <span data-ttu-id="6cafd-109">No entanto, quando você cria um token SAS para blob hello, blob Olá é tooanyone acessível com esse URI.</span><span class="sxs-lookup"><span data-stu-id="6cafd-109">However, when you create a SAS token for hello blob, hello blob is accessible tooanyone with that URI.</span></span> <span data-ttu-id="6cafd-110">Se outro usuário interceptar Olá URI, esse usuário será capaz de tooaccess modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6cafd-110">If another user intercepts hello URI, that user is able tooaccess hello template.</span></span> <span data-ttu-id="6cafd-111">Usar um token SAS é uma boa maneira de limitar o acesso tooyour modelos, mas você não deve incluir dados confidenciais, como senhas diretamente no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6cafd-111">Using a SAS token is a good way of limiting access tooyour templates, but you should not include sensitive data like passwords directly in hello template.</span></span>
> 
> 

<span data-ttu-id="6cafd-112">Olá exemplo a seguir configura um contêiner de conta de armazenamento privado e carrega um modelo:</span><span class="sxs-lookup"><span data-stu-id="6cafd-112">hello following example sets up a private storage account container and uploads a template:</span></span>
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="6cafd-113">Forneça um token SAS durante a implantação</span><span class="sxs-lookup"><span data-stu-id="6cafd-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="6cafd-114">toodeploy um modelo particular em uma conta de armazenamento, gerar um token SAS e incluí-lo em hello URI para o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6cafd-114">toodeploy a private template in a storage account, generate a SAS token and include it in hello URI for hello template.</span></span> <span data-ttu-id="6cafd-115">Defina tooallow de tempo de expiração Olá suficiente implantação toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="6cafd-115">Set hello expiry time tooallow enough time toocomplete hello deployment.</span></span>
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get hello URI with hello SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

<span data-ttu-id="6cafd-116">Para ver um exemplo de como usar um token SAS com modelos vinculados, consulte [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6cafd-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="6cafd-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6cafd-117">Next steps</span></span>
* <span data-ttu-id="6cafd-118">Para modelos de toodeploying uma introdução, consulte [implantar recursos com modelos do Gerenciador de recursos e o Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6cafd-118">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="6cafd-119">Para um script de exemplo completo que implanta um modelo, veja [Implantar o script de modelo do Resource Manager](resource-manager-samples-powershell-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="6cafd-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md)</span></span>
* <span data-ttu-id="6cafd-120">parâmetros de toodefine no modelo, consulte [criar modelos](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="6cafd-120">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="6cafd-121">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="6cafd-121">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

