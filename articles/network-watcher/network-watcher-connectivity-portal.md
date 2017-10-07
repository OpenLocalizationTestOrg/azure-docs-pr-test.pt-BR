---
title: aaaCheck conectividade com o observador de rede do Azure - portal do Azure | Microsoft Docs
description: "Esta página explica como toouse conectividade para verificar com o observador de rede usando Olá portal do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a>Verifique a conectividade com o observador de rede do Azure usando Olá portal do Azure

> [!div class="op_single_selector"]
> - [Portal](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [CLI 2.0](network-watcher-connectivity-cli.md)
> - [API REST do Azure](network-watcher-connectivity-rest.md)

Saiba como toouse tooverify de conectividade se uma conexão TCP direto de tooa uma máquina virtual que recebe o ponto de extremidade pode ser estabelecida.

## <a name="before-you-begin"></a>Antes de começar

Este artigo pressupõe que você tenha Olá recursos a seguir:

* Uma instância do observador de rede na região Olá deseja toocheck conectividade.

* Conectividade de toocheck de máquinas virtuais com.

> [!IMPORTANT]
> A verificação de conectividade requer uma extensão de máquina virtual `AzureNetworkWatcherExtension`. Para instalar a extensão de saudação em uma VM do Windows, visite [extensão de máquina virtual do agente do Inspetor de rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para a visita de VM do Linux [extensão de máquina virtual do agente do Inspetor de rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="check-connectivity-tooa-virtual-machine"></a>Verifique a conectividade tooa virtual machine

Este exemplo verifica a máquina de virtual de destino conectividade tooa pela porta 80.

Navegue tooyour observador de rede e clique em **verificação de conectividade (visualização)**. Selecione a conectividade de toocheck de máquina virtual de saudação do. Em Olá **destino** seção escolher **selecione uma máquina virtual** e escolha a máquina virtual correta de saudação e porta tootest.

Depois de clicar em **verificar**, conectividade de saudação entre máquinas virtuais Olá Olá porta especificada são verificadas. No exemplo hello, destino Olá VM está inacessível, uma lista de saltos serão mostrados.

![Verificar os resultados de conectividade para uma máquina virtual][1]

## <a name="check-remote-endpoint-connectivity"></a>Verificar a conectividade de ponto de extremidade remoto

conectividade de saudação toocheck e latência tooa ponto de extremidade remoto, escolha Olá **especificar manualmente** botão de opção na Olá **destino** seção, Olá url e a porta de saudação de entrada e clique em **verificar** .  Isso é usado para pontos de extremidade remotos como pontos de extremidade de sites e de armazenamento.

![Resultados da verificação de conectividade para um site Web][2]

## <a name="next-steps"></a>Próximas etapas

Saiba como o pacote tooautomate captura com alertas de máquina Virtual por meio da exibição [criar uma captura de pacote de disparo de alerta](network-watcher-alert-triggered-packet-capture.md)

Localize se determinado tráfego é permitido dentro ou fora de sua VM visitando [Verificar o fluxo do IP](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
