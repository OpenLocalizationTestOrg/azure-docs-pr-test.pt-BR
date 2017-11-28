---
title: "aaaCI/CD com o mecanismo do serviço de contêiner do Azure e o modo Swarm | Microsoft Docs"
description: "Usar o mecanismo do serviço de contêiner do Azure com o Docker Swarm modo, um registro de contêiner do Azure e o Visual Studio Team Services toodeliver continuamente um aplicativo do .NET Core multi-contêiner"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: "Docker, Contêineres, Microsserviços, Swarm, Azure, Visual Studio Team Services, DevOps, Mecanismo do ACS"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a><span data-ttu-id="27e85-104">CI/CD completo pipeline toodeploy um aplicativo de multi-contêiner no serviço de contêiner do Azure com o mecanismo do ACS e o modo de Swarm de Docker usando o Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="27e85-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Visual Studio Team Services</span></span>

<span data-ttu-id="27e85-105">*Este artigo se baseia em [CI/CD completo pipeline toodeploy um aplicativo de multi-contêiner no serviço de contêiner do Azure com o Docker Swarm usando o Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentação*</span><span class="sxs-lookup"><span data-stu-id="27e85-105">*This article is based on [Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*</span></span>

<span data-ttu-id="27e85-106">Hoje em dia, um dos Olá maiores desafios ao desenvolvimento de aplicativos modernos para nuvem hello está sendo toodeliver capaz desses aplicativos continuamente.</span><span class="sxs-lookup"><span data-stu-id="27e85-106">Nowadays, One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="27e85-107">Neste artigo, você aprenderá como tooimplement uma integração completa contínua e implantação (CI/CD) pipeline usando:</span><span class="sxs-lookup"><span data-stu-id="27e85-107">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using:</span></span> 
* <span data-ttu-id="27e85-108">Mecanismo do Serviço de Contêiner do Azure com o modo Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="27e85-108">Azure Container Service Engine with Docker Swarm Mode</span></span>
* <span data-ttu-id="27e85-109">Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="27e85-109">Azure Container Registry</span></span>
* <span data-ttu-id="27e85-110">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="27e85-110">Visual Studio Team Services</span></span>

<span data-ttu-id="27e85-111">Este artigo se baseia em um aplicativo simples, disponível no [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), desenvolvido com o ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="27e85-111">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span></span> <span data-ttu-id="27e85-112">aplicativo Hello é composto de quatro diferentes serviços: três web APIs e um web front-end:</span><span class="sxs-lookup"><span data-stu-id="27e85-112">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![Aplicativo de exemplo MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

<span data-ttu-id="27e85-114">o objetivo de saudação é toodeliver este aplicativo continuamente em um cluster de Docker Swarm modo, usando o Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="27e85-114">hello objective is toodeliver this application continuously in a Docker Swarm Mode cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="27e85-115">a figura de saudação a seguir detalhes esse pipeline entrega contínua:</span><span class="sxs-lookup"><span data-stu-id="27e85-115">hello following figure details this continuous delivery pipeline:</span></span>

![Aplicativo de exemplo MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

<span data-ttu-id="27e85-117">Aqui está uma breve explicação das etapas de saudação:</span><span class="sxs-lookup"><span data-stu-id="27e85-117">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="27e85-118">Alterações de código são o repositório de código fonte toohello confirmada (aqui, GitHub)</span><span class="sxs-lookup"><span data-stu-id="27e85-118">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="27e85-119">O GitHub dispara uma compilação no Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="27e85-119">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="27e85-120">Visual Studio Team Services obtém a versão mais recente de saudação do fontes hello e cria todas as imagens de saudação que compõem o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="27e85-120">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="27e85-121">Visual Studio Team Services envia cada registro da imagem tooa Docker criado usando o serviço de registro de contêiner do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="27e85-121">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="27e85-122">O Visual Studio Team Services dispara uma nova versão</span><span class="sxs-lookup"><span data-stu-id="27e85-122">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="27e85-123">versão Olá executa alguns comandos usando o SSH no nó do contêiner do Azure serviço cluster mestre Olá</span><span class="sxs-lookup"><span data-stu-id="27e85-123">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="27e85-124">Modo de docker Swarm no cluster Olá extrai versão mais recente de saudação de imagens de saudação</span><span class="sxs-lookup"><span data-stu-id="27e85-124">Docker Swarm Mode on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="27e85-125">Olá nova versão do aplicativo hello é implantada usando a pilha de Docker</span><span class="sxs-lookup"><span data-stu-id="27e85-125">hello new version of hello application is deployed using Docker Stack</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="27e85-126">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="27e85-126">Prerequisites</span></span>

<span data-ttu-id="27e85-127">Antes de iniciar este tutorial, você precisa toocomplete Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27e85-127">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="27e85-128">Criar um cluster no modo Swarm no Serviço de Contêiner do Azure com o Mecanismo do ACS</span><span class="sxs-lookup"><span data-stu-id="27e85-128">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [<span data-ttu-id="27e85-129">Conecte-se com o cluster de por nuvem Olá no serviço de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="27e85-129">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="27e85-130">Criar um registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="27e85-130">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="27e85-131">Ter uma conta do Visual Studio Team Services e projeto de equipe criados</span><span class="sxs-lookup"><span data-stu-id="27e85-131">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="27e85-132">Bifurcação Olá GitHub repositório tooyour conta do GitHub</span><span class="sxs-lookup"><span data-stu-id="27e85-132">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> <span data-ttu-id="27e85-133">o orchestrator Docker Swarm Olá no serviço de contêiner do Azure usa autônomo herdado por nuvem.</span><span class="sxs-lookup"><span data-stu-id="27e85-133">hello Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span></span> <span data-ttu-id="27e85-134">Atualmente, a saudação integrado [por nuvem modo](https://docs.docker.com/engine/swarm/) (no Docker 1.12 e superior) não é um orquestrador com suporte no serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="27e85-134">Currently, hello integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span></span> <span data-ttu-id="27e85-135">Por esse motivo, estamos usando [ACS mecanismo](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), um contribuído pela comunidade [quickstart modelo](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), ou uma solução de Docker em Olá [Azure Marketplace](https://azuremarketplace.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="27e85-135">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in hello [Azure Marketplace](https://azuremarketplace.microsoft.com).</span></span>
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="27e85-136">Etapa 1: Configurar sua conta do Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="27e85-136">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="27e85-137">Nesta seção, você configura sua conta do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="27e85-137">In this section, you configure your Visual Studio Team Services account.</span></span> <span data-ttu-id="27e85-138">tooconfigure VSTS serviços pontos de extremidade, no seu projeto do Visual Studio Team Services, clique em Olá **configurações** ícone na barra de ferramentas hello e selecione **serviços**.</span><span class="sxs-lookup"><span data-stu-id="27e85-138">tooconfigure VSTS Services Endpoints, in your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

![Abra o Ponto de extremidade de serviço](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a><span data-ttu-id="27e85-140">Conectar o Visual Studio Team Services e a conta o Azure</span><span class="sxs-lookup"><span data-stu-id="27e85-140">Connect Visual Studio Team Services and Azure account</span></span>

<span data-ttu-id="27e85-141">Configure uma conexão entre seu projeto do VSTS e sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="27e85-141">Set up a connection between your VSTS project and your Azure account.</span></span>

1. <span data-ttu-id="27e85-142">Olá esquerda, clique em **novo ponto de extremidade de serviço** > **do Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="27e85-142">On hello left, click **New Service Endpoint** > **Azure Resource Manager**.</span></span>
2. <span data-ttu-id="27e85-143">tooauthorize VSTS toowork com sua conta do Azure, selecione seu **assinatura** e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="27e85-143">tooauthorize VSTS toowork with your Azure account, select your **Subscription** and click **OK**.</span></span>

    ![Visual Studio Team Services – Autorizar Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="27e85-145">Conectar o Visual Studio Team Services e o GitHub</span><span class="sxs-lookup"><span data-stu-id="27e85-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="27e85-146">Configure uma conexão entre seu projeto VSTS e sua conta GitHub.</span><span class="sxs-lookup"><span data-stu-id="27e85-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="27e85-147">Olá esquerda, clique em **novo ponto de extremidade de serviço** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="27e85-147">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>
2. <span data-ttu-id="27e85-148">tooauthorize VSTS toowork com sua conta do GitHub, clique em **autorizar** e siga o procedimento Olá na janela de saudação que é aberta.</span><span class="sxs-lookup"><span data-stu-id="27e85-148">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services - Autorizar GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a><span data-ttu-id="27e85-150">Conecte-se o cluster do VSTS tooyour serviço de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="27e85-150">Connect VSTS tooyour Azure Container Service cluster</span></span>

<span data-ttu-id="27e85-151">últimas etapas Olá antes de entrar no pipeline de CI/CD Olá são tooconfigure conexões externas tooyour Docker Swarm cluster do Azure.</span><span class="sxs-lookup"><span data-stu-id="27e85-151">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="27e85-152">Para o cluster Docker Swarm hello, adicione um ponto de extremidade do tipo **SSH**.</span><span class="sxs-lookup"><span data-stu-id="27e85-152">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="27e85-153">Em seguida, insira informações de conexão SSH saudação do cluster por nuvem (nó mestre).</span><span class="sxs-lookup"><span data-stu-id="27e85-153">Then enter hello SSH connection information of your Swarm cluster (master node).</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

<span data-ttu-id="27e85-155">Todas as configurações de saudação é feito agora.</span><span class="sxs-lookup"><span data-stu-id="27e85-155">All hello configuration is done now.</span></span> <span data-ttu-id="27e85-156">Próximas etapas de Olá, você criará um pipeline de CI/CD Olá que compila e implanta Olá aplicativo toohello Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="27e85-156">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="27e85-157">Etapa 2: Criar a definição de compilação Olá</span><span class="sxs-lookup"><span data-stu-id="27e85-157">Step 2: Create hello build definition</span></span>

<span data-ttu-id="27e85-158">Nesta etapa, você pode configurar uma definição de compilação para o seu projeto do VSTS e define o fluxo de trabalho de compilação de saudação para as imagens de contêiner</span><span class="sxs-lookup"><span data-stu-id="27e85-158">In this step, you set up a build definition for your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="27e85-159">Configuração da definição inicial</span><span class="sxs-lookup"><span data-stu-id="27e85-159">Initial definition setup</span></span>

1. <span data-ttu-id="27e85-160">toocreate uma definição de compilação, conecte-se tooyour do Visual Studio Team Services do projeto e clique em **Build e versão**.</span><span class="sxs-lookup"><span data-stu-id="27e85-160">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> <span data-ttu-id="27e85-161">Em Olá **definições de compilação** seção, clique em **+ novo**.</span><span class="sxs-lookup"><span data-stu-id="27e85-161">In hello **Build definitions** section, click **+ New**.</span></span> 

    ![Visual Studio Team Services - Nova Definição da Compilação](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. <span data-ttu-id="27e85-163">Selecione Olá **vazio processo**.</span><span class="sxs-lookup"><span data-stu-id="27e85-163">Select hello **Empty process**.</span></span>

    ![Visual Studio Team Services – Nova Definição de Compilação Vazia](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. <span data-ttu-id="27e85-165">Em seguida, clique em Olá **variáveis** guia e crie duas novas variáveis: **RegistryURL** e **AgentURL**.</span><span class="sxs-lookup"><span data-stu-id="27e85-165">Then, click hello **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span></span> <span data-ttu-id="27e85-166">Colar valores de saudação do registro e DNS de agentes do Cluster.</span><span class="sxs-lookup"><span data-stu-id="27e85-166">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services – Configuração de Variáveis de Compilação](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. <span data-ttu-id="27e85-168">Em Olá **definições de compilação** page, abra Olá **gatilhos** guia e configurar a integração contínua da saudação compilação toouse com bifurcação de saudação do projeto de MyShop Olá que você criou nos pré-requisitos Olá.</span><span class="sxs-lookup"><span data-stu-id="27e85-168">On hello **Build Definitions** page, open hello **Triggers** tab and configure hello build toouse continuous integration with hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="27e85-169">Em seguida, selecione **Alterações em lote**.</span><span class="sxs-lookup"><span data-stu-id="27e85-169">Then, select **Batch changes**.</span></span> <span data-ttu-id="27e85-170">Certifique-se de que você selecione *docker linux* como Olá **Branch especificação**.</span><span class="sxs-lookup"><span data-stu-id="27e85-170">Make sure that you select *docker-linux* as hello **Branch specification**.</span></span>

    ![Visual Studio Team Services - Configuração do Repositório de Compilação](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. <span data-ttu-id="27e85-172">Por fim, clique em Olá **opções** guia e configurar a fila de agente padrão Olá muito**hospedado Linux visualização**.</span><span class="sxs-lookup"><span data-stu-id="27e85-172">Finally, click hello **Options** tab and configure hello Default agent queue too**Hosted Linux Preview**.</span></span>

    ![Visual Studio Team Services – Configuração do Agente de Host](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="27e85-174">Definir o fluxo de trabalho de compilação de saudação</span><span class="sxs-lookup"><span data-stu-id="27e85-174">Define hello build workflow</span></span>
<span data-ttu-id="27e85-175">as próximas etapas Olá definem o fluxo de trabalho de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="27e85-175">hello next steps define hello build workflow.</span></span> <span data-ttu-id="27e85-176">Primeiro, é necessário tooconfigure fonte de saudação do código de saudação.</span><span class="sxs-lookup"><span data-stu-id="27e85-176">First, you need tooconfigure hello source of hello code.</span></span> <span data-ttu-id="27e85-177">toodo-la, marque **GitHub** e **repositório** e **ramificação** (docker-linux).</span><span class="sxs-lookup"><span data-stu-id="27e85-177">toodo it, select **GitHub** and your **repository** and **branch** (docker-linux).</span></span>

![Visual Studio Team Services – Configurar o código-fonte](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

<span data-ttu-id="27e85-179">Há cinco toobuild de imagens de contêiner para Olá *MyShop* aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27e85-179">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="27e85-180">Cada imagem é criada usando Olá que dockerfile localizado em pastas de projeto hello:</span><span class="sxs-lookup"><span data-stu-id="27e85-180">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="27e85-181">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="27e85-181">ProductsApi</span></span>
* <span data-ttu-id="27e85-182">Proxy</span><span class="sxs-lookup"><span data-stu-id="27e85-182">Proxy</span></span>
* <span data-ttu-id="27e85-183">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="27e85-183">RatingsApi</span></span>
* <span data-ttu-id="27e85-184">RecommendationsApi</span><span class="sxs-lookup"><span data-stu-id="27e85-184">RecommandationsApi</span></span>
* <span data-ttu-id="27e85-185">ShopFront</span><span class="sxs-lookup"><span data-stu-id="27e85-185">ShopFront</span></span>

<span data-ttu-id="27e85-186">Você precisa de duas etapas de Docker para cada imagem, uma imagem de saudação toobuild e uma imagem de saudação toopush no registro do contêiner do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="27e85-186">You need two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="27e85-187">Clique em tooadd uma etapa no fluxo de trabalho de compilação hello, **+ adicionar a etapa de compilação** e selecione **Docker**.</span><span class="sxs-lookup"><span data-stu-id="27e85-187">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - Adicionar Etapas da Compilação](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. <span data-ttu-id="27e85-189">Para cada imagem, configure uma etapa que usa Olá `docker build` comando.</span><span class="sxs-lookup"><span data-stu-id="27e85-189">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services - Compilação do Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    <span data-ttu-id="27e85-191">Operação de criação para hello, selecione o registro de contêiner do Azure, hello **criar uma imagem** ação e Olá Dockerfile que define cada imagem.</span><span class="sxs-lookup"><span data-stu-id="27e85-191">For hello build operation, select your Azure Container Registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="27e85-192">Olá conjunto **diretório de trabalho** como diretório de raiz de Dockerfile hello, definir Olá **nome da imagem**e selecione **incluir mais recente marca**.</span><span class="sxs-lookup"><span data-stu-id="27e85-192">Set hello **Working Directory** as hello Dockerfile root directory, define hello **Image Name**, and select **Include Latest Tag**.</span></span>
    
    <span data-ttu-id="27e85-193">Olá, nome da imagem tem toobe neste formato: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span><span class="sxs-lookup"><span data-stu-id="27e85-193">hello Image Name has toobe in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span></span> <span data-ttu-id="27e85-194">Substituir **[nome]** com o nome da imagem hello:</span><span class="sxs-lookup"><span data-stu-id="27e85-194">Replace **[NAME]** with hello image name:</span></span>
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. <span data-ttu-id="27e85-195">Para cada imagem, configurar uma segunda etapa que usa Olá `docker push` comando.</span><span class="sxs-lookup"><span data-stu-id="27e85-195">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services - Envio do Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    <span data-ttu-id="27e85-197">Para a operação de envio por push hello, selecione o registro de contêiner do Azure, hello **enviar por Push uma imagem** ação, digite Olá **nome da imagem** que é criado na etapa anterior hello e selecione **incluem marca mais recente **.</span><span class="sxs-lookup"><span data-stu-id="27e85-197">For hello push operation, select your Azure container registry, hello **Push an image** action, enter hello **Image Name** that is built in hello previous step and select **Include Latest Tag**.</span></span>

4. <span data-ttu-id="27e85-198">Depois de configurar o build hello e enviar por push as etapas para cada uma das imagens de cinco hello, adicione que três etapas mais Olá criar fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="27e85-198">After you configure hello build and push steps for each of hello five images, add three more steps in hello build workflow.</span></span>

   ![Visual Studio Team Services – Adicionar Tarefa de Linha de Comando](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. <span data-ttu-id="27e85-200">Uma tarefa de linha de comando que usa uma saudação do bash script tooreplace *RegistryURL* ocorrência no arquivo de docker compose.yml Olá com variável de RegistryURL hello.</span><span class="sxs-lookup"><span data-stu-id="27e85-200">A command-line task that uses a bash script tooreplace hello *RegistryURL* occurrence in hello docker-compose.yml file with hello RegistryURL variable.</span></span> 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services – Atualizar arquivo de composição com a URL do Registro](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. <span data-ttu-id="27e85-202">Uma tarefa de linha de comando que usa uma saudação do bash script tooreplace *AgentURL* ocorrência no arquivo de docker compose.yml Olá com variável de AgentURL hello.</span><span class="sxs-lookup"><span data-stu-id="27e85-202">A command-line task that uses a bash script tooreplace hello *AgentURL* occurrence in hello docker-compose.yml file with hello AgentURL variable.</span></span>
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. <span data-ttu-id="27e85-203">Uma tarefa que descarta Olá atualizou o arquivo de composição como um artefato de compilação para que ele pode ser usado na versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="27e85-203">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="27e85-204">Consulte Olá após a tela para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="27e85-204">See hello following screen for details.</span></span>

         ![Visual Studio Team Services – Publicar Artefato](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - Publicar arquivo de composição](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. <span data-ttu-id="27e85-207">Clique em **Salvar & fila** tootest sua definição de compilação.</span><span class="sxs-lookup"><span data-stu-id="27e85-207">Click **Save & queue** tootest your build definition.</span></span>

   ![Visual Studio Team Services – Salvar e enfileirar](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services – Nova Fila](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. <span data-ttu-id="27e85-210">Se hello **criar** está correto, você tem toosee esta tela:</span><span class="sxs-lookup"><span data-stu-id="27e85-210">If hello **Build** is correct, you have toosee this screen:</span></span>

  ![Visual Studio Team Services – Compilação bem-sucedida](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="27e85-212">Etapa 3: Criar a definição de versão Olá</span><span class="sxs-lookup"><span data-stu-id="27e85-212">Step 3: Create hello release definition</span></span>

<span data-ttu-id="27e85-213">Visual Studio Team Services permite que você muito[gerenciar versões em ambientes](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="27e85-213">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="27e85-214">Você pode habilitar a implantação contínua toomake-se de que seu aplicativo é implantado em seus ambientes diferentes (como desenvolvimento, teste, pré-produção e produção) de forma suave.</span><span class="sxs-lookup"><span data-stu-id="27e85-214">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="27e85-215">Você pode criar um ambiente que representa seu cluster do Serviço de Contêiner do Azure no modo Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="27e85-215">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span></span>

![Visual Studio Team Services - versão tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="27e85-217">Configuração da versão inicial</span><span class="sxs-lookup"><span data-stu-id="27e85-217">Initial release setup</span></span>

1. <span data-ttu-id="27e85-218">toocreate uma definição de versão, clique em **versões** > **+ versão**</span><span class="sxs-lookup"><span data-stu-id="27e85-218">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="27e85-219">fonte de artefato Olá tooconfigure, clique em **artefatos** > **vincular a uma fonte de artefato**.</span><span class="sxs-lookup"><span data-stu-id="27e85-219">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="27e85-220">Vincule aqui, esta nova compilação de toohello de definição de versão definido na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="27e85-220">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="27e85-221">Depois disso, o arquivo de docker compose.yml de saudação está disponível no processo de liberação de saudação.</span><span class="sxs-lookup"><span data-stu-id="27e85-221">After that, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services - Artefatos da Versão](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. <span data-ttu-id="27e85-223">gatilho de versão de hello tooconfigure, clique em **gatilhos** e selecione **implantação contínua**.</span><span class="sxs-lookup"><span data-stu-id="27e85-223">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="27e85-224">Gatilho de saudação do conjunto em Olá mesma fonte de artefato.</span><span class="sxs-lookup"><span data-stu-id="27e85-224">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="27e85-225">Essa configuração garante que uma nova versão inicia quando a compilação de saudação for concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="27e85-225">This setting ensures that a new release starts when hello build completes successfully.</span></span>

    ![Visual Studio Team Services - Gatilhos da Versão](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. <span data-ttu-id="27e85-227">Clique em variáveis de versão do tooconfigure Olá, **variáveis** e selecione **+ variável** toocreate três novas variáveis com informações de saudação do registro Olá: **docker.username**, **docker.password**, e **docker.registry**.</span><span class="sxs-lookup"><span data-stu-id="27e85-227">tooconfigure hello release variables, click **Variables** and select **+Variable** toocreate three new variables with hello info of hello registry: **docker.username**, **docker.password**, and **docker.registry**.</span></span> <span data-ttu-id="27e85-228">Colar valores de saudação do registro e DNS de agentes do Cluster.</span><span class="sxs-lookup"><span data-stu-id="27e85-228">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services - Configuração do Repositório de Compilação](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > <span data-ttu-id="27e85-230">Conforme mostrado na tela anterior hello, clique em Olá **bloqueio** caixa de seleção no docker.password.</span><span class="sxs-lookup"><span data-stu-id="27e85-230">As shown on hello previous screen, click hello **Lock** checkbox in docker.password.</span></span> <span data-ttu-id="27e85-231">Essa configuração é a senha de saudação do toorestrict importantes.</span><span class="sxs-lookup"><span data-stu-id="27e85-231">This setting is important toorestrict hello password.</span></span>
    >

### <a name="define-hello-release-workflow"></a><span data-ttu-id="27e85-232">Definir o fluxo de trabalho do hello versão</span><span class="sxs-lookup"><span data-stu-id="27e85-232">Define hello release workflow</span></span>

<span data-ttu-id="27e85-233">fluxo de trabalho de versão de saudação é composto de duas tarefas que você adicionar.</span><span class="sxs-lookup"><span data-stu-id="27e85-233">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="27e85-234">Configurar uma saudação de cópia de toosecurely tarefa compor arquivo tooa *implantar* pasta Olá Docker Swarm nó mestre, usando a conexão SSH de saudação foi configurado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="27e85-234">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="27e85-235">Consulte Olá após a tela para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="27e85-235">See hello following screen for details.</span></span>
    
    <span data-ttu-id="27e85-236">Pasta de origem: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span><span class="sxs-lookup"><span data-stu-id="27e85-236">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span></span>

    ![Visual Studio Team Services - SCP da Versão](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. <span data-ttu-id="27e85-238">Configurar uma segunda tooexecute de tarefa um toorun de comando bash `docker` e `docker stack deploy` comandos no nó mestre hello.</span><span class="sxs-lookup"><span data-stu-id="27e85-238">Configure a second task tooexecute a bash command toorun `docker` and `docker stack deploy` commands on hello master node.</span></span> <span data-ttu-id="27e85-239">Consulte Olá após a tela para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="27e85-239">See hello following screen for details.</span></span>

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services - Bash da Versão](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    <span data-ttu-id="27e85-241">comando Olá executado no mestre de saudação usa hello CLI do Docker e Olá Olá de toodo de CLI do Docker Compose tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27e85-241">hello command executed on hello master uses hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="27e85-242">Faça logon no registro de contêiner do Azure toohello (ele usa três variáveis de compilação que são definidas em Olá **variáveis** guia)</span><span class="sxs-lookup"><span data-stu-id="27e85-242">Log in toohello Azure container registry (it uses three build variables that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="27e85-243">Definir Olá **DOCKER_HOST** toowork variável com o ponto de extremidade do hello por nuvem (: 2375)</span><span class="sxs-lookup"><span data-stu-id="27e85-243">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="27e85-244">Navegue toohello *implantar* pasta que foi criado por Olá anterior a tarefa de cópia seguro e que contém o arquivo de docker compose.yml Olá</span><span class="sxs-lookup"><span data-stu-id="27e85-244">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="27e85-245">Executar `docker stack deploy` comandos pull novas imagens de saudação e criar contêineres de saudação.</span><span class="sxs-lookup"><span data-stu-id="27e85-245">Execute `docker stack deploy` commands that pull hello new images and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="27e85-246">Conforme mostrado na tela anterior hello, deixe Olá **falhar em STDERR** caixa de seleção está desmarcada.</span><span class="sxs-lookup"><span data-stu-id="27e85-246">As shown on hello previous screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="27e85-247">Essa configuração permite que nós toocomplete Olá versão processo devido muito`docker-compose` imprime várias mensagens de diagnósticas, como contêineres de interrupção ou excluído, na saída de erro padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="27e85-247">This setting allows us toocomplete hello release process due too`docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="27e85-248">Se você marcar a caixa de seleção hello, Visual Studio Team Services informa que ocorreram erros durante a versão de hello, mesmo se tudo correr bem.</span><span class="sxs-lookup"><span data-stu-id="27e85-248">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="27e85-249">Salve a nova definição da versão.</span><span class="sxs-lookup"><span data-stu-id="27e85-249">Save this new release definition.</span></span>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="27e85-250">Etapa 4: Testar o pipeline de CI/CD Olá</span><span class="sxs-lookup"><span data-stu-id="27e85-250">Step 4: Test hello CI/CD pipeline</span></span>

<span data-ttu-id="27e85-251">Agora que você concluir configuração Olá, é hora tootest esse novo pipeline de CI/CD.</span><span class="sxs-lookup"><span data-stu-id="27e85-251">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="27e85-252">Olá tootest de maneira mais fácil é tooupdate Olá Olá de código e a confirmação do código-fonte é alterado para o repositório do GitHub.</span><span class="sxs-lookup"><span data-stu-id="27e85-252">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="27e85-253">Alguns segundos depois que você enviar por push código hello, você verá uma nova compilação em execução no Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="27e85-253">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="27e85-254">Depois de concluído com êxito, uma nova versão é disparada e implantado a nova versão saudação do aplicativo hello no cluster do serviço de contêiner do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="27e85-254">Once completed successfully, a new release is triggered and deployed hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27e85-255">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="27e85-255">Next steps</span></span>

* <span data-ttu-id="27e85-256">Para obter mais informações sobre CI/CD com o Visual Studio Team Services, consulte Olá [visão geral do VSTS criar](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="27e85-256">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
* <span data-ttu-id="27e85-257">Para obter mais informações sobre o mecanismo do ACS, consulte Olá [repositório GitHub do mecanismo de ACS](https://github.com/Azure/acs-engine).</span><span class="sxs-lookup"><span data-stu-id="27e85-257">For more information about ACS Engine, see hello [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span></span>
* <span data-ttu-id="27e85-258">Para obter mais informações sobre o modo de Docker Swarm, consulte Olá [Docker Swarm visão geral do modo](https://docs.docker.com/engine/swarm/).</span><span class="sxs-lookup"><span data-stu-id="27e85-258">For more information about Docker Swarm mode, see hello [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span></span>
