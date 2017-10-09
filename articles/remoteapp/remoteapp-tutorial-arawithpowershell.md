---
title: aaaUse cmdlets do PowerShell com o Azure RemoteApp | Microsoft Docs
description: Saiba como toouse cmdlets do Windows PowerShell no Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a>Usar os cmdlets do Windows PowerShell com o Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

 Você pode usar tooadminister de cmdlets do PowerShell do Azure RemoteApp hello e manter suas coleções. Use Olá tooget informações de Introdução a seguir.

## <a name="get-hello-cmdlets"></a>Obter Olá cmdlets
- - -
Baixe primeiro o cmdlets do Powershell do Azure Olá [aqui](http://go.microsoft.com/?linkid=9811175), Olá RemoteApp cmdlets são incluídos. 

Check-out Olá [ajuda de cmdlet do Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a>Configurar a sua assinatura toouse de cmdlets do Azure
- - -
Execute [neste guia](/powershell/azure/overview) , você pode usar os cmdlets de saudação em relação a sua assinatura do Azure.

Você pode usar esses tooget etapas iniciado rapidamente:

1. Baixe e instale Olá [cmdlets do PowerShell do Azure](http://go.microsoft.com/?linkid=9811175).
2. Inicie o Microsoft Azure PowerShell.
3. Executar **Add-AzureAccount** tooauthenticate tooyour assinatura do Azure. Quando solicitado, digite Olá o mesmo nome de usuário e senha que você use toosign no portal de tooAzure.  
4. Executar **Get-AzureSubscription** assinaturas de saudação toolist associadas à sua conta de usuário. 
5. Executar **Select-AzureSubscription - SubscriptionName &lt;nome da assinatura&gt;**  ou **Select-AzureSubscription - SubscriptionId &lt;ID da assinatura&gt;**  toospecify Olá assinatura toouse.

Parabéns, o console do PowerShell do Azure está configurado e pronto toouse. Lembre-se de que você precisará toorepeate etapas 2 a 5 cada vez que iniciar o console do hello hello Azure PowerShell.  


## <a name="list-all-collections"></a>Listar todas as coleções
- - -
     Get-AzureRemoteAppCollection

## <a name="delete-a-collection"></a>Excluir uma coleção
- - -
    Remove-AzureRemoteAppCollection <enter collection name>

Exemplo: `Remove-AzureRemoteAppCollection ContosoProduction`.

## <a name="create-a-cloud-collection"></a>Criar uma coleção na nuvem
- - -
É simple, execute Olá comando a seguir:

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

Olá acima comando publica automaticamente os aplicativos do Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio e Word).

Criação de coleção pode levar 30 minutos ou mais toocomplete. Portanto, este comando retorna uma ID de acompanhamento que pode ser usada da seguinte maneira:

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

Após a coleta de saudação é feita, você pode adicionar a coleção de toohello de usuários com hello comando a seguir:

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

E pronto! Esse usuário deve ser capaz de tooconnect toohello aplicativo usando o cliente do Azure RemoteApp Olá encontrado [aqui](https://www.remoteapp.windowsazure.com/).

## <a name="available-cmdlets"></a>Cmdlets disponíveis
Há muitos outros comandos que temos, documentação de saudação para eles estarão disponíveis em breve:

Cmdlets de coleção de RemoteApp básicos: 

* New-AzureRemoteAppCollection
* Get-AzureRemoteAppCollection
* Set-AzureRemoteAppCollection
* Update-AzureRemoteAppCollection
* Remove-AzureRemoteAppCollection
* Add-AzureRemoteAppUser
* Get-AzureRemoteAppUser
* Remove-AzureRemoteAppUser
* Get-AzureRemoteAppSession
* Disconnect-AzureRemoteAppSession
* Invoke-AzureRemoteAppSessionLogoff
* Send-AzureRemoteAppSessionMessage
* Get-AzureRemoteAppProgram
* Get-AzureRemoteAppStartMenuProgram
* Publish-AzureRemoteAppProgram
* Unpublish-AzureRemoteAppProgram
* Get-AzureRemoteAppCollectionUsageDetails
* Get-AzureRemoteAppCollectionUsageSummary
* Get-AzureRemoteAppPlan

Cmdlets da rede virtual do RemoteApp:

* New-AzureRemoteAppVNet
* Get-AzureRemoteAppVNet
* Set-AzureRemoteAppVNet
* Remove-AzureRemoteAppVNet
* Get-AzureRemoteAppVpnDevice
* Get-- AzureRemoteAppVpnDeviceConfigScript
* Reset-AzureRemoteAppVpnSharedKey

Cmdlets de imagem do modelo do RemoteApp:

* New-AzureRemoteAppTemplateImage
* Get-AzureRemoteAppTemplateImage
* Rename-AzureRemoteAppTemplateImage
* Remove-AzureRemoteAppTemplateImage

Outros cmdlets do RemoteApp:

* Get-AzureRemoteAppLocation
* Get-AzureRemoteAppWorkspace
* Set-AzureRemoteAppWorkspace
* Get-AzureRemoteAppOperationResult

