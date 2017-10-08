---
title: aaaManage CDN do Azure com o PowerShell | Microsoft Docs
description: "Saiba como toouse Olá toomanage de cmdlets do PowerShell do Azure CDN do Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: fb6f57a5-6e26-4847-8fd9-b51fb05a79eb
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269373136d4ef018e4d31f147456b4be2253b463
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="88eea-103">Gerenciar a CDN do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="88eea-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="88eea-104">PowerShell fornece uma saudação mais flexível métodos toomanage os perfis de CDN do Azure e os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="88eea-104">PowerShell provides one of hello most flexible methods toomanage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="88eea-105">Você pode usar o PowerShell interativamente ou escrevendo scripts tooautomate tarefas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="88eea-105">You can use PowerShell interactively or by writing scripts tooautomate management tasks.</span></span>  <span data-ttu-id="88eea-106">Este tutorial demonstra várias das tarefas mais comuns de saudação pode ser realizadas com o PowerShell toomanage os perfis de CDN do Azure e os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="88eea-106">This tutorial demonstrates several of hello most common tasks you can accomplish with PowerShell toomanage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88eea-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="88eea-107">Prerequisites</span></span>
<span data-ttu-id="88eea-108">toouse PowerShell toomanage os perfis de CDN do Azure e os pontos de extremidade, você deve ter hello Azure PowerShell module instalada.</span><span class="sxs-lookup"><span data-stu-id="88eea-108">toouse PowerShell toomanage your Azure CDN profiles and endpoints, you must have hello Azure PowerShell module installed.</span></span>  <span data-ttu-id="88eea-109">toolearn como tooinstall PowerShell do Azure e conecte-se tooAzure usando Olá `Login-AzureRmAccount` cmdlet, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="88eea-109">toolearn how tooinstall Azure PowerShell and connect tooAzure using hello `Login-AzureRmAccount` cmdlet, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88eea-110">Você deve fazer logon com `Login-AzureRmAccount` antes de executar os cmdlets do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="88eea-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a><span data-ttu-id="88eea-111">Listando os cmdlets do Azure CDN Olá</span><span class="sxs-lookup"><span data-stu-id="88eea-111">Listing hello Azure CDN cmdlets</span></span>
<span data-ttu-id="88eea-112">Você pode listar todos os cmdlets do Azure CDN hello usando Olá `Get-Command` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="88eea-112">You can list all hello Azure CDN cmdlets using hello `Get-Command` cmdlet.</span></span>

```text
PS C:\> Get-Command -Module AzureRM.Cdn

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Get-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpointNameAvailability             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfileSsoUrl                        2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Publish-AzureRmCdnEndpointContent                  2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnCustomDomain                      2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnEndpoint                          2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnProfile                           2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Start-AzureRmCdnEndpoint                           2.0.0      AzureRm.Cdn
Cmdlet          Stop-AzureRmCdnEndpoint                            2.0.0      AzureRm.Cdn
Cmdlet          Test-AzureRmCdnCustomDomain                        2.0.0      AzureRm.Cdn
Cmdlet          Unpublish-AzureRmCdnEndpointContent                2.0.0      AzureRm.Cdn
```

## <a name="getting-help"></a><span data-ttu-id="88eea-113">Obtendo ajuda</span><span class="sxs-lookup"><span data-stu-id="88eea-113">Getting help</span></span>
<span data-ttu-id="88eea-114">Você pode obter ajuda com qualquer um desses cmdlets usando Olá `Get-Help` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="88eea-114">You can get help with any of these cmdlets using hello `Get-Help` cmdlet.</span></span>  <span data-ttu-id="88eea-115">`Get-Help` fornece o uso e a sintaxe, e opcionalmente mostra exemplos.</span><span class="sxs-lookup"><span data-stu-id="88eea-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

