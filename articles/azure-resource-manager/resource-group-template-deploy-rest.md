---
title: Implantar recursos com a API REST e o modelo | Microsoft Docs
description: "Use o Azure Resource Manager e a API REST do Resource Manager para implantar recursos no Azure. Os recursos são definidos em um modelo do Resource Manager."
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
ms.openlocfilehash: 46856a25fb57bb2c5a3c1aeae13c11655e1a58a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="ad508-104">Implantar recursos com modelos do Resource Manager e a API REST do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ad508-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ad508-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad508-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="ad508-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ad508-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="ad508-107">Portal</span><span class="sxs-lookup"><span data-stu-id="ad508-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="ad508-108">API REST</span><span class="sxs-lookup"><span data-stu-id="ad508-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="ad508-109">Este artigo explica como usar a API REST do Resource Manager com modelos do Resource Manager para implantar seus recursos no Azure.</span><span class="sxs-lookup"><span data-stu-id="ad508-109">This article explains how to use the Resource Manager REST API with Resource Manager templates to deploy your resources to Azure.</span></span>  

> [!TIP]
> <span data-ttu-id="ad508-110">Para obter ajuda com a depuração de erros durante a implantação, consulte:</span><span class="sxs-lookup"><span data-stu-id="ad508-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="ad508-111">[Exibir operações de implantação](resource-manager-deployment-operations.md) para saber como obter informações que ajudarão a solucionar o erro</span><span class="sxs-lookup"><span data-stu-id="ad508-111">[View deployment operations](resource-manager-deployment-operations.md) to learn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="ad508-112">[Solucionar erros comuns ao implantar recursos no Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md) para saber como resolver os erros comuns da implantação</span><span class="sxs-lookup"><span data-stu-id="ad508-112">[Troubleshoot common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md) to learn how to resolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="ad508-113">Seu modelo pode ser um arquivo local ou um arquivo externo que está disponível por meio de um URI.</span><span class="sxs-lookup"><span data-stu-id="ad508-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="ad508-114">Quando seu modelo reside em uma conta de armazenamento, você pode restringir o acesso a ele e fornecer um token de SAS (Assinatura de Acesso Compartilhado) durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="ad508-114">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="ad508-115">Implantar com a API REST</span><span class="sxs-lookup"><span data-stu-id="ad508-115">Deploy with the REST API</span></span>
1. <span data-ttu-id="ad508-116">Definir [Parâmetros e cabeçalhos comuns](https://docs.microsoft.com/rest/api/index), incluindo tokens de autenticação.</span><span class="sxs-lookup"><span data-stu-id="ad508-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="ad508-117">Se você não tiver um grupo de recursos existente, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ad508-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="ad508-118">Forneça sua ID de assinatura, o nome do novo grupo de recursos e local que você precisa para sua solução.</span><span class="sxs-lookup"><span data-stu-id="ad508-118">Provide your subscription ID, the name of the new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="ad508-119">Para obter mais informações, consulte [Criar um grupo de recursos](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="ad508-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="ad508-120">Valide sua implantação antes de executá-la usando a operação [Validar uma implantação do modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) .</span><span class="sxs-lookup"><span data-stu-id="ad508-120">Validate your deployment before executing it by running the [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="ad508-121">Ao testar a implantação, forneça parâmetros exatamente como faria ao executar a implantação (mostrado na próxima etapa).</span><span class="sxs-lookup"><span data-stu-id="ad508-121">When testing the deployment, provide parameters exactly as you would when executing the deployment (shown in the next step).</span></span>
4. <span data-ttu-id="ad508-122">Crie uma implantação.</span><span class="sxs-lookup"><span data-stu-id="ad508-122">Create a deployment.</span></span> <span data-ttu-id="ad508-123">Forneça sua ID da assinatura, o nome do grupo de recursos, o nome da implantação e um link para seu modelo.</span><span class="sxs-lookup"><span data-stu-id="ad508-123">Provide your subscription ID, the name of the resource group, the name of the deployment, and a link to your template.</span></span> <span data-ttu-id="ad508-124">Para obter informações sobre o arquivo de modelo, consulte [Arquivo de parâmetro](#parameter-file).</span><span class="sxs-lookup"><span data-stu-id="ad508-124">For information about the template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="ad508-125">Para obter mais informações sobre a API REST para criar um grupo de recursos, consulte [Criar uma implantação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="ad508-125">For more information about the REST API to create a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="ad508-126">Observe que **mode** está definido como **Incremental**.</span><span class="sxs-lookup"><span data-stu-id="ad508-126">Notice the **mode** is set to **Incremental**.</span></span> <span data-ttu-id="ad508-127">Para executar uma implantação completa, defina **mode** como **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ad508-127">To run a complete deployment, set **mode** to **Complete**.</span></span> <span data-ttu-id="ad508-128">Tenha cuidado ao usar o modo completo, pois você pode excluir acidentalmente recursos que não estão em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="ad508-128">Be careful when using the complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
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
   
      <span data-ttu-id="ad508-129">Se você quiser registrar o conteúdo da resposta, o conteúdo da solicitação ou ambos, inclua **debugSetting** na solicitação.</span><span class="sxs-lookup"><span data-stu-id="ad508-129">If you want to log response content, request content, or both, include **debugSetting** in the request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="ad508-130">Você pode configurar sua conta de armazenamento para usar um token de SAS (Assinatura de Acesso Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="ad508-130">You can set up your storage account to use a shared access signature (SAS) token.</span></span> <span data-ttu-id="ad508-131">Para obter mais informações, consulte [Delegando Acesso com uma Assinatura de Acesso Compartilhado](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="ad508-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="ad508-132">Obtém o status da implantação do modelo.</span><span class="sxs-lookup"><span data-stu-id="ad508-132">Get the status of the template deployment.</span></span> <span data-ttu-id="ad508-133">Para obter mais informações, consulte [obter informações sobre uma implantação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="ad508-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="ad508-134">Arquivo de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="ad508-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="ad508-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ad508-135">Next steps</span></span>
* <span data-ttu-id="ad508-136">Para saber mais sobre como lidar com operações assíncronas de REST, confira [Track asynchronous Azure operations](resource-manager-async-operations.md) (Rastrear operações assíncronas do Azure).</span><span class="sxs-lookup"><span data-stu-id="ad508-136">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="ad508-137">Para obter um exemplo de como implantar recursos por meio da biblioteca de cliente do .NET, veja [Implantar recursos usando bibliotecas do .NET e um modelo](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad508-137">For an example of deploying resources through the .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="ad508-138">Para definir os parâmetros no modelo, consulte [Criando modelos](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="ad508-138">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="ad508-139">Para obter orientação sobre como implantar a solução em ambientes diferentes, confira [Ambientes de desenvolvimento e de teste no Microsoft Azure](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="ad508-139">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="ad508-140">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ad508-140">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

