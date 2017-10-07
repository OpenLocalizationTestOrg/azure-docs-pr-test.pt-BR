---
title: aaaService Gerenciador de recursos de Cluster de malha - grupos de aplicativos | Microsoft Docs
description: "Visão geral da funcionalidade de grupo de aplicativos no Gerenciador de recursos de Cluster do serviço de malha de saudação do hello"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a>Grupos de tooApplication de Introdução
Gerenciador de recursos de Cluster do Service Fabric normalmente gerencia os recursos de cluster, distribuindo a carga de saudação (representado por [métricas](service-fabric-cluster-resource-manager-metrics.md)) uniformemente em todo o cluster hello. Service Fabric gerencia a capacidade de saudação de nós Olá Olá cluster e hello como um todo via [capacidade](service-fabric-cluster-resource-manager-cluster-description.md). As métricas e a capacidade funcionam muito bem para muitas cargas de trabalho, mas padrões que fazem uso intenso de diferentes Instâncias de Aplicativos do Service Fabric às vezes trazem requisitos adicionais. Por exemplo, você pode querer:

- Reservar alguma capacidade em nós cluster Olá Olá para serviços de saudação dentro de algumas instâncias de aplicativo nomeada
- Limitar Olá o número total de nós Olá serviços dentro de uma instância de aplicativo nomeada são executados (em vez de propagação-los em todo o cluster Olá)
- Definir capacidades na própria instância de aplicativo nomeada Olá número de saudação do toolimit serviços ou o total de consumo de recursos dos serviços de saudação dentro dele

toomeet esses requisitos, Olá Gerenciador de recursos de Cluster do serviço de malha dá suporte a um recurso chamado de grupos de aplicativos.

## <a name="limiting-hello-maximum-number-of-nodes"></a>Limitar o número máximo de saudação de nós
caso de uso mais simples Olá para capacidade de aplicativo é quando uma instância do aplicativo precisa toobe limitado tooa determinado número máximo de nós. Isso consolida todos os serviços na instância de aplicativo para um determinado número de máquinas. A consolidação é útil quando você estiver tentando toopredict ou limitar o uso de recursos físicos pelos serviços de saudação na instância nomeada do aplicativo. 

Olá imagem a seguir mostra uma instância do aplicativo com e sem um número máximo de nós definidos:

<center>
![Instância do aplicativo definindo o número máximo de nós][Image1]
</center>

No exemplo à esquerda do hello, aplicativo hello não tem um número máximo de nós definidos e tem três serviços. Olá Gerenciador de recursos de Cluster tem espalhados todas as réplicas em seis nós disponíveis tooachieve Olá melhor equilíbrio em cluster hello (comportamento padrão de saudação). Exemplo de direito hello, vemos Olá mesmo aplicativo limitado toothree nós.

parâmetro Hello que controla esse comportamento é chamado de MaximumNodes. Esse parâmetro pode ser definido durante a criação do aplicativo ou atualizado para uma instância do aplicativo que já estava em execução.

Powershell

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

C#

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

Em conjunto de saudação de nós, Olá Gerenciador de recursos de Cluster não garante que objetos de serviço serão colocados juntos ou quais nós são usados.

## <a name="application-metrics-load-and-capacity"></a>Métrica, carga e capacidade do aplicativo
Grupos de aplicativos também permitem que você toodefine métricas associadas a uma instância de determinado aplicativo nomeado e a capacidade dessa instância aplicativo para essas métricas. Métricas de aplicativo permitem que você tootrack, reservar e limitar o consumo de recursos Olá dos serviços de saudação dentro dessa instância do aplicativo.

Para cada métrica do aplicativo, há dois valores que podem ser definidos:

- **Capacidade de aplicativo total** – esta configuração representa a capacidade total de saudação do aplicativo hello para uma métrica específica. Olá Gerenciador de recursos de Cluster não permite a criação de saudação de quaisquer novos serviços nessa instância de aplicativo que cause a carga total tooexceed esse valor. Por exemplo, digamos que instância de aplicativo hello tinha uma capacidade de 10 e já tinha a carga de cinco. criação de saudação do serviço com uma carga total padrão de 10 será desativada.
- **Capacidade máxima do nó** – essa configuração especifica Olá máximo total de carga para o aplicativo hello em um único nó. Se a carga será essa capacidade, Olá Gerenciador de recursos de Cluster move nós de tooother de réplicas de modo que hello carga diminui.


Powershell:

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

C#:

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a>Reserva de capacidade
Outro uso comum de grupos de aplicativos é tooensure recursos em Olá cluster são reservados para uma instância de determinado aplicativo. espaço de saudação é sempre reservado quando a instância do aplicativo hello é criada.

A reserva de espaço em cluster Olá para o aplicativo hello acontece imediatamente, mesmo quando:
- instância do aplicativo Hello é criada, mas ainda não tiver todos os serviços dentro dele
- número de saudação de serviços na instância do aplicativo hello muda sempre 
- Serviços de saudação existem mas não estão consumindo recursos Olá 

Reservar recursos para uma instância de aplicativo requer especificar dois parâmetros adicionais: *MinimumNodes* e *NodeReservationCapacity*

- **MinimumNodes** -define o número mínimo de saudação de nós que Olá aplicativo instância deve ser executada.  
- **NodeReservationCapacity** -essa configuração é por métrica para o aplicativo hello. valor de saudação é Olá métrica reservada para o aplicativo hello em qualquer nó onde Olá serviços nesse aplicativo executar.

Combinando **MinimumNodes** e **NodeReservationCapacity** garante uma reserva de carga mínima para o aplicativo hello em cluster hello. Se houver menos restantes capacidade em Olá cluster reserva total de saudação necessários, falha na criação do aplicativo hello. 

Vejamos um exemplo de reserva de capacidade:

<center>
Instâncias do aplicativo definindo a capacidade reservada![][Image2]
</center>

No exemplo à esquerda do hello, os aplicativos não têm qualquer capacidade de aplicativo definidas. Olá Gerenciador de recursos de Cluster de balanceamento de tudo de acordo com as regras de toonormal.

No exemplo hello saudação à direita, digamos que Application1 foi criado com hello configurações a seguir:

- Conjunto de MinimumNodes tootwo
- Uma métrica de aplicativo definida com
  - NodeReservationCapacity de 20

Powershell

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

C#

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

Malha do serviço de reserva a capacidade em dois nós para Application1 e não permitir que os serviços de tooconsume Application2 essa capacidade mesmo se não houver que nenhuma carga está sendo consumida pelos serviços de saudação dentro Application1 no tempo de saudação. Essa capacidade reservada do aplicativo será considerada consumido e contagens contra Olá capacidade nesse nó e o cluster Olá restante.  reserva de saudação é deduzida do hello restantes capacidade cluster imediatamente, mas Olá reservado consumo é deduzido da capacidade de saudação de um nó específico somente quando o objeto de pelo menos um serviço é colocado sobre ele. Essa reserva posterior permite flexibilidade e melhor utilização de recursos já que os recursos são reservados nos nós apenas quando necessário.

## <a name="obtaining-hello-application-load-information"></a>Obtendo informações de carga do aplicativo hello
Para cada aplicativo que tem uma capacidade de aplicativo definidas para uma ou mais métricas, você pode obter informações de saudação sobre carga de agregação Olá relatada pelas réplicas de seus serviços.

Powershell:

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

C#

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

consulta de ApplicationLoad Olá retorna as informações básicas sobre a capacidade do aplicativo que foi especificado para o aplicativo hello Olá. Essas informações incluem informações de nós de mínimo e máximo de saudação e número de saudação aplicativo hello no momento atual. Elas também incluem informações sobre cada métrica de carga do aplicativo, incluindo:

