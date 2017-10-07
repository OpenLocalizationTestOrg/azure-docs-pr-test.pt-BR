---
title: "aaaContinuous tooAzure de implantação do serviço de aplicativo | Microsoft Docs"
description: "Saiba como tooenable tooAzure de implantação contínua do serviço de aplicativo."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a><span data-ttu-id="08229-103">TooAzure de implantação contínua do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="08229-103">Continuous Deployment tooAzure App Service</span></span>
<span data-ttu-id="08229-104">Este tutorial mostra como tooconfigure um fluxo de trabalho de implantação contínua para seu [do serviço de aplicativo do Azure] aplicativo.</span><span class="sxs-lookup"><span data-stu-id="08229-104">This tutorial shows you how tooconfigure a continuous deployment workflow for your [Azure App Service] app.</span></span> <span data-ttu-id="08229-105">Integração com o serviço de aplicativo com BitBucket, GitHub, e [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) habilita um contínua fluxo de trabalho de implantação onde Azure recebe atualizações mais recentes de saudação do seu projeto publicado tooone desses serviços.</span><span class="sxs-lookup"><span data-stu-id="08229-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in hello most recent updates from your project published tooone of these services.</span></span> <span data-ttu-id="08229-106">A implantação contínua é uma ótima opção para projetos nos quais várias contribuições frequentes são integradas.</span><span class="sxs-lookup"><span data-stu-id="08229-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span>

