---
title: "aaaFind próximo salto com Azure rede Inspetor de próximo salto - portal do Azure | Microsoft Docs"
description: "Este artigo descreve como descobrir quais saudação do tipo de próximo salto é e endereço ip usando próximo salto Olá portal do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a>Descobrir que tipo de próximo salto Olá está usando o recurso de próximo salto Olá no Inspetor de rede do Azure usando o portal de saudação

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [API REST do Azure](network-watcher-check-next-hop-rest.md)

Próximo salto é um recurso do observador de rede que fornece a capacidade de saudação tipo hello de próximo salto e o endereço IP com base em uma máquina virtual especificada. Esse recurso é útil para determinar se o tráfego que deixa uma máquina virtual atravessa um gateway, internet ou redes virtuais tooget tooits destino.

## <a name="before-you-begin"></a>Antes de começar

Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede. cenário de Olá também pressupõe que um grupo de recursos com uma máquina virtual válida existe toobe usado.

## <a name="scenario"></a>Cenário

cenário de saudação abordado neste artigo usa toofind de próximo salto tipo hello de próximo salto e o endereço IP de um recurso. toolearn mais sobre o próximo nó, visite [visão geral próximo salto](network-watcher-next-hop-overview.md).

Neste cenário, você:

* Recupere o próximo salto de saudação de uma máquina virtual.

## <a name="get-next-hop"></a>Obter o próximo salto

### <a name="step-1"></a>Etapa 1

Navegue tooyour recurso observador de rede Olá portal do Azure.

### <a name="step-2"></a>Etapa 2

Clique em **do próximo salto** no painel de navegação do hello, Olá selecione máquina de virtual e interface de rede, preencha Olá IP de origem e de destino e, em seguida, clique em Olá **do próximo salto** botão.

> [!NOTE]
> Próximo salto requer que o recurso VM hello está alocado toorun.

![visão geral de obtenção do próximo salto][1]

### <a name="step-3"></a>Etapa 3

Após a conclusão da tarefa hello, resultados de saudação são fornecidos. Olá endereço IP e o tipo de próximo salto saudação do dispositivo é, é exibida. Olá tabela a seguir mostra os valores retornados disponíveis Olá no portal de saudação.

**Tipo do próximo salto**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Nenhum

Se uma rota personalizada foi usado tooroute esse tráfego de rota definidas pelo usuário da saudação (UDR) também é exibido com resultados de saudação.

![resultados da obtenção do próximo salto][2]

## <a name="next-steps"></a>Próximas etapas

Saiba como tooreview as configurações de grupo de segurança de rede por meio de programação visitando [NSG auditoria com o observador de rede](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














