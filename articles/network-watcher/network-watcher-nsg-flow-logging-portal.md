---
title: "logs de fluxo de grupo de segurança da rede do aaaManage com o observador de rede do Azure | Microsoft Docs"
description: "Esta página explica como toomanage fluxo de grupo de segurança de rede se registra no Inspetor de rede do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a>Gerenciar logs de fluxo de grupo de segurança de rede no hello portal do Azure

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [API REST](network-watcher-nsg-flow-logging-rest.md)

Logs de fluxo de grupo de segurança de rede são um recurso do observador de rede que permite que você tooview informações sobre o tráfego IP de entrada e saída por meio de um grupo de segurança de rede. Esses logs de fluxo são gravados no formato JSON e fornecem informações importantes, incluindo: 

- Fluxos de entrada e saída por regra.
- Olá NIC Olá fluxo aplica-se a.
- 5-tupla informações sobre o fluxo de saudação (origem/destino IP, porta de origem/destino, protocolo).
- Informação sobre o tráfego ter sido permitido ou negado.

## <a name="before-you-begin"></a>Antes de começar

Este cenário pressupõe que você já seguiu etapas Olá [criar uma instância do observador de rede](network-watcher-create.md). cenário de saudação também pressupõe que você tenha um grupo de recursos com uma máquina virtual válido.

## <a name="register-insights-provider"></a>Provedor de informações de registro

Fluxo de log toowork com êxito, Olá **Insights** provedor deve ser registrado. provedor de saudação tooregister, Olá execute as etapas a seguir: 

1. Vá muito**assinaturas**e em seguida, selecione a assinatura Olá para o qual você deseja tooenable fluxo logs. 
2. Em Olá **assinatura** folha, selecione **provedores de recursos**. 
3. Examinar a lista de saudação de provedores e verifique se esse Olá **Insights** provedor está registrado. Se não estiver, selecione **Registrar**.

![Exibir provedores][providers]

## <a name="enable-flow-logs"></a>Habilitar logs de fluxo

Essas etapas levá-lo pelo processo de saudação de habilitar os logs de fluxo em um grupo de segurança de rede.

### <a name="step-1"></a>Etapa 1

Acesse a instância do observador de rede tooa e, em seguida, selecione **NSG fluxo logs**.

![Visão geral dos logs de fluxo][1]

### <a name="step-2"></a>Etapa 2

Selecione um grupo de segurança de rede na lista de saudação.

![Visão geral dos logs de fluxo][2]

### <a name="step-3"></a>Etapa 3 

Em Olá **configurações dos logs do fluxo de** folha, definir status da saudação muito**em**e, em seguida, configure uma conta de armazenamento.  Quando terminar, selecione **OK**. Em seguida, selecione **Salvar**.

![Visão geral dos logs de fluxo][3]

## <a name="download-flow-logs"></a>Baixar logs de fluxo

Os Logs de fluxo são salvos em uma conta de armazenamento. Baixe o tooview de logs de fluxo-los.

### <a name="step-1"></a>Etapa 1

logs de fluxo de toodownload, selecione **você pode baixar os logs de fluxo de contas de armazenamento configurado**. Esta etapa usa o modo de exibição de conta de armazenamento tooa onde você pode escolher quais toodownload de logs.

![Configurações dos logs do fluxo][4]

### <a name="step-2"></a>Etapa 2

Vá toohello conta de armazenamento correta. Em seguida, selecione **Contêineres** > **insights-log-networksecuritygroupflowevent**.

![Configurações dos logs do fluxo][5]

### <a name="step-3"></a>Etapa 3

Vá toohello local do log de fluxo hello, selecioná-lo e, em seguida, selecione **baixar**.

![Configurações dos logs do fluxo][6]

Para obter informações sobre a estrutura de saudação do log hello, visite [visão geral do log fluxo de grupo de segurança de rede](network-watcher-nsg-flow-logging-overview.md).

## <a name="next-steps"></a>Próximas etapas

Saiba como muito[visualizar seus logs de fluxo NSG com PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
