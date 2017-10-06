---
title: aaaOverview de capacidade dedicado de Hubs de eventos do Azure | Microsoft Docs
description: "Visão geral da capacidade de Hubs de Eventos Dedicados do Microsoft Azure ."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: sethm;babanisa
ms.openlocfilehash: 79c09975e5c0a6d4729c8f836576770abaaf322e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-event-hubs-dedicated"></a>Visão geral de Hubs de Eventos Dedicados

*Dedicado de Hubs de evento* capacidade oferece único locatário implantações para clientes com hello mais exigentes. Em larga escala, Hubs de eventos do Azure pode ser entrada mais de 2 milhões de eventos por segundo ou backup GB too2 por segundo de telemetria com latência de armazenamento e o segundo completamente durável. Este também habilita soluções integradas com o processamento em tempo real e o lote em Olá mesmo sistema. Com o arquivamento dos Hubs de eventos incluídos na oferta Olá, você pode reduzir a complexidade de saudação de sua solução tendo um único fluxo oferecer suporte a pipelines com base em lotes e em tempo real.

Olá tabela a seguir compara as camadas de serviço disponível Olá dos Hubs de eventos. oferta de saudação dedicado de Hubs de evento é um preço mensal fixado, em comparação com toousage preços para a maioria dos recursos do Standard e Basic. camada dedicado Olá oferece recursos de saudação do plano padrão hello, mas com a capacidade de escala do enterprise para clientes com cargas de trabalho exigentes. 

| Recurso | Basic | Standard | Dedicado |
| --- |:---:|:---:|:---:|
| Eventos de entrada | Pagamento por milhão de eventos | Pagamento por milhão de eventos | Incluso |
| Unidade de taxa de transferência (entrada de 1 MB/s, saída de 2 MB/s) | Pagamento por hora | Pagamento por hora | Incluso |
| Tamanho da mensagem | 256 KB | 256 KB | 1 MB |
| Políticas do publicador | N/D | Sim | Sim |     
| Grupos de consumidores | 1 - padrão | 20 | 20 |
| Reprodução de mensagem | Sim | Sim | Sim |
| Unidades de produtividade máxima | 20 | 20 (too100 flexível)  | 1 CU≈200 |
| Conexões orientadas | 100 incluídos | 1000 incluídos | 100.000 incluídos |
| Conexões agenciadas adicionais | N/D | Sim | Sim |
| Retenção de mensagem | 1 dia incluído | 1 dia incluído | Backup too7 dias incluídos |
| Arquivo morto (visualização) | N/D   | Pagamento por hora | Incluso |

## <a name="benefits-of-event-hubs-dedicated-capacity"></a>Os benefícios da capacidade dos Hubs de Eventos Dedicados

Olá benefícios a seguir está disponível ao usar dedicado de Hubs de evento:

* Hospedagem de único locatário, sem ruído de outros locatários.
* Mensagem de tamanho aumenta too1 MB comparado too256 KB para Standard e Basic.
* Desempenho repetível em todas as ocasiões.
* A garantia de capacidade toomeet que a intermitência precisa.
* Escalonável entre 1 e unidades de capacidade 8 (CU) – fornecendo too2 milhão eventos de entrada por segundo.
  * Per gerencia escala Olá dedicado de Hubs de evento, onde cada atualização Cumulativa pode fornecer aproximadamente equivalente a saudação de 200 unidades de taxa de transferência (TU).
* Sem manutenção – gerenciamos o balanceamento de carga, as atualizações do SO, os patches de segurança e o particionamento.
* Preço mensal fixo.

Dedicado de Hubs de evento também remove algumas das limitações de taxa de transferência de saudação de oferta de saudação padrão. Unidades de taxa de transferência em camadas básica e padrão intitular too1000 eventos por segundo ou 1 MB por segundo de entrada por TU e double essa quantidade de saída. oferta de escala dedicado Olá não tem nenhuma restrição na entrada e contagem de eventos de saída. Esses limites são regidos apenas pela capacidade de saudação adquirida hubs de eventos de processamento de saudação.

Este serviço é destinado a usuários de telemetria maior hello e toocustomers disponíveis com um enterprise agreement.

## <a name="how-tooonboard"></a>Como tooonboard

plataforma de saudação dedicado de Hubs de eventos é oferecida por meio de um enterprise agreement com diferentes tamanhos de Per. Cada atualização Cumulativa fornece aproximadamente equivalente a saudação de 200 unidades de taxa de transferência. Você pode dimensionar sua capacidade para cima ou para baixo em toda a saudação mês toomeet suas necessidades, adicionando ou removendo Per. plano dedicado Olá é exclusivo em que você terá uma integração mais prática de saudação Hubs de eventos produto team tooget Olá flexíveis de implantação certa para você. 

## <a name="next-steps"></a>Próximas etapas
Entre em contato com seu representante de vendas da Microsoft ou Microsoft Support tooget mais detalhes sobre capacidade de dedicado de Hubs de eventos. Você também pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

Para obter informações detalhadas sobre preços, visite Olá links a seguir:

- [Preço de Hubs de Eventos Dedicados](https://azure.microsoft.com/pricing/details/event-hubs/). Você também pode contatar o representante da Microsoft ou Microsoft Support tooget mais detalhes sobre capacidade dedicado de Hubs de evento.
- Olá [perguntas frequentes sobre Hubs de evento](event-hubs-faq.md) contém informações sobre preços e respostas algumas perguntas frequentes sobre Hubs de eventos. 
