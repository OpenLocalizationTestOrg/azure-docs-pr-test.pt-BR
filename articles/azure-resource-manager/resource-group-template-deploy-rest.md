---
title: recursos de aaaDeploy com API REST e o modelo | Microsoft Docs
description: "Use toodeploy um tooAzure de recursos de Gerenciador de recursos do Azure e API de REST do Gerenciador de recursos. Olá recursos são definidos em um modelo do Gerenciador de recursos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="fa783-104">Implantar recursos com modelos do Resource Manager e a API REST do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fa783-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fa783-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa783-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="fa783-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="fa783-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="fa783-107">Portal</span><span class="sxs-lookup"><span data-stu-id="fa783-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="fa783-108">API REST</span><span class="sxs-lookup"><span data-stu-id="fa783-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="fa783-109">Este artigo explica como toouse Olá REST API do Gerenciador de recursos com o Gerenciador de recursos modelos toodeploy tooAzure seus recursos.</span><span class="sxs-lookup"><span data-stu-id="fa783-109">This article explains how toouse hello Resource Manager REST API with Resource Manager templates toodeploy your resources tooAzure.</span></span>  

> [!TIP]
> <span data-ttu-id="fa783-110">Para obter ajuda com a depuração de erros durante a implantação, consulte:</span><span class="sxs-lookup"><span data-stu-id="fa783-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="fa783-111">[Exibir operações de implantação](resource-manager-deployment-operations.md) toolearn sobre a obtenção de informações que ajudam você a solucionar o erro</span><span class="sxs-lookup"><span data-stu-id="fa783-111">[View deployment operations](resource-manager-deployment-operations.md) toolearn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="fa783-112">[Solucionar erros comuns ao implantar recursos tooAzure com o Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn como tooresolve erros comuns de implantação</span><span class="sxs-lookup"><span data-stu-id="fa783-112">[Troubleshoot common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn how tooresolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="fa783-113">Seu modelo pode ser um arquivo local ou um arquivo externo que está disponível por meio de um URI.</span><span class="sxs-lookup"><span data-stu-id="fa783-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="fa783-114">Quando o modelo estiver em uma conta de armazenamento, você pode restringir o modelo de toohello de acesso e fornecer um token de assinatura (SAS) de acesso compartilhado durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="fa783-114">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="fa783-115">Implantar com hello API REST</span><span class="sxs-lookup"><span data-stu-id="fa783-115">Deploy with hello REST API</span></span>
1. <span data-ttu-id="fa783-116">Definir [Parâmetros e cabeçalhos comuns](https://docs.microsoft.com/rest/api/index), incluindo tokens de autenticação.</span><span class="sxs-lookup"><span data-stu-id="fa783-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="fa783-117">Se você não tiver um grupo de recursos existente, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="fa783-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="fa783-118">Forneça seu ID de assinatura, o nome de saudação do novo grupo de recursos hello e local que você precisa para sua solução.</span><span class="sxs-lookup"><span data-stu-id="fa783-118">Provide your subscription ID, hello name of hello new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="fa783-119">Para obter mais informações, consulte [Criar um grupo de recursos](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="fa783-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="fa783-120">Validar sua implantação antes de executá-lo executando Olá [validar uma implantação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operação.</span><span class="sxs-lookup"><span data-stu-id="fa783-120">Validate your deployment before executing it by running hello [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="fa783-121">Ao testar a implantação de hello, forneça parâmetros exatamente como faria ao executar implantação hello (mostrada na próxima etapa do hello).</span><span class="sxs-lookup"><span data-stu-id="fa783-121">When testing hello deployment, provide parameters exactly as you would when executing hello deployment (shown in hello next step).</span></span>
4. <span data-ttu-id="fa783-122">Crie uma implantação.</span><span class="sxs-lookup"><span data-stu-id="fa783-122">Create a deployment.</span></span> <span data-ttu-id="fa783-123">Fornece sua ID de assinatura, nome Olá Olá do grupo de recursos, nome de saudação da implantação de saudação e um modelo de tooyour de link.</span><span class="sxs-lookup"><span data-stu-id="fa783-123">Provide your subscription ID, hello name of hello resource group, hello name of hello deployment, and a link tooyour template.</span></span> <span data-ttu-id="fa783-124">Para obter informações sobre o arquivo de modelo hello, consulte [arquivo de parâmetro](#parameter-file).</span><span class="sxs-lookup"><span data-stu-id="fa783-124">For information about hello template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="fa783-125">Para obter mais informações sobre a API REST de saudação toocreate um grupo de recursos, consulte [criar uma implantação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="fa783-125">For more information about hello REST API toocreate a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="fa783-126">Saudação de aviso **modo** está definido muito**Incremental**.</span><span class="sxs-lookup"><span data-stu-id="fa783-126">Notice hello **mode** is set too**Incremental**.</span></span> <span data-ttu-id="fa783-127">toorun uma implantação completa, defina **modo** muito**concluir**.</span><span class="sxs-lookup"><span data-stu-id="fa783-127">toorun a complete deployment, set **mode** too**Complete**.</span></span> <span data-ttu-id="fa783-128">Tenha cuidado ao usar o modo completo Olá inadvertidamente, você pode excluir recursos que não estão no modelo.</span><span class="sxs-lookup"><span data-stu-id="fa783-128">Be careful when using hello complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      <span data-ttu-id="fa783-129">Se desejar que o conteúdo da resposta toolog, conteúdo da solicitação ou ambos, incluir **debugSetting** na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa783-129">If you want toolog response content, request content, or both, include **debugSetting** in hello request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="fa783-130">Você pode configurar seu toouse de conta de armazenamento um token de acesso compartilhado (SAS) de assinatura.</span><span class="sxs-lookup"><span data-stu-id="fa783-130">You can set up your storage account toouse a shared access signature (SAS) token.</span></span> <span data-ttu-id="fa783-131">Para obter mais informações, consulte [Delegando Acesso com uma Assinatura de Acesso Compartilhado](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="fa783-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="fa783-132">Obter status de saudação da implantação de modelo hello.</span><span class="sxs-lookup"><span data-stu-id="fa783-132">Get hello status of hello template deployment.</span></span> <span data-ttu-id="fa783-133">Para obter mais informações, consulte [obter informações sobre uma implantação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="fa783-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="fa783-134">Arquivo de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="fa783-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="fa783-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fa783-135">Next steps</span></span>
* <span data-ttu-id="fa783-136">toolearn sobre como lidar com operações assíncronas de REST, consulte [controlar operações assíncronas de Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="fa783-136">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="fa783-137">Para obter um exemplo de implantação de recursos por meio da biblioteca de cliente .NET hello, consulte [implantar recursos usando as bibliotecas .NET e um modelo](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fa783-137">For an example of deploying resources through hello .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="fa783-138">parâmetros de toodefine no modelo, consulte [criar modelos](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="fa783-138">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="fa783-139">Para obter orientação sobre a implantação de ambientes de toodifferent sua solução, consulte [ambientes de desenvolvimento e teste no Microsoft Azure](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="fa783-139">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="fa783-140">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="fa783-140">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

