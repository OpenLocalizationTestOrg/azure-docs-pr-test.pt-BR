---
title: "aaaTroubleshoot conexões - 1.0 da CLI do Azure e o Gateway de rede Virtual do Azure | Microsoft Docs"
description: "Esta página explica como solucionar problemas de toouse Olá observador de rede do Azure 1.0 da CLI do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: a0511689d773f9c7216b0fe5470e27f754eb600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a>Como solucionar problemas de conexões e gateway de rede virtual do usando a CLI do Azure 1.0 do Observador de Rede do Azure

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API REST](network-watcher-troubleshoot-manage-rest.md)

Observador de rede fornece vários recursos que diz respeito a toounderstanding seus recursos de rede no Azure. Um desses recursos é a solução de problemas de recursos. Recursos de solução de problemas pode ser chamada por meio do portal de saudação, o PowerShell, CLI ou API REST. Quando chamado, o observador de rede inspeciona a integridade de saudação de um Gateway de rede Virtual ou uma Conexão e retorna suas descobertas.

Este artigo usa a CLI 1.0 do Azure para plataforma cruzada, que está disponível para Windows, Mac e Linux. 

## <a name="before-you-begin"></a>Antes de começar

Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.

Para obter uma lista de tipos de gateway com suporte, visite [Tipos de Gateway com suporte](/network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Visão geral

Solução de problemas de recursos fornece a capacidade de saudação solucionar problemas que surgem com Gateways de rede Virtual e conexões. Quando é feita uma solicitação tooresource de solução de problemas, os logs estão sendo consultados e inspecionado. Quando inspeção estiver concluída, os resultados de saudação são retornados. Solicitações de recursos para solução de problemas de solicitações são de longa execução, que pode levar vários tooreturn de minutos que um resultado. logs de saudação de solução de problemas são armazenados em um contêiner em uma conta de armazenamento especificado.

## <a name="retrieve-a-virtual-network-gateway-connection"></a>Como recuperar uma conexão de gateway de rede virtual

Neste exemplo, a solução de problemas de recursos está sendo executada em uma conexão. Você também pode passá-lo por um gateway de rede virtual. Olá cmdlet a seguir lista Olá-conexões vpn em um grupo de recursos.

```azurecli
azure network vpn-connection list -g resourceGroupName
```

Você também pode executar Olá comando toosee conexões Olá em uma assinatura.

```azurecli
azure network vpn-connection list -s subscription
```

Depois que você tem o nome de saudação do conexão Olá, você pode executar esse comando tooget sua Id de recurso:

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento

Solução de problemas de recurso retorna dados sobre integridade de saudação do recurso hello, ele também salva logs tooa armazenamento conta toobe revisado. Nesta etapa, criaremos uma conta de armazenamento. Você pode usar uma conta de armazenamento existente se já tiver uma.

1. Criar conta de armazenamento Olá

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. Obter chaves de conta de armazenamento Olá

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. Criar contêiner Olá

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a>Como executar a solução de problemas de recursos do Observador de rede

Solucionar problemas de recursos com hello `network watcher troubleshoot` cmdlet. Passamos o grupo de recursos de Olá Olá cmdlet, nome da saudação observador de rede, Olá Id de conexão de saudação Olá Olá Id da conta de armazenamento hello e Olá toostore do hello caminho toohello blob solucionar resulta em.

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

Depois de executar o cmdlet Olá, observador de rede revisa a integridade de Olá Olá recursos tooverify. Ele retorna resultados de saudação toohello shell e armazena logs de resultados Olá Olá conta de armazenamento especificado.

## <a name="understanding-hello-results"></a>Entendendo os resultados da saudação

texto da ação de saudação fornece diretrizes gerais sobre como tooresolve Olá problema. Se uma ação pode ser executada para o problema de saudação, um link é fornecido com diretrizes adicionais. No caso de Olá onde não há nenhuma orientação adicional, resposta Olá fornece Olá url tooopen um caso de suporte.  Para obter mais informações sobre propriedades de saudação de resposta hello e o que está incluído, visite [visão geral da solução de problemas do Inspetor de rede](network-watcher-troubleshoot-overview.md)

Para obter instruções sobre como baixar os arquivos de contas de armazenamento do azure, consulte muito[Introdução ao armazenamento de BLOBs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Outra ferramenta que pode ser usada é o Gerenciador de armazenamento. Para obter mais informações sobre o Gerenciador de armazenamento podem ser encontradas aqui em Olá link a seguir: [Gerenciador de armazenamento](http://storageexplorer.com/)

## <a name="next-steps"></a>Próximas etapas

Se as configurações foram alteradas se parar a conectividade de VPN, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack para baixo Olá rede segurança e o grupo de regras de segurança que podem ser em questão.
