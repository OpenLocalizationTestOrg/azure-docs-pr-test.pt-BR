---
title: "Usar o PowerShell para gerenciar recursos do Barramento de Serviço do Azure | Microsoft Docs"
description: "Use o módulo do PowerShell para criar e gerenciar recursos do Barramento de Serviço"
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 1205f9fcabf5788c970fbce257aa5ad04f32cddc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-manage-service-bus-resources"></a><span data-ttu-id="cbbcf-103">Use o módulo do PowerShell para gerenciar recursos do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="cbbcf-103">Use PowerShell to manage Service Bus resources</span></span>

<span data-ttu-id="cbbcf-104">O PowerShell do Microsoft Azure é um ambiente de script que você pode usar para controlar e automatizar a implantação e o gerenciamento dos serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-104">Microsoft Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of Azure services.</span></span> <span data-ttu-id="cbbcf-105">Este artigo descreve como usar o [Módulo do PowerShell do Resource Manager do Barramento de Serviço](/powershell/module/azurerm.servicebus) para provisionar e gerenciar entidades do Barramento de Serviço (namespaces, filas, tópicos e assinaturas) usando um script ou console local do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-105">This article describes how to use the [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) to provision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="cbbcf-106">Também é possível gerenciar entidades do Barramento de Serviço usando modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="cbbcf-107">Para obter mais informações, consulte o artigo [Criar recursos do Barramento de Serviço usando modelos do Azure Resource Manager](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cbbcf-107">For more information, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbbcf-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cbbcf-108">Prerequisites</span></span>

<span data-ttu-id="cbbcf-109">Antes de começar, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="cbbcf-109">Before you begin, you'll need the following:</span></span>

* <span data-ttu-id="cbbcf-110">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-110">An Azure subscription.</span></span> <span data-ttu-id="cbbcf-111">Para saber mais sobre como adquirir uma assinatura, confira [Opções de compra][purchase options], [ofertas para membros][member offers] ou [conta gratuita][free account].</span><span class="sxs-lookup"><span data-stu-id="cbbcf-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="cbbcf-112">Um computador com o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="cbbcf-113">Para obter instruções, consulte [Introdução aos cmdlets do Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="cbbcf-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="cbbcf-114">Um entendimento geral dos scripts do PowerShell, dos pacotes NuGet e do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-114">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="cbbcf-115">Introdução</span><span class="sxs-lookup"><span data-stu-id="cbbcf-115">Get started</span></span>

<span data-ttu-id="cbbcf-116">A primeira etapa é usar o PowerShell para fazer logon em sua conta do Azure e assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-116">The first step is to use PowerShell to log in to your Azure account and Azure subscription.</span></span> <span data-ttu-id="cbbcf-117">Siga as instruções contidas em [Introdução aos cmdlets do Azure PowerShell](/powershell/azure/get-started-azureps) para fazer logon em sua conta do Azure e recuperar e acessar os recursos em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-117">Follow the instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) to log in to your Azure account, and retrieve and access the resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="cbbcf-118">Provisionar um namespace do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="cbbcf-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="cbbcf-119">Ao trabalhar com namespaces do Barramento de Serviço, você pode usar os cmdlets [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace) e [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace).</span><span class="sxs-lookup"><span data-stu-id="cbbcf-119">When working with Service Bus namespaces, you can use the [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="cbbcf-120">Este exemplo cria algumas variáveis locais no script; `$Namespace` e `$Location`.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-120">This example creates a few local variables in the script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="cbbcf-121">`$Namespace` é o nome do namespace do Barramento de Serviço com o qual queremos trabalhar.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-121">`$Namespace` is the name of the Service Bus namespace with which we want to work.</span></span>
* <span data-ttu-id="cbbcf-122">`$Location` identifica o datacenter em que iremos provisionar o namespace.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-122">`$Location` identifies the data center in which will we provision the namespace.</span></span>
* <span data-ttu-id="cbbcf-123">`$CurrentNamespace` armazena o namespace de referência que recuperamos (ou criamos).</span><span class="sxs-lookup"><span data-stu-id="cbbcf-123">`$CurrentNamespace` stores the reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="cbbcf-124">Em um script real, `$Namespace` e `$Location` podem ser passados como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="cbbcf-125">Esta parte do script tem a seguinte função:</span><span class="sxs-lookup"><span data-stu-id="cbbcf-125">This part of the script does the following:</span></span>

1. <span data-ttu-id="cbbcf-126">Tenta recuperar um namespace do Barramento de Serviço com o nome especificado.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-126">Attempts to retrieve a Service Bus namespace with the specified name.</span></span>
2. <span data-ttu-id="cbbcf-127">Se o namespace for encontrado, ele informará o que foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-127">If the namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="cbbcf-128">Se o namespace não for encontrado, ele vai criar o namespace e, em seguida, recuperar o namespace recentemente criado.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-128">If the namespace is not found, it creates the namespace and then retrieves the newly created namespace.</span></span>
   
    ``` powershell
    # Query to see if the namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if the namespace already exists or needs to be created
    if ($CurrentNamespace)
    {
        Write-Host "The namespace $Namespace already exists in the $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "The $Namespace namespace does not exist."
        Write-Host "Creating the $Namespace namespace in the $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "The $Namespace namespace in Resource Group $ResGrpName in the $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="cbbcf-129">Criar uma regra de autorização de namespace</span><span class="sxs-lookup"><span data-stu-id="cbbcf-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="cbbcf-130">O exemplo a seguir mostra como gerenciar regras de autorização de namespace usando os cmdlets [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule) e [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span><span class="sxs-lookup"><span data-stu-id="cbbcf-130">The following example shows how to manage namespace authorization rules using the [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query to see if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if the rule already exists or needs to be created
if ($CurrentRule)
{
    Write-Host "The $AuthRule rule already exists for the namespace $Namespace."
}
else
{
    Write-Host "The $AuthRule rule does not exist."
    Write-Host "Creating the $AuthRule rule for the $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "The $AuthRule rule for the $Namespace namespace has been successfully created."

    Write-Host "Setting rights on the namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights to the namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a><span data-ttu-id="cbbcf-131">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="cbbcf-131">Create a queue</span></span>

<span data-ttu-id="cbbcf-132">Para criar uma fila ou um tópico, execute uma verificação de namespace usando o script na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-132">To create a queue or topic, perform a namespace check using the script in the previous section.</span></span> <span data-ttu-id="cbbcf-133">Em seguida, crie a fila:</span><span class="sxs-lookup"><span data-stu-id="cbbcf-133">Then, create the queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "The queue $QueueName already exists in the $Location region:"
}
else
{
    Write-Host "The $QueueName queue does not exist."
    Write-Host "Creating the $QueueName queue in the $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "The $QueueName queue in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="cbbcf-134">Modificar propriedades da fila</span><span class="sxs-lookup"><span data-stu-id="cbbcf-134">Modify queue properties</span></span>

<span data-ttu-id="cbbcf-135">Após executar o script na seção anterior, você pode usar o cmdlet [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) para atualizar as propriedades de uma fila, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbbcf-135">After executing the script in the preceding section, you can use the [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet to update the properties of a queue, as in the following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="cbbcf-136">Provisionamento de outras entidades do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="cbbcf-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="cbbcf-137">Você pode usar o [Módulo do PowerShell do Barramento de Serviço](/powershell/module/azurerm.servicebus) para provisionar outras entidades, como tópicos e assinaturas.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-137">You can use the [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) to provision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="cbbcf-138">Esses cmdlets são sintaticamente semelhantes aos cmdlets de criação de fila demonstrados na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-138">These cmdlets are syntactically similar to the queue creation cmdlets demonstrated in the previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbbcf-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cbbcf-139">Next steps</span></span>

- <span data-ttu-id="cbbcf-140">Consulte a documentação completa sobre o módulo do PowerShell do Resource Manager do Barramento de Serviço [aqui](/powershell/module/azurerm.servicebus).</span><span class="sxs-lookup"><span data-stu-id="cbbcf-140">See the complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="cbbcf-141">Esta página lista todos os cmdlets disponíveis.</span><span class="sxs-lookup"><span data-stu-id="cbbcf-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="cbbcf-142">Para obter informações sobre o uso de modelos do Azure Resource Manager, consulte o artigo [Criar recursos do Barramento de Serviço usando modelos do Azure Resource Manager](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cbbcf-142">For information about using Azure Resource Manager templates, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="cbbcf-143">Informações sobre [Bibliotecas de gerenciamento .NET do Barramento de Serviço](service-bus-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="cbbcf-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="cbbcf-144">Há algumas formas alternativas de gerenciar entidades do Barramento de Serviço, conforme descrito nessas postagens de blog:</span><span class="sxs-lookup"><span data-stu-id="cbbcf-144">There are some alternate ways to manage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="cbbcf-145">Como criar filas, tópicos e assinaturas do Barramento de Serviço usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbbcf-145">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="cbbcf-146">Como criar um namespace do Barramento de Serviço e um Hub de Eventos usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbbcf-146">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="cbbcf-147">Scripts do PowerShell do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="cbbcf-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
