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
# <a name="service-fabric-on-linux"></a><span data-ttu-id="8e157-103">Service Fabric no Linux</span><span class="sxs-lookup"><span data-stu-id="8e157-103">Service Fabric on Linux</span></span>
<span data-ttu-id="8e157-104">visualização de saudação do Service Fabric no Linux permite toobuild, implantar e gerenciar aplicativos altamente escalonáveis, altamente disponíveis no Linux, exatamente como você faria no Windows.</span><span class="sxs-lookup"><span data-stu-id="8e157-104">hello preview of Service Fabric on Linux enables you toobuild, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="8e157-105">estruturas de malha do serviço de saudação (serviços confiáveis e atores confiável) estão disponíveis em Java no Linux em adição tooC # (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="8e157-105">hello Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition tooC# (.NET Core).</span></span>  <span data-ttu-id="8e157-106">Você também pode compilar os [serviços executáveis convidados](service-fabric-deploy-existing-app.md) com qualquer linguagem ou estrutura.</span><span class="sxs-lookup"><span data-stu-id="8e157-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="8e157-107">Além disso, visualização de saudação também oferece suporte a orquestração contêineres do Docker.</span><span class="sxs-lookup"><span data-stu-id="8e157-107">In addition, hello preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="8e157-108">Contêineres do docker podem executar arquivos executáveis de convidado ou nativo serviços do Service Fabric, que usa estruturas de malha do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e157-108">Docker containers can run guest executables or native Service Fabric services, which use hello Service Fabric frameworks.</span></span>

<span data-ttu-id="8e157-109">O Service Fabric no Linux é conceitualmente equivalente tooService malha no Windows (exceto para as especificações de sistema operacional e suporte de linguagem de programação).</span><span class="sxs-lookup"><span data-stu-id="8e157-109">Service Fabric on Linux is conceptually equivalent tooService Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="8e157-110">Portanto, a maioria dos nossos [documentação existente](http://aka.ms/servicefabricdocs) aplica-se em ajudando você se familiarizará com a tecnologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e157-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with hello technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="8e157-111">Sistemas operacionais e linguagens de programação com suporte</span><span class="sxs-lookup"><span data-stu-id="8e157-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="8e157-112">Olá limitado visualização dá suporte a saudação criação de desenvolvimento de uma caixa de clusters Além disso toomulti máquina clusters no Azure em execução 16.04 de servidor do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="8e157-112">hello limited preview supports hello creation of one-box development clusters in addition toomulti-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="8e157-113">dá suporte à visualização de Olá Olá Reliable Actors e Olá estruturas de serviços sem estado confiável em Java e c# em adição tooguest executáveis e orquestrar a contêineres do Docker.</span><span class="sxs-lookup"><span data-stu-id="8e157-113">hello preview supports hello Reliable Actors and hello Reliable Stateless Services frameworks in Java and C# in addition tooguest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="8e157-114">O Linux ainda não dá suporte às Reliable Collections.</span><span class="sxs-lookup"><span data-stu-id="8e157-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="8e157-115">Não há suporte para clusters somente de suporte-apenas uma caixa e clusters de vários computadores Linux do Azure são compatíveis com visualização hello.</span><span class="sxs-lookup"><span data-stu-id="8e157-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in hello preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="8e157-116">Ferramentas com suporte</span><span class="sxs-lookup"><span data-stu-id="8e157-116">Supported tooling</span></span>
<span data-ttu-id="8e157-117">visualização de saudação dá suporte à interação com o cluster Olá por meio da CLI de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="8e157-117">hello preview supports interaction with hello cluster through Service Fabric CLI.</span></span> <span data-ttu-id="8e157-118">Para desenvolvedores Java, a integração com o Eclipse e o Yeoman é fornecida com o Eclipse com suporte no Linux e no OSX.</span><span class="sxs-lookup"><span data-stu-id="8e157-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="8e157-119">Olá integração OSX usa uma VM do Linux subjacente Olá via vagrant.</span><span class="sxs-lookup"><span data-stu-id="8e157-119">hello OSX integration uses a Linux VM under hello hood via vagrant.</span></span> <span data-ttu-id="8e157-120">Para desenvolvedores do c#, integração com Yeoman é fornecida toogenerate modelos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8e157-120">For C# developers, integration with Yeoman is provided toogenerate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e157-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8e157-121">Next steps</span></span>

* <span data-ttu-id="8e157-122">Familiarize-se com hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) e [serviços confiáveis](service-fabric-reliable-services-introduction.md) estruturas de programação</span><span class="sxs-lookup"><span data-stu-id="8e157-122">Get familiar with hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="8e157-123">Preparar seu ambiente de desenvolvimento no Linux</span><span class="sxs-lookup"><span data-stu-id="8e157-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="8e157-124">Preparar seu ambiente de desenvolvimento no OSX</span><span class="sxs-lookup"><span data-stu-id="8e157-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="8e157-125">Criar seu primeiro aplicativo do Java do Service Fabric no Linux</span><span class="sxs-lookup"><span data-stu-id="8e157-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="8e157-126">Configurar a implantação e integração contínua do Service Fabric com Jenkins e GitHub</span><span class="sxs-lookup"><span data-stu-id="8e157-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span></span>](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [<span data-ttu-id="8e157-127">Diferenças Windows/Linux do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8e157-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
