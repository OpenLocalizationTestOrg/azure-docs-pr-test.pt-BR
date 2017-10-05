---
title: Gerenciar a CDN do Azure com o PowerShell | Microsoft Docs
description: Saiba como usar os cmdlets do Azure PowerShell para gerenciar a CDN do Azure.
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
ms.openlocfilehash: 5bd2eed7b34cafa43e8f38279890405d4ae55568
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="9fda0-103">Gerenciar a CDN do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fda0-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="9fda0-104">O PowerShell fornece um dos métodos mais flexíveis para gerenciar os perfis e os pontos de extremidade de CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="9fda0-104">PowerShell provides one of the most flexible methods to manage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="9fda0-105">Você pode usar o PowerShell interativamente ou escrevendo scripts para automatizar as tarefas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="9fda0-105">You can use PowerShell interactively or by writing scripts to automate management tasks.</span></span>  <span data-ttu-id="9fda0-106">Este tutorial demonstra várias tarefas mais comuns que você pode fazer com o PowerShell para gerenciar os perfis e os pontos de extremidade de CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="9fda0-106">This tutorial demonstrates several of the most common tasks you can accomplish with PowerShell to manage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fda0-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9fda0-107">Prerequisites</span></span>
<span data-ttu-id="9fda0-108">Para usar o PowerShell para gerenciar os perfis e os pontos de extremidade de CDN do Azure, você deve ter o módulo do Azure PowerShell instalado.</span><span class="sxs-lookup"><span data-stu-id="9fda0-108">To use PowerShell to manage your Azure CDN profiles and endpoints, you must have the Azure PowerShell module installed.</span></span>  <span data-ttu-id="9fda0-109">Para aprender a instalar o Azure PowerShell e conectar o Azure usando o cmdlet `Login-AzureRmAccount` , consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9fda0-109">To learn how to install Azure PowerShell and connect to Azure using the `Login-AzureRmAccount` cmdlet, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fda0-110">Você deve fazer logon com `Login-AzureRmAccount` antes de executar os cmdlets do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9fda0-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-the-azure-cdn-cmdlets"></a><span data-ttu-id="9fda0-111">Listando os cmdlets de CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="9fda0-111">Listing the Azure CDN cmdlets</span></span>
<span data-ttu-id="9fda0-112">Você pode listar todos os cmdlets de CDN do Azure usando o cmdlet `Get-Command` .</span><span class="sxs-lookup"><span data-stu-id="9fda0-112">You can list all the Azure CDN cmdlets using the `Get-Command` cmdlet.</span></span>

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

## <a name="getting-help"></a><span data-ttu-id="9fda0-113">Obtendo ajuda</span><span class="sxs-lookup"><span data-stu-id="9fda0-113">Getting help</span></span>
<span data-ttu-id="9fda0-114">Você pode obter ajuda com qualquer um desses cmdlets usando o cmdlet `Get-Help` .</span><span class="sxs-lookup"><span data-stu-id="9fda0-114">You can get help with any of these cmdlets using the `Get-Help` cmdlet.</span></span>  <span data-ttu-id="9fda0-115">`Get-Help` fornece o uso e a sintaxe, e opcionalmente mostra exemplos.</span><span class="sxs-lookup"><span data-stu-id="9fda0-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

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
    To see the examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="9fda0-116">Listando os perfis CDN do Azure existentes</span><span class="sxs-lookup"><span data-stu-id="9fda0-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="9fda0-117">O cmdlet `Get-AzureRmCdnProfile` sem nenhum parâmetro recupera todos os seus perfis CDN existentes.</span><span class="sxs-lookup"><span data-stu-id="9fda0-117">The `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="9fda0-118">Essa saída pode ser transferida para os cmdlets para fazer uma enumeração.</span><span class="sxs-lookup"><span data-stu-id="9fda0-118">This output can be piped to cmdlets for enumeration.</span></span>

