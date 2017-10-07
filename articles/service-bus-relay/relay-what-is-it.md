---
title: "aaaWhat é retransmissão do Azure e por que usar visão geral | Microsoft Docs"
description: "Visão geral da Retransmissão do Azure"
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1e3e971d-2a24-4f96-a88a-ce3ea2b1a1cd
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 4cfd77048210a435c446b908b7896737cad0edbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-relay"></a>O que é Retransmissão do Azure?

Olá retransmissão Azure serviço facilita híbridas de aplicativos, permitindo que você toosecurely exponham serviços que residem dentro de uma empresa corporativa rede toohello nuvem pública, sem ter que tooopen uma conexão do firewall, ou exigem intrusiva altera tooa infraestrutura de rede corporativa. A retransmissão dá suporte a vários protocolos de transporte e padrões de serviços Web diferentes.

serviço de retransmissão Olá dá suporte à solicitação/resposta unidirecional tradicional e o tráfego de ponto a ponto. Ele também suporta distribuição de eventos em cenários de publicação/assinatura do escopo da internet tooenable e comunicação do soquete bidirecional para eficiência de aumento de ponto a ponto. 

Olá retransmitida padrão de transferência de dados, um serviço local conecta-se o serviço de retransmissão toohello por meio de uma porta de saída e cria um soquete bidirecional para comunicação vinculada endereço de reunião em particular de tooa. cliente de Hello, em seguida, pode se comunicar com o serviço de local de saudação enviando o serviço de retransmissão do tráfego toohello direcionando o endereço de reunião hello. serviço de retransmissão Hello "retransmite" serviço de local de toohello dados através de um cliente do soquete bidirecional tooeach dedicado. Olá cliente não precisa de um conexão direta toohello local serviço, não é necessário tooknow onde Olá serviço reside e Olá local serviço não precisa de nenhuma porta de entrada aberta no firewall hello.

elementos de chave de recurso Olá fornecidos pela retransmissão são comunicação bidirecional, sem buffer entre limites de rede com TCP como limitação, descoberta de ponto de extremidade, o status de conectividade e sobrepostos de segurança de ponto de extremidade. recursos de retransmissão Olá diferem das tecnologias de integração de nível de rede, como VPN, dessa retransmissão pode ser tooa com escopo definido o ponto de extremidade de aplicativo único em um único computador, enquanto a tecnologia VPN é muito mais invasiva como ele se baseia na alteração de ambiente de rede Olá .

A Retransmissão do Azure tem dois recursos:

1. [Conexões híbridas](#hybrid-connections) - usa soquetes de web padrão aberto de saudação habilitar cenários de várias plataformas.
2. [Retransmissões de WCF](#wcf-relays) -chamadas de procedimento remoto tooenable usa o Windows Communication Foundation (WCF). Retransmissão do WCF é retransmissão herdados de saudação oferta que muitos clientes já usarem com seu modelos de programação de WCF.

Conexões híbridas e retransmissões WCF habilitar tooassets conexão segura que existem em uma rede corporativa enterprise. Uso de um em detrimento de outros Olá é dependente de suas necessidades específicas, conforme descrito em Olá a tabela a seguir:

|  | Retransmissão de WCF | Conexões Híbridas |
| --- |:---:|:---:|
| **WCF** |x | |
| **.NET Core** | |x |
| **.NET Framework** |x |x |
| **JavaScript/NodeJS** | |x |
| **Protocolo Aberto Baseado em Padrões** | |x |
| **Vários modelos de programação de RPC** | |x |

## <a name="hybrid-connections"></a>Conexões Híbridas

Olá [Azure retransmissão híbrida conexões](relay-hybrid-connections-protocol.md) recurso é uma evolução segura, o protocolo open do hello existente recursos de retransmissão que podem ser implementados em qualquer plataforma e em qualquer linguagem que tem uma funcionalidade básica do WebSocket, que inclua explicitamente Olá API WebSocket em navegadores da web comuns. A capacidade de Conexões Híbridas baseia-se em HTTP e WebSockets.

### <a name="service-history"></a>Histórico de serviço

Conexões híbridas substitui primeiro hello, recurso de "Serviços BizTalk" que foi criado na retransmissão do WCF do Azure Service Bus de saudação o mesmo nome. nova funcionalidade de conexões híbridas Hello complementa o recurso de retransmissão do WCF existente hello e esses recursos de dois serviço existirem lado a lado no serviço de retransmissão do Azure de saudação. Eles compartilham um gateway comum, mas têm implementações diferentes.

## <a name="wcf-relays"></a>Retransmissões de WCF

Olá funciona de retransmissão do WCF para Olá completo .NET Framework (NETFX) e do WCF. Iniciar conexão Olá entre o serviço local e serviço de retransmissão hello usando um conjunto de associações de "retransmissão" do WCF. Em segundo plano hello, associações de retransmissão Olá mapeiam toonew transporte associação elementos projetados toocreate WCF canal componentes que se integram ao barramento de serviço na nuvem de saudação.

## <a name="architecture-processing-of-incoming-relay-requests"></a>Arquitetura: processamento de mensagens de solicitações de retransmissão
Quando um cliente envia uma solicitação toohello [Azure retransmissão](/azure/service-bus-relay/) serviço, o balanceador de carga do Azure Olá encaminha tooany de nós de gateway hello. Se a solicitação de saudação é uma solicitação de escuta, nó de gateway Olá cria uma nova retransmissão. Se solicitação de saudação for uma retransmissão específica do tooa de solicitação de conexão, nó de gateway de saudação encaminha Olá conexão solicitação toohello gateway nó que possui a retransmissão de saudação. nó de gateway de saudação que possui a retransmissão Olá envia uma reunião solicitação toohello escuta cliente, solicitando Olá ouvinte toocreate um nó de gateway de toohello um canal temporário que recebeu a solicitação de conexão de saudação.

Quando a conexão de retransmissão de saudação for estabelecida, os clientes de saudação poderão trocar mensagens por meio do nó de gateway de saudação que é usado para a reunião de saudação.

![Processamento de mensagens de solicitações de retransmissão WCF](./media/relay-what-is-it/ic690645.png)

## <a name="next-steps"></a>Próximas etapas

* [Perguntas frequentes sobre retransmissão](relay-faq.md)
* [Criar um namespace](relay-create-namespace-portal.md)
* [Introdução ao .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introdução ao Node](relay-hybrid-connections-node-get-started.md)

