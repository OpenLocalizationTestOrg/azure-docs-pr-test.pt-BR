---
title: "aaaReport e verificação de integridade com o Azure Service Fabric | Microsoft Docs"
description: "Saiba como relatórios de integridade de toosend do seu código de serviço e como fornece integridade de saudação toocheck do seu serviço usando ferramentas de monitoramento de integridade de saudação que Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a>Relatar e verificar a integridade de serviço
Quando os serviços de encontram problemas, seus incidentes de correção de capacidade toorespond tooand e interrupções depende de sua capacidade toodetect Olá problemas rapidamente. Se você relatar problemas e falhas de Gerenciador de integridade do Azure Service Fabric toohello do seu código de serviço, você pode usar ferramentas do Service Fabric fornece o status de integridade de saudação toocheck de monitoramento de integridade padrão.

Há três maneiras que você pode relatar a integridade do serviço de saudação:

* Usar os objetos [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) ou [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).  
  Você pode usar o hello `Partition` e `CodePackageActivationContext` tooreport integridade de saudação de elementos que fazem parte do contexto atual de saudação de objetos. Por exemplo, código que é executado como parte de uma réplica pode reportar integridade somente essa réplica, partição Olá que pertence a e aplicativo hello que ele faz parte do.
* Usar o `FabricClient`.   
  Você pode usar `FabricClient` tooreport integridade do código de serviço Olá se Olá cluster não está [segura](service-fabric-cluster-security.md) ou se o serviço de hello está sendo executado com privilégios de administrador. A maioria dos cenários do mundo real não usa clusters inseguros ou fornece privilégios de administrador. Com `FabricClient`, você poderá relatar a integridade de qualquer entidade que faz parte do cluster de saudação. Idealmente, no entanto, o código de serviço deve apenas enviar relatórios de integridade próprio tooits relacionados.
* Olá Use APIs REST no cluster hello, aplicativo, aplicativo implantado, serviço, o pacote de serviço, partição, réplica ou níveis de nó. Isso pode ser usado tooreport a integridade de dentro de um contêiner.

Este artigo o orienta por meio de um exemplo que relata a integridade do código de saudação do serviço. exemplo Hello também mostra como ferramentas Olá fornecidas pela malha do serviço podem ser usado toocheck status de integridade de saudação. Este artigo é pretendido toobe integridade de toohello uma rápida introdução recursos de malha do serviço de monitoramento. Para obter mais informações, você pode ler a série de saudação de artigos detalhados sobre integridade que começam com hello link no final deste artigo hello.

## <a name="prerequisites"></a>Pré-requisitos
Você deve ter o seguinte Olá instalado:

* Visual Studio 2015 ou Visual Studio 2017
* SDK da Malha do Serviço

## <a name="toocreate-a-local-secure-dev-cluster"></a>toocreate um cluster de desenvolvimento de segurança local
* Abra o PowerShell com privilégios de administrador e execute Olá comandos a seguir:

