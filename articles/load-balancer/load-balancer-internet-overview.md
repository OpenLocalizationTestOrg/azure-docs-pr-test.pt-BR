---
title: "aaaInternet voltado para a visão geral do balanceador de carga | Microsoft Docs"
description: "Visão geral do balanceador de carga para a Internet e seus recursos. Como um balanceador de carga funciona no Azure usando máquinas virtuais e serviços de nuvem."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a>Visão geral do balanceador de carga para a Internet

Balanceador de carga do Azure mapeia Olá público IP endereço e número da porta de entrada tráfego toohello privado IP endereço e número da porta da máquina virtual de saudação e vice-versa para o tráfego de resposta de saudação da máquina virtual de saudação. Regras de balanceamento de carga permitem que você toodistribute a tipos específicos de tráfego entre várias máquinas virtuais ou serviços. Por exemplo, você pode distribuir a carga de saudação do tráfego de solicitação da web em vários servidores web ou funções da web.

Para um serviço de nuvem que contém as instâncias de funções web ou funções de trabalho, você pode definir um ponto de extremidade público no arquivo de definição (. csdef) do serviço de saudação.

Olá *servicedefinition. csdef* arquivo contém a configuração de ponto de extremidade hello e quando você tiver várias instâncias de função para uma implantação de função web ou de trabalho, o balanceador de carga Olá será instalado para ele. implantação em nuvem Olá maneira tooadd instâncias tooyour é alterar a contagem de instâncias de saudação do arquivo de configuração de serviço hello (. csfg).

Olá figura a seguir mostra um ponto de extremidade com balanceamento de carga no tráfego da web que é compartilhado entre três máquinas virtuais para Olá pública e privada a porta TCP 80. Essas três máquinas virtuais estão em um conjunto de balanceamento de carga.

![exemplo de balanceador de carga público](./media/load-balancer-internet-overview/IC727496.png)

Figura 1 – Ponto de extremidade com balanceamento de carga para tráfego da Web

Quando os clientes da Internet enviam solicitações de página da web toohello de endereço IP público do serviço de nuvem Olá na porta TCP 80, Olá balanceador de carga do Azure distribui as solicitações de saudação entre Olá três máquinas virtuais em conjunto com balanceamento de carga de saudação. Para obter mais informações sobre algoritmos de Balanceador de carga, consulte Olá [página de visão geral do balanceador de carga](load-balancer-overview.md#load-balancer-features).

Por padrão, Azure Load Balancer distribui o tráfego de rede igualmente entre várias instâncias da máquina virtual. Também é possível configurar a afinidade de sessão. Para obter mais informações, consulte [load balancer distribution mode (modo de distribuição do balanceador de carga)](load-balancer-distribution-mode.md).

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre [balanceador de carga interno](load-balancer-internal-overview.md) toobetter entender qual balanceador de carga é uma escolha melhor para sua implantação de nuvem.

Também é possível [começar a criar um balanceador de carga para a Internet](load-balancer-get-started-internet-arm-ps.md) e configurar o tipo de [modo de distribuição](load-balancer-distribution-mode.md) para um comportamento específico de tráfego de rede do balanceador de carga.

Se seu aplicativo precisa tookeep conexões ativo para os servidores atrás de um balanceador de carga, você pode saber mais sobre [ocioso configurações de tempo limite TCP para um balanceador de carga](load-balancer-tcp-idle-timeout.md). Ele ajudará toolearn sobre o comportamento de conexão ociosa, quando você estiver usando um balanceador de carga do Azure.
