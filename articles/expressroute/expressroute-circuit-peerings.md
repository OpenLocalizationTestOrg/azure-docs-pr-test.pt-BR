---
title: "aaaAzure ExpressRoute circuitos e domínios de roteamento | Microsoft Docs"
description: "Esta página fornece uma visão geral de circuitos de rota expressa e domínios de roteamento de saudação."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6f0c5d8e-cc60-4a04-8641-2c211bda93d9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 1d43cbf668accdd7aa4efb053ea1e9027d10e4a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-circuits-and-routing-domains"></a>Circuitos do ExpressRoute e domínios de roteamento
 Você deve solicitar uma *circuito de rota expressa* tooconnect sua tooMicrosoft de infraestrutura local por meio de um provedor de conectividade. a Figura Olá abaixo fornece uma representação lógica de conectividade entre sua WAN e da Microsoft.

![](./media/expressroute-circuit-peerings/expressroute-basic.png)

## <a name="expressroute-circuits"></a>Circuitos do ExpressRoute
Um *circuito do ExpressRoute* representa uma conexão lógica entre a infraestrutura local e os serviços de nuvem da Microsoft por meio de um provedor de conectividade. É possível solicitar vários circuitos do ExpressRoute. Cada circuito pode ser em Olá mesmas ou em diferentes regiões, e pode ser conectado tooyour local por meio de provedores diferentes de conectividade. 

Circuitos de rota expressa não mapeiem entidades físicas tooany. Um circuito é identificado exclusivamente por um GUID padrão chamado de chave de serviço (s-key). chave de serviço de saudação é Olá única informação trocadas entre a Microsoft, o provedor de conectividade hello e você. Olá s-chave não é um segredo para fins de segurança. Há um mapeamento 1:1 entre um circuito de rota expressa e hello s-key.

Um circuito de rota expressa pode ter até emparelhamentos independentes toothree: privada do Azure de pública, o Azure e a Microsoft. Cada emparelhamento é um par de sessões BGP independente, cada uma delas configurada de modo redundante para alta disponibilidade. Há um mapeamento de 1:N (1 <= N <= 3) entre um circuito do ExpressRoute e os domínios de roteamento. Um circuito do ExpressRoute pode ter qualquer tipo de emparelhamento (um, dois ou os três) habilitado por circuito do ExpressRoute.

Cada circuito tem uma largura de banda fixa (50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, 1 Gbps, 10 Gbps) e provedor de conectividade tooa mapeadas e um local de emparelhamento. largura de banda Olá que selecionar é compartilhada entre todos os emparelhamentos de saudação para o circuito de saudação. 

### <a name="quotas-limits-and-limitations"></a>Cotas, limites e limitações
Cotas e limites padrão aplicam-se a todos os circuitos do ExpressRoute. Consulte toohello [assinatura do Azure e limites de serviço, cotas e restrições](../azure-subscription-service-limits.md) página para obter informações atualizadas sobre as cotas.

## <a name="expressroute-routing-domains"></a>Domínios de roteamento do ExpressRoute
Um circuito do ExpressRoute tem vários domínios de roteamento associados a ele: público do Azure, privado do Azure e Microsoft. Cada um dos domínios de roteamento Olá é configurada de forma idêntica em um par de roteadores (ativa ou compartilhamento de carga configuration) para alta disponibilidade. Os serviços do Azure estão categorizados como *público do Azure* e *privada do Azure* toorepresent Olá esquemas de endereçamento IP.

![](./media/expressroute-circuit-peerings/expressroute-peerings.png)

### <a name="private-peering"></a>Emparelhamento privado
Ou seja, as máquinas virtuais (IaaS), os serviços de computação do Azure e serviços de nuvem (PaaS), que são implantados em uma rede virtual podem ser conectados por meio do domínio de emparelhamento privado hello. domínio de emparelhamento particular Olá é considerado toobe uma extensão confiável de sua rede principal para o Microsoft Azure. Você pode configurar a conectividade bidirecional entre sua rede principal e as redes virtuais (VNets) do Azure. Esse emparelhamento permite conectar toovirtual máquinas e serviços diretamente em seus endereços IP privados de nuvem.  

Você pode se conectar a mais de uma rede virtual toohello emparelhamento domínio particular. Saudação de revisão [página de perguntas Frequentes](expressroute-faqs.md) para obter informações sobre limites e as limitações. Você pode visitar Olá [assinatura do Azure e limites de serviço, cotas e restrições](../azure-subscription-service-limits.md) página para obter informações atualizadas sobre os limites.  Consulte toohello [roteamento](expressroute-routing.md) página para obter informações detalhadas sobre a configuração de roteamento.

### <a name="public-peering"></a>Emparelhamento público
Serviços como o Armazenamento do Azure, Sites e Bancos de dados SQL são oferecidos em endereços IP públicos. Em particular, você pode conectar tooservices hospedados em endereços IP públicos, incluindo VIPs dos serviços de nuvem, por meio do domínio de roteamento emparelhamento público hello. Você pode se conectar Olá pública emparelhamento domínio tooyour DMZ e conecte-se tooall Azure Olá de serviços em seus endereços IP públicos de sua WAN sem a necessidade de tooconnect por meio da internet. 

