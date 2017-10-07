---
title: aaaCI/CD de tooAzure Jenkins VMs com Team Services | Microsoft Docs
description: "Configurar a integração contínua (CI) e a implantação contínua (CD) de um aplicativo Node. js usando Jenkins tooAzure VMs do gerenciamento de versão no Visual Studio Team Services (VSTS) ou o Microsoft Team Foundation Server (TFS)"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="b5a12-103">Implantar seu aplicativo tooLinux VMs usando Jenkins e do Team Services</span><span class="sxs-lookup"><span data-stu-id="b5a12-103">Deploy your app tooLinux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="b5a12-104">CI (integração contínua) e CD (implantação contínua) é um pipeline por meio do qual você pode compilar, lançar e implantar seu código.</span><span class="sxs-lookup"><span data-stu-id="b5a12-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="b5a12-105">Team Services fornece um conjunto de ferramentas de automação de CI/CD completo, repleto para tooAzure de implantação.</span><span class="sxs-lookup"><span data-stu-id="b5a12-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment tooAzure.</span></span> <span data-ttu-id="b5a12-106">Jenkins é uma ferramenta de terceiros popular baseada em servidor de CI/CD que também fornece a automação de CI/CD.</span><span class="sxs-lookup"><span data-stu-id="b5a12-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="b5a12-107">Você pode usar ambos os toocustomize juntos como entregar seu aplicativo na nuvem ou serviço.</span><span class="sxs-lookup"><span data-stu-id="b5a12-107">You can use both together toocustomize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="b5a12-108">Neste tutorial, você use Jenkins toobuild um **aplicativo web Node.js**e o Visual Studio Team Services toodeploy-tooa [grupo de implantação](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) que contém máquinas virtuais Linux.</span><span class="sxs-lookup"><span data-stu-id="b5a12-108">In this tutorial, you use Jenkins toobuild a **Node.js web app**, and Visual Studio Team Services toodeploy it tooa [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="b5a12-109">Você vai:</span><span class="sxs-lookup"><span data-stu-id="b5a12-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b5a12-110">Compilar seu aplicativo no Jenkins</span><span class="sxs-lookup"><span data-stu-id="b5a12-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="b5a12-111">Configurar o Jenkins para integração com o Team Services</span><span class="sxs-lookup"><span data-stu-id="b5a12-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="b5a12-112">Criar um grupo de implantação para Olá máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="b5a12-112">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="b5a12-113">Criar uma definição de lançamento que configura Olá VMs e implanta o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="b5a12-113">Create a release definition that configures hello VMs and deploys hello app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b5a12-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="b5a12-114">Before you begin</span></span>

