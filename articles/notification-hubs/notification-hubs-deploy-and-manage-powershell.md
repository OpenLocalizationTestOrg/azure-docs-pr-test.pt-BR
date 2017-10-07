---
title: "aaaDeploy e gerenciar os Hubs de notificação usando o PowerShell"
description: "Como tooCreate e gerenciar notificação Hubs usando o PowerShell para automação"
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
ms.openlocfilehash: 8835bdefa0d360354263eab8040259ad08281771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="ddfb1-103">Implantar e gerenciar os Hubs de Notificação usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ddfb1-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="ddfb1-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ddfb1-104">Overview</span></span>
<span data-ttu-id="ddfb1-105">Este artigo mostra como criar toouse e Hubs de notificação de Azure gerenciar usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-105">This article shows you how toouse Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="ddfb1-106">Olá tarefas comuns de automação a seguir é mostrada neste tópico.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-106">hello following common automation tasks are shown in this topic.</span></span>

* <span data-ttu-id="ddfb1-107">Criar um hub de notificação</span><span class="sxs-lookup"><span data-stu-id="ddfb1-107">Create a Notification Hub</span></span>
* <span data-ttu-id="ddfb1-108">Definir credenciais</span><span class="sxs-lookup"><span data-stu-id="ddfb1-108">Set Credentials</span></span>

