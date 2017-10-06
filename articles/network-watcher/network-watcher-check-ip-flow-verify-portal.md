---
title: "Verifique se o tráfego aaaVerify com fluxo de IP de Inspetor de rede do Azure - portal do Azure | Microsoft Docs"
description: "Este artigo descreve como toocheck se tooor de tráfego de uma máquina virtual é permitido ou negado"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Verifique se o tráfego é permitido ou negado tooor de uma VM com IP fluxo verificar um componente do observador de rede do Azure

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [API REST do Azure](network-watcher-check-ip-flow-verify-rest.md)


Fluxo IP, verifique se é um recurso do observador de rede que permite que você tooverify se o tráfego é permitido tooor de uma máquina virtual. validação de saudação pode ser executada para o tráfego de entrada ou saído. Esse cenário é útil tooget um estado atual do se uma máquina virtual pode se comunicar recursos externos tooan ou outro recurso. Fluxo IP, verifique se pode ser usado tooverify se suas regras de grupo de segurança de rede (NSG) estão configuradas corretamente e solucionar problemas fluxos que estão sendo bloqueados por regras NSG. Outro motivo para usar IP fluxo Verifique se está tooensure tráfego que deseja bloquear está sendo bloqueado corretamente pelo Olá NSG.

## <a name="before-you-begin"></a>Antes de começar

Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede ou ter uma instância existente do observador de rede. cenário de Olá também pressupõe que um grupo de recursos com uma máquina virtual válida existe toobe usado.

## <a name="scenario"></a>Cenário

Esse cenário usa tooverify IP fluxo verificar se uma máquina virtual pode se comunicar tooanother máquina pela porta 443. Se Olá tráfego é negado, ele retornará regra de segurança de saudação que está negando esse tráfego. toolearn mais sobre IP fluxo verificar, visite [fluxo verificar a visão geral de IP](network-watcher-ip-flow-verify-overview.md)

### <a name="run-ip-flow-verify"></a>Executar a verificação de fluxo de IP

Navegue tooyour observador de rede e clique em **Verifique se o fluxo IP**. Selecione máquina virtual de saudação e interface de rede que você deseja que o tráfego de tooverify do. Insira as informações adicionais de filtragem e clique em **Verificar**.

Depois de clicar em **verificar**, fluxo de saudação com base em critérios de saudação fornecida é verificado. é o resultado de saudação **acesso permitido** ou **acesso negado**. Se o acesso é negado, Olá o grupo de segurança de rede (NSG) e regra de segurança que bloqueiam o tráfego é fornecida. Se a negação de saudação do tráfego é o comportamento esperado, regra Olá foi bem-sucedida.

> [!NOTE]
> Fluxo IP verificar requer que o recurso VM hello está alocado.

Como você pode ver da saudação imagem a seguir, o tráfego HTTPS de saída Olá foi permitido.

![visão geral da verificação de fluxo de IP][1]

Conforme visto no Olá a imagem a seguir, o tráfego é alterado tooinbound e hello too123 alterada de porta de entrada. O tráfego é negado Agora, mensagem de saudação "Acesso negado" é fornecida junto com hello rede segurança e o grupo de regra de segurança que negar o tráfego de saudação.

![resultados do fluxo de IP][2]

## <a name="next-steps"></a>Próximas etapas

Se o tráfego está sendo bloqueado e não deve ser, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack para baixo Olá rede segurança e o grupo de regras de segurança que são definidas.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













