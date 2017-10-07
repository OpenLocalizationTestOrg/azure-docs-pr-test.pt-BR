---
title: "ambientes de serviço de aplicativo do aaaIntroduction tooAzure"
description: "Uma breve visão geral sobre os ambientes do Serviço de Aplicativo do Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 3c7eaefa-1850-4643-8540-428e8982b7cb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 9261041333cf59374974a039edf89c4983c45cdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environments"></a>Ambientes de serviço tooApp de Introdução #
 
## <a name="overview"></a>Visão geral ##

Um Ambiente do Serviço de Aplicativo do Azure é um recurso do Serviço de Aplicativo do Azure que fornece um ambiente totalmente isolado e dedicado a executar com segurança os aplicativos do Serviço de Aplicativo em grande escala. Essa funcionalidade pode hospedar os [aplicativos Web][webapps], [aplicativos móveis][mobileapps], [aplicativos de API][APIapps] e [funções][Functions].

Os ASEs (Ambientes do Serviço de Aplicativo) são apropriados para cargas de trabalho de aplicativos que exijam:

- Escala muito alta.
- Isolamento e acesso à rede segura.
- Alta utilização de memória.

Os clientes podem criar vários ASEs dentro de uma única região do Azure, bem como entre várias regiões do Azure. Isso torna os ASEs ideais para escalar horizontalmente camadas de aplicativo sem monitoração de estado para dar suporte a cargas de trabalho RPS altas.

ASs são isolado toorunning apenas os aplicativos de um único cliente e sempre são implantados em uma rede virtual. Os clientes têm controle refinado sobre o tráfego de rede de entrada e de saída do aplicativo. Aplicativos podem estabelecer conexões seguras de alta velocidade sobre os recursos corporativos VPNs tooon local.

Todos os artigos e como-tooinstructions sobre ASs estão disponíveis em Olá [Leiame para ambientes de serviço de aplicativo][ASEReadme]:

* Os ASEs permitem a hospedagem de aplicativos de grande escala com acesso à rede segura. Para obter mais informações, consulte Olá [mergulho profundo AzureCon](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) em ASs.
* Vários ASs podem ser usado tooscale horizontalmente. Para obter mais informações, consulte [como tooset backup de um volume de aplicativo distribuído geograficamente](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/).
* ASs podem ser usado tooconfigure arquitetura de segurança, conforme mostrado no hello mergulho profundo AzureCon. toosee como a arquitetura de segurança Olá mostrada no hello mergulho profundo AzureCon foi configurada, consulte Olá [artigo sobre como tooimplement uma arquitetura de segurança em camadas](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security) com ambientes de serviço de aplicativo.
* Os aplicativos executados nos ASEs podem ter seu acesso restrito por dispositivos upstream como WAFs (firewalls do aplicativo Web). Para saber mais, confira [Configurar um WAF para ambientes do Serviço de Aplicativo](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall).

## <a name="dedicated-environment"></a>Ambiente dedicado ##

É uma ASE dedicado exclusivamente tooa única assinatura e podem hospedar 100 instâncias. intervalo de saudação pode abranger 100 instâncias em um único planos de serviço de aplicativo do serviço de aplicativo plano too100 instância única e todos os aspectos.

Um ASE é composto de funções de trabalho e front-ends. Os front-ends são responsáveis pela terminação HTTP/HTTPS, bem como pelo balanceamento de cargas automático de solicitações do aplicativo em um ASE. Front-ends são automaticamente adicionados como Olá planos de serviço de aplicativo no hello ASE são dimensionados.

As funções de trabalho são funções que hospedam aplicativos cliente. As funções de trabalho estão disponíveis em três tamanhos fixos:

* Um núcleo/3,5 GB de RAM
* Dois núcleos/7 GB de RAM
* Quatro núcleos/14 GB de RAM

Os clientes não precisam trabalhadores e toomanage front-ends. Toda a infraestrutura é adicionada automaticamente cconforme os clientes dimensionam os planos de Serviço do Aplicativo. Como a criação ou expandidos em uma ASE planos do serviço de aplicativo, Olá necessário infraestrutura é adicionada ou removida conforme apropriado.

Há uma taxa mensal simples para uma ASE paga a infraestrutura de saudação e não são alterados com tamanho de saudação do hello ASE. Além disso, há um custo por núcleo do plano do Serviço do Aplicativo. Todos os aplicativos hospedados em uma ASE estão em hello isolado preços SKU. Para obter informações sobre preços para uma ASE, consulte Olá [preços do serviço de aplicativo] [ Pricing] página e examine as opções disponíveis de saudação para ASs.

## <a name="virtual-network-support"></a>Suporte de rede virtual ##

Um ASE pode ser criado apenas em uma rede virtual do Azure Resource Manager. toolearn mais sobre redes virtuais do Azure, consulte Olá [perguntas Frequentes de redes virtuais do Azure](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/). Um ASE sempre existe em uma rede virtual e mais precisamente, dentro de uma sub-rede de uma rede virtual. Você pode usar os recursos de segurança de saudação do redes virtuais toocontrol de entrada e saída comunicações para seus aplicativos de rede.

Um ASE pode ser voltado para a Internet com um endereço IP público ou voltado para o interior com apenas um endereço de ILB (balanceador de carga Interno) do Azure.

[Grupos de segurança de rede] [ NSGs] restringir a sub-rede de toohello de comunicações de rede de entrada onde uma ASE reside. Você pode usar os NSGs toorun aplicativos atrás de upstream dispositivos e serviços como WAFs e provedores de SaaS de rede.

Aplicativos frequentemente necessário tooaccess a recursos corporativos, como bancos de dados internos e serviços da web. Se você implantar Olá ASE em uma rede virtual que tenha uma rede de local de toohello de conexão VPN, aplicativos Olá Olá ASE podem acessar recursos de locais de saudação. Esse recurso é verdadeiro independentemente de é Olá VPN um [site a site](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/) ou [rota expressa do Azure](http://azure.microsoft.com/services/expressroute/) VPN.

Para obter mais informações sobre o funcionamento dos ASEs com redes virtuais e redes locais, consulte [Considerações de rede do Ambiente do Serviço de Aplicativo][ASENetwork].

## <a name="app-service-environment-v1"></a>Ambiente do Serviço de Aplicativo v1 ##

O Ambiente do Serviço de Aplicativo tem duas versões: ASEv1 e ASEv2. Olá informações anteriores foi baseado em ASEv2. Este mostra seção Olá diferenças entre ASEv1 e ASEv2. 

Em ASEv1, é necessário toomanage todos os recursos de Olá manualmente. Isso inclui front-ends hello, funcionários e endereços IP usados para SSL baseado em IP. Antes de você pode dimensionar seu plano de serviço de aplicativo, você precisa toofirst expandir pool do trabalhador Olá onde você deseja toohost-lo.

O ASEv1 usa um modelo de preço diferente do ASEv2. No ASEv1, você paga por cada núcleo alocado. Isso inclui os núcleos usados para front-ends ou funções de trabalho que não hospedam nenhuma carga de trabalho. Em ASEv1, tamanho de máximo escala saudação padrão de uma ASE é 55 total de hosts. Isso inclui funções de trabalho e front-ends. Um tooASEv1 de vantagem é que ele pode ser implantado em uma rede virtual clássica e uma rede virtual do Gerenciador de recursos. toolearn mais sobre ASEv1, consulte [introdução do ambiente de serviço de aplicativo v1][ASEv1Intro].

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
