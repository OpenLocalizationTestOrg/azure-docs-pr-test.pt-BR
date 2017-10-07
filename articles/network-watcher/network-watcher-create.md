---
title: "aaaCreate uma instância do observador de rede do Azure | Microsoft Docs"
description: "Esta página fornece Olá etapas toocreate uma instância do observador de rede usando o portal de saudação e a API REST do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a>Criar uma instância do Observador de Rede do Azure

Observador de rede é um serviço regional que permite que você toomonitor e diagnosticar as condições em uma rede cenário nível, para e do Azure. Monitoramento do nível do cenário permite que você toodiagnose problemas em uma exibição de nível de rede de tooend final. Diagnóstico de rede e as ferramentas de visualização disponíveis com o observador de rede ajudarão-lo a entender, diagnosticar e obter a rede de tooyour insights no Azure.

> [!NOTE]
> Observador de rede atualmente suporta apenas CLI 1.0, Olá instruções toocreate uma nova instância do observador de rede é fornecida para CLI 1.0.

## <a name="create-a-network-watcher-in-hello-portal"></a>Criar um observador de rede no portal de saudação

Navegue muito**mais serviços** > **rede** > **observador de rede**. Você pode selecionar todas as assinaturas de saudação desejado tooenable observador de rede para. Essa ação cria um Observador de Rede em todas as regiões que ele está disponível.

![criar um observador de rede][1]

Quando você habilita o observador de rede usando o Portal de saudação, Olá nome da instância do observador de rede Olá será automaticamente definido tooNetworkWatcher_region_name onde region_name corresponde toohello região do Azure em que a instância de saudação foi habilitada.  Por exemplo, um Observador de Rede habilitado na região Centro-Oeste dos EUA será nomeado NetworkWatcher_westcentralus

Além disso, instância do observador de rede Olá automaticamente será adicionada a um grupo de recursos denominado NetworkWatcherRG.  Esse grupo de recursos será criado, se ele ainda não existir.

Se desejar que o nome da saudação toocustomize de uma instância do observador de rede e hello grupo de recursos que ele é colocado no, você pode usar o Powershell, Olá API REST ou ARMClient métodos descritos abaixo.  Cada opção, Olá grupo de recursos deve existir antes de você colocar Olá observador de rede para ele.  

## <a name="create-a-network-watcher-with-powershell"></a>Criar um Observador de Rede com o PowerShell

toocreate uma instância do observador de rede, execute Olá exemplo a seguir:

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a>Criar um observador de rede com hello API REST

ARMclient é toocall usado Olá REST API usando o PowerShell. O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)

### <a name="log-in-with-armclient"></a>Fazer logon com o ARMClient

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a>Criar o observador de rede Olá

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a>Próximas etapas

Agora que você tem uma instância do observador de rede, saiba mais sobre os recursos de saudação disponíveis:

* [Topologia](network-watcher-topology-overview.md)
* [Captura de pacotes](network-watcher-packet-capture-overview.md)
* [Verificação de fluxo de IP](network-watcher-ip-flow-verify-overview.md)
* [Próximo salto](network-watcher-next-hop-overview.md)
* [Exibição de grupo de segurança](network-watcher-security-group-view-overview.md)
* [Registro do fluxo NSG](network-watcher-nsg-flow-logging-overview.md)
* [Solução de problemas do Gateway de Rede Virtual](network-watcher-troubleshoot-overview.md)

Quando uma instância do observador de rede tiver sido criada, captura de pacote pode ser configurada pelo seguinte artigo Olá: [criar uma captura de pacote de disparo de alerta](network-watcher-alert-triggered-packet-capture.md)

[1]: ./media/network-watcher-create/figure1.png