```powershell
# Output the name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="9fda0-119">Você também pode retornar um único perfil especificando o grupo de recursos e o nome do perfil.</span><span class="sxs-lookup"><span data-stu-id="9fda0-119">You can also return a single profile by specifying the profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="9fda0-120">É possível ter vários perfis CDN com o mesmo nome, desde que eles estejam em grupos de recursos diferentes.</span><span class="sxs-lookup"><span data-stu-id="9fda0-120">It is possible to have multiple CDN profiles with the same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="9fda0-121">Omitir o parâmetro `ResourceGroupName` retorna todos os perfis com um nome correspondente.</span><span class="sxs-lookup"><span data-stu-id="9fda0-121">Omitting the `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="9fda0-122">Listando os pontos de extremidade CDN existentes</span><span class="sxs-lookup"><span data-stu-id="9fda0-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="9fda0-123">`Get-AzureRmCdnEndpoint` pode recuperar um ponto de extremidade individual ou todos os pontos de extremidade em um perfil.</span><span class="sxs-lookup"><span data-stu-id="9fda0-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all the endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of the endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of the endpoints on all of the profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of the endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="9fda0-124">Criando perfis e pontos de extremidade CDN</span><span class="sxs-lookup"><span data-stu-id="9fda0-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="9fda0-125">`New-AzureRmCdnProfile` e `New-AzureRmCdnEndpoint` são usados para criar perfis e pontos de extremidade CDN.</span><span class="sxs-lookup"><span data-stu-id="9fda0-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used to create CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="9fda0-126">Verificando a disponibilidade do nome do ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="9fda0-126">Checking endpoint name availability</span></span>
<span data-ttu-id="9fda0-127">`Get-AzureRmCdnEndpointNameAvailability` retorna um objeto indicando se um nome do ponto de extremidade está disponível.</span><span class="sxs-lookup"><span data-stu-id="9fda0-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message to the console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="9fda0-128">Adicionando um domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="9fda0-128">Adding a custom domain</span></span>
<span data-ttu-id="9fda0-129">`New-AzureRmCdnCustomDomain` adiciona um nome de domínio personalizado a um ponto de extremidade existente.</span><span class="sxs-lookup"><span data-stu-id="9fda0-129">`New-AzureRmCdnCustomDomain` adds a custom domain name to an existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9fda0-130">Você deve configurar o CNAME com seu provedor DNS como descrito em [Como mapear o Domínio Personalizado para o ponto de extremidade CDN (Rede de Distribuição de Conteúdo)](cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="9fda0-130">You must set up the CNAME with your DNS provider as described in [How to map Custom Domain to Content Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="9fda0-131">Você pode testar o mapeamento antes de modificar o ponto de extremidade usando `Test-AzureRmCdnCustomDomain`.</span><span class="sxs-lookup"><span data-stu-id="9fda0-131">You can test the mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check the mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create the custom domain on the endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="9fda0-132">Modificando um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="9fda0-132">Modifying an endpoint</span></span>
<span data-ttu-id="9fda0-133">`Set-AzureRmCdnEndpoint` modifica um ponto de extremidade existente.</span><span class="sxs-lookup"><span data-stu-id="9fda0-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save the changed endpoint and apply the changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="9fda0-134">Limpando/Pré-carregando ativos CDN</span><span class="sxs-lookup"><span data-stu-id="9fda0-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="9fda0-135">`Unpublish-AzureRmCdnEndpointContent` limpa ativos armazenados em cache enquanto `Publish-AzureRmCdnEndpointContent` pré-carrega os ativos nos pontos de extremidade com suporte.</span><span class="sxs-lookup"><span data-stu-id="9fda0-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="9fda0-136">Iniciando/Parando os pontos de extremidade CDN</span><span class="sxs-lookup"><span data-stu-id="9fda0-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="9fda0-137">`Start-AzureRmCdnEndpoint` e `Stop-AzureRmCdnEndpoint` podem ser usados para iniciar e parar os pontos de extremidade individuais ou grupos de pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="9fda0-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used to start and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop the cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="9fda0-138">Excluindo os recursos CDN</span><span class="sxs-lookup"><span data-stu-id="9fda0-138">Deleting CDN resources</span></span>
<span data-ttu-id="9fda0-139">`Remove-AzureRmCdnProfile` e `Remove-AzureRmCdnEndpoint` podem ser usados para remover os pontos de extremidade e os perfis.</span><span class="sxs-lookup"><span data-stu-id="9fda0-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used to remove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all the endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="9fda0-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9fda0-140">Next Steps</span></span>
<span data-ttu-id="9fda0-141">Saiba como automatizar a CDN do Azure com [.NET](cdn-app-dev-net.md) ou [Node.js](cdn-app-dev-node.md).</span><span class="sxs-lookup"><span data-stu-id="9fda0-141">Learn how to automate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="9fda0-142">Para saber mais sobre os recursos CDN, consulte [Visão Geral da CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9fda0-142">To learn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>

