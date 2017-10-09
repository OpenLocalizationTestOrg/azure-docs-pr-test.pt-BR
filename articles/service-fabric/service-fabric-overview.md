---
title: "aaaOverview da malha do serviço no Azure | Microsoft Docs"
description: "Uma visão geral de malha do serviço, em que os aplicativos são compostos de vários microservices tooprovide escala e resiliência. Service Fabric é uma plataforma de sistemas distribuídos usado toobuild escalonável, confiável e gerenciados facilmente aplicativos para a nuvem de saudação."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: masnider
ms.assetid: bbcc652a-a790-4bc4-926b-e8cd966587c0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: mfussell
ms.openlocfilehash: 427fcedf97e6b2aae42d240c63e9f85daed8d962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-service-fabric"></a>Visão geral do Azure Service Fabric
Malha do serviço do Azure é uma plataforma de sistemas distribuídos que torna mais fácil toopackage, implantar e gerenciar contêineres e microservices escalonável e confiável. Service Fabric também aborda os desafios de saudação significativos no desenvolvimento e gerenciamento de aplicativos nativos de nuvem. Desenvolvedores e administradores podem evitar problemas complexos de infraestrutura e se concentrarem na implementação de cargas de trabalho essenciais e exigentes que são escalonáveis, confiáveis e gerenciáveis. Malha do serviço representa a plataforma de última geração Olá para desenvolver e gerenciar esses corporativa, nível 1, aplicativos de escala de nuvem em execução em contêineres.

Este breve vídeo apresenta o Service Fabric e os microsserviços: <center><a target="_blank" href="https://aka.ms/servicefabricvideo">  
<img src="./media/service-fabric-overview/OverviewVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="applications-composed-of-microservices"></a>Aplicativos compostos por microsserviços 
Malha do serviço permite que você toobuild e gerenciar aplicativos de escalonáveis e confiáveis compostos microservices executados em alta densidade em um pool compartilhado de máquinas, que é chamado tooas um cluster. Ele fornece uma toobuild de tempo de execução sofisticados, leve distribuído, escalonável, com e sem monitoração microservices executar em contêineres. Ele também fornece tooprovision de recursos de gerenciamento de aplicativo abrangente, implantar, monitorar, atualização/patch e excluir aplicativos implantados, incluindo os serviços em contêineres.

O Service Fabric é a tecnologia de diversos serviços atuais da Microsoft, incluindo Banco de Dados SQL do Azure, Azure Cosmos DB, Cortana, Microsoft Power BI, Microsoft Intune, Hubs de Eventos do Azure, Hub IoT do Azure, Dynamics 365, Skype for Business e vários serviços principais do Azure.

O Service Fabric é toocreate personalizada nativo serviços de nuvem que podem começar pequenas, conforme necessário e aumentar a escala de toomassive com centenas ou milhares de computadores.

Os serviços em escala da Internet de hoje são criados por microsserviços. Exemplos de microsserviços são gateways de protocolo, perfis de usuário, carrinhos de compra, processamento de inventário, filas e caches. O Service Fabric é uma plataforma de microsserviços que fornece a cada microsserviço (ou contêiner) um nome exclusivo que pode ser com ou sem estado.

Malha do serviço fornece abrangentes em tempo de execução e o ciclo de vida do gerenciamento recursos tooapplications que são compostos desses microservices. Ele hospeda microservices dentro de contêineres que são implantados e ativados no cluster do Service Fabric hello. Uma mudança de máquinas virtuais toocontainers possibilita um aumento de ordem de magnitude de densidade. Da mesma forma, outra ordem de magnitude em densidade será possível quando você move de contêineres toomicroservices nesses contêineres. Por exemplo, um único cluster para um Banco de Dados SQL do Azure engloba centenas de computadores que executam dezenas de milhares de contêineres que hospedam um total de centenas de milhares de bancos de dados. Cada banco de dados é um microsserviço com estado do Service Fabric. 

Para obter mais informações sobre a abordagem de microservices hello, leia [por um aplicativo de toobuilding microservices abordagem?](service-fabric-overview-microservices.md)

## <a name="container-deployment-and-orchestration"></a>Orquestração e implantação de contêiner
O Service Fabric é um [orquestrador de cotêiner](service-fabric-cluster-resource-manager-introduction.md) da Microsoft que implanta microsserviços em um cluster de computadores. Microservices pode ser desenvolvido em muitas maneiras de usar Olá [modelos de programação do Service Fabric](service-fabric-choose-framework.md), [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md), toodeploying [qualquer código de sua escolha](service-fabric-deploy-existing-app.md). É importante, você pode combinar os serviços em processos e serviços em contêineres Olá mesmo aplicativo. Se você quiser apenas muito[implantar e gerenciar contêineres](service-fabric-containers-overview.md), Service Fabric é uma opção ideal como um orquestrador de contêiner.

## <a name="any-os-any-cloud"></a>Qualquer sistema operacional, qualquer nuvem
O Service Fabric pode ser executado em qualquer lugar. Você pode criar clusters para o Service Fabric em muitos ambientes, incluindo o Azure, ou localmente, no Windows Server ou no Linux. Você ainda pode até criar clusters em outras nuvens públicas. Além disso, o ambiente de desenvolvimento de saudação em Olá SDK é **idênticos** toohello ambiente de produção, com nenhum emulador envolvidos. Em outras palavras, o que é executado em seu cluster de desenvolvimento local implanta toohello clusters em outros ambientes.

![Plataforma Service Fabric][Image1]

