---
title: "Balanceador de carga aaaCreate um voltados para Internet - clássico do portal do Azure | Microsoft Docs"
description: "Saiba como toocreate um balanceador de carga voltado para Internet no modelo de implantação clássico usando Olá portal clássico do Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a>Introdução à criação de uma balanceador de carga (clássico) no portal clássico do Azure de saudação da Internet

> [!div class="op_single_selector"]
> * [Portal clássico do Azure](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Serviços de Nuvem do Azure](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Antes de trabalhar com recursos do Azure, é importante toounderstand que o Azure atualmente tem dois modelos de implantação: Gerenciador de recursos do Azure e clássico. Verifique se você entendeu [os modelos e as ferramentas de implantação](../azure-classic-rm.md) antes de trabalhar com qualquer recurso do Azure. Você pode exibir a documentação de saudação para diferentes ferramentas clicando Olá guias na parte superior da saudação deste artigo. Este artigo aborda o modelo de implantação clássico hello. Você também pode [aprender a usar o Gerenciador de recursos do Azure de Balanceador de carga de toocreate um voltados à Internet de como](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a>Configurar um balanceador de carga da Internet para máquinas virtuais

No tráfego de rede ordem tooload saldo de saudação da Internet em máquinas virtuais de saudação de um serviço de nuvem, você deve criar um conjunto com balanceamento de carga. Esse procedimento pressupõe que você já criou máquinas virtuais de saudação e que são todos em Olá mesmo serviço de nuvem.

**tooconfigure um conjunto com balanceamento de carga para máquinas virtuais**

1. No portal clássico do Azure do hello, clique em **máquinas virtuais**e clique em nome de saudação de uma máquina virtual no conjunto de balanceamento de carga de saudação.
2. Clique em **Pontos de Extremidade** e depois em **Adicionar**.
3. Em Olá **adicionar uma máquina de virtual do ponto de extremidade tooa** página, clique na seta direita hello.
4. Em Olá **especificar detalhes de saudação do ponto de extremidade de saudação** página:

   * Em **nome**, digite um nome para o ponto de extremidade de saudação ou selecione o nome de saudação da lista de saudação de pontos de extremidade predefinidas para protocolos comuns.
   * Em **protocolo**, selecione o protocolo de saudação exigido pelo tipo de saudação do ponto de extremidade, TCP ou UDP, conforme necessário.
   * Em **porta pública e porta privada**, digite Olá números de porta que você deseja Olá toouse de máquina virtual, conforme necessário. Você pode usar regras de firewall e porta privada Olá no tráfego de tooredirect Olá máquina virtual de forma que seja apropriado para seu aplicativo. porta privada Olá pode Olá igual a porta pública hello. Por exemplo, um ponto de extremidade para o tráfego da web (HTTP), você pode atribuir tooboth 80 Olá públicas e privadas porta.

5. Selecione **criar um conjunto com balanceamento de carga**e, em seguida, clique na seta direita hello.
6. Em Olá **configurar conjunto de balanceamento de carga de saudação** página, digite um nome para o conjunto de balanceamento de carga hello e, em seguida, atribuir valores de saudação comportamento de sonda de saudação balanceador de carga do Azure. Olá balanceador de carga usa testes toodetermine se máquinas virtuais de saudação em conjunto com balanceamento de carga de saudação tooreceive disponível o tráfego de entrada.
7. Clique em Olá marca de seleção toocreate Olá com balanceamento de carga de ponto de extremidade. Você verá **Sim** em Olá **o nome do conjunto com balanceamento de carga** coluna da saudação **pontos de extremidade** página para a máquina virtual de saudação.
8. No portal de saudação, clique em **máquinas virtuais**, clique em nome de saudação de uma máquina virtual adicional no conjunto de balanceamento de carga de saudação **pontos de extremidade**e, em seguida, clique em **adicionar**.
9. Em Olá **adicionar uma máquina de virtual do ponto de extremidade tooa** , clique em **Adicionar ponto de extremidade tooan existente com balanceamento de carga conjunto**, selecione o nome de saudação do conjunto de balanceamento de carga de hello e, em seguida, clique na seta direita hello.
10. Em Olá **especificar detalhes de saudação do ponto de extremidade de saudação** página, digite um nome para o ponto de extremidade de saudação e, em seguida, clique em marca de seleção de saudação.

Para Olá máquinas virtuais em conjunto com balanceamento de carga do hello, repita as etapas 8 a 10.

## <a name="next-steps"></a>Próximas etapas

[Introdução à configuração de um balanceador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurar um modo de distribuição do balanceador de carga](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
