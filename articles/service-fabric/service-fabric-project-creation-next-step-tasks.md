---
title: "etapas de criação de projeto Avançar malha aaaService | Microsoft Docs"
description: "Este artigo contém o conjunto de tooa de links de tarefas básicas de desenvolvimento para a malha do serviço"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="ec7d7-103">O seu aplicativo do Service Fabric e as próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ec7d7-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="ec7d7-104">O seu aplicativo do Service Fabric do Azure foi criado.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="ec7d7-105">Este artigo descreve a composição de saudação do seu projeto e algumas das próximas etapas possíveis.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-105">This article describes hello makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="ec7d7-106">Seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="ec7d7-106">Your application</span></span>
<span data-ttu-id="ec7d7-107">Cada novo aplicativo inclui um projeto de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-107">Every new application includes an application project.</span></span> <span data-ttu-id="ec7d7-108">Pode haver um ou dois projetos adicionais, dependendo do tipo de saudação do serviço escolhido.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-108">There may be one or two additional projects, depending on hello type of service chosen.</span></span>

### <a name="hello-application-project"></a><span data-ttu-id="ec7d7-109">projeto de aplicativo Hello</span><span class="sxs-lookup"><span data-stu-id="ec7d7-109">hello application project</span></span>
<span data-ttu-id="ec7d7-110">projeto de aplicativo Hello consiste em:</span><span class="sxs-lookup"><span data-stu-id="ec7d7-110">hello application project consists of:</span></span>

* <span data-ttu-id="ec7d7-111">Um conjunto de serviços de toohello de referências que compõem seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-111">A set of references toohello services that make up your application.</span></span>
* <span data-ttu-id="ec7d7-112">Três publicar perfis (1-nó Local, 5-nó Local e nuvem) que você pode usar toomaintain preferências para trabalhar com diferentes ambientes – como ponto de extremidade de cluster de tooa relacionados preferências e se tooperform atualizar implantações por padrão.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use toomaintain preferences for working with different environments--such as preferences related tooa cluster endpoint and whether tooperform upgrade deployments by default.</span></span>
* <span data-ttu-id="ec7d7-113">Três arquivos de parâmetro aplicativo (o mesmo que acima) que você pode usar configurações de aplicativo específico do ambiente toomaintain, como o número de saudação de toocreate de partições para um serviço.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-113">Three application parameter files (same as above) that you can use toomaintain environment-specific application configurations, such as hello number of partitions toocreate for a service.</span></span>
* <span data-ttu-id="ec7d7-114">Um script de implantação que você pode usar toodeploy seu aplicativo de linha de comando hello ou como parte de um pipeline de implantação e a integração contínuo automatizado.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-114">A deployment script that you can use toodeploy your application from hello command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="ec7d7-115">manifesto de aplicativo Hello, que descreve o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-115">hello application manifest, which describes hello application.</span></span> <span data-ttu-id="ec7d7-116">Você pode encontrar hello manifesto na pasta de ApplicationPackageRoot hello.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-116">You can find hello manifest under hello ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="ec7d7-117">Serviço sem estado</span><span class="sxs-lookup"><span data-stu-id="ec7d7-117">Stateless service</span></span>
<span data-ttu-id="ec7d7-118">Quando você adiciona um novo serviço sem monitoração de estado, o Visual Studio adiciona uma solução de tooyour de projeto de serviço que inclui um tipo que descendem do `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-118">When you add a new stateless service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="ec7d7-119">serviço de saudação incrementa uma variável local em um contador.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-119">hello service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="ec7d7-120">Serviço com estado</span><span class="sxs-lookup"><span data-stu-id="ec7d7-120">Stateful service</span></span>
<span data-ttu-id="ec7d7-121">Quando você adiciona um novo serviço com monitoração de estado, o Visual Studio adiciona uma solução de tooyour de projeto de serviço que inclui um tipo que descendem do `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-121">When you add a new stateful service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="ec7d7-122">Olá, serviço incrementa um contador em seu `RunAsync` método e armazena o resultado da saudação em um `ReliableDictionary`.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-122">hello service increments a counter in its `RunAsync` method and stores hello result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="ec7d7-123">Serviço de ator</span><span class="sxs-lookup"><span data-stu-id="ec7d7-123">Actor service</span></span>
<span data-ttu-id="ec7d7-124">Quando você adiciona um novo ator confiável, o Visual Studio adiciona o Gerenciador de tooyour dois projetos: um projeto de ator e um projeto de interface.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-124">When you add a new reliable actor, Visual Studio adds two projects tooyour solution: an actor project and an interface project.</span></span>

