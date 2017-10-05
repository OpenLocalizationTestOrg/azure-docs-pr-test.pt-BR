---
title: Relatar e verificar a integridade com o Service Fabric do Azure| Microsoft Docs
description: "Saiba como enviar relatórios de integridade do seu código de serviço e como verificar a integridade do serviço usando as ferramentas de monitoramento de integridade fornecidas pelo Azure Service Fabric."
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
ms.openlocfilehash: 83981d5bec14c06c509f1a8a4153dc23298f5ce0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="44ac7-103">Relatar e verificar a integridade de serviço</span><span class="sxs-lookup"><span data-stu-id="44ac7-103">Report and check service health</span></span>
<span data-ttu-id="44ac7-104">Quando seus serviços enfrentam problemas, sua capacidade de reagir e corrigir os incidentes e as interrupções depende da sua capacidade de detectar os problemas rapidamente.</span><span class="sxs-lookup"><span data-stu-id="44ac7-104">When your services encounter problems, your ability to respond to and fix incidents and outages depends on your ability to detect the issues quickly.</span></span> <span data-ttu-id="44ac7-105">Se relatar problemas e falhas ao gerenciador de integridade do Azure Service Fabric usando seu código de serviço, você pode usar ferramentas padrão de monitoramento de integridade fornecidas pelo Service Fabric para verificar o status de integridade.</span><span class="sxs-lookup"><span data-stu-id="44ac7-105">If you report problems and failures to the Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides to check the health status.</span></span>

<span data-ttu-id="44ac7-106">Há três maneiras de relatar a integridade no serviço:</span><span class="sxs-lookup"><span data-stu-id="44ac7-106">There are three ways that you can report health from the service:</span></span>

