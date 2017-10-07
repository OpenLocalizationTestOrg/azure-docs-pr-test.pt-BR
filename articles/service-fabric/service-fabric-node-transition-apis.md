---
title: "aaaStart e parar tootest de nós de cluster do Azure microservices | Microsoft Docs"
description: "Saiba como toouse falha injeção tootest um aplicativo do Service Fabric Iniciando e interrompendo nós de cluster."
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/12/2017
ms.author: lemai
ms.openlocfilehash: 7d3f5147328e6233a67533fbfb2a525aa5fc060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a>Substituindo hello nó iniciar e parar nó APIs com hello API de transição do nó

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a>O que Olá nó parar e iniciar o nó pelas APIs?

Olá parar API de nó (gerenciados: [StopNodeAsync()][stopnode], PowerShell: [Stop ServiceFabricNode][stopnodeps]) para de um nó de malha do serviço.  Um nó de malha do serviço é o processo, não uma VM ou máquina – Olá VM ou máquina ainda será executado.  Restante de saudação do documento hello "nó" significa que o nó de malha do serviço.  Parada de um nó coloca-o em um *interrompido* estado em que ele não é um membro do cluster hello e não é possível hospedar serviços, assim, simulando uma *para baixo* nó.  Isso é útil para injetar falhas em Olá sistema tootest seu aplicativo.  Olá iniciar API de nó (gerenciados: [StartNodeAsync()][startnode], PowerShell: [início ServiceFabricNode][startnodeps]]) reverte Olá parar a API de nó,  o que leva Olá nó tooa back o estado normal.

## <a name="why-are-we-replacing-these"></a>Por que os estamos substituindo?

Conforme descrito anteriormente, um *interrompido* nó de malha do serviço é um nó de destino intencionalmente usando Olá parar API de nó.  Um *para baixo* nó é um nó que está inativo por qualquer outro motivo (por exemplo, Olá VM ou máquina está desativado).  Com hello parar API de nó, sistema Olá não expõe informações toodifferentiate entre *interrompido* nós e *para baixo* nós.

Além disso, alguns erros retornados por essas APIs não são mais tão descritivos quanto poderiam ser.  Por exemplo, chamar hello parar API de nó em uma já *interrompido* nó retornará Erro Olá *InvalidAddress*.  Essa experiência poderia ser melhorada.

Além disso, duração Olá que parou um nó é "infinita" até Olá que API do nó de início é invocado.  Descobrimos que isso pode causar problemas e pode ser propenso a erros.  Por exemplo, vimos problemas em que um usuário chamado hello parar API de nó em um nó e, em seguida, esquecer.  Posteriormente, é claro se o nó de saudação foi *para baixo* ou *interrompido*.


## <a name="introducing-hello-node-transition-apis"></a>Introdução ao Olá APIs de transição do nó

Abordamos esses problemas acima em um novo conjunto de APIs.  Olá nova API de transição de nó (gerenciados: [StartNodeTransitionAsync()][snt]) pode ser usado tootransition um tooa de nó do Service Fabric *interrompido* estado ou tootransition-lo de um *interrompido* tooa de estado normal de backup do estado.  Observe que hello "Start" no nome de saudação do hello API não se refere a toostarting um nó.  Refere-se uma operação assíncrona que o sistema Olá executará tootransition Olá nó tooeither de toobeginning *interrompido* ou estado foi iniciado.

**Uso**

Se Olá API de transição de nó não gerará uma exceção quando invocado, em seguida, Olá sistema aceitou a operação assíncrona hello e executará a ele.  Uma chamada bem-sucedida não implica a conclusão da operação de saudação ainda.  informações de tooget sobre Olá atual estado da operação hello, Olá chamada de API de progresso do nó de transição (gerenciados: [GetNodeTransitionProgressAsync()][gntp]) com o guid de saudação usada ao chamar o nó API de transição para esta operação.  Olá nó transição andamento API retorna um objeto de NodeTransitionProgress.  A propriedade do objeto estado Especifica o estado atual de saudação da operação de saudação.  Se o estado de saudação é "Running", em seguida, Olá operação está em execução.  Se ela for concluída, a operação de saudação concluída sem erros.  Se estiver com defeito, houve um problema ao executar a operação de saudação.  Exceção da propriedade de resultado Olá propriedade indicará quais Olá emitir era.  Consulte https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate para obter mais informações sobre a propriedade State de saudação e a seção de "Exemplo de uso" hello abaixo para obter exemplos de código.