Para obter mais informações sobre a criação de clusters local, leia [criando um cluster no Windows Server ou Linux](service-fabric-deploy-anywhere.md) ou para criar um cluster do Azure [por meio do portal do Azure de saudação](service-fabric-cluster-creation-via-portal.md).

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Microsserviços com e sem estado para o Service Fabric
Malha do serviço permite que aplicativos toobuild que consistem em microservices ou contêineres. Microservices sem monitoração de estado (como gateways de protocolo e proxies da web) não mantém um estado mutável fora de uma solicitação e sua resposta do serviço de saudação. As funções de trabalho dos Serviços de Nuvem do Azure são um exemplo de serviço sem estado. Microservices com monitoração de estado (como contas de usuário, bancos de dados, dispositivos, carrinhos de compra e filas) manter um estado mutável autoritativo além Olá solicitação e sua resposta. Os aplicativos em escala da Internet de hoje consistem em uma combinação de microsserviços com e sem estado. 

Uma chave differentation com o Service Fabric é seu foco forte na criação de serviços com monitoração de estado, com hello [modelos de programação internos ](service-fabric-choose-framework.md) ou com os serviços em contêineres com monitoração de estado. Olá [cenários de aplicativo](service-fabric-application-scenarios.md) descrevem Olá cenários onde os serviços com monitoração de estado são usados.


## <a name="application-lifecycle-management"></a>Gerenciamento do ciclo de vida de aplicativos
Malha do serviço oferece suporte para CI/CD de aplicativos de nuvem, incluindo os contêineres e ciclo de vida do aplicativo completo de saudação. Esse ciclo de vida inclui o desenvolvimento por meio de implantação, gerenciamento diário e manutenção tooeventual encerramento.

Recursos de gerenciamento de ciclo de vida de aplicativo do Service Fabric permitem aos administradores de aplicativo e IT operadores toouse fluxos de trabalho simples, com pouca tooprovision, implantar, patch e monitoram aplicativos. Esses fluxos de trabalho internos reduzem significativamente a carga do hello aplicativos tookeep de operadores de TI continuamente disponíveis.

A maioria dos aplicativos consiste em uma combinação de microsserviços com e sem estado, contêineres e outros executáveis que são implantados juntos. Por ter tipos fortes em aplicativos hello, Service Fabric permite a implantação de saudação de várias instâncias do aplicativo. Cada instância é gerenciada e atualizada independentemente. Vale destacar que o Service Fabric pode implantar contêineres ou qualquer executável e torná-los confiáveis. Por exemplo, o Service Fabric implanta .NET, ASP.NET Core, node.js, contêineres do Windows, contêineres do Linux, máquinas virtuais Java, scripts, Angular ou literalmente qualquer outro item que componha seu aplicativo.

O Service Fabric é integrado com as ferramentas de CI/CD como [Visual Studio Team Services](https://www.visualstudio.com/team-services/), [Jenkins](https://jenkins.io/index.html) e [Octopus Deploy](https://octopus.com/) e pode ser usado com qualquer outra ferramenta de CI/CD popular.

Para saber mais sobre o gerenciamento do ciclo de vida do aplicativo, leia [Ciclo de vida do aplicativo](service-fabric-application-lifecycle.md). Para obter mais informações sobre como toodeploy qualquer código, consulte [implantar um executável de convidado](service-fabric-deploy-existing-app.md).

## <a name="key-capabilities"></a>Principais recursos
Ao usar a Malha do Serviço, você pode:

* Implante datacenters tooAzure ou tooon locais que executam o Windows ou Linux com zero alterações de código. Gravar uma vez e, em seguida, implantar cluster do Service Fabric tooany em qualquer lugar.
* Desenvolva aplicativos escalonáveis que são compostos de microservices usando modelos de programação de malha do serviço hello, contêineres ou qualquer código.
* Desenvolva microsserviços com e sem monitoração de estado altamente confiáveis. Simplificar o design de saudação do seu aplicativo usando microservices com monitoração de estado. 
* Use Olá novel Reliable Actors modelo toocreate nuvem objetos de programação com o estado e código independente.
* Implante e orquestre contêineres que incluam contêineres do Windows e contêineres do Linux. O Service Fabric é um orquestrador de contêiner com monitoração de estado e com reconhecimento de dados.
* Implante aplicativos em segundos, de alta densidade com centenas ou milhares de aplicativos ou contêineres por computador.
* Implante diferentes versões do mesmo aplicativo lado a lado e atualizar cada aplicativo independentemente de saudação.
* Gerencie o ciclo de vida de saudação de seus aplicativos sem qualquer tempo de inatividade, incluindo as atualizações mais recentes e incondicionais.
* Expansão ou escala em número de saudação de nós em um cluster. À medida que você dimensiona nós, seus aplicativos são dimensionados automaticamente.
* Monitorar e diagnosticar a integridade de saudação de seus aplicativos e definir políticas para execução automática reparos.
* Assista balanceador de recurso Olá orquestram redistribuição de saudação de aplicativos em cluster hello. Service Fabric recupera de falhas e otimiza Olá distribuição de carga com base nos recursos disponíveis.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Próximas etapas
* Para mais informações:
  * [Por que um microservices abordagem toobuilding aplicativos?](service-fabric-overview-microservices.md)
  * [Visão geral da terminologia](service-fabric-technical-overview.md)
* Configurando o [ambiente de desenvolvimento](service-fabric-get-started.md)  
* Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md)

[Image1]: media/service-fabric-overview/Service-Fabric-Overview.png
