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
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a><span data-ttu-id="d8136-103">Use o PowerShell toocreate um toouse de aplicativo do AD do Azure com hello API de serviços de mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="d8136-103">Use PowerShell toocreate an Azure AD app toouse with hello Azure Media Services API</span></span>

<span data-ttu-id="d8136-104">Saiba como toouse um PowerShell script toocreate um aplicativo do Azure Active Directory (AD do Azure) e o serviço principal tooaccess recursos dos serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8136-104">Learn how toouse a PowerShell script toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="d8136-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d8136-105">Prerequisites</span></span>

- <span data-ttu-id="d8136-106">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8136-106">An Azure account.</span></span> <span data-ttu-id="d8136-107">Se você não tiver uma conta, comece com uma [avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8136-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="d8136-108">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="d8136-108">A Media Services account.</span></span> <span data-ttu-id="d8136-109">Para obter mais informações, consulte [criar uma conta de serviços de mídia do Azure no portal do Azure de saudação](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d8136-109">For more information, see [Create an Azure Media Services account in hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="d8136-110">Azure PowerShell versão 0.8.8 ou uma versão posterior.</span><span class="sxs-lookup"><span data-stu-id="d8136-110">Azure PowerShell version 0.8.8 or a later version.</span></span> <span data-ttu-id="d8136-111">Para obter mais informações, consulte [como toouse do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d8136-111">For more information, see [How toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
- <span data-ttu-id="d8136-112">Cmdlets do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d8136-112">Azure Resource Manager cmdlets.</span></span>  

## <a name="create-an-azure-ad-app-by-using-powershell"></a><span data-ttu-id="d8136-113">Criar um aplicativo do Azure AD usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8136-113">Create an Azure AD app by using PowerShell</span></span>  

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

<span data-ttu-id="d8136-114">Para obter mais informações, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8136-114">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="d8136-115">Usar Azure PowerShell toocreate um serviço principal tooaccess recursos</span><span class="sxs-lookup"><span data-stu-id="d8136-115">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [<span data-ttu-id="d8136-116">Gerenciar o Controle de Acesso Baseado em Função usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8136-116">Manage Role-Based Access Control by using Azure PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
- [<span data-ttu-id="d8136-117">Como toomanually configura o daemon aplicativos usando certificados</span><span class="sxs-lookup"><span data-stu-id="d8136-117">How toomanually configure daemon apps by using certificates</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a><span data-ttu-id="d8136-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8136-118">Next steps</span></span>

<span data-ttu-id="d8136-119">Introdução ao [carregando arquivos tooyour conta](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="d8136-119">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