<span data-ttu-id="08229-107">toofind-out como a implantação contínua tooconfigure manualmente a partir de um repositório de nuvem não listada Olá Portal do Azure (como [GitLab](https://gitlab.com/)), consulte [Configurando implantação contínua usando as etapas manuais](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span><span class="sxs-lookup"><span data-stu-id="08229-107">toofind out how tooconfigure continuous deployment manually from a cloud repository not listed by hello Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <span data-ttu-id="08229-108"><a name="overview"></a>Habilitar a implantação contínua</span><span class="sxs-lookup"><span data-stu-id="08229-108"><a name="overview"></a>Enable continuous deployment</span></span>
<span data-ttu-id="08229-109">implantação contínua de tooenable,</span><span class="sxs-lookup"><span data-stu-id="08229-109">tooenable continuous deployment,</span></span>

1. <span data-ttu-id="08229-110">Publica o repositório de conteúdo toohello do aplicativo que será usado para implantação contínua.</span><span class="sxs-lookup"><span data-stu-id="08229-110">Publish your app content toohello repository that will be used for continuous deployment.</span></span>  
    <span data-ttu-id="08229-111">Para obter mais informações sobre a publicação de seus serviços de toothese de projeto, consulte [criar um repositório (GitHub)], [criar um repositório (BitBucket)], e [Introdução ao VSTS].</span><span class="sxs-lookup"><span data-stu-id="08229-111">For more information on publishing your project toothese services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span></span>
2. <span data-ttu-id="08229-112">Na folha de menu do aplicativo no hello [portal do Azure], clique em **implantação de aplicativos > Opções de implantação**.</span><span class="sxs-lookup"><span data-stu-id="08229-112">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="08229-113">Clique em **Escolher fonte**, em seguida, selecione origem de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="08229-113">Click **Choose Source**, then select hello deployment source.</span></span>  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > <span data-ttu-id="08229-114">tooconfigure uma conta do VSTS para implantação de serviço de aplicativo, consulte este [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span><span class="sxs-lookup"><span data-stu-id="08229-114">tooconfigure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>
   > 
   > 
3. <span data-ttu-id="08229-115">Concluir o fluxo de trabalho de autorização de saudação.</span><span class="sxs-lookup"><span data-stu-id="08229-115">Complete hello authorization workflow.</span></span>
4. <span data-ttu-id="08229-116">Em Olá **origem de implantação** folha, escolha o projeto hello e branch toodeploy do.</span><span class="sxs-lookup"><span data-stu-id="08229-116">In hello **Deployment source** blade, choose hello project and branch toodeploy from.</span></span> <span data-ttu-id="08229-117">Quando terminar, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="08229-117">When you're done, click **OK**.</span></span>
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > <span data-ttu-id="08229-118">Ao habilitar a implantação contínua com GitHub ou BitBucket, os projetos públicos e privados serão exibidos.</span><span class="sxs-lookup"><span data-stu-id="08229-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span></span>
   > 
   > 
   
    <span data-ttu-id="08229-119">Serviço de aplicativo cria uma associação com o repositório selecionado hello, extrai nos arquivos de saudação do branch de saudação especificado e mantém um clone do repositório para seu aplicativo de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="08229-119">App Service creates an association with hello selected repository, pulls in hello files from hello specified branch, and maintains a clone of your repository for your App Service app.</span></span> <span data-ttu-id="08229-120">Quando você configurar uma implantação contínua de saudação do portal Azure VSTS, integração Olá usa saudação do serviço de aplicativo [mecanismo de implantação do Kudu](https://github.com/projectkudu/kudu/wiki), que já automatiza tarefas de compilação e implantação com cada `git push`.</span><span class="sxs-lookup"><span data-stu-id="08229-120">When you configure VSTS continuous deployment from hello Azure portal, hello integration uses hello App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span></span> <span data-ttu-id="08229-121">Você não precisa tooseparately configurar implantação contínua no VSTS.</span><span class="sxs-lookup"><span data-stu-id="08229-121">You do not need tooseparately set up continuous deployment in VSTS.</span></span> <span data-ttu-id="08229-122">Depois que esse processo for concluído, hello **opções de implantação** folha aplicativo mostrará uma implantação ativa que indica a implantação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="08229-122">After this process completes, hello **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span></span>
5. <span data-ttu-id="08229-123">tooverify Olá aplicativo é implantado com êxito, clique em Olá **URL** na parte superior de saudação da folha de saudação do aplicativo no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="08229-123">tooverify hello app is successfully deployed, click hello **URL** at hello top of hello app's blade in hello Azure portal.</span></span>
6. <span data-ttu-id="08229-124">tooverify implantação contínua está ocorrendo no repositório de saudação de sua escolha, enviar por push a um repositório de toohello de alteração.</span><span class="sxs-lookup"><span data-stu-id="08229-124">tooverify that continuous deployment is occurring from hello repository of your choice, push a change toohello repository.</span></span> <span data-ttu-id="08229-125">Seu aplicativo deve atualizar as alterações de saudação tooreflect logo após a conclusão do repositório de toohello push hello.</span><span class="sxs-lookup"><span data-stu-id="08229-125">Your app should update tooreflect hello changes shortly after hello push toohello repository completes.</span></span> <span data-ttu-id="08229-126">Você pode verificar que ter recebido atualização Olá Olá **opções de implantação** folha do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="08229-126">You can verify that it has pulled in hello update in hello **Deployment options** blade of your app.</span></span>

## <span data-ttu-id="08229-127"><a name="VSsolution"></a>Implantação contínua de uma solução do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="08229-127"><a name="VSsolution"></a>Continuous deployment of a Visual Studio solution</span></span>
<span data-ttu-id="08229-128">Enviar um tooAzure de solução do Visual Studio do serviço de aplicativo é tão fácil quanto enviar um arquivo simples index. HTML.</span><span class="sxs-lookup"><span data-stu-id="08229-128">Pushing a Visual Studio solution tooAzure App Service is just as easy as pushing a simple index.html file.</span></span> <span data-ttu-id="08229-129">Olá processo de implantação do serviço de aplicativo simplifica a todos os detalhes de hello, incluindo restauração dependências do NuGet e compilar os binários do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="08229-129">hello App Service deployment process streamlines all hello details, including restoring NuGet dependencies and building hello application binaries.</span></span> <span data-ttu-id="08229-130">Você pode siga as práticas recomendadas de controle do código-fonte de saudação de manter o código apenas em seu repositório Git e permitem que a implantação do serviço de aplicativo cuidar do rest hello.</span><span class="sxs-lookup"><span data-stu-id="08229-130">You can follow hello source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of hello rest.</span></span>

<span data-ttu-id="08229-131">Olá etapas para enviar por push o tooApp de solução do Visual Studio são Olá mesmo como Olá [seção anterior](#overview), desde que você configure sua solução e o repositório da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="08229-131">hello steps for pushing your Visual Studio solution tooApp Service are hello same as in hello [previous section](#overview), provided that you configure your solution and repository as follows:</span></span>

* <span data-ttu-id="08229-132">Use Olá Visual Studio fonte controle opção toogenerate um `.gitignore` arquivo como imagem de saudação abaixo ou adicione manualmente um `.gitignore` arquivo na raiz do repositório com conteúdo toothis semelhante [. gitignore exemplo](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="08229-132">Use hello Visual Studio source control option toogenerate a `.gitignore` file such as hello image below or manually add a `.gitignore` file in your repository root with content similar toothis [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* <span data-ttu-id="08229-133">Adicione repositório de tooyour árvore do diretório da solução inteira Olá, com o arquivo hello na raiz do repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="08229-133">Add hello entire solution's directory tree tooyour repository, with hello .sln file in hello repository root.</span></span>

<span data-ttu-id="08229-134">Depois de configurar o repositório conforme descrito e configurado o seu aplicativo no Azure para a publicação contínua de um dos repositórios Git on-line de saudação, você pode desenvolver seu aplicativo ASP.NET localmente no Visual Studio e continuamente implantar seu código simplesmente por Enviar por push o repositório do Git alterações tooyour on-line.</span><span class="sxs-lookup"><span data-stu-id="08229-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of hello online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes tooyour online Git repository.</span></span>

## <span data-ttu-id="08229-135"><a name="disableCD"></a>Desabilitar a implantação contínua</span><span class="sxs-lookup"><span data-stu-id="08229-135"><a name="disableCD"></a>Disable continuous deployment</span></span>
<span data-ttu-id="08229-136">implantação contínua de toodisable,</span><span class="sxs-lookup"><span data-stu-id="08229-136">toodisable continuous deployment,</span></span>

1. <span data-ttu-id="08229-137">Na folha de menu do aplicativo no hello [portal do Azure], clique em **implantação de aplicativos > Opções de implantação**.</span><span class="sxs-lookup"><span data-stu-id="08229-137">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="08229-138">Em seguida, clique em **Disconnect** em Olá **opções de implantação** folha.</span><span class="sxs-lookup"><span data-stu-id="08229-138">Then click **Disconnect** in hello **Deployment options** blade.</span></span>
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. <span data-ttu-id="08229-139">Depois de responder **Sim** toohello mensagem de confirmação, você pode retornar a folha de tooyour do aplicativo e clique em **implantação de aplicativos > Opções de implantação** se você gostaria que tooset a publicação de outra origem.</span><span class="sxs-lookup"><span data-stu-id="08229-139">After answering **Yes** toohello confirmation message, you can return tooyour app's blade and click **APP DEPLOYMENT > Deployment options** if you would like tooset up publishing from another source.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="08229-140">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="08229-140">Additional Resources</span></span>
* [<span data-ttu-id="08229-141">Como tooinvestigate comum problemas com implantação contínua</span><span class="sxs-lookup"><span data-stu-id="08229-141">How tooinvestigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="08229-142">[Como toouse PowerShell do Azure]</span><span class="sxs-lookup"><span data-stu-id="08229-142">[How toouse PowerShell for Azure]</span></span>
* <span data-ttu-id="08229-143">[Como toouse Olá ferramentas de linha de comando do Azure para Mac e Linux]</span><span class="sxs-lookup"><span data-stu-id="08229-143">[How toouse hello Azure Command-Line Tools for Mac and Linux]</span></span>
* <span data-ttu-id="08229-144">[Documentação do Git]</span><span class="sxs-lookup"><span data-stu-id="08229-144">[Git documentation]</span></span>
* [<span data-ttu-id="08229-145">Kudu do Projeto</span><span class="sxs-lookup"><span data-stu-id="08229-145">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="08229-146">Usar o Azure tooautomatically gerar um aplicativo do CI/CD pipeline toodeploy um ASP.NET 4</span><span class="sxs-lookup"><span data-stu-id="08229-146">Use Azure tooautomatically generate a CI/CD pipeline toodeploy an ASP.NET 4 app</span></span>](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> <span data-ttu-id="08229-147">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="08229-147">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="08229-148">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="08229-148">No credit cards required; no commitments.</span></span>
> 
> 

[do serviço de aplicativo do Azure]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[portal do Azure]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Como toouse PowerShell do Azure]: /powershell/azureps-cmdlets-docs
[Como toouse Olá ferramentas de linha de comando do Azure para Mac e Linux]:../cli-install-nodejs.md
[Documentação do Git]: http://git-scm.com/documentation

[criar um repositório (GitHub)]: https://help.github.com/articles/create-a-repo
[criar um repositório (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[Introdução ao VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview
