---
title: "Criar um namespace do Barramento de Serviço usando um modelo do Azure Resource Manager | Microsoft Docs"
description: "Usar modelo do Azure Resource Manager para criar um namespace do Barramento de Serviço"
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
ms.openlocfilehash: 8fff390919a1807995646dab322b4cbe56dd0268
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="11fdf-103">Criar um namespace do Barramento de Serviço usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="11fdf-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="11fdf-104">Este artigo descreve como usar um modelo do Azure Resource Manager que cria um namespace de Barramento de Serviço do tipo **Mensagens** com um SKU Standard/Básico.</span><span class="sxs-lookup"><span data-stu-id="11fdf-104">This article describes how to use an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="11fdf-105">O artigo também define os parâmetros que são especificados para execução da implantação.</span><span class="sxs-lookup"><span data-stu-id="11fdf-105">The article also defines the parameters that are specified for the execution of the deployment.</span></span> <span data-ttu-id="11fdf-106">Você pode usar este modelo para suas próprias implantações ou personalizá-lo para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="11fdf-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="11fdf-107">Para saber mais sobre a criação de modelos, confira [Criando modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="11fdf-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="11fdf-108">Para ver o modelo completo, confira o [Modelo de namespace do Barramento de Serviço][Service Bus namespace template] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="11fdf-108">For the complete template, see the [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="11fdf-109">Os modelos do Azure Resource Manager a seguir estão disponíveis para download e implantação.</span><span class="sxs-lookup"><span data-stu-id="11fdf-109">The following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="11fdf-110">Criar um namespace do Barramento de Serviço com fila</span><span class="sxs-lookup"><span data-stu-id="11fdf-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="11fdf-111">Criar um namespace do Barramento de Serviço com tópico e assinatura</span><span class="sxs-lookup"><span data-stu-id="11fdf-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="11fdf-112">Create a Service Bus namespace with queue and authorization rule (Criar um namespace de Barramento de Serviço com fila e regra de autorização)</span><span class="sxs-lookup"><span data-stu-id="11fdf-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="11fdf-113">Criar um namespace do Barramento de Serviço com tópico, assinatura e regra</span><span class="sxs-lookup"><span data-stu-id="11fdf-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="11fdf-114">Para verificar os modelos mais recentes, visite a galeria [Modelos de Início Rápido do Azure][Azure Quickstart Templates] e pesquise por Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="11fdf-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="11fdf-115">O que você implantará?</span><span class="sxs-lookup"><span data-stu-id="11fdf-115">What will you deploy?</span></span>
<span data-ttu-id="11fdf-116">Com esse modelo, você implantará um namespace de Barramento de Serviço com uma SKU [Básica, Standard ou Premium](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="11fdf-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="11fdf-117">Para executar a implantação automaticamente, clique no seguinte botão:</span><span class="sxs-lookup"><span data-stu-id="11fdf-117">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="11fdf-118">[![Implantar no Azure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="11fdf-118">[![Deploy to Azure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="11fdf-119">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="11fdf-119">Parameters</span></span>
<span data-ttu-id="11fdf-120">Com o Gerenciador de Recursos do Azure, você define parâmetros para os valores que deseja especificar quando o modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="11fdf-120">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="11fdf-121">O modelo inclui uma seção chamada `Parameters` , que contém todos os valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="11fdf-121">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="11fdf-122">Você deve definir um parâmetro para os valores que variam de acordo com o projeto que você está implantando ou com o ambiente em que a implantação ocorre.</span><span class="sxs-lookup"><span data-stu-id="11fdf-122">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="11fdf-123">Não defina parâmetros para valores que permanecem sempre os mesmos.</span><span class="sxs-lookup"><span data-stu-id="11fdf-123">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="11fdf-124">Cada valor de parâmetro é usado no modelo para definir os recursos que são implantados.</span><span class="sxs-lookup"><span data-stu-id="11fdf-124">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="11fdf-125">Este modelo define os parâmetros a seguir.</span><span class="sxs-lookup"><span data-stu-id="11fdf-125">This template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="11fdf-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="11fdf-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="11fdf-127">O nome do namespace do Barramento de Serviço a ser criado.</span><span class="sxs-lookup"><span data-stu-id="11fdf-127">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of the Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="11fdf-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="11fdf-128">serviceBusSKU</span></span>
<span data-ttu-id="11fdf-129">O nome do [SKU](https://azure.microsoft.com/pricing/details/service-bus/) do Barramento de Serviço a ser criado.</span><span class="sxs-lookup"><span data-stu-id="11fdf-129">The name of the Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) to create.</span></span>

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
        "description": "The messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="11fdf-130">O modelo definirá os valores permitidos para esse parâmetro (Basic, Standard ou Premium) e atribuirá um valor padrão (Standard) se nenhum valor for especificado.</span><span class="sxs-lookup"><span data-stu-id="11fdf-130">The template defines the values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="11fdf-131">Para saber mais sobre os preços do Barramento de Serviço, confira [Preços e cobrança do Barramento de Serviço][Service Bus pricing and billing].</span><span class="sxs-lookup"><span data-stu-id="11fdf-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="11fdf-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="11fdf-132">serviceBusApiVersion</span></span>
<span data-ttu-id="11fdf-133">A versão da API do Barramento de Serviço do modelo.</span><span class="sxs-lookup"><span data-stu-id="11fdf-133">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by the template" 
       } 
```

## <a name="resources-to-deploy"></a><span data-ttu-id="11fdf-134">Recursos a implantar</span><span class="sxs-lookup"><span data-stu-id="11fdf-134">Resources to deploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="11fdf-135">Namespace do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="11fdf-135">Service Bus namespace</span></span>
<span data-ttu-id="11fdf-136">Cria um namespace do Barramento de Serviço padrão do tipo **Mensagens**.</span><span class="sxs-lookup"><span data-stu-id="11fdf-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="11fdf-137">Comandos para executar a implantação</span><span class="sxs-lookup"><span data-stu-id="11fdf-137">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="11fdf-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="11fdf-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="11fdf-139">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="11fdf-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="11fdf-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11fdf-140">Next steps</span></span>
<span data-ttu-id="11fdf-141">Agora que você criou e implantou recursos usando o Azure Resource Manager, saiba como gerenciar esses recursos lendo estes artigos:</span><span class="sxs-lookup"><span data-stu-id="11fdf-141">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by reading these articles:</span></span>

* [<span data-ttu-id="11fdf-142">Gerenciar o Barramento de Serviço com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="11fdf-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="11fdf-143">Gerenciar recursos do Barramento de Serviço com o Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="11fdf-143">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
