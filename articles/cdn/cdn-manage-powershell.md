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
# <a name="manage-azure-cdn-with-powershell"></a>Gerenciar a CDN do Azure com o PowerShell
PowerShell fornece uma saudação mais flexível métodos toomanage os perfis de CDN do Azure e os pontos de extremidade.  Você pode usar o PowerShell interativamente ou escrevendo scripts tooautomate tarefas de gerenciamento.  Este tutorial demonstra várias das tarefas mais comuns de saudação pode ser realizadas com o PowerShell toomanage os perfis de CDN do Azure e os pontos de extremidade.

## <a name="prerequisites"></a>Pré-requisitos
toouse PowerShell toomanage os perfis de CDN do Azure e os pontos de extremidade, você deve ter hello Azure PowerShell module instalada.  toolearn como tooinstall PowerShell do Azure e conecte-se tooAzure usando Olá `Login-AzureRmAccount` cmdlet, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

> [!IMPORTANT]
> Você deve fazer logon com `Login-AzureRmAccount` antes de executar os cmdlets do Azure PowerShell.
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a>Listando os cmdlets do Azure CDN Olá
Você pode listar todos os cmdlets do Azure CDN hello usando Olá `Get-Command` cmdlet.

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

## <a name="getting-help"></a>Obtendo ajuda
Você pode obter ajuda com qualquer um desses cmdlets usando Olá `Get-Help` cmdlet.  `Get-Help` fornece o uso e a sintaxe, e opcionalmente mostra exemplos.

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

## <a name="listing-existing-azure-cdn-profiles"></a>Listando os perfis CDN do Azure existentes
Olá `Get-AzureRmCdnProfile` cmdlet sem parâmetros recupera todos os seus perfis CDN existentes.

```powershell
Get-AzureRmCdnProfile
```

Essa saída pode ser toocmdlets indicada para enumeração.

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

Você também pode retornar um único perfil, especificando o grupo de recursos e o nome do perfil de saudação.

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> É possível toohave CDN vários perfis com hello mesmo nome, desde que eles estão em diferentes grupos de recursos.  Omitir Olá `ResourceGroupName` parâmetro retorna todos os perfis com um nome correspondente.
> 
> 

## <a name="listing-existing-cdn-endpoints"></a>Listando os pontos de extremidade CDN existentes
`Get-AzureRmCdnEndpoint`pode recuperar um ponto de extremidade individual ou todos os pontos de extremidade de saudação em um perfil.  

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

## <a name="creating-cdn-profiles-and-endpoints"></a>Criando perfis e pontos de extremidade CDN
`New-AzureRmCdnProfile`e `New-AzureRmCdnEndpoint` são usadas toocreate CDN perfis e pontos de extremidade.

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a>Verificando a disponibilidade do nome do ponto de extremidade
`Get-AzureRmCdnEndpointNameAvailability` retorna um objeto indicando se um nome do ponto de extremidade está disponível.

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a>Adicionando um domínio personalizado
`New-AzureRmCdnCustomDomain`Adiciona um domínio personalizado nome tooan ponto de extremidade existente.

> [!IMPORTANT]
> Você deve configurar Olá CNAME com seu provedor DNS conforme descrito em [como ponto de extremidade da rede de entrega (CDN) tooContent toomap domínio personalizado](cdn-map-content-to-custom-domain.md).  Você pode testar o mapeamento de saudação antes de modificar o ponto de extremidade usando `Test-AzureRmCdnCustomDomain`.
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

## <a name="modifying-an-endpoint"></a>Modificando um ponto de extremidade
`Set-AzureRmCdnEndpoint` modifica um ponto de extremidade existente.

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a>Limpando/Pré-carregando ativos CDN
`Unpublish-AzureRmCdnEndpointContent` limpa ativos armazenados em cache enquanto `Publish-AzureRmCdnEndpointContent` pré-carrega os ativos nos pontos de extremidade com suporte.

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a>Iniciando/Parando os pontos de extremidade CDN
`Start-AzureRmCdnEndpoint`e `Stop-AzureRmCdnEndpoint` podem ser usado toostart e interromper os pontos de extremidade individuais ou grupos de pontos de extremidade.

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a>Excluindo os recursos CDN
`Remove-AzureRmCdnProfile`e `Remove-AzureRmCdnEndpoint` podem ser usados tooremove perfis e pontos de extremidade.

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a>Próximas etapas
Saiba como tooautomate CDN do Azure com [.NET](cdn-app-dev-net.md) ou [Node.js](cdn-app-dev-node.md).

toolearn sobre os recursos CDN, consulte [visão geral da CDN](cdn-overview.md).

