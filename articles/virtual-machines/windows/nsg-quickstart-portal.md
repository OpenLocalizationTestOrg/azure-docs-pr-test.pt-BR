---
title: "aaaOpen portas tooa VM usando Olá portal do Azure | Microsoft Docs"
description: "Saiba como tooopen uma porta / criar um ponto de extremidade tooyour VM do Windows usando o modelo de implantação do Gerenciador de recursos de Olá Olá Portal do Azure"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a>Como tooopen portas tooa máquina virtual Olá portal do Azure
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Comandos rápidos
Você também pode [executar essas etapas usando o Azure PowerShell](nsg-quickstart-powershell.md).

Primeiro, crie o seu Grupo de Segurança de Rede. Selecione um grupo de recursos no portal de saudação, escolha **adicionar**, em seguida, procure e selecione **grupo de segurança de rede**:

![Adicionar um Grupo de Segurança de Rede](./media/nsg-quickstart-portal/add-nsg.png)

Insira um nome para o seu Grupo de Segurança de Rede, selecione ou crie um grupo de recursos e selecione uma localização. Selecione **Criar** quando terminar:

![Criar um grupo de segurança de rede](./media/nsg-quickstart-portal/create-nsg.png)

Selecione o novo Grupo de Segurança de Rede. Selecione as regras de segurança de entrada e selecione Olá **adicionar** botão toocreate uma regra:

![Adicionar uma regra de entrada](./media/nsg-quickstart-portal/add-inbound-rule.png)

Escolha um comum **Service** do menu suspenso de hello, tais como *HTTP*. Você também pode selecionar *personalizado* tooprovide toouse uma porta específica. Se desejar, altere a prioridade de saudação ou nome. prioridade Hello afeta ordem Olá na qual as regras são aplicadas - Olá inferior Olá numérico valor, hello anteriores Olá regra é aplicada. Você também pode selecionar **avançado** na parte superior de saudação do tooenter tela uma determinada fonte de intervalo de porta ou bloco IP, por exemplo. Quando você estiver pronto, selecione **Okey** toocreate regra de saudação:

![Criar uma regra de entrada](./media/nsg-quickstart-portal/create-inbound-rule.png)

A etapa final é tooassociate ao grupo de segurança da sua rede com uma sub-rede ou uma interface de rede específico. Vamos associar Olá grupo de segurança de rede com uma sub-rede. Selecione **Sub-redes** e escolha **Associar**:

![Associar um Grupo de Segurança de Rede a uma sub-rede](./media/nsg-quickstart-portal/associate-subnet.png)

Selecione a rede virtual e selecione sub-rede apropriada hello:

![Associar um Grupo de Segurança de Rede à rede virtual](./media/nsg-quickstart-portal/select-vnet-subnet.png)

Você criou um Grupo de Segurança de Rede, uma regra de entrada que permite o tráfego na porta 80 e o associou a uma sub-rede. Todas as máquinas virtuais que você se conectar a sub-rede toothat estão acessíveis na porta 80.

## <a name="more-information-on-network-security-groups"></a>Mais informações sobre os Grupos de Segurança de Rede
Olá aqui rápido comandos permitem que você tooget para cima e em execução com tooyour de fluxo de tráfego VM. Grupos de segurança de rede fornecem vários recursos excelentes e granularidade para controlar recursos tooyour de acesso. Você pode ler mais sobre a [criação de um Grupo de Segurança de Rede e as regras ACL aqui](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).

Para aplicativos Web altamente disponíveis, você deve colocar suas VMs atrás de um balanceador de carga do Azure. Balanceador de carga Olá distribui tráfego tooVMs, com um grupo de segurança de rede que fornece filtragem. Para obter mais informações, consulte [como balancear tooload Linux virtual máquinas no Azure toocreate um aplicativo altamente disponível](tutorial-load-balancer.md).

## <a name="next-steps"></a>Próximas etapas
Neste exemplo, você criou um tráfego HTTP de tooallow regra simples. Você pode encontrar informações sobre como criar ambientes mais detalhadas no hello artigos a seguir:

* [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [O que é um NSG (grupo de segurança de rede)?](../../virtual-network/virtual-networks-nsg.md)