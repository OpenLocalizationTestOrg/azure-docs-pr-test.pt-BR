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
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="91f3e-104">Otimizar o desempenho de saudação e confiabilidade de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="91f3e-104">Optimize hello performance and reliability of Azure Functions</span></span>

<span data-ttu-id="91f3e-105">Este artigo fornece desempenho de saudação tooimprove orientação e confiabilidade de seus aplicativos de função.</span><span class="sxs-lookup"><span data-stu-id="91f3e-105">This article provides guidance tooimprove hello performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="91f3e-106">Evite funções grandes de longa duração</span><span class="sxs-lookup"><span data-stu-id="91f3e-106">Avoid long running functions</span></span>

<span data-ttu-id="91f3e-107">As funções grandes de longa duração podem causar problemas de tempo limite inesperados.</span><span class="sxs-lookup"><span data-stu-id="91f3e-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="91f3e-108">Uma função pode se tornar grande devido a dependências do toomany Node. js.</span><span class="sxs-lookup"><span data-stu-id="91f3e-108">A function can become large due toomany Node.js dependencies.</span></span> <span data-ttu-id="91f3e-109">A importação dessas dependências pode causar aumento no tempo de carregamento resultando em tempos limite inesperados.</span><span class="sxs-lookup"><span data-stu-id="91f3e-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="91f3e-110">As dependências são carregadas explícita e implicitamente.</span><span class="sxs-lookup"><span data-stu-id="91f3e-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="91f3e-111">Um único módulo carregado pelo seu código pode carregar seus próprios módulos adicionais.</span><span class="sxs-lookup"><span data-stu-id="91f3e-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="91f3e-112">Sempre que possível, refatore funções grandes em conjuntos menores de funções que funcionem juntos e retornem respostas rápidas.</span><span class="sxs-lookup"><span data-stu-id="91f3e-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="91f3e-113">Por exemplo, um webhook ou uma função do gatilho HTTP pode exigir uma resposta de confirmação dentro de um tempo limite; é comum para webhooks toorequire uma resposta imediata.</span><span class="sxs-lookup"><span data-stu-id="91f3e-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks toorequire an immediate response.</span></span> <span data-ttu-id="91f3e-114">Você pode passar a carga de gatilho Olá HTTP para um toobe fila processada por uma função de gatilho de fila.</span><span class="sxs-lookup"><span data-stu-id="91f3e-114">You can pass hello HTTP trigger payload into a queue toobe processed by a queue trigger function.</span></span> <span data-ttu-id="91f3e-115">Essa abordagem permite que você trabalho real do toodefer hello e retornar uma resposta imediata.</span><span class="sxs-lookup"><span data-stu-id="91f3e-115">This approach allows you toodefer hello actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="91f3e-116">Comunicação entre funções</span><span class="sxs-lookup"><span data-stu-id="91f3e-116">Cross function communication</span></span>

<span data-ttu-id="91f3e-117">Ao integrar várias funções, geralmente é uma melhor prática toouse filas de armazenamento para cruzada comunicação de função.</span><span class="sxs-lookup"><span data-stu-id="91f3e-117">When integrating multiple functions, it is generally a best practice toouse storage queues for cross function communication.</span></span>  <span data-ttu-id="91f3e-118">Olá principal motivo é filas de armazenamento são mais baratas e muito mais fácil tooprovision.</span><span class="sxs-lookup"><span data-stu-id="91f3e-118">hello main reason is storage queues are cheaper and much easier tooprovision.</span></span> 

<span data-ttu-id="91f3e-119">Mensagens individuais em uma fila de armazenamento são limitadas em tamanho too64 KB.</span><span class="sxs-lookup"><span data-stu-id="91f3e-119">Individual messages in a storage queue are limited in size too64 KB.</span></span> <span data-ttu-id="91f3e-120">Se você precisar a mensagens maiores toopass entre as funções, uma fila do barramento de serviço do Azure pode ser usado toosupport tamanhos de mensagem backup too256 KB.</span><span class="sxs-lookup"><span data-stu-id="91f3e-120">If you need toopass larger messages between functions, an Azure Service Bus queue could be used toosupport message sizes up too256 KB.</span></span>

<span data-ttu-id="91f3e-121">Tópicos de barramento de serviço são úteis se você precisar de filtragem de mensagens antes do processamento.</span><span class="sxs-lookup"><span data-stu-id="91f3e-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="91f3e-122">Hubs de eventos são úteis toosupport comunicações de alto volume.</span><span class="sxs-lookup"><span data-stu-id="91f3e-122">Event hubs are useful toosupport high volume communications.</span></span>


## <a name="write-functions-toobe-stateless"></a><span data-ttu-id="91f3e-123">Gravar funções toobe sem monitoração de estado</span><span class="sxs-lookup"><span data-stu-id="91f3e-123">Write functions toobe stateless</span></span> 

<span data-ttu-id="91f3e-124">As funções devem ser sem estado e idempotentes se possível.</span><span class="sxs-lookup"><span data-stu-id="91f3e-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="91f3e-125">Associe quaisquer informações de estado necessárias a seus dados.</span><span class="sxs-lookup"><span data-stu-id="91f3e-125">Associate any required state information with your data.</span></span> <span data-ttu-id="91f3e-126">Por exemplo, um pedido sendo processado provavelmente teria um membro `state` associado.</span><span class="sxs-lookup"><span data-stu-id="91f3e-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="91f3e-127">Uma função pode processar uma ordem com base nesse estado enquanto a função hello em si permanece sem monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="91f3e-127">A function could process an order based on that state while hello function itself remains stateless.</span></span> 

<span data-ttu-id="91f3e-128">Funções de idempotentes são recomendadas especialmente com gatilhos de timer.</span><span class="sxs-lookup"><span data-stu-id="91f3e-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="91f3e-129">Por exemplo, se você tiver algo que absolutamente deve ser executado uma vez por dia, grave-a para que possa executar qualquer momento durante o dia de saudação com hello mesmos resultados.</span><span class="sxs-lookup"><span data-stu-id="91f3e-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during hello day with hello same results.</span></span> <span data-ttu-id="91f3e-130">função Hello pode sair quando não houver nenhum trabalho de um dia específico.</span><span class="sxs-lookup"><span data-stu-id="91f3e-130">hello function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="91f3e-131">Também se uma execução anterior falhou toocomplete, Olá próxima execução deve continuar onde parou.</span><span class="sxs-lookup"><span data-stu-id="91f3e-131">Also if a previous run failed toocomplete, hello next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="91f3e-132">Grave funções defensivas</span><span class="sxs-lookup"><span data-stu-id="91f3e-132">Write defensive functions</span></span>

<span data-ttu-id="91f3e-133">Suponha que sua função pode encontrar uma exceção a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="91f3e-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="91f3e-134">Crie funções com hello toocontinue de capacidade de um ponto de falha anterior durante a execução da próxima hello.</span><span class="sxs-lookup"><span data-stu-id="91f3e-134">Design your functions with hello ability toocontinue from a previous fail point during hello next execution.</span></span> <span data-ttu-id="91f3e-135">Considere um cenário que requer Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="91f3e-135">Consider a scenario that requires hello following actions:</span></span>

1. <span data-ttu-id="91f3e-136">Consulta de 10.000 linhas em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="91f3e-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="91f3e-137">Crie uma mensagem da fila para cada um dos tooprocess linhas ainda mais para baixo da linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="91f3e-137">Create a queue message for each of those rows tooprocess further down hello line.</span></span>
 
<span data-ttu-id="91f3e-138">Dependendo de quão complexo é o sistema, você pode ter: serviços posteriores envolvidos se comportando mal, interrupções de rede ou limites de cota alcançados, etc. Tudo isso pode afetar sua função a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="91f3e-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="91f3e-139">É necessário toodesign seu toobe funções preparado para ele.</span><span class="sxs-lookup"><span data-stu-id="91f3e-139">You need toodesign your functions toobe prepared for it.</span></span>

<span data-ttu-id="91f3e-140">Como o seu código reage se ocorrer uma falha após a inserção de 5.000 desses itens em uma fila para processamento?</span><span class="sxs-lookup"><span data-stu-id="91f3e-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="91f3e-141">Controle itens em um conjunto concluído.</span><span class="sxs-lookup"><span data-stu-id="91f3e-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="91f3e-142">Caso contrário, você pode inseri-los de novo posteriormente.</span><span class="sxs-lookup"><span data-stu-id="91f3e-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="91f3e-143">Isso pode ter um sério impacto em seu fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="91f3e-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="91f3e-144">Se um item da fila já foi processado, permitir que sua função toobe não operacional.</span><span class="sxs-lookup"><span data-stu-id="91f3e-144">If a queue item was already processed, allow your function toobe a no-op.</span></span>

