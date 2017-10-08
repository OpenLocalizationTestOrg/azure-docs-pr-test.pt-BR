---
title: "aaaIntroduction tooApp v1 do ambiente de serviço"
description: "Saiba mais sobre o recurso de saudação v1 do ambiente de serviço de aplicativo que fornece unidades de escala, segura e unida a rede virtual dedicado para executar todos os seus aplicativos."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 78e6d4f5-da46-4eb5-a632-b5fdc17d2394
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 6e3cd1909b241887b5ec19412b9f7884d870cc3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environment-v1"></a>Introdução tooApp v1 do ambiente de serviço

> [!NOTE]
> Este artigo é sobre Olá v1 do ambiente de serviço de aplicativo.  Há uma versão mais recente do hello ambiente de serviço de aplicativo que é mais fácil toouse e é executado na infraestrutura mais avançada. toolearn mais sobre a nova versão de hello começam com hello [Introdução toohello ambiente de serviço de aplicativo](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Visão geral
Um Ambiente de Serviço de Aplicativo é uma opção de plano de serviço [Premium][PremiumTier] do Serviço de Aplicativo do Azure que fornece um ambiente totalmente isolado e dedicado para executar com segurança todos os seus aplicativos do Serviço de Aplicativo do Azure em alta escala, incluindo [Aplicativos Web][WebApps], [Aplicativos Móveis][MobileApps] e [Aplicativos de API][APIApps].  

Os Ambientes de Serviço de Aplicativo são ideais para cargas de trabalho de aplicativos que exigem:

* Escala muito alta
* Isolamento e acesso seguro à rede

Os clientes podem criar vários Ambientes de Serviço de Aplicativo dentro de uma única região do Azure, bem como entre várias regiões do Azure.  Isso faz dos Ambientes de Serviço de Aplicativo ideais para dimensionar horizontalmente camadas de aplicativo sem estado para dar suporte a cargas de trabalho RPS altas.

Ambientes de serviço de aplicativo são isolado toorunning apenas os aplicativos de um único cliente e sempre são implantados em uma rede virtual.  Os clientes têm um controle refinado sobre os tráfegos de rede aplicativo de entrada e saída e aplicativos podem estabelecer conexões seguras de alta velocidade sobre recursos corporativos de tooon locais de redes virtuais.

Todos os artigos e como-a do sobre ambientes de serviço de aplicativo estão disponíveis no hello [Leiame para ambientes de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).

Para uma visão geral de como os ambientes de serviço de aplicativo habilitar alta escala e proteger o acesso de rede, consulte Olá [mergulho profundo AzureCon] [ AzureConDeepDive] em ambientes de serviço de aplicativo!

Para uma análise aprofundada sobre a expansão horizontal usando vários ambientes de serviço de aplicativo consulte artigo Olá sobre como toosetup uma [base do aplicativo distribuído geograficamente][GeodistributedAppFootprint].

toosee como a arquitetura de segurança Olá mostrada no hello mergulho profundo AzureCon foi configurada, consulte o artigo Olá sobre como implementar um [em camadas de arquitetura de segurança](app-service-app-service-environment-layered-security.md) com ambientes de serviço de aplicativo.

Os aplicativos executados nos Ambientes do Serviço de Aplicativo podem ter seu acesso restrito por dispositivos upstream como WAF (firewalls do aplicativo Web).  artigo Olá [Configurando um WAF para ambientes de serviço de aplicativo](app-service-app-service-environment-web-application-firewall.md) abrange neste cenário. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a>Recursos de computação dedicados
Todos de computação Olá recursos em um ambiente de serviço de aplicativo são dedicados exclusivamente tooa única assinatura e um ambiente de serviço de aplicativo pode ser configurado com os recursos de computação toofifty (50) para uso exclusivo por um único aplicativo.

Um ambiente de serviço de aplicativo é composto de um pool de recursos de computação de front-end, bem como pools de recursos de computação um toothree trabalho. 

pool de front-end Olá contém recursos de computação responsáveis pela terminação de SSL, como também balanceamento automático de carga de solicitações de aplicativo em um ambiente de serviço de aplicativo. 

Cada pool de trabalho contém recursos de computação alocados muito[planos de serviço de aplicativo][AppServicePlan], que por sua vez contêm um ou mais aplicativos de serviço de aplicativo do Azure.  Como pode haver até toothree pools de trabalho diferente em um ambiente de serviço de aplicativo, você tem recursos de computação diferente de toochoose Olá flexibilidade para cada pool de trabalho.  

Por exemplo, isso permite que você toocreate pool de um trabalho com menos avançados recursos de computação para planos de serviço de aplicativo se destina para teste ou desenvolvimento de aplicativos.  Um segundo (ou até mesmo terceiro) pool de trabalho de pode usar recursos de computação mais poderosos para planos de serviço de aplicativo executando aplicativos de produção.

Para obter mais detalhes sobre a quantidade de saudação do toohello disponíveis de recursos de computação front-end e de grupos de trabalho, consulte [como um ambiente de serviço de aplicativo de tooConfigure][HowToConfigureanAppServiceEnvironment].  

Para obter detalhes sobre Olá disponível calcular tamanhos de recursos com suporte em um ambiente de serviço de aplicativo, consulte Olá [preços do serviço de aplicativo] [ AppServicePricing] página e examine Olá de opções disponíveis para ambientes de serviço de aplicativo na camada de preços de Premium Olá.

## <a name="virtual-network-support"></a>Suporte a Rede Virtual
Um Ambiente do Serviço de Aplicativo pode ser criado **ou** em uma rede virtual do Azure Resource Manager, **ou** em uma rede virtual do modelo de implantação clássico ([mais informações sobre redes virtuais][MoreInfoOnVirtualNetworks]).  Como um ambiente de serviço de aplicativo sempre existe em uma rede virtual e com mais precisão em uma sub-rede de uma rede virtual, você pode aproveitar os recursos de segurança de saudação do redes virtuais toocontrol ambas as comunicações de rede de entrada e saída.  

Um Ambiente de Serviço de Aplicativo pode ser voltado para a Internet com um endereço IP público ou voltado para o interior com apenas um endereço ILB (Balanceador de Carga Interno).

Você pode usar [grupos de segurança de rede] [ NetworkSecurityGroups] toorestrict sub-rede toohello comunicações onde reside um ambiente de serviço de aplicativo de entrada.  Isso permite que aplicativos toorun por trás de upstream dispositivos e serviços, como firewalls de aplicativo web e provedores de SaaS de rede.

Aplicativos frequentemente necessário tooaccess a recursos corporativos, como bancos de dados internos e serviços da web.  Uma abordagem comum é toomake essas tráfego de rede disponível toointernal somente pontos de extremidade que fluem em uma rede virtual do Azure.  Depois que um ambiente de serviço de aplicativo é toohello unida mesma rede virtual que serviços internos hello, os aplicativos em execução no ambiente de saudação pode acessá-los, incluindo pontos de extremidade pode ser acessados via [Site a Site] [ SiteToSite]e [Azure ExpressRoute] [ ExpressRoute] conexões.

Para obter mais detalhes sobre o funcionamento dos ambientes de serviço de aplicativo com redes virtuais e redes locais Consulte Olá artigos a seguir [arquitetura de rede][NetworkArchitectureOverview], [controle de entrada Tráfego][ControllingInboundTraffic], e [uma conexão segura tooBackends][SecurelyConnectingToBackends]. 

## <a name="getting-started"></a>Introdução
tooget iniciado com ambientes de serviço de aplicativo, consulte [como tooCreate um ambiente de serviço de aplicativo][HowToCreateAnAppServiceEnvironment]

Todos os artigos e como-para para ambientes de serviço de aplicativo estão disponíveis no hello [Leiame para ambientes de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).

Para obter mais informações sobre a plataforma do serviço de aplicativo do Azure hello, consulte [do serviço de aplicativo do Azure][AzureAppService].

Para obter uma visão geral de saudação arquitetura de rede do ambiente de serviço de aplicativo, consulte Olá [visão geral da arquitetura de rede] [ NetworkArchitectureOverview] artigo.

Para obter detalhes sobre o uso de um ambiente de serviço de aplicativo com o ExpressRoute, consulte Olá artigo a seguir [rota expressa e ambientes de serviço de aplicativo][NetworkConfigDetailsForExpressRoute].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[MoreInfoOnVirtualNetworks]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePlan]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[LogicApps]: http://azure.microsoft.com/documentation/articles/app-service-logic-what-are-logic-apps/
[AzureConDeepDive]:  https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/
[GeodistributedAppFootprint]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[HowToConfigureanAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[ControllingInboundTraffic]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SecurelyConnectingToBackends]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NetworkArchitectureOverview]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[NetworkConfigDetailsForExpressRoute]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 

<!-- IMAGES -->


