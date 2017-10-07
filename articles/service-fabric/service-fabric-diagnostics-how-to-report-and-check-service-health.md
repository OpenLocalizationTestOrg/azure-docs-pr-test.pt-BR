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
# <a name="report-and-check-service-health"></a><span data-ttu-id="0db12-103">Relatar e verificar a integridade de serviço</span><span class="sxs-lookup"><span data-stu-id="0db12-103">Report and check service health</span></span>
<span data-ttu-id="0db12-104">Quando os serviços de encontram problemas, seus incidentes de correção de capacidade toorespond tooand e interrupções depende de sua capacidade toodetect Olá problemas rapidamente.</span><span class="sxs-lookup"><span data-stu-id="0db12-104">When your services encounter problems, your ability toorespond tooand fix incidents and outages depends on your ability toodetect hello issues quickly.</span></span> <span data-ttu-id="0db12-105">Se você relatar problemas e falhas de Gerenciador de integridade do Azure Service Fabric toohello do seu código de serviço, você pode usar ferramentas do Service Fabric fornece o status de integridade de saudação toocheck de monitoramento de integridade padrão.</span><span class="sxs-lookup"><span data-stu-id="0db12-105">If you report problems and failures toohello Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides toocheck hello health status.</span></span>

<span data-ttu-id="0db12-106">Há três maneiras que você pode relatar a integridade do serviço de saudação:</span><span class="sxs-lookup"><span data-stu-id="0db12-106">There are three ways that you can report health from hello service:</span></span>

