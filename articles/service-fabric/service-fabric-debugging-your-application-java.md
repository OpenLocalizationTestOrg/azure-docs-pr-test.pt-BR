---
title: Depurar o aplicativo do Azure Service Fabric no Eclipse | Microsoft Docs
description: "Melhore a confiabilidade e o desempenho dos seus serviços desenvolvendo-os e depurando-os no Eclipse em um cluster de desenvolvimento local."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: f3bcee3794de35005bd387ecfae7e6707f3cb5ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="7e8e5-103">Depurar seu aplicativo Java do Service Fabric usando o Eclipse</span><span class="sxs-lookup"><span data-stu-id="7e8e5-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7e8e5-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="7e8e5-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="7e8e5-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="7e8e5-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="7e8e5-106">Inicie um cluster de desenvolvimento local seguindo as etapas em [Configurando o ambiente de desenvolvimento do Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7e8e5-106">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="7e8e5-107">Atualize entryPoint.sh do serviço que você quer depurar para que ele inicie o processo java com parâmetros de depuração remota.</span><span class="sxs-lookup"><span data-stu-id="7e8e5-107">Update entryPoint.sh of the service you wish to debug, so that it starts the java process with remote debug parameters.</span></span> <span data-ttu-id="7e8e5-108">Esse arquivo pode ser encontrado no seguinte local: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="7e8e5-108">This file can be found at the following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="7e8e5-109">Neste exemplo, a porta 8001 foi definida para depuração.</span><span class="sxs-lookup"><span data-stu-id="7e8e5-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="7e8e5-110">Atualize o Manifesto do Aplicativo, definindo a contagem de instâncias ou a contagem de réplicas para o serviço que está sendo depurado como 1.</span><span class="sxs-lookup"><span data-stu-id="7e8e5-110">Update the Application Manifest by setting the instance count or the replica count for the service that is being debugged to 1.</span></span> <span data-ttu-id="7e8e5-111">Essa configuração evita conflitos para a porta que é usada para depuração.</span><span class="sxs-lookup"><span data-stu-id="7e8e5-111">This setting avoids conflicts for the port that is used for debugging.</span></span> <span data-ttu-id="7e8e5-112">Por exemplo, para serviços sem estado, defina ``InstanceCount="1"`` e, para serviços com estado, defina o destino e o tamanho mínimo do conjunto de réplicas para 1, como se segue: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="7e8e5-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set the target and min replica set sizes to 1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="7e8e5-113">Implante o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7e8e5-113">Deploy the application.</span></span>

5. <span data-ttu-id="7e8e5-114">No IDE do Eclipse, escolha **Executar -> Configurações de Depuração -> Aplicativo Java Remoto e propriedades de conexão de entrada** e defina as propriedades da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="7e8e5-114">In the Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set the properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="7e8e5-115">Defina pontos de interrupção nos pontos desejados e depure o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7e8e5-115">Set breakpoints at desired points and debug the application.</span></span>

<span data-ttu-id="7e8e5-116">Se o aplicativo estiver falhando, talvez seja conveniente habilitar os despejos de núcleo.</span><span class="sxs-lookup"><span data-stu-id="7e8e5-116">If the application is crashing, you may also want to enable coredumps.</span></span> <span data-ttu-id="7e8e5-117">Execute ``ulimit -c`` em um shell e, se retornar 0, os despejos de núcleo não estão habilitados.</span><span class="sxs-lookup"><span data-stu-id="7e8e5-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="7e8e5-118">Para habilitar despejos de núcleo ilimitados, execute o seguinte comando: ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="7e8e5-118">To enable unlimited coredumps, execute the following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="7e8e5-119">Você também pode verificar o status usando o comando ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="7e8e5-119">You can also verify the status using the command ``ulimit -a``.</span></span>  <span data-ttu-id="7e8e5-120">Se quiser atualizar o caminho de geração do despejo de núcleo, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="7e8e5-120">If you wanted to update the coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="7e8e5-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7e8e5-121">Next steps</span></span>

* <span data-ttu-id="7e8e5-122">[Coletar logs usando o Diagnóstico do Azure no Linux](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="7e8e5-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="7e8e5-123">[Monitorar e diagnosticar serviços localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7e8e5-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
