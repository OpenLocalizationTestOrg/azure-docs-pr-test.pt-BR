---
title: "Configurações de porta da Retransmissão do Azure | Microsoft Docs"
description: "Detalhes sobre os valores de porta da Retransmissão do Azure."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2018
ms.author: sethm
ms.openlocfilehash: 055f04d496b56a5e8542911aa78292d7746ae80b
ms.sourcegitcommit: 9890483687a2b28860ec179f5fd0a292cdf11d22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="azure-relay-port-settings"></a>Configurações de porta de Retransmissão do Azure

A tabela a seguir descreve a configuração necessária dos valores de porta para uma Retransmissão do Azure.

## <a name="hybrid-connections"></a>Conexões Híbridas
As Conexões Híbridas usam WebSockets como o mecanismo de transporte subjacente, que usa apenas **HTTPS**. 

## <a name="wcf-relays"></a>Retransmissões de WCF
  
|Associação|Segurança de transporte|Porta|  
|-------------|------------------------|----------|  
|[Classe BasicHttpRelayBinding](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (cliente)|sim|HTTPS| 
| |" |Não |HTTP|  
|[Classe BasicHttpRelayBinding](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (serviço)|Você pode usar o|9351/HTTP|  
|[Classe NetEventRelayBinding](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (cliente)|sim|9351/HTTPS|  
||" |Não |9350/HTTP|  
|[Classe NetEventRelayBinding](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (serviço)|Você pode usar o|9351/HTTP|  
|[Classe NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (cliente/serviço)|Você pode usar o|5671/9352/HTTP (9352/9353 se híbrido for usado)|  
|[Classe NetOnewayRelayBinding](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (cliente)|sim|9351/HTTPS|  
||" |Não |9350/HTTP|  
|[Classe NetOnewayRelayBinding](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (serviço)|Você pode usar o|9351/HTTP|  
|[Classe WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (cliente)|sim|HTTPS|  
||" |Não |HTTP|  
|[Classe WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (serviço)|Você pode usar o|9351/HTTP|  
|[Classe WS2007HttpRelayBinding](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (cliente)|sim|HTTPS|  
||" |Não |HTTP|  
|[Classe WS2007HttpRelayBinding](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (serviço)|Você pode usar o|9351/HTTP|

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre a Retransmissão do Azure, visite estes links:
* [O que é Retransmissão do Azure?](relay-what-is-it.md)
* [Perguntas frequentes sobre retransmissão](relay-faq.md)