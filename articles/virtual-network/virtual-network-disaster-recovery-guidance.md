---
title: "toodo aaaWhat no evento de saudação de uma interrupção de serviço do Azure afetando redes virtuais do Azure | Microsoft Docs"
description: "Saiba quais toodo no evento de saudação de uma interrupção de serviço do Azure afetando redes virtuais do Azure."
services: virtual-network
documentationcenter: 
author: NarayanAnnamalai
manager: jefco
editor: 
ms.assetid: ad260ab9-d873-43b3-8896-f9a1db9858a5
ms.service: virtual-network
ms.workload: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: narayan;aglick
ms.openlocfilehash: db022d2a042d255cf8ec6afb68cd8436aeecfe08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network--business-continuity"></a>Rede Virtual – Continuidade de Negócios
## <a name="overview"></a>Visão geral
Uma rede Virtual (VNet) é uma representação lógica da rede em nuvem hello. Ele permite que você toodefine sua própria privada IP endereço espaço e segmento Olá de rede em sub-redes. VNets serve como um toohost de limite de confiança seus recursos de computação como máquinas virtuais do Azure e os serviços de nuvem (funções web/trabalho). Uma rede virtual permite a comunicação de IP privada direta entre os recursos de saudação hospedado nela. Uma rede Virtual também pode ser vinculado tooan rede de local por meio de uma das opções de híbrida hello como um Gateway de VPN ou rota expressa.

Uma rede virtual é criada no escopo de saudação de uma região. Você pode criar VNets com o mesmo espaço de endereço em duas regiões diferentes (ou seja, nos Leste e Oeste dos EUA, mas não é possível conectá-los tooone outro diretamente). 

## <a name="business-continuity"></a>Continuidade dos negócios
O seu aplicativo pode ser interrompido de várias maneiras diferentes. Uma determinada região poderia ser totalmente cortada devido a desastres naturais tooa ou um desastre parcial devido a falha de tooa de vários dispositivos/serviços. impacto de saudação no hello serviço de rede virtual é diferente em cada uma dessas situações.

**P: o que fazer em caso de saudação de uma interrupção tooan toda a região? Por exemplo, se uma região é completamente corte devido a desastres naturais tooa? O que acontece toohello redes virtuais hospedadas em região Olá?**

R: os recursos Olá Olá e de rede de Virtual em Olá afetados região permanece inacessível durante o tempo de saudação da interrupção do serviço hello.

![Diagrama de Rede Virtual Simples](./media/virtual-network-disaster-recovery-guidance/vnet.png)

**P: qual é possível toodo recriar Olá a mesma rede Virtual em uma região diferente?**

R: A Rede Virtual (VNet) é um recurso relativamente leve. Você pode chamar APIs do Azure toocreate uma rede virtual com hello mesmo espaço de endereço em uma região diferente. toore-criar hello mesmo ambiente que estava presente no hello afetado região, você tem toomake API chamadas toore-implante seus serviços de nuvem (funções web/trabalho) e máquinas virtuais que você tinha. Você também terá toospin até um Gateway de VPN e conectar-se a rede de local de tooyour se você tiver conectividade de local (como em uma implantação híbrida).

instruções de saudação para criar uma rede virtual são encontradas [aqui](virtual-networks-create-vnet-arm-pportal.md). 

**P: Uma réplica de uma VNet em uma determinada região pode ser recriada em outra região antecipadamente?**

R: Sim, você pode criar dois VNets usando Olá mesmo IP privado espaço de endereço e recursos em duas regiões diferentes depois do tempo. Se um cliente foi hospedando serviços em redes de saudação da internet, eles podem ter configurar toogeo Gerenciador de tráfego de rota tráfego toohello região que está ativa. No entanto, um cliente não pode se conectar a dois VNets com hello mesmo endereço rede de local de tootheir espaço como ele pode causar problemas de roteamento. No tempo de saudação de um desastre e a perda de uma rede virtual em uma região, um cliente pode se conectar Olá outra VNet na região de saudação disponível com a rede local correspondente endereço espaço tootheir.

instruções de saudação para criar uma rede virtual são encontradas [aqui](virtual-networks-create-vnet-arm-pportal.md).

