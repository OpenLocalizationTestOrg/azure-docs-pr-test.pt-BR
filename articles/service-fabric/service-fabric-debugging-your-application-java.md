---
title: "aaaDebug seu aplicativo de malha do serviço do Azure no Eclipse | Microsoft Docs"
description: "Melhore Olá confiabilidade e o desempenho de seus serviços, desenvolver e depurá-los no Eclipse em um cluster de desenvolvimento local."
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
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="762ac-103">Depurar seu aplicativo Java do Service Fabric usando o Eclipse</span><span class="sxs-lookup"><span data-stu-id="762ac-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="762ac-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="762ac-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="762ac-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="762ac-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="762ac-106">Iniciar um cluster de desenvolvimento local, seguindo as etapas de saudação em [configurar seu ambiente de desenvolvimento do Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="762ac-106">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="762ac-107">Atualizar entryPoint.sh do serviço de saudação desejar toodebug, para que ele inicie o processo de java Olá com parâmetros de depuração remota.</span><span class="sxs-lookup"><span data-stu-id="762ac-107">Update entryPoint.sh of hello service you wish toodebug, so that it starts hello java process with remote debug parameters.</span></span> <span data-ttu-id="762ac-108">Esse arquivo pode ser encontrado em Olá local a seguir: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="762ac-108">This file can be found at hello following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="762ac-109">Neste exemplo, a porta 8001 foi definida para depuração.</span><span class="sxs-lookup"><span data-stu-id="762ac-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="762ac-110">Atualizar Olá manifesto do aplicativo, definindo a contagem de instâncias de saudação ou hello, contagem de réplica para o serviço de saudação que está sendo depurado too1.</span><span class="sxs-lookup"><span data-stu-id="762ac-110">Update hello Application Manifest by setting hello instance count or hello replica count for hello service that is being debugged too1.</span></span> <span data-ttu-id="762ac-111">Essa configuração evita conflitos de porta de saudação que é usado para depurar.</span><span class="sxs-lookup"><span data-stu-id="762ac-111">This setting avoids conflicts for hello port that is used for debugging.</span></span> <span data-ttu-id="762ac-112">Por exemplo, para serviços sem monitoração de estado, defina ``InstanceCount="1"`` e para serviços com monitoração de estado conjunto Olá min e destino do conjunto de réplicas too1 tamanhos da seguinte maneira: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="762ac-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set hello target and min replica set sizes too1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="762ac-113">Implante o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="762ac-113">Deploy hello application.</span></span>

5. <span data-ttu-id="762ac-114">No hello IDE do Eclipse, selecione **execução -> configurações de depuração -> aplicativo Java remoto e as propriedades de conexão de entrada** e definir propriedades de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="762ac-114">In hello Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set hello properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="762ac-115">Definir pontos de interrupção em pontos desejados e depurar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="762ac-115">Set breakpoints at desired points and debug hello application.</span></span>

<span data-ttu-id="762ac-116">Se o aplicativo hello estiver falhando, também convém tooenable coredumps.</span><span class="sxs-lookup"><span data-stu-id="762ac-116">If hello application is crashing, you may also want tooenable coredumps.</span></span> <span data-ttu-id="762ac-117">Execute ``ulimit -c`` em um shell e, se retornar 0, os despejos de núcleo não estão habilitados.</span><span class="sxs-lookup"><span data-stu-id="762ac-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="762ac-118">tooenable coredumps ilimitados, execute Olá comando a seguir: ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="762ac-118">tooenable unlimited coredumps, execute hello following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="762ac-119">Você também pode verificar o status de saudação usando o comando Olá ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="762ac-119">You can also verify hello status using hello command ``ulimit -a``.</span></span>  <span data-ttu-id="762ac-120">Se desejar que o caminho de geração de dump central tooupdate Olá, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="762ac-120">If you wanted tooupdate hello coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="762ac-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="762ac-121">Next steps</span></span>

* <span data-ttu-id="762ac-122">[Coletar logs usando o Diagnóstico do Azure no Linux](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="762ac-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="762ac-123">[Monitorar e diagnosticar serviços localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="762ac-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