**Diferenciar entre um nó de parada e um nó para baixo** se um nó é *interrompido* usando Olá API de transição de nó, saída de saudação de uma consulta de nó (gerenciados: [GetNodeListAsync()] [ nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) mostrará que este nó tem um *IsStopped* valor da propriedade true.  Observe que isso é diferente do valor Olá Olá *NodeStatus* propriedade dirá *para baixo*.  Se hello *NodeStatus* propriedade tem um valor de *para baixo*, mas *IsStopped* é false, e em seguida, o nó de saudação não foi parado usando Olá API de transição de nó e é  *Para baixo* devido a algum outro motivo.  Se hello *IsStopped* propriedade é true e hello *NodeStatus* é de propriedade *para baixo*, e foi parado usando Olá API de transição do nó.

Iniciando um *interrompido* nó usando Olá nó transição API retornará-toofunction como membro do cluster de saudação normal novamente.  Olá saída da consulta de nó Olá API mostrará *IsStopped* como false, e *NodeStatus* como algo que não é para baixo (por exemplo, para cima).


**Limitado a duração** ao usar o hello nó transição API toostop um nó, parâmetros, uma saudação necessários *stopNodeDurationInSeconds*, representa Olá a quantidade de tempo no nó de saudação tookeep segundos  *interrompido*.  Esse valor deve estar no intervalo, que tem um mínimo de 600 e 14400 máximo permitida de saudação.  Após esse tempo expirar, nó Olá será reiniciado com o estado automaticamente.  Consulte tooSample 1 abaixo para obter um exemplo de uso.

> [!WARNING]
> Evitar a mistura de APIs de transição de nó e Olá nó parar e iniciar APIs de nó.  recomendação de saudação é muito usar apenas a API de transição do nó hello.  > Se um nó já foi interrompido usando Olá parar de API do nó, ele deve ser iniciado usando Olá iniciar nó API primeiro antes de usar o hello > APIs de transição do nó.

> [!WARNING]
> Várias APIs de transição de nó não não possível fazer chamadas em Olá mesmo nó em paralelo.  Em tal situação, Olá API de transição de nó será > lançar um FabricException com um valor de propriedade ErrorCode de NodeTransitionInProgress.  Depois que tiver uma transição de nó em um nó específico > foi iniciado, você deve aguardar até que a operação Olá atinge um estado terminal (ForceCancelled ou com falha, concluído) antes de iniciar uma > transição novos no hello mesmo nó.  São permitidas chamadas de transição de nó paralelas em nós diferentes.


#### <a name="sample-usage"></a>Exemplo de uso


**Exemplo 1** -Olá usos de exemplo a seguir Olá nó transição API toostop um nó.

```csharp
        // Helper function tooget information about a node
        static Node GetNodeInfo(FabricClient fc, string node)
        {
            NodeList n = null;
            while (n == null)
            {
                n = fc.QueryManager.GetNodeListAsync(node).GetAwaiter().GetResult();
                Task.Delay(TimeSpan.FromSeconds(1)).GetAwaiter();
            };

            return n.FirstOrDefault();
        }

        static async Task WaitForStateAsync(FabricClient fc, Guid operationId, TestCommandProgressState targetState)
        {
            NodeTransitionProgress progress = null;

            do
            {
                bool exceptionObserved = false;
                try
                {
                    progress = await fc.TestManager.GetNodeTransitionProgressAsync(operationId, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                    exceptionObserved = true;
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                    exceptionObserved = true;
                }

                if (!exceptionObserved)
                {
                    Console.WriteLine("Current state of operation '{0}': {1}", operationId, progress.State);

                    if (progress.State == TestCommandProgressState.Faulted)
                    {
                        // Inspect hello progress object's Result.Exception.HResult tooget hello error code.
                        Console.WriteLine("'{0}' failed with: {1}, HResult: {2}", operationId, progress.Result.Exception, progress.Result.Exception.HResult);

                        // ...additional logic as required
                    }

                    if (progress.State == targetState)
                    {
                        Console.WriteLine("Target state '{0}' has been reached", targetState);
                        break;
                    }
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (true);
        }

        static async Task StopNodeAsync(FabricClient fc, string nodeName, int durationInSeconds)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            // Create a Guid
            Guid guid = Guid.NewGuid();

            // Create a NodeStopDescription object, which will be used as a parameter into StartNodeTransition
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, durationInSeconds);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStopDescription from above, which will stop hello target node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    // This is retryable
                }
                catch (FabricTransientException fte)
                {
                    // This is retryable
                }

                // Backoff
                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

**Exemplo 2** - Olá seguindo o exemplo inicia um *interrompido* nó.  Ele usa alguns métodos auxiliares do primeiro exemplo de saudação.

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = n.NodeInstanceId;

            // Create a NodeStartDescription object, which will be used as a parameter into StartNodeTransition
            NodeStartDescription description = new NodeStartDescription(guid, n.NodeName, nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

**Exemplo 3** - Olá exemplo a seguir mostra o uso incorreto.  Esse uso está incorreto porque Olá *stopDurationInSeconds* é maior que o intervalo permitida de saudação.  Como StartNodeTransitionAsync() falhará com um erro fatal, operação Olá não foi aceito e API de progresso de saudação não deve ser chamado.  Este exemplo usa alguns métodos auxiliares do primeiro exemplo de saudação.

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds toodemonstrate error
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, 99999);

            try
            {
                await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
            }

            catch (FabricException e)
            {
                Console.WriteLine("Caught {0}", e);
                Console.WriteLine("ErrorCode {0}", e.ErrorCode);
                // Output:
                // Caught System.Fabric.FabricException: System.Runtime.InteropServices.COMException (-2147017629)
                // StopDurationInSeconds is out of range ---> System.Runtime.InteropServices.COMException: Exception from HRESULT: 0x80071C63
                // << Parts of exception omitted>>
                //
                // ErrorCode InvalidDuration
            }
        }
```

**Exemplo 4** - Olá exemplo a seguir mostra as informações de erro de saudação que serão retornadas de saudação nó transição andamento API quando operação Olá iniciada pelo Olá API de transição do nó é aceito, mas falha posteriormente durante a execução.  No caso de Olá falha porque Olá nó transição API tentativas toostart um nó que não existe.  Este exemplo usa alguns métodos auxiliares do primeiro exemplo de saudação.

```csharp
        static async Task StartNodeWithNonexistentNodeAsync(FabricClient fc)
        {
            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = 12345;

            // Intentionally use a nonexistent node
            NodeStartDescription description = new NodeStartDescription(guid, "NonexistentNode", nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hello desired state is reached.  In this case, it will end up in hello Faulted state since hello node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect hello progress object's Result.Exception.HResult tooget hello error code.
            // In this case, it will be NodeNotFound.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Faulted).ConfigureAwait(false);
        }
```

[stopnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StopNodeAsync_System_String_System_Numerics_BigInteger_System_Fabric_CompletionMode_
[stopnodeps]: https://msdn.microsoft.com/library/mt125982.aspx
[startnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StartNodeAsync_System_String_System_Numerics_BigInteger_System_String_System_Int32_System_Fabric_CompletionMode_System_Threading_CancellationToken_
[startnodeps]: https://msdn.microsoft.com/library/mt163520.aspx
[nodequery]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient#System_Fabric_FabricClient_QueryClient_GetNodeListAsync_System_String_
[nodequeryps]: https://docs.microsoft.com/powershell/servicefabric/vlatest/Get-ServiceFabricNode?redirectedfrom=msdn
[snt]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_StartNodeTransitionAsync_System_Fabric_Description_NodeTransitionDescription_System_TimeSpan_System_Threading_CancellationToken_
[gntp]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_GetNodeTransitionProgressAsync_System_Guid_System_TimeSpan_System_Threading_CancellationToken_