<span data-ttu-id="ddfb1-109">Se você também precisará toocreate um novo namespace de barramento de serviço para seus hubs de notificação, consulte [gerenciar o barramento de serviço com o PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span><span class="sxs-lookup"><span data-stu-id="ddfb1-109">If you also need toocreate a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="ddfb1-110">Não há suporte para o gerenciamento de Hubs de notificações diretamente pelo Olá cmdlets incluídos com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-110">Managing Notifications Hubs is not supported directly by hello cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="ddfb1-111">Olá melhor abordagem do PowerShell é o assembly de Microsoft.Azure.NotificationHubs.dll Olá tooreference.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-111">hello best approach from PowerShell is tooreference hello Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="ddfb1-112">assembly Hello é distribuído com hello [pacote NuGet de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="ddfb1-112">hello assembly is distributed with hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddfb1-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ddfb1-113">Prerequisites</span></span>
<span data-ttu-id="ddfb1-114">Antes de começar este artigo, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="ddfb1-114">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="ddfb1-115">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-115">An Azure subscription.</span></span> <span data-ttu-id="ddfb1-116">O Azure é uma plataforma baseada em assinatura.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-116">Azure is a subscription-based platform.</span></span> <span data-ttu-id="ddfb1-117">Para saber mais sobre como adquirir uma assinatura, confira [Opções de compra], [Ofertas para membros] ou [Teste Gratuito].</span><span class="sxs-lookup"><span data-stu-id="ddfb1-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="ddfb1-118">Um computador com o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-118">A computer with Azure PowerShell.</span></span> <span data-ttu-id="ddfb1-119">Para obter instruções, consulte [Instalar e configurar o PowerShell do Azure].</span><span class="sxs-lookup"><span data-stu-id="ddfb1-119">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="ddfb1-120">Uma compreensão geral dos scripts do PowerShell, pacotes do NuGet e saudação do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-120">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a><span data-ttu-id="ddfb1-121">Incluindo uma referência toohello .NET assembly para o barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="ddfb1-121">Including a reference toohello .NET assembly for Service Bus</span></span>
<span data-ttu-id="ddfb1-122">Gerenciamento de Hubs de notificação do Azure ainda não está incluído com hello cmdlets do PowerShell no Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-122">Managing Azure Notification Hubs is not yet included with hello PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="ddfb1-123">tooprovision hubs de notificação, você pode usar o cliente .NET de saudação fornecido no hello [pacote NuGet de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="ddfb1-123">tooprovision notification hubs, you can use hello .NET client provided in hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="ddfb1-124">Primeiro, verifique se o script pode localizar Olá **Microsoft.Azure.NotificationHubs.dll** assembly, que é instalado como um pacote do NuGet em um projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-124">First, make sure your script can locate hello **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="ddfb1-125">Toobe ordem flexível, script hello executa estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ddfb1-125">In order toobe flexible, hello script performs these steps:</span></span>

1. <span data-ttu-id="ddfb1-126">Determina o caminho de saudação em que ele foi invocado.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-126">Determines hello path at which it was invoked.</span></span>
2. <span data-ttu-id="ddfb1-127">Percorre Olá caminho até encontrar uma pasta chamada `packages`.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-127">Traverses hello path until it finds a folder named `packages`.</span></span> <span data-ttu-id="ddfb1-128">Esta pasta é criada quando você instala pacotes NuGet para projetos do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-128">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="ddfb1-129">Saudação de pesquisa recursivamente `packages` pasta para um assembly chamado **Microsoft.Azure.NotificationHubs.dll**.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-129">Recursively searches hello `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="ddfb1-130">Referências Olá assembly para que tipos de saudação estão disponíveis para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-130">References hello assembly so that hello types are available for later use.</span></span>

<span data-ttu-id="ddfb1-131">Aqui está como essas etapas são implementadas em um script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ddfb1-131">Here's how these steps are implemented in a PowerShell script:</span></span>

``` powershell

try
{
    # WARNING: Make sure tooreference hello latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding hello [Microsoft.Azure.NotificationHubs.dll] assembly toohello script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "hello [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added toohello script."
}

catch [System.Exception]
{
    Write-Error("Could not add hello Microsoft.Azure.NotificationHubs.dll assembly toohello script. Make sure you build hello solution before running hello provisioning script.")
}
```

## <a name="create-hello-namespacemanager-class"></a><span data-ttu-id="ddfb1-132">Criar a classe do Gerenciador de namespace Olá</span><span class="sxs-lookup"><span data-stu-id="ddfb1-132">Create hello NamespaceManager class</span></span>
<span data-ttu-id="ddfb1-133">tooprovision Hubs de notificação, crie uma instância da saudação [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) classe da saudação SDK.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-133">tooprovision Notification Hubs, create an instance of hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from hello SDK.</span></span> 

<span data-ttu-id="ddfb1-134">Você pode usar o hello [AzureSBAuthorizationRule Get] cmdlet incluído com o Azure PowerShell tooretrieve uma regra de autorização que usou tooprovide uma cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-134">You can use hello [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell tooretrieve an authorization rule that's used tooprovide a connection string.</span></span> <span data-ttu-id="ddfb1-135">Podemos armazenar uma referência toohello `NamespaceManager` instância no hello `$NamespaceManager` variável.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-135">We'll store a reference toohello `NamespaceManager` instance in hello `$NamespaceManager` variable.</span></span> <span data-ttu-id="ddfb1-136">Usaremos `$NamespaceManager` tooprovision um hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-136">We will use `$NamespaceManager` tooprovision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="ddfb1-137">Provisionando um novo hub de notificação</span><span class="sxs-lookup"><span data-stu-id="ddfb1-137">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="ddfb1-138">tooprovision um novo hub de notificação, use Olá [API .NET para Hubs de notificação].</span><span class="sxs-lookup"><span data-stu-id="ddfb1-138">tooprovision a new notification hub, use hello [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="ddfb1-139">Nesta parte do script hello configurar quatro variáveis locais.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-139">In this part of hello script you set up four local variables.</span></span> 

1. <span data-ttu-id="ddfb1-140">`$Namespace`: Defina esse toohello nome do namespace Olá onde você deseja toocreate um hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-140">`$Namespace` : Set this toohello name of hello namespace where you want toocreate a notification hub.</span></span>
2. <span data-ttu-id="ddfb1-141">`$Path`: Defina esse nome de toohello do caminho do novo hub de notificação hello.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-141">`$Path` : Set this path toohello name of hello new notification hub.</span></span>  <span data-ttu-id="ddfb1-142">Por exemplo, "MyHub".</span><span class="sxs-lookup"><span data-stu-id="ddfb1-142">For example, "MyHub".</span></span>    
3. <span data-ttu-id="ddfb1-143">`$WnsPackageSid`: Defina esse SID do pacote toohello para que o aplicativo do Windows da saudação [Centro de desenvolvimento do Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="ddfb1-143">`$WnsPackageSid` : Set this toohello package SID for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>
4. <span data-ttu-id="ddfb1-144">`$WnsSecretkey`: Defina essa chave secreta toohello para que o aplicativo do Windows da saudação [Centro de desenvolvimento do Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="ddfb1-144">`$WnsSecretkey`: Set this toohello secret key for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>

<span data-ttu-id="ddfb1-145">Essas variáveis são usadas tooconnect tooyour namespace e criar um novo toohandle de Hub de notificação configurado notificações de serviços de notificação do Windows (WNS) com as credenciais do WNS para um aplicativo do Windows.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-145">These variables are used tooconnect tooyour namespace and create a new Notification Hub configured toohandle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="ddfb1-146">Para obter informações sobre como obter Olá pacote SID e consulte a chave secreta, hello [Introdução aos Hubs de notificação](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-146">For information on obtaining hello package SID and secret key see, hello [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="ddfb1-147">trecho de código de script Hello usa Olá `NamespaceManager` toocheck toosee do objeto se Olá Hub de notificação identificado por `$Path` existe.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-147">hello script snippet uses hello `NamespaceManager` object toocheck toosee if hello Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="ddfb1-148">Se não existir, o script hello criará uma `NotificationHubDescription` com WNS credenciais e passar essa toohello `NamespaceManager` classe `CreateNotificationHub` método.</span><span class="sxs-lookup"><span data-stu-id="ddfb1-148">If it does not exist, hello script will create an `NotificationHubDescription` with WNS credentials and pass that toohello `NamespaceManager` class `CreateNotificationHub` method.</span></span>

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query hello namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if hello namespace already exists
if ($CurrentNamespace)
{
    Write-Output "hello namespace [$Namespace] in hello [$($CurrentNamespace.Region)] region was found."

    # Create hello NamespaceManager object used toocreate a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."

    # Check toosee if hello Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "hello [$Path] notification hub already exists in hello [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating hello [$Path] notification hub in hello [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "hello [$Path] notification hub was created in hello [$Namespace] namespace."
    }
}
else
{
    Write-Host "hello [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a><span data-ttu-id="ddfb1-149">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ddfb1-149">Additional Resources</span></span>
* [<span data-ttu-id="ddfb1-150">Gerenciar o Barramento de Serviço com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ddfb1-150">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="ddfb1-151">Como toocreate Service Bus filas, tópicos e assinaturas usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="ddfb1-151">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="ddfb1-152">Como toocreate um Namespace de barramento de serviço e um Hub de eventos usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="ddfb1-152">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="ddfb1-153">Alguns scripts prontos também estão disponíveis para download:</span><span class="sxs-lookup"><span data-stu-id="ddfb1-153">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="ddfb1-154">Scripts do PowerShell do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="ddfb1-154">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[Opções de compra]: http://azure.microsoft.com/pricing/purchase-options/
[Ofertas para membros]: http://azure.microsoft.com/pricing/member-offers/
[Teste Gratuito]: http://azure.microsoft.com/pricing/free-trial/
[Instalar e configurar o PowerShell do Azure]: /powershell/azureps-cmdlets-docs
[API .NET para Hubs de notificação]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[AzureSBAuthorizationRule Get]: https://msdn.microsoft.com/library/azure/dn495113.aspx