* <span data-ttu-id="b5a12-115">É necessário acesso tooa Jenkins conta.</span><span class="sxs-lookup"><span data-stu-id="b5a12-115">You need access tooa Jenkins account.</span></span> <span data-ttu-id="b5a12-116">Se você ainda não tiver criado um servidor Jenkins, confira a [Documentação do Jenkins](https://jenkins.io/doc/).</span><span class="sxs-lookup"><span data-stu-id="b5a12-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="b5a12-117">Entrar na conta do Team Services do tooyour (`https://{youraccount}.visualstudio.com`).</span><span class="sxs-lookup"><span data-stu-id="b5a12-117">Sign in tooyour Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="b5a12-118">Você pode obter uma [conta gratuita do Team Services](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span><span class="sxs-lookup"><span data-stu-id="b5a12-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="b5a12-119">Para obter mais informações, consulte [conectar os serviços de tooTeam](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="b5a12-119">For more information, see [Connect tooTeam Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="b5a12-120">Crie um PAT (token de acesso pessoal) em sua conta do Team Services se você ainda não tiver um.</span><span class="sxs-lookup"><span data-stu-id="b5a12-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="b5a12-121">Jenkins requer essa tooaccess informações sobre sua conta do Team Services.</span><span class="sxs-lookup"><span data-stu-id="b5a12-121">Jenkins requires this information tooaccess your Team Services account.</span></span>
  <span data-ttu-id="b5a12-122">Leitura [como criar um token de acesso pessoal para Team Services e o TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn como toogenerate um.</span><span class="sxs-lookup"><span data-stu-id="b5a12-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn how toogenerate one.</span></span>

## <a name="get-hello-sample-app"></a><span data-ttu-id="b5a12-123">Obter o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="b5a12-123">Get hello sample app</span></span>

<span data-ttu-id="b5a12-124">É necessário um toodeploy aplicativo armazenado em um repositório Git.</span><span class="sxs-lookup"><span data-stu-id="b5a12-124">You need an app toodeploy stored in a Git repository.</span></span>
<span data-ttu-id="b5a12-125">Para este tutorial, recomendamos o uso [deste aplicativo de exemplo disponível no GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span><span class="sxs-lookup"><span data-stu-id="b5a12-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="b5a12-126">Crie uma bifurcação deste aplicativo e anote o local de saudação (URL) para uso em etapas posteriores deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b5a12-126">Create a fork of this app and take note of hello location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="b5a12-127">Verifique a bifurcação de saudação **pública** toosimplify se tooGitHub mais tarde.</span><span class="sxs-lookup"><span data-stu-id="b5a12-127">Make hello fork **public** toosimplify connecting tooGitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="b5a12-128">Para saber mais, confira [Criar bifurcação de um repositório](https://help.github.com/articles/fork-a-repo/) e [Transformar em público um repositório privado](https://help.github.com/articles/making-a-private-repository-public/).</span><span class="sxs-lookup"><span data-stu-id="b5a12-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="b5a12-129">Olá aplicativo foi criado usando [Yeoman](http://yeoman.io/learning/index.html); ele usa **Express**, **bower**, e **grunt**; e tem algumas **npm**pacotes como dependências.</span><span class="sxs-lookup"><span data-stu-id="b5a12-129">hello app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="b5a12-130">aplicativo de exemplo Hello contém um conjunto de [modelos do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) que são usada toodynamically criar máquinas virtuais de saudação para implantação no Azure.</span><span class="sxs-lookup"><span data-stu-id="b5a12-130">hello sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used toodynamically create hello virtual machines for deployment on Azure.</span></span> <span data-ttu-id="b5a12-131">Esses modelos são usados por tarefas no hello [definição de versão do Team Services](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span><span class="sxs-lookup"><span data-stu-id="b5a12-131">These templates are used by tasks in hello [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="b5a12-132">modelo principal Olá cria um grupo de segurança de rede, uma máquina virtual e uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b5a12-132">hello main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="b5a12-133">Ele atribui um endereço IP público e abre a porta 80 de entrada.</span><span class="sxs-lookup"><span data-stu-id="b5a12-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="b5a12-134">Ele também adiciona uma marca que é usada pela implantação de saudação do hello implantação grupo Olá muito selecione máquinas tooreceive.</span><span class="sxs-lookup"><span data-stu-id="b5a12-134">It also adds a tag that is used by hello deployment group too select hello machines tooreceive hello deployment.</span></span>
>
> <span data-ttu-id="b5a12-135">exemplo Hello também contém um script que define o Nginx e implanta o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b5a12-135">hello sample also contains a script that sets up Nginx and deploys hello app.</span></span> <span data-ttu-id="b5a12-136">Ele é executado em cada uma das máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5a12-136">It is executed on each of hello virtual machines.</span></span> <span data-ttu-id="b5a12-137">Especificamente, o script hello instala nó, Nginx e PM2; Configura Nginx e PM2; em seguida, inicia o aplicativo de nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5a12-137">Specifically, hello script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts hello Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="b5a12-138">Configurar os plug-ins do Jenkins</span><span class="sxs-lookup"><span data-stu-id="b5a12-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="b5a12-139">Primeiro, você deve configurar dois plug-ins Jenkins para **NodeJS** e **Integração com o Team Services**.</span><span class="sxs-lookup"><span data-stu-id="b5a12-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="b5a12-140">Abra sua conta do Jenkins e escolha **Gerenciar Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="b5a12-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="b5a12-141">Em Olá **Jenkins gerenciar** escolha **gerenciar plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="b5a12-141">In hello **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="b5a12-142">Filtro Olá lista toolocate Olá **NodeJS** plug-in e instalá-lo sem reinicialização.</span><span class="sxs-lookup"><span data-stu-id="b5a12-142">Filter hello list toolocate hello **NodeJS** plugin and install it without restart.</span></span>

   ![Adicionando Olá NodeJS plug-in tooJenkins](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="b5a12-144">Filtro Olá lista toofind Olá **Team Foundation Server** plug-in e instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="b5a12-144">Filter hello list toofind hello **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="b5a12-145">(Esse plug-in funciona para Team Services e Team Foundation Server.) Não é necessário reiniciar o Jenkins.</span><span class="sxs-lookup"><span data-stu-id="b5a12-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="b5a12-146">Configurar o build do Jenkins para Node.js</span><span class="sxs-lookup"><span data-stu-id="b5a12-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="b5a12-147">No Jenkins, crie um novo projeto de build e configure-o da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b5a12-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="b5a12-148">Em Olá **geral** , insira um nome para seu projeto de compilação.</span><span class="sxs-lookup"><span data-stu-id="b5a12-148">In hello **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="b5a12-149">Em Olá **código-fonte gerenciamento** guia, selecione **Git** e insira os detalhes de saudação do repositório de saudação e ramificação Olá que contém o código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5a12-149">In hello **Source Code Management** tab, select **Git** and enter hello details of hello repository and hello branch containing your app code.</span></span>

   ![Adicionar uma construção de tooyour do repositório](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="b5a12-151">Se o repositório não é público, escolha **adicionar** e forneça credenciais tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="b5a12-151">If your repository is not public, choose **Add** and provide credentials tooconnect tooit.</span></span>

1. <span data-ttu-id="b5a12-152">Em Olá **criar gatilhos** guia, selecione **sondagem SCM** e digite Olá agendamento `H/03 * * * *` repositório do Git Olá toopoll para que as alterações a cada três minutos.</span><span class="sxs-lookup"><span data-stu-id="b5a12-152">In hello **Build Triggers** tab, select **Poll SCM** and enter hello schedule `H/03 * * * *` toopoll hello Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="b5a12-153">Em Olá **ambiente de compilação** guia, selecione **fornecer nó &amp; npm bin / caminho da pasta** e digite `NodeJS` para Olá valor do nó JS instalação.</span><span class="sxs-lookup"><span data-stu-id="b5a12-153">In hello **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for hello Node JS Installation value.</span></span> <span data-ttu-id="b5a12-154">Deixe o **arquivo npmrc** definido como "usar padrão do sistema".</span><span class="sxs-lookup"><span data-stu-id="b5a12-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="b5a12-155">Em Olá **criar** , insira o comando Olá `npm install` tooensure todas as dependências são atualizadas.</span><span class="sxs-lookup"><span data-stu-id="b5a12-155">In hello **Build** tab, enter hello command `npm install` tooensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="b5a12-156">Configurar o Jenkins para integração com o Team Services</span><span class="sxs-lookup"><span data-stu-id="b5a12-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="b5a12-157">Em Olá **ações de pós-compilação** guia, para **arquivos tooarchive**, digite `**/*` tooinclude todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="b5a12-157">In hello **Post-build Actions** tab, for **Files tooarchive**, enter `**/*` tooinclude all files.</span></span>

1. <span data-ttu-id="b5a12-158">Para **disparar versão no TFS/Team Services**, digite a URL completa Olá da sua conta (como `https://your-account-name.visualstudio.com`), Olá nome do projeto, um nome para a definição de versão de saudação (criada posteriormente), e Olá credenciais tooconnect tooyour conta.</span><span class="sxs-lookup"><span data-stu-id="b5a12-158">For **Trigger release in TFS/Team Services**, enter hello full URL of your account (such as `https://your-account-name.visualstudio.com`), hello project name, a name for hello release definition (created later), and hello credentials tooconnect tooyour account.</span></span>
   <span data-ttu-id="b5a12-159">É necessário o nome de usuário e a saudação PAT criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b5a12-159">You need your user name and hello PAT you created earlier.</span></span> 

   ![Configuração de ações pós-build do Jenkins](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="b5a12-161">Salve o projeto de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5a12-161">Save hello build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="b5a12-162">Criar um ponto de extremidade de serviço do Jenkins</span><span class="sxs-lookup"><span data-stu-id="b5a12-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="b5a12-163">Um ponto de extremidade de serviço permite Team Services tooconnect tooJenkins.</span><span class="sxs-lookup"><span data-stu-id="b5a12-163">A service endpoint allows Team Services tooconnect tooJenkins.</span></span>

1. <span data-ttu-id="b5a12-164">Olá abrir **serviços** página no Team Services, abra Olá **novo ponto de extremidade de serviço** lista e escolha **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="b5a12-164">Open hello **Services** page in Team Services, open hello **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![Adicionar um ponto de extremidade do Jenkins](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="b5a12-166">Insira um nome que você usará toorefer toothis conexão.</span><span class="sxs-lookup"><span data-stu-id="b5a12-166">Enter a name you will use toorefer toothis connection.</span></span>

1. <span data-ttu-id="b5a12-167">Insira a URL de saudação do servidor Jenkins e escala Olá **aceitar certificados não confiáveis do SSL** opção.</span><span class="sxs-lookup"><span data-stu-id="b5a12-167">Enter hello URL of your Jenkins server, and tick hello **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="b5a12-168">Digite hello nome de usuário e senha para sua conta Jenkins.</span><span class="sxs-lookup"><span data-stu-id="b5a12-168">Enter hello user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="b5a12-169">Escolha **verificar conexão** toocheck que Olá informação está correta.</span><span class="sxs-lookup"><span data-stu-id="b5a12-169">Choose **Verify connection** toocheck that hello information is correct.</span></span>

1. <span data-ttu-id="b5a12-170">Escolha **Okey** toocreate ponto de extremidade de serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5a12-170">Choose **OK** toocreate hello service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="b5a12-171">Criar um grupo de implantação</span><span class="sxs-lookup"><span data-stu-id="b5a12-171">Create a deployment group</span></span>

<span data-ttu-id="b5a12-172">É necessário um [o grupo de implantação](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) muito contêm máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5a12-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) too contain hello virtual machines.</span></span>

1. <span data-ttu-id="b5a12-173">Olá abrir **versões** guia da saudação **criar &amp; versão** hub, em seguida, abra Olá **grupos de implantação** guia e escolha **+ novo**.</span><span class="sxs-lookup"><span data-stu-id="b5a12-173">Open hello **Releases** tab of hello **Build &amp; Release** hub, then open hello **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="b5a12-174">Insira um nome para o grupo de implantação hello e uma descrição opcional.</span><span class="sxs-lookup"><span data-stu-id="b5a12-174">Enter a name for hello deployment group, and an optional description.</span></span>
   <span data-ttu-id="b5a12-175">Depois, escolha **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b5a12-175">Then choose **Create**.</span></span>

<span data-ttu-id="b5a12-176">tarefa de implantação de grupo de recursos do Azure Olá cria e registra VMs hello quando ele é executado usando o modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="b5a12-176">hello Azure Resource Group Deployment task creates and registers hello VMs when it runs using hello Azure Resource Manager template.</span></span>
<span data-ttu-id="b5a12-177">Você não precisa toocreate e registrar máquinas virtuais de saudação por conta própria.</span><span class="sxs-lookup"><span data-stu-id="b5a12-177">You don't need toocreate and register hello virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="b5a12-178">Criar uma definição de versão</span><span class="sxs-lookup"><span data-stu-id="b5a12-178">Create a release definition</span></span>

<span data-ttu-id="b5a12-179">Uma definição de versão Especifica que o processo de saudação do Team Services será executado toodeploy Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5a12-179">A release definition specifies hello process Team Services will execute toodeploy hello app.</span></span>
<span data-ttu-id="b5a12-180">definição de versão toocreate Olá no Team Services:</span><span class="sxs-lookup"><span data-stu-id="b5a12-180">toocreate hello release definition in Team Services:</span></span>

1. <span data-ttu-id="b5a12-181">Olá abrir **versões** guia da saudação **criar &amp; versão** hub, abra Olá  **+**  suspensa na lista de saudação de definições de versão e escolha Olá **criar definição de versão**.</span><span class="sxs-lookup"><span data-stu-id="b5a12-181">Open hello **Releases** tab of hello **Build &amp; Release** hub, open hello **+** drop-down in hello list of release definitions, and choose hello **Create release definition**.</span></span> 

1. <span data-ttu-id="b5a12-182">Selecione Olá **vazio** modelo e escolha **próximo**.</span><span class="sxs-lookup"><span data-stu-id="b5a12-182">Select hello **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="b5a12-183">Em Olá **artefatos** seção, clique em **vincular um artefato** e escolha **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="b5a12-183">In hello **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="b5a12-184">Selecione sua conexão de ponto de extremidade de serviço do Jenkins.</span><span class="sxs-lookup"><span data-stu-id="b5a12-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="b5a12-185">Em seguida, selecione o trabalho de origem Jenkins hello e escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="b5a12-185">Then select hello Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="b5a12-186">Em Olá nova definição de versão, escolha **+ adicionar tarefas** e adicione um **implantação de grupo de recursos do Azure** ambiente de padrão de toohello de tarefas.</span><span class="sxs-lookup"><span data-stu-id="b5a12-186">In hello new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task toohello default environment.</span></span>

1. <span data-ttu-id="b5a12-187">Escolha Olá suspensa toohello próxima seta **+ adicionar tarefas** link e adicionar uma definição de toohello de fase de grupo de implantação.</span><span class="sxs-lookup"><span data-stu-id="b5a12-187">Choose hello drop down arrow next toohello **+ Add tasks** link and add a deployment group phase toohello definition.</span></span>

   ![Adicionar uma fase de grupo de implantação](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="b5a12-189">No catálogo de tarefa hello, abra Olá **utilitário** seção e adicionar uma instância de saudação **Script do Shell** tarefa.</span><span class="sxs-lookup"><span data-stu-id="b5a12-189">In hello Task catalog, open hello **Utility** section and add an instance of hello **Shell Script** task.</span></span>

1. <span data-ttu-id="b5a12-190">modelo de parâmetros de saudação usado na tarefa de implantação de grupo de recursos do Azure Olá define Olá administrador senha usada tooconnect toohello VMs.</span><span class="sxs-lookup"><span data-stu-id="b5a12-190">hello parameters template used in hello Azure Resource Group Deployment task sets hello admin password used tooconnect toohello VMs.</span></span>
   <span data-ttu-id="b5a12-191">Fornecer essa senha com variável Olá **$(adminpassword)**:</span><span class="sxs-lookup"><span data-stu-id="b5a12-191">You provide this password with hello variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="b5a12-192">Olá abrir **variáveis** guia e, em Olá **variáveis** seção, insira o nome da saudação `adminpassword`.</span><span class="sxs-lookup"><span data-stu-id="b5a12-192">Open hello **Variables** tab and, in hello **Variables** section, enter hello name `adminpassword`.</span></span>

   - <span data-ttu-id="b5a12-193">Insira a senha de administrador de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5a12-193">Enter hello administrator password.</span></span>

   - <span data-ttu-id="b5a12-194">Escolha hello "cadeado" ícone próximo toohello valor textbox tooprotect Olá senha.</span><span class="sxs-lookup"><span data-stu-id="b5a12-194">Choose hello "padlock" icon next toohello value textbox tooprotect hello password.</span></span> 

## <a name="configure-hello-azure-resource-group-deployment-task"></a><span data-ttu-id="b5a12-195">Configurar tarefas de implantação de grupo de recursos do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="b5a12-195">Configure hello Azure Resource Group Deployment task</span></span>

<span data-ttu-id="b5a12-196">Olá **implantação de grupo de recursos do Azure** tarefa é o grupo de implantação de saudação toocreate usado.</span><span class="sxs-lookup"><span data-stu-id="b5a12-196">hello **Azure Resource Group Deployment** task is used toocreate hello deployment group.</span></span> <span data-ttu-id="b5a12-197">Configure-o da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b5a12-197">Configure it as follows:</span></span>

* <span data-ttu-id="b5a12-198">**Assinatura do Azure:** selecione uma conexão na lista de saudação em **conexões de serviço do Azure disponíveis**.</span><span class="sxs-lookup"><span data-stu-id="b5a12-198">**Azure Subscription:** Select a connection from hello list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="b5a12-199">Se nenhuma conexão aparecer, escolha **gerenciar**, selecione **novo ponto de extremidade de serviço** , em seguida, **do Azure Resource Manager**e siga os prompts de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5a12-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow hello prompts.</span></span>
  <span data-ttu-id="b5a12-200">Retornar tooyour versão definição, Olá atualização **AzureRM assinatura** lista e conexão Olá selecione que você criou.</span><span class="sxs-lookup"><span data-stu-id="b5a12-200">Return tooyour release definition, refresh hello **AzureRM Subscription** list, and select hello connection you created.</span></span>

* <span data-ttu-id="b5a12-201">**Grupo de recursos**: insira um nome de grupo de recursos de saudação criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b5a12-201">**Resource group**: Enter a name of hello resource group you created earlier.</span></span>

* <span data-ttu-id="b5a12-202">**Local**: selecione uma região para a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5a12-202">**Location**: Select a region for hello deployment.</span></span>

  ![Criar um novo grupo de recursos](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="b5a12-204">**Local do modelo**: `URL of hello file`</span><span class="sxs-lookup"><span data-stu-id="b5a12-204">**Template location**: `URL of hello file`</span></span>

* <span data-ttu-id="b5a12-205">**Link do modelo**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span><span class="sxs-lookup"><span data-stu-id="b5a12-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="b5a12-206">**Link de parâmetros de modelo**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span><span class="sxs-lookup"><span data-stu-id="b5a12-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="b5a12-207">**Substituir parâmetros de modelo**: uma lista de saudação substituem os valores, por exemplo: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span><span class="sxs-lookup"><span data-stu-id="b5a12-207">**Override template parameters**: A list of hello override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="b5a12-208">Insira seus próprios valores específicos de Olá {espaços reservados}.</span><span class="sxs-lookup"><span data-stu-id="b5a12-208">Insert your own specific values for hello {placeholders}.</span></span> 

* <span data-ttu-id="b5a12-209">**Habilitar os pré-requisitos**: `Configure with Deployment Group agent`</span><span class="sxs-lookup"><span data-stu-id="b5a12-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="b5a12-210">**Ponto de extremidade do TFS para o VSTS**: escolha **adicionar** e, no diálogo "Adicionar novo Team Foundation Server/Team Services Conexão" Olá, selecione **Token de autenticação com base em**.</span><span class="sxs-lookup"><span data-stu-id="b5a12-210">**TFS/VSTS endpoint**: Choose **Add** and, in hello "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="b5a12-211">Insira um nome de conexão hello e URL de saudação do seu projeto de equipe.</span><span class="sxs-lookup"><span data-stu-id="b5a12-211">Enter a name of hello connection and hello URL of your team project.</span></span> <span data-ttu-id="b5a12-212">Em seguida, gerar e insira um [Token de acesso pessoal (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) o projeto de equipe do tooauthenticate Olá conexão tooyour.</span><span class="sxs-lookup"><span data-stu-id="b5a12-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello connection tooyour team project.</span></span>

  ![Criar um token de acesso pessoal](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="b5a12-214">**Projeto de equipe**: selecione o projeto atual.</span><span class="sxs-lookup"><span data-stu-id="b5a12-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="b5a12-215">**Grupo de implantação**: insira Olá o mesmo nome de grupo de implantação que você usou para Olá **grupo de recursos** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b5a12-215">**Deployment Group**: Enter hello same deployment group name as you used for hello **Resource group** parameter.</span></span>

<span data-ttu-id="b5a12-216">as configurações padrão de saudação para tarefas de implantação de grupo de recursos do Azure Olá são toocreate ou atualizar um recurso e toodo assim incrementalmente.</span><span class="sxs-lookup"><span data-stu-id="b5a12-216">hello default settings for hello Azure Resource Group Deployment task are toocreate or update a resource, and toodo so incrementally.</span></span> <span data-ttu-id="b5a12-217">tarefa de saudação cria Olá VMs Olá primeira vez que ele é executado e subsequentemente apenas atualizá-los.</span><span class="sxs-lookup"><span data-stu-id="b5a12-217">hello task creates hello VMs hello first time it runs, and subsequently just update them.</span></span>

## <a name="configure-hello-shell-script-task"></a><span data-ttu-id="b5a12-218">Configurar a tarefa de Script do Shell Olá</span><span class="sxs-lookup"><span data-stu-id="b5a12-218">Configure hello Shell Script task</span></span>

<span data-ttu-id="b5a12-219">Olá **Script do Shell** tarefa é uma configuração de saudação do tooprovide usado para toorun um script no aplicativo de saudação cada servidor tooinstall Node. js e iniciar.</span><span class="sxs-lookup"><span data-stu-id="b5a12-219">hello **Shell Script** task is used tooprovide hello configuration for a script toorun on each server tooinstall Node.js and start hello app.</span></span> <span data-ttu-id="b5a12-220">Configure-o da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b5a12-220">Configure it as follows:</span></span>

* <span data-ttu-id="b5a12-221">**Caminho do Script**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span><span class="sxs-lookup"><span data-stu-id="b5a12-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="b5a12-222">**Especificar Diretório de Trabalho**: `Checked`</span><span class="sxs-lookup"><span data-stu-id="b5a12-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="b5a12-223">**Diretório de Trabalho**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span><span class="sxs-lookup"><span data-stu-id="b5a12-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-hello-release-definition"></a><span data-ttu-id="b5a12-224">Renomear e salvar a definição de versão Olá</span><span class="sxs-lookup"><span data-stu-id="b5a12-224">Rename and save hello release definition</span></span>

1. <span data-ttu-id="b5a12-225">Editar nome Olá Olá versão toohello nome de definição de especificado no **ações de pós-compilação** guia de compilação Olá Jenkins.</span><span class="sxs-lookup"><span data-stu-id="b5a12-225">Edit hello name of hello release definition toohello name you specified in the **Post-build Actions** tab of hello build in Jenkins.</span></span> <span data-ttu-id="b5a12-226">Jenkins requer esse nome toobe capaz de tootrigger uma nova versão quando artefatos de origem Olá são atualizados.</span><span class="sxs-lookup"><span data-stu-id="b5a12-226">Jenkins requires this name toobe able tootrigger a new release when hello source artifacts are updated.</span></span>

1. <span data-ttu-id="b5a12-227">Opcionalmente, altere o nome de saudação do ambiente Olá clicando no nome da saudação.</span><span class="sxs-lookup"><span data-stu-id="b5a12-227">Optionally, change hello name of hello environment by clicking on hello name.</span></span> 

1. <span data-ttu-id="b5a12-228">Escolha **Salvar** e depois **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5a12-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="b5a12-229">Iniciar uma implantação manual</span><span class="sxs-lookup"><span data-stu-id="b5a12-229">Start a manual deployment</span></span>

1. <span data-ttu-id="b5a12-230">Escolha **+ Versão** e selecione **Criar Versão**.</span><span class="sxs-lookup"><span data-stu-id="b5a12-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="b5a12-231">Selecione a compilação Olá é concluída na lista suspensa da realçado hello e escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="b5a12-231">Select hello build you completed in hello highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="b5a12-232">Escolha o link de versão de saudação na mensagem de saudação do pop-up.</span><span class="sxs-lookup"><span data-stu-id="b5a12-232">Choose hello release link in hello popup message.</span></span> <span data-ttu-id="b5a12-233">Por exemplo: "A versão **Release-1** foi criada".</span><span class="sxs-lookup"><span data-stu-id="b5a12-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="b5a12-234">Olá abrir **Logs** guia saída de console toowatch hello versão.</span><span class="sxs-lookup"><span data-stu-id="b5a12-234">Open hello **Logs** tab toowatch hello release console output.</span></span>

1. <span data-ttu-id="b5a12-235">No navegador, abra Olá URL de um dos servidores de saudação você adicionou o grupo de implantação tooyour.</span><span class="sxs-lookup"><span data-stu-id="b5a12-235">In your browser, open hello URL of one of hello servers you added tooyour deployment group.</span></span> <span data-ttu-id="b5a12-236">Por exemplo, insira: `http://{your-server-ip-address}`</span><span class="sxs-lookup"><span data-stu-id="b5a12-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="b5a12-237">Iniciar uma implantação de CI/CD</span><span class="sxs-lookup"><span data-stu-id="b5a12-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="b5a12-238">Em Olá versão definição, desmarque Olá **habilitado** caixa de seleção no hello **opções de controle** seção de configurações de saudação para tarefas de implantação de grupo de recursos do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b5a12-238">In hello release definition, uncheck hello **Enabled** checkbox in hello **Control Options** section of hello settings for hello Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="b5a12-239">Para o grupo de implantação existente toohello de implantações futuras, você não precisa toore-executar essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="b5a12-239">For future deployments toohello existing deployment group, you do not need toore-execute this task.</span></span>

1. <span data-ttu-id="b5a12-240">Vá toohello repositório do Git de origem e modificar o conteúdo de saudação do hello **h1** no arquivo hello [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span><span class="sxs-lookup"><span data-stu-id="b5a12-240">Go toohello source Git repository and modify hello contents of hello **h1** heading in hello file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="b5a12-241">Confirme a alteração.</span><span class="sxs-lookup"><span data-stu-id="b5a12-241">Commit your change.</span></span>

1. <span data-ttu-id="b5a12-242">Depois de alguns minutos, você verá uma nova versão criada no hello **versões** página do Team Services ou o TFS.</span><span class="sxs-lookup"><span data-stu-id="b5a12-242">After a few minutes, you will see a new release created in hello **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="b5a12-243">Abra a implantação de Olá Olá versão toosee ocorrendo.</span><span class="sxs-lookup"><span data-stu-id="b5a12-243">Open hello release toosee hello deployment taking place.</span></span> <span data-ttu-id="b5a12-244">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="b5a12-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5a12-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b5a12-245">Next Steps</span></span>

<span data-ttu-id="b5a12-246">Neste tutorial, você Olá a implantação automatizada de um tooAzure de aplicativo usando compilação Jenkins e Team Services para versão.</span><span class="sxs-lookup"><span data-stu-id="b5a12-246">In this tutorial, you automated hello deployment of an app tooAzure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="b5a12-247">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="b5a12-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b5a12-248">Compilar seu aplicativo no Jenkins</span><span class="sxs-lookup"><span data-stu-id="b5a12-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="b5a12-249">Configurar o Jenkins para integração com o Team Services</span><span class="sxs-lookup"><span data-stu-id="b5a12-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="b5a12-250">Criar um grupo de implantação para Olá máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="b5a12-250">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="b5a12-251">Criar uma definição de lançamento que configura Olá VMs e implanta o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="b5a12-251">Create a release definition that configures hello VMs and deploys hello app</span></span>

<span data-ttu-id="b5a12-252">Mais informações sobre como toodeploy uma LÂMPADA (Linux, Apache, MySQL e PHP) de pilha avança toohello toolearn de tutorial Avançar.</span><span class="sxs-lookup"><span data-stu-id="b5a12-252">Advance toohello next tutorial toolearn more about how toodeploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b5a12-253">Implantar a pilha LAMP</span><span class="sxs-lookup"><span data-stu-id="b5a12-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)