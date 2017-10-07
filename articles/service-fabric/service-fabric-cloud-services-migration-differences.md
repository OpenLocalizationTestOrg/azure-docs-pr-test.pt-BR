---
title: "aaaDifferences entre serviços de nuvem e malha do serviço | Microsoft Docs"
description: "Uma visão geral conceitual para a migração de aplicativos de serviços de nuvem tooService malha."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 0b87b1d3-88ad-4658-a465-9f05a3376dee
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: bbc5ef4fe0fe1b0da55454cb6b766925030198fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-hello-differences-between-cloud-services-and-service-fabric-before-migrating-applications"></a>Saiba mais sobre as diferenças de saudação entre serviços de nuvem e malha do serviço antes de migrar aplicativos.
Microsoft Azure Service Fabric é uma plataforma de aplicativos de nuvem de última geração Olá para aplicativos distribuídos altamente escalonáveis, altamente confiáveis. Ele apresenta muitos recursos novos para empacotamento, implantação, atualização e gerenciamento de aplicativos em nuvem distribuídos. 

Este é um aplicativo de toomigrating Guia introdutório de serviços de nuvem tooService malha. Ele se concentra principalmente nas diferenças de arquitetura e de design entre os Serviços de Nuvem e o Service Fabric.

## <a name="applications-and-infrastructure"></a>Aplicativos e infraestrutura
Uma diferença fundamental entre serviços de nuvem e malha do serviço é a relação de saudação entre VMs, cargas de trabalho e aplicativos. Uma carga de trabalho aqui é definida como código Olá gravar tooperform uma tarefa específica ou fornecer um serviço.

* **Os Serviços de Nuvem dizem respeito à implantação de aplicativos como máquinas virtuais.** código de saudação que você escreve é tooa firmemente acopladas instância VM, como uma função Web ou trabalho. toodeploy uma carga de trabalho em serviços de nuvem é toodeploy uma ou instâncias de VM mais carga de trabalho Olá execução. Há uma distinção entre aplicativos e máquinas virtuais; portanto, não há nenhuma definição formal de um aplicativo. Um aplicativo pode ser considerado como um conjunto de instâncias de função de trabalho ou Web em uma implantação de Serviços de Nuvem ou toda uma implantação de Serviços de Nuvem. Neste exemplo, um aplicativo é mostrado como um conjunto de instâncias de função.

![Topologia e aplicativos dos Serviços de Nuvem][1]

* **O Service Fabric é sobre como implantar aplicativos tooexisting VMs ou máquinas que executam o serviço de malha no Windows ou Linux.** Serviços de saudação que gravar estão completamente separados do hello subjacente de infraestrutura, que é abstraída pela plataforma de aplicativo do Service Fabric hello, portanto, um aplicativo pode ser implantado toomultiple ambientes. Uma carga de trabalho no Service Fabric é chamada de "serviço", e um ou mais serviços são agrupados em um aplicativo formalmente definido que é executado na plataforma de aplicativo hello Service Fabric. Vários aplicativos podem ser implantado tooa único cluster do Service Fabric.

![Topologia e aplicativos Service Fabric][2]

O Service Fabric em si é uma camada de plataforma de aplicativo que é executada no Windows ou no Linux, enquanto os Serviços de Nuvem são um sistema para a implantação de VMs gerenciadas pelo Azure com cargas de trabalho anexadas.
modelo de aplicativo do Service Fabric Olá tem uma série de vantagens:

* Rapidez na implantação. A criação de instâncias da VM pode ser demorada. Na malha do serviço, as VMs são implantadas somente quando tooform um cluster que hospeda Olá plataforma de aplicativo de malha do serviço. Daí em diante, os pacotes de aplicativos podem ser implantado toohello cluster muito rapidamente.
* Hospedagem de alta densidade. Nos Serviços de Nuvem, uma VM de função de trabalho hospeda uma carga de trabalho. No Service Fabric, aplicativos são independentes das VMs Olá que execução-los, que significa que você pode implantar um grande número de aplicativos tooa pequeno número de máquinas virtuais, que pode reduzir o custo geral para implantações maiores.
* Olá Service Fabric plataforma pode ser executada em qualquer lugar que tem máquinas do Windows Server ou Linux, se ele está Azure ou no local. plataforma de saudação fornece uma camada de abstração pela infraestrutura subjacente Olá para que seu aplicativo possa ser executados em ambientes diferentes. 
* Gerenciamento de aplicativo distribuído. O Service Fabric é uma plataforma que não apenas hospeda aplicativos distribuídos, mas também o ajuda a gerenciar o ciclo de vida independentemente Olá hospeda a VM ou do ciclo de vida da máquina.

## <a name="application-architecture"></a>Arquitetura do aplicativo
Olá arquitetura de um aplicativo de serviços de nuvem geralmente inclui várias dependências de serviço externo, como o barramento de serviço, tabela do Azure e armazenamento de Blob, SQL, Redis e outros toomanage Olá estado e os dados de um aplicativo e a comunicação entre Web e funções de trabalho em uma implantação de serviços de nuvem. Um exemplo de um aplicativo de Serviços de Nuvem completo pode ter esta aparência:  

