---
title: "Visão geral de arquitetura do aplicativo serviço ambientes de aaaNetwork"
description: "Visão geral da arquitetura da topologia de rede dos Ambientes de Serviço de Aplicativo."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 13d03a37-1fe2-4e3e-9d57-46dfb330ba52
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 3cbc86883f5687a9ada35a3ab2f577a450a3fa0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="network-architecture-overview-of-app-service-environments"></a>Visão geral da arquitetura de rede dos Ambientes de Serviço de Aplicativo
## <a name="introduction"></a>Introdução
Ambientes de serviço de aplicativo sempre são criados em uma sub-rede de um [rede virtual] [ virtualnetwork] -aplicativos em execução em um ambiente de serviço de aplicativo podem se comunicar com privada pontos de extremidade localizado dentro de saudação mesmo virtual topologia de rede.  Desde que os clientes podem bloquear partes de sua infraestrutura de rede virtual, é importante toounderstand tipos de saudação de fluxos de comunicação de rede que ocorrem com um ambiente de serviço de aplicativo.

## <a name="general-network-flow"></a>Fluxo de rede geral
Quando um Ambiente de Serviço de Aplicativo (ASE) usa um endereço IP virtual (VIP) público para aplicativos, todo o tráfego de entrada chega nesse VIP público.  Isso inclui o tráfego HTTP e HTTPS para aplicativos, bem como outro tráfego para FTP, funcionalidade de depuração remota e operações de gerenciamento do Azure.  Para obter uma lista completa de saudação portas específicas (necessárias e opcionais) que estão disponíveis no VIP público Olá consulte o artigo de saudação em [controlando o tráfego de entrada] [ controllinginboundtraffic] tooan ambiente de serviço de aplicativo. 

Ambientes de serviço de aplicativo também dão suporte a executar aplicativos que estão associados somente tooa virtual rede endereço interno, também chamado tooas um endereço ILB (balanceador de carga interno).  Em um ILB tráfego ASE, HTTP e HTTPS habilitado para aplicativos, bem como as chamadas remotas de depuração, chegarem Olá endereço ILB.  Para configurações mais comuns do ASE ILB, tráfego de FTP/FTPS também chegará em Olá endereço ILB.  No entanto as operações de gerenciamento do Azure ainda fluirá tooports 454/455 em Olá o VIP público de um ILB habilitado ASE.

Olá diagrama a seguir mostra uma visão geral da saudação diversos fluxos de rede de entrada e saída para um ambiente de serviço de aplicativo que os aplicativos de saudação são associados tooa público endereço IP virtual:

![Fluxos de rede geral][GeneralNetworkFlows]

Um Ambiente de Serviço de Aplicativo pode se comunicar com uma variedade de pontos de extremidade privados do cliente.  Por exemplo, os aplicativos executados em Olá que ambiente de serviço de aplicativo pode se conectar a servidores toodatabase em execução em máquinas virtuais no Olá mesma topologia de rede virtual.

> [!IMPORTANT]
> Examinar o diagrama de rede hello, Olá "outras computação recursos" são implantados em uma sub-rede diferente do hello ambiente de serviço de aplicativo. Implantando recursos em Olá a mesma sub-rede com hello ASE bloqueará conectividade com recursos de toothose ASE (com exceção de roteamento específico intra-ASE). Implantar tooa sub-rede diferente em vez disso, (em Olá mesma rede virtual). Olá ambiente de serviço de aplicativo será capaz de tooconnect. Nenhuma configuração adicional é necessária.
> 
> 

Os Ambientes de Serviço de Aplicativo também se comunicam com recursos do Banco de Dados SQL e Armazenamento do Azure necessários para gerenciar e operar um Ambiente de Serviço de Aplicativo.  Alguns dos recursos de armazenamento e Sql Olá que um ambiente de serviço de aplicativo se comunica com estão localizados em Olá Olá ambiente de serviço de aplicativo, enquanto outros estão localizados em regiões do Azure remotos mesma região.  Como resultado, conectividade de saída toohello Internet é sempre necessária para um ambiente de serviço de aplicativo toofunction corretamente. 

Como um ambiente de serviço de aplicativo é implantado em uma sub-rede, grupos de segurança de rede podem ser usado toocontrol sub-rede de toohello de tráfego de entrada.  Para obter detalhes sobre como toocontrol entrada tráfego tooan ambiente de serviço de aplicativo, consulte o seguinte Olá [artigo][controllinginboundtraffic].

Para obter detalhes sobre como tooallow saída conectividade com a Internet de um ambiente de serviço de aplicativo, consulte Olá após o artigo sobre como trabalhar com [rota expressa][ExpressRoute].  Olá mesma abordagem descrita no artigo Olá se aplica ao trabalhar com conectividade Site a Site e usando o túnel forçado.

## <a name="outbound-network-addresses"></a>Endereços de rede de saída
Quando um ambiente de serviço de aplicativo faz chamadas de saída, um endereço IP é sempre associado a todas as chamadas realizadas hello.  endereço IP específico Olá usado depende se o ponto de extremidade de hello está sendo chamado está localizado dentro de topologia de rede virtual hello, ou fora de topologia de rede virtual hello.

Se o ponto de extremidade hello está sendo chamado **fora** da topologia de rede virtual hello, Olá saído endereço (também conhecido como Olá saída NAT) que é usado é o VIP público Olá Olá ambiente de serviço de aplicativo.  Esse endereço pode ser encontrado na interface de usuário do portal de Olá para Olá ambiente de serviço de aplicativo na folha de propriedades.

