---
title: "aaaIntroduction tooReliable coleções nos serviços de monitoração de estado do Azure Service Fabric | Microsoft Docs"
description: "Serviços de malha do serviço com monitoração de estado fornecem coleções confiáveis que permitem que você toowrite aplicativos de nuvem altamente disponível, escalonável e baixa latência."
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
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 9f67c48f13e8b91b84977e127e2545cbb9d9a158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliable-collections-in-azure-service-fabric-stateful-services"></a>Introdução tooReliable coleções nos serviços de monitoração de estado do Azure Service Fabric
Coleções confiáveis habilitar aplicativos de nuvem altamente disponível, escalonável e baixa latência toowrite como se estivesse escrevendo aplicativos de computador único. Olá classes Olá **Microsoft.ServiceFabric.Data.Collections** namespace fornecem um conjunto de coleções que fazem automaticamente seu estado altamente disponível. Os desenvolvedores precisam tooprogram somente toohello confiável APIs de coleção e permitem que o coleções confiável gerenciar hello replicados e estado local.

Olá principal diferença entre coleções confiável e outras tecnologias de alta disponibilidade (como o Redis, o serviço de tabela do Azure e o serviço de fila do Azure) é que o estado de saudação é mantido localmente na instância do serviço de saudação ao que está sendo feita também altamente disponível. Isso significa que:

* Todas as leituras são locais, o que resulta em leituras de baixa latência e alta taxa de transferência.
* Todas as gravações geram Olá número mínimo do IOs de rede, que resulta em baixa latência e alta taxa de transferência grava.

![Imagem da evolução das coleções.](media/service-fabric-reliable-services-reliable-collections/ReliableCollectionsEvolution.png)

Coleções confiáveis podem ser pensadas como evolução natural de saudação do hello **System. Collections** classes: um novo conjunto de coleções que são projetados para aplicativos de nuvem e em vários computadores de saudação sem aumentar a complexidade para desenvolvedor de saudação. Sendo assim, as Coleções confiáveis são:

* Replicadas: alterações de estado são replicadas para alta disponibilidade.
* Persistente: Os dados são persistente toodisk para durabilidade contra falhas em grande escala (por exemplo, uma queda de energia de datacenter).
* Assíncrona: As APIs são assíncrona tooensure threads não são bloqueadas quando incorrer em e/s.
* Transacional: APIs utilizam a abstração de saudação de transações para poder gerenciar facilmente a várias coleções confiável dentro de um serviço.

Coleções confiáveis fornecem uma coerência forte garante fora Olá caixa toomake pensando sobre o estado do aplicativo mais fácil.
Consistência forte é obtida, garantindo a transação confirmações terminar somente após a transação inteira Olá foi registrada por um quorum de maioria das réplicas, inclusive Olá primário.
consistência do tooachieve mais fraca, aplicativos podem confirmar toohello back cliente/solicitante antes de confirmação assíncrona Olá retorna.

APIs de coleções confiável Hello são uma evolução de coleções simultâneas APIs (encontrado no hello **Concurrent** namespace):

* Assíncrono: Retorna uma tarefa porque, ao contrário de coleções simultâneas, operações de saudação são replicadas e persistente.
* Parâmetros out não: usa `ConditionalValue<T>` tooreturn um bool e um valor em vez de parâmetros de saída. `ConditionalValue<T>`é como `Nullable<T>` , mas não exige T toobe uma struct.
* Transações: Usa uma ações transação objeto tooenable Olá usuário toogroup em várias coleções confiável em uma transação.

Hoje, **Microsoft.ServiceFabric.Data.Collections** contém três coleções:

* [Dicionário Confiável](https://msdn.microsoft.com/library/azure/dn971511.aspx): representa uma coleção de pares chave/valor replicada, transacional e assíncrona. Semelhante muito**ConcurrentDictionary**, ambos Olá chave e valor Olá pode ser de qualquer tipo.
* [Fila Confiável](https://msdn.microsoft.com/library/azure/dn971527.aspx): representa uma fila PEPS (primeiro a entrar, primeiro a sair) estrita, assíncrona, transacional e replicada. Semelhante muito**ConcurrentQueue**, Olá valor pode ser de qualquer tipo.
* [Fila Simultânea Confiável](service-fabric-reliable-services-reliable-concurrent-queue.md): representa uma fila de ordenação de melhor esforço replicada, transacional e assíncrona para alta taxa de transferência. Semelhante toohello **ConcurrentQueue**, Olá valor pode ser de qualquer tipo.

## <a name="next-steps"></a>Próximas etapas
* [Recomendações e Diretrizes de Coleções Confiáveis](service-fabric-reliable-services-reliable-collections-guidelines.md)
* [Trabalhando com Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Transações e bloqueios](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Gerenciador de Estado Confiável e aspectos internos da coleção](service-fabric-reliable-services-reliable-collections-internals.md)
* Gerenciando dados
  * [Backup e restauração](service-fabric-reliable-services-backup-restore.md)
  * [Notificações](service-fabric-reliable-services-notifications.md)
  * [Serialização de coleção confiável](service-fabric-reliable-services-reliable-collections-serialization.md)
  * [Serialização e atualização](service-fabric-application-upgrade-data-serialization.md)
  * [Configuração do Gerenciador de Estado Confiável](service-fabric-reliable-services-configuration.md)
* Outros
  * [Início Rápido dos Serviços Confiáveis](service-fabric-reliable-services-quick-start.md)
  * [Referência do desenvolvedor para Coleções Confiáveis](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