![Arquitetura dos Serviços de Nuvem][9]

Aplicativos de serviço de malha também podem escolher toouse Olá mesmo serviços externos em um aplicativo completo. Usando este exemplo de arquitetura de serviços de nuvem, o caminho de migração mais simples do hello de serviços de nuvem tooService malha é tooreplace somente implantação do hello serviços de nuvem com um aplicativo de malha do serviço, mantendo Olá Olá a mesma arquitetura geral. Olá Web e funções de trabalho podem ser serviços sem monitoração de estado de malha de porta tooService com alterações mínimas de código.

![Arquitetura do Service Fabric após migração simples][10]

Neste estágio, o sistema de saudação deve continuar toowork Olá mesmo de antes. Aproveitando os recursos de serviço com estado do Service Fabric, os armazenamentos de estado externos podem ser internalizados como serviços com estado, quando for o caso. Isso é mais envolvido que uma migração simple de serviços Web e funções de trabalho tooService malha sem monitoração de estado, pois ele requer a criação de serviços personalizados que fornecem aplicativos de tooyour funcionalidade equivalente como serviços externos Olá foram antes. Olá vantagens de fazer isso: 

* Removendo dependências externas 
* Unificar Olá implantação, gerenciamento e modelos de atualização. 

Uma arquitetura de exemplo resultante da internalização desses serviços poderia ter esta aparência:

![Arquitetura do Service Fabric após migração completa][11]

## <a name="communication-and-workflow"></a>Comunicação e fluxo de trabalho
A maioria dos aplicativos do Serviço de Nuvem consistem em mais de uma camada. Da mesma forma, um aplicativo Service Fabric consiste em mais de um serviço (normalmente muitos serviços). Dois modelos comuns de comunicação têm comunicação direta e por meio de armazenamento durável externo.

### <a name="direct-communication"></a>Comunicação direta
Com a comunicação direta, as camadas podem se comunicar diretamente por meio do ponto de extremidade exposto por cada camada. Em ambientes sem monitoração de estado, como serviços de nuvem, essa significa selecionar uma instância de uma função VM, ou aleatoriamente ou carga de round-robin toobalance e conexão tooits ponto de extremidade diretamente.

![Comunicação direta dos Serviços de Nuvem][5]

 A comunicação direta é um modelo de comunicação comum no Service Fabric. a principal diferença Olá entre serviços de nuvem e malha do serviço está em serviços de nuvem conectar tooa VM, enquanto na malha do serviço a serviço tooa se conectar. Essa é uma distinção importante por duas razões:

* Os serviços do Service Fabric não são toohello associada VMs que hospedam-los; serviços pode mover-se no cluster hello e são na verdade, toomove esperado ao redor por vários motivos: recursos de balanceamento, failover, atualizações de aplicativos e infraestrutura e restrições de posicionamento ou carga. Isso significa que o endereço da instância do serviço pode mudar a qualquer hora. 
* Uma VM no Service Fabric pode hospedar vários serviços, cada um com pontos de extremidade exclusivos.

Malha do serviço fornece um mecanismo de descoberta de serviço, chamado hello Naming Service, que pode ser usado tooresolve endereços de ponto de extremidade dos serviços. 

![Comunicação direta do Service Fabric][6]

### <a name="queues"></a>Filas
Um mecanismo de comunicação comum entre camadas em ambientes sem monitoração de estado, como serviços de nuvem é toouse um toodurably de fila de armazenamento externo armazenar tarefas de trabalho de uma camada tooanother. Um cenário comum é uma camada da web que envia os trabalhos tooan fila do Azure ou o barramento de serviço em que instâncias de função de trabalho podem remover da fila e processar trabalhos de saudação.

![Comunicação em fila dos Serviços de Nuvem][7]

saudação do mesmo modelo de comunicação pode ser usado na malha do serviço. Isso pode ser útil ao migrar um tooService de aplicativo de serviços de nuvem existente malha. 

![Comunicação direta do Service Fabric][8]

## <a name="next-steps"></a>Próximas etapas
Olá caminho de migração mais simples de serviços de nuvem tooService malha é tooreplace somente hello implantação de serviços de nuvem com um aplicativo de serviço de malha, mantendo Olá arquitetura geral do seu aplicativo aproximadamente Olá mesmo. Olá artigo a seguir fornece uma guia toohelp converter um tooa serviço sem monitoração de estado de malha do serviço Web ou função de trabalho.

* [Migração simples: converter um tooa serviço sem monitoração de estado de malha do serviço Web ou função de trabalho](service-fabric-cloud-services-migration-worker-role-stateless-service.md)

<!--Image references-->
[1]: ./media/service-fabric-cloud-services-migration-differences/topology-cloud-services.png
[2]: ./media/service-fabric-cloud-services-migration-differences/topology-service-fabric.png
[5]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-direct.png
[6]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-direct.png
[7]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-queues.png
[8]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-queues.png
[9]: ./media/service-fabric-cloud-services-migration-differences/cloud-services-architecture.png
[10]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-simple.png
[11]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-full.png
