---
title: "aaaAzure recursos internos do Gerenciador de estado confiável do serviço de malha e coleção confiável | Microsoft Docs"
description: "Aprofunde-se nos conceitos e design de coleções confiáveis no Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a>Gerenciador de Estado Confiável do Azure Service Fabric e elementos internos de Coleções Confiáveis
Este documento se aprofunda dentro do Gerenciador de estado confiável e coleções confiável toosee como componentes principais do trabalham em segundo plano de saudação.

> [!NOTE]
> Este documento é um trabalho em andamento. Adicionar comentários toothis artigo tootell nos quais tópico você gostaria que toolearn mais sobre.
>

##  <a name="local-persistence-model-log-and-checkpoint"></a>Modelo de persistência local: ponto de verificação e de log
Olá Gerenciador de estado confiável e coleções confiável seguem um modelo de persistência que é chamado de ponto de verificação e de Log.
Nesse modelo, cada alteração de estado é registrada primeiro no disco e, em seguida, aplicada na memória.
Olá estado completa em si é mantido somente ocasionalmente (também conhecido como ponto de verificação).
benefício de saudação é que os deltas são transformados em sequenciais somente de acréscimo gravações em disco para melhorar o desempenho.

toobetter entender hello Log e o modelo de ponto de verificação, vejamos primeiro cenário de saudação de disco infinito.
Olá Gerenciador de estado confiável registra cada operação antes que seja replicada.
Log permite que a operação de Olá Olá coleções confiável tooapply apenas na memória.
Desde que os logs são mantidos, mesmo quando a réplica Olá falha e precisa toobe reiniciado, Olá Gerenciador de estado confiável tem informações suficientes em seu log tooreplay todas as operações de saudação réplica Olá perdeu.
Como disco Olá é infinito, registros de log nunca precisam ter toobe removido e coleção confiável hello precisa estado do toomanage somente Olá na memória.

Agora vamos dar uma olhada no cenário de saudação de disco finito.
Como registros de log acumulam, Olá Gerenciador de estado confiável será executado sem espaço em disco.
Antes que ocorram, Olá Gerenciador de estado confiável precisa tootruncate da sala de toomake de log para os registros mais recentes hello.
Solicitações do Gerenciador de estado confiável Olá coleções confiável toocheckpoint toodisk seu estado na memória.
Neste ponto, Olá coleções confiável persistir estado na memória.
Depois de coleções confiável Olá concluir seus pontos de verificação, Olá Gerenciador de estado confiável pode truncar Olá log toofree espaço em disco.
Quando a réplica Olá precisa toobe reiniciado, coleções confiável recuperar seu estado de ponto de verificação e hello Gerenciador de estado confiável recupera e reproduz todas as alterações de estado de saudação que ocorreram desde o último ponto de verificação de saudação.

A adição de outro valor de ponto de verificação aprimora os tempos de recuperação em cenários comuns. Log contém todas as operações que ocorreram desde o último ponto de verificação de saudação.
Portanto, ele pode incluir várias versões de um item, tal como vários valores para uma determinada linha no Dicionário Confiável.
Por outro lado, pontos de verificação um conjunto confiável Olá somente a versão mais recente de cada valor de uma chave.

## <a name="next-steps"></a>Próximas etapas
* [Transações e Bloqueios](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

