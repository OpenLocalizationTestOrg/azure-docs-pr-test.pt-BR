---
title: "aaaTroubleshoot conexões - PowerShell e o Gateway de rede Virtual do Azure | Microsoft Docs"
description: "Esta página explica como toouse Olá observador de rede do Azure solucionar problemas do cmdlet do PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: b7dbe6e44e0fa1ea0481223a84098d7a57c068a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>Como solucionar problemas de conexões e gateway de rede virtual do usando o PowerShell do Observador de rede do Azure

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API REST](network-watcher-troubleshoot-manage-rest.md)

Observador de rede fornece vários recursos que diz respeito a toounderstanding seus recursos de rede no Azure. Um desses recursos é a solução de problemas de recursos. Recursos de solução de problemas pode ser chamada por meio do portal de saudação, o PowerShell, CLI ou API REST. Quando chamado, o observador de rede inspeciona a integridade de saudação de um Gateway de rede Virtual ou uma Conexão e retorna suas descobertas.

## <a name="before-you-begin"></a>Antes de começar

Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.

Para obter uma lista de tipos de gateway com suporte, visite [Tipos de Gateway com suporte](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Visão geral

Solução de problemas de recursos fornece a capacidade de saudação solucionar problemas que surgem com Gateways de rede Virtual e conexões. Quando é feita uma solicitação tooresource de solução de problemas, os logs estão sendo consultados e inspecionado. Quando inspeção estiver concluída, os resultados de saudação são retornados. Solicitações de recursos para solução de problemas de solicitações são de longa execução, que pode levar vários tooreturn de minutos que um resultado. logs de saudação de solução de problemas são armazenados em um contêiner em uma conta de armazenamento especificado.

## <a name="retrieve-network-watcher"></a>Recuperar o Observador de Rede

Olá primeira etapa é a instância do tooretrieve Olá observador de rede. Olá `$networkWatcher` variável é passada toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet na etapa 4.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a>Como recuperar uma conexão de gateway de rede virtual

Neste exemplo, a solução de problemas de recursos está sendo executada em uma conexão. Você também pode passá-lo por um gateway de rede virtual.

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento

Solução de problemas de recurso retorna dados sobre integridade de saudação do recurso hello, ele também salva logs tooa armazenamento conta toobe revisado. Nesta etapa, criaremos uma conta de armazenamento. Você pode usar uma conta de armazenamento existente se já tiver uma.

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a>Como executar a solução de problemas de recursos do Observador de rede

Solucionar problemas de recursos com hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet. Passamos Olá cmdlet Olá observador de rede objeto, Olá Id de Conexão de saudação ou Gateway de rede Virtual, id de conta de armazenamento Olá e resultados de Olá Olá caminho toostore.

> [!NOTE]
> Olá `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet é demorado e pode levar toocomplete de alguns minutos.

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

Depois de executar o cmdlet Olá, observador de rede revisa a integridade de Olá Olá recursos tooverify. Ele retorna resultados de saudação toohello shell e armazena logs de resultados Olá Olá conta de armazenamento especificado.

## <a name="understanding-hello-results"></a>Entendendo os resultados da saudação

texto da ação de saudação fornece diretrizes gerais sobre como tooresolve Olá problema. Se uma ação pode ser executada para o problema de saudação, um link é fornecido com diretrizes adicionais. No caso de Olá onde não há nenhuma orientação adicional, resposta Olá fornece Olá url tooopen um caso de suporte.  Para obter mais informações sobre propriedades de saudação de resposta hello e o que está incluído, visite [visão geral da solução de problemas do Inspetor de rede](network-watcher-troubleshoot-overview.md)

Para obter instruções sobre como baixar os arquivos de contas de armazenamento do azure, consulte muito[Introdução ao armazenamento de BLOBs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Outra ferramenta que pode ser usada é o Gerenciador de armazenamento. Para obter mais informações sobre o Gerenciador de armazenamento podem ser encontradas aqui em Olá link a seguir: [Gerenciador de armazenamento](http://storageexplorer.com/)

## <a name="next-steps"></a>Próximas etapas

Se as configurações foram alteradas se parar a conectividade de VPN, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack para baixo Olá rede segurança e o grupo de regras de segurança que podem ser em questão.
