---
title: "Entrega contínua com o Git e o Visual Studio Team Services no Azure | Microsoft Docs"
description: "Saiba como configurar seus projetos de equipe do Visual Studio Team Services para usarem o Git para serem compilados e implantados automaticamente no recurso Aplicativo Web no Serviço de Aplicativo do Azure ou nos serviços de nuvem."
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
ms.openlocfilehash: f4f5f231536bc381d17898ff2c592be821168a65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="e695d-103">Entrega contínua no Azure usando Visual Studio Team Services e Git</span><span class="sxs-lookup"><span data-stu-id="e695d-103">Continuous delivery to Azure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="e695d-104">Você pode usar os projetos de equipe do Visual Studio Team Services para hospedar um repositório Git para seu código-fonte, e compilar e implantá-lo automaticamente em aplicativos Web ou serviços de nuvem do Azure sempre que enviar por push uma confirmação ao repositório.</span><span class="sxs-lookup"><span data-stu-id="e695d-104">You can use Visual Studio Team Services team projects to host a Git repository for your source code, and automatically build and deploy to Azure web apps or cloud services whenever you push a commit to the repository.</span></span>

<span data-ttu-id="e695d-105">Você precisará do Visual Studio 2013 e do SDK do Azure instalados.</span><span class="sxs-lookup"><span data-stu-id="e695d-105">You'll need Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="e695d-106">Se você ainda não tiver o Visual Studio 2013, baixe-o selecionando o link **Introdução gratuita (a página pode estar em inglês)** em [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="e695d-106">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="e695d-107">Instale o SDK do Azure [aqui](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="e695d-107">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="e695d-108">Você precisa de uma conta do Visual Studio Team Services para concluir este tutorial: você pode [abrir uma conta do Visual Studio Team Services gratuitamente](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="e695d-108">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="e695d-109">Para configurar um serviço de nuvem para compilação e implantação automática no Azure usando o Visual Studio Team Services, siga essas etapas.</span><span class="sxs-lookup"><span data-stu-id="e695d-109">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="e695d-110">1: Criar um repositório Git</span><span class="sxs-lookup"><span data-stu-id="e695d-110">1: Create a Git repository</span></span>
1. <span data-ttu-id="e695d-111">Se você ainda não tiver uma conta do Visual Studio Team Services, pode obter uma [aqui](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="e695d-111">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="e695d-112">Quando criar seu projeto da equipe, escolha o Git como seu sistema de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="e695d-112">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="e695d-113">Siga as instruções para conectar o Visual Studio ao projeto da equipe.</span><span class="sxs-lookup"><span data-stu-id="e695d-113">Follow the instructions to connect Visual Studio to your team project.</span></span>
2. <span data-ttu-id="e695d-114">No **Team Explorer**, escolha o link **Clonar este repositório**.</span><span class="sxs-lookup"><span data-stu-id="e695d-114">In **Team Explorer**, choose the **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="e695d-115">Especifique o local da cópia local e selecione o botão **Clonar** .</span><span class="sxs-lookup"><span data-stu-id="e695d-115">Specify the location of the local copy and then choose the **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-to-the-repository"></a><span data-ttu-id="e695d-116">2: Criar um projeto e confirmá-lo no repositório</span><span class="sxs-lookup"><span data-stu-id="e695d-116">2: Create a project and commit it to the repository</span></span>
1. <span data-ttu-id="e695d-117">No **Team Explorer**, na seção **Soluções**, selecione o link **Novo** para criar um novo projeto no repositório local.</span><span class="sxs-lookup"><span data-stu-id="e695d-117">In **Team Explorer**, in the **Solutions** section, choose the **New** link to create a new project in the local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="e695d-118">Você pode implantar um aplicativo Web ou um serviço de nuvem (aplicativo do Azure) seguindo as etapas neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="e695d-118">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span> <span data-ttu-id="e695d-119">Crie um novo projeto de Serviço de Nuvem do Azure ou um novo projeto ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e695d-119">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="e695d-120">Certifique-se de que o projeto direciona-se ao .NET Framework 4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e695d-120">Make sure that the project targets the .NET Framework 4 or later.</span></span> <span data-ttu-id="e695d-121">Se você está criando um projeto de serviço de nuvem, adicione uma função de trabalho e uma função web MVC do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e695d-121">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="e695d-122">Se você quiser criar um aplicativo Web, escolha o modelo de projeto de **Aplicativo Web ASP.NET** e escolha **MVC**.</span><span class="sxs-lookup"><span data-stu-id="e695d-122">If you want to create a web app, choose the **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="e695d-123">Consulte [Criar um aplicativo web ASP.NET no Serviço de Aplicativo do Azure](../app-service-web/app-service-web-get-started-dotnet.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="e695d-123">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="e695d-124">Abra o menu de atalho da solução e escolha **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="e695d-124">Open the shortcut menu for the solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="e695d-125">Se for a primeira vez que usa o Git no Visual Studio Team Services, você precisará fornecer algumas informações para se identificar no Git.</span><span class="sxs-lookup"><span data-stu-id="e695d-125">If this is the first time you've used Git in Visual Studio Team Services, you'll need to provide some information to identify yourself in Git.</span></span> <span data-ttu-id="e695d-126">Na área **Alterações Pendentes** do **Team Explorer**, insira seu nome de usuário e endereço de email.</span><span class="sxs-lookup"><span data-stu-id="e695d-126">In the **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="e695d-127">Digite um comentário para a confirmação e, em seguida, escolha o botão **Confirmar** .</span><span class="sxs-lookup"><span data-stu-id="e695d-127">Enter a comment for the commit and then choose the **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="e695d-128">Observe as opções para incluir ou excluir alterações específicas ao fazer check-in.</span><span class="sxs-lookup"><span data-stu-id="e695d-128">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="e695d-129">Se as alterações desejadas tiverem sido excluídas, escolha **Incluir Tudo**.</span><span class="sxs-lookup"><span data-stu-id="e695d-129">If the changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="e695d-130">Você confirmou as alterações em sua cópia local do repositório.</span><span class="sxs-lookup"><span data-stu-id="e695d-130">You've now committed the changes in your local copy of the repository.</span></span> <span data-ttu-id="e695d-131">Em seguida, sincronize as alterações com o servidor escolhendo o link **Sincronizar** .</span><span class="sxs-lookup"><span data-stu-id="e695d-131">Next, sync those changes with the server by choosing the **Sync** link.</span></span>

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="e695d-132">3: Conectar o projeto ao Azure</span><span class="sxs-lookup"><span data-stu-id="e695d-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="e695d-133">Agora que possui um repositório Git no Visual Studio Team Services com algum código-fonte nele, você está pronto para conectar seu repositório Git ao Azure.</span><span class="sxs-lookup"><span data-stu-id="e695d-133">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready to connect your git repository to Azure.</span></span>  <span data-ttu-id="e695d-134">No [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), selecione o serviço de nuvem ou aplicativo Web ou crie um novo; para isso, selecione o ícone + na parte inferior esquerda e escolha **Serviço de Nuvem** ou **Aplicativo Web**, depois selecione **Criação Rápida**.</span><span class="sxs-lookup"><span data-stu-id="e695d-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the + icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="e695d-135">Para serviços de nuvem, escolha o link **Configurar a publicação com o Visual Studio Team Services** .</span><span class="sxs-lookup"><span data-stu-id="e695d-135">For cloud services, choose the **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="e695d-136">Para aplicativos Web, escolha o link **Configurar a implantação por meio do controle do código-fonte** .</span><span class="sxs-lookup"><span data-stu-id="e695d-136">For web apps, choose the **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="e695d-137">No assistente, digite o nome da sua conta do Visual Studio Team Services na caixa de texto e escolha o link **Autorizar agora** .</span><span class="sxs-lookup"><span data-stu-id="e695d-137">In the wizard, type the name of your Visual Studio Team Services account in the textbox and choose the **Authorize Now** link.</span></span> <span data-ttu-id="e695d-138">Você pode ser solicitado a entrar.</span><span class="sxs-lookup"><span data-stu-id="e695d-138">You might be asked to sign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="e695d-139">Na caixa de diálogo pop-up **Solicitação de Conexão**, escolha **Aceitar** para autorizar o Azure a configurar seu projeto de equipe no Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="e695d-139">In the **Connection Request** pop-up dialog, choose **Accept** to authorize Azure to configure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="e695d-140">Depois que a autorização obtiver êxito, você verá uma lista suspensa que contém os projetos de equipe do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="e695d-140">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="e695d-141">Selecione o nome do projeto da equipe que você criou nas etapas anteriores e escolha o botão de marca de seleção do assistente.</span><span class="sxs-lookup"><span data-stu-id="e695d-141">Select the name of team project that you created in the previous steps, and choose the wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="e695d-142">Na próxima vez em que você enviar uma confirmação por push ao repositório, o Visual Studio Team Services vai compilar e implantar seu projeto no Azure.</span><span class="sxs-lookup"><span data-stu-id="e695d-142">The next time you push a commit to your repository, Visual Studio Team Services will build and deploy your project to Azure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="e695d-143">4: Disparar uma recompilação e reimplantar seu projeto</span><span class="sxs-lookup"><span data-stu-id="e695d-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="e695d-144">No Visual Studio, abra um arquivo e altere-o.</span><span class="sxs-lookup"><span data-stu-id="e695d-144">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="e695d-145">Por exemplo, altere o arquivo `_Layout.cshtml` na pasta Modos de Exibição\\Compartilhado em uma função web do MVC.</span><span class="sxs-lookup"><span data-stu-id="e695d-145">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="e695d-146">Edite o texto do rodapé do site e salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="e695d-146">Edit the footer text for the site and save the file.</span></span>
   
    ![][18]
3. <span data-ttu-id="e695d-147">No **Gerenciador de Soluções**, abra o menu de atalho do nó da solução, nó do projeto ou do arquivo que você alterou e então escolha **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="e695d-147">In **Solution Explorer**, open the shortcut menu for the solution node, project node, or the file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="e695d-148">Digite um comentário e escolha **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="e695d-148">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="e695d-149">Selecione o link **Sincronizar** .</span><span class="sxs-lookup"><span data-stu-id="e695d-149">Choose the **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="e695d-150">Escolha o link **Enviar por push** para enviar sua confirmação por push ao repositório no Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="e695d-150">Choose the **Push** link to push your commit to the repository in Visual Studio Team Services.</span></span> <span data-ttu-id="e695d-151">(Você também pode usar o botão **Sincronizar** para copiar suas confirmações no repositório.</span><span class="sxs-lookup"><span data-stu-id="e695d-151">(You can also use the **Sync** button to copy your commits to the repository.</span></span> <span data-ttu-id="e695d-152">A diferença é que **Sincronizar** também efetua pull das alterações mais recentes do repositório.</span><span class="sxs-lookup"><span data-stu-id="e695d-152">The difference is that **Sync** also pulls the latest changes from the repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="e695d-153">Escolha o botão **Início** para retornar à home page do **Team Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e695d-153">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="e695d-154">Escolha **Compilações** para exibir as compilações em andamento.</span><span class="sxs-lookup"><span data-stu-id="e695d-154">Choose **Builds** to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="e695d-155">**Team Explorer** mostra que uma compilação foi disparada para seu check-in.</span><span class="sxs-lookup"><span data-stu-id="e695d-155">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="e695d-156">Para exibir um log detalhado enquanto a compilação está em andamento, clique duas vezes no nome da compilação em andamento.</span><span class="sxs-lookup"><span data-stu-id="e695d-156">To view a detailed log as the build progresses, double-click the name of the build in progress.</span></span>
10. <span data-ttu-id="e695d-157">Enquanto a compilação estiver em andamento, examine a definição de compilação que foi criada quando você usou o assistente para vincular ao Azure.</span><span class="sxs-lookup"><span data-stu-id="e695d-157">While the build is in-progress, take a look at the build definition that was created when you used the wizard to link to Azure.</span></span>  <span data-ttu-id="e695d-158">Abra o menu de atalho da definição de compilação e escolha **Editar Definição de Compilação**.</span><span class="sxs-lookup"><span data-stu-id="e695d-158">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="e695d-159">Na guia **Gatilho** , você verá que a definição de compilação está definida, por padrão, para compilar em cada check-in.</span><span class="sxs-lookup"><span data-stu-id="e695d-159">In the **Trigger** tab, you will see that the build definition is set to build on every check-in, by default.</span></span> <span data-ttu-id="e695d-160">(Para um serviço de nuvem, o Visual Studio Team Services compila e implanta a ramificação mestre no ambiente de preparo automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e695d-160">(For a cloud service, Visual Studio Team Services builds and deploys the master branch to the staging environment automatically.</span></span> <span data-ttu-id="e695d-161">Você ainda precisa executar uma etapa manual para implantar no site ativo.</span><span class="sxs-lookup"><span data-stu-id="e695d-161">You still have to do a manual step to deploy to the live site.</span></span> <span data-ttu-id="e695d-162">Para um aplicativo Web que não tem um ambiente de preparo, ele implanta a ramificação mestra diretamente no site ativo.</span><span class="sxs-lookup"><span data-stu-id="e695d-162">For a web app that doesn't have staging environment, it deploys the master branch directly to the live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="e695d-163">Na guia **Processo** , você pode ver que o ambiente de implantação está definido como o nome do seu serviço de nuvem ou aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e695d-163">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="e695d-164">Especifique valores para as propriedades se você desejar valores diferentes dos padrões.</span><span class="sxs-lookup"><span data-stu-id="e695d-164">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="e695d-165">As propriedades de publicação no Azure estão na seção **Implantação** e talvez você também precise definir parâmetros MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e695d-165">The properties for Azure publishing are in the **Deployment** section, and you might also need to set MSBuild parameters.</span></span> <span data-ttu-id="e695d-166">Por exemplo, em um projeto de serviço de nuvem, para especificar uma configuração de serviço diferente de "Nuvem", defina os parâmetros do MSbuild como `/p:TargetProfile=[YourProfile]`, em que *[YourProfile]* corresponde a um arquivo de configuração de serviço com um nome como ServiceConfiguration.*YourProfile*.cscfg.</span><span class="sxs-lookup"><span data-stu-id="e695d-166">For example, in a cloud service project, to specify a service configuration other than "Cloud", set the MSbuild parameters to `/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="e695d-167">A tabela a seguir mostra as propriedades disponíveis na seção **Implantação** :</span><span class="sxs-lookup"><span data-stu-id="e695d-167">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="e695d-168">Propriedade</span><span class="sxs-lookup"><span data-stu-id="e695d-168">Property</span></span> | <span data-ttu-id="e695d-169">Valor Padrão</span><span class="sxs-lookup"><span data-stu-id="e695d-169">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="e695d-170">Permitir certificados não confiáveis</span><span class="sxs-lookup"><span data-stu-id="e695d-170">Allow Untrusted Certificates</span></span> |<span data-ttu-id="e695d-171">Se falso, os certificados SSL deve ser assinados por uma autoridade raiz.</span><span class="sxs-lookup"><span data-stu-id="e695d-171">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="e695d-172">Permitir Atualização</span><span class="sxs-lookup"><span data-stu-id="e695d-172">Allow Upgrade</span></span> |<span data-ttu-id="e695d-173">Permite que a implantação atualize uma implantação existente em vez de criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="e695d-173">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="e695d-174">Preserve o endereço IP.</span><span class="sxs-lookup"><span data-stu-id="e695d-174">Preserves the IP address.</span></span> |
    | <span data-ttu-id="e695d-175">Não exclua</span><span class="sxs-lookup"><span data-stu-id="e695d-175">Do Not Delete</span></span> |<span data-ttu-id="e695d-176">Se verdadeiro, não substitua uma implantação não relacionada existente (a atualização é permitida).</span><span class="sxs-lookup"><span data-stu-id="e695d-176">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="e695d-177">Caminho para Configurações de Implantação</span><span class="sxs-lookup"><span data-stu-id="e695d-177">Path to Deployment Settings</span></span> |<span data-ttu-id="e695d-178">O caminho para seu arquivo .pubxml para um aplicativo Web, relacionado à pasta raiz do repositório.</span><span class="sxs-lookup"><span data-stu-id="e695d-178">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="e695d-179">Ignorado para serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e695d-179">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="e695d-180">Ambiente de implantação do Sharepoint</span><span class="sxs-lookup"><span data-stu-id="e695d-180">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="e695d-181">O mesmo que o nome do serviço.</span><span class="sxs-lookup"><span data-stu-id="e695d-181">The same as the service name.</span></span> |
    | <span data-ttu-id="e695d-182">Ambiente de implantação do Azure</span><span class="sxs-lookup"><span data-stu-id="e695d-182">Azure Deployment Environment</span></span> |<span data-ttu-id="e695d-183">O nome do aplicativo Web ou do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e695d-183">The web app or cloud service name.</span></span> |
14. <span data-ttu-id="e695d-184">A essa altura, sua compilação deve estar concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="e695d-184">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="e695d-185">Se você clicar duas vezes no nome da compilação, o Visual Studio mostrará um **Resumo da Compilação**, incluindo qualquer resultado de teste de projetos de teste de unidade associados.</span><span class="sxs-lookup"><span data-stu-id="e695d-185">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="e695d-186">No [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), você poderá exibir a implantação associada na guia **Implantações** quando o ambiente de preparo estiver selecionado.</span><span class="sxs-lookup"><span data-stu-id="e695d-186">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="e695d-187">Navegue até a URL do site.</span><span class="sxs-lookup"><span data-stu-id="e695d-187">Browse to your site's URL.</span></span> <span data-ttu-id="e695d-188">Para um aplicativo Web, basta clicar no botão **Procurar** no portal.</span><span class="sxs-lookup"><span data-stu-id="e695d-188">For a web app, just choose  the **Browse** button in the portal.</span></span> <span data-ttu-id="e695d-189">Para um serviço de nuvem, escolha a URL na seção **Visão Rápida** da página **Painel** que mostra o ambiente de preparo.</span><span class="sxs-lookup"><span data-stu-id="e695d-189">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment.</span></span>
    
    <span data-ttu-id="e695d-190">Por padrão, as implantações de integração contínua para serviços de nuvem são publicadas no ambiente de preparo.</span><span class="sxs-lookup"><span data-stu-id="e695d-190">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="e695d-191">Você pode alterar isso definindo a propriedade **Ambiente de Serviço de Nuvem Alternativo** para a **Produção**.</span><span class="sxs-lookup"><span data-stu-id="e695d-191">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="e695d-192">Esta é a localização do URL do site está na página do painel do serviço de nuvem:</span><span class="sxs-lookup"><span data-stu-id="e695d-192">Here's where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="e695d-193">Uma nova guia do navegador será aberta para revelar seu site em execução.</span><span class="sxs-lookup"><span data-stu-id="e695d-193">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="e695d-194">Se fizer outras alterações em seu projeto, você disparará mais compilações e acumulará várias implantações.</span><span class="sxs-lookup"><span data-stu-id="e695d-194">If you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="e695d-195">O mais recente é marcado como Ativo.</span><span class="sxs-lookup"><span data-stu-id="e695d-195">The latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="e695d-196">5: Reimplantar um build anterior</span><span class="sxs-lookup"><span data-stu-id="e695d-196">5: Redeploy an earlier build</span></span>
<span data-ttu-id="e695d-197">Esta etapa é opcional.</span><span class="sxs-lookup"><span data-stu-id="e695d-197">This step is optional.</span></span> <span data-ttu-id="e695d-198">No portal clássico do Azure, selecione uma implantação anterior e escolha **Reimplantar** para que seu site retroceda até um check-in anterior.</span><span class="sxs-lookup"><span data-stu-id="e695d-198">In the Azure classic portal, choose an earlier deployment and choose **Redeploy** to rewind your site to an earlier check-in.</span></span> <span data-ttu-id="e695d-199">Observe que isso vai disparar uma nova compilação no TFS e criará uma nova entrada em seu histórico de implantação.</span><span class="sxs-lookup"><span data-stu-id="e695d-199">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="e695d-200">6: Alterar a implantação de Produção</span><span class="sxs-lookup"><span data-stu-id="e695d-200">6: Change the Production deployment</span></span>
<span data-ttu-id="e695d-201">Quando estiver pronto, você pode promover o ambiente de preparo para o ambiente de produção escolhendo **Trocar** no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="e695d-201">When you are ready, you can promote the Staging environment to the Production environment by choosing **Swap** in the Azure classic portal.</span></span> <span data-ttu-id="e695d-202">O ambiente de preparo recém-implantado é promovido para a produção e o ambiente de produção anterior, se houver, torna-se um ambiente de preparo.</span><span class="sxs-lookup"><span data-stu-id="e695d-202">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="e695d-203">A implantação Ativa pode ser diferente dos ambientes de preparo e de produção, mas o histórico de implantação de compilações recentes é o mesmo, independentemente do ambiente.</span><span class="sxs-lookup"><span data-stu-id="e695d-203">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="e695d-204">7: Implantar por meio de uma ramificação em funcionamento.</span><span class="sxs-lookup"><span data-stu-id="e695d-204">7: Deploy from a working branch.</span></span>
<span data-ttu-id="e695d-205">Quando usa o Git, normalmente você faz alterações em uma ramificação em andamento e a integra à ramificação mestre quando seu desenvolvimento estiver concluído.</span><span class="sxs-lookup"><span data-stu-id="e695d-205">When you use Git, you usually make changes in a working branch and integrate into the master branch when your development reaches a finished state.</span></span> <span data-ttu-id="e695d-206">Durante a fase de desenvolvimento de um projeto, você compilará e implantará a ramificação em andamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="e695d-206">During the development phase of a project, you'll want to build and deploy the working branch to Azure.</span></span>

1. <span data-ttu-id="e695d-207">No **Team Explorer**, escolha o botão **Início** e depois escolha o botão **Ramificações**.</span><span class="sxs-lookup"><span data-stu-id="e695d-207">In **Team Explorer**, choose the **Home** button and then choose the **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="e695d-208">Escolha o link **Nova Ramificação** .</span><span class="sxs-lookup"><span data-stu-id="e695d-208">Choose the **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="e695d-209">Insira o nome da ramificação, como “em andamento” e escolha **Criar Ramificação**.</span><span class="sxs-lookup"><span data-stu-id="e695d-209">Enter the name of the branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="e695d-210">Isso cria uma nova ramificação local.</span><span class="sxs-lookup"><span data-stu-id="e695d-210">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="e695d-211">Publique a ramificação.</span><span class="sxs-lookup"><span data-stu-id="e695d-211">Publish the branch.</span></span> <span data-ttu-id="e695d-212">Escolha o nome da ramificação em **Ramificações Não Publicadas** e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e695d-212">Choose the branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="e695d-213">Por padrão, somente alterações na ramificação mestre disparam uma compilação contínua.</span><span class="sxs-lookup"><span data-stu-id="e695d-213">By default, only changes to the master branch trigger a continuous build.</span></span> <span data-ttu-id="e695d-214">Para definir o build contínuo para uma ramificação em andamento, escolha a página **Compilações** no **Team Explorer** e escolha **Editar Definição de Build**.</span><span class="sxs-lookup"><span data-stu-id="e695d-214">To set up continuous build for a working branch, choose the **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="e695d-215">Abra a guia **Configurações da Origem** .</span><span class="sxs-lookup"><span data-stu-id="e695d-215">Open the **Source Settings** tab.</span></span> <span data-ttu-id="e695d-216">Em **Ramificações Monitoradas para Integração e Build Contínuos**, selecione **Clique aqui para Adicionar uma Nova Linha**.</span><span class="sxs-lookup"><span data-stu-id="e695d-216">Under **Monitored branches for continuous integration and build**, choose **Click here to add a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="e695d-217">Especifique a ramificação que você criou, como refs/heads/working.</span><span class="sxs-lookup"><span data-stu-id="e695d-217">Specify the branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="e695d-218">Faça uma alteração no código, abra o menu de atalho do arquivo alterado e escolha **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="e695d-218">Make a change in the code, open the shortcut menu for the changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="e695d-219">Escolha o link **Confirmações Não Sincronizadas** e clique no botão **Sincronizar** ou no link **Enviar por push** para copiar as alterações para a cópia da ramificação em andamento no Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="e695d-219">Choose the **Unsynced Commits** link, and choose  the **Sync** button or the **Push** link to copy the changes to the copy of the working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="e695d-220">Navegue até a exibição **Compilações** e encontre a compilação que foi acionada para a ramificação em andamento.</span><span class="sxs-lookup"><span data-stu-id="e695d-220">Navigate to the **Builds** view and find the build that just got triggered for the working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e695d-221">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e695d-221">Next steps</span></span>
<span data-ttu-id="e695d-222">Para obter mais dicas sobre como usar o Git com o Visual Studio Team Services, consulte [Desenvolver e compartilhar seu código no Git usando o Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) e para obter informações sobre como usar um repositório Git que não é gerenciado pelo Visual Studio Team Services para publicar no Azure, consulte [Implantação Contínua para o Serviço de Aplicativo do Azure](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="e695d-222">To learn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services to publish to Azure, see [Continuous Deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="e695d-223">Para obter mais informações sobre o Visual Studio Team Services, consulte [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="e695d-223">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
