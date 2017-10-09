---
title: "aaaUse PowerShell toocreate um tooaccess de aplicativo do AD do Azure Olá API de serviços de mídia do Azure | Microsoft Docs"
description: "Saiba como toouse PowerShell toocreate um aplicativo do Azure Active Directory (AD do Azure) e configurá-lo tooaccess Olá API de serviços de mídia do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 1a8b4a53ad10b559f6ee4242b95c5bd15ee8e903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a>Use o PowerShell toocreate um toouse de aplicativo do AD do Azure com hello API de serviços de mídia do Azure

Saiba como toouse um PowerShell script toocreate um aplicativo do Azure Active Directory (AD do Azure) e o serviço principal tooaccess recursos dos serviços de mídia do Azure.  

## <a name="prerequisites"></a>Pré-requisitos

- Uma conta do Azure. Se você não tiver uma conta, comece com uma [avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Uma conta dos Serviços de Mídia. Para obter mais informações, consulte [criar uma conta de serviços de mídia do Azure no portal do Azure de saudação](media-services-portal-create-account.md).
- Azure PowerShell versão 0.8.8 ou uma versão posterior. Para obter mais informações, consulte [como toouse do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
- Cmdlets do Azure Resource Manager.  

## <a name="create-an-azure-ad-app-by-using-powershell"></a>Criar um aplicativo do Azure AD usando o PowerShell  

```powershell
Login-AzureRmAccount
Import-Module AzureRM.Resources
Set-AzureRmContext -SubscriptionId $SubscriptionId
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password

Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 
$NewRole = $null
$Scope = "/subscriptions/your subscription id/resourceGroups/userresourcegroup/providers/microsoft.media/mediaservices/your media account"

$Retries = 0;While ($NewRole -eq $null -and $Retries -le 6)
{
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

Para obter mais informações, consulte Olá artigos a seguir:

- [Usar Azure PowerShell toocreate um serviço principal tooaccess recursos](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [Gerenciar o Controle de Acesso Baseado em Função usando o Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
- [Como toomanually configura o daemon aplicativos usando certificados](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a>Próximas etapas

Introdução ao [carregando arquivos tooyour conta](media-services-portal-upload-files.md).