<span data-ttu-id="91f3e-145">Tirar proveito das medidas de defesa já fornecido para componentes que você usa na plataforma do Azure funções hello.</span><span class="sxs-lookup"><span data-stu-id="91f3e-145">Take advantage of defensive measures already provided for components you use in hello Azure Functions platform.</span></span> <span data-ttu-id="91f3e-146">Por exemplo, consulte **tratar mensagens suspeitas fila** na documentação de saudação do [dispara a fila de armazenamento do Azure](functions-bindings-storage-queue.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="91f3e-146">For example, see **Handling poison queue messages** in hello documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a><span data-ttu-id="91f3e-147">Não combinação de teste e produção de código em Olá mesmo aplicativo de função</span><span class="sxs-lookup"><span data-stu-id="91f3e-147">Don't mix test and production code in hello same function app</span></span>

<span data-ttu-id="91f3e-148">As funções em um aplicativo de funções compartilham recursos.</span><span class="sxs-lookup"><span data-stu-id="91f3e-148">Functions within a function app share resources.</span></span> <span data-ttu-id="91f3e-149">Por exemplo, a memória é compartilhada.</span><span class="sxs-lookup"><span data-stu-id="91f3e-149">For example, memory is shared.</span></span> <span data-ttu-id="91f3e-150">Se você estiver usando um aplicativo de função na produção, não adicione funções de teste e tooit de recursos.</span><span class="sxs-lookup"><span data-stu-id="91f3e-150">If you're using a function app in production, don't add test-related functions and resources tooit.</span></span> <span data-ttu-id="91f3e-151">Ele pode causar sobrecarga inesperada durante a execução de código de produção.</span><span class="sxs-lookup"><span data-stu-id="91f3e-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="91f3e-152">Cuidado com o que você carrega em seus aplicativos de funções de produção.</span><span class="sxs-lookup"><span data-stu-id="91f3e-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="91f3e-153">Média de memória em cada função no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="91f3e-153">Memory is averaged across each function in hello app.</span></span>

<span data-ttu-id="91f3e-154">Se você tiver um assembly compartilhado referenciado em várias funções .Net, coloque-o em uma pasta compartilhada comum.</span><span class="sxs-lookup"><span data-stu-id="91f3e-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="91f3e-155">Referência do assembly hello com um toohello semelhante instrução exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="91f3e-155">Reference hello assembly with a statement similar toohello following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="91f3e-156">Caso contrário, é fácil tooaccidentally implantar várias versões de teste do mesmo binário que se comportam de maneira diferente entre as funções de saudação.</span><span class="sxs-lookup"><span data-stu-id="91f3e-156">Otherwise, it is easy tooaccidentally deploy multiple test versions of hello same binary that behave differently between functions.</span></span>

<span data-ttu-id="91f3e-157">Não use o log detalhado no código de produção.</span><span class="sxs-lookup"><span data-stu-id="91f3e-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="91f3e-158">Ele tem um impacto negativo no desempenho.</span><span class="sxs-lookup"><span data-stu-id="91f3e-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="91f3e-159">Usar o código assíncrono, mas evitar chamadas de bloqueio</span><span class="sxs-lookup"><span data-stu-id="91f3e-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="91f3e-160">A programação assíncrona é uma prática recomendada.</span><span class="sxs-lookup"><span data-stu-id="91f3e-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="91f3e-161">No entanto, evite sempre referenciando Olá `Result` propriedade ou chamar `Wait` método em um `Task` instância.</span><span class="sxs-lookup"><span data-stu-id="91f3e-161">However, always avoid referencing hello `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="91f3e-162">Essa abordagem pode gerar esgotamento toothread.</span><span class="sxs-lookup"><span data-stu-id="91f3e-162">This approach can lead toothread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="91f3e-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="91f3e-163">Next steps</span></span>
<span data-ttu-id="91f3e-164">Para obter mais informações, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="91f3e-164">For more information, see hello following resources:</span></span>

<span data-ttu-id="91f3e-165">Como Azure Functions usa o serviço de aplicativo do Azure, você deve estar ciente das diretrizes de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91f3e-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* [<span data-ttu-id="91f3e-166">Otimizações de desempenho HTTP para padrões e práticas</span><span class="sxs-lookup"><span data-stu-id="91f3e-166">Patterns and Practices HTTP Performance Optimizations</span></span>](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

