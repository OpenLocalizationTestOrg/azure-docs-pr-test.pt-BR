---
title: "aaaService malha programação visão geral do modelo | Microsoft Docs"
description: "Service Fabric oferece duas estruturas para a criação de serviços: Olá a estrutura de serviços de saudação e da estrutura de ator. Elas oferecem vantagens e desvantagens distintas com relação à simplicidade e ao controle."
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: vturecek
ms.assetid: 974b2614-014e-4587-a947-28fcef28b382
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: vturecek
ms.openlocfilehash: b48af2a7b41935bdf0e4594c765f363e520c254e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-programming-model-overview"></a>Visão geral do modelo de programação do Service Fabric
Service Fabric oferece toowrite de várias maneiras e gerenciar seus serviços. Serviços podem escolher toouse Olá APIs de malha do serviço tootake aproveitar os recursos e estruturas de aplicativo da plataforma hello. Os serviços também podem ser um programa executável compilado, escrito em qualquer linguagem ou código executado em um contêiner simplesmente hospedado em um cluster do Service Fabric.

## <a name="guest-executables"></a>Executáveis de convidado
Um [executável do convidado](service-fabric-deploy-existing-app.md) é um executável arbitrário existente (escrito em qualquer linguagem) que pode ser executado como um serviço em seu aplicativo. Executáveis de convidado não chame diretamente Olá APIs do SDK do serviço de malha. No entanto, ainda se beneficiam de plataforma de saudação de recursos oferece, como descoberta de serviço, integridade personalizado e carregar relatórios chamando APIs REST expostos pelo serviço de malha. Eles também têm suporte completo do ciclo de vida do aplicativo.

Comece a usar executáveis convidados implantando seu primeiro [aplicativo executável convidado](service-fabric-deploy-existing-app.md).

## <a name="containers"></a>Contêineres
Por padrão, o Service Fabric implanta e ativa esses serviços como processos. O Service Fabric também pode implantar serviços em [contêineres](service-fabric-containers-overview.md). O Service Fabric dá suporte à implantação de contêineres do Linux e do Windows no Windows Server 2016. Imagens de contêiner podem ser extraídas de qualquer repositório de contêiner e implantado toohello máquina. Você pode implantar os aplicativos existentes como convidado exectuables, com ou sem estado confiável serviços do Service Fabric ou Reliable Actors em contêineres e você podem combinar serviços em processos e serviços em contêineres Olá mesmo aplicativo.

[Saiba mais sobre colocação de seus serviços em contêineres no Windows ou Linux](service-fabric-deploy-container.md)

## <a name="reliable-services"></a>Reliable Services
Serviços confiáveis é uma estrutura de leve para escrever serviços que integram a plataforma do Service Fabric hello e aproveitar o conjunto completo de saudação de recursos de plataforma. Serviços confiáveis fornecem um conjunto mínimo de APIs que permitem Olá Service Fabric runtime toomanage Olá do ciclo de vida dos serviços de e que permitem que seu toointeract serviços com tempo de execução de saudação. estrutura de aplicativo Hello é mínima, dando a você total controle sobre as opções de design e implementação e pode ser usado toohost qualquer outra estrutura de aplicativo, como o ASP.NET Core.

Serviços confiáveis podem ser plataformas de serviço toomost sem monitoração de estado, de forma semelhante, como servidores web, em que cada instância do serviço de saudação é criada da mesma e estado é mantido em uma solução externa, como o armazenamento de tabela do Azure ou banco de dados do Azure.

Serviços confiáveis também podem ser tooService com monitoração de estado, exclusiva malha, onde o estado é mantido diretamente no serviço de saudação usando coleções confiável. O estado fica altamente disponível por meio de replicação e é distribuído por meio de particionamento, tudo gerenciado automaticamente pelo Service Fabric.

[Saiba mais sobre os Reliable Services](service-fabric-reliable-services-introduction.md) ou comece [escrevendo o seu primeiro Reliable Service](service-fabric-reliable-services-quick-start.md).

## <a name="reliable-actors"></a>Reliable Actors
Estrutura de Reliable Actor Olá criado com base em serviços confiáveis, é uma estrutura de aplicativo que implementa o padrão de ator Virtual hello, com base no padrão de design de ator hello. estrutura de Reliable Actor de saudação usa unidades independentes de computação e de estado com a execução de thread único chamada atores. estrutura de Reliable Actor Olá fornece comunicação interna para atores e configurações de expansão e de persistência de estado previamente configurado.

Como atores confiável em si é uma estrutura de aplicativo criada no serviços confiáveis, ele é totalmente integrado com a plataforma do Service Fabric hello e os benefícios de todo o conjunto de recursos oferecidos pela plataforma de saudação Olá.

[Saiba mais sobre os Reliable Actors](service-fabric-reliable-actors-introduction.md) ou comece escrevendo [o seu primeiro serviço do Reliable Actor](service-fabric-reliable-actors-get-started.md)

## <a name="aspnet-core"></a>ASP.NET Core
O Service Fabric integra-se com [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) para a criação de serviços Web e API que podem ser incluídos como parte do seu aplicativo. 

[Criar um serviço de front-end usando o ASP.NET Core](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a>Próximas etapas
[Visão geral do Service Fabric e contêineres](service-fabric-containers-overview.md)

[Visão geral dos Reliable Services](service-fabric-reliable-services-introduction.md)

[Visão geral dos Reliable Services](service-fabric-reliable-actors-introduction.md)

[Service Fabric e ASP.NET Core ](service-fabric-reliable-services-communication-aspnetcore.md)