<span data-ttu-id="ec7d7-125">projeto de ator Olá fornece métodos para a configuração e Obtendo o valor de saudação de um contador que é confiável persistente em estado de saudação do ator.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-125">hello actor project provides methods for setting and getting hello value of a counter that is reliably persisted within hello actor's state.</span></span> <span data-ttu-id="ec7d7-126">Olá interface projeto fornece uma interface que outros serviços podem usar o ator de saudação tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-126">hello interface project provides an interface that other services can use tooinvoke hello actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="ec7d7-127">API Web sem monitoração de estado</span><span class="sxs-lookup"><span data-stu-id="ec7d7-127">Stateless Web API</span></span>
<span data-ttu-id="ec7d7-128">projeto de API da Web sem monitoração de estado Olá fornece básico que você pode usar tooopen seus clientes de tooexternal do aplicativo de serviço web.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-128">hello stateless Web API project provides a basic web service that you can use tooopen your application tooexternal clients.</span></span> <span data-ttu-id="ec7d7-129">Para obter mais informações sobre como o projeto de saudação estruturado, consulte [serviços de API da Web do serviço do Fabric com OWIN auto-hospedagem](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="ec7d7-129">For more information about how hello project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="ec7d7-130">Núcleo do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ec7d7-130">ASP.NET core</span></span>
<span data-ttu-id="ec7d7-131">Olá SDK do Service Fabric fornece Olá mesmo conjunto de modelos do ASP.NET Core que estão disponíveis para projetos do ASP.NET Core de autônomo: vazio, [API da Web][aspnet-webapi], e [aplicativo Web][aspnet-webapp].</span><span class="sxs-lookup"><span data-stu-id="ec7d7-131">hello Service Fabric SDK provides hello same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="ec7d7-132">Executáveis de convidado e contêineres de convidado</span><span class="sxs-lookup"><span data-stu-id="ec7d7-132">Guest executables and guest containers</span></span>

<span data-ttu-id="ec7d7-133">Um serviço de malha 'Convidado' é um serviço que não é compilado com modelos de programação da plataforma hello.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-133">A Service Fabric 'guest' is a service that is not built with hello platform's programming models.</span></span> <span data-ttu-id="ec7d7-134">Você pode empacotar binários Olá para o convidado ou [diretamente no pacote de aplicativo hello](service-fabric-deploy-existing-app.md) ou [por meio de uma imagem de contêiner](service-fabric-deploy-container.md).</span><span class="sxs-lookup"><span data-stu-id="ec7d7-134">You can package hello binaries for a guest either [directly in hello application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="ec7d7-135">Em ambos os casos, o Visual Studio cria Olá artefatos necessários no hello **ApplicationPackageRoot** pasta do projeto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-135">In both cases, Visual Studio creates hello necessary artifacts in hello **ApplicationPackageRoot** folder of hello application project.</span></span> <span data-ttu-id="ec7d7-136">Visual Studio não irá criar um novo projeto de serviço porque o código Olá já existe em outro lugar.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-136">Visual Studio will not create a new service project because hello code already exists elsewhere.</span></span> <span data-ttu-id="ec7d7-137">Se você quiser toomanage seu convidado projetos junto com o projeto de aplicativo do Service Fabric hello, você pode adicioná-los toohello mesma solução do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-137">If you would like toomanage your guest projects alongside hello Service Fabric application project, you can add them toohello same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec7d7-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ec7d7-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="ec7d7-139">Criar um cluster do Azure</span><span class="sxs-lookup"><span data-stu-id="ec7d7-139">Create an Azure cluster</span></span>
<span data-ttu-id="ec7d7-140">Olá SDK do Service Fabric fornece um cluster local para desenvolvimento e teste.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-140">hello Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="ec7d7-141">toocreate um cluster no Azure, consulte [Configurando um cluster do Service Fabric do portal do Azure de saudação][create-cluster-in-portal].</span><span class="sxs-lookup"><span data-stu-id="ec7d7-141">toocreate a cluster in Azure, see [Setting up a Service Fabric cluster from hello Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-tooazure"></a><span data-ttu-id="ec7d7-142">Publicar seu aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="ec7d7-142">Publish your application tooAzure</span></span>
<span data-ttu-id="ec7d7-143">Você pode publicar seu aplicativo diretamente do Visual Studio tooan cluster do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-143">You can publish your application directly from Visual Studio tooan Azure cluster.</span></span> <span data-ttu-id="ec7d7-144">como fazer isso, consulte toolearn [publicar seu aplicativo tooAzure][publish-app-to-azure].</span><span class="sxs-lookup"><span data-stu-id="ec7d7-144">toolearn how, see [Publishing your application tooAzure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a><span data-ttu-id="ec7d7-145">Usar o Gerenciador do Service Fabric toovisualize seu cluster</span><span class="sxs-lookup"><span data-stu-id="ec7d7-145">Use Service Fabric Explorer toovisualize your cluster</span></span>
<span data-ttu-id="ec7d7-146">Service Fabric Explorer oferece uma maneira fácil toovisualize seu cluster, incluindo aplicativos implantados e layout físico.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-146">Service Fabric Explorer offers an easy way toovisualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="ec7d7-147">mais, consulte toolearn [visualizando o cluster usando o Gerenciador do Service Fabric][visualize-with-sfx].</span><span class="sxs-lookup"><span data-stu-id="ec7d7-147">toolearn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="ec7d7-148">Versão e atualização de serviços</span><span class="sxs-lookup"><span data-stu-id="ec7d7-148">Version and upgrade your services</span></span>
<span data-ttu-id="ec7d7-149">O Service Fabric permite controle de versão independente e atualização de serviços independentes em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ec7d7-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="ec7d7-150">mais, consulte toolearn [controle de versão e atualizar seus serviços][app-upgrade-tutorial].</span><span class="sxs-lookup"><span data-stu-id="ec7d7-150">toolearn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="ec7d7-151">Configurar a integração contínua com o Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="ec7d7-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="ec7d7-152">toolearn como você pode configurar um processo de integração contínua para seu aplicativo de malha do serviço, consulte [configurar a integração contínua com o Visual Studio Team Services][ci-with-vso].</span><span class="sxs-lookup"><span data-stu-id="ec7d7-152">toolearn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
