---
title: "aaaApplication cenários e design | Microsoft Docs"
description: "Visão geral das categorias de aplicativos em nuvem no Service Fabric. Discute o design de aplicativo que usa serviços com e sem monitoração de estado."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3a8ca6ea-b8e9-4bc3-9e20-262437d2528e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 7/02/2017
ms.author: mfussell
ms.openlocfilehash: e36d5b2d21a6a1e3e85c9b21190072616e4921e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-scenarios"></a>Cenários de aplicativos do Service Fabric
Malha do serviço do Azure oferece uma plataforma confiável e flexível que permite que você toowrite e executar muitos tipos de aplicativos e serviços comerciais. Esses aplicativos e microservices pode ser com ou sem estado e são com balanceamento de recursos em máquinas virtuais toomaximize eficiência. a arquitetura exclusiva do Service Fabric Olá permite tooperform perto de análise de dados em tempo real, cálculo de memória, transações paralelas e em seus aplicativos de processamento de eventos. Você pode escalar verticalmente (realmente reduzir ou expandir) seus aplicativos com facilidade, de acordo com os requisitos de recurso em constante mudança.

plataforma do Service Fabric Olá no Azure é ideal para Olá categorias de aplicativos a seguir:

* **Serviços altamente disponíveis**: serviços do Service Fabric fornecem failover rápido criando várias réplicas de serviço secundárias. Se um nó, um processo ou um serviço individual falhar devido a toohardware ou outra falha, uma das réplicas secundárias Olá é promovida tooa a réplica primária com o mínimo de perda de serviço.
* **Serviços escalonáveis**: serviços individuais podem ser particionados, permitindo toobe de estado de expansão através do cluster de saudação. Além disso, serviços individuais podem ser criados e removidos imediatamente do hello. Os serviços podem ser rapidamente e facilmente expandidos de algumas instâncias em alguns toothousands de nós de instâncias em vários nós e dimensionados em novamente, dependendo de suas necessidades de recursos. Você pode usar o Service Fabric toobuild esses serviços e gerenciar seu ciclo de vida completo.
* **Cálculo de dados não estático**: Service Fabric permite que dados toobuild, entrada/saída e aplicativos com computação intensiva com monitoração de estado. Malha do serviço permite que a colocação de saudação do processamento (computação) e os dados em aplicativos. Normalmente, quando seu aplicativo requer acesso toodata, é associada a uma camada de cache ou armazenamento de dados externos de latência de rede. Com os serviços do Service Fabric com monitoração de estado, essa latência é eliminada, o que habilita leituras e gravações com mais desempenho. Por exemplo, digamos que você tenha um aplicativo que executa uma seleção de recomendação em tempo real para clientes com um requisito de tempo de ida e volta de menos de 100 milissegundos. características de desempenho e latência de saudação de serviços do Service Fabric (onde computação Olá da seleção de recomendação é colocada com regras e dados de saudação) fornece a um usuário de toohello experiência responsivo em comparação com a implementação padrão de saudação modelo de se ter toofetch Olá necessários dados de armazenamento remoto.  
* **Aplicativos interativos baseados em sessão**: o Service Fabric é útil se os aplicativos, como jogos online ou mensagens instantâneas, exigirem baixa latência em leituras e gravações. Serviço de malha permite você toobuild esses aplicativos interativos, com monitoração de estado sem ter que toocreate um armazenamento separado ou em cache, conforme necessário para aplicativos sem monitoração de estado. (Isso aumenta a latência e potencialmente apresenta problemas de consistência).
* **Análise de dados e fluxos de trabalho**: Olá rápidas leituras e gravações do Service Fabric permitem que os aplicativos que confiável devem processar eventos ou fluxos de dados. Malha do serviço também permite que os aplicativos que descrevem os pipelines de processamento, onde os resultados devem ser confiáveis e passado em toohello próximos estágio sem perda. Isso inclui sistemas transacionais e financeiros, em que as garantias de computação e consistência de dados são essenciais.
* **Coleta de dados, processamento e IoT**: como o Service Fabric trata de grande escala e tem baixa latência por meio de seus serviços com monitoração de estado, é ideal para processamento de dados em milhões de dispositivos onde estão os dados Olá para dispositivo hello e computação Olá localizada.
Vimos vários clientes que criaram sistemas IoT usando o Service Fabric, incluindo a [BMW](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/24/service-fabric-customer-profile-bmw-technology-corporation/), a [Schneider Electric](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/05/service-fabric-customer-profile-schneider-electric/) e a [Mesh Systems](https://blogs.msdn.microsoft.com/azureservicefabric/2016/06/20/service-fabric-customer-profile-mesh-systems/).

## <a name="application-design-case-studies"></a>Estudos de caso de design do aplicativo
Um número de estudos de caso mostrando como o Service Fabric é usado toodesign aplicativos publicado no hello [blog da equipe do Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/) e hello [site de soluções microservices](https://azure.microsoft.com/solutions/microservice-applications/).

## <a name="design-applications-composed-of-stateless-and-stateful-microservices"></a>Projetar aplicativos compostos de microsserviços com e sem monitoração de estado
A criação de aplicativos com funções de trabalho com o Serviço de Nuvem do Azure é um exemplo de serviço sem estado. Por outro lado, com monitoração de estado microservices manter seu estado autoritativo além Olá solicitação e sua resposta. Isso fornece alta disponibilidade e a consistência de estado de saudação por meio de APIs simples que fornecem garantias transacionais com o apoio de replicação. Serviços de monitoração de estado do Service Fabric democratize a alta disponibilidade, colocando-tooall tipos de aplicativos, e não apenas em bancos de dados e outros repositórios de dados. Essa é uma progressão natural. Aplicativos já moveu de bancos de dados puramente relacionais para bancos de dados de tooNoSQL de alta disponibilidade. Agora próprios aplicativos Olá podem ter seu estado de "ativo" e os dados gerenciados dentro delas para obter ganhos de desempenho adicionais sem sacrificar confiabilidade, consistência e disponibilidade.

Ao criar aplicativos que consiste em microservices, você normalmente tem uma combinação de aplicativos web sem monitoração de estado (ASP.NET, Node.js, etc.) chamando para serviços de camada intermediária com e sem monitoração de negócios, todos implantado em Olá mesmo cluster do Service Fabric usando comandos de implantação do Service Fabric hello. Cada um desses serviços é independente com o uso de recursos, confiabilidade e tooscale levar em consideração, melhorando a agilidade no desenvolvimento e ciclo de vida do gerenciamento.

Com monitoração de estado microservices simplificar designs de aplicativos porque eles eliminam a necessidade de saudação de filas adicionais hello e caches que normalmente são necessários tooaddress Olá requisitos de latência e disponibilidade de aplicativos sem monitoração de estado puramente. Como os serviços com monitoração de estado naturalmente são altamente disponível e baixa latência, isso significa que há menos toomanage partes móveis em seu aplicativo como um todo. diagramas de saudação abaixo ilustram as diferenças de saudação entre a criação de um aplicativo sem monitoração de estado e um que é com monitoração de estado. Aproveitando Olá [serviços confiáveis](service-fabric-reliable-services-introduction.md) e [Reliable Actors](service-fabric-reliable-actors-introduction.md) modelos de programação, com monitoração de estado serviços reduzem a complexidade do aplicativo e alcançar alta taxa de transferência e baixa latência.

## <a name="an-application-built-using-stateless-services"></a>Um aplicativo criado usando serviços sem monitoração de estado
![Aplicativo usando serviço sem estado][Image1]

## <a name="an-application-built-using-stateful-services"></a>Um aplicativo criado usando os serviços com monitoração de estado
![Aplicativo usando serviço sem estado][Image2]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Próximas etapas

* Escutar muito[estudos de caso do cliente](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=qDJnf86yC_5206218965
)
* Saiba mais sobre [estudos de caso de cliente](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/)
* Saiba mais sobre [padrões e cenários](service-fabric-patterns-and-scenarios.md)

* Introdução à criação de serviços com e sem monitoração com hello Service Fabric [serviços confiáveis](service-fabric-reliable-services-quick-start.md) e [atores confiáveis](service-fabric-reliable-actors-get-started.md) modelos de programação.
* Consulte também Olá seguintes tópicos:
  * [Fale-me sobre os microsserviços](service-fabric-overview-microservices.md)
  * [Definir e gerenciar o estado do serviço](service-fabric-concepts-state.md)
  * [Disponibilidade dos serviços de malha do serviço](service-fabric-availability-services.md)
  * [Dimensionar serviços do Service Fabric](service-fabric-concepts-scalability.md)
  * [Particionar serviços do Service Fabric](service-fabric-concepts-partitioning.md)

[Image1]: media/service-fabric-application-scenarios/AppwithStatelessServices.jpg
[Image2]: media/service-fabric-application-scenarios/AppwithStatefulServices.jpg
