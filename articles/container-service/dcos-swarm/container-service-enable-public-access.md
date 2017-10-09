---
title: "o aplicativo de contêiner do aaaEnable access tooAzure DC/sistema operacional | Microsoft Docs"
description: "Como público tooenable acessar contêineres tooDC/sistema operacional no serviço de contêiner do Azure."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a>Habilitar o aplicativo de serviço de contêiner do Azure tooan acesso público
Qualquer contêiner de DC/OS em Olá ACS [pool de agente pública](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) é exposto automaticamente toohello internet. Por padrão, as portas **80**, **443**, **8080** estão abertas e qualquer contêiner (público) que esteja ouvindo nessas portas estará acessível. Este artigo mostra como tooopen mais portas para seus aplicativos no serviço de contêiner do Azure.

## <a name="open-a-port-portal"></a>Abrir uma porta (portal)
Primeiro, precisamos de porta de saudação tooopen que desejamos.

1. Faça logon no portal de toohello.
2. Grupo de recursos de saudação localizar implantado Olá serviço de contêiner do Azure.
3. Selecione o balanceador de carga do agente de saudação (que é chamado semelhante muito**agente XXXX-XXXX lb**).
   
    ![Balanceador de carga do serviço de contêiner do Azure](./media/container-service-enable-public-access/agent-load-balancer.png)
4. Clique em **Investigações** e então em **Adicionar**.
   
    ![Investigações do balanceador de carga do serviço de contêiner do Azure](./media/container-service-enable-public-access/add-probe.png)
5. Preencha o formulário de investigação de saudação e clique em **Okey**.
   
   | Campo | Descrição |
   | --- | --- |
   | Nome |Um nome descritivo da investigação de saudação. |
   | Porta |porta Olá Olá tootest de contêiner. |
   | Caminho |(Quando estiver no modo de HTTP) Olá tooprobe de caminho relativo do site. Não há suporte para HTTPS. |
   | Intervalo |quantidade de saudação de tempo entre a investigação tentativas, em segundos. |
   | Limite não íntegro |Número de investigação consecutivas tentativas antes de considerar o contêiner de saudação não íntegro. |
6. Volta na propriedades Olá Olá agente do balanceador de carga, clique em **regras de balanceamento de carga** e **adicionar**.
   
    ![Regras do balanceador de carga do serviço de contêiner do Azure](./media/container-service-enable-public-access/add-balancer-rule.png)
7. Preencha o formulário de Balanceador de carga hello e clique em **Okey**.
   
   | Campo | Descrição |
   | --- | --- |
   | Nome |Um nome descritivo saudação do balanceador de carga. |
   | Porta |porta de entrada de saudação pública. |
   | Porta de back-end |porta de público interno Olá Olá contêiner tooroute do tráfego de para. |
   | Pool de back-end |contêineres de saudação do pool será o destino de saudação para este balanceador de carga. |
   | Investigação |Olá toodetermine investigação usada se um destino em Olá **pool de back-end** está íntegro. |
   | Persistência de sessão |Determina como o tráfego de um cliente deve ser tratado durante Olá Olá sessão de.<br><br>**Nenhum**: solicitações sucessivas do mesmo cliente pode ser tratado por qualquer contêiner de saudação.<br>**Cliente IP**: Olá de solicitações sucessivas do hello mesmo IP do cliente são manipuladas pelo mesmo contêiner.<br>**Cliente IP e protocolo**: Olá de solicitações sucessivas do hello a mesma combinação de IP e protocolo de cliente são manipuladas pelo mesmo contêiner. |
   | Tempo limite de ociosidade |(Somente TCP) Em minutos, Olá tookeep tempo abrir um cliente TCP/HTTP sem depender de *keep-alive* mensagens. |

## <a name="add-a-security-rule-portal"></a>Adicionar uma regra de segurança (portal)
Em seguida, precisamos tooadd uma regra de segurança que roteia o tráfego de nosso porta aberta por meio de firewall de saudação.

1. Faça logon no portal de toohello.
2. Grupo de recursos de saudação localizar implantado Olá serviço de contêiner do Azure.
3. Selecione Olá **pública** grupo de segurança de rede do agente (que é chamado semelhante muito**XXXX-agente-público-nsg-XXXX**).
   
    ![Grupo de segurança de rede do serviço de contêiner do Azure](./media/container-service-enable-public-access/agent-nsg.png)
4. Selecione **Regras de segurança de entrada** e **Adicionar**.
   
    ![Regras do grupo de segurança de rede do serviço de contêiner do Azure](./media/container-service-enable-public-access/add-firewall-rule.png)
5. Insira a porta pública Olá tooallow de regra de firewall e clique em **Okey**.
   
   | Campo | Descrição |
   | --- | --- |
   | Nome |Um nome descritivo Olá de regra de firewall. |
   | Prioridade |Classificação de prioridade para a regra de saudação. Olá inferior Olá número Olá Olá prioridade. |
   | Fonte |Restringir Olá entrada IP endereço intervalo toobe permitido ou negado por essa regra. Use **qualquer** toonot especificam uma restrição. |
   | O Barramento de |Selecione um conjunto de serviços predefinidos para os quais foi definida essa regra de segurança. Caso contrário, use **personalizado** toocreate seus próprios. |
   | Protocolo |Restrinja o tráfego baseado em **TCP** ou **UDP**. Use **qualquer** toonot especificam uma restrição. |
   | Intervalo de portas |Quando **Service** é **personalizado**, especifica o intervalo de saudação de portas que essa regra afeta. Você pode usar uma única porta, como **80** ou um intervalo, como **1024–1500**. |
   | Ação |Permitir ou negar o tráfego que atenda aos critérios de saudação. |

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre a diferença de saudação entre [públicos e privados agentes de DC/OS](container-service-dcos-agents.md).

Leia mais informações sobre [como gerenciar seus contêineres de DC/OS](container-service-mesos-marathon-ui.md).