![Comandos que mostram como toocreate um cluster de desenvolvimento seguro](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a>toodeploy um aplicativo e verificar sua integridade
1. Abra o Visual Studio como administrador.
2. Criar um projeto usando Olá **serviço de monitoração de estado** modelo.
   
    ![Criar um aplicativo do Service Fabric com serviço com estado](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. Pressione **F5** aplicativo hello de toorun no modo de depuração. aplicativo Hello é cluster local toohello implantado.
4. Depois que o aplicativo hello está em execução, ícone do Gerenciador de Cluster Local Olá na área de notificação hello e selecione **gerenciar o Cluster Local** de tooopen de menu de atalho Olá Service Fabric Explorer.
   
    ![Abra o Service Fabric Explorer na área de notificação](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. integridade do aplicativo Hello deve ser exibida como esta imagem. Neste momento, o aplicativo hello deverão estar Íntegro sem erros.
   
    ![Aplicativo de integridade no Gerenciador do Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. Você também pode verificar a integridade de saudação usando o PowerShell. Você pode usar ```Get-ServiceFabricApplicationHealth``` toocheck integridade de um aplicativo e você pode usar ```Get-ServiceFabricServiceHealth``` toocheck integridade do serviço. Olá relatório de integridade de saudação do mesmo aplicativo no PowerShell é nesta imagem.
   
    ![Aplicativo de integridade no PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a>código de serviço tooyour do eventos de integridade personalizado tooadd
modelos de projeto do Service Fabric Olá no Visual Studio contêm o código de exemplo. Olá etapas a seguir mostram como você pode relatar eventos de integridade personalizado no seu código de serviço. Esses relatórios mostram automaticamente em ferramentas padrão de saudação do Service Fabric fornece, como Service Fabric Explorer, exibição de integridade do portal do Azure e do PowerShell de monitoramento de integridade.

1. Reabra o aplicativo hello que você criou anteriormente no Visual Studio, ou criar um novo aplicativo usando Olá **serviço de monitoração de estado** modelo do Visual Studio.
2. Abrir o arquivo de Stateful1.cs hello e localize Olá `myDictionary.TryGetValueAsync` chamar hello `RunAsync` método. Você pode ver que esse método retorna um `result` que mantém Olá valor atual do contador de saudação porque a lógica de chave Olá neste aplicativo é tookeep um execução de contagem. Se esse fosse um aplicativo real, e falta de saudação do resultado representado uma falha, você desejaria tooflag desse evento.
3. tooreport um evento de integridade quando falta de saudação do resultado representa uma falha, adicione Olá etapas a seguir.
   
    a. Adicionar Olá `System.Fabric.Health` namespace toohello Stateful1.cs arquivo.
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    b. Adicionar Olá código a seguir após Olá `myDictionary.TryGetValueAsync` chamar
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    Relatamos a integridade da réplica porque ela está sendo relatada de um serviço com estado. Olá `HealthInformation` parâmetro armazena informações sobre o problema de integridade de saudação que está sendo relatado.
   
    Se você tivesse criado um serviço sem monitoração de estado, use Olá código a seguir
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. Se o serviço é executado com privilégios de administrador ou se hello cluster não for [segura](service-fabric-cluster-security.md), você também pode usar `FabricClient` tooreport integridade conforme Olá etapas a seguir.  
   
    a. Criar hello `FabricClient` instância após Olá `var myDictionary` declaração.
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    b. Adicionar Olá código a seguir após Olá `myDictionary.TryGetValueAsync` chamar.
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. Vamos simular essa falha e ser exibido em ferramentas de monitoramento de integridade de saudação. Falha de saudação toosimulate, comente a primeira linha hello integridade Olá código de relatório que você adicionou anteriormente. Depois que você comentar a primeira linha de saudação, código Olá se parecerá com hello exemplo a seguir.
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   Esse código é acionado relatório de integridade Olá sempre `RunAsync` executa. Após você alterar hello, pressione **F5** aplicativo hello de toorun.
6. Depois que o aplicativo hello está em execução, abra integridade de saudação do Service Fabric Explorer toocheck do aplicativo hello. Neste momento, o Service Fabric Explorer mostra que o aplicativo hello está íntegro. Isso é devido a erro de saudação que foi relatado do código de saudação que adicionamos anteriormente.
   
    ![Aplicativo não íntegro no Gerenciador do Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. Se você selecionar a réplica primária Olá na exibição de árvore de saudação do Service Fabric Explorer, você verá que **estado de integridade** indica um erro, muito. Service Fabric Explorer também exibe o relatório de integridade Olá detalhes que foram adicionados toohello `HealthInformation` parâmetro no código de saudação. Você pode ver Olá mesmo relatórios de integridade no PowerShell e Olá portal do Azure.
   
    ![Integridade da réplica no Gerenciador do Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

Este relatório permanece no Gerenciador de integridade Olá até que ele seja substituído por outro relatório ou até que essa réplica será excluída. Como nós não definimos `TimeToLive` para este relatório de integridade no hello `HealthInformation` objeto relatório Olá nunca expira.

É recomendável que a integridade deve ser relatada no nível mais granular hello, que nesse caso é a réplica hello. Você também pode relatar a integridade em `Partition`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

integridade de tooreport em `Application`, `DeployedApplication`, e `DeployedServicePackage`, use `CodePackageActivationContext`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a>Próximas etapas
* [Aprofunde-se na integridade do Service Fabric](service-fabric-health-introduction.md)
* [API REST para relatar a integridade do serviço](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [API REST para relatar a integridade do aplicativo](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

