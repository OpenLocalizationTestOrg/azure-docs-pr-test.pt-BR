---
title: "aaaTransactions e modos de bloqueio no Azure Service Fabric confiável coleções | Microsoft Docs"
description: "Gerenciador de estado confiável do Azure Service Fabric e Bloqueio e Transações de Coleções Confiáveis."
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
ms.openlocfilehash: 340e029aa98f43ad6e46b48f687dad01f9d96f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-and-lock-modes-in-azure-service-fabric-reliable-collections"></a>Transações e modos de bloqueio em Coleções Confiáveis do Azure Service Fabric

## <a name="transaction"></a>Transação
Uma transação é uma sequência de operações realizadas como uma única unidade lógica de trabalho.
Uma transação deve apresentar Olá propriedades ACID a seguir. (consulte: https://technet.microsoft.com/en-us/library/ms190612)
* **Atomicidade**: uma transação deve ser uma unidade atômica de trabalho. Em outras palavras, todas as suas modificações de dados são realizadas ou nenhuma delas é realizada.
* **Consistência**: quando concluída, uma transação deve deixar todos os dados em um estado consistente. Todas as estruturas de dados internos devem estar corretas no final de saudação da transação de saudação.
* **Isolamento**: as modificações feitas por transações simultâneas devem ser isoladas contra modificações de saudação feitas por qualquer outra transação simultânea. nível de isolamento de saudação usado para uma operação em um ITransaction é determinado pelo Olá IReliableState executar operação de saudação.
* **Durabilidade**: após uma transação, seus efeitos ficam permanentemente no sistema de saudação. modificações de saudação persistirem mesmo em caso de saudação de uma falha do sistema.

### <a name="isolation-levels"></a>Níveis de isolamento
Nível de isolamento define o grau de saudação transações de saudação toowhich devem ser isoladas das modificações feitas por outras transações.
Há dois níveis de isolamento com suporte nas Coleções Confiáveis:

* **Leitura repetida**: Especifica que as instruções não podem ler dados que foram modificados, mas ainda não foram confirmados por outras transações e que nenhuma outra transação pode modificar dados que foram lidos pela transação atual de saudação até Olá atual conclusão da transação. Para obter mais detalhes, consulte [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).
* **Instantâneo**: Especifica que os dados lidos por qualquer instrução em uma transação são a versão transacionalmente consistente Olá dos dados Olá que existiam no início de saudação da transação de saudação.
  transação Olá pode reconhecer apenas modificações de dados que foram confirmadas antes do início de saudação da transação de saudação.
  Modificações de dados feitas por outras transações após Olá início da transação atual Olá não são visíveis toostatements execução na transação atual hello.
  efeito Olá é como se instruções Olá em uma transação de um instantâneo dos dados Olá confirmada conforme se encontravam no início de saudação da transação de saudação.
  Os instantâneos são consistentes entre as Coleções Confiáveis.
  Para obter mais detalhes, consulte [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).

Coleções confiáveis automaticamente escolha toouse de nível de isolamento Olá para uma determinada operação leitura dependendo da operação de saudação e função hello da réplica Olá no tempo de saudação da criação da transação.
A seguir é a tabela de saudação que descreve os padrões de nível de isolamento para operações de fila e dicionário confiável.

| Operação\função | Primário | Secundário |
| --- |:--- |:--- |
| Leitura de entidade única |Leitura repetida |Instantâneo |
| Enumeração, Contagem |Instantâneo |Instantâneo |

> [!NOTE]
> Exemplos comuns de Operações de Entidade Única são `IReliableDictionary.TryGetValueAsync`, `IReliableQueue.TryPeekAsync`.
> 

Olá dicionário confiável e Olá fila confiável suportam grava seu de leitura.
Em outras palavras, qualquer gravação dentro de uma transação serão visíveis tooa seguinte lidos que pertence a toohello mesma transação.

## <a name="locks"></a>Bloqueios
Em coleções confiável, todas as transações de implementar rigorosos duas fases de bloqueio: uma transação não liberar bloqueios Olá adquiriu até que a transação Olá termina com uma operação de anulação ou uma confirmação.

Dicionário Confiável usa bloqueio para todas as operações de entidade única em nível de linha.
Fila Confiável compensa simultaneidade para propriedade PEPS transacional estrita.
Fila Confiável usa bloqueios de nível de operação permitindo que uma transação com `TryPeekAsync` e/ou `TryDequeueAsync` e uma transação com `EnqueueAsync` por vez.
Observe que toopreserve FIFO, se um `TryPeekAsync` ou `TryDequeueAsync` nunca observa que Olá fila confiável está vazio, também será bloqueado `EnqueueAsync`.

Operações de gravação sempre utilizam bloqueios exclusivos.
Para operações de leitura, Olá bloqueio depende de dois fatores.
Qualquer operação de leitura feita usando o isolamento de Instantâneo é livre de bloqueio.
Qualquer operação de Leitura Repetida por padrão recebe bloqueios compartilhados.
No entanto, para qualquer operação de leitura que dá suporte à leitura repetida, usuário Olá pode pedir para um bloqueio de atualização em vez da saudação bloqueio compartilhado.
Um bloqueio de atualização é que um bloqueio assimétrico usado tooprevent uma forma comum de deadlock que ocorre quando várias transações bloqueiam recursos para possíveis atualizações em um momento posterior.

matriz de compatibilidade de bloqueio Olá pode ser encontrada em Olá a tabela a seguir:

| Solicitação\concedida | Nenhum | Compartilhado | Atualizar | Exclusivo |
| --- |:--- |:--- |:--- |:--- |
| Compartilhado |Sem conflito |Sem conflito |Conflito |Conflito |
| Atualizar |Sem conflito |Sem conflito |Conflito |Conflito |
| Exclusivo |Sem conflito |Conflito |Conflito |Conflito |

Argumento de tempo limite em Olá APIs de coleções confiável é usado para detecção de deadlock.
Por exemplo, duas transações (T1 e T2) estão tentando tooread e atualizar K1.
É possível que eles toodeadlock, porque ambos acabam tendo Olá compartilhado bloqueio.
Nesse caso, uma ou ambas as operações de saudação atingirá o tempo limite.

Esse cenário de deadlock é um ótimo exemplo de como um Bloqueio de atualização pode evitar deadlocks.

## <a name="next-steps"></a>Próximas etapas
* [Trabalhando com Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Notificações do Reliable Services](service-fabric-reliable-services-notifications.md)
* [Backup e restauração do Reliable Services (recuperação de desastre)](service-fabric-reliable-services-backup-restore.md)
* [Configuração do Gerenciador de Estado Confiável](service-fabric-reliable-services-configuration.md)
* [Referência do desenvolvedor para Coleções Confiáveis](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

