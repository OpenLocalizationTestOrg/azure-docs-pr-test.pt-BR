---
title: entrega de aaaContinuous com Git e do Visual Studio Team Services no Azure | Microsoft Docs
description: "Saiba como tooconfigure o Visual Studio Team Services projetos da equipe toouse Git tooautomatically criar e implantar o recurso de aplicativo Web toohello nos serviços de nuvem ou do serviço de aplicativo do Azure."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="897ae-103">Fornecimento contínuo tooAzure usando o Visual Studio Team Services e o Git</span><span class="sxs-lookup"><span data-stu-id="897ae-103">Continuous delivery tooAzure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="897ae-104">Você pode usar toohost de projetos de equipe do Visual Studio Team Services um repositório Git para seu código-fonte e automaticamente criar e implantar aplicativos da web de tooAzure ou serviços em nuvem sempre que você enviar por push a um repositório de toohello de confirmação.</span><span class="sxs-lookup"><span data-stu-id="897ae-104">You can use Visual Studio Team Services team projects toohost a Git repository for your source code, and automatically build and deploy tooAzure web apps or cloud services whenever you push a commit toohello repository.</span></span>

<span data-ttu-id="897ae-105">Você precisará Visual Studio 2013 e hello SDK do Azure instalado.</span><span class="sxs-lookup"><span data-stu-id="897ae-105">You'll need Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="897ae-106">Se você ainda não tiver o Visual Studio 2013, baixá-lo escolhendo Olá **comece gratuitamente** link [www.visualstudio.com](http://www.visualstudio.com). Instalar Olá SDK do Azure na [aqui](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="897ae-106">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="897ae-107">É necessário um toocomplete de conta do Visual Studio Team Services este tutorial: você pode [abrir uma conta do Visual Studio Team Services gratuitamente](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="897ae-107">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="897ae-108">tooset a um tooautomatically de serviço de nuvem compilar e implantar tooAzure usando o Visual Studio Team Services, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="897ae-108">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="897ae-109">1: Criar um repositório Git</span><span class="sxs-lookup"><span data-stu-id="897ae-109">1: Create a Git repository</span></span>
1. <span data-ttu-id="897ae-110">Se você ainda não tiver uma conta do Visual Studio Team Services, pode obter uma [aqui](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="897ae-110">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="897ae-111">Quando criar seu projeto da equipe, escolha o Git como seu sistema de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="897ae-111">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="897ae-112">Execute o projeto de equipe de tooyour Olá instruções tooconnect Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="897ae-112">Follow hello instructions tooconnect Visual Studio tooyour team project.</span></span>
2. <span data-ttu-id="897ae-113">Em **Team Explorer**, escolha Olá **a clonagem deste repositório** link.</span><span class="sxs-lookup"><span data-stu-id="897ae-113">In **Team Explorer**, choose hello **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="897ae-114">Especificar local de saudação da cópia local do hello e escolha Olá **Clone** botão.</span><span class="sxs-lookup"><span data-stu-id="897ae-114">Specify hello location of hello local copy and then choose hello **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a><span data-ttu-id="897ae-115">2: criar um projeto e confirmá-la toohello repositório</span><span class="sxs-lookup"><span data-stu-id="897ae-115">2: Create a project and commit it toohello repository</span></span>
1. <span data-ttu-id="897ae-116">Em **Team Explorer**, em Olá **soluções** , escolha Olá **novo** link toocreate um novo projeto no repositório local hello.</span><span class="sxs-lookup"><span data-stu-id="897ae-116">In **Team Explorer**, in hello **Solutions** section, choose hello **New** link toocreate a new project in hello local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="897ae-117">Você pode implantar um aplicativo web ou um serviço de nuvem (aplicativo do Azure) pelo Olá seguir as etapas neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="897ae-117">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span> <span data-ttu-id="897ae-118">Crie um novo projeto de Serviço de Nuvem do Azure ou um novo projeto ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="897ae-118">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="897ae-119">Certifique-se de destinos do projeto Olá Olá .NET Framework 4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="897ae-119">Make sure that hello project targets hello .NET Framework 4 or later.</span></span> <span data-ttu-id="897ae-120">Se você está criando um projeto de serviço de nuvem, adicione uma função de trabalho e uma função web MVC do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="897ae-120">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="897ae-121">Se você quiser toocreate um aplicativo web, escolha Olá **aplicativo Web ASP.NET** modelo de projeto e escolha **MVC**.</span><span class="sxs-lookup"><span data-stu-id="897ae-121">If you want toocreate a web app, choose hello **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="897ae-122">Consulte [Criar um aplicativo web ASP.NET no Serviço de Aplicativo do Azure](../app-service-web/app-service-web-get-started-dotnet.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="897ae-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="897ae-123">Abra Olá menu de atalho Olá solução e escolha **confirmar**.</span><span class="sxs-lookup"><span data-stu-id="897ae-123">Open hello shortcut menu for hello solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="897ae-124">Se esse for Olá pela primeira vez que você usou o Git no Visual Studio Team Services, você precisará tooprovide tooidentify algumas informações por conta própria no Git.</span><span class="sxs-lookup"><span data-stu-id="897ae-124">If this is hello first time you've used Git in Visual Studio Team Services, you'll need tooprovide some information tooidentify yourself in Git.</span></span> <span data-ttu-id="897ae-125">Em Olá **alterações pendentes** área de **Team Explorer**, insira seu nome de usuário e endereço de email.</span><span class="sxs-lookup"><span data-stu-id="897ae-125">In hello **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="897ae-126">Digite um comentário para confirmação hello e escolha Olá **confirmação** botão.</span><span class="sxs-lookup"><span data-stu-id="897ae-126">Enter a comment for hello commit and then choose hello **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="897ae-127">Observação: Olá opções tooinclude ou excluir alterações específicas ao fazer check-in.</span><span class="sxs-lookup"><span data-stu-id="897ae-127">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="897ae-128">Se Olá alterações que você deseja são excluídos, escolha **incluir tudo**.</span><span class="sxs-lookup"><span data-stu-id="897ae-128">If hello changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="897ae-129">Você tem agora Olá confirmada alterações em sua cópia local do repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="897ae-129">You've now committed hello changes in your local copy of hello repository.</span></span> <span data-ttu-id="897ae-130">Em seguida, sincronizar as alterações com o servidor de saudação escolhendo Olá **sincronização** link.</span><span class="sxs-lookup"><span data-stu-id="897ae-130">Next, sync those changes with hello server by choosing hello **Sync** link.</span></span>

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="897ae-131">3: conectar Olá projeto tooAzure</span><span class="sxs-lookup"><span data-stu-id="897ae-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="897ae-132">Agora que você tem um repositório Git no Visual Studio Team Services com um código de origem nele, você está pronto tooconnect seu tooAzure de repositório do git.</span><span class="sxs-lookup"><span data-stu-id="897ae-132">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready tooconnect your git repository tooAzure.</span></span>  <span data-ttu-id="897ae-133">Em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), selecione o aplicativo web ou serviço de nuvem ou crie um novo escolhendo o ícone na esquerda inferior hello e escolhendo + Olá **serviço de nuvem** ou **aplicativo Web**e **criação rápida**.</span><span class="sxs-lookup"><span data-stu-id="897ae-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello + icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="897ae-134">Para serviços de nuvem, escolha Olá **configurar a publicação com o Visual Studio Team Services** link.</span><span class="sxs-lookup"><span data-stu-id="897ae-134">For cloud services, choose hello **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="897ae-135">Para aplicativos da web, escolha Olá **configurar a implantação do controle de origem** link.</span><span class="sxs-lookup"><span data-stu-id="897ae-135">For web apps, choose hello **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="897ae-136">No Assistente de saudação, digite o nome de saudação da sua conta do Visual Studio Team Services na caixa de texto de saudação e escolha Olá **autorizar agora** link.</span><span class="sxs-lookup"><span data-stu-id="897ae-136">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and choose hello **Authorize Now** link.</span></span> <span data-ttu-id="897ae-137">Você pode ser solicitado toosign no.</span><span class="sxs-lookup"><span data-stu-id="897ae-137">You might be asked toosign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="897ae-138">Em Olá **solicitação de Conexão** caixa de diálogo pop-up, escolha **aceitar** tooauthorize tooconfigure do Azure que sua equipe de projeto no Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="897ae-138">In hello **Connection Request** pop-up dialog, choose **Accept** tooauthorize Azure tooconfigure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="897ae-139">Depois que a autorização obtiver êxito, você verá uma lista suspensa que contém os projetos de equipe do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="897ae-139">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="897ae-140">Selecione Olá nome de projeto de equipe que você criou nas etapas anteriores hello e escolha o botão de marca de seleção do Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="897ae-140">Select hello name of team project that you created in hello previous steps, and choose hello wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="897ae-141">Olá próxima vez que você enviar por push a um repositório de tooyour confirmação, o Visual Studio Team Services criará e implantará tooAzure seu projeto.</span><span class="sxs-lookup"><span data-stu-id="897ae-141">hello next time you push a commit tooyour repository, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="897ae-142">4: Disparar uma recompilação e reimplantar seu projeto</span><span class="sxs-lookup"><span data-stu-id="897ae-142">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="897ae-143">No Visual Studio, abra um arquivo e altere-o.</span><span class="sxs-lookup"><span data-stu-id="897ae-143">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="897ae-144">Por exemplo, altere o arquivo hello `_Layout.cshtml` em modos de exibição de saudação\\pasta compartilhada em uma função da web MVC.</span><span class="sxs-lookup"><span data-stu-id="897ae-144">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="897ae-145">Editar texto de rodapé Olá para o site de saudação e salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="897ae-145">Edit hello footer text for hello site and save hello file.</span></span>
   
    ![][18]
3. <span data-ttu-id="897ae-146">Em **Solution Explorer**, abra o menu de atalho de Olá Olá Olá, nó de projeto ou nó da solução arquivo você alterado e, em seguida, escolha **confirmar**.</span><span class="sxs-lookup"><span data-stu-id="897ae-146">In **Solution Explorer**, open hello shortcut menu for hello solution node, project node, or hello file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="897ae-147">Digite um comentário e escolha **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="897ae-147">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="897ae-148">Escolha Olá **sincronização** link.</span><span class="sxs-lookup"><span data-stu-id="897ae-148">Choose hello **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="897ae-149">Escolha Olá **Push** link toopush seu repositório de toohello de confirmação no Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="897ae-149">Choose hello **Push** link toopush your commit toohello repository in Visual Studio Team Services.</span></span> <span data-ttu-id="897ae-150">(Você também pode usar o hello **sincronização** botão toocopy seu repositório de toohello confirmações.</span><span class="sxs-lookup"><span data-stu-id="897ae-150">(You can also use hello **Sync** button toocopy your commits toohello repository.</span></span> <span data-ttu-id="897ae-151">Olá diferença é que **sincronização** também recebe Olá últimas alterações no repositório de hello.)</span><span class="sxs-lookup"><span data-stu-id="897ae-151">hello difference is that **Sync** also pulls hello latest changes from hello repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="897ae-152">Escolha Olá **inicial** botão tooreturn toohello **Team Explorer** página inicial.</span><span class="sxs-lookup"><span data-stu-id="897ae-152">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="897ae-153">Escolha **cria** tooview Olá compilações em andamento.</span><span class="sxs-lookup"><span data-stu-id="897ae-153">Choose **Builds** tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="897ae-154">**Team Explorer** mostra que uma compilação foi disparada para seu check-in.</span><span class="sxs-lookup"><span data-stu-id="897ae-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="897ae-155">tooview um log detalhado Olá compilação em andamento, clique duas vezes no nome Olá Olá compilação em andamento.</span><span class="sxs-lookup"><span data-stu-id="897ae-155">tooview a detailed log as hello build progresses, double-click hello name of hello build in progress.</span></span>
10. <span data-ttu-id="897ae-156">Enquanto a compilação de saudação está em andamento, dê uma olhada na definição de compilação de saudação que foi criada quando você usou Olá Assistente toolink tooAzure.</span><span class="sxs-lookup"><span data-stu-id="897ae-156">While hello build is in-progress, take a look at hello build definition that was created when you used hello wizard toolink tooAzure.</span></span>  <span data-ttu-id="897ae-157">Abra o menu de atalho Olá Olá para definição de compilação e escolha **editar definição de compilação**.</span><span class="sxs-lookup"><span data-stu-id="897ae-157">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="897ae-158">Em Olá **gatilho** guia, você verá que definição de compilação de saudação é definida toobuild em cada check-in, por padrão.</span><span class="sxs-lookup"><span data-stu-id="897ae-158">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in, by default.</span></span> <span data-ttu-id="897ae-159">(Para um serviço de nuvem do Visual Studio Team Services cria e implanta Olá ramificação mestre toohello automaticamente o ambiente de preparo.</span><span class="sxs-lookup"><span data-stu-id="897ae-159">(For a cloud service, Visual Studio Team Services builds and deploys hello master branch toohello staging environment automatically.</span></span> <span data-ttu-id="897ae-160">Você ainda terá toodo site ao vivo do toodeploy toohello uma etapa manual.</span><span class="sxs-lookup"><span data-stu-id="897ae-160">You still have toodo a manual step toodeploy toohello live site.</span></span> <span data-ttu-id="897ae-161">Para um aplicativo web que não tem um ambiente de preparo, implanta ramificação mestre Olá diretamente toohello live site.</span><span class="sxs-lookup"><span data-stu-id="897ae-161">For a web app that doesn't have staging environment, it deploys hello master branch directly toohello live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="897ae-162">Em Olá **processo** guia, você pode ver o ambiente de implantação Olá é definido toohello nome do seu aplicativo web ou serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="897ae-162">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="897ae-163">Especifica valores para propriedades de saudação se você quiser que os valores diferentes de padrões de saudação.</span><span class="sxs-lookup"><span data-stu-id="897ae-163">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="897ae-164">Olá propriedades de publicação do Azure estão em Olá **implantação** seção e você talvez também seja necessário tooset MSBuild parâmetros.</span><span class="sxs-lookup"><span data-stu-id="897ae-164">hello properties for Azure publishing are in hello **Deployment** section, and you might also need tooset MSBuild parameters.</span></span> <span data-ttu-id="897ae-165">Por exemplo, em um projeto de serviço de nuvem, toospecify uma configuração de serviço diferente de "Nuvem", definir muito Olá MSbuild parâmetros`/p:TargetProfile=[YourProfile]` onde *[YourProfile]* corresponde a um arquivo de configuração de serviço com um nome como ServiceConfiguration. *YourProfile*. cscfg.</span><span class="sxs-lookup"><span data-stu-id="897ae-165">For example, in a cloud service project, toospecify a service configuration other than "Cloud", set hello MSbuild parameters too`/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="897ae-166">Olá tabela a seguir mostra propriedades disponíveis Olá em Olá **implantação** seção:</span><span class="sxs-lookup"><span data-stu-id="897ae-166">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="897ae-167">Propriedade</span><span class="sxs-lookup"><span data-stu-id="897ae-167">Property</span></span> | <span data-ttu-id="897ae-168">Valor Padrão</span><span class="sxs-lookup"><span data-stu-id="897ae-168">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="897ae-169">Permitir certificados não confiáveis</span><span class="sxs-lookup"><span data-stu-id="897ae-169">Allow Untrusted Certificates</span></span> |<span data-ttu-id="897ae-170">Se falso, os certificados SSL deve ser assinados por uma autoridade raiz.</span><span class="sxs-lookup"><span data-stu-id="897ae-170">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="897ae-171">Permitir Atualização</span><span class="sxs-lookup"><span data-stu-id="897ae-171">Allow Upgrade</span></span> |<span data-ttu-id="897ae-172">Olá implantação tooupdate permite que uma implantação existente em vez de criar um novo.</span><span class="sxs-lookup"><span data-stu-id="897ae-172">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="897ae-173">Preserva o endereço IP hello.</span><span class="sxs-lookup"><span data-stu-id="897ae-173">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="897ae-174">Não exclua</span><span class="sxs-lookup"><span data-stu-id="897ae-174">Do Not Delete</span></span> |<span data-ttu-id="897ae-175">Se verdadeiro, não substitua uma implantação não relacionada existente (a atualização é permitida).</span><span class="sxs-lookup"><span data-stu-id="897ae-175">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="897ae-176">Caminho tooDeployment configurações</span><span class="sxs-lookup"><span data-stu-id="897ae-176">Path tooDeployment Settings</span></span> |<span data-ttu-id="897ae-177">Olá caminho tooyour. pubxml arquivo para um aplicativo web, a pasta raiz de toohello relativo do repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="897ae-177">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="897ae-178">Ignorado para serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="897ae-178">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="897ae-179">Ambiente de implantação do Sharepoint</span><span class="sxs-lookup"><span data-stu-id="897ae-179">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="897ae-180">Olá mesmo como o nome do serviço hello.</span><span class="sxs-lookup"><span data-stu-id="897ae-180">hello same as hello service name.</span></span> |
    | <span data-ttu-id="897ae-181">Ambiente de implantação do Azure</span><span class="sxs-lookup"><span data-stu-id="897ae-181">Azure Deployment Environment</span></span> |<span data-ttu-id="897ae-182">Olá aplicativo ou nuvem nome do serviço web.</span><span class="sxs-lookup"><span data-stu-id="897ae-182">hello web app or cloud service name.</span></span> |
14. <span data-ttu-id="897ae-183">A essa altura, sua compilação deve estar concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="897ae-183">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="897ae-184">Se você clicar duas vezes nome de compilação hello, o Visual Studio mostra uma **Resumo da compilação**, incluindo os resultados dos testes de associadas a projetos de teste de unidade.</span><span class="sxs-lookup"><span data-stu-id="897ae-184">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="897ae-185">Em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), você pode exibir a implantação de saudação associada em Olá **implantações** guia quando Olá ambiente de preparo é selecionado.</span><span class="sxs-lookup"><span data-stu-id="897ae-185">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="897ae-186">Procure tooyour URL do seu site.</span><span class="sxs-lookup"><span data-stu-id="897ae-186">Browse tooyour site's URL.</span></span> <span data-ttu-id="897ae-187">Para um aplicativo web, basta escolher Olá **procurar** botão no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="897ae-187">For a web app, just choose  hello **Browse** button in hello portal.</span></span> <span data-ttu-id="897ae-188">De um serviço de nuvem, escolha URL Olá Olá **rápidos** seção Olá **painel** página que mostra o ambiente de preparo hello.</span><span class="sxs-lookup"><span data-stu-id="897ae-188">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment.</span></span>
    
    <span data-ttu-id="897ae-189">As implantações de integração contínua para serviços de nuvem são publicados toohello ambiente de preparo por padrão.</span><span class="sxs-lookup"><span data-stu-id="897ae-189">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="897ae-190">Você pode alterar essa configuração Olá **ambiente de serviço de nuvem alternativo** propriedade muito**produção**.</span><span class="sxs-lookup"><span data-stu-id="897ae-190">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="897ae-191">Aqui é onde Olá URL do site na página do painel do serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="897ae-191">Here's where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="897ae-192">Uma nova guia do navegador será aberto tooreveal seu site em execução.</span><span class="sxs-lookup"><span data-stu-id="897ae-192">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="897ae-193">Se você fizer outras alterações tooyour projeto, você gatilho mais cria e acumularão várias implantações.</span><span class="sxs-lookup"><span data-stu-id="897ae-193">If you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="897ae-194">Olá mais recente um é marcado como ativo.</span><span class="sxs-lookup"><span data-stu-id="897ae-194">hello latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="897ae-195">5: Reimplantar um build anterior</span><span class="sxs-lookup"><span data-stu-id="897ae-195">5: Redeploy an earlier build</span></span>
<span data-ttu-id="897ae-196">Esta etapa é opcional.</span><span class="sxs-lookup"><span data-stu-id="897ae-196">This step is optional.</span></span> <span data-ttu-id="897ae-197">Olá portal clássico do Azure, escolha uma implantação anterior e escolha **reimplantar** toorewind tooan seu site anteriormente check-in.</span><span class="sxs-lookup"><span data-stu-id="897ae-197">In hello Azure classic portal, choose an earlier deployment and choose **Redeploy** toorewind your site tooan earlier check-in.</span></span> <span data-ttu-id="897ae-198">Observe que isso vai disparar uma nova compilação no TFS e criará uma nova entrada em seu histórico de implantação.</span><span class="sxs-lookup"><span data-stu-id="897ae-198">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="897ae-199">6: alterar a implantação de produção de hello</span><span class="sxs-lookup"><span data-stu-id="897ae-199">6: Change hello Production deployment</span></span>
<span data-ttu-id="897ae-200">Quando você estiver pronto, você pode promover Olá preparo toohello ambiente de produção, escolhendo **trocar** em Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="897ae-200">When you are ready, you can promote hello Staging environment toohello Production environment by choosing **Swap** in hello Azure classic portal.</span></span> <span data-ttu-id="897ae-201">ambiente de preparo Olá implantado recentemente é promovida tooProduction e ambiente de produção anterior hello, se houver, torna-se um ambiente de preparo.</span><span class="sxs-lookup"><span data-stu-id="897ae-201">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="897ae-202">Olá implantação ativa pode ser diferente para ambientes de preparo e produção de hello, mas o histórico de implantação de saudação de builds recentes é Olá mesmo independentemente do ambiente.</span><span class="sxs-lookup"><span data-stu-id="897ae-202">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="897ae-203">7: Implantar por meio de uma ramificação em funcionamento.</span><span class="sxs-lookup"><span data-stu-id="897ae-203">7: Deploy from a working branch.</span></span>
<span data-ttu-id="897ae-204">Quando você usa o Git, você normalmente fazer alterações em uma ramificação de trabalho e integrar a ramificação mestre hello quando o desenvolvimento de atinge um estado concluído.</span><span class="sxs-lookup"><span data-stu-id="897ae-204">When you use Git, you usually make changes in a working branch and integrate into hello master branch when your development reaches a finished state.</span></span> <span data-ttu-id="897ae-205">Durante a fase de desenvolvimento de saudação de um projeto, você deseja toobuild e implantar Olá tooAzure de ramificação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="897ae-205">During hello development phase of a project, you'll want toobuild and deploy hello working branch tooAzure.</span></span>

1. <span data-ttu-id="897ae-206">Em **Team Explorer**, escolha Olá **início** botão e, em seguida, escolha Olá **ramificações** botão.</span><span class="sxs-lookup"><span data-stu-id="897ae-206">In **Team Explorer**, choose hello **Home** button and then choose hello **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="897ae-207">Escolha Olá **nova ramificação** link.</span><span class="sxs-lookup"><span data-stu-id="897ae-207">Choose hello **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="897ae-208">Insira nome de saudação do branch hello, como "trabalho" e escolha **criar ramificação**.</span><span class="sxs-lookup"><span data-stu-id="897ae-208">Enter hello name of hello branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="897ae-209">Isso cria uma nova ramificação local.</span><span class="sxs-lookup"><span data-stu-id="897ae-209">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="897ae-210">Publica o branch de saudação.</span><span class="sxs-lookup"><span data-stu-id="897ae-210">Publish hello branch.</span></span> <span data-ttu-id="897ae-211">Escolher nome de branch Olá em **não publicado ramificações**e escolha **publicar**.</span><span class="sxs-lookup"><span data-stu-id="897ae-211">Choose hello branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="897ae-212">Por padrão, somente altera o disparador de ramificação mestre toohello uma compilação contínua.</span><span class="sxs-lookup"><span data-stu-id="897ae-212">By default, only changes toohello master branch trigger a continuous build.</span></span> <span data-ttu-id="897ae-213">tooset backup contínua compilação para uma ramificação de trabalho, escolha Olá **cria** página **Team Explorer**e escolha **editar definição de compilação**.</span><span class="sxs-lookup"><span data-stu-id="897ae-213">tooset up continuous build for a working branch, choose hello **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="897ae-214">Olá abrir **configurações de fonte** guia. Em **monitorados ramificações de integração contínua e compilação**, escolha **clique aqui tooadd uma nova linha**.</span><span class="sxs-lookup"><span data-stu-id="897ae-214">Open hello **Source Settings** tab. Under **Monitored branches for continuous integration and build**, choose **Click here tooadd a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="897ae-215">Especifique a ramificação de saudação que você criou, como cabeçalhos/refs/trabalho.</span><span class="sxs-lookup"><span data-stu-id="897ae-215">Specify hello branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="897ae-216">Faça uma alteração no código hello, menu de atalho Olá abrir arquivo hello alterado e, em seguida, escolha **confirmar**.</span><span class="sxs-lookup"><span data-stu-id="897ae-216">Make a change in hello code, open hello shortcut menu for hello changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="897ae-217">Escolha Olá **as confirmações** link e escolha Olá **sincronização** botão ou hello **Push** saudação do link toocopy altera toohello cópia de ramificação de trabalho Olá no Visual Studio Serviços de equipe.</span><span class="sxs-lookup"><span data-stu-id="897ae-217">Choose hello **Unsynced Commits** link, and choose  hello **Sync** button or hello **Push** link toocopy hello changes toohello copy of hello working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="897ae-218">Navegue toohello **cria** exibir e encontrar a compilação de saudação que foi disparada apenas para a ramificação de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="897ae-218">Navigate toohello **Builds** view and find hello build that just got triggered for hello working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="897ae-219">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="897ae-219">Next steps</span></span>
<span data-ttu-id="897ae-220">toolearn mais dicas sobre como usar o Git com o Visual Studio Team Services, consulte [desenvolver e compartilhar seu código no Git usando o Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) e para obter informações sobre como usar um repositório Git que não é gerenciado pelo Visual Studio Team Services toopublish tooAzure, consulte [tooAzure implantação contínua do serviço de aplicativo](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="897ae-220">toolearn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services toopublish tooAzure, see [Continuous Deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="897ae-221">Para obter mais informações sobre o Visual Studio Team Services, consulte [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="897ae-221">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