![Endereço IP de saída][OutboundIPAddress]

Esse endereço também pode ser determinado para ASs que têm apenas um VIP público, criando um aplicativo em Olá ambiente de serviço de aplicativo e, em seguida, executar uma *nslookup* no endereço de saudação do aplicativo. endereço IP resultante Olá é tanto VIP público hello, como endereço NAT da saída do ambiente de serviço de aplicativo hello.

Se o ponto de extremidade hello está sendo chamado **dentro de** da topologia de rede virtual hello, endereço de saída de saudação do aplicativo de chamada hello serão endereço IP interno de Olá Olá individuais do recurso de computação executando o aplicativo hello.  No entanto não há um mapeamento persistente de tooapps de endereços IP internos rede virtual.  Aplicativos podem se mover entre os recursos de computação diferentes e pool de saudação de recursos de computação disponíveis em um ambiente de serviço de aplicativo pode alterar devido a operações de tooscaling.

No entanto, como um ambiente de serviço de aplicativo sempre está localizado em uma sub-rede, é garantida que endereço IP interno de saudação de um recurso de computação executando um aplicativo será sempre está no intervalo CIDR de saudação da sub-rede hello.  Como resultado, quando ACLs refinadas ou grupos de segurança de rede são usados toosecure acessar pontos de extremidade tooother na rede virtual hello, Olá intervalo de sub-rede com toobe de necessidades de ambiente de serviço de aplicativo hello concedeu acesso.

Olá diagrama a seguir mostra esses conceitos mais detalhadamente:

![Endereços de rede de saída][OutboundNetworkAddresses]

Em Olá acima diagrama:

* Como o VIP público Olá Olá ambiente de serviço de aplicativo é 192.23.1.2, que é o endereço IP saído Olá usado ao fazer chamadas muito pontos de extremidade de "Internet".
* Olá intervalo CIDR de saudação contendo a sub-rede para Olá ambiente de serviço de aplicativo é 10.0.1.0/26.  Outros pontos de extremidade em Olá a mesma infraestrutura de rede virtual verá chamadas de aplicativos como originados em algum lugar dentro desse intervalo de endereços.

## <a name="calls-between-app-service-environments"></a>Chamadas entre Ambientes de Serviço de Aplicativo
Um cenário mais complexo que pode ocorrer se você implantar vários ambientes de serviço de aplicativo hello mesma rede virtual e fazer chamadas de saída de um ambiente de serviço de aplicativo tooanother ambiente de serviço de aplicativo.  Esses tipos de chamadas entre Ambientes de Serviço de Aplicativo também serão tratadas como chamadas de "Internet".

Olá diagrama a seguir mostra um exemplo de uma arquitetura em camadas com aplicativos em um ambiente de serviço de aplicativo (por exemplo Aplicativos web de "Porta da frente") chamando aplicativos em um ambiente de serviço de aplicativo segundo (por exemplo, aplicativos de API back-end internos não se destina toobe acessível de saudação da Internet). 

![Chamadas entre Ambientes de Serviço de Aplicativo][CallsBetweenAppServiceEnvironments] 

No hello exemplo acima hello "ASE um" ambiente de serviço de aplicativo tem um endereço IP de saída de 192.23.1.2.  Se um aplicativo em execução nesse ambiente de serviço de aplicativo faz um chamada de saída tooan aplicativo em execução em um segundo aplicativo ambiente de serviço ("ASE dois") localizados em Olá mesmo virtual de rede, hello saída chamada será tratada como uma chamada de "Internet".  Assim que chegam a saudação de tráfego de rede Olá segundo ambiente de serviço de aplicativo mostrará como provenientes de 192.23.1.2 (ou seja, não Olá sub-rede intervalo de endereços de Olá primeiro ambiente de serviço de aplicativo).

Embora chamadas entre diferentes ambientes de serviço de aplicativo são tratadas como chamadas de "Internet", quando ambos os ambientes de serviço de aplicativo estão localizados em Olá mesmo tráfego de rede de saudação de região do Azure permanece na rede do Azure regional de saudação e não fisicamente fluirá sobre Olá Internet pública.  Como resultado, você pode usar um grupo de segurança de rede na sub-rede de saudação do hello segundo ambiente de serviço de aplicativo tooonly permitir chamadas recebidas de Olá primeiro aplicativo ambiente de serviço (cujo endereço IP de saída é 192.23.1.2), garantindo, assim, a comunicação segura entre hello Ambientes de serviço de aplicativo.

## <a name="additional-links-and-information"></a>Informações e links adicionais
Todos os artigos e como-para para ambientes de serviço de aplicativo estão disponíveis no hello [Leiame para ambientes de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).

Obter detalhes sobre portas usadas pelos ambientes de serviço de aplicativo de entrada e toocontrol de grupos de segurança de rede usando o tráfego de entrada está disponível [aqui][controllinginboundtraffic].

Detalhes sobre o uso definidos pelo usuário rotas toogrant saída Internet acesso tooApp ambientes de serviço está disponível neste [artigo][ExpressRoute]. 

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[controllinginboundtraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[ExpressRoute]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/

<!-- IMAGES -->
[GeneralNetworkFlows]: ./media/app-service-app-service-environment-network-architecture-overview/NetworkOverview-1.png
[OutboundIPAddress]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundIPAddress-1.png
[OutboundNetworkAddresses]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundNetworkAddresses-1.png
[CallsBetweenAppServiceEnvironments]: ./media/app-service-app-service-environment-network-architecture-overview/CallsBetweenEnvironments-1.png

