---
title: aaaDefinine e gerenciar o estado no Azure microservices | Microsoft Docs
description: "Como toodefine e gerenciar o estado do serviço no Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a>Estado do serviço
**Estado do serviço** refere-se toohello na memória ou nos dados de disco, um serviço requer toofunction. Ele inclui, por exemplo, estruturas de dados hello e variáveis de membro desse serviço Olá lê e grava toodo trabalho. Dependendo de como o serviço Olá é desenvolvido, também pode incluir arquivos ou outros recursos que são armazenados no disco. Por exemplo, Olá arquivos de um banco de dados usaria toostore dados e logs de transação.

Como um exemplo de serviço, vamos considerar uma calculadora. Um serviço de calculadora básica pega dois números e retorna sua soma. Executar este cálculo não envolve nenhuma variável de membro ou outras informações.

Agora considere Olá Calculadora mesmo, mas com um método adicional para armazenar e retornando soma última Olá ele calculado. Agora, trata-se de um serviço com estado. Monitoração de estado significa que contém algum estado que ele grava toowhen, ele calcula uma soma de novo e lê a partir quando você pedir sum calculado do tooreturn Olá último.

No Azure Service Fabric, o primeiro serviço de saudação é chamado de serviço sem monitoração de estado. segundo serviço de saudação é chamado de serviço com monitoração de estado.

## <a name="storing-service-state"></a>Armazenando o estado do serviço
Estado pode ser externalizado ou colocalizado com o código de saudação que é manipular o estado de saudação. Externalização de estado geralmente é feita usando um banco de dados externo ou outros dados de repositório que é executado em máquinas diferentes pela rede hello ou fora do processo em Olá mesma máquina. Em nosso exemplo de cálculo, Olá repositório de dados pode ser uma instância de armazenamento de tabela do Azure ou o banco de dados SQL. Soma de saudação de toocompute cada solicitação executa uma atualização de dados e solicitações toohello serviço tooreturn Olá valor resultam no valor atual de saudação sendo buscada no repositório de saudação. 

Estado também pode ser colocalizado com o código de saudação que manipula o estado de saudação. Serviços com estado no Service Fabric normalmente são criados usando esse modelo. Malha do serviço fornece Olá tooensure de infraestrutura que esse estado é altamente disponível, consistente e duráveis e serviços Olá criado dessa maneira pode dimensionar com facilidade.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre os conceitos de malha do serviço, consulte Olá artigos a seguir:

* [Disponibilidade dos serviços de malha do serviço](service-fabric-availability-services.md)
* [Escalabilidade de serviços da Malha do Serviço](service-fabric-concepts-scalability.md)
* [Particionando serviços da Malha do Serviço](service-fabric-concepts-partitioning.md)
* [Reliable Services do Service Fabric](service-fabric-reliable-services-introduction.md)
