---
title: Requisitos do ExpressRoute de aaaQoS | Microsoft Docs
description: "Esta página fornece requisitos detalhados para a configuração e gerenciamento de QoS para circuitos do ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a>Requisitos de QoS para o ExpressRoute
Skype for Business tem várias cargas de trabalho que exigem tratamento de QoS diferenciado. Se você planejar serviços de voz tooconsume por meio de rota expressa, você deve seguir toohello requisitos descritos abaixo.

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> Requisitos de QoS se aplica a toohello emparelhamento da Microsoft somente. valores de DSCP Olá em seu tráfego de rede recebido no emparelhamento público do Azure e emparelhamento particular do Azure será too0 de redefinição. 
> 
> 

Olá tabela a seguir fornece uma lista de marcações de DSCP usado pelo Skype for Business. Consulte também[gerenciamento de QoS para o Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) para obter mais informações.

| **Classe de Tráfego** | **Tratamento (Marcação DSCP)** | **Cargas de Trabalho do Skype for Business** |
| --- | --- | --- |
| **Voz** |EF (46) |Voz do Skype / Lync |
| **Interativo** |AF41 (34) |Vídeo, VBSS |
| AF21 (18) |Compartilhamento de aplicativo | |
| **Padrão** |AF11 (10) |Transferência de arquivo |
| CS0 (0) |Qualquer outra coisa | |

* Você deve classificar as cargas de trabalho de saudação e marcar os valores de DSCP saudação à direita. Siga a orientação Olá fornecida [aqui](https://technet.microsoft.com/library/gg405409.aspx) sobre como as marcações de DSCP tooset em sua rede.
* Você deve configurar e dar suporte a várias filas de QoS em sua rede. Voz deve ser uma classe autônoma e receber o tratamento de EF Olá especificado no RFC 3246. 
* Você pode decidir Olá mecanismo, a política de detecção de congestionamento e alocação de largura de banda por classe de tráfego de enfileiramento de mensagens. Porém, hello DSCP marcando para Skype para cargas de trabalho de negócios deve ser preservado. Se você estiver usando marcas DSCP não listadas acima, por exemplo, AF31 (26), você deve reescrever esse too0 do valor DSCP antes de enviar Olá tooMicrosoft de pacote. Microsoft envia somente pacotes marcados com hello valor DSCP mostrado no hello acima da tabela. 

## <a name="next-steps"></a>Próximas etapas
* Consulte os requisitos de toohello para [roteamento](expressroute-routing.md) e [NAT](expressroute-nat.md).
* Veja a seguir Olá links tooconfigure sua conexão de rota expressa.
  
  * [Criar um circuito do ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Configurar o roteamento](expressroute-howto-routing-classic.md)
  * [Vincular um circuito de rota expressa do tooan de rede virtual](expressroute-howto-linkvnet-classic.md)

