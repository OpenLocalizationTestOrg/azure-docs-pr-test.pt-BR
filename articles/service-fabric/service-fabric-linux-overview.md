---
title: aaaAzure Service Fabric no Linux | Microsoft Docs
description: "Suportam a clusters Service Fabric Linux e Java, o que significa que você será capaz de toodeploy e hospedar aplicativos do Service Fabric escritos em Java e c# em Linux."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: ca0e092b00faec560963c0d6cc379593d085f6a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-on-linux"></a>Service Fabric no Linux
visualização de saudação do Service Fabric no Linux permite toobuild, implantar e gerenciar aplicativos altamente escalonáveis, altamente disponíveis no Linux, exatamente como você faria no Windows. estruturas de malha do serviço de saudação (serviços confiáveis e atores confiável) estão disponíveis em Java no Linux em adição tooC # (.NET Core).  Você também pode compilar os [serviços executáveis convidados](service-fabric-deploy-existing-app.md) com qualquer linguagem ou estrutura. Além disso, visualização de saudação também oferece suporte a orquestração contêineres do Docker. Contêineres do docker podem executar arquivos executáveis de convidado ou nativo serviços do Service Fabric, que usa estruturas de malha do serviço de saudação.

O Service Fabric no Linux é conceitualmente equivalente tooService malha no Windows (exceto para as especificações de sistema operacional e suporte de linguagem de programação). Portanto, a maioria dos nossos [documentação existente](http://aka.ms/servicefabricdocs) aplica-se em ajudando você se familiarizará com a tecnologia de saudação.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a>Sistemas operacionais e linguagens de programação com suporte
Olá limitado visualização dá suporte a saudação criação de desenvolvimento de uma caixa de clusters Além disso toomulti máquina clusters no Azure em execução 16.04 de servidor do Ubuntu. dá suporte à visualização de Olá Olá Reliable Actors e Olá estruturas de serviços sem estado confiável em Java e c# em adição tooguest executáveis e orquestrar a contêineres do Docker.  

> [!NOTE]
> O Linux ainda não dá suporte às Reliable Collections. Não há suporte para clusters somente de suporte-apenas uma caixa e clusters de vários computadores Linux do Azure são compatíveis com visualização hello.
>
>


## <a name="supported-tooling"></a>Ferramentas com suporte
visualização de saudação dá suporte à interação com o cluster Olá por meio da CLI de malha do serviço. Para desenvolvedores Java, a integração com o Eclipse e o Yeoman é fornecida com o Eclipse com suporte no Linux e no OSX. Olá integração OSX usa uma VM do Linux subjacente Olá via vagrant. Para desenvolvedores do c#, integração com Yeoman é fornecida toogenerate modelos de aplicativos.

## <a name="next-steps"></a>Próximas etapas

* Familiarize-se com hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) e [serviços confiáveis](service-fabric-reliable-services-introduction.md) estruturas de programação
* [Preparar seu ambiente de desenvolvimento no Linux](service-fabric-get-started-linux.md)
* [Preparar seu ambiente de desenvolvimento no OSX](service-fabric-get-started-mac.md)
* [Criar seu primeiro aplicativo do Java do Service Fabric no Linux](service-fabric-create-your-first-linux-application-with-java.md)
* [Configurar a implantação e integração contínua do Service Fabric com Jenkins e GitHub](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [Diferenças Windows/Linux do Service Fabric](service-fabric-linux-windows-differences.md)
