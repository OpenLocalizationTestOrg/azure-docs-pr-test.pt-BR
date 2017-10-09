---
title: "uso de aaaAdvanced de serviços confiáveis | Microsoft Docs"
description: "Saiba mais sobre o uso avançado do Reliable Services do Service Fabric para obter maior flexibilidade em seus serviços."
services: Service-Fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: masnider
ms.assetid: f2942871-863d-47c3-b14a-7cdad9a742c7
ms.service: Service-Fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: e6d6310a4deae9edcfcd76551e1337f0e39e9e5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-usage-of-hello-reliable-services-programming-model"></a>O uso de serviços confiáveis hello, modelo de programação avançado
O Service Fabric do Azure simplifica o desenvolvimento e o gerenciamento de serviços confiáveis com e sem estado. Este guia aborda usos avançados de toogain serviços confiáveis mais controle e flexibilidade sobre seus serviços. Tooreading anterior guia, familiarize-se com [modelo de programação de serviços confiáveis Olá](service-fabric-reliable-services-introduction.md).

Os serviços com e sem estado têm dois pontos de entrada principais para o código de usuário:

* `RunAsync(C#) / runAsync(Java)` é um ponto de entrada de finalidade geral para seu código de serviço.
* `CreateServiceReplicaListeners(C#)` e `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` servem para abrir ouvintes de comunicação para solicitações de cliente.

Para a maioria dos serviços, esses dois pontos de entrada são suficientes. Para casos raros, quando é necessário ter mais controle sobre o ciclo de vida do serviço, existem eventos de ciclo de vida adicionais disponíveis.

## <a name="stateless-service-instance-lifecycle"></a>Ciclo de vida de instância de serviço sem estado
O ciclo de vida de um serviço sem estado é muito simples. Um serviço sem estado só pode ser aberto, fechado ou anulado. `RunAsync` em um serviço sem estado é executado quando uma instância de serviço é aberta e cancelado quando uma instância de serviço é fechada ou anulada.

Embora `RunAsync` devem ser suficientes em quase todos os casos, Olá abrir, fechar e eventos de anulação em um serviço sem monitoração de estado também estão disponíveis:

* `Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java`OnOpenAsync é chamado quando a instância de serviço sem monitoração de estado de saudação é sobre toobe usado. As tarefas de inicialização do serviço estendido podem ser iniciadas nesse momento.
* `Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java`OnCloseAsync é chamado quando a instância de serviço sem monitoração de estado Olá vai toobe desligamento normalmente. Isso pode ocorrer quando o código do serviço hello está sendo atualizado, a instância do serviço hello está sendo movida devido tooload balanceamento ou for detectada uma falha temporária. OnCloseAsync pode ser usado toosafely fechar todos os recursos, parar qualquer processamento em segundo plano, terminar de salvar o estado externo ou fechar conexões existentes.
* `void OnAbort() - C# / void onAbort() - Java`OnAbort é chamado quando a instância de serviço sem monitoração de estado hello está sendo desligada forçada. Isso geralmente é chamado quando uma falha permanente foi detectada no nó hello, ou quando o Service Fabric confiável não pode gerenciar o ciclo de vida da instância de serviço Olá devido a falhas de toointernal.

## <a name="stateful-service-replica-lifecycle"></a>Ciclo de vida de réplica de serviço com estado

> [!NOTE]
> Ainda não há suporte para Reliable Services com monitoração de estado em Java.
>
>

Um ciclo de vida de uma réplica de serviço com estado é muito mais complexo do que uma instância de serviço sem estado. Além disso tooopen, feche e anular eventos, uma réplica de serviço com monitoração de estado sofre alterações de função durante seu ciclo de vida. Quando uma réplica de serviço com monitoração de estado altera funções, hello `OnChangeRoleAsync` evento é acionado:

* `Task OnChangeRoleAsync(ReplicaRole, CancellationToken)`OnChangeRoleAsync é chamado quando a réplica de serviço com monitoração de estado de saudação é alterar a função, por exemplo, tooprimary ou secundário. Réplicas primárias recebem status de gravação (são permitidos toocreate e gravar tooReliable coleções). Réplicas secundárias recebem status de leitura (podem somente ler das coleções confiáveis existentes). A maioria dos trabalho em um serviço com monitoração de estado é executado na réplica primária hello. Réplicas secundárias podem realizar validação somente leitura, geração de relatórios, mineração de dados ou outros trabalhos somente leitura.

Em um serviço com monitoração de estado, apenas réplica primária Olá tem acesso de gravação toostate e, portanto, geralmente quando Olá executa trabalho real. Olá `RunAsync` método em um serviço com monitoração de estado é executado somente quando a réplica de serviço com monitoração de estado de saudação é primária. Olá `RunAsync` método é cancelado quando as alterações de função da réplica primária longe primário, bem como durante a saudação fechar e anular eventos.

Usando Olá `OnChangeRoleAsync` evento permite tooperform trabalho dependendo da função de réplica, bem como alterações de toorole de resposta.

Um serviço com monitoração de estado também fornece eventos de ciclo de vida de saudação quatro mesmo como um serviço sem monitoração de estado, com hello a mesma semântica e casos de uso:

```csharp
* Task OnOpenAsync(IStatefulServicePartition, CancellationToken)
* Task OnCloseAsync(CancellationToken)
* void OnAbort()
```

## <a name="next-steps"></a>Próximas etapas
Para mais avançados tópicos relacionados tooService malha, consulte Olá artigos a seguir:

* [Configurando Reliable Services com estado](service-fabric-reliable-services-configuration.md)
* [Introdução à integridade da Malha do Serviço](service-fabric-health-introduction.md)
* [Usando relatórios de integridade do sistema para solução de problemas](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Configurando os serviços com hello Gerenciador de recursos de Cluster do serviço de malha](service-fabric-cluster-resource-manager-configure-services.md)