* <span data-ttu-id="0db12-107">Usar os objetos [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) ou [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).</span><span class="sxs-lookup"><span data-stu-id="0db12-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="0db12-108">Você pode usar o hello `Partition` e `CodePackageActivationContext` tooreport integridade de saudação de elementos que fazem parte do contexto atual de saudação de objetos.</span><span class="sxs-lookup"><span data-stu-id="0db12-108">You can use hello `Partition` and `CodePackageActivationContext` objects tooreport hello health of elements that are part of hello current context.</span></span> <span data-ttu-id="0db12-109">Por exemplo, código que é executado como parte de uma réplica pode reportar integridade somente essa réplica, partição Olá que pertence a e aplicativo hello que ele faz parte do.</span><span class="sxs-lookup"><span data-stu-id="0db12-109">For example, code that runs as part of a replica can report health only on that replica, hello partition that it belongs to, and hello application that it is a part of.</span></span>
* <span data-ttu-id="0db12-110">Usar o `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="0db12-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="0db12-111">Você pode usar `FabricClient` tooreport integridade do código de serviço Olá se Olá cluster não está [segura](service-fabric-cluster-security.md) ou se o serviço de hello está sendo executado com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="0db12-111">You can use `FabricClient` tooreport health from hello service code if hello cluster is not [secure](service-fabric-cluster-security.md) or if hello service is running with admin privileges.</span></span> <span data-ttu-id="0db12-112">A maioria dos cenários do mundo real não usa clusters inseguros ou fornece privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="0db12-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="0db12-113">Com `FabricClient`, você poderá relatar a integridade de qualquer entidade que faz parte do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="0db12-113">With `FabricClient`, you can report health on any entity that is a part of hello cluster.</span></span> <span data-ttu-id="0db12-114">Idealmente, no entanto, o código de serviço deve apenas enviar relatórios de integridade próprio tooits relacionados.</span><span class="sxs-lookup"><span data-stu-id="0db12-114">Ideally, however, service code should only send reports that are related tooits own health.</span></span>
* <span data-ttu-id="0db12-115">Olá Use APIs REST no cluster hello, aplicativo, aplicativo implantado, serviço, o pacote de serviço, partição, réplica ou níveis de nó.</span><span class="sxs-lookup"><span data-stu-id="0db12-115">Use hello REST APIs at hello cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="0db12-116">Isso pode ser usado tooreport a integridade de dentro de um contêiner.</span><span class="sxs-lookup"><span data-stu-id="0db12-116">This can be used tooreport health from within a container.</span></span>

<span data-ttu-id="0db12-117">Este artigo o orienta por meio de um exemplo que relata a integridade do código de saudação do serviço.</span><span class="sxs-lookup"><span data-stu-id="0db12-117">This article walks you through an example that reports health from hello service code.</span></span> <span data-ttu-id="0db12-118">exemplo Hello também mostra como ferramentas Olá fornecidas pela malha do serviço podem ser usado toocheck status de integridade de saudação.</span><span class="sxs-lookup"><span data-stu-id="0db12-118">hello example also shows how hello tools provided by Service Fabric can be used toocheck hello health status.</span></span> <span data-ttu-id="0db12-119">Este artigo é pretendido toobe integridade de toohello uma rápida introdução recursos de malha do serviço de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="0db12-119">This article is intended toobe a quick introduction toohello health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="0db12-120">Para obter mais informações, você pode ler a série de saudação de artigos detalhados sobre integridade que começam com hello link no final deste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="0db12-120">For more detailed information, you can read hello series of in-depth articles about health that start with hello link at hello end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0db12-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0db12-121">Prerequisites</span></span>
<span data-ttu-id="0db12-122">Você deve ter o seguinte Olá instalado:</span><span class="sxs-lookup"><span data-stu-id="0db12-122">You must have hello following installed:</span></span>

* <span data-ttu-id="0db12-123">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="0db12-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="0db12-124">SDK da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="0db12-124">Service Fabric SDK</span></span>

## <a name="toocreate-a-local-secure-dev-cluster"></a><span data-ttu-id="0db12-125">toocreate um cluster de desenvolvimento de segurança local</span><span class="sxs-lookup"><span data-stu-id="0db12-125">toocreate a local secure dev cluster</span></span>
* <span data-ttu-id="0db12-126">Abra o PowerShell com privilégios de administrador e execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0db12-126">Open PowerShell with admin privileges, and run hello following commands:</span></span>

![Comandos que mostram como toocreate um cluster de desenvolvimento seguro](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a><span data-ttu-id="0db12-128">toodeploy um aplicativo e verificar sua integridade</span><span class="sxs-lookup"><span data-stu-id="0db12-128">toodeploy an application and check its health</span></span>
1. <span data-ttu-id="0db12-129">Abra o Visual Studio como administrador.</span><span class="sxs-lookup"><span data-stu-id="0db12-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="0db12-130">Criar um projeto usando Olá **serviço de monitoração de estado** modelo.</span><span class="sxs-lookup"><span data-stu-id="0db12-130">Create a project by using hello **Stateful Service** template.</span></span>
   
    ![Criar um aplicativo do Service Fabric com serviço com estado](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="0db12-132">Pressione **F5** aplicativo hello de toorun no modo de depuração.</span><span class="sxs-lookup"><span data-stu-id="0db12-132">Press **F5** toorun hello application in debug mode.</span></span> <span data-ttu-id="0db12-133">aplicativo Hello é cluster local toohello implantado.</span><span class="sxs-lookup"><span data-stu-id="0db12-133">hello application is deployed toohello local cluster.</span></span>
4. <span data-ttu-id="0db12-134">Depois que o aplicativo hello está em execução, ícone do Gerenciador de Cluster Local Olá na área de notificação hello e selecione **gerenciar o Cluster Local** de tooopen de menu de atalho Olá Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="0db12-134">After hello application is running, right-click hello Local Cluster Manager icon in hello notification area and select **Manage Local Cluster** from hello shortcut menu tooopen Service Fabric Explorer.</span></span>
   
    ![Abra o Service Fabric Explorer na área de notificação](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="0db12-136">integridade do aplicativo Hello deve ser exibida como esta imagem.</span><span class="sxs-lookup"><span data-stu-id="0db12-136">hello application health should be displayed as in this image.</span></span> <span data-ttu-id="0db12-137">Neste momento, o aplicativo hello deverão estar Íntegro sem erros.</span><span class="sxs-lookup"><span data-stu-id="0db12-137">At this time, hello application should be healthy with no errors.</span></span>
   
    ![Aplicativo de integridade no Gerenciador do Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="0db12-139">Você também pode verificar a integridade de saudação usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0db12-139">You can also check hello health by using PowerShell.</span></span> <span data-ttu-id="0db12-140">Você pode usar ```Get-ServiceFabricApplicationHealth``` toocheck integridade de um aplicativo e você pode usar ```Get-ServiceFabricServiceHealth``` toocheck integridade do serviço.</span><span class="sxs-lookup"><span data-stu-id="0db12-140">You can use ```Get-ServiceFabricApplicationHealth``` toocheck an application's health, and you can use ```Get-ServiceFabricServiceHealth``` toocheck a service's health.</span></span> <span data-ttu-id="0db12-141">Olá relatório de integridade de saudação do mesmo aplicativo no PowerShell é nesta imagem.</span><span class="sxs-lookup"><span data-stu-id="0db12-141">hello health report for hello same application in PowerShell is in this image.</span></span>
   
    ![Aplicativo de integridade no PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a><span data-ttu-id="0db12-143">código de serviço tooyour do eventos de integridade personalizado tooadd</span><span class="sxs-lookup"><span data-stu-id="0db12-143">tooadd custom health events tooyour service code</span></span>
<span data-ttu-id="0db12-144">modelos de projeto do Service Fabric Olá no Visual Studio contêm o código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="0db12-144">hello Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="0db12-145">Olá etapas a seguir mostram como você pode relatar eventos de integridade personalizado no seu código de serviço.</span><span class="sxs-lookup"><span data-stu-id="0db12-145">hello following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="0db12-146">Esses relatórios mostram automaticamente em ferramentas padrão de saudação do Service Fabric fornece, como Service Fabric Explorer, exibição de integridade do portal do Azure e do PowerShell de monitoramento de integridade.</span><span class="sxs-lookup"><span data-stu-id="0db12-146">Such reports show up automatically in hello standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="0db12-147">Reabra o aplicativo hello que você criou anteriormente no Visual Studio, ou criar um novo aplicativo usando Olá **serviço de monitoração de estado** modelo do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0db12-147">Reopen hello application that you created previously in Visual Studio, or create a new application by using hello **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="0db12-148">Abrir o arquivo de Stateful1.cs hello e localize Olá `myDictionary.TryGetValueAsync` chamar hello `RunAsync` método.</span><span class="sxs-lookup"><span data-stu-id="0db12-148">Open hello Stateful1.cs file, and find hello `myDictionary.TryGetValueAsync` call in hello `RunAsync` method.</span></span> <span data-ttu-id="0db12-149">Você pode ver que esse método retorna um `result` que mantém Olá valor atual do contador de saudação porque a lógica de chave Olá neste aplicativo é tookeep um execução de contagem.</span><span class="sxs-lookup"><span data-stu-id="0db12-149">You can see that this method returns a `result` that holds hello current value of hello counter because hello key logic in this application is tookeep a count running.</span></span> <span data-ttu-id="0db12-150">Se esse fosse um aplicativo real, e falta de saudação do resultado representado uma falha, você desejaria tooflag desse evento.</span><span class="sxs-lookup"><span data-stu-id="0db12-150">If this were a real application, and if hello lack of result represented a failure, you would want tooflag that event.</span></span>
3. <span data-ttu-id="0db12-151">tooreport um evento de integridade quando falta de saudação do resultado representa uma falha, adicione Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="0db12-151">tooreport a health event when hello lack of result represents a failure, add hello following steps.</span></span>
   
    <span data-ttu-id="0db12-152">a.</span><span class="sxs-lookup"><span data-stu-id="0db12-152">a.</span></span> <span data-ttu-id="0db12-153">Adicionar Olá `System.Fabric.Health` namespace toohello Stateful1.cs arquivo.</span><span class="sxs-lookup"><span data-stu-id="0db12-153">Add hello `System.Fabric.Health` namespace toohello Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="0db12-154">b.</span><span class="sxs-lookup"><span data-stu-id="0db12-154">b.</span></span> <span data-ttu-id="0db12-155">Adicionar Olá código a seguir após Olá `myDictionary.TryGetValueAsync` chamar</span><span class="sxs-lookup"><span data-stu-id="0db12-155">Add hello following code after hello `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="0db12-156">Relatamos a integridade da réplica porque ela está sendo relatada de um serviço com estado.</span><span class="sxs-lookup"><span data-stu-id="0db12-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="0db12-157">Olá `HealthInformation` parâmetro armazena informações sobre o problema de integridade de saudação que está sendo relatado.</span><span class="sxs-lookup"><span data-stu-id="0db12-157">hello `HealthInformation` parameter stores information about hello health issue that's being reported.</span></span>
   
    <span data-ttu-id="0db12-158">Se você tivesse criado um serviço sem monitoração de estado, use Olá código a seguir</span><span class="sxs-lookup"><span data-stu-id="0db12-158">If you had created a stateless service, use hello following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="0db12-159">Se o serviço é executado com privilégios de administrador ou se hello cluster não for [segura](service-fabric-cluster-security.md), você também pode usar `FabricClient` tooreport integridade conforme Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="0db12-159">If your service is running with admin privileges or if hello cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` tooreport health as shown in hello following steps.</span></span>  
   
    <span data-ttu-id="0db12-160">a.</span><span class="sxs-lookup"><span data-stu-id="0db12-160">a.</span></span> <span data-ttu-id="0db12-161">Criar hello `FabricClient` instância após Olá `var myDictionary` declaração.</span><span class="sxs-lookup"><span data-stu-id="0db12-161">Create hello `FabricClient` instance after hello `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="0db12-162">b.</span><span class="sxs-lookup"><span data-stu-id="0db12-162">b.</span></span> <span data-ttu-id="0db12-163">Adicionar Olá código a seguir após Olá `myDictionary.TryGetValueAsync` chamar.</span><span class="sxs-lookup"><span data-stu-id="0db12-163">Add hello following code after hello `myDictionary.TryGetValueAsync` call.</span></span>
   
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
5. <span data-ttu-id="0db12-164">Vamos simular essa falha e ser exibido em ferramentas de monitoramento de integridade de saudação.</span><span class="sxs-lookup"><span data-stu-id="0db12-164">Let's simulate this failure and see it show up in hello health monitoring tools.</span></span> <span data-ttu-id="0db12-165">Falha de saudação toosimulate, comente a primeira linha hello integridade Olá código de relatório que você adicionou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0db12-165">toosimulate hello failure, comment out hello first line in hello health reporting code that you added earlier.</span></span> <span data-ttu-id="0db12-166">Depois que você comentar a primeira linha de saudação, código Olá se parecerá com hello exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="0db12-166">After you comment out hello first line, hello code will look like hello following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="0db12-167">Esse código é acionado relatório de integridade Olá sempre `RunAsync` executa.</span><span class="sxs-lookup"><span data-stu-id="0db12-167">This code fires hello health report each time `RunAsync` executes.</span></span> <span data-ttu-id="0db12-168">Após você alterar hello, pressione **F5** aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="0db12-168">After you make hello change, press **F5** toorun hello application.</span></span>
6. <span data-ttu-id="0db12-169">Depois que o aplicativo hello está em execução, abra integridade de saudação do Service Fabric Explorer toocheck do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0db12-169">After hello application is running, open Service Fabric Explorer toocheck hello health of hello application.</span></span> <span data-ttu-id="0db12-170">Neste momento, o Service Fabric Explorer mostra que o aplicativo hello está íntegro.</span><span class="sxs-lookup"><span data-stu-id="0db12-170">This time, Service Fabric Explorer shows that hello application is unhealthy.</span></span> <span data-ttu-id="0db12-171">Isso é devido a erro de saudação que foi relatado do código de saudação que adicionamos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0db12-171">This is because of hello error that was reported from hello code that we added previously.</span></span>
   
    ![Aplicativo não íntegro no Gerenciador do Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="0db12-173">Se você selecionar a réplica primária Olá na exibição de árvore de saudação do Service Fabric Explorer, você verá que **estado de integridade** indica um erro, muito.</span><span class="sxs-lookup"><span data-stu-id="0db12-173">If you select hello primary replica in hello tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="0db12-174">Service Fabric Explorer também exibe o relatório de integridade Olá detalhes que foram adicionados toohello `HealthInformation` parâmetro no código de saudação.</span><span class="sxs-lookup"><span data-stu-id="0db12-174">Service Fabric Explorer also displays hello health report details that were added toohello `HealthInformation` parameter in hello code.</span></span> <span data-ttu-id="0db12-175">Você pode ver Olá mesmo relatórios de integridade no PowerShell e Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0db12-175">You can see hello same health reports in PowerShell and hello Azure portal.</span></span>
   
    ![Integridade da réplica no Gerenciador do Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="0db12-177">Este relatório permanece no Gerenciador de integridade Olá até que ele seja substituído por outro relatório ou até que essa réplica será excluída.</span><span class="sxs-lookup"><span data-stu-id="0db12-177">This report remains in hello health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="0db12-178">Como nós não definimos `TimeToLive` para este relatório de integridade no hello `HealthInformation` objeto relatório Olá nunca expira.</span><span class="sxs-lookup"><span data-stu-id="0db12-178">Because we did not set `TimeToLive` for this health report in hello `HealthInformation` object, hello report never expires.</span></span>

<span data-ttu-id="0db12-179">É recomendável que a integridade deve ser relatada no nível mais granular hello, que nesse caso é a réplica hello.</span><span class="sxs-lookup"><span data-stu-id="0db12-179">We recommend that health should be reported on hello most granular level, which in this case is hello replica.</span></span> <span data-ttu-id="0db12-180">Você também pode relatar a integridade em `Partition`.</span><span class="sxs-lookup"><span data-stu-id="0db12-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="0db12-181">integridade de tooreport em `Application`, `DeployedApplication`, e `DeployedServicePackage`, use `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="0db12-181">tooreport health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="0db12-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0db12-182">Next steps</span></span>
* [<span data-ttu-id="0db12-183">Aprofunde-se na integridade do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0db12-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="0db12-184">API REST para relatar a integridade do serviço</span><span class="sxs-lookup"><span data-stu-id="0db12-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="0db12-185">API REST para relatar a integridade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="0db12-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

