---
title: "Leiame do ambiente de serviço de aplicativo aaaAzure"
description: "Lista a saudação documentação que descreve o ambiente de serviço de aplicativo do Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 77452413-5193-4762-8b3d-5fa8e4edf1ca
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 6edc74804ded7497e70c31c9e08252257add4415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a>Documentação do ambiente do Serviço de Aplicativo
 Um Ambiente do Serviço de Aplicativo do Azure é um recurso do Serviço de Aplicativo do Azure que fornece um ambiente totalmente isolado e dedicado a executar com segurança os aplicativos do Serviço de Aplicativo em grande escala. Esse recurso pode hospedar os [aplicativos Web][webapps], [aplicativos móveis][mobileapps], [aplicativos de API][APIApps] e [funções][Functions].

Os ASE (Ambientes de Serviço de Aplicativo) são ideais para cargas de trabalho de aplicativos que exijam:

* Uma escala muito alta.
* Isolamento e acesso seguro à rede.

Os clientes podem criar vários ASEs dentro de uma única região do Azure, bem como entre várias regiões do Azure. Essa versatilidade torna os ASEs ideais para escalar horizontalmente camadas de aplicativo sem estado para dar suporte a cargas de trabalho RPS altas.

ASs são isolado toorunning apenas os aplicativos de um único cliente e sempre são implantados em uma rede virtual do Azure. Os clientes têm controle refinado sobre o tráfego de rede do aplicativo de entrada e saída usando os [Grupos de Segurança de Rede][NSGs]. Aplicativos também podem estabelecer conexões seguras de alta velocidade sobre recursos corporativos de tooon locais de redes virtuais.

Aplicativos normalmente precisam de recursos corporativos tooaccess, como bancos de dados internos e serviços da web. Os aplicativos executados em ASEs podem acessar recursos por meio de conexões VPN [site a site][SiteToSite] e [Azure ExpressRoute][ExpressRoute].

* [O que é um Ambiente do Serviço de Aplicativo?][Intro]
* [Criar um ambiente de serviço de aplicativo][MakeExternalASE]
* [Criar um ambiente do Serviço de Aplicativo de balanceador de carga interno][MakeILBASE]
* [Usar um ambiente do Serviço de Aplicativo][UsingASE]
* [Considerações de rede e hello ambiente de serviço de aplicativo][ASENetwork]
* [Criar um ambiente do Serviço de Aplicativo de um modelo][MakeASEfromTemplate]


## <a name="videos"></a>Vídeos
Mestre moderno PaaS para Olá Enterprise com o serviço de aplicativo do Azure
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

Implantando aplicativos altamente escalonáveis e seguros
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

Executando aplicativos Enterprise Web e móveis no Serviço de Aplicativo do Azure
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a>Ambiente do Serviço de Aplicativo v1 ##
Há duas versões do Ambiente do Serviço de Aplicativo: ASEv1 e ASEv2. Para obter informações sobre ASEv1, confira a [documentação do Ambiente do Serviço de Aplicativo v1][ASEv1README].


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[ASEv1README]: ../app-service-app-service-environments-readme.md
[SiteToSite]: ../../vpn-gateway/vpn-gateway-site-to-site-create.md
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