```text
PS C:\> Get-Help Get-AzureRmCdnProfile

NAME
    Get-AzureRmCdnProfile

SYNOPSIS
    Gets an Azure CDN profile.


SYNTAX
    Get-AzureRmCdnProfile [-ProfileName <String>] [-ResourceGroupName <String>] [-InformationAction
    <ActionPreference>] [-InformationVariable <String>] [<CommonParameters>]


DESCRIPTION
    Gets an Azure CDN profile and all related information.


RELATED LINKS

REMARKS
    toosee hello examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="88eea-116">Listando os perfis CDN do Azure existentes</span><span class="sxs-lookup"><span data-stu-id="88eea-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="88eea-117">Olá `Get-AzureRmCdnProfile` cmdlet sem parâmetros recupera todos os seus perfis CDN existentes.</span><span class="sxs-lookup"><span data-stu-id="88eea-117">hello `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="88eea-118">Essa saída pode ser toocmdlets indicada para enumeração.</span><span class="sxs-lookup"><span data-stu-id="88eea-118">This output can be piped toocmdlets for enumeration.</span></span>

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="88eea-119">Você também pode retornar um único perfil, especificando o grupo de recursos e o nome do perfil de saudação.</span><span class="sxs-lookup"><span data-stu-id="88eea-119">You can also return a single profile by specifying hello profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="88eea-120">É possível toohave CDN vários perfis com hello mesmo nome, desde que eles estão em diferentes grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="88eea-120">It is possible toohave multiple CDN profiles with hello same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="88eea-121">Omitir Olá `ResourceGroupName` parâmetro retorna todos os perfis com um nome correspondente.</span><span class="sxs-lookup"><span data-stu-id="88eea-121">Omitting hello `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="88eea-122">Listando os pontos de extremidade CDN existentes</span><span class="sxs-lookup"><span data-stu-id="88eea-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="88eea-123">`Get-AzureRmCdnEndpoint`pode recuperar um ponto de extremidade individual ou todos os pontos de extremidade de saudação em um perfil.</span><span class="sxs-lookup"><span data-stu-id="88eea-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all hello endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of hello endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of hello endpoints on all of hello profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of hello endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="88eea-124">Criando perfis e pontos de extremidade CDN</span><span class="sxs-lookup"><span data-stu-id="88eea-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="88eea-125">`New-AzureRmCdnProfile`e `New-AzureRmCdnEndpoint` são usadas toocreate CDN perfis e pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="88eea-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used toocreate CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="88eea-126">Verificando a disponibilidade do nome do ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="88eea-126">Checking endpoint name availability</span></span>
<span data-ttu-id="88eea-127">`Get-AzureRmCdnEndpointNameAvailability` retorna um objeto indicando se um nome do ponto de extremidade está disponível.</span><span class="sxs-lookup"><span data-stu-id="88eea-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="88eea-128">Adicionando um domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="88eea-128">Adding a custom domain</span></span>
<span data-ttu-id="88eea-129">`New-AzureRmCdnCustomDomain`Adiciona um domínio personalizado nome tooan ponto de extremidade existente.</span><span class="sxs-lookup"><span data-stu-id="88eea-129">`New-AzureRmCdnCustomDomain` adds a custom domain name tooan existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88eea-130">Você deve configurar Olá CNAME com seu provedor DNS conforme descrito em [como ponto de extremidade da rede de entrega (CDN) tooContent toomap domínio personalizado](cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="88eea-130">You must set up hello CNAME with your DNS provider as described in [How toomap Custom Domain tooContent Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="88eea-131">Você pode testar o mapeamento de saudação antes de modificar o ponto de extremidade usando `Test-AzureRmCdnCustomDomain`.</span><span class="sxs-lookup"><span data-stu-id="88eea-131">You can test hello mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check hello mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create hello custom domain on hello endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="88eea-132">Modificando um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="88eea-132">Modifying an endpoint</span></span>
<span data-ttu-id="88eea-133">`Set-AzureRmCdnEndpoint` modifica um ponto de extremidade existente.</span><span class="sxs-lookup"><span data-stu-id="88eea-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="88eea-134">Limpando/Pré-carregando ativos CDN</span><span class="sxs-lookup"><span data-stu-id="88eea-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="88eea-135">`Unpublish-AzureRmCdnEndpointContent` limpa ativos armazenados em cache enquanto `Publish-AzureRmCdnEndpointContent` pré-carrega os ativos nos pontos de extremidade com suporte.</span><span class="sxs-lookup"><span data-stu-id="88eea-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="88eea-136">Iniciando/Parando os pontos de extremidade CDN</span><span class="sxs-lookup"><span data-stu-id="88eea-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="88eea-137">`Start-AzureRmCdnEndpoint`e `Stop-AzureRmCdnEndpoint` podem ser usado toostart e interromper os pontos de extremidade individuais ou grupos de pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="88eea-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used toostart and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="88eea-138">Excluindo os recursos CDN</span><span class="sxs-lookup"><span data-stu-id="88eea-138">Deleting CDN resources</span></span>
<span data-ttu-id="88eea-139">`Remove-AzureRmCdnProfile`e `Remove-AzureRmCdnEndpoint` podem ser usados tooremove perfis e pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="88eea-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used tooremove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="88eea-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="88eea-140">Next Steps</span></span>
<span data-ttu-id="88eea-141">Saiba como tooautomate CDN do Azure com [.NET](cdn-app-dev-net.md) ou [Node.js](cdn-app-dev-node.md).</span><span class="sxs-lookup"><span data-stu-id="88eea-141">Learn how tooautomate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="88eea-142">toolearn sobre os recursos CDN, consulte [visão geral da CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="88eea-142">toolearn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>

