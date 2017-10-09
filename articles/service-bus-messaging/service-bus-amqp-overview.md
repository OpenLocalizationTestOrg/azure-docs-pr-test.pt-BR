---
title: "aaaOverview do AMQP 1.0 no barramento de serviço do Azure | Microsoft Docs"
description: Saiba mais sobre como usar o hello Advanced Message Queuing Protocol (AMQP) 1.0 no Azure.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0e8d19cc-de36-478e-84ae-e089bbc2d515
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: c35a20c50dd24845d9a4c7a0251e8240848a6f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-support-in-service-bus"></a>Suporte ao AMQP 1.0 no Barramento de Serviço
Ambos Olá locais e serviço de nuvem do barramento de serviço do Azure [Service Bus for Windows Server (Service Bus 1.1)](https://msdn.microsoft.com/library/dn282144.aspx) suporte Olá Advanced Message Queueing Protocol (AMQP) 1.0. AMQP permite que você toobuild entre plataformas, aplicativos híbridos usando um protocolo padrão aberto. Você pode criar aplicativos que usam componentes que são criados usando estruturas e linguagens diferentes e que são executados em sistemas operacionais diferentes. Todos esses componentes podem se conectar tooService barramento e perfeitamente troquem mensagens corporativas estruturadas com eficiência e com fidelidade total.

## <a name="introduction-what-is-amqp-10-and-why-is-it-important"></a>Introdução: O que é AMQP 1.0 e por que é importante?
Tradicionalmente, os produtos de middleware orientados à mensagens têm usado protocolos proprietários para comunicação entre os aplicativos cliente e os agentes. Isso significa que depois de selecionar o agente de mensagens de um fornecedor específico, você deve usar tooconnect de bibliotecas do fornecedor que seu agente de toothat de aplicativos cliente. Isso resulta em um nível de dependência de fornecedor, como portar um produto diferente do aplicativo tooa requer alterações de código em todos os aplicativos de saudação conectado. 

Além disso, é complicado conectar agentes de mensagens de diferentes fornecedores. Isso geralmente exige a nível do aplicativo ponte toomove mensagens de um sistema tooanother e tootranslate entre os formatos de mensagem proprietária. Este é um requisito comum; Por exemplo, quando você deve fornecer um novo tooolder de interface unificada sistemas diferentes, ou integrar sistemas de TI após uma fusão.

indústria de software Olá é uma empresa ágeis; novas linguagens de programação e estruturas de aplicativo são introduzidas em uma velocidade vezes desconcertante. Da mesma forma, requisitos de saudação do sistemas de TI evoluem ao longo do tempo e desenvolvedores desejam tootake proveito dos recursos de plataforma mais recentes da saudação. No entanto, às vezes, hello fornecedor mensagens selecionado não oferece suporte essas plataformas. Como os protocolos de mensagens são proprietários, não é possível para outras bibliotecas de tooprovide para essas novas plataformas. Portanto, você deve usar abordagens, como criar gateways ou pontes que permitem que você produto mensagens de saudação do toocontinue toouse.

desenvolvimento de saudação do hello Advanced Message Queuing Protocol (AMQP) 1.0 foi motivados por esses problemas. Ela se originou no JP Morgan Chase, que, como as empresas de serviços financeiras mais, são usuários pesados de middleware orientado a mensagens. meta de saudação foi simple: toocreate um protocolo de mensagens de padrão aberto que tornou possível toobuild baseada em mensagem aplicativos que usam componentes desenvolvidos utilizando diferentes linguagens, estruturas e sistemas operacionais, todos usando componentes de ponta de um intervalo de fornecedores.

## <a name="amqp-10-technical-features"></a>Recursos técnicos do AMQP 1.0
O AMQP 1.0 é um protocolo de mensagens eficiente, confiável e de nível de transmissão que você pode usar toobuild robusta entre plataformas, aplicativos de mensagens. protocolo de saudação tem um objetivo simples: toodefine mecânica de saudação do hello segura, confiável e eficiente transferir mensagens entre duas partes. mensagens de saudação são codificadas usando uma representação de dados portátil que permite heterogêneos remetentes e destinatários tooexchange estruturado mensagens corporativas com fidelidade total. a seguir Olá é um resumo dos recursos mais importantes do hello:

* **Eficiente**: AMQP 1.0 é um protocolo orientado a conexão que usa codificação para Olá binária instruções de protocolo e Olá mensagens corporativas transferidas por meio dele. Ele incorpora a utilização de saudação do sofisticados de controle de fluxo esquemas toomaximize de saudação componentes de rede e Olá conectado. Dito isso, protocolo de saudação foi projetado toostrike um equilíbrio entre eficiência, flexibilidade e interoperabilidade.
* **Confiável**: Olá protocolo AMQP 1.0 permite toobe mensagens trocada com um intervalo de garantias de confiabilidade do tooreliable disparar e esquecer, exatamente-uma vez confirmado entrega.
* **Flexível**: AMQP 1.0 é um protocolo flexível que pode ser usado toosupport diferentes topologias. Olá mesmo protocolo pode ser usado para comunicações de cliente-para-cliente, agente de cliente e agente para agente.
* **Modelos de agente independente**: Olá especificação AMQP 1.0 não faz quaisquer requisitos sobre o modelo de mensagens de saudação usado por um agente. Isso significa que é possível tooeasily adicionar tooexisting de suporte do AMQP 1.0 agentes de mensagens.

## <a name="amqp-10-is-a-standard-with-a-capital-s"></a>AMQP 1.0 é um padrão (com um capital')
O AMQP 1.0 é um padrão internacional aprovado pela ISO e IEC como ISO/IEC 19464:2014.

AMQP 1.0 foi desenvolvida desde 2008 por um grupo central de mais de 20 empresas, fornecedores de tecnologia e empresas de usuário final. Durante esse tempo, as empresas contribuíram seus requisitos de negócios reais e fornecedores de tecnologia de saudação evoluíram Olá protocolo toomeet esses requisitos. Em todo o processo de saudação fornecedores participaram workshops no qual eles colaboraram interoperabilidade de saudação toovalidate entre suas implementações.

Em outubro de 2011, o trabalho de desenvolvimento Olá transição Comitê técnico de tooa na hello organização para Olá avanço de Structured Information Standards (OASIS) e saudação padrão OASIS AMQP 1.0 foi lançada em outubro de 2012. Olá empresas a seguir participaram Comitê técnico Olá durante o desenvolvimento de saudação de saudação padrão:

* **Fornecedores de tecnologia**: Axway Software, Huawei Technologies, IIT Software, INETCO Systems, Kaazing, Microsoft, Mitre Corporation, Primeton Technologies, progresso Software, Red Hat, SITA, Software AG, Solace Systems, VMware, WSO2, Zenika.
* **Empresas de usuário**: Bank of America, Credit Suisse, Deutsche Boerse, Goldman Sachs, JPMorgan Chase.

Alguns dos Olá comumente citaram benefícios de padrões abertos:

* Menos chance de bloqueio de fornecedor
* Interoperabilidade
* Ampla disponibilidade de bibliotecas e ferramentas
* Proteção contra obsolescência
* Disponibilidade de equipe capacitada
* Risco menor e gerenciável

## <a name="amqp-10-and-service-bus"></a>AMQP 1.0 e Service Bus
Suporte a AMQP 1.0 no barramento de serviço do Azure significa que agora você pode aproveitar a saudação barramento de serviço enfileiramento e publicar/assinar recursos de mensagens orientados de uma variedade de plataformas usando um protocolo binário eficiente. Além disso, você pode criar aplicativos formados por componentes criados com o uso de uma mistura de linguagens, estruturas e sistemas operacionais.

Olá figura a seguir ilustra um exemplo de implantação na qual os clientes de Java em execução no Linux, escrito usando a API do Java Message Service (JMS) padrão hello e .NET em execução no Windows, trocam mensagens por meio do barramento de serviço usando AMQP 1.0.

![][0]

**Figura 1: Exemplo de cenário de implantação mostrando mensagens entre plataformas usando o Barramento de Serviço e o AMQP 1.0**

Em Olá esse tempo seguintes bibliotecas de cliente são conhecidas toowork com o barramento de serviço:

| idioma | Biblioteca |
| --- | --- |
| Java |Cliente do Apache Qpid Java Message Service (JMS)<br/>Cliente Java IIT Software SwiftMQ |
| C |Apache Qpid Proton-C |
| PHP |Apache Qpid Proton-PHP |
| Python |Apache Qpid Proton-Python |
| C# |AMQP .Net Lite |

**Figura 2: Tabela de bibliotecas de cliente do AMQP 1.0**

## <a name="summary"></a>Resumo
* O AMQP 1.0 é um protocolo de mensagens aberto e confiável que você pode usar aplicativos toobuild entre plataformas. O AMQP 1.0 é um padrão OASIS.
* O suporte do AMQP 1.0 agora está disponível no barramento de serviço do Azure, bem como para o barramento de serviço do Windows Server (Service Bus 1.1). Os preços são Olá que mesmos para Olá existente protocolos.

## <a name="next-steps"></a>Próximas etapas
Pronto toolearn mais? Visite Olá links a seguir:

* [Usando o Barramento de Serviço do .NET com AMQP]
* [Usando o Barramento de Serviço do Java com AMQP]
* [Instalando o Apache Qpid Proton-C em uma VM Linux do Azure]
* [AMQP no Barramento de Serviço para Windows Server]

[0]: ./media/service-bus-amqp-overview/service-bus-amqp-1.png
[Usando o Barramento de Serviço do .NET com AMQP]: service-bus-amqp-dotnet.md
[Usando o Barramento de Serviço do Java com AMQP]: service-bus-amqp-java.md
[Instalando o Apache Qpid Proton-C em uma VM Linux do Azure]: service-bus-amqp-apache.md
[AMQP no Barramento de Serviço para Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
