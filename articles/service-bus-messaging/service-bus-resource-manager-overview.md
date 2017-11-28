---
title: recursos do Azure Service Bus aaaCreate usando modelos do Gerenciador de recursos do Azure | Microsoft Docs
description: "Usar o Gerenciador de recursos do Azure modelos tooautomate Olá criação de recursos do barramento de serviço"
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
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="bc3d8-103">Criar recursos do Barramento de Serviço usando modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bc3d8-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="bc3d8-104">Este artigo descreve como toocreate e implantar recursos de barramento de serviço usando o provedor de recursos do barramento de serviço hello, PowerShell e modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-104">This article describes how toocreate and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and hello Service Bus resource provider.</span></span>

<span data-ttu-id="bc3d8-105">Modelos do Gerenciador de recursos do Azure ajudarão-lo a definir Olá toodeploy de recursos para uma solução e toospecify parâmetros e variáveis que permitem valores tooinput para ambientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-105">Azure Resource Manager templates help you define hello resources toodeploy for a solution, and toospecify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="bc3d8-106">Olá modelo consiste em JSON e expressões que você pode usar valores de tooconstruct para sua implantação.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="bc3d8-107">Para obter informações detalhadas sobre como escrever modelos do Gerenciador de recursos do Azure e uma discussão sobre o formato de saudação de modelo, consulte [estrutura e a sintaxe de modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bc3d8-107">For detailed information about writing Azure Resource Manager templates, and a discussion of hello template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bc3d8-108">Olá exemplos mostram esse artigo como toouse toocreate do Gerenciador de recursos do Azure um namespace de barramento de serviço e de entidade (fila) de mensagens.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-108">hello examples in this article show how toouse Azure Resource Manager toocreate a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="bc3d8-109">Para obter outros exemplos de modelo, visite Olá [Galeria de modelos de início rápido do Azure] [ Azure Quickstart Templates gallery] e procure "Barramento de serviço".</span><span class="sxs-lookup"><span data-stu-id="bc3d8-109">For other template examples, visit hello [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="bc3d8-110">Modelos do Gerenciador de Recursos do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="bc3d8-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="bc3d8-111">Esses modelos do Azure Resource Manager no Barramento de Serviço estão disponíveis para download e implantação.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="bc3d8-112">Clique em Olá seguindo os links para obter detalhes sobre cada um, com modelos de toohello links no GitHub:</span><span class="sxs-lookup"><span data-stu-id="bc3d8-112">Click hello following links for details about each one, with links toohello templates on GitHub:</span></span>

* [<span data-ttu-id="bc3d8-113">Criar um namespace do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="bc3d8-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="bc3d8-114">Criar um namespace do Barramento de Serviço com fila</span><span class="sxs-lookup"><span data-stu-id="bc3d8-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="bc3d8-115">Criar um namespace do Barramento de Serviço com tópico e assinatura</span><span class="sxs-lookup"><span data-stu-id="bc3d8-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="bc3d8-116">Create a Service Bus namespace with queue and authorization rule (Criar um namespace de Barramento de Serviço com fila e regra de autorização)</span><span class="sxs-lookup"><span data-stu-id="bc3d8-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="bc3d8-117">Criar um namespace do Barramento de Serviço com tópico, assinatura e regra</span><span class="sxs-lookup"><span data-stu-id="bc3d8-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="bc3d8-118">Implantação com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc3d8-118">Deploy with PowerShell</span></span>

<span data-ttu-id="bc3d8-119">Olá procedimento a seguir descreve como toouse PowerShell toodeploy um modelo do Gerenciador de recursos do Azure que cria um **padrão** camada namespace de barramento de serviço e uma fila no namespace.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-119">hello following procedure describes how toouse PowerShell toodeploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="bc3d8-120">Este exemplo é baseado no hello [criar um namespace de barramento de serviço com a fila](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) modelo.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-120">This example is based on hello [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="bc3d8-121">fluxo de trabalho aproximado Olá é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bc3d8-121">hello approximate workflow is as follows:</span></span>

1. <span data-ttu-id="bc3d8-122">Instale o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-122">Install PowerShell.</span></span>
2. <span data-ttu-id="bc3d8-123">Crie modelo hello e (opcionalmente) um arquivo de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-123">Create hello template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="bc3d8-124">No PowerShell, faça logon no tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-124">In PowerShell, log in tooyour Azure account.</span></span>
4. <span data-ttu-id="bc3d8-125">Crie um novo grupo de recursos se já não tiver um.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="bc3d8-126">Testar a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-126">Test hello deployment.</span></span>
6. <span data-ttu-id="bc3d8-127">Se desejar, defina o modo de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-127">If desired, set hello deployment mode.</span></span>
7. <span data-ttu-id="bc3d8-128">Implante o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-128">Deploy hello template.</span></span>

<span data-ttu-id="bc3d8-129">Para obter informações completas sobre a implantação de modelos do Azure Resource Manager, consulte [Implantar recursos com modelos do Azure Resource Manager][Deploy resources with Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="bc3d8-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="bc3d8-130">Instalar o PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc3d8-130">Install PowerShell</span></span>

<span data-ttu-id="bc3d8-131">Instale o Azure PowerShell, seguindo as instruções de saudação do [Introdução ao Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="bc3d8-131">Install Azure PowerShell by following hello instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="bc3d8-132">Criar um modelo</span><span class="sxs-lookup"><span data-stu-id="bc3d8-132">Create a template</span></span>

<span data-ttu-id="bc3d8-133">Olá clone ou copie [201 servicebus-criar-fila](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) modelo do GitHub:</span><span class="sxs-lookup"><span data-stu-id="bc3d8-133">Clone or copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
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

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="bc3d8-134">Criar um arquivo de parâmetros (opcional)</span><span class="sxs-lookup"><span data-stu-id="bc3d8-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="bc3d8-135">toouse um arquivo de parâmetros opcionais, Olá cópia [201 servicebus-criar-fila](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) arquivo.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-135">toouse an optional parameters file, copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="bc3d8-136">Substituir valor de saudação do `serviceBusNamespaceName` com o nome de saudação do namespace de barramento de serviço Olá desejado toocreate nesta implantação e substituir o valor de saudação de `serviceBusQueueName` com o nome de saudação da fila de saudação você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-136">Replace hello value of `serviceBusNamespaceName` with hello name of hello Service Bus namespace you want toocreate in this deployment, and replace hello value of `serviceBusQueueName` with hello name of hello queue you want toocreate.</span></span>

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

<span data-ttu-id="bc3d8-137">Para obter mais informações, consulte Olá [parâmetros](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) tópico.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-137">For more information, see hello [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a><span data-ttu-id="bc3d8-138">Faça logon no tooAzure e defina Olá assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="bc3d8-138">Log in tooAzure and set hello Azure subscription</span></span>

<span data-ttu-id="bc3d8-139">Em um prompt do PowerShell, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="bc3d8-139">From a PowerShell prompt, run hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="bc3d8-140">Você é solicitado toolog em tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-140">You are prompted toolog on tooyour Azure account.</span></span> <span data-ttu-id="bc3d8-141">Depois de fazer logon, execute Olá tooview de comando a seguir as assinaturas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-141">After logging on, run hello following command tooview your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="bc3d8-142">Esse comando retorna uma lista de assinaturas do Azure disponíveis.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="bc3d8-143">Escolha uma assinatura para Olá a sessão atual executando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-143">Choose a subscription for hello current session by running hello following command.</span></span> <span data-ttu-id="bc3d8-144">Substituir `<YourSubscriptionId>` com hello GUID para Olá assinatura do Azure, você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-144">Replace `<YourSubscriptionId>` with hello GUID for hello Azure subscription you want toouse.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a><span data-ttu-id="bc3d8-145">Grupo de recursos de saudação do conjunto</span><span class="sxs-lookup"><span data-stu-id="bc3d8-145">Set hello resource group</span></span>

<span data-ttu-id="bc3d8-146">Se você não tiver um recurso existente do grupo, crie um novo grupo de recursos com hello * * AzureRmResourceGroup New * * comando.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-146">If you do not have an existing resource group, create a new resource group with hello **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="bc3d8-147">Fornece nome de saudação do grupo de recursos de saudação e local que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-147">Provide hello name of hello resource group and location you want toouse.</span></span> <span data-ttu-id="bc3d8-148">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bc3d8-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="bc3d8-149">Se for bem-sucedido, será exibido um resumo do novo grupo de recursos hello.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-149">If successful, a summary of hello new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a><span data-ttu-id="bc3d8-150">Implantação de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="bc3d8-150">Test hello deployment</span></span>

<span data-ttu-id="bc3d8-151">Valide a implantação executando Olá `Test-AzureRmResourceGroupDeployment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-151">Validate your deployment by running hello `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="bc3d8-152">Ao testar a implantação de hello, forneça parâmetros exatamente como faria ao executar implantação hello.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-152">When testing hello deployment, provide parameters exactly as you would when executing hello deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a><span data-ttu-id="bc3d8-153">Criar implantação Olá</span><span class="sxs-lookup"><span data-stu-id="bc3d8-153">Create hello deployment</span></span>

<span data-ttu-id="bc3d8-154">toocreate Olá nova execução de implantação, Olá `New-AzureRmResourceGroupDeployment` cmdlet e forneça os parâmetros necessários do hello quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-154">toocreate hello new deployment, run hello `New-AzureRmResourceGroupDeployment` cmdlet, and provide hello necessary parameters when prompted.</span></span> <span data-ttu-id="bc3d8-155">parâmetros de saudação incluem um nome para sua implantação, nome de saudação do seu grupo de recursos e o caminho de saudação ou o arquivo de modelo de toohello de URL.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-155">hello parameters include a name for your deployment, hello name of your resource group, and hello path or URL toohello template file.</span></span> <span data-ttu-id="bc3d8-156">Se hello **modo** parâmetro não for especificado, Olá valor padrão de **Incremental** é usado.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-156">If hello **Mode** parameter is not specified, hello default value of **Incremental** is used.</span></span> <span data-ttu-id="bc3d8-157">Para saber mais, consulte [Implantações incrementais e completas](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="bc3d8-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="bc3d8-158">Olá prompts de comando a seguir é para parâmetros de saudação três na janela do PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="bc3d8-158">hello following command prompts you for hello three parameters in hello PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

<span data-ttu-id="bc3d8-159">toospecify um arquivo de parâmetros em vez disso, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-159">toospecify a parameters file instead, use hello following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="bc3d8-160">Você também pode usar parâmetros embutido quando você executa o cmdlet de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-160">You can also use inline parameters when you run hello deployment cmdlet.</span></span> <span data-ttu-id="bc3d8-161">comando Olá é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bc3d8-161">hello command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="bc3d8-162">toorun um [completa](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) de implantação, Olá conjunto **modo** parâmetro muito**concluir**:</span><span class="sxs-lookup"><span data-stu-id="bc3d8-162">toorun a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set hello **Mode** parameter too**Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="bc3d8-163">Verificar a implantação de saudação</span><span class="sxs-lookup"><span data-stu-id="bc3d8-163">Verify hello deployment</span></span>
<span data-ttu-id="bc3d8-164">Se os recursos de saudação são implantados com êxito, um resumo de implantação de saudação é exibido na janela do PowerShell Olá:</span><span class="sxs-lookup"><span data-stu-id="bc3d8-164">If hello resources are deployed successfully, a summary of hello deployment is displayed in hello PowerShell window:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bc3d8-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bc3d8-165">Next steps</span></span>
<span data-ttu-id="bc3d8-166">Agora você viu fluxo de trabalho básico hello e comandos para a implantação de um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc3d8-166">You've now seen hello basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="bc3d8-167">Para obter mais informações, visite Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="bc3d8-167">For more detailed information, visit hello following links:</span></span>

* <span data-ttu-id="bc3d8-168">[Visão geral do Azure Resource Manager][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="bc3d8-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="bc3d8-169">[Implantar recursos com modelos do Resource Manager e o Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="bc3d8-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="bc3d8-170">Criando modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="bc3d8-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
