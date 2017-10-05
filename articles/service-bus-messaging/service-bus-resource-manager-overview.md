---
title: "Criar recursos do Barramento de Serviço do Azure usando modelos do Azure Resource Manager | Microsoft Docs"
description: "Usar modelos do Azure Resource Manager para automatizar a criação de recursos do Barramento de Serviço"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: c8142d8edfd3a527b13d655bac21acf5332f2d14
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="c6fa9-103">Criar recursos do Barramento de Serviço usando modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c6fa9-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="c6fa9-104">Este artigo descreve como criar e implantar recursos do Barramento de Serviço usando modelos do Azure Resource Manager, o PowerShell e o provedor de recursos do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-104">This article describes how to create and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and the Service Bus resource provider.</span></span>

<span data-ttu-id="c6fa9-105">Os modelos do Azure Resource Manager ajudam você a definir os recursos a serem implantados em uma solução e a especificar os parâmetros e variáveis que lhe permitem inserir valores para diferentes ambientes.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-105">Azure Resource Manager templates help you define the resources to deploy for a solution, and to specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="c6fa9-106">O modelo consiste em JSON e expressões que podem ser usados na criação de valores para sua implantação.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="c6fa9-107">Para obter informações detalhadas sobre a criação de modelos do Azure Resource Manager e uma discussão sobre o formato do modelo, consulte [Estrutura e sintaxe dos modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c6fa9-107">For detailed information about writing Azure Resource Manager templates, and a discussion of the template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c6fa9-108">Os exemplos neste artigo mostram como usar o Azure Resource Manager para criar um namespace do Barramento de Serviço e uma entidade de mensagens (fila).</span><span class="sxs-lookup"><span data-stu-id="c6fa9-108">The examples in this article show how to use Azure Resource Manager to create a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="c6fa9-109">Para obter outros exemplos de modelo, visite a [Galeria de Modelos de Início Rápido do Azure][Azure Quickstart Templates gallery] e pesquise “Barramento de Serviço”.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-109">For other template examples, visit the [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="c6fa9-110">Modelos do Gerenciador de Recursos do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="c6fa9-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="c6fa9-111">Esses modelos do Azure Resource Manager no Barramento de Serviço estão disponíveis para download e implantação.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="c6fa9-112">Clique nos links abaixo para obter detalhes sobre cada um, com links para os modelos no GitHub:</span><span class="sxs-lookup"><span data-stu-id="c6fa9-112">Click the following links for details about each one, with links to the templates on GitHub:</span></span>

* [<span data-ttu-id="c6fa9-113">Criar um namespace do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="c6fa9-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="c6fa9-114">Criar um namespace do Barramento de Serviço com fila</span><span class="sxs-lookup"><span data-stu-id="c6fa9-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="c6fa9-115">Criar um namespace do Barramento de Serviço com tópico e assinatura</span><span class="sxs-lookup"><span data-stu-id="c6fa9-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="c6fa9-116">Create a Service Bus namespace with queue and authorization rule (Criar um namespace de Barramento de Serviço com fila e regra de autorização)</span><span class="sxs-lookup"><span data-stu-id="c6fa9-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="c6fa9-117">Criar um namespace do Barramento de Serviço com tópico, assinatura e regra</span><span class="sxs-lookup"><span data-stu-id="c6fa9-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="c6fa9-118">Implantação com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6fa9-118">Deploy with PowerShell</span></span>

<span data-ttu-id="c6fa9-119">O procedimento a seguir descreve como usar o PowerShell para implantar um modelo do Azure Resource Manager que cria um namespace de Barramento de Serviço de camada **Padrão** e uma fila dentro desse namespace.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-119">The following procedure describes how to use PowerShell to deploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="c6fa9-120">Este exemplo se baseia no modelo [Criar um namespace de Barramento de Serviço com fila](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue).</span><span class="sxs-lookup"><span data-stu-id="c6fa9-120">This example is based on the [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="c6fa9-121">O fluxo de trabalho é mais ou menos o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c6fa9-121">The approximate workflow is as follows:</span></span>

1. <span data-ttu-id="c6fa9-122">Instale o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-122">Install PowerShell.</span></span>
2. <span data-ttu-id="c6fa9-123">Crie o modelo e (opcionalmente) um arquivo de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-123">Create the template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="c6fa9-124">No PowerShell, faça logon em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-124">In PowerShell, log in to your Azure account.</span></span>
4. <span data-ttu-id="c6fa9-125">Crie um novo grupo de recursos se já não tiver um.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="c6fa9-126">Teste a implantação.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-126">Test the deployment.</span></span>
6. <span data-ttu-id="c6fa9-127">Se desejar, defina o modo de implantação.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-127">If desired, set the deployment mode.</span></span>
7. <span data-ttu-id="c6fa9-128">Implante o modelo.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-128">Deploy the template.</span></span>

<span data-ttu-id="c6fa9-129">Para obter informações completas sobre a implantação de modelos do Azure Resource Manager, consulte [Implantar recursos com modelos do Azure Resource Manager][Deploy resources with Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="c6fa9-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="c6fa9-130">Instalar o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6fa9-130">Install PowerShell</span></span>

<span data-ttu-id="c6fa9-131">Instale o Azure PowerShell seguindo as instruções em [Introdução ao Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="c6fa9-131">Install Azure PowerShell by following the instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="c6fa9-132">Criar um modelo</span><span class="sxs-lookup"><span data-stu-id="c6fa9-132">Create a template</span></span>

<span data-ttu-id="c6fa9-133">Clone ou copie o modelo [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) a partir do GitHub:</span><span class="sxs-lookup"><span data-stu-id="c6fa9-133">Clone or copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by the template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="c6fa9-134">Criar um arquivo de parâmetros (opcional)</span><span class="sxs-lookup"><span data-stu-id="c6fa9-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="c6fa9-135">Para usar um arquivo de parâmetros opcionais, copie o arquivo [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="c6fa9-135">To use an optional parameters file, copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="c6fa9-136">Substitua o valor de `serviceBusNamespaceName` pelo nome do namespace do Barramento de Serviço que você deseja criar nessa implantação e substitua o valor do `serviceBusQueueName` pelo nome da fila que deseja criar.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-136">Replace the value of `serviceBusNamespaceName` with the name of the Service Bus namespace you want to create in this deployment, and replace the value of `serviceBusQueueName` with the name of the queue you want to create.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

<span data-ttu-id="c6fa9-137">Para saber mais, consulte o tópico [Parâmetros](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).</span><span class="sxs-lookup"><span data-stu-id="c6fa9-137">For more information, see the [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-to-azure-and-set-the-azure-subscription"></a><span data-ttu-id="c6fa9-138">Fazer logon no Azure e definir a assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="c6fa9-138">Log in to Azure and set the Azure subscription</span></span>

<span data-ttu-id="c6fa9-139">Em um prompt do PowerShell, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c6fa9-139">From a PowerShell prompt, run the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="c6fa9-140">Você precisará entrar em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-140">You are prompted to log on to your Azure account.</span></span> <span data-ttu-id="c6fa9-141">Após o logon, execute o comando a seguir para exibir as assinaturas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-141">After logging on, run the following command to view your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="c6fa9-142">Esse comando retorna uma lista de assinaturas do Azure disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="c6fa9-143">Escolha uma assinatura para a sessão atual executando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-143">Choose a subscription for the current session by running the following command.</span></span> <span data-ttu-id="c6fa9-144">Substitua `<YourSubscriptionId>` pelo GUID da assinatura do Azure que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-144">Replace `<YourSubscriptionId>` with the GUID for the Azure subscription you want to use.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-the-resource-group"></a><span data-ttu-id="c6fa9-145">Definir o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c6fa9-145">Set the resource group</span></span>

<span data-ttu-id="c6fa9-146">Se você não tiver um grupo de recursos existente, crie um novo com o comando **New-AzureRmResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-146">If you do not have an existing resource group, create a new resource group with the **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="c6fa9-147">Forneça o nome do grupo de recursos e local que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-147">Provide the name of the resource group and location you want to use.</span></span> <span data-ttu-id="c6fa9-148">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c6fa9-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="c6fa9-149">Se for bem-sucedido, um resumo do novo grupo de recursos será exibido.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-149">If successful, a summary of the new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-the-deployment"></a><span data-ttu-id="c6fa9-150">Teste a implantação</span><span class="sxs-lookup"><span data-stu-id="c6fa9-150">Test the deployment</span></span>

<span data-ttu-id="c6fa9-151">Valide a implantação executando o cmdlet `Test-AzureRmResourceGroupDeployment`.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-151">Validate your deployment by running the `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="c6fa9-152">Ao testar a implantação, forneça parâmetros exatamente como faria durante a sua execução.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-152">When testing the deployment, provide parameters exactly as you would when executing the deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="create-the-deployment"></a><span data-ttu-id="c6fa9-153">Criar a implantação</span><span class="sxs-lookup"><span data-stu-id="c6fa9-153">Create the deployment</span></span>

<span data-ttu-id="c6fa9-154">Para criar a nova implantação, execute o cmdlet `New-AzureRmResourceGroupDeployment` e forneça os parâmetros necessários quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-154">To create the new deployment, run the `New-AzureRmResourceGroupDeployment` cmdlet, and provide the necessary parameters when prompted.</span></span> <span data-ttu-id="c6fa9-155">Os parâmetros incluem um nome para sua implantação, o nome do seu grupo de recursos e o caminho ou a URL para o arquivo do modelo.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-155">The parameters include a name for your deployment, the name of your resource group, and the path or URL to the template file.</span></span> <span data-ttu-id="c6fa9-156">Caso o parâmetro **Mode** não esteja especificado, o valor padrão de **Incremental** será usado.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-156">If the **Mode** parameter is not specified, the default value of **Incremental** is used.</span></span> <span data-ttu-id="c6fa9-157">Para saber mais, consulte [Implantações incrementais e completas](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="c6fa9-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="c6fa9-158">O comando abaixo solicita os três parâmetros na janela do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c6fa9-158">The following command prompts you for the three parameters in the PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

<span data-ttu-id="c6fa9-159">Para especificar um arquivo de parâmetros em vez disso, use o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-159">To specify a parameters file instead, use the following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -TemplateParameterFile <path to parameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="c6fa9-160">Você também pode usar parâmetros embutidos quando executa o cmdlet de implantação.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-160">You can also use inline parameters when you run the deployment cmdlet.</span></span> <span data-ttu-id="c6fa9-161">O comando é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c6fa9-161">The command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="c6fa9-162">Para executar uma implantação [completa](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments), defina o parâmetro **Mode** como **Complete**:</span><span class="sxs-lookup"><span data-stu-id="c6fa9-162">To run a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set the **Mode** parameter to **Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="verify-the-deployment"></a><span data-ttu-id="c6fa9-163">Verificar a implantação</span><span class="sxs-lookup"><span data-stu-id="c6fa9-163">Verify the deployment</span></span>
<span data-ttu-id="c6fa9-164">Se os recursos forem implantados com êxito, um resumo da implantação será exibido na janela do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c6fa9-164">If the resources are deployed successfully, a summary of the deployment is displayed in the PowerShell window:</span></span>

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a><span data-ttu-id="c6fa9-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6fa9-165">Next steps</span></span>
<span data-ttu-id="c6fa9-166">Agora você já viu o fluxo de trabalho básico e os comandos para implantar um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6fa9-166">You've now seen the basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="c6fa9-167">Para obter informações mais detalhadas, visite os seguintes links:</span><span class="sxs-lookup"><span data-stu-id="c6fa9-167">For more detailed information, visit the following links:</span></span>

* <span data-ttu-id="c6fa9-168">[Visão geral do Azure Resource Manager][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="c6fa9-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="c6fa9-169">[Implantar recursos com modelos do Resource Manager e o Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="c6fa9-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="c6fa9-170">Criando modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="c6fa9-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
