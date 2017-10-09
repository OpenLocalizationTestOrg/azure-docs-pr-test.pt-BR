---
title: aaaAzure perguntas frequentes sobre o rota expressa | Microsoft Docs
description: "Olá perguntas frequentes sobre o rota expressa contém informações sobre suporte para serviços do Azure, custo, dados e conexões, SLA, provedores e locais, largura de banda e detalhes técnicos adicionais."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 09b17bc4-d0b3-4ab0-8c14-eed730e1446e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: c01e83f1497103e2fa85251dce6fb41844e46e9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-faq"></a>Perguntas Frequentes sobre ExpressRoute

## <a name="what-is-expressroute"></a>O que é ExpressRoute?

ExpressRoute é um serviço do Azure que permite a criação de conexões privadas entre os datacenters da Microsoft e a infraestrutura no seu local ou em uma instalação de colocalização. Conexões de rota expressa não passam pela Internet pública e oferecem maior segurança, a confiabilidade hello e velocidades com menor latências de que as conexões típicas pela Internet da saudação.

### <a name="what-are-hello-benefits-of-using-expressroute-and-private-network-connections"></a>Quais são os benefícios de saudação do uso de conexões de rede privada e rota expressa?

Conexões de rota expressa não passam pela Olá Internet pública. Eles oferecem maior segurança, confiabilidade e velocidades com latências inferiores e consistentes que as conexões típicas pela Internet da saudação. Em alguns casos, usando dados de tootransfer de conexões de rota expressa entre dispositivos locais e Azure pode gerar benefícios de custos significativas.

### <a name="where-is-hello-service-available"></a>Onde o serviço hello está disponível?

Consulte esta página para localização de serviço e disponibilidade: [Locais e Parceiros do ExpressRoute](expressroute-locations.md).

### <a name="how-can-i-use-expressroute-tooconnect-toomicrosoft-if-i-dont-have-partnerships-with-one-of-hello-expressroute-carrier-partners"></a>Como usar a rota expressa tooconnect tooMicrosoft se eu não tenho parcerias com um dos parceiros de rota expressa operadora Olá?

Você pode selecionar uma operadora regional e levadas tooone de conexões Ethernet de intercâmbio de saudação suportada locais do provedor. Depois, você pode emparelhar com a Microsoft no local do provedor de saudação. Verificar Olá última seção [ExpressRoute parceiros e locais](expressroute-locations.md) toosee se seu provedor de serviços estiver presente em qualquer um dos locais do exchange hello. Em seguida, você pode ordenar um circuito de rota expressa por meio de saudação serviço provedor tooconnect tooAzure.

### <a name="how-much-does-expressroute-cost"></a>Quanto custa o ExpressRoute?

