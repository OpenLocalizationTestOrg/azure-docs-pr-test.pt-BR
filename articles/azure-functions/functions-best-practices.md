---
title: "práticas recomendadas de aaaBest para funções do Azure | Microsoft Docs"
description: "Aprenda as práticas recomendadas e padrões para o Azure Functions."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, padrões, práticas recomendadas, funções, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a>Otimizar o desempenho de saudação e confiabilidade de funções do Azure

Este artigo fornece desempenho de saudação tooimprove orientação e confiabilidade de seus aplicativos de função. 


## <a name="avoid-long-running-functions"></a>Evite funções grandes de longa duração

As funções grandes de longa duração podem causar problemas de tempo limite inesperados. Uma função pode se tornar grande devido a dependências do toomany Node. js. A importação dessas dependências pode causar aumento no tempo de carregamento resultando em tempos limite inesperados. As dependências são carregadas explícita e implicitamente. Um único módulo carregado pelo seu código pode carregar seus próprios módulos adicionais.  

Sempre que possível, refatore funções grandes em conjuntos menores de funções que funcionem juntos e retornem respostas rápidas. Por exemplo, um webhook ou uma função do gatilho HTTP pode exigir uma resposta de confirmação dentro de um tempo limite; é comum para webhooks toorequire uma resposta imediata. Você pode passar a carga de gatilho Olá HTTP para um toobe fila processada por uma função de gatilho de fila. Essa abordagem permite que você trabalho real do toodefer hello e retornar uma resposta imediata.


## <a name="cross-function-communication"></a>Comunicação entre funções

Ao integrar várias funções, geralmente é uma melhor prática toouse filas de armazenamento para cruzada comunicação de função.  Olá principal motivo é filas de armazenamento são mais baratas e muito mais fácil tooprovision. 

Mensagens individuais em uma fila de armazenamento são limitadas em tamanho too64 KB. Se você precisar a mensagens maiores toopass entre as funções, uma fila do barramento de serviço do Azure pode ser usado toosupport tamanhos de mensagem backup too256 KB.

Tópicos de barramento de serviço são úteis se você precisar de filtragem de mensagens antes do processamento.

Hubs de eventos são úteis toosupport comunicações de alto volume.


## <a name="write-functions-toobe-stateless"></a>Gravar funções toobe sem monitoração de estado 

As funções devem ser sem estado e idempotentes se possível. Associe quaisquer informações de estado necessárias a seus dados. Por exemplo, um pedido sendo processado provavelmente teria um membro `state` associado. Uma função pode processar uma ordem com base nesse estado enquanto a função hello em si permanece sem monitoração de estado. 

Funções de idempotentes são recomendadas especialmente com gatilhos de timer. Por exemplo, se você tiver algo que absolutamente deve ser executado uma vez por dia, grave-a para que possa executar qualquer momento durante o dia de saudação com hello mesmos resultados. função Hello pode sair quando não houver nenhum trabalho de um dia específico. Também se uma execução anterior falhou toocomplete, Olá próxima execução deve continuar onde parou.


## <a name="write-defensive-functions"></a>Grave funções defensivas

Suponha que sua função pode encontrar uma exceção a qualquer momento. Crie funções com hello toocontinue de capacidade de um ponto de falha anterior durante a execução da próxima hello. Considere um cenário que requer Olá ações a seguir:

1. Consulta de 10.000 linhas em um banco de dados.
2. Crie uma mensagem da fila para cada um dos tooprocess linhas ainda mais para baixo da linha de saudação.
 
Dependendo de quão complexo é o sistema, você pode ter: serviços posteriores envolvidos se comportando mal, interrupções de rede ou limites de cota alcançados, etc. Tudo isso pode afetar sua função a qualquer momento. É necessário toodesign seu toobe funções preparado para ele.

Como o seu código reage se ocorrer uma falha após a inserção de 5.000 desses itens em uma fila para processamento? Controle itens em um conjunto concluído. Caso contrário, você pode inseri-los de novo posteriormente. Isso pode ter um sério impacto em seu fluxo de trabalho. 

Se um item da fila já foi processado, permitir que sua função toobe não operacional.

Tirar proveito das medidas de defesa já fornecido para componentes que você usa na plataforma do Azure funções hello. Por exemplo, consulte **tratar mensagens suspeitas fila** na documentação de saudação do [dispara a fila de armazenamento do Azure](functions-bindings-storage-queue.md#trigger).
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a>Não combinação de teste e produção de código em Olá mesmo aplicativo de função

As funções em um aplicativo de funções compartilham recursos. Por exemplo, a memória é compartilhada. Se você estiver usando um aplicativo de função na produção, não adicione funções de teste e tooit de recursos. Ele pode causar sobrecarga inesperada durante a execução de código de produção.

Cuidado com o que você carrega em seus aplicativos de funções de produção. Média de memória em cada função no aplicativo hello.

Se você tiver um assembly compartilhado referenciado em várias funções .Net, coloque-o em uma pasta compartilhada comum. Referência do assembly hello com um toohello semelhante instrução exemplo a seguir: 

    #r "..\Shared\MyAssembly.dll". 

Caso contrário, é fácil tooaccidentally implantar várias versões de teste do mesmo binário que se comportam de maneira diferente entre as funções de saudação.

Não use o log detalhado no código de produção. Ele tem um impacto negativo no desempenho.



## <a name="use-async-code-but-avoid-blocking-calls"></a>Usar o código assíncrono, mas evitar chamadas de bloqueio

A programação assíncrona é uma prática recomendada. No entanto, evite sempre referenciando Olá `Result` propriedade ou chamar `Wait` método em um `Task` instância. Essa abordagem pode gerar esgotamento toothread.


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá recursos a seguir:

Como Azure Functions usa o serviço de aplicativo do Azure, você deve estar ciente das diretrizes de serviço de aplicativo.
* [Otimizações de desempenho HTTP para padrões e práticas](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

