---
title: "Próximas etapas da criação do projeto no Service Fabric | Microsoft Docs"
description: "Este artigo contém links para um conjunto de tarefas básicas de desenvolvimento para o Service Fabric"
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
ms.openlocfilehash: 74019850c507902d9ef7ec47a364fff234aaf32b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="ad1fa-103">O seu aplicativo do Service Fabric e as próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ad1fa-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="ad1fa-104">O seu aplicativo do Service Fabric do Azure foi criado.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="ad1fa-105">Este artigo descreve a composição do seu projeto e algumas das próximas etapas possíveis.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-105">This article describes the makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="ad1fa-106">Seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="ad1fa-106">Your application</span></span>
<span data-ttu-id="ad1fa-107">Cada novo aplicativo inclui um projeto de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-107">Every new application includes an application project.</span></span> <span data-ttu-id="ad1fa-108">Pode haver um ou dois projetos adicionais dependendo do tipo de serviço escolhido.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-108">There may be one or two additional projects, depending on the type of service chosen.</span></span>

### <a name="the-application-project"></a><span data-ttu-id="ad1fa-109">O projeto de aplicativo</span><span class="sxs-lookup"><span data-stu-id="ad1fa-109">The application project</span></span>
<span data-ttu-id="ad1fa-110">O projeto de aplicativo consiste em:</span><span class="sxs-lookup"><span data-stu-id="ad1fa-110">The application project consists of:</span></span>

* <span data-ttu-id="ad1fa-111">Um conjunto de referências para os serviços que compõem o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-111">A set of references to the services that make up your application.</span></span>
* <span data-ttu-id="ad1fa-112">Três perfis de publicação, (Local de 1 Nó, Local de 5 Nós e Nuvem) que você pode usar para atualizar as preferências para trabalhar com ambientes diferentes, como preferências relacionadas a um ponto de extremidade do cluster e se realizará ou não implantações de atualização por padrão.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use to maintain preferences for working with different environments--such as preferences related to a cluster endpoint and whether to perform upgrade deployments by default.</span></span>
* <span data-ttu-id="ad1fa-113">Três arquivos de parâmetro de aplicativos (os mesmos que acima) que você pode usar para atualizar as configurações do aplicativo específicas do ambiente, como o número de partições a criar para um serviço.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-113">Three application parameter files (same as above) that you can use to maintain environment-specific application configurations, such as the number of partitions to create for a service.</span></span>
* <span data-ttu-id="ad1fa-114">Um script de implantação que você pode usar para implantar o aplicativo na linha de comando ou como parte de uma pipeline de implantação e integração contínua automatizada.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-114">A deployment script that you can use to deploy your application from the command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="ad1fa-115">O manifesto do aplicativo, que o descreve.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-115">The application manifest, which describes the application.</span></span> <span data-ttu-id="ad1fa-116">Você pode encontrar o manifesto na pasta ApplicationPackageRoot.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-116">You can find the manifest under the ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="ad1fa-117">Serviço sem estado</span><span class="sxs-lookup"><span data-stu-id="ad1fa-117">Stateless service</span></span>
<span data-ttu-id="ad1fa-118">Ao adicionar um novo serviço sem estado, o Visual Studio adiciona à sua solução um projeto de serviço que inclua um tipo descendente de `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-118">When you add a new stateless service, Visual Studio adds a service project to your solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="ad1fa-119">O serviço incrementa uma variável local em um contador.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-119">The service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="ad1fa-120">Serviço com estado</span><span class="sxs-lookup"><span data-stu-id="ad1fa-120">Stateful service</span></span>
<span data-ttu-id="ad1fa-121">Ao adicionar um novo serviço com estado, o Visual Studio adiciona à sua solução um projeto de serviço que inclua um tipo descendente de `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-121">When you add a new stateful service, Visual Studio adds a service project to your solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="ad1fa-122">O serviço incrementa um contador em seu método `RunAsync` e armazena o resultado em um `ReliableDictionary`.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-122">The service increments a counter in its `RunAsync` method and stores the result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="ad1fa-123">Serviço de ator</span><span class="sxs-lookup"><span data-stu-id="ad1fa-123">Actor service</span></span>
<span data-ttu-id="ad1fa-124">Ao adicionar um novo reliable actor, o Visual Studio adiciona dois projetos à sua solução: um projeto de ator e um projeto de interface.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-124">When you add a new reliable actor, Visual Studio adds two projects to your solution: an actor project and an interface project.</span></span>

