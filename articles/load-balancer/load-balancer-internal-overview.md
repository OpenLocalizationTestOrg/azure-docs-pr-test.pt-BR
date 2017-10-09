---
title: "Visão geral de Balanceador de carga de aaaInternal | Microsoft Docs"
description: "Visão geral do balanceador de carga interno e seus recursos. Como um balanceador de carga funciona para pontos de extremidade interno do Azure e possíveis cenários tooconfigure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a>Visão geral do balanceador de carga interno

Ao contrário de saudação Internet oposta balanceador de carga balanceador de carga interno (ILB) do hello direciona tooresources somente do tráfego dentro de serviço de nuvem hello ou usando VPN tooaccess Olá infraestrutura do Azure. infraestrutura de saudação restringe acesso toohello com balanceamento de carga endereços IP virtual (VIPs) de um serviço de nuvem ou uma rede Virtual para que eles nunca será o ponto de extremidade do tooan diretamente expostos à Internet. Isso permite interno de linha de negócios (LOB) toorun de aplicativos no Azure e ser acessado de dentro da nuvem de saudação ou dos recursos locais.

## <a name="why-you-may-need-an-internal-load-balancer"></a>Por que talvez seja necessário balanceador de carga interno

O ILB (Balanceamento de Carga Interno) do Azure fornece balanceamento de carga entre máquinas virtuais que residem em um serviço de nuvem ou em uma rede virtual com escopo regional. Para obter informações sobre o uso de saudação e a configuração de redes virtuais com um escopo regional, consulte [redes virtuais regionais](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) em Olá blog do Azure. Redes virtuais existentes configuradas para um grupo de afinidade não podem usar o ILB.

O ILB permite Olá seguintes tipos de balanceamento de carga:

* Dentro de um serviço de nuvem de máquinas virtuais tooa conjunto de máquinas virtuais que residem dentro de saudação mesmo serviço de nuvem (consulte a Figura 1).
* Em uma rede virtual, de máquinas virtuais no conjunto de tooa Olá rede virtual de máquinas virtuais que residem dentro de saudação mesmo serviço de nuvem do hello virtual de rede (consulte a Figura 2).
* Para uma rede virtual entre locais, de conjunto de tooa de computadores no local de máquinas virtuais que residem dentro de saudação mesmo serviço de nuvem do hello virtual de rede (consulte a Figura 3).
* Aplicativos voltados para Internet, multicamados no qual as camadas de back-end de saudação não estão conectados à Internet mas exigem balanceamento de carga para tráfego de camada do hello voltado para a Internet.
* Balanceamento de carga para aplicativos LOB (linha de negócios) hospedados no Azure sem exigir hardware ou software do balanceador de carga adicional. Incluindo servidores locais no conjunto de saudação de computadores cujo tráfego tem a carga balanceada.

## <a name="internet-facing-multi-tier-applications"></a>Aplicativos para a Internet de diversas camadas

camada da web de saudação tem pontos de extremidade com acesso à Internet para clientes de Internet e é parte de um conjunto com balanceamento de carga. o balanceador de carga Olá distribui o tráfego dos clientes da web para TCP porta 443 (HTTPS) toohello servidores web.

servidores de banco de dados de saudação estejam por trás de um ponto de extremidade ILB que usam servidores de web Olá para armazenamento. Essa carga de serviço do banco de dados com balanceamento de ponto de extremidade, o tráfego tem a carga balanceada entre servidores de banco de dados Olá Olá ILB conjunto.

Olá imagem mostra a seguir Olá aplicativo multicamadas da Internet em Olá mesmo serviço de nuvem.

![Serviço de nuvem único de balanceamento de carga interno](./media/load-balancer-internal-overview/IC736321.png)

Figura 1 – Aplicativo para a Internet de várias camadas

Outro uso possíveis para um aplicativo de várias camado é quando Olá ILB implantado tooa serviço de nuvem diferente de Olá um serviço Olá consumidor para Olá ILB.

Nuvem serviços usando Olá mesma rede virtual será necessário acessam o ponto de extremidade do toohello ILB. Olá seguindo a imagem mostra servidores web front-end estão em um serviço de nuvem diferente de saudação de banco de dados back-end e usando Olá pontos de extremidade ILB Olá mesma rede virtual.

![Balanceamento de carga interno entre serviços de nuvem](./media/load-balancer-internal-overview/IC744147.png)

Figura 2 – Servidores front-end em um serviço de nuvem diferente

## <a name="intranet-line-of-business-applications"></a>Aplicativos de linha de negócios intranet

Tráfego de clientes na rede local de saudação obter com balanceamento de carga em conjunto de saudação de servidores LOB usando a rede de tooAzure de conexão VPN.

máquina de cliente Olá terá acesso tooan endereço IP do serviço de VPN do Azure usando VPN de ponto toosite. Ele permite Olá use Olá aplicativo LOB hospedado por trás do ponto de extremidade do hello ILB.

![Usando VPN de ponto toosite de balanceamento de carga interno](./media/load-balancer-internal-overview/IC744148.png)

Figura 3: aplicativos LOB hospedados por trás de ponto de extremidade Olá LB

Outro cenário para Olá LOB é toohave uma toosite VPN toohello rede virtual site onde o ponto de extremidade do hello ILB está configurado. Isso permite que o local rede tráfego roteado de toobe toohello ILB ponto de extremidade.

![Usando o site toosite VPN de balanceamento de carga interno](./media/load-balancer-internal-overview/IC744150.png)

Figura 4 - o tráfego de rede local roteada toohello ILB ponto de extremidade

## <a name="limitations"></a>Limitações

As configurações do Balanceador de Carga Interno não dão suporte a SNAT. Olá o contexto deste documento, SNAT refere-se tooport com origem NAT.  Isso se aplica a tooscenarios onde uma VM em um pool de Balanceador de carga precisa de endereço IP de front-end do tooreach Olá respectivos interno balanceador de carga. Não há suporte para cenário no balanceador de carga interno. Falhas de Conexão ocorrerá quando o fluxo de saudação é com balanceamento de carga toohello VM originado fluxo Olá. Você deve usar um balanceador de carga de estilo de proxy para esses cenários.

## <a name="next-steps"></a>Próximas etapas

[Suporte do Azure Resource Manager para o Azure Load Balancer](load-balancer-arm.md)

[Introdução à configuração de um balanceador de carga para a Internet](load-balancer-get-started-internet-arm-ps.md)

[Introdução à configuração de um balanceador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurar um modo de distribuição do balanceador de carga](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
