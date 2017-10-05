---
title: "Implantar e gerenciar os Hubs de Notificação usando o PowerShell"
description: "Como criar e gerenciar os hubs de notificação usando o PowerShell para automação"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 7c58f2c8-0399-42bc-9e1e-a7f073426451
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 4db058e4bd91dc287b14e887abc6c378c65c4a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="6ce0d-103">Implantar e gerenciar os Hubs de Notificação usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ce0d-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="6ce0d-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6ce0d-104">Overview</span></span>
<span data-ttu-id="6ce0d-105">Este artigo mostra como usar Criar e Gerenciar Hubs de Notificação de Azure usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-105">This article shows you how to use Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="6ce0d-106">As tarefas de automação comuns a seguir são mostradas neste tópico.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-106">The following common automation tasks are shown in this topic.</span></span>

* <span data-ttu-id="6ce0d-107">Criar um hub de notificação</span><span class="sxs-lookup"><span data-stu-id="6ce0d-107">Create a Notification Hub</span></span>
* <span data-ttu-id="6ce0d-108">Definir credenciais</span><span class="sxs-lookup"><span data-stu-id="6ce0d-108">Set Credentials</span></span>

<span data-ttu-id="6ce0d-109">Se você também precisar criar um novo namespace de barramento de serviço para os hubs de notificação, confira [Gerenciar o Barramento de Serviço com o PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span><span class="sxs-lookup"><span data-stu-id="6ce0d-109">If you also need to create a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="6ce0d-110">O gerenciamento de hubs de notificação não tem suporte direto dos cmdlets incluídos com o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-110">Managing Notifications Hubs is not supported directly by the cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="6ce0d-111">A melhor abordagem do PowerShell e fazer referência ao assembly Microsoft.Azure.NotificationHubs.dll.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-111">The best approach from PowerShell is to reference the Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="6ce0d-112">O assembly é distribuído com o [pacote NuGet de Hubs de Notificações do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="6ce0d-112">The assembly is distributed with the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ce0d-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6ce0d-113">Prerequisites</span></span>
<span data-ttu-id="6ce0d-114">Antes de começar este artigo, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6ce0d-114">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="6ce0d-115">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-115">An Azure subscription.</span></span> <span data-ttu-id="6ce0d-116">O Azure é uma plataforma baseada em assinatura.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-116">Azure is a subscription-based platform.</span></span> <span data-ttu-id="6ce0d-117">Para saber mais sobre como adquirir uma assinatura, confira [Opções de compra], [Ofertas para membros] ou [Teste Gratuito].</span><span class="sxs-lookup"><span data-stu-id="6ce0d-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="6ce0d-118">Um computador com o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-118">A computer with Azure PowerShell.</span></span> <span data-ttu-id="6ce0d-119">Para obter instruções, consulte [Instalar e configurar o PowerShell do Azure].</span><span class="sxs-lookup"><span data-stu-id="6ce0d-119">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="6ce0d-120">Um entendimento geral dos scripts do PowerShell, dos pacotes NuGet e do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-120">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="including-a-reference-to-the-net-assembly-for-service-bus"></a><span data-ttu-id="6ce0d-121">Incluindo uma referência ao assembly .NET para o Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="6ce0d-121">Including a reference to the .NET assembly for Service Bus</span></span>
<span data-ttu-id="6ce0d-122">O gerenciamento de hubs de notificação do Azure ainda não está incluído com os cmdlets do PowerShell no PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-122">Managing Azure Notification Hubs is not yet included with the PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="6ce0d-123">Para provisionar hubs de notificação, você pode usar o cliente .NET fornecido a [pacote NuGet de Hubs de Notificações do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="6ce0d-123">To provision notification hubs, you can use the .NET client provided in the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="6ce0d-124">Primeiro, verifique se o seu script pode localizar o assembly **Microsoft.Azure.NotificationHubs.dll** , que é instalado como um pacote do NuGet em um projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-124">First, make sure your script can locate the **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="6ce0d-125">Para que seja flexível, o script executa estas etapas:</span><span class="sxs-lookup"><span data-stu-id="6ce0d-125">In order to be flexible, the script performs these steps:</span></span>

1. <span data-ttu-id="6ce0d-126">Determina o caminho no qual ele foi invocado.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-126">Determines the path at which it was invoked.</span></span>
2. <span data-ttu-id="6ce0d-127">Percorre o caminho até encontrar uma pasta denominada `packages`.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-127">Traverses the path until it finds a folder named `packages`.</span></span> <span data-ttu-id="6ce0d-128">Esta pasta é criada quando você instala pacotes NuGet para projetos do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-128">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="6ce0d-129">Pesquisa recursivamente a pasta `packages` para um assembly denominado **Microsoft.Azure.NotificationHubs.dll**.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-129">Recursively searches the `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="6ce0d-130">Faz referência ao assembly para que os tipos estejam disponíveis para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-130">References the assembly so that the types are available for later use.</span></span>

<span data-ttu-id="6ce0d-131">Aqui está como essas etapas são implementadas em um script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6ce0d-131">Here's how these steps are implemented in a PowerShell script:</span></span>

``` powershell

try
{
    # WARNING: Make sure to reference the latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding the [Microsoft.Azure.NotificationHubs.dll] assembly to the script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "The [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added to the script."
}

catch [System.Exception]
{
    Write-Error("Could not add the Microsoft.Azure.NotificationHubs.dll assembly to the script. Make sure you build the solution before running the provisioning script.")
}
```

## <a name="create-the-namespacemanager-class"></a><span data-ttu-id="6ce0d-132">Criar a classe NamespaceManager</span><span class="sxs-lookup"><span data-stu-id="6ce0d-132">Create the NamespaceManager class</span></span>
<span data-ttu-id="6ce0d-133">Para provisionar os Hubs de Notificação, crie uma instância da classe [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) do SDK.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-133">To provision Notification Hubs, create an instance of the [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from the SDK.</span></span> 

<span data-ttu-id="6ce0d-134">Você pode usar o cmdlet [Get-AzureSBAuthorizationRule] incluído com o PowerShell do Azure para recuperar uma regra de autorização que é usada para fornecer uma cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-134">You can use the [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell to retrieve an authorization rule that's used to provide a connection string.</span></span> <span data-ttu-id="6ce0d-135">Armazenaremos uma referência para a instância `NamespaceManager` na variável `$NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-135">We'll store a reference to the `NamespaceManager` instance in the `$NamespaceManager` variable.</span></span> <span data-ttu-id="6ce0d-136">Vamos usar `$NamespaceManager` para provisionar um hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-136">We will use `$NamespaceManager` to provision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create the NamespaceManager object to create the hub
Write-Output "Creating a NamespaceManager object for the [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for the [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="6ce0d-137">Provisionando um novo hub de notificação</span><span class="sxs-lookup"><span data-stu-id="6ce0d-137">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="6ce0d-138">Para provisionar um novo Hub de Notificação, use a [API do .NET para Hubs de Notificação].</span><span class="sxs-lookup"><span data-stu-id="6ce0d-138">To provision a new notification hub, use the [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="6ce0d-139">Nesta parte do script, você configura quatro variáveis locais.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-139">In this part of the script you set up four local variables.</span></span> 

1. <span data-ttu-id="6ce0d-140">`$Namespace` : defina isso para o nome do namespace em que você deseja criar um hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-140">`$Namespace` : Set this to the name of the namespace where you want to create a notification hub.</span></span>
2. <span data-ttu-id="6ce0d-141">`$Path` : defina esse caminho para o nome do novo hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-141">`$Path` : Set this path to the name of the new notification hub.</span></span>  <span data-ttu-id="6ce0d-142">Por exemplo, "MyHub".</span><span class="sxs-lookup"><span data-stu-id="6ce0d-142">For example, "MyHub".</span></span>    
3. <span data-ttu-id="6ce0d-143">`$WnsPackageSid` : defina isso para o SID do pacote para seu aplicativo do Windows do [Centro de Desenvolvimento do Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="6ce0d-143">`$WnsPackageSid` : Set this to the package SID for you Windows App from the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>
4. <span data-ttu-id="6ce0d-144">`$WnsSecretkey`: defina isso para a chave secreta para seu aplicativo do Windows do [Centro de Desenvolvimento do Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="6ce0d-144">`$WnsSecretkey`: Set this to the secret key for you Windows App from the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>

<span data-ttu-id="6ce0d-145">Essas variáveis são usadas para se conectar ao seu namespace e criar um novo hub de notificação configurado para manipular as notificações do WNS (Windows Notification Services) com credenciais dos WNS para um aplicativo do Windows.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-145">These variables are used to connect to your namespace and create a new Notification Hub configured to handle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="6ce0d-146">Para obter informações sobre como obter o SID de pacote e a chave de segredo, consulte o tutorial [Introdução aos Hubs de Notificação](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="6ce0d-146">For information on obtaining the package SID and secret key see, the [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="6ce0d-147">O trecho de script usa o objeto `NamespaceManager` para verificar se o Hub de Notificação identificado pelo `$Path` existe.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-147">The script snippet uses the `NamespaceManager` object to check to see if the Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="6ce0d-148">Se não existir, o script criará um `NotificationHubDescription` com as credenciais do WNS e o passará à classe `NamespaceManager`, método `CreateNotificationHub`.</span><span class="sxs-lookup"><span data-stu-id="6ce0d-148">If it does not exist, the script will create an `NotificationHubDescription` with WNS credentials and pass that to the `NamespaceManager` class `CreateNotificationHub` method.</span></span>

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query the namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if the namespace already exists
if ($CurrentNamespace)
{
    Write-Output "The namespace [$Namespace] in the [$($CurrentNamespace.Region)] region was found."

    # Create the NamespaceManager object used to create a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for the [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for the [$Namespace] namespace has been successfully created."

    # Check to see if the Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "The [$Path] notification hub already exists in the [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating the [$Path] notification hub in the [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "The [$Path] notification hub was created in the [$Namespace] namespace."
    }
}
else
{
    Write-Host "The [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a><span data-ttu-id="6ce0d-149">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6ce0d-149">Additional Resources</span></span>
* [<span data-ttu-id="6ce0d-150">Gerenciar o Barramento de Serviço com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ce0d-150">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="6ce0d-151">Como criar filas, tópicos e assinaturas do Barramento de Serviço usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ce0d-151">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="6ce0d-152">Como criar um namespace do Barramento de Serviço e um Hub de Eventos usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ce0d-152">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="6ce0d-153">Alguns scripts prontos também estão disponíveis para download:</span><span class="sxs-lookup"><span data-stu-id="6ce0d-153">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="6ce0d-154">Scripts do PowerShell do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="6ce0d-154">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

<span data-ttu-id="6ce0d-155">[Opções de compra]: http://azure.microsoft.com/pricing/purchase-options/</span><span class="sxs-lookup"><span data-stu-id="6ce0d-155">[Purchase Options]: http://azure.microsoft.com/pricing/purchase-options/</span></span>
<span data-ttu-id="6ce0d-156">[Ofertas para membros]: http://azure.microsoft.com/pricing/member-offers/</span><span class="sxs-lookup"><span data-stu-id="6ce0d-156">[Member Offers]: http://azure.microsoft.com/pricing/member-offers/</span></span>
<span data-ttu-id="6ce0d-157">[Teste Gratuito]: http://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="6ce0d-157">[Free Trial]: http://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="6ce0d-158">[Instalar e configurar o PowerShell do Azure]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="6ce0d-158">[Install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="6ce0d-159">[API do .NET para Hubs de Notificação]: https://msdn.microsoft.com/library/azure/mt414893.aspx</span><span class="sxs-lookup"><span data-stu-id="6ce0d-159">[.NET API for Notification Hubs]: https://msdn.microsoft.com/library/azure/mt414893.aspx</span></span>
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
<span data-ttu-id="6ce0d-160">[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx</span><span class="sxs-lookup"><span data-stu-id="6ce0d-160">[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx</span></span>

