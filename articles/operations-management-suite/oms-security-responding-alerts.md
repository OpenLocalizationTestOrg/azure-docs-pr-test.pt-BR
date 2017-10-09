---
title: "aaaMonitoring e respondendo tooSecurity alertas no Operations Management Suite solução de segurança e auditoria | Microsoft Docs"
description: "Este documento ajuda você toouse Olá threat intelligence opção disponível no OMS segurança e auditoria toomonitor e responde a alertas de toosecurity."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 7d45a32b-1341-4bb5-a436-1f42a8a2590a
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/13/2017
ms.author: yurid
ms.openlocfilehash: 3d92b6809b7bd934c889afc119e5e34ff2b85f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-responding-toosecurity-alerts-in-operations-management-suite-security-and-audit-solution"></a>Monitorar e responder a alertas toosecurity no Operations Management Suite solução de segurança e auditoria
Este documento ajuda você a usar a opção de inteligência de ameaça Olá disponível no OMS segurança e auditoria toomonitor e responder a alertas de toosecurity.

## <a name="what-is-oms"></a>O que é o OMS?
O OMS (Microsoft Operations Management Suite) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda a gerenciar e proteger sua infraestrutura local e de nuvem. Para obter mais informações sobre o OMS, leia o artigo de saudação [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="threat-intelligence"></a>Inteligência contra ameaças
Em um ambiente corporativo em que os usuários tem acesso amplo toohello rede e usar uma variedade de dispositivos tooconnect toocorporate dados, é fundamental que você pode monitorar ativamente os recursos e responder rapidamente toosecurity incidentes. Isso é determinado importante da perspectiva de ciclo de vida de segurança Olá porque alguns segurança cibernética ameaças não podem gerar alertas ou atividades suspeitas que podem ser identificadas por controles técnicos tradicionais de segurança. 

Usando Olá **inteligência de ameaça** opção disponíveis no OMS segurança e auditoria, os administradores de TI pode identificar ameaças de segurança em ambiente hello, por exemplo, identificar se um determinado computador fizer parte de um [ botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection). Computadores podem ser nós em uma botnet quando os invasores forma ilícita instalar malware que secretamente se conecta a esse comando de toohello do computador e o controle. Ela também pode identificar ameaças potenciais recebidas de canais de comunicação underground, como [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents). 

Em ordem toobuild essa inteligência de ameaça, o OMS segurança e auditoria usar dados provenientes de várias fontes em Microsoft. OMS segurança e auditoria utilizará esse dados tooidentify possíveis ameaças em seu ambiente.

Painel de inteligência de ameaça Olá é composto por três principais opções:

* Servidores com o tráfego de saída mal-intencionado
* Tipos de ameaças detectados
* Mapa de inteligência contra ameaças

> [!NOTE]
> para obter uma visão geral de todas essas opções, leia [Introdução à solução de Segurança e Auditoria do Operations Management Suite](oms-security-getting-started.md).
> 
> 

### <a name="responding-toosecurity-alerts"></a>Respondendo a alertas de toosecurity
Uma das etapas de saudação de um [resposta a incidentes segurança](https://technet.microsoft.com/library/cc512623.aspx) processo é tooidentify severidade Olá Olá comprometimento do sistema. Nesta fase, você deve executar Olá tarefas a seguir:

* Determinar a natureza de saudação do ataque Olá
* Determinar o ponto de ataque de saudação de origem
* Determine a intenção de saudação do ataque hello. Olá ataque foi direcionado especificamente em informações específicas de tooacquire sua organização, ou foi aleatório?
* Identificar os sistemas de saudação que tem sido comprometidos
* Identificar arquivos Olá que foram acessados e determinam a confidencialidade Olá desses arquivos

Você pode aproveitar **inteligência de ameaça** informações toohelp de solução de segurança da OMS e auditoria essas tarefas. Siga as etapas de saudação abaixo tooaccess isso **inteligência de ameaça** opções:

1. Em Olá **Microsoft Operations Management Suite** clique de painel principal **segurança e auditoria** lado a lado.
   
    ![Segurança e Auditoria](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. Em Olá **segurança e auditoria** painel, você verá Olá **inteligência de ameaça** opções na direita hello, conforme mostrado abaixo:
   
    ![Threat Intel](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

Esses três blocos oferecem uma visão geral de ameaças de saudação atual. Em Olá **servidor com tráfego malicioso de saída** será capaz de tooidentify se houver qualquer computador que você está monitorando (dentro ou fora da sua rede) que é enviar tráfego mal-intencionado toohello da Internet. 

Olá **detectado tipos de ameaças** bloco mostra um resumo de ameaças Olá atual "no Olá curinga", se você clicar nesse bloco você verá mais detalhes sobre essas ameaças como é mostrado abaixo:

![Tipos de ameaças detectados](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

É possível extrair mais informações sobre cada ameaça clicando nela. exemplo Hello abaixo mostra mais detalhes sobre Botnet:

![mais detalhes sobre uma ameaça](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

Conforme descrito no começo desta seção hello, essas informações podem ser muito útil durante um caso de resposta a incidentes. Ele também pode ser importante durante uma investigação forense, onde você precisa de fonte de saudação do toofind de ataque hello, qual sistema foi comprometido e Olá da linha do tempo. Nesse relatório, você pode identificar facilmente alguns detalhes importantes sobre ataque hello, tais como: Olá a origem do ataque hello, Olá IP local que foi comprometido e Olá estado da sessão atual da conexão de saudação. 

Olá **mapa de inteligência de ameaça** ajudará você a tooidentify Olá locais atuais em todo o mundo de saudação que têm o tráfego mal-intencionado. Há laranja (entrada) e (saídas) setas vermelhas neste mapa que identificam a direção do tráfego hello, se você clicar em um dessas setas, ele mostrará tipo hello de ameaça e hello direção de tráfego, conforme mostrado abaixo:

![mapa do threat intel](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> Você pode ver uma demonstração sobre como toouse esse recurso durante a resposta a incidentes processo observando apresentação Olá [reduzir as ameaças de segurança do datacenter com investigação interativa usando o Operations Management Suite](https://myignite.microsoft.com/videos/5000) entregue no Microsoft Ignite.
> 

### <a name="responding-toodistinct-malicious-ip-accessed"></a>Respondendo toodistinct IP mal-intencionados acessado
Em alguns cenários, você pode observar um potencial IP mal-intencionado que foi acessado de um computador monitorado:

![mapa do threat intel](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Este alerta e outros em Olá mesma categoria, são gerados por meio da segurança do OMS, aproveitando [Microsoft Threat Intelligence](https://youtu.be/O4WtxgUrDc8). Olá dados de inteligência de ameaça é coletada pela Microsoft, bem como adquirido dos principais provedores de inteligência de ameaça. Esses dados forem atualizados frequentemente e adaptada movendo toofast ameaças. Devido a natureza tooits, ele deve ser combinado com outras fontes de informações de segurança ao [investigando](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) um alerta de segurança. 

## <a name="customize-alerts-received-via-e-mail"></a>Personalizar alertas recebidos via email

Você pode personalizar quais usuários em sua organização serão notificados quando os alertas de segurança forem disparados pela Segurança do OMS. Essa opção está disponível em Visão geral / Olá de configurações no painel do OMS:

![Email](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig7.png)

## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu como Olá toouse **inteligência de ameaça** opção no OMS segurança e auditoria solução toorespond toosecurity os alertas. toolearn mais sobre a segurança do OMS, consulte Olá artigos a seguir:

* [Operations Management Suite (OMS) overview](operations-management-suite-overview.md)
* [Introdução à solução de Segurança e Auditoria do Operations Management Suite](oms-security-getting-started.md)
* [Monitorando recursos na solução de Segurança e Auditoria do Operations Management Suite](oms-security-monitoring-resources.md)

