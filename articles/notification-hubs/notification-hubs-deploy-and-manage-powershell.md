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
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a>Implantar e gerenciar os Hubs de Notificação usando o PowerShell
## <a name="overview"></a>Visão geral
Este artigo mostra como criar toouse e Hubs de notificação de Azure gerenciar usando o PowerShell. Olá tarefas comuns de automação a seguir é mostrada neste tópico.

* Criar um hub de notificação
* Definir credenciais

Se você também precisará toocreate um novo namespace de barramento de serviço para seus hubs de notificação, consulte [gerenciar o barramento de serviço com o PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).

Não há suporte para o gerenciamento de Hubs de notificações diretamente pelo Olá cmdlets incluídos com o Azure PowerShell. Olá melhor abordagem do PowerShell é o assembly de Microsoft.Azure.NotificationHubs.dll Olá tooreference. assembly Hello é distribuído com hello [pacote NuGet de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este artigo, você deve ter o seguinte hello:

* Uma assinatura do Azure. O Azure é uma plataforma baseada em assinatura. Para saber mais sobre como adquirir uma assinatura, confira [Opções de compra], [Ofertas para membros] ou [Teste Gratuito].
* Um computador com o PowerShell do Azure. Para obter instruções, consulte [Instalar e configurar o PowerShell do Azure].
* Uma compreensão geral dos scripts do PowerShell, pacotes do NuGet e saudação do .NET Framework.

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a>Incluindo uma referência toohello .NET assembly para o barramento de serviço
Gerenciamento de Hubs de notificação do Azure ainda não está incluído com hello cmdlets do PowerShell no Azure PowerShell. tooprovision hubs de notificação, você pode usar o cliente .NET de saudação fornecido no hello [pacote NuGet de Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Primeiro, verifique se o script pode localizar Olá **Microsoft.Azure.NotificationHubs.dll** assembly, que é instalado como um pacote do NuGet em um projeto do Visual Studio. Toobe ordem flexível, script hello executa estas etapas:

1. Determina o caminho de saudação em que ele foi invocado.
2. Percorre Olá caminho até encontrar uma pasta chamada `packages`. Esta pasta é criada quando você instala pacotes NuGet para projetos do Visual Studio.
3. Saudação de pesquisa recursivamente `packages` pasta para um assembly chamado **Microsoft.Azure.NotificationHubs.dll**.
4. Referências Olá assembly para que tipos de saudação estão disponíveis para uso posterior.

Aqui está como essas etapas são implementadas em um script do PowerShell:

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

## <a name="create-hello-namespacemanager-class"></a>Criar a classe do Gerenciador de namespace Olá
tooprovision Hubs de notificação, crie uma instância da saudação [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) classe da saudação SDK. 

Você pode usar o hello [AzureSBAuthorizationRule Get] cmdlet incluído com o Azure PowerShell tooretrieve uma regra de autorização que usou tooprovide uma cadeia de caracteres de conexão. Podemos armazenar uma referência toohello `NamespaceManager` instância no hello `$NamespaceManager` variável. Usaremos `$NamespaceManager` tooprovision um hub de notificação.

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a>Provisionando um novo hub de notificação
tooprovision um novo hub de notificação, use Olá [API .NET para Hubs de notificação].

Nesta parte do script hello configurar quatro variáveis locais. 

1. `$Namespace`: Defina esse toohello nome do namespace Olá onde você deseja toocreate um hub de notificação.
2. `$Path`: Defina esse nome de toohello do caminho do novo hub de notificação hello.  Por exemplo, "MyHub".    
3. `$WnsPackageSid`: Defina esse SID do pacote toohello para que o aplicativo do Windows da saudação [Centro de desenvolvimento do Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).
4. `$WnsSecretkey`: Defina essa chave secreta toohello para que o aplicativo do Windows da saudação [Centro de desenvolvimento do Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).

Essas variáveis são usadas tooconnect tooyour namespace e criar um novo toohandle de Hub de notificação configurado notificações de serviços de notificação do Windows (WNS) com as credenciais do WNS para um aplicativo do Windows. Para obter informações sobre como obter Olá pacote SID e consulte a chave secreta, hello [Introdução aos Hubs de notificação](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial. 

* trecho de código de script Hello usa Olá `NamespaceManager` toocheck toosee do objeto se Olá Hub de notificação identificado por `$Path` existe.
* Se não existir, o script hello criará uma `NotificationHubDescription` com WNS credenciais e passar essa toohello `NamespaceManager` classe `CreateNotificationHub` método.

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




## <a name="additional-resources"></a>Recursos adicionais
* [Gerenciar o Barramento de Serviço com o PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [Como toocreate Service Bus filas, tópicos e assinaturas usando um script do PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [Como toocreate um Namespace de barramento de serviço e um Hub de eventos usando um script do PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

Alguns scripts prontos também estão disponíveis para download:

* [Scripts do PowerShell do Barramento de Serviço](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[Opções de compra]: http://azure.microsoft.com/pricing/purchase-options/
[Ofertas para membros]: http://azure.microsoft.com/pricing/member-offers/
[Teste Gratuito]: http://azure.microsoft.com/pricing/free-trial/
[Instalar e configurar o PowerShell do Azure]: /powershell/azureps-cmdlets-docs
[API .NET para Hubs de notificação]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[AzureSBAuthorizationRule Get]: https://msdn.microsoft.com/library/azure/dn495113.aspx

