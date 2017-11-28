---
title: Azure Service Fabric no Linux | Microsoft Docs
description: "Os clusters do Service Fabric dão suporte para o Linux e para o Java, o que significa que você poderá implantar e hospedar aplicativos do Service Fabric escritos em Java e em C# no Linux."
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
ms.openlocfilehash: dddc9f698d9776999d406117b46285a0f90d9620
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="service-fabric-on-linux"></a><span data-ttu-id="bbcb0-103">Service Fabric no Linux</span><span class="sxs-lookup"><span data-stu-id="bbcb0-103">Service Fabric on Linux</span></span>
<span data-ttu-id="bbcb0-104">A visualização do Service Fabric no Linux permite criar, implantar e gerenciar aplicativos altamente disponíveis e altamente escalonáveis no Linux, assim como você faria no Windows.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-104">The preview of Service Fabric on Linux enables you to build, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="bbcb0-105">As estruturas do Service Fabric (Reliable Services e Reliable Actors) estão disponíveis em Java no Linux, além de em C# (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="bbcb0-105">The Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition to C# (.NET Core).</span></span>  <span data-ttu-id="bbcb0-106">Você também pode compilar os [serviços executáveis convidados](service-fabric-deploy-existing-app.md) com qualquer linguagem ou estrutura.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="bbcb0-107">Além disso, a preview também dá suporte à orquestração de contêineres de Docker.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-107">In addition, the preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="bbcb0-108">Os contêineres de Docker podem executar arquivos executáveis de convidado ou serviços nativos do Service Fabric, que usam as estruturas do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-108">Docker containers can run guest executables or native Service Fabric services, which use the Service Fabric frameworks.</span></span>

<span data-ttu-id="bbcb0-109">O Service Fabric no Linux é conceitualmente equivalente ao Service Fabric no Windows (exceto pelas especificações de sistema operacional e pelo suporte à linguagem de programação).</span><span class="sxs-lookup"><span data-stu-id="bbcb0-109">Service Fabric on Linux is conceptually equivalent to Service Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="bbcb0-110">Portanto, a maior parte da nossa [documentação existente](http://aka.ms/servicefabricdocs) destina-se a ajudar você a se familiarizar com a tecnologia.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with the technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="bbcb0-111">Sistemas operacionais e linguagens de programação com suporte</span><span class="sxs-lookup"><span data-stu-id="bbcb0-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="bbcb0-112">A visualização limitada oferece suporte à criação de clusters de desenvolvimento de uma caixa, além de clusters de vários computadores no Azure executando o Ubuntu Server 16.04.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-112">The limited preview supports the creation of one-box development clusters in addition to multi-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="bbcb0-113">A preview dá suporte para Reliable Actors e para as estruturas de serviços sem monitoração de estado confiáveis em Java e em C#, além dos executáveis de convidado e da orquestração de contêineres de Docker.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-113">The preview supports the Reliable Actors and the Reliable Stateless Services frameworks in Java and C# in addition to guest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="bbcb0-114">O Linux ainda não dá suporte às Reliable Collections.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="bbcb0-115">Também não há suporte para clusters autônomos – somente os clusters de uma caixa e de vários computadores Linux do Azure têm suporte na preview.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in the preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="bbcb0-116">Ferramentas com suporte</span><span class="sxs-lookup"><span data-stu-id="bbcb0-116">Supported tooling</span></span>
<span data-ttu-id="bbcb0-117">A versão prévia dá suporte à interação com o cluster por meio da CLI do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-117">The preview supports interaction with the cluster through Service Fabric CLI.</span></span> <span data-ttu-id="bbcb0-118">Para desenvolvedores Java, a integração com o Eclipse e o Yeoman é fornecida com o Eclipse com suporte no Linux e no OSX.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="bbcb0-119">A integração OSX usa uma VM do Linux nos bastidores por meio do Vagrant.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-119">The OSX integration uses a Linux VM under the hood via vagrant.</span></span> <span data-ttu-id="bbcb0-120">Para desenvolvedores C#, a integração com o Yeoman é fornecida para gerar modelos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-120">For C# developers, integration with Yeoman is provided to generate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbcb0-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bbcb0-121">Next steps</span></span>

* <span data-ttu-id="bbcb0-122">Familiarize-se com as estruturas de programação [Reliable Actors](service-fabric-reliable-actors-introduction.md) e [Reliable Services](service-fabric-reliable-services-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="bbcb0-122">Get familiar with the [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="bbcb0-123">Preparar seu ambiente de desenvolvimento no Linux</span><span class="sxs-lookup"><span data-stu-id="bbcb0-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="bbcb0-124">Preparar seu ambiente de desenvolvimento no OSX</span><span class="sxs-lookup"><span data-stu-id="bbcb0-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="bbcb0-125">Criar seu primeiro aplicativo do Java do Service Fabric no Linux</span><span class="sxs-lookup"><span data-stu-id="bbcb0-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="bbcb0-126">Configurar a implantação e integração contínua do Service Fabric com Jenkins e GitHub</span><span class="sxs-lookup"><span data-stu-id="bbcb0-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span></span>](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [<span data-ttu-id="bbcb0-127">Diferenças Windows/Linux do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bbcb0-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
