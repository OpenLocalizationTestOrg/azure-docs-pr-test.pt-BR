---
title: "aaaCI/CD com o serviço de contêiner do Azure e por nuvem | Microsoft Docs"
description: "Usar serviço de contêiner do Azure com o Docker Swarm, um registro de contêiner do Azure e do Visual Studio Team Services toodeliver continuamente um aplicativo do .NET Core vários contêiner"
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Swarm, Azure, Visual Studio Team Services, DevOps"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a><span data-ttu-id="780b0-104">CI/CD completo pipeline toodeploy um aplicativo de multi-contêiner no serviço de contêiner do Azure com o Docker Swarm usando o Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="780b0-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services</span></span>

<span data-ttu-id="780b0-105">Um dos Olá maiores desafios ao desenvolvimento de aplicativos modernos para nuvem hello está sendo toodeliver capaz desses aplicativos continuamente.</span><span class="sxs-lookup"><span data-stu-id="780b0-105">One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="780b0-106">Neste artigo, saiba como criar a tooimplement uma integração contínua total e pipeline de implantação (CI/CD) usando o serviço de contêiner do Azure com o Docker Swarm, o registro de contêiner do Azure e o Visual Studio Team Services e gerenciamento de liberações.</span><span class="sxs-lookup"><span data-stu-id="780b0-106">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Visual Studio Team Services build and release management.</span></span>

<span data-ttu-id="780b0-107">Este artigo se baseia em um aplicativo simples, disponível no [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), desenvolvido com o ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="780b0-107">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span></span> <span data-ttu-id="780b0-108">aplicativo Hello é composto de quatro diferentes serviços: três web APIs e um web front-end:</span><span class="sxs-lookup"><span data-stu-id="780b0-108">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![Aplicativo de exemplo MyShop](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

<span data-ttu-id="780b0-110">o objetivo de saudação é toodeliver esse aplicativo continuamente em um cluster de Docker Swarm, usando o Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="780b0-110">hello objective is toodeliver this application continuously in a Docker Swarm cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="780b0-111">a figura de saudação a seguir detalhes esse pipeline entrega contínua:</span><span class="sxs-lookup"><span data-stu-id="780b0-111">hello following figure details this continuous delivery pipeline:</span></span>

![Aplicativo de exemplo MyShop](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

<span data-ttu-id="780b0-113">Aqui está uma breve explicação das etapas de saudação:</span><span class="sxs-lookup"><span data-stu-id="780b0-113">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="780b0-114">Alterações de código são o repositório de código fonte toohello confirmada (aqui, GitHub)</span><span class="sxs-lookup"><span data-stu-id="780b0-114">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="780b0-115">O GitHub dispara uma compilação no Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="780b0-115">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="780b0-116">Visual Studio Team Services obtém a versão mais recente de saudação do fontes hello e cria todas as imagens de saudação que compõem o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="780b0-116">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="780b0-117">Visual Studio Team Services envia cada registro da imagem tooa Docker criado usando o serviço de registro de contêiner do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="780b0-117">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="780b0-118">O Visual Studio Team Services dispara uma nova versão</span><span class="sxs-lookup"><span data-stu-id="780b0-118">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="780b0-119">versão Olá executa alguns comandos usando o SSH no nó do contêiner do Azure serviço cluster mestre Olá</span><span class="sxs-lookup"><span data-stu-id="780b0-119">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="780b0-120">Por nuvem de docker Olá cluster recebe Olá versão mais recente das imagens de saudação</span><span class="sxs-lookup"><span data-stu-id="780b0-120">Docker Swarm on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="780b0-121">Olá nova versão do aplicativo hello é implantada usando o Docker Compose</span><span class="sxs-lookup"><span data-stu-id="780b0-121">hello new version of hello application is deployed using Docker Compose</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="780b0-122">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="780b0-122">Prerequisites</span></span>

<span data-ttu-id="780b0-123">Antes de iniciar este tutorial, você precisa toocomplete Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="780b0-123">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="780b0-124">Criar um Cluster Swarm no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="780b0-124">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)
- [<span data-ttu-id="780b0-125">Conecte-se com o cluster de por nuvem Olá no serviço de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="780b0-125">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="780b0-126">Criar um registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="780b0-126">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="780b0-127">Ter uma conta do Visual Studio Team Services e projeto de equipe criados</span><span class="sxs-lookup"><span data-stu-id="780b0-127">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="780b0-128">Bifurcação Olá GitHub repositório tooyour conta do GitHub</span><span class="sxs-lookup"><span data-stu-id="780b0-128">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="780b0-129">Você também precisa de um computador Ubuntu (14.04 ou 16.04) com o Docker instalado.</span><span class="sxs-lookup"><span data-stu-id="780b0-129">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span></span> <span data-ttu-id="780b0-130">Este computador é usado pelo Visual Studio Team Services durante a saudação de compilação e processos de versão.</span><span class="sxs-lookup"><span data-stu-id="780b0-130">This machine is used by Visual Studio Team Services during hello build and release processes.</span></span> <span data-ttu-id="780b0-131">Uma maneira toocreate essa máquina é imagem de saudação toouse disponível no hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span><span class="sxs-lookup"><span data-stu-id="780b0-131">One way toocreate this machine is toouse hello image available in hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span></span> 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="780b0-132">Etapa 1: Configurar sua conta do Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="780b0-132">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="780b0-133">Nesta seção, você configura sua conta do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="780b0-133">In this section, you configure your Visual Studio Team Services account.</span></span>

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a><span data-ttu-id="780b0-134">Configurar um agente de compilação Linux do Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="780b0-134">Configure a Visual Studio Team Services Linux build agent</span></span>

<span data-ttu-id="780b0-135">imagens do Docker toocreate e enviar por push que criar essas imagens em um registro de contêiner do Azure do Visual Studio Team Services, você precisa tooregister um agente do Linux.</span><span class="sxs-lookup"><span data-stu-id="780b0-135">toocreate Docker images and push these images into an Azure container registry from a Visual Studio Team Services build, you need tooregister a Linux agent.</span></span> <span data-ttu-id="780b0-136">Você tem estas opções de instalação:</span><span class="sxs-lookup"><span data-stu-id="780b0-136">You have these installation options:</span></span>

* [<span data-ttu-id="780b0-137">Implantar um agente no Linux</span><span class="sxs-lookup"><span data-stu-id="780b0-137">Deploy an agent on Linux</span></span>](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [<span data-ttu-id="780b0-138">Use o Docker toorun Olá VSTS agent</span><span class="sxs-lookup"><span data-stu-id="780b0-138">Use Docker toorun hello VSTS agent</span></span>](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a><span data-ttu-id="780b0-139">Instalar a extensão de Docker integração VSTS Olá</span><span class="sxs-lookup"><span data-stu-id="780b0-139">Install hello Docker Integration VSTS extension</span></span>

<span data-ttu-id="780b0-140">A Microsoft fornece uma extensão VSTS toowork com o Docker na compilação e processos de versão.</span><span class="sxs-lookup"><span data-stu-id="780b0-140">Microsoft provides a VSTS extension toowork with Docker in build and release processes.</span></span> <span data-ttu-id="780b0-141">Essa extensão está disponível em Olá [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span><span class="sxs-lookup"><span data-stu-id="780b0-141">This extension is available in hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span></span> <span data-ttu-id="780b0-142">Clique em **instalar** tooadd essa conta do VSTS de tooyour extensão:</span><span class="sxs-lookup"><span data-stu-id="780b0-142">Click **Install** tooadd this extension tooyour VSTS account:</span></span>

![Instalar Olá integração de Docker](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

<span data-ttu-id="780b0-144">Conta VSTS tooyour tooconnect usando suas credenciais serão solicitadas.</span><span class="sxs-lookup"><span data-stu-id="780b0-144">You are asked tooconnect tooyour VSTS account using your credentials.</span></span> 

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="780b0-145">Conectar o Visual Studio Team Services e o GitHub</span><span class="sxs-lookup"><span data-stu-id="780b0-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="780b0-146">Configure uma conexão entre seu projeto VSTS e sua conta GitHub.</span><span class="sxs-lookup"><span data-stu-id="780b0-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="780b0-147">No seu projeto do Visual Studio Team Services, clique em Olá **configurações** ícone na barra de ferramentas hello e selecione **serviços**.</span><span class="sxs-lookup"><span data-stu-id="780b0-147">In your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

    ![Visual Studio Team Services - Conexão Externa](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. <span data-ttu-id="780b0-149">Olá esquerda, clique em **novo ponto de extremidade de serviço** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="780b0-149">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>

    ![Visual Studio Team Services - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. <span data-ttu-id="780b0-151">tooauthorize VSTS toowork com sua conta do GitHub, clique em **autorizar** e siga o procedimento Olá na janela de saudação que é aberta.</span><span class="sxs-lookup"><span data-stu-id="780b0-151">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services - Autorizar GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a><span data-ttu-id="780b0-153">Conecte-se o registro do VSTS tooyour contêiner do Azure e o cluster do serviço de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="780b0-153">Connect VSTS tooyour Azure container registry and Azure Container Service cluster</span></span>

<span data-ttu-id="780b0-154">últimas etapas Olá antes de entrar no pipeline de CI/CD Olá são registro de contêiner de tooyour tooconfigure conexões externas e o cluster Docker Swarm no Azure.</span><span class="sxs-lookup"><span data-stu-id="780b0-154">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour container registry and your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="780b0-155">Em Olá **serviços** configurações do seu projeto do Visual Studio Team Services, adicione um ponto de extremidade de serviço do tipo **Docker registro**.</span><span class="sxs-lookup"><span data-stu-id="780b0-155">In hello **Services** settings of your Visual Studio Team Services project, add a service endpoint of type **Docker Registry**.</span></span> 

2. <span data-ttu-id="780b0-156">No hello pop-up que é aberta, digite o URL de hello e credenciais de saudação do registro do contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="780b0-156">In hello popup that opens, enter hello URL and hello credentials of your Azure container registry.</span></span>

    ![Visual Studio Team Services - Registro do Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. <span data-ttu-id="780b0-158">Para o cluster Docker Swarm hello, adicione um ponto de extremidade do tipo **SSH**.</span><span class="sxs-lookup"><span data-stu-id="780b0-158">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="780b0-159">Em seguida, insira informações de conexão SSH saudação do cluster por nuvem.</span><span class="sxs-lookup"><span data-stu-id="780b0-159">Then enter hello SSH connection information of your Swarm cluster.</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

<span data-ttu-id="780b0-161">Todas as configurações de saudação é feito agora.</span><span class="sxs-lookup"><span data-stu-id="780b0-161">All hello configuration is done now.</span></span> <span data-ttu-id="780b0-162">Próximas etapas de Olá, você criará um pipeline de CI/CD Olá que compila e implanta Olá aplicativo toohello Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="780b0-162">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="780b0-163">Etapa 2: Criar a definição de compilação Olá</span><span class="sxs-lookup"><span data-stu-id="780b0-163">Step 2: Create hello build definition</span></span>

<span data-ttu-id="780b0-164">Nesta etapa, você configurar seu projeto VSTS definitionfor uma compilação e define o fluxo de trabalho de compilação de saudação para as imagens de contêiner</span><span class="sxs-lookup"><span data-stu-id="780b0-164">In this step, you set up a build definitionfor your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="780b0-165">Configuração da definição inicial</span><span class="sxs-lookup"><span data-stu-id="780b0-165">Initial definition setup</span></span>

1. <span data-ttu-id="780b0-166">toocreate uma definição de compilação, conecte-se tooyour do Visual Studio Team Services do projeto e clique em **Build e versão**.</span><span class="sxs-lookup"><span data-stu-id="780b0-166">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> 

2. <span data-ttu-id="780b0-167">Em Olá **definições de compilação** seção, clique em **+ novo**.</span><span class="sxs-lookup"><span data-stu-id="780b0-167">In hello **Build definitions** section, click **+ New**.</span></span> <span data-ttu-id="780b0-168">Selecione Olá **vazio** modelo.</span><span class="sxs-lookup"><span data-stu-id="780b0-168">Select hello **Empty** template.</span></span>

    ![Visual Studio Team Services - Nova Definição da Compilação](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. <span data-ttu-id="780b0-170">Configurar nova compilação do hello com uma fonte de repositório do GitHub, seleção **integração contínua**e a fila de agente hello selecione onde você registrou seu agente do Linux.</span><span class="sxs-lookup"><span data-stu-id="780b0-170">Configure hello new build with a GitHub repository source, check **Continuous integration**, and select hello agent queue where you registered your Linux agent.</span></span> <span data-ttu-id="780b0-171">Clique em **criar** toocreate Olá definição de compilação.</span><span class="sxs-lookup"><span data-stu-id="780b0-171">Click **Create** toocreate hello build definition.</span></span>

    ![Visual Studio Team Services - Criar Definição da Compilação](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. <span data-ttu-id="780b0-173">Em Olá **definições de compilação** página, primeiro abra Olá **repositório** guia e configurar a bifurcação de saudação de toouse Olá compilação do projeto de MyShop Olá que você criou nos pré-requisitos Olá.</span><span class="sxs-lookup"><span data-stu-id="780b0-173">On hello **Build Definitions** page, first open hello **Repository** tab and configure hello build toouse hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="780b0-174">Certifique-se de que você selecione *acs documentos* como Olá **branch padrão**.</span><span class="sxs-lookup"><span data-stu-id="780b0-174">Make sure that you select *acs-docs* as hello **Default branch**.</span></span>

    ![Visual Studio Team Services - Configuração do Repositório de Compilação](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. <span data-ttu-id="780b0-176">Em Olá **gatilhos** guia, defina Olá compilação toobe acionado após cada confirmação.</span><span class="sxs-lookup"><span data-stu-id="780b0-176">On hello **Triggers** tab, configure hello build toobe triggered after each commit.</span></span> <span data-ttu-id="780b0-177">Selecione **Integração contínua** e **Alterações de lote**.</span><span class="sxs-lookup"><span data-stu-id="780b0-177">Select **Continuous integration** and **Batch changes**.</span></span>

    ![Visual Studio Team Services - Configuração do Gatilho de Compilação](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="780b0-179">Definir o fluxo de trabalho de compilação de saudação</span><span class="sxs-lookup"><span data-stu-id="780b0-179">Define hello build workflow</span></span>
<span data-ttu-id="780b0-180">as próximas etapas Olá definem o fluxo de trabalho de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="780b0-180">hello next steps define hello build workflow.</span></span> <span data-ttu-id="780b0-181">Há cinco toobuild de imagens de contêiner para Olá *MyShop* aplicativo.</span><span class="sxs-lookup"><span data-stu-id="780b0-181">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="780b0-182">Cada imagem é criada usando Olá que dockerfile localizado em pastas de projeto hello:</span><span class="sxs-lookup"><span data-stu-id="780b0-182">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="780b0-183">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="780b0-183">ProductsApi</span></span>
* <span data-ttu-id="780b0-184">Proxy</span><span class="sxs-lookup"><span data-stu-id="780b0-184">Proxy</span></span>
* <span data-ttu-id="780b0-185">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="780b0-185">RatingsApi</span></span>
* <span data-ttu-id="780b0-186">RecommendationsApi</span><span class="sxs-lookup"><span data-stu-id="780b0-186">RecommandationsApi</span></span>
* <span data-ttu-id="780b0-187">ShopFront</span><span class="sxs-lookup"><span data-stu-id="780b0-187">ShopFront</span></span>

<span data-ttu-id="780b0-188">Você precisa de duas etapas de Docker tooadd de cada imagem, uma imagem de saudação toobuild e uma imagem de saudação toopush no registro do contêiner do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="780b0-188">You need tooadd two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="780b0-189">Clique em tooadd uma etapa no fluxo de trabalho de compilação hello, **+ adicionar a etapa de compilação** e selecione **Docker**.</span><span class="sxs-lookup"><span data-stu-id="780b0-189">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - Adicionar Etapas da Compilação](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. <span data-ttu-id="780b0-191">Para cada imagem, configure uma etapa que usa Olá `docker build` comando.</span><span class="sxs-lookup"><span data-stu-id="780b0-191">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services - Compilação do Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    <span data-ttu-id="780b0-193">Operação de criação para hello, selecione o registro de contêiner do Azure, hello **criar uma imagem** ação e Olá Dockerfile que define cada imagem.</span><span class="sxs-lookup"><span data-stu-id="780b0-193">For hello build operation, select your Azure container registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="780b0-194">Saudação de conjunto **contexto de compilação** como Olá Dockerfile diretório raiz e definir Olá **nome da imagem**.</span><span class="sxs-lookup"><span data-stu-id="780b0-194">Set hello **Build context** as hello Dockerfile root directory, and define hello **Image Name**.</span></span> 
    
    <span data-ttu-id="780b0-195">Conforme mostrado no hello antes da tela, inicie o nome de imagem de Olá com hello URI do registro do contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="780b0-195">As shown on hello preceding screen, start hello image name with hello URI of your Azure container registry.</span></span> <span data-ttu-id="780b0-196">(Você também pode usar uma marca de saudação tooparameterize variável build de imagem de hello, como o identificador de compilação Olá neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="780b0-196">(You can also use a build variable tooparameterize hello tag of hello image, such as hello build identifier in this example.)</span></span>

3. <span data-ttu-id="780b0-197">Para cada imagem, configurar uma segunda etapa que usa Olá `docker push` comando.</span><span class="sxs-lookup"><span data-stu-id="780b0-197">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services - Envio do Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    <span data-ttu-id="780b0-199">Para a operação de envio por push hello, selecione o registro de contêiner do Azure, hello **enviar por Push uma imagem** ação e digite Olá **nome da imagem** que é criado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="780b0-199">For hello push operation, select your Azure container registry, hello **Push an image** action, and enter hello **Image Name** that is built in hello previous step.</span></span>

4. <span data-ttu-id="780b0-200">Depois de configurar o build hello e enviar por push as etapas para cada uma das imagens de cinco hello, adicione que mais duas etapas no hello criar fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="780b0-200">After you configure hello build and push steps for each of hello five images, add two more steps in hello build workflow.</span></span>

    <span data-ttu-id="780b0-201">a.</span><span class="sxs-lookup"><span data-stu-id="780b0-201">a.</span></span> <span data-ttu-id="780b0-202">Uma tarefa de linha de comando que usa uma saudação do bash script tooreplace *BuildNumber* ocorrência no arquivo de docker compose.yml Olá com hello atual criar ID. Consulte Olá após a tela para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="780b0-202">A command-line task that uses a bash script tooreplace hello *BuildNumber* occurrence in hello docker-compose.yml file with hello current build Id. See hello following screen for details.</span></span>

    ![Visual Studio Team Services - Atualizar arquivo de composição](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    <span data-ttu-id="780b0-204">b.</span><span class="sxs-lookup"><span data-stu-id="780b0-204">b.</span></span> <span data-ttu-id="780b0-205">Uma tarefa que descarta Olá atualizou o arquivo de composição como um artefato de compilação para que ele pode ser usado na versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="780b0-205">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="780b0-206">Consulte Olá após a tela para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="780b0-206">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - Publicar arquivo de composição](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. <span data-ttu-id="780b0-208">Clique em **Salvar** e nomeie sua definição de compilação.</span><span class="sxs-lookup"><span data-stu-id="780b0-208">Click **Save** and name your build definition.</span></span>

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="780b0-209">Etapa 3: Criar a definição de versão Olá</span><span class="sxs-lookup"><span data-stu-id="780b0-209">Step 3: Create hello release definition</span></span>

<span data-ttu-id="780b0-210">Visual Studio Team Services permite que você muito[gerenciar versões em ambientes](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="780b0-210">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="780b0-211">Você pode habilitar a implantação contínua toomake-se de que seu aplicativo é implantado em seus ambientes diferentes (como desenvolvimento, teste, pré-produção e produção) de forma suave.</span><span class="sxs-lookup"><span data-stu-id="780b0-211">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="780b0-212">Você pode criar um novo ambiente que representa o cluster Docker Swarm do Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="780b0-212">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span></span>

![Visual Studio Team Services - versão tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="780b0-214">Configuração da versão inicial</span><span class="sxs-lookup"><span data-stu-id="780b0-214">Initial release setup</span></span>

1. <span data-ttu-id="780b0-215">toocreate uma definição de versão, clique em **versões** > **+ versão**</span><span class="sxs-lookup"><span data-stu-id="780b0-215">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="780b0-216">fonte de artefato Olá tooconfigure, clique em **artefatos** > **vincular a uma fonte de artefato**.</span><span class="sxs-lookup"><span data-stu-id="780b0-216">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="780b0-217">Vincule aqui, esta nova compilação de toohello de definição de versão definido na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="780b0-217">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="780b0-218">Ao fazer isso, o arquivo de docker compose.yml de saudação está disponível no processo de liberação de saudação.</span><span class="sxs-lookup"><span data-stu-id="780b0-218">By doing this, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services - Artefatos da Versão](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. <span data-ttu-id="780b0-220">gatilho de versão de hello tooconfigure, clique em **gatilhos** e selecione **implantação contínua**.</span><span class="sxs-lookup"><span data-stu-id="780b0-220">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="780b0-221">Gatilho de saudação do conjunto em Olá mesma fonte de artefato.</span><span class="sxs-lookup"><span data-stu-id="780b0-221">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="780b0-222">Essa configuração garante que uma nova versão começa assim que a compilação de saudação for concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="780b0-222">This setting ensures that a new release starts as soon as hello build completes successfully.</span></span>

    ![Visual Studio Team Services - Gatilhos da Versão](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a><span data-ttu-id="780b0-224">Definir o fluxo de trabalho do hello versão</span><span class="sxs-lookup"><span data-stu-id="780b0-224">Define hello release workflow</span></span>

<span data-ttu-id="780b0-225">fluxo de trabalho de versão de saudação é composto de duas tarefas que você adicionar.</span><span class="sxs-lookup"><span data-stu-id="780b0-225">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="780b0-226">Configurar uma saudação de cópia de toosecurely tarefa compor arquivo tooa *implantar* pasta Olá Docker Swarm nó mestre, usando a conexão SSH de saudação foi configurado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="780b0-226">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="780b0-227">Consulte Olá após a tela para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="780b0-227">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - SCP da Versão](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. <span data-ttu-id="780b0-229">Configurar uma segunda tooexecute de tarefa um toorun de comando bash `docker` e `docker-compose` comandos no nó mestre hello.</span><span class="sxs-lookup"><span data-stu-id="780b0-229">Configure a second task tooexecute a bash command toorun `docker` and `docker-compose` commands on hello master node.</span></span> <span data-ttu-id="780b0-230">Consulte Olá após a tela para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="780b0-230">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - Bash da Versão](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    <span data-ttu-id="780b0-232">comando Olá executado em Olá use mestre Olá CLI do Docker e Olá Olá de toodo de CLI do Docker Compose tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="780b0-232">hello command executed on hello master use hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="780b0-233">Registro de contêiner do Azure toohello login (ele usa três variab'les de compilação que são definidos em Olá **variáveis** guia)</span><span class="sxs-lookup"><span data-stu-id="780b0-233">Login toohello Azure container registry (it uses three build variab\`les that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="780b0-234">Definir Olá **DOCKER_HOST** toowork variável com o ponto de extremidade do hello por nuvem (: 2375)</span><span class="sxs-lookup"><span data-stu-id="780b0-234">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="780b0-235">Navegue toohello *implantar* pasta que foi criado por Olá anterior a tarefa de cópia seguro e que contém o arquivo de docker compose.yml Olá</span><span class="sxs-lookup"><span data-stu-id="780b0-235">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="780b0-236">Executar `docker-compose` comandos pull novas imagens de Olá, interromper serviços hello, remover serviços hello e criar contêineres de saudação.</span><span class="sxs-lookup"><span data-stu-id="780b0-236">Execute `docker-compose` commands that pull hello new images, stop hello services, remove hello services, and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="780b0-237">Conforme mostrado no hello antes da tela, deixe Olá **falhar em STDERR** caixa de seleção está desmarcada.</span><span class="sxs-lookup"><span data-stu-id="780b0-237">As shown on hello preceding screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="780b0-238">Esta é uma configuração importante, porque `docker-compose` imprime várias mensagens de diagnósticas, como contêineres de interrupção ou excluído, na saída de erro padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="780b0-238">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="780b0-239">Se você marcar a caixa de seleção hello, Visual Studio Team Services informa que ocorreram erros durante a versão de hello, mesmo se tudo correr bem.</span><span class="sxs-lookup"><span data-stu-id="780b0-239">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="780b0-240">Salve a nova definição da versão.</span><span class="sxs-lookup"><span data-stu-id="780b0-240">Save this new release definition.</span></span>


>[!NOTE]
><span data-ttu-id="780b0-241">Essa implantação inclui algum tempo de inatividade porque estamos Parando serviços antigo hello e executando Olá um novo.</span><span class="sxs-lookup"><span data-stu-id="780b0-241">This deployment includes some downtime because we are stopping hello old services and running hello new one.</span></span> <span data-ttu-id="780b0-242">Ele é possível tooavoid isso fazendo uma implantação de verde e azul.</span><span class="sxs-lookup"><span data-stu-id="780b0-242">It is possible tooavoid this by doing a blue-green deployment.</span></span>
>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="780b0-243">Etapa 4.</span><span class="sxs-lookup"><span data-stu-id="780b0-243">Step 4.</span></span> <span data-ttu-id="780b0-244">Pipeline de CI/CD de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="780b0-244">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="780b0-245">Agora que você concluir configuração Olá, é hora tootest esse novo pipeline de CI/CD.</span><span class="sxs-lookup"><span data-stu-id="780b0-245">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="780b0-246">Olá tootest de maneira mais fácil é tooupdate Olá Olá de código e a confirmação do código-fonte é alterado para o repositório do GitHub.</span><span class="sxs-lookup"><span data-stu-id="780b0-246">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="780b0-247">Alguns segundos depois que você enviar por push código hello, você verá uma nova compilação em execução no Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="780b0-247">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="780b0-248">Depois de concluído com êxito, uma nova versão será disparada e implantará a nova versão saudação do aplicativo hello no cluster do serviço de contêiner do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="780b0-248">Once completed successfully, a new release will be triggered and will deploy hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="780b0-249">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="780b0-249">Next Steps</span></span>

* <span data-ttu-id="780b0-250">Para obter mais informações sobre CI/CD com o Visual Studio Team Services, consulte Olá [visão geral do VSTS criar](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="780b0-250">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