Conectividade sempre é iniciada de seu tooMicrosoft WAN do Azure services. Serviços do Microsoft Azure não será capaz de tooinitiate conexões em sua rede por meio deste domínio de roteamento. Após habilitar o emparelhamento público, será capaz de tooconnect tooall do Azure services. Não permitir que tooselectively serviços de coleta para o qual estamos anunciar rotas para. Você pode revisar Olá lista de prefixos que anunciar tooyou por esse emparelhamento Olá [intervalos de IP de Datacenter do Microsoft Azure](http://www.microsoft.com/download/details.aspx?id=41653) página. página de saudação é atualizada semanalmente.

Você pode definir filtros de rota personalizados em seu tooconsume somente Olá rotas de rede que é necessário. Consulte toohello [roteamento](expressroute-routing.md) página para obter informações detalhadas sobre a configuração de roteamento. 

Consulte Olá [página de perguntas Frequentes](expressroute-faqs.md) para obter mais informações sobre serviços de suporte por meio do domínio de roteamento emparelhamento público hello. 

### <a name="microsoft-peering"></a>Emparelhamento da Microsoft
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

Conectividade tooall outros serviços online da Microsoft (como serviços do Office 365) será por meio de emparelhamento da Microsoft hello. Habilitar a conectividade bidirecional entre os serviços de nuvem WAN e da Microsoft por meio do domínio de roteamento emparelhamento da Microsoft de saudação. Você deve se conectar a serviços de nuvem tooMicrosoft somente em endereços IP públicos pertencentes a você ou seu provedor de conectividade e é preciso cumprir as regras de saudação definida tooall. Consulte Olá [pré-requisitos do ExpressRoute](expressroute-prerequisites.md) para obter mais informações.

Consulte Olá [página de perguntas Frequentes](expressroute-faqs.md) para obter mais informações sobre serviços de suporte, os custos e detalhes de configuração. Consulte Olá [locais de rota expressa](expressroute-locations.md) página para obter informações sobre a lista de saudação de provedores de conectividade oferece suporte de emparelhamento da Microsoft.

## <a name="routing-domain-comparison"></a>Comparação de domínios de roteamento
tabela de saudação abaixo compara três domínios de roteamento hello.

|  | **Emparelhamento privado** | **Emparelhamento público** | **Emparelhamento da Microsoft** |
| --- | --- | --- | --- |
| **Número máximo de prefixos com suporte por emparelhamento** |4000 por padrão, 10.000 com o ExpressRoute Premium |200 |200 |
| **Intervalos de endereços IP com suporte** |Todos os endereços IPv4 válidos em sua WAN. |Os endereços IPv4 públicos pertencentes a você ou ao seu provedor de conectividade. |Os endereços IPv4 públicos pertencentes a você ou ao seu provedor de conectividade. |
| **Requisitos do número do AS** |Números públicos e privados do AS. Você deve possuir o hello pública como número, se você escolher toouse um. |Números públicos e privados do AS. No entanto, você deve comprovar a propriedade de endereços IP públicos. |Números públicos e privados do AS. No entanto, você deve comprovar a propriedade de endereços IP públicos. |
| **Roteando endereços IP de interface** |RFC1918 e endereços IP públicos |Tooyou registrado no roteamento de registros de endereços de IP público. |Tooyou registrado no roteamento de registros de endereços de IP público. |
| **Suporte a Hash MD5** |Sim |Sim |Sim |

Você pode escolher tooenable um ou mais dos domínios de roteamento hello como parte do seu circuito de rota expressa. Você pode escolher todos os domínios de roteamento Olá colocados em toohave Olá VPN mesmo se você quiser toocombine-los em um único domínio de roteamento. Você também pode colocá-los em diferentes domínios de roteamentos, diagrama de toohello semelhante. Olá recomendado de configuração é que o emparelhamento privado é conectado diretamente toohello Central de rede e Olá público e links de emparelhamento da Microsoft são conectados tooyour DMZ.

Se você escolher toohave todos os três sessões de emparelhamento, você deve ter três pares de sessões BGP (um par para cada tipo de emparelhamento). pares de sessão BGP Olá fornecem um link altamente disponível. Se estiver conectando por meio de provedores de conectividade da camada 2, você será responsável por configurar e gerenciar o roteamento. Você pode saber mais, revisando Olá [fluxos de trabalho](expressroute-workflows.md) para configurar a rota expressa.

## <a name="next-steps"></a>Próximas etapas
* Encontrar um provedor de serviços. Consulte [Locais e provedores de serviços do ExpressRoute](expressroute-locations.md).
* Verifique se todos os pré-requisitos foram atendidos. Consulte [Pré-requisitos do ExpressRoute](expressroute-prerequisites.md).
* Configurar sua conexão do ExpressRoute.
  * [Criar e gerenciar circuitos de ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md)
  * [Configurar o roteamento (emparelhamento) para circuitos ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)

