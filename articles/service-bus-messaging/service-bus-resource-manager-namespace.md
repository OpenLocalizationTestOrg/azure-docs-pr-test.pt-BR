---
title: "namespace de barramento de serviço aaaCreate usando um modelo do Gerenciador de recursos do Azure | Microsoft Docs"
description: "Use o Gerenciador de recursos do Azure modelo toocreate um namespace de barramento de serviço"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: dc0d6482-6344-4cef-8644-d4573639f5e4
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: fddf370affe761a734991ae9b60c1e5825e54ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="8aae2-103">Criar um namespace do Barramento de Serviço usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8aae2-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="8aae2-104">Este artigo descreve como toouse um modelo do Gerenciador de recursos do Azure que cria um namespace de barramento de serviço do tipo **mensagens** com um SKU Standard/Basic.</span><span class="sxs-lookup"><span data-stu-id="8aae2-104">This article describes how toouse an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="8aae2-105">artigo Olá também define os parâmetros de saudação que são especificados para a execução de saudação da implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8aae2-105">hello article also defines hello parameters that are specified for hello execution of hello deployment.</span></span> <span data-ttu-id="8aae2-106">Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="8aae2-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="8aae2-107">Para saber mais sobre a criação de modelos, veja [Criando modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="8aae2-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="8aae2-108">Para o modelo completo de Olá, consulte Olá [modelo de namespace do barramento de serviço] [ Service Bus namespace template] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="8aae2-108">For hello complete template, see hello [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="8aae2-109">saudação do Azure Resource Manager modelos a seguir está disponível para download e implantação.</span><span class="sxs-lookup"><span data-stu-id="8aae2-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="8aae2-110">Criar um namespace do Barramento de Serviço com fila</span><span class="sxs-lookup"><span data-stu-id="8aae2-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="8aae2-111">Criar um namespace do Barramento de Serviço com tópico e assinatura</span><span class="sxs-lookup"><span data-stu-id="8aae2-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="8aae2-112">Create a Service Bus namespace with queue and authorization rule (Criar um namespace de Barramento de Serviço com fila e regra de autorização)</span><span class="sxs-lookup"><span data-stu-id="8aae2-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="8aae2-113">Criar um namespace do Barramento de Serviço com tópico, assinatura e regra</span><span class="sxs-lookup"><span data-stu-id="8aae2-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="8aae2-114">toocheck para modelos de hello mais recentes, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] galeria e pesquisa para o barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="8aae2-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="8aae2-115">O que você implantará?</span><span class="sxs-lookup"><span data-stu-id="8aae2-115">What will you deploy?</span></span>
<span data-ttu-id="8aae2-116">Com esse modelo, você implantará um namespace de Barramento de Serviço com uma SKU [Básica, Standard ou Premium](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="8aae2-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="8aae2-117">toorun Olá implantação automaticamente, clique em Olá botão a seguir:</span><span class="sxs-lookup"><span data-stu-id="8aae2-117">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="8aae2-118">[![Implantar tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="8aae2-118">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="8aae2-119">parâmetros</span><span class="sxs-lookup"><span data-stu-id="8aae2-119">Parameters</span></span>
<span data-ttu-id="8aae2-120">No Gerenciador de recursos do Azure, você define parâmetros para os valores desejados toospecify quando Olá modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="8aae2-120">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="8aae2-121">modelo de saudação inclui uma seção chamada `Parameters` que contém todos os valores de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="8aae2-121">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="8aae2-122">Você deve definir um parâmetro para os valores que variam com base no projeto Olá que estiver implantando ou com base no ambiente de saudação que você está implantando.</span><span class="sxs-lookup"><span data-stu-id="8aae2-122">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="8aae2-123">Não defina parâmetros para valores sempre ficará Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="8aae2-123">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="8aae2-124">Cada valor de parâmetro é usado em Olá modelo toodefine Olá recursos implantados.</span><span class="sxs-lookup"><span data-stu-id="8aae2-124">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="8aae2-125">Esse modelo define Olá parâmetros a seguir.</span><span class="sxs-lookup"><span data-stu-id="8aae2-125">This template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="8aae2-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="8aae2-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="8aae2-127">nome de saudação do hello toocreate de namespace de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="8aae2-127">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="8aae2-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="8aae2-128">serviceBusSKU</span></span>
<span data-ttu-id="8aae2-129">nome de saudação do hello barramento de serviço [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span><span class="sxs-lookup"><span data-stu-id="8aae2-129">hello name of hello Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span></span>

```json
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Basic", 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "hello messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="8aae2-130">modelo de saudação define os valores de saudação que são permitidos para este parâmetro (Basic, Standard ou Premium) e atribui um valor padrão (padrão) se nenhum valor for especificado.</span><span class="sxs-lookup"><span data-stu-id="8aae2-130">hello template defines hello values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="8aae2-131">Para saber mais sobre os preços do Barramento de Serviço, confira [Preços e cobrança do Barramento de Serviço][Service Bus pricing and billing].</span><span class="sxs-lookup"><span data-stu-id="8aae2-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="8aae2-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="8aae2-132">serviceBusApiVersion</span></span>
<span data-ttu-id="8aae2-133">versão de API do barramento de serviço de saudação do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8aae2-133">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by hello template" 
       } 
```

## <a name="resources-toodeploy"></a><span data-ttu-id="8aae2-134">Recursos toodeploy</span><span class="sxs-lookup"><span data-stu-id="8aae2-134">Resources toodeploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="8aae2-135">Namespace do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="8aae2-135">Service Bus namespace</span></span>
<span data-ttu-id="8aae2-136">Cria um namespace do Barramento de Serviço padrão do tipo **Mensagens**.</span><span class="sxs-lookup"><span data-stu-id="8aae2-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

```json
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "properties": {
        }
    }
]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="8aae2-137">Implantação de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="8aae2-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="8aae2-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8aae2-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="8aae2-139">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8aae2-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="8aae2-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8aae2-140">Next steps</span></span>
<span data-ttu-id="8aae2-141">Agora que você criou e implantou recursos usando o Gerenciador de recursos do Azure, Aprenda como toomanage esses recursos ao ler estes artigos:</span><span class="sxs-lookup"><span data-stu-id="8aae2-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by reading these articles:</span></span>

* [<span data-ttu-id="8aae2-142">Gerenciar o Barramento de Serviço com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8aae2-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="8aae2-143">Gerenciar recursos do barramento de serviço com hello Explorador do barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="8aae2-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