Consulte [detalhes de preços](https://azure.microsoft.com/pricing/details/expressroute/) para obter informações a respeito.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-hello-vpn-connection-i-purchase-from-my-network-service-provider-have-toobe-hello-same-speed"></a>Se eu pagar por um circuito ExpressRoute de uma determinada largura de banda, Olá conexão VPN que adquiri junto do meu provedor de serviços de rede tem toobe Olá mesma velocidade?

Não. Você pode comprar uma conexão VPN de qualquer velocidade de seu provedor de serviços. No entanto, sua conexão tooAzure é a largura de banda do toohello limitado rota expressa circuito que você comprar.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-hello-ability-tooburst-up-toohigher-speeds-if-necessary"></a>Se eu pagar por um circuito ExpressRoute de uma determinada largura de banda, é necessário Olá capacidade tooburst backup toohigher velocidades se necessário?

Sim. Circuitos ExpressRoute são configurado tooallow você tooburst tootwo horas Olá limite de largura de banda adquirido sem nenhum custo adicional. Verifique com seu toosee do provedor de serviços se eles oferecem suporte a esse recurso.

### <a name="can-i-use-hello-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a>É possível usar Olá mesmo privada rede conexão com a rede virtual e outros serviços do Azure simultaneamente?

Sim. Um circuito de rota expressa, uma vez configurado, permite que você tooaccess serviços em uma rede virtual e outros serviços do Azure simultaneamente. Você se conectar redes toovirtual ao longo do caminho de emparelhamento privado hello e tooother serviços pelo caminho de emparelhamento público hello.

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a>o ExpressRoute oferece um SLA (contrato de nível de serviço)?

Para obter informações, consulte Olá [ExpressRoute SLA](https://azure.microsoft.com/support/legal/sla/) página.

## <a name="supported-services"></a>Serviços com suporte

O ExpressRoute dá suporte a [três domínios de roteamento](expressroute-circuit-peerings.md) para vários tipos de serviço.

### <a name="private-peering"></a>Emparelhamento privado

* Redes virtuais, incluindo todas as máquinas virtuais e serviços de nuvem

### <a name="public-peering"></a>Emparelhamento público

* Power BI
* Dynamics 365 for Finance and Operations (anteriormente conhecido como Dynamics AX Online)
* A maioria das hello Azure services com hello algumas exceções a seguir:
  * CDN
  * Teste de carga do Visual Studio Team Services
  * Autenticação Multifator
  * Gerenciador de Tráfego

### <a name="microsoft-peering"></a>Emparelhamento da Microsoft

* [Office 365](http://aka.ms/ExpressRouteOffice365)
* Aplicativos de Dynamics 365 Customer Engagement (anteriormente conhecidos como o CRM Online)
  * Dynamics 365 for Sales
  * Dynamics 365 for Customer Service
  * Dynamics 365 for Field Service
  * Dynamics 365 for Project Service

## <a name="data-and-connections"></a>Dados e conexões

### <a name="are-there-limits-on-hello-amount-of-data-that-i-can-transfer-using-expressroute"></a>Há limites na quantidade de saudação de dados que eu posso transferir usando o ExpressRoute?

Nós não estabelecemos um limite na quantidade de saudação de transferência de dados. Consulte também[detalhes de preços](https://azure.microsoft.com/pricing/details/expressroute/) para obter informações sobre taxas de largura de banda.

### <a name="what-connection-speeds-are-supported-by-expressroute"></a>Quais velocidades de conexão têm suporte pelo ExpressRoute?

Ofertas de largura de banda com suporte:

50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, 1 Gbps, 2 Gbps, 5 Gbps e 10 Gbps

### <a name="which-service-providers-are-available"></a>Que provedores de serviços estão disponíveis?

Consulte [ExpressRoute parceiros e locais](expressroute-locations.md) para lista de saudação de provedores de serviços e locais.

## <a name="technical-details"></a>Detalhes técnicos

### <a name="what-are-hello-technical-requirements-for-connecting-my-on-premises-location-tooazure"></a>Quais são os requisitos técnicos de saudação para conectar meu tooAzure de local no local?

Consulte a [Página de pré-requisitos para ExpressRoute](expressroute-prerequisites.md) para requisitos.

### <a name="are-connections-tooexpressroute-redundant"></a>Conexões tooExpressRoute são redundantes?

Sim. Cada circuito ExpressRoute tem um par redundante de várias conexões configuradas tooprovide alta disponibilidade.

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a>Eu perderei a conectividade se um dos meus links de ExpressRoute falhar?

Você não perderá conectividade se uma de saudação entre conexões falhar. Uma conexão redundante é carga de saudação toosupport disponível da rede. Além disso, você pode criar vários circuitos em uma outro emparelhamento local tooachieve resiliência contra falhas.

### <a name="onep2plink"></a>Se eu não estiver localizada em uma troca de nuvem e meu provedor de serviços oferece conexão ponto a ponto, é necessário tooorder duas conexões físicas entre minha rede local e a Microsoft?

Se seu provedor de serviços pode estabelecer dois circuitos de Ethernet virtuais sobre conexão física hello, você só precisa de uma conexão física. Olá conexão física (por exemplo, uma fibra ótica) é encerrado em uma camada 1 (L1) dispositivo (consulte a imagem de saudação). circuitos virtuais de Ethernet Olá dois são marcados com diferentes IDs de VLAN, uma para o circuito de primária Olá e outra para Olá secundário. As IDs de VLAN estão no cabeçalho de Ethernet olá 802.1 q externa. cabeçalho de Ethernet olá 802.1 q interna (não mostrado) é mapeado tooa específico [domínio de roteamento de rota expressa](expressroute-circuit-peerings.md).

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-tooazure-using-expressroute"></a>Posso estender uma das minha tooAzure VLANs usando o ExpressRoute?

Não. Não há suporte para extensões de conectividade de camada 2 ao Azure.

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a>Posso ter mais de um circuito de ExpressRoute em minha assinatura?

Sim. Você pode ter mais de um circuito de ExpressRoute em sua assinatura. limite de padrão de saudação é definido too10. Você pode contatar o limite de saudação do Microsoft Support tooincrease, se necessário.

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a>Posso ter circuitos de ExpressRoute de diferentes provedores de serviços?

Sim. Você pode ter circuitos de ExpressRoute de muitos provedores de serviços. Cada circuito de ExpressRoute é associado apenas a um provedor de serviços. 

### <a name="can-i-have-multiple-expressroute-circuits-in-hello-same-location"></a>Posso ter vários circuitos de rota expressa em Olá mesmo local?

Sim. Você pode ter vários circuitos de rota expressa, com hello mesmo ou Olá de provedores de serviço diferentes no mesmo local. No entanto, você não pode vincular mais de um toohello de circuito de rota expressa mesmo virtual de rede de saudação mesmo local.

### <a name="how-do-i-connect-my-virtual-networks-tooan-expressroute-circuit"></a>Como se conectar meu circuito de rota expressa do tooan de redes virtuais

etapas básicas de saudação são:

* Estabelecer um circuito de rota expressa e ter o provedor de serviços de saudação habilitá-lo.
* Você ou o provedor de hello, configure Olá BGP emparelhamento (s).
* Vincule um circuito de rota expressa em toohello Olá rede virtual.

Para obter mais informações, consulte [Fluxos de trabalho do ExpressRoute para provisionamento e estados do circuito](expressroute-workflows.md).

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a>Existem limites de conectividade para meu circuito de ExpressRoute?

Sim. Olá [ExpressRoute parceiros e locais](expressroute-locations.md) artigo fornece uma visão geral dos limites de conectividade de saudação para um circuito de rota expressa. Conectividade para um circuito de rota expressa é limitado tooa única região geopolíticas. Conectividade pode ser regiões geopolíticas toocross expandido habilitando o recurso de premium Olá rota expressa.

### <a name="can-i-link-toomore-than-one-virtual-network-tooan-expressroute-circuit"></a>Posso vincular toomore que uma rede virtual tooan circuito ExpressRoute?

Sim. Você pode ter too10 conexões de redes virtuais em um circuito de rota expressa padrão e o too100 em um [circuito de rota expressa premium](#expressroute-premium). 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-tooa-single-expressroute-circuit"></a>Tenho várias assinaturas do Azure que contêm redes virtuais. Posso conectar redes virtuais que estão em assinaturas diferentes tooa único circuito ExpressRoute?

Sim. Você pode autorizar o too10 toouse outras assinaturas do Azure um único circuito ExpressRoute. Esse limite pode ser aumentado habilitando o recurso de premium Olá rota expressa.

Para obter mais informações, consulte [Compartilhando um circuito de ExpressRoute entre várias assinaturas](expressroute-howto-linkvnet-arm.md).

### <a name="are-virtual-networks-connected-toohello-same-circuit-isolated-from-each-other"></a>São redes virtuais toohello conectado mesmo circuito isolado umas das outras?

Não. De um roteamento toohello vinculado de redes de perspectiva, todos os virtuais mesmo circuito de ExpressRoute fazem parte do mesmo domínio de roteamento de hello e não são isoladas uma da outra. Se você precisa de rotear o isolamento, será necessário toocreate um circuito ExpressRoute separado.

### <a name="can-i-have-one-virtual-network-connected-toomore-than-one-expressroute-circuit"></a>Posso ter um toomore de rede virtual conectado que um circuito ExpressRoute?

Sim. Você pode vincular uma única rede virtual com o toofour circuitos do ExpressRoute. Eles devem ser ordenados por meio de quatro [locais diferentes de ExpressRoute](expressroute-locations.md).

### <a name="can-i-access-hello-internet-from-my-virtual-networks-connected-tooexpressroute-circuits"></a>Pode acessar Olá Internet de circuitos de tooExpressRoute conectado Minhas redes virtuais?

Sim. Se você não tenha anunciado rotas padrão (0.0.0.0/0) ou prefixos de rota de Internet por meio da sessão BGP hello, você pode conectar toohello Internet de uma rede virtual vinculada de tooan circuito de rota expressa.

### <a name="can-i-block-internet-connectivity-toovirtual-networks-connected-tooexpressroute-circuits"></a>Posso bloquear Internet conectividade toovirtual redes conectadas tooExpressRoute circuitos?

Sim. Você pode anunciar padrão (0.0.0.0/0) de rotas tooblock todas as máquinas de toovirtual de conectividade de Internet implantado em uma rede virtual e rotear todo o tráfego de saída através do circuito de rota expressa hello.

Se você anunciar rotas padrão, Forçamos tooservices tráfego oferecido pela pública local tooyour back emparelhamento (como o armazenamento do Azure e banco de dados SQL). Você terá tooconfigure seu tooAzure de tráfego roteadores tooreturn por meio do caminho de emparelhamento público hello ou em Olá da Internet.

### <a name="can-virtual-networks-linked-toohello-same-expressroute-circuit-talk-tooeach-other"></a>Pode toohello vinculado redes virtuais mesmo circuito de rota expressa falar tooeach outros?

Sim. Máquinas virtuais implantadas em redes virtuais toohello conectado mesmo circuito de ExpressRoute pode se comunicar uns com os outros.

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a>Posso usar a conectividade site a site para redes virtuais em conjunto com ExpressRoute?

Sim. O ExpressRoute pode coexistir com VPN dos tipos site a site.

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-toouse-expressroute"></a>Pode mover uma rede virtual da configuração de site a site / ponto a site toouse ExpressRoute?

Sim. Você terá toocreate um gateway de rota expressa na sua rede virtual. Há um pequeno tempo de inatividade associado com o processo de saudação.

### <a name="why-is-there-a-public-ip-address-associated-with-hello-expressroute-gateway-on-a-virtual-network"></a>Por que há um endereço IP público associado Olá gateway de rota expressa em uma rede virtual?

endereço IP público de saudação é usado para gerenciamento interno apenas. Este endereço IP público não é toohello exposto à Internet e não constitui uma exposição de segurança da sua rede virtual.

### <a name="what-do-i-need-tooconnect-tooazure-storage-over-expressroute"></a>O que eu preciso tooconnect tooAzure armazenamento através do ExpressRoute?

Você deve estabelecer um circuito de ExpressRoute e configurar rotas para emparelhamento público.

### <a name="are-there-limits-on-hello-number-of-routes-i-can-advertise"></a>Há limites no número de saudação de rotas que posso anunciar?

Sim. Podemos aceitar too4000 prefixos de rota para emparelhamento privado e 200 para emparelhamento público e emparelhamento da Microsoft. Você pode aumentar esse too10 000 rotas para emparelhamento privado, se você habilitar o recurso de premium Olá rota expressa.

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-hello-bgp-session"></a>Há restrições em intervalos IP que posso anunciar sobre a sessão BGP de Olá?

Não podemos aceitar prefixos privados (RFC1918) na Olá pública e a sessão BGP de emparelhamento Microsoft.

### <a name="what-happens-if-i-exceed-hello-bgp-limits"></a>O que acontece se eu exceder os limites BGP Olá?

As sessões BGP serão interrompidas. Elas serão redefinidas quando a contagem de prefixo de saudação fica abaixo do limite de saudação.

### <a name="what-is-hello-expressroute-bgp-hold-time-can-it-be-adjusted"></a>O que é Olá ExpressRoute BGP mantenha tempo? Pode ser ajustado?

tempo de espera de saudação é 180. mensagens de saudação keep-alive são enviadas a cada 60 segundos. Esses são fixos configurações no hello lado da Microsoft que não pode ser alterado. É possível que você temporizadores diferentes tooconfigure e parâmetros da sessão BGP Olá serão negociados adequadamente.

### <a name="after-i-advertise-hello-default-route-00000-toomy-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-tooi-fix-this"></a>Depois que posso anunciar redes virtuais do toomy saudação padrão rota (0.0.0.0/0), não é possível ativar Windows em execução no meu VMs do Azure. Como tooI corrigir isso?

Olá etapas a seguir ajuda a Azure reconhece a solicitação de ativação de saudação:

1. Estabelece Olá emparelhamento público para o circuito de rota expressa.
2. Executar uma pesquisa DNS e localizar o endereço IP de saudação do **kms.core.windows.net**
3. Olá serviço de gerenciamento de chaves deve reconhecer essa solicitação de ativação hello proveniente do Azure e honrar Olá solicitação. Execute uma saudação três tarefas a seguir:

   * Em sua rede local, Olá rotear o tráfego destinado a saudação endereço IP que você obteve na etapa 2 tooAzure de backup por meio do emparelhamento público do hello.
   * Ter seu NSP provedor forma pin Olá tráfego back tooAzure por meio do emparelhamento público do hello.
   * Criar uma rota definida pelo usuário que IP hello pontos com Internet próximo salto e aplicá-lo sub-redes toohello onde estão as máquinas virtuais.

### <a name="can-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>Posso alterar a largura de banda de saudação de um circuito ExpressRoute?

Sim, você pode tentar tooincrease largura de banda de saudação do seu circuito de rota expressa em Olá portal do Azure, ou usando o PowerShell. Se houver capacidade disponível na porta física hello, no qual o circuito foi criado, sua alteração será bem-sucedida. 

Se sua alteração falhar, isso significa que o não há capacidade suficiente deixado na porta atual hello e precisar toocreate um novo circuito de rota expressa com maior largura de banda de hello, ou que não há nenhuma capacidade adicional nesse local, caso em que você não poderá largura de banda tooincrease hello. 

Você também terá toofollow com seu tooensure do provedor de conectividade que elas sejam atualizadas limitadores Olá no aumento de largura de banda suas redes toosupport hello. No entanto, você não pode reduzir largura de banda de saudação do circuito ExpressRoute. Você toocreate um novo circuito de rota expressa com menos largura de banda e excluir o circuito antigo hello.

### <a name="how-do-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>Como alterar a largura de banda de saudação de um circuito ExpressRoute?

Você pode atualizar a largura de banda de saudação do circuito de rota expressa hello usando Olá API REST ou cmdlet do PowerShell.

## <a name="expressroute-premium"></a>ExpressRoute premium

### <a name="what-is-expressroute-premium"></a>O que é o ExpressRoute Premium?

Rota expressa premium é uma coleção de saudação recursos a seguir:

* Aumenta o limite da tabela de roteamento de 4000 rotas too10, 000 rotas para emparelhamento privado.
* Maior número de VNets que podem ser conectado toohello circuito de rota expressa (o padrão é 10). Para obter mais informações, consulte Olá [limites de rota expressa](#limits) tabela.
* Conectividade tooOffice 365 e Dynamics 365.
* Conectividade global pela rede de núcleo do Microsoft hello. Agora, você pode conectar uma VNet em uma região geopolítica a um circuito de ExpressRoute em outra região.<br>
    **Exemplos:**

    *  Você pode vincular uma rede virtual criada na Europa Ocidental tooan circuito de rota expressa criado no Vale do Silício. 
    *  No emparelhamento público hello, prefixos de outras regiões geopolíticas são publicados, de modo que você pode se conectar, por exemplo, SQL Azure na Europa Ocidental de um circuito no Vale do Silício.


### <a name="limits"></a>Quantos VNets posso vincular circuito de rota expressa tooan se eu habilitado premium de rota expressa?

Olá tabelas a seguir mostram os limites de rota expressa hello e número de Olá de VNets por circuito de rota expressa:

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a>Como habilito o ExpressRoute premium?

Recursos premium de rota expressa podem ser habilitados quando hello está ativado e podem ser desligados por atualizar o estado de circuito hello. Você pode habilitar a rota expressa premium no momento da criação de circuito ou pode chamar a API REST de saudação / cmdlet do PowerShell.

### <a name="how-do-i-disable-expressroute-premium"></a>Como desabilito o ExpressRoute premium?

Você pode desabilitar a rota expressa premium chamando Olá API REST ou cmdlet do PowerShell. Você deve certificar-se de que você tenha dimensionado sua conectividade necessidades toomeet saudação padrão limites antes de desativar a rota expressa premium. Se sua utilização pode ser expandido além dos limites de padrão de saudação, premium de rota expressa Olá solicitação toodisable falhará.

### <a name="can-i-pick-and-choose-hello-features-i-want-from-hello-premium-feature-set"></a>Pode posso escolher recursos Olá desejados do conjunto de recursos premium Olá?

Não. Você não pode escolher os recursos de saudação. Habilitamos todos os recursos quando você ativa o ExpressRoute premium.

### <a name="how-much-does-expressroute-premium-cost"></a>Quanto custa o ExpressRoute premium?

Consulte também[detalhes de preços](https://azure.microsoft.com/pricing/details/expressroute/) custo.

### <a name="do-i-pay-for-expressroute-premium-in-addition-toostandard-expressroute-charges"></a>Eu pago para ExpressRoute premium além toostandard encargos de rota expressa?

Sim. Encargos de premium de rota expressa aplicam sobre encargos de circuito de rota expressa e encargos exigidos pelo provedor de conectividade de saudação.

## <a name="expressroute-for-office-365-and-dynamics-365"></a>ExpressRoute para o Office 365 e o Dynamics 365

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-tooconnect-toooffice-365-services-and-dynamics-365"></a>Como criar um tooconnect de circuito de rota expressa serviços tooOffice 365 e Dynamics 365?

1. Saudação de revisão [página pré-requisitos de rota expressa](expressroute-prerequisites.md) toomake se você atende aos requisitos de saudação.
2. tooensure que precisa de sua conectividade são atendidos, examine Olá lista de provedores de serviços e locais em Olá [ExpressRoute parceiros e locais](expressroute-locations.md) artigo.
3. Planeje seus requisitos de capacidade, revisando [Planejamento de rede e ajuste de desempenho para o Office 365](http://aka.ms/tune/)
4. Execute as etapas de Olá listadas no hello tooset de fluxos de trabalho a conectividade [fluxos de trabalho de rota expressa para provisionamento e estados de circuito](expressroute-workflows.md).

> [!IMPORTANT]
> Certifique-se de que você tenha ativado o complemento do ExpressRoute premium ao configurar serviços de conectividade do tooOffice 365 e Dynamics 365.
> 
> 

### <a name="do-i-need-tooenable-azure-public-peering-tooconnect-toooffice-365-services-and-dynamics-365"></a>É necessário tooenable Azure pública emparelhamento tooconnect tooOffice 365 services e Dynamics 365?

Não, você só precisa tooenable Peering Microsoft. TooAzure de tráfego de autenticação AD é enviado pela Microsoft Peering. 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-toooffice-365-services-and-dynamics-365"></a>Meu circuitos de rota expressa existentes podem dar suporte aos serviços de conectividade tooOffice 365 e Dynamics 365?

Sim. O circuito de rota expressa existente pode ser configurado toosupport conectividade tooOffice 365 services. Certifique-se de que suficiente capacidade tooconnect tooOffice 365 services e que você tenha ativado o complemento premium. [Planejamento da rede e ajuste de desempenho para o Office 365](http://aka.ms/tune/) ajuda você a planejar suas necessidades de conectividade. Veja também [Criar e modificar um circuito do ExpressRoute](expressroute-howto-circuit-classic.md).

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a>Quais serviços do Office 365 podem ser acessados por uma conexão de ExpressRoute?

Consulte também[intervalos de endereços IP e URLs do Office 365](http://aka.ms/o365endpoints) página para uma lista atualizada dos serviços de suporte por meio do ExpressRoute.

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a>Qual é o custo do ExpressRoute para serviços do Office 365 e Dynamics 365?

Serviços do Office 365 e Dynamics 365 exigem premium complemento toobe habilitado. Consulte Olá [página de detalhes de preços](https://azure.microsoft.com/pricing/details/expressroute/) para custos.

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a>Em que regiões há suporte para ExpressRoute para Office 365?

Consulte [Parceiros e locais do ExpressRoute](expressroute-locations.md) para obter mais informações.

### <a name="can-i-access-office-365-over-hello-internet-even-if-expressroute-was-configured-for-my-organization"></a>Posso acessar Office 365 sobre Olá Internet, mesmo se a rota expressa foi configurada para minha organização?

Sim. Pontos de extremidade do Office 365 serviço estão acessíveis por meio de saudação à Internet, mesmo que a rota expressa foi configurada para sua rede. Se você estiver em um local que é configurado tooconnect tooOffice 365 services por meio de rota expressa, você se conecta por meio de rota expressa.

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a>Posso acessar os serviços da Comunidade Governamental dos EUA (GCC) do Office 365 por um circuito ExpressRoute do Governo dos EUA para o Azure?

Sim. Pontos de extremidade de serviço do Office 365 GCC estão acessíveis por meio de saudação US Government rota expressa do Azure. No entanto, você primeiro necessidade tooopen tíquete de suporte em Olá prefixos de saudação tooprovide portal do Azure você pretende tooadvertise tooMicrosoft. Os tooOffice 365 GCC os serviços de conectividade serão estabelecidos depois que o tíquete de suporte Olá é resolvido. 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a>O Dynamics 365 for Operations (anteriormente conhecido como Dynamics AX Online) pode ser acessado por uma conexão do ExpressRoute?

Sim. O [Dynamics 365 for Operations](https://www.microsoft.com/dynamics365/operations) é hospedado no Azure. Você pode habilitar o emparelhamento público do Azure em sua tooit de tooconnect de circuito de rota expressa.

## <a name="route-filters-for-microsoft-peering"></a>Filtros de rota para emparelhamento da Microsoft

### <a name="i-am-turning-on-microsoft-peering-for-hello-first-time-what-routes-will-i-see"></a>Eu estou ativar emparelhamento da Microsoft para Olá primeira vez, quais rotas haverá?

Você não verá nenhuma rota. Você tem tooattach um filtro tooyour circuito toostart prefixo de anúncios de rota. Para obter instruções, consulte [Configurar os filtros de rota para emparelhamento da Microsoft](how-to-routefilter-powershell.md).

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-tooselect-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-toodo-it"></a>Eu ativado emparelhamento da Microsoft e agora estou tentando tooselect Exchange Online, mas ele é mostra um erro que não estou autorizado toodo-lo.

Ao usar filtros de rota, qualquer cliente pode ativar emparelhamento da Microsoft. No entanto, para o consumo de serviços do Office 365, você ainda precisa tooget autorizado pelo Office 365.

### <a name="do-i-need-tooget-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a>É necessário tooget autorização para ativar Dynamics 365 sobre emparelhamento da Microsoft?

Não, você não precisa autorização para Dynamics 365. Você pode criar uma regra e selecionar a comunidade Dynamics 365 sem autorização.

### <a name="i-already-have-microsoft-peering-how-can-i-take-advantage-of-route-filters"></a>Eu já tenho emparelhamento da Microsoft, como posso aproveitar os filtros de rota?

Você pode criar um filtro de rota, serviços Olá selecione desejado toouse e anexar Olá filtro tooyour emparelhamento da Microsoft. Para obter instruções, consulte [Configurar os filtros de rota para emparelhamento da Microsoft](how-to-routefilter-powershell.md).

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-tooenable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a>Tenho Microsoft emparelhamento em um local, agora estou tentando tooenable-lo em outro local e não esteja vendo os prefixos.

* Emparelhamento da Microsoft de circuitos ExpressRoute que foram configurados anterior tooAugust 1, 2017 terá todos os prefixos de serviço anunciados através do emparelhamento da Microsoft, mesmo se os filtros de roteamento não estão definidos.

* Emparelhamento da Microsoft de circuitos de rota expressa configurados em ou após 1 de agosto de 2017 não terá quaisquer prefixos anunciados até que um filtro de rota é anexado toohello circuito. Você não verá nenhum prefixo por padrão.