<span data-ttu-id="ad1fa-125">O projeto de ator fornece métodos para a configuração e a obtenção do valor de um contador mantido de forma confiável no estado do ator.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-125">The actor project provides methods for setting and getting the value of a counter that is reliably persisted within the actor's state.</span></span> <span data-ttu-id="ad1fa-126">O projeto de interface fornece uma interface que outros serviços podem usar para invocar o ator.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-126">The interface project provides an interface that other services can use to invoke the actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="ad1fa-127">API Web sem monitoração de estado</span><span class="sxs-lookup"><span data-stu-id="ad1fa-127">Stateless Web API</span></span>
<span data-ttu-id="ad1fa-128">O projeto de API da Web sem monitoração de estado fornece um serviço Web básico que você pode usar para abrir o aplicativo para clientes externos.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-128">The stateless Web API project provides a basic web service that you can use to open your application to external clients.</span></span> <span data-ttu-id="ad1fa-129">Para ter mais informações sobre como o projeto é estruturado, consulte [Serviços da API Web do Service Fabric com a auto-hospedagem OWIN](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="ad1fa-129">For more information about how the project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="ad1fa-130">Núcleo do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ad1fa-130">ASP.NET core</span></span>
<span data-ttu-id="ad1fa-131">O SDK do Service Fabric fornece o mesmo conjunto de modelos do ASP.NET Core que está disponível para projetos do ASP.NET Core autônomos: vazio, [API Web][aspnet-webapi] e [Aplicativo Web][aspnet-webapp].</span><span class="sxs-lookup"><span data-stu-id="ad1fa-131">The Service Fabric SDK provides the same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="ad1fa-132">Executáveis de convidado e contêineres de convidado</span><span class="sxs-lookup"><span data-stu-id="ad1fa-132">Guest executables and guest containers</span></span>

<span data-ttu-id="ad1fa-133">Um 'convidado' do Service Fabric é um serviço que não é compilado com os modelos de programação da plataforma.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-133">A Service Fabric 'guest' is a service that is not built with the platform's programming models.</span></span> <span data-ttu-id="ad1fa-134">Você pode empacotar os binários de um convidado [diretamente no pacote de aplicativos](service-fabric-deploy-existing-app.md) ou então [por meio de uma imagem de contêiner](service-fabric-deploy-container.md).</span><span class="sxs-lookup"><span data-stu-id="ad1fa-134">You can package the binaries for a guest either [directly in the application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="ad1fa-135">Em ambos os casos, o Visual Studio cria os artefatos necessários na pasta **ApplicationPackageRoot** do projeto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-135">In both cases, Visual Studio creates the necessary artifacts in the **ApplicationPackageRoot** folder of the application project.</span></span> <span data-ttu-id="ad1fa-136">O Visual Studio não criará um novo projeto de serviço porque o código já existe em outro lugar.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-136">Visual Studio will not create a new service project because the code already exists elsewhere.</span></span> <span data-ttu-id="ad1fa-137">Se você deseja gerenciar seus projetos de convidado junto com o projeto de aplicativo do Service Fabric, você pode adicioná-los à mesma solução do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-137">If you would like to manage your guest projects alongside the Service Fabric application project, you can add them to the same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad1fa-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ad1fa-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="ad1fa-139">Criar um cluster do Azure</span><span class="sxs-lookup"><span data-stu-id="ad1fa-139">Create an Azure cluster</span></span>
<span data-ttu-id="ad1fa-140">O SDK do Service Fabric fornece um cluster local para desenvolvimento e teste.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-140">The Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="ad1fa-141">Para criar um cluster no Azure, veja [Configurar um cluster do Service Fabric do Portal do Azure][create-cluster-in-portal].</span><span class="sxs-lookup"><span data-stu-id="ad1fa-141">To create a cluster in Azure, see [Setting up a Service Fabric cluster from the Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-to-azure"></a><span data-ttu-id="ad1fa-142">Publicar seu aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="ad1fa-142">Publish your application to Azure</span></span>
<span data-ttu-id="ad1fa-143">Você pode publicar o seu aplicativo diretamente do Visual Studio para um cluster do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-143">You can publish your application directly from Visual Studio to an Azure cluster.</span></span> <span data-ttu-id="ad1fa-144">Para saber como, consulte [Publicar seu aplicativo no Azure][publish-app-to-azure].</span><span class="sxs-lookup"><span data-stu-id="ad1fa-144">To learn how, see [Publishing your application to Azure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-to-visualize-your-cluster"></a><span data-ttu-id="ad1fa-145">Usar o Explorador do Service Fabric para visualizar o seu cluster</span><span class="sxs-lookup"><span data-stu-id="ad1fa-145">Use Service Fabric Explorer to visualize your cluster</span></span>
<span data-ttu-id="ad1fa-146">O Explorador do Service Fabric oferece uma maneira fácil de visualizar o seu cluster, incluindo aplicativos implantados e layout físico.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-146">Service Fabric Explorer offers an easy way to visualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="ad1fa-147">Para saber mais, veja [Visualizar o cluster com o Service Fabric Explorer][visualize-with-sfx].</span><span class="sxs-lookup"><span data-stu-id="ad1fa-147">To learn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="ad1fa-148">Versão e atualização de serviços</span><span class="sxs-lookup"><span data-stu-id="ad1fa-148">Version and upgrade your services</span></span>
<span data-ttu-id="ad1fa-149">O Service Fabric permite controle de versão independente e atualização de serviços independentes em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ad1fa-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="ad1fa-150">Para saber mais, consulte [Controlar a versão e atualizar seus serviços][app-upgrade-tutorial].</span><span class="sxs-lookup"><span data-stu-id="ad1fa-150">To learn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="ad1fa-151">Configurar a integração contínua com o Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="ad1fa-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="ad1fa-152">Para saber como configurar um processo de integração contínua para seu aplicativo do Service Fabric, confira [Configurar a integração contínua com o Visual Studio Team Services][ci-with-vso].</span><span class="sxs-lookup"><span data-stu-id="ad1fa-152">To learn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

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
