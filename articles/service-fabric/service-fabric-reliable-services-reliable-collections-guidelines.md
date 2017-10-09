---
title: "aaaGuidelines & recomendações para coleções confiável no Azure Service Fabric | Microsoft Docs"
description: "Diretrizes e recomendações para usar as Coleções Confiáveis do Service Fabric"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/3/2017
ms.author: mcoskun
ms.openlocfilehash: bcdbc9d013bc044e06c43761e7f515c7e4bf340c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-and-recommendations-for-reliable-collections-in-azure-service-fabric"></a>Diretrizes e recomendações para Coleções Confiáveis no Azure Service Fabric
Esta seção fornece diretrizes para usar o Gerenciador de Estado Confiável e Coleções Confiáveis. meta de saudação é toohelp usuários evitem armadilhas comuns.

diretrizes de saudação são organizadas como recomendações simples prefixadas com termos Olá *fazer*, *considere*, *Evite* e *não*.

* Não modifique um objeto de tipo personalizado retornado por operações de leitura (por exemplo, `TryPeekAsync` ou `TryGetValueAsync`). Coleções confiáveis, como coleções simultâneas, retornam um objeto de toohello de referência e não uma cópia.
* Faça a saudação de cópia em profundidade retornada um objeto de um tipo personalizado antes de modificá-lo. Como estruturas e tipos internos são passagem-por-valor, não é necessário toodo uma cópia profunda sobre eles.
* Não use `TimeSpan.MaxValue` para tempos limites. Tempos limite deve ser usado toodetect deadlocks.
* Não use uma transação depois que ela tiver sido confirmada, anulada ou descartada.
* Não use uma enumeração fora do escopo de transação de saudação que foi criado.
* Não crie uma transação dentro da instrução `using` de outra transação porque isso pode causar deadlocks.
* Certifique-se de que a implementação de `IComparable<TKey>` esteja correta. sistema de saudação leva a dependência `IComparable<TKey>` para mesclar as linhas e pontos de verificação.
* Usar bloqueio de atualização durante a leitura de um item com uma intenção tooupdate-tooprevent uma determinada classe de deadlocks.
* Considere a possibilidade de manter os itens (por exemplo, TKey + TValue para dicionário confiável) abaixo de 80 KBytes: Olá menor melhor. Isso reduz a quantidade de saudação de requisitos de e/s de rede, bem como em disco e uso Heap de objeto grande. Geralmente, isso reduz o replicando dados duplicados quando apenas uma pequena parte do valor de hello está sendo atualizada. Tooachieve de maneira comum em dicionário confiável, é toobreak as linhas em toomultiple linhas.
* Considere o uso de backup e recuperação de desastres toohave funcionalidade de restauração.
* Evitar misturar operações de várias entidades e operações da única entidade (por exemplo `GetCountAsync`, `CreateEnumerableAsync`) em Olá mesma transação devido toohello diferentes níveis de isolamento.
* Trate InvalidOperationException. Transações de usuário podem ser anuladas pelo sistema Olá por diversas razões. Por exemplo, ao Gerenciador de estado confiável de saudação é alterar sua função de primário ou quando uma transação de longa execução está bloqueando o truncamento de log transacional hello. Nesses casos, o usuário pode receber InvalidOperationException, indicando que a transação já foi encerrada. Supondo que, encerramento de saudação da transação Olá não foi solicitado pelo usuário hello, toohandle de maneira melhor essa exceção é toodispose transação de saudação, verifique se o token de cancelamento de saudação foi sinalizado (ou função hello da réplica Olá foi alterada) e se não Crie uma nova transação e tente novamente.  

Aqui estão algumas coisas tookeep em mente:

* tempo limite padrão de saudação é quatro segundos para Olá todas as APIs de coleção confiável. A maioria dos usuários devem usar o tempo limite padrão de saudação.
* Olá token de cancelamento padrão é `CancellationToken.None` em todas as APIs de coleções confiável.
* Olá parâmetro de tipo de chave (*TKey*) para um dicionário confiável deve implementar corretamente `GetHashCode()` e `Equals()`. As chaves devem ser imutáveis.
* a alta disponibilidade para Olá coleções confiável tooachieve, cada serviço deve ter pelo menos um destino e mínimo réplica Definir tamanho de 3.
* Operações de leitura em Olá secundária podem ler versões que não são confirmada de quorum.
  Isso significa que uma versão dos dados que é lida por meio de um único secundário pode ter um progresso falso.
  As leituras do Primário são sempre estáveis: elas nunca podem ter um progresso falso.

### <a name="next-steps"></a>Próximas etapas
* [Trabalhando com Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Transações e bloqueios](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Gerenciador de Estado Confiável e aspectos internos da coleção](service-fabric-reliable-services-reliable-collections-internals.md)
* Gerenciando dados
  * [Backup e restauração](service-fabric-reliable-services-backup-restore.md)
  * [Notificações](service-fabric-reliable-services-notifications.md)
  * [Serialização e atualização](service-fabric-application-upgrade-data-serialization.md)
  * [Configuração do Gerenciador de Estado Confiável](service-fabric-reliable-services-configuration.md)
* Outros
  * [Início Rápido dos Serviços Confiáveis](service-fabric-reliable-services-quick-start.md)
  * [Referência do desenvolvedor para Coleções Confiáveis](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
