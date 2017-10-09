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
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a>Depurar seu aplicativo Java do Service Fabric usando o Eclipse
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
> 

1. Iniciar um cluster de desenvolvimento local, seguindo as etapas de saudação em [configurar seu ambiente de desenvolvimento do Service Fabric](service-fabric-get-started-linux.md).

2. Atualizar entryPoint.sh do serviço de saudação desejar toodebug, para que ele inicie o processo de java Olá com parâmetros de depuração remota. Esse arquivo pode ser encontrado em Olá local a seguir: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``. Neste exemplo, a porta 8001 foi definida para depuração.

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. Atualizar Olá manifesto do aplicativo, definindo a contagem de instâncias de saudação ou hello, contagem de réplica para o serviço de saudação que está sendo depurado too1. Essa configuração evita conflitos de porta de saudação que é usado para depurar. Por exemplo, para serviços sem monitoração de estado, defina ``InstanceCount="1"`` e para serviços com monitoração de estado conjunto Olá min e destino do conjunto de réplicas too1 tamanhos da seguinte maneira: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.

4. Implante o aplicativo hello.

5. No hello IDE do Eclipse, selecione **execução -> configurações de depuração -> aplicativo Java remoto e as propriedades de conexão de entrada** e definir propriedades de saudação da seguinte maneira:

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  Definir pontos de interrupção em pontos desejados e depurar o aplicativo hello.

Se o aplicativo hello estiver falhando, também convém tooenable coredumps. Execute ``ulimit -c`` em um shell e, se retornar 0, os despejos de núcleo não estão habilitados. tooenable coredumps ilimitados, execute Olá comando a seguir: ``ulimit -c unlimited``. Você também pode verificar o status de saudação usando o comando Olá ``ulimit -a``.  Se desejar que o caminho de geração de dump central tooupdate Olá, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``. 

### <a name="next-steps"></a>Próximas etapas

* [Coletar logs usando o Diagnóstico do Azure no Linux](service-fabric-diagnostics-how-to-setup-lad.md).
* [Monitorar e diagnosticar serviços localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).
