---
title: "clusters de caos na malha do serviço aaaInduce | Microsoft Docs"
description: "Usando a injeção de falha e as APIs de serviço de análise de Cluster toomanage caos em cluster hello."
services: service-fabric
documentationcenter: .net
author: motanv
manager: anmola
editor: motanv
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: motanv
ms.openlocfilehash: 7e87cae22645fc4ba52e258471d8f3a4ffdb1cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a>Induzir o Controlled Chaos em clusters do Service Fabric
Os sistemas distribuídos em larga escala, como as infraestruturas de nuvem, não são confiáveis por natureza. Malha do Azure do serviço permite que desenvolvedores toowrite confiável serviços distribuídos em uma infraestrutura não confiável. toowrite serviços distribuídos robusto sobre uma infraestrutura não confiável, os desenvolvedores precisam estabilidade de saudação toobe tootest capaz de seus serviços enquanto Olá subjacente infraestrutura confiável está passando por transições de estado complicado toofaults vencimento.

Olá [injeção de falha e o serviço de análise de Cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (também conhecido como Olá falhas Analysis Service) permite que os desenvolvedores Olá tooinduce falhas tootest seus serviços. Esses direcionados simulados falhas, como [reiniciar uma partição](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), pode ajudar o exercício transições de estado hello mais comuns. No entanto, as falhas simuladas direcionadas são tendenciosas por definição e, portanto, podem ignorar bugs que aparecem apenas em uma sequência de transições de estado complicada, longa e difícil de prever. Para um teste imparcial, você pode usar o Chaos.

Caos simula falhas periódicas, intercaladas (normais e anormais) em todo o cluster Olá por longos períodos de tempo. Depois que você configurou caos com taxa de saudação e tipo de saudação de falhas, você pode iniciar caos por meio do c# ou Powershell API toostart gerar falhas no cluster hello e nos serviços. Você pode configurar caos toorun por um período de tempo especificado (por exemplo, para uma hora), após o qual caos interrompe automaticamente, ou você pode chamar a API StopChaos (c# ou Powershell) toostop-lo a qualquer momento.

> [!NOTE]
> Em sua forma atual, caos induz falhas apenas seguras, que implica que na ausência de saudação de falhas externas de uma perda de quorum, ou perda de dados nunca ocorre.
>

Durante a execução caos, ele gera eventos diferentes que capturam o estado de saudação do hello executado no momento da saudação. Por exemplo, um ExecutingFaultsEvent contém todas as falhas de saudação que caos decidiu tooexecute na iteração. Um ValidationFailedEvent contém detalhes de saudação de uma falha de validação (problemas de integridade ou de estabilidade) que foi encontrado durante a validação de saudação do cluster hello. Você pode chamar o relatório de saudação do Olá GetChaosReport API (c# ou Powershell) tooget de execuções de caos. Esses eventos são persistidos em um [dicionário confiável](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), que tem uma política de truncamento determinada por duas configurações: **MaxStoredChaosEventCount** (o valor padrão é 25000) e **StoredActionCleanupIntervalInSeconds** (o valor padrão é 3600). Cada *StoredActionCleanupIntervalInSeconds* verificações caos e todos os mas hello mais recente *MaxStoredChaosEventCount* eventos, são removidos do dicionário de saudação confiável.

## <a name="faults-induced-in-chaos"></a>Falhas induzidas no Chaos
Caos gera falhas em inteiras de cluster do Service Fabric hello e compacta falhas que são vistas em meses ou anos em algumas horas. combinação de saudação de falhas intercaladas com taxa de falhas de alta Olá encontra casos de canto que poderão ser perdidos caso contrário. Este exercício de caos leva tooa um aprimoramento significativo na qualidade do código de saudação do serviço de saudação.

Caos induzir a falhas de saudação categorias a seguir:

* Reiniciar um nó
* Reiniciar um pacote de códigos implantado
* Remover uma réplica
* Reiniciar uma réplica
* Mover uma réplica primária (configurável)
* Mover uma réplica secundária (configurável)

O Chaos é executado em várias iterações. Cada iteração consiste em falhas e período de validação de cluster para Olá especificado. Você pode configurar o tempo de saudação gasto para Olá cluster toostabilize e toosucceed de validação. Se for encontrada uma falha na validação de cluster, caos gera e persistir um ValidationFailedEvent com carimbo de hora de UTC hello e detalhes da falha hello. Por exemplo, considere uma instância de caos definida toorun para uma hora com um máximo de três falhas simultâneas. Caos induzir três falhas e, em seguida, valida a integridade do cluster hello. Ele itera Olá anterior passa etapa até que seja explicitamente interrompido por meio de saudação StopChaosAsync API ou uma hora. Se o cluster de saudação se tornará não íntegro em qualquer iteração (ou seja, ele não estabilizar em Olá passado no MaxClusterStabilizationTimeout), caos gera um ValidationFailedEvent. Esse evento indica que algo deu errado e pode precisar de mais investigação.

tooget que falhas de caos induzido, você pode usar a API GetChaosReport (powershell ou c#). Olá API obtém o próximo segmento de saudação do hello caos relatório com base em token de continuação passado hello ou Olá passado no intervalo de tempo. Você pode especificar Olá ContinuationToken tooget Olá próximo segmento de relatório de caos hello ou você pode especificar Olá-intervalo de tempo por meio de StartTimeUtc e EndTimeUtc, mas você não pode especificar Olá ContinuationToken e o intervalo de tempo de saudação em Olá mesma chamada. Quando há mais de 100 eventos caos, Olá relatório caos é retornado em segmentos onde um segmento contém eventos de caos não mais do que 100.

## <a name="important-configuration-options"></a>Opções de configuração importantes
* **TimeToRun**: tempo total durante o qual o Chaos é executado antes de ser finalizado com êxito. Você pode interromper caos antes que ele tenha executado por período de TimeToRun Olá Olá StopChaos API.

* **MaxClusterStabilizationTimeout**: quantidade máxima de saudação do tempo toowait para Olá cluster toobecome Íntegro antes de produzir um ValidationFailedEvent. Essa espera é tooreduce Olá carga no cluster Olá enquanto está recuperando. Olá verificações realizadas são:
  * Se a integridade do cluster Olá é Okey
  * Se a integridade do serviço Olá é Okey
  * Se o tamanho do conjunto de réplicas de destino de saudação é obtida para a partição de serviço Olá
  * Não há réplicas InBuild
* **MaxConcurrentFaults**: Olá número máximo de falhas simultâneas que são induzidos em cada iteração. número mais alto de Olá Olá, hello mais agressiva é caos e Olá failovers e hello estado transição combinações Olá cluster passa por também são mais complexos. 

> [!NOTE]
> Independentemente um valor alto como *MaxConcurrentFaults* tem caos garante - na ausência de saudação de falhas externas - não há perda de quorum ou perda de dados.
>

* **EnableMoveReplicaFaults**: habilita ou desabilita a falhas de saudação que provocam Olá réplicas primárias ou secundárias toomove. Essas falhas estão desabilitadas por padrão.
* **WaitTimeBetweenIterations**: quantidade de saudação do toowait de tempo entre as iterações. Ou seja, Olá que caos fará uma pausa após ter executado uma rodada de falhas e ter concluído a validação correspondente Olá de integridade de saudação do cluster de saudação do tempo. Olá valor mais alto do hello, Olá inferior é a taxa de injeção de média de falhas de saudação.
* **WaitTimeBetweenFaults**: quantidade de saudação do toowait de tempo entre duas falhas consecutivas em uma única iteração. Olá valor mais alto de hello, Olá inferior simultaneidade de saudação do (ou Olá sobreposição entre) falhas.
* **ClusterHealthPolicy**: política de integridade do Cluster é toovalidate usado Olá integridade de cluster Olá entre iterações de caos. Se a integridade do cluster Olá é um erro ou se ocorrer uma exceção inesperada durante a execução de falhas, caos aguardará 30 minutos antes de saudação próxima verificação de integridade - cluster de saudação tooprovide com toorecuperate algum tempo.
* **Contexto**: uma coleção pares chave/valor do tipo (cadeia de caracteres, cadeia de caracteres). mapa de saudação pode ser usado toorecord saber Olá caos executar. Não pode haver mais de 100 desses pares e cada cadeia de caracteres (chave ou valor) pode ter no máximo 4095 caracteres. Este mapa é definido pelo inicializador de saudação do contexto de saudação de repositório Olá caos executar toooptionally sobre Olá específico execute.

## <a name="how-toorun-chaos"></a>Como toorun caos

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using System.Fabric;

using System.Diagnostics;
using System.Fabric.Chaos.DataStructures;

class Program
{
    private class ChaosEventComparer : IEqualityComparer<ChaosEvent>
    {
        public bool Equals(ChaosEvent x, ChaosEvent y)
        {
            return x.TimeStampUtc.Equals(y.TimeStampUtc);
        }

        public int GetHashCode(ChaosEvent obj)
        {
            return obj.TimeStampUtc.GetHashCode();
        }
    }

    static void Main(string[] args)
    {
        var clusterConnectionString = "localhost:19000";
        using (var client = new FabricClient(clusterConnectionString))
        {
            var startTimeUtc = DateTime.UtcNow;
            var stabilizationTimeout = TimeSpan.FromSeconds(30.0);
            var timeToRun = TimeSpan.FromMinutes(60.0);
            var maxConcurrentFaults = 3;

            var parameters = new ChaosParameters(
                stabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun);

            try
            {
                client.TestManager.StartChaosAsync(parameters).GetAwaiter().GetResult();
            }
            catch (FabricChaosAlreadyRunningException)
            {
                Console.WriteLine("An instance of Chaos is already running in hello cluster.");
            }

            var filter = new ChaosReportFilter(startTimeUtc, DateTime.MaxValue);

            var eventSet = new HashSet<ChaosEvent>(new ChaosEventComparer());

            while (true)
            {
                var report = client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult();

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.Add(chaosEvent))
                    {
                        Console.WriteLine(chaosEvent);
                    }
                }

                // When Chaos stops, a StoppedEvent is created.
                // If a StoppedEvent is found, exit hello loop.
                var lastEvent = report.History.LastOrDefault();

                if (lastEvent is StoppedEvent)
                {
                    break;
                }

                Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
            }
        }
    }
}
```

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRun -MaxConcurrentFaults $concurrentFaults -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec

while($true)
{
    $stopped = $false
    $report = Get-ServiceFabricChaosReport -StartTimeUtc $now -EndTimeUtc ([System.DateTime]::MaxValue)

    foreach ($e in $report.History) {

        if(-Not ($events.Contains($e.TimeStampUtc.Ticks)))
        {
            $events.Add($e.TimeStampUtc.Ticks, $e)
            if($e -is [System.Fabric.Chaos.DataStructures.ValidationFailedEvent])
            {
                Write-Host -BackgroundColor White -ForegroundColor Red $e
            }
            else
            {
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    $stopped = $true
                }

                Write-Host $e
            }
        }
    }

    if($stopped -eq $true)
    {
        break
    }

    Start-Sleep -Seconds 1
}

Stop-ServiceFabricChaos
```