* Nome da métrica: O nome da métrica de saudação.
* Capacidade de reserva: Capacidade de Cluster que está reservada no cluster Olá para este aplicativo.
* Carga do Aplicativo: a Carga Total de réplicas filho deste Aplicativo.
* Capacidade do Aplicativo: valor máximo permitido de Carga do Aplicativo.

## <a name="removing-application-capacity"></a>Removendo a capacidade do aplicativo
Depois de definir parâmetros de capacidade do aplicativo hello para um aplicativo, eles podem ser removidos usando APIs do aplicativo de atualização ou cmdlets do PowerShell. Por exemplo:

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

Este comando remove todos os parâmetros de gerenciamento de capacidade de aplicativo de instância de aplicativo hello. Isso inclui MinimumNodes, MaximumNodes e métricas de saudação do aplicativo, se houver. efeito de saudação do comando de saudação é imediato. Depois que esse comando for concluído, Olá Gerenciador de recursos de Cluster usa o comportamento padrão de saudação para gerenciamento de aplicativos. Os parâmetros de capacidade do aplicativo podem ser especificados novamente por meio de `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.

### <a name="restrictions-on-application-capacity"></a>Restrições à capacidade do aplicativo
Há várias restrições aos parâmetros de Capacidade de Aplicativo que devem ser respeitadas. Se houver erros de validação, nenhuma alteração será feita.

- Todos os parâmetros de inteiro devem ser números não negativos.
- MinimumNodes nunca deve ser maior que MaximumNodes.
- Se as capacidades de uma métrica de carga forem definidas, elas deverão seguir estas regras:
  - A Capacidade de Reserva do Nó não deve ser maior que a Capacidade Máxima do Nó. Por exemplo, você não pode limitar a capacidade de saudação de métrica hello "CPU" em unidades de tootwo nó hello e tente tooreserve três unidades em cada nó.
  - Se MaximumNodes for especificado, em seguida, Olá produto de MaximumNodes e a capacidade máxima do nó deve não ser maior capacidade Total do aplicativo. Por exemplo, digamos que Olá capacidade máxima do nó de métrica de carga "CPU" é definido tooeight. Digamos que também definir Olá too10 máximo de nós. Nesse caso, a Capacidade Total do Aplicativo deve ser maior do que 80 para esta métrica de carga.

restrições de saudação são aplicadas tanto durante a criação de aplicativos e atualizações.

## <a name="how-not-toouse-application-capacity"></a>Como toouse capacidade de aplicativo
- Não tente toouse Olá grupo de aplicativos recursos tooconstrain Olá aplicativo tooa _específico_ subconjunto de nós. Em outras palavras, você pode especificar que o aplicativo hello é executado no máximo cinco nós, mas não quais cinco nós específicos no cluster hello. A restrição de um aplicativo toospecific nós podem ser realizados usando restrições de posicionamento para serviços.
- Não tente toouse Olá capacidade do aplicativo tooensure dois serviços da saudação mesmo aplicativo são colocadas em Olá mesmos nós. Em vez disso, use [afinidade](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) ou [restrições de posicionamento](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).

## <a name="next-steps"></a>Próximas etapas
- Para saber mais sobre como configurar os serviços, [Saiba mais sobre como configurar serviços](service-fabric-cluster-resource-manager-configure-services.md)
- toofind out sobre como Olá Gerenciador de recursos de Cluster gerencia e equilibra a carga no cluster hello, check-out artigo Olá em [balanceamento de carga](service-fabric-cluster-resource-manager-balancing.md)
- Desde o início de saudação e [obter uma introdução toohello Gerenciador de recursos de Cluster do serviço de malha](service-fabric-cluster-resource-manager-introduction.md)
- Para obter mais informações sobre como as métricas funcionam em geral, leia sobre [Métricas de Carga do Service Fabric](service-fabric-cluster-resource-manager-metrics.md)
- Olá Gerenciador de recursos de Cluster tem muitas opções para descrever o cluster hello. toofind mais sobre eles, leia este artigo em [que descreve um cluster do Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
