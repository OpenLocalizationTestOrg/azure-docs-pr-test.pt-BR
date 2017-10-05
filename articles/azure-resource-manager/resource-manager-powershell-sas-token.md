---
title: Implantar o modelo do Azure com o token SAS e o PowerShell | Microsoft Docs
description: "Use o Azure Resource Manager e o Azure PowerShell para implantar recursos para o Azure de um modelo que é protegido com o token SAS."
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
ms.openlocfilehash: 1e3cea027b599e2b1af1ced0fdf14e2cc8a0db82
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a><span data-ttu-id="fa813-103">Implantar o modelo particular do Resource Manager com o Azure PowerShell e o token SAS</span><span class="sxs-lookup"><span data-stu-id="fa813-103">Deploy private Resource Manager template with SAS token and Azure PowerShell</span></span>

<span data-ttu-id="fa813-104">Quando seu modelo reside em uma conta de armazenamento, você pode restringir o acesso a ele e fornecer um token de SAS (Assinatura de Acesso Compartilhado) durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="fa813-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="fa813-105">Este tópico explica como usar o Azure PowerShell com modelos do Resource Manager para fornecer um token SAS durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="fa813-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span></span> 

## <a name="add-private-template-to-storage-account"></a><span data-ttu-id="fa813-106">Adicionar modelo privado à conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="fa813-106">Add private template to storage account</span></span>

<span data-ttu-id="fa813-107">Você pode adicionar seus modelos a uma conta de armazenamento e vinculá-los durante a implantação com um token SAS.</span><span class="sxs-lookup"><span data-stu-id="fa813-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa813-108">Seguindo as etapas abaixo, o blob que contém o modelo fica acessível somente para o proprietário da conta.</span><span class="sxs-lookup"><span data-stu-id="fa813-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span></span> <span data-ttu-id="fa813-109">No entanto, quando você cria um token SAS para o blob, o blob fica acessível para qualquer pessoa com o URI.</span><span class="sxs-lookup"><span data-stu-id="fa813-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span></span> <span data-ttu-id="fa813-110">Se outro usuário interceptar o URI, esse usuário será capaz de acessar o modelo.</span><span class="sxs-lookup"><span data-stu-id="fa813-110">If another user intercepts the URI, that user is able to access the template.</span></span> <span data-ttu-id="fa813-111">Usar um token SAS é uma boa maneira de limitar o acesso aos seus modelos, mas você não deve incluir dados confidenciais como senhas diretamente no modelo.</span><span class="sxs-lookup"><span data-stu-id="fa813-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span></span>
> 
> 

<span data-ttu-id="fa813-112">O seguinte exemplo configura um contêiner de conta de armazenamento privado e carrega um modelo:</span><span class="sxs-lookup"><span data-stu-id="fa813-112">The following example sets up a private storage account container and uploads a template:</span></span>
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="fa813-113">Forneça um token SAS durante a implantação</span><span class="sxs-lookup"><span data-stu-id="fa813-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="fa813-114">Para implantar um modelo privado em uma conta de armazenamento, gere um token SAS e inclua-o no URI para o modelo.</span><span class="sxs-lookup"><span data-stu-id="fa813-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="fa813-115">Defina a hora de vencimento de forma a permitir que haja tempo suficiente para concluir a implantação.</span><span class="sxs-lookup"><span data-stu-id="fa813-115">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get the URI with the SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

<span data-ttu-id="fa813-116">Para ver um exemplo de como usar um token SAS com modelos vinculados, consulte [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fa813-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="fa813-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fa813-117">Next steps</span></span>
* <span data-ttu-id="fa813-118">Para obter uma introdução à implantação de modelos, veja [Implantar recursos com modelos do Resource Manager e o Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="fa813-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="fa813-119">Para um script de exemplo completo que implanta um modelo, veja [Implantar o script de modelo do Resource Manager](resource-manager-samples-powershell-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="fa813-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md)</span></span>
* <span data-ttu-id="fa813-120">Para definir os parâmetros no modelo, consulte [Criando modelos](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="fa813-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="fa813-121">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="fa813-121">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