* <span data-ttu-id="44ac7-107">Usar os objetos [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) ou [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).</span><span class="sxs-lookup"><span data-stu-id="44ac7-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="44ac7-108">Você pode usar os objetos `Partition` e `CodePackageActivationContext` para relatar a integridade de elementos que fazem parte do contexto atual.</span><span class="sxs-lookup"><span data-stu-id="44ac7-108">You can use the `Partition` and `CodePackageActivationContext` objects to report the health of elements that are part of the current context.</span></span> <span data-ttu-id="44ac7-109">Por exemplo, o código que é executado como parte de uma réplica pode relatar a integridade apenas dessa réplica, da partição a qual pertence e do aplicativo do qual faz parte.</span><span class="sxs-lookup"><span data-stu-id="44ac7-109">For example, code that runs as part of a replica can report health only on that replica, the partition that it belongs to, and the application that it is a part of.</span></span>
* <span data-ttu-id="44ac7-110">Usar o `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="44ac7-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="44ac7-111">Você poderá usar o `FabricClient` para relatar a integridade do código do serviço se o cluster não for [seguro](service-fabric-cluster-security.md) ou se o serviço estiver sendo executado com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="44ac7-111">You can use `FabricClient` to report health from the service code if the cluster is not [secure](service-fabric-cluster-security.md) or if the service is running with admin privileges.</span></span> <span data-ttu-id="44ac7-112">A maioria dos cenários do mundo real não usa clusters inseguros ou fornece privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="44ac7-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="44ac7-113">Com o `FabricClient`, você poderá relatar a integridade de qualquer entidade que faz parte do cluster.</span><span class="sxs-lookup"><span data-stu-id="44ac7-113">With `FabricClient`, you can report health on any entity that is a part of the cluster.</span></span> <span data-ttu-id="44ac7-114">No entanto, o ideal é que o código do serviço envie apenas relatórios relacionados à sua própria integridade.</span><span class="sxs-lookup"><span data-stu-id="44ac7-114">Ideally, however, service code should only send reports that are related to its own health.</span></span>
* <span data-ttu-id="44ac7-115">Use as APIs REST no cluster, no aplicativo, no aplicativo implantado, no serviço, no pacote de serviço, na partição, na réplica ou nos níveis de nó.</span><span class="sxs-lookup"><span data-stu-id="44ac7-115">Use the REST APIs at the cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="44ac7-116">Isso pode ser usado para relatar a integridade no interior de um contêiner.</span><span class="sxs-lookup"><span data-stu-id="44ac7-116">This can be used to report health from within a container.</span></span>

<span data-ttu-id="44ac7-117">Este artigo apresenta um exemplo que relata a integridade do código de serviço.</span><span class="sxs-lookup"><span data-stu-id="44ac7-117">This article walks you through an example that reports health from the service code.</span></span> <span data-ttu-id="44ac7-118">O exemplo também mostra como as ferramentas fornecidas pelo Service Fabric podem ser usadas para verificar o status de integridade.</span><span class="sxs-lookup"><span data-stu-id="44ac7-118">The example also shows how the tools provided by Service Fabric can be used to check the health status.</span></span> <span data-ttu-id="44ac7-119">Este artigo é uma rápida introdução aos recursos de monitoramento de integridade do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="44ac7-119">This article is intended to be a quick introduction to the health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="44ac7-120">Para obter informações mais detalhadas, você pode ler a série de artigos explicativos sobre integridade, começando com o link no fim deste artigo.</span><span class="sxs-lookup"><span data-stu-id="44ac7-120">For more detailed information, you can read the series of in-depth articles about health that start with the link at the end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44ac7-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="44ac7-121">Prerequisites</span></span>
<span data-ttu-id="44ac7-122">Você deve ter o seguinte instalado:</span><span class="sxs-lookup"><span data-stu-id="44ac7-122">You must have the following installed:</span></span>

* <span data-ttu-id="44ac7-123">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="44ac7-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="44ac7-124">SDK da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="44ac7-124">Service Fabric SDK</span></span>

## <a name="to-create-a-local-secure-dev-cluster"></a><span data-ttu-id="44ac7-125">Para criar um cluster de desenvolvimento local seguro</span><span class="sxs-lookup"><span data-stu-id="44ac7-125">To create a local secure dev cluster</span></span>
* <span data-ttu-id="44ac7-126">Abra o PowerShell com privilégios de administrador e execute os comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="44ac7-126">Open PowerShell with admin privileges, and run the following commands:</span></span>

![Comandos que mostram como criar um cluster de desenvolvimento seguro](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="to-deploy-an-application-and-check-its-health"></a><span data-ttu-id="44ac7-128">Para implantar um aplicativo e verificar sua integridade</span><span class="sxs-lookup"><span data-stu-id="44ac7-128">To deploy an application and check its health</span></span>
1. <span data-ttu-id="44ac7-129">Abra o Visual Studio como administrador.</span><span class="sxs-lookup"><span data-stu-id="44ac7-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="44ac7-130">Crie um projeto usando o modelo **Serviço com Estado** .</span><span class="sxs-lookup"><span data-stu-id="44ac7-130">Create a project by using the **Stateful Service** template.</span></span>
   
    ![Criar um aplicativo do Service Fabric com serviço com estado](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="44ac7-132">Pressione **F5** para executar o aplicativo no modo de depuração.</span><span class="sxs-lookup"><span data-stu-id="44ac7-132">Press **F5** to run the application in debug mode.</span></span> <span data-ttu-id="44ac7-133">O aplicativo é implantado no cluster local.</span><span class="sxs-lookup"><span data-stu-id="44ac7-133">The application is deployed to the local cluster.</span></span>
4. <span data-ttu-id="44ac7-134">Depois que o aplicativo estiver em execução, clique com o botão direito do mouse no ícone do Gerenciador de Cluster Local na área de notificação e selecione **Gerenciar Cluster Local** no menu de atalho para abrir o Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="44ac7-134">After the application is running, right-click the Local Cluster Manager icon in the notification area and select **Manage Local Cluster** from the shortcut menu to open Service Fabric Explorer.</span></span>
   
    ![Abra o Service Fabric Explorer na área de notificação](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="44ac7-136">A integridade do aplicativo deve ser exibida como nesta imagem.</span><span class="sxs-lookup"><span data-stu-id="44ac7-136">The application health should be displayed as in this image.</span></span> <span data-ttu-id="44ac7-137">Neste momento, o aplicativo deve estar íntegro, sem erros.</span><span class="sxs-lookup"><span data-stu-id="44ac7-137">At this time, the application should be healthy with no errors.</span></span>
   
    ![Aplicativo de integridade no Gerenciador do Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="44ac7-139">Você também pode verificar a integridade usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="44ac7-139">You can also check the health by using PowerShell.</span></span> <span data-ttu-id="44ac7-140">Você pode usar ```Get-ServiceFabricApplicationHealth``` para verificar a integridade de um aplicativo e ```Get-ServiceFabricServiceHealth``` para verificar a integridade de um serviço.</span><span class="sxs-lookup"><span data-stu-id="44ac7-140">You can use ```Get-ServiceFabricApplicationHealth``` to check an application's health, and you can use ```Get-ServiceFabricServiceHealth``` to check a service's health.</span></span> <span data-ttu-id="44ac7-141">O relatório de integridade para o mesmo aplicativo no PowerShell está nesta imagem.</span><span class="sxs-lookup"><span data-stu-id="44ac7-141">The health report for the same application in PowerShell is in this image.</span></span>
   
    ![Aplicativo de integridade no PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="to-add-custom-health-events-to-your-service-code"></a><span data-ttu-id="44ac7-143">Para adicionar eventos de integridade personalizados ao seu código de serviço</span><span class="sxs-lookup"><span data-stu-id="44ac7-143">To add custom health events to your service code</span></span>
<span data-ttu-id="44ac7-144">Os modelos de projeto do Service Fabric no Visual Studio contêm código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="44ac7-144">The Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="44ac7-145">As etapas a seguir mostram como você pode relatar eventos de integridade personalizados do seu código de serviço.</span><span class="sxs-lookup"><span data-stu-id="44ac7-145">The following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="44ac7-146">Esses relatórios serão exibidos automaticamente nas ferramentas padrão para monitoramento de integridade fornecidas pelo Service Fabric, como o Service Fabric Explorer, a exibição de integridade do Portal do Azure e o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="44ac7-146">Such reports show up automatically in the standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="44ac7-147">Abra novamente o aplicativo que você criou anteriormente no Visual Studio ou crie um novo usando o modelo de **Serviço com Estado** do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="44ac7-147">Reopen the application that you created previously in Visual Studio, or create a new application by using the **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="44ac7-148">Abra o arquivo Stateful1.cs e encontre a chamada `myDictionary.TryGetValueAsync` no método `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="44ac7-148">Open the Stateful1.cs file, and find the `myDictionary.TryGetValueAsync` call in the `RunAsync` method.</span></span> <span data-ttu-id="44ac7-149">Você pode ver que esse método retorna um `result` que mantém o valor atual do contador, pois a lógica principal desse aplicativo é manter uma contagem em execução.</span><span class="sxs-lookup"><span data-stu-id="44ac7-149">You can see that this method returns a `result` that holds the current value of the counter because the key logic in this application is to keep a count running.</span></span> <span data-ttu-id="44ac7-150">Se esse fosse um aplicativo real e a falta de resultado representasse uma falha, seria necessário sinalizar esse evento.</span><span class="sxs-lookup"><span data-stu-id="44ac7-150">If this were a real application, and if the lack of result represented a failure, you would want to flag that event.</span></span>
3. <span data-ttu-id="44ac7-151">Para relatar um evento de integridade quando a falta de resultado representa uma falha, adicione as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="44ac7-151">To report a health event when the lack of result represents a failure, add the following steps.</span></span>
   
    <span data-ttu-id="44ac7-152">a.</span><span class="sxs-lookup"><span data-stu-id="44ac7-152">a.</span></span> <span data-ttu-id="44ac7-153">Adicione o namespace `System.Fabric.Health` ao arquivo Stateful1.cs.</span><span class="sxs-lookup"><span data-stu-id="44ac7-153">Add the `System.Fabric.Health` namespace to the Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="44ac7-154">b.</span><span class="sxs-lookup"><span data-stu-id="44ac7-154">b.</span></span> <span data-ttu-id="44ac7-155">Adicione o seguinte código após a chamada `myDictionary.TryGetValueAsync`</span><span class="sxs-lookup"><span data-stu-id="44ac7-155">Add the following code after the `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="44ac7-156">Relatamos a integridade da réplica porque ela está sendo relatada de um serviço com estado.</span><span class="sxs-lookup"><span data-stu-id="44ac7-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="44ac7-157">O parâmetro `HealthInformation` armazena informações sobre o problema de integridade que está sendo relatado.</span><span class="sxs-lookup"><span data-stu-id="44ac7-157">The `HealthInformation` parameter stores information about the health issue that's being reported.</span></span>
   
    <span data-ttu-id="44ac7-158">Se você tiver criado um serviço sem estado, use o código a seguir</span><span class="sxs-lookup"><span data-stu-id="44ac7-158">If you had created a stateless service, use the following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="44ac7-159">Se o serviço estiver sendo executado com privilégios de administrador ou se o cluster não for [seguro](service-fabric-cluster-security.md), também será possível usar `FabricClient` para relatar a integridade conforme mostrado nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="44ac7-159">If your service is running with admin privileges or if the cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` to report health as shown in the following steps.</span></span>  
   
    <span data-ttu-id="44ac7-160">a.</span><span class="sxs-lookup"><span data-stu-id="44ac7-160">a.</span></span> <span data-ttu-id="44ac7-161">Crie a instância do `var myDictionary` após a declaração `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="44ac7-161">Create the `FabricClient` instance after the `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="44ac7-162">b.</span><span class="sxs-lookup"><span data-stu-id="44ac7-162">b.</span></span> <span data-ttu-id="44ac7-163">Adicione o seguinte código após a chamada `myDictionary.TryGetValueAsync` :</span><span class="sxs-lookup"><span data-stu-id="44ac7-163">Add the following code after the `myDictionary.TryGetValueAsync` call.</span></span>
   
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
5. <span data-ttu-id="44ac7-164">Vamos simular essa falha e ver como ela é exibida nas ferramentas de monitoramento de integridade.</span><span class="sxs-lookup"><span data-stu-id="44ac7-164">Let's simulate this failure and see it show up in the health monitoring tools.</span></span> <span data-ttu-id="44ac7-165">Para simular a falha, comente a primeira linha no código de relatório de integridade adicionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="44ac7-165">To simulate the failure, comment out the first line in the health reporting code that you added earlier.</span></span> <span data-ttu-id="44ac7-166">Depois de comentar a primeira linha, o código se parecerá com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="44ac7-166">After you comment out the first line, the code will look like the following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="44ac7-167">Esse código aciona o relatório de integridade sempre que o `RunAsync` é executado.</span><span class="sxs-lookup"><span data-stu-id="44ac7-167">This code fires the health report each time `RunAsync` executes.</span></span> <span data-ttu-id="44ac7-168">Depois de fazer a alteração, pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="44ac7-168">After you make the change, press **F5** to run the application.</span></span>
6. <span data-ttu-id="44ac7-169">Depois que o aplicativo estiver em execução, abra o Service Fabric Explorer para verificar a integridade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="44ac7-169">After the application is running, open Service Fabric Explorer to check the health of the application.</span></span> <span data-ttu-id="44ac7-170">Desta vez, o Service Fabric Explorer mostra que o aplicativo não está íntegro.</span><span class="sxs-lookup"><span data-stu-id="44ac7-170">This time, Service Fabric Explorer shows that the application is unhealthy.</span></span> <span data-ttu-id="44ac7-171">Isso ocorre devido ao erro relatado no código que adicionamos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="44ac7-171">This is because of the error that was reported from the code that we added previously.</span></span>
   
    ![Aplicativo não íntegro no Gerenciador do Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="44ac7-173">Se você selecionar a réplica primária na exibição de árvore do Service Fabric Explorer, verá que **Estado de Integridade** indica um erro também.</span><span class="sxs-lookup"><span data-stu-id="44ac7-173">If you select the primary replica in the tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="44ac7-174">O Service Fabric Explorer também exibe os detalhes do relatório de integridade que foram adicionados ao parâmetro `HealthInformation` no código.</span><span class="sxs-lookup"><span data-stu-id="44ac7-174">Service Fabric Explorer also displays the health report details that were added to the `HealthInformation` parameter in the code.</span></span> <span data-ttu-id="44ac7-175">Você pode ver os mesmos relatórios de integridade no PowerShell e no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="44ac7-175">You can see the same health reports in PowerShell and the Azure portal.</span></span>
   
    ![Integridade da réplica no Gerenciador do Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="44ac7-177">Esse relatório permanece no gerenciador de integridade até que seja substituído por outro relatório ou até que essa réplica seja excluída.</span><span class="sxs-lookup"><span data-stu-id="44ac7-177">This report remains in the health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="44ac7-178">Como nós não definimos `TimeToLive` para este relatório de integridade no objeto `HealthInformation`, o relatório nunca expira.</span><span class="sxs-lookup"><span data-stu-id="44ac7-178">Because we did not set `TimeToLive` for this health report in the `HealthInformation` object, the report never expires.</span></span>

<span data-ttu-id="44ac7-179">Recomendamos que a integridade seja relatada no nível mais granular. Neste caso, é a réplica.</span><span class="sxs-lookup"><span data-stu-id="44ac7-179">We recommend that health should be reported on the most granular level, which in this case is the replica.</span></span> <span data-ttu-id="44ac7-180">Você também pode relatar a integridade em `Partition`.</span><span class="sxs-lookup"><span data-stu-id="44ac7-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="44ac7-181">Para relatar a integridade em `Application`, `DeployedApplication` e `DeployedServicePackage`, use `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="44ac7-181">To report health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="44ac7-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="44ac7-182">Next steps</span></span>
* [<span data-ttu-id="44ac7-183">Aprofunde-se na integridade do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="44ac7-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="44ac7-184">API REST para relatar a integridade do serviço</span><span class="sxs-lookup"><span data-stu-id="44ac7-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="44ac7-185">API REST para relatar a integridade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="44ac7-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

