---
title: "Entrega contínua com o Visual Studio Team Services no Azure | Microsoft Docs"
description: "Saiba como configurar seus projetos de equipe do Visual Studio Team Services para serem compilados e implantados automaticamente no recurso Aplicativo Web no Serviço de Aplicativo do Azure ou nos serviços de nuvem."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: d80ce63eb7ddfd7c45726be887a772f9a7594b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a><span data-ttu-id="3e8ca-103">Entrega contínua no Azure usando Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="3e8ca-103">Continuous delivery to Azure using Visual Studio Team Services</span></span>
<span data-ttu-id="3e8ca-104">Você pode configurar seus projetos de equipe do Visual Studio Team Services para compilação e implantação automática em aplicativos Web ou serviços de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-104">You can configure your Visual Studio Team Services team projects to automatically build and deploy to Azure web apps or cloud services.</span></span>  <span data-ttu-id="3e8ca-105">(Para obter informações sobre como configurar uma compilação contínua e implantar um sistema usando um Team Foundation Server *local* , consulte [Entrega contínua de serviços de nuvem no Azure](cloud-services-dotnet-continuous-delivery.md).)</span><span class="sxs-lookup"><span data-stu-id="3e8ca-105">(For information on how to set up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="3e8ca-106">Este tutorial pressupõe que você possui o Visual Studio 2013 e o SDK do Azure instalados.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-106">This tutorial assumes you have Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="3e8ca-107">Se você ainda não tiver o Visual Studio 2013, baixe-o selecionando o link **Introdução gratuita (a página pode estar em inglês)** em [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="3e8ca-107">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="3e8ca-108">Instale o SDK do Azure [aqui](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="3e8ca-108">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="3e8ca-109">Você precisa de uma conta do Visual Studio Team Services para concluir este tutorial: você pode [abrir uma conta do Visual Studio Team Services gratuitamente](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="3e8ca-109">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="3e8ca-110">Para configurar um serviço de nuvem para compilação e implantação automática no Azure usando o Visual Studio Team Services, siga essas etapas.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-110">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="3e8ca-111">1: Criar um projeto de equipe</span><span class="sxs-lookup"><span data-stu-id="3e8ca-111">1: Create a team project</span></span>
<span data-ttu-id="3e8ca-112">Siga as instruções contidas [aqui](http://go.microsoft.com/fwlink/?LinkId=512980) para criar seu projeto de equipe e vinculá-lo ao Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-112">Follow the instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) to create your team project and link it to Visual Studio.</span></span> <span data-ttu-id="3e8ca-113">Este passo a passo pressupõe que você está usando oo Controle de Versão do Team Foundation (TFVC).</span><span class="sxs-lookup"><span data-stu-id="3e8ca-113">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="3e8ca-114">Se quiser usar o Git para controle de versão, consulte [a versão do Git neste passo a passo](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="3e8ca-114">If you want to use Git for version control, see [the Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-to-source-control"></a><span data-ttu-id="3e8ca-115">2: Faça check-in em um projeto para o controle do código-fonte</span><span class="sxs-lookup"><span data-stu-id="3e8ca-115">2: Check in a project to source control</span></span>
1. <span data-ttu-id="3e8ca-116">No Visual Studio, abra a solução que você deseja implantar ou crie uma nova.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-116">In Visual Studio, open the solution you want to deploy, or create a new one.</span></span>
   <span data-ttu-id="3e8ca-117">Você pode implantar um aplicativo Web ou um serviço de nuvem (aplicativo do Azure) seguindo as etapas neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-117">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span>
   <span data-ttu-id="3e8ca-118">Se você desejar criar uma nova solução, crie um novo projeto de Serviço de Nuvem do Azure ou um novo projeto ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-118">If you want to create a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="3e8ca-119">Verifique se o projeto é direcionado para o .NET Framework 4 ou 4.5 e, se você estiver criando um projeto de serviço de nuvem, adicione uma função web e uma função de trabalho ASP.NET MVC e escolha o aplicativo da Internet para a função web.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-119">Make sure that the project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for the web role.</span></span> <span data-ttu-id="3e8ca-120">Quando solicitado, escolha **Aplicativo da Internet**.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-120">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="3e8ca-121">Se você quiser criar um aplicativo Web, escolha o modelo de projeto de Aplicativo Web ASP.NET e escolha MVC.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-121">If you want to create a web app, choose the ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="3e8ca-122">Consulte [Criar um aplicativo web ASP.NET no Serviço de Aplicativo do Azure](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="3e8ca-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3e8ca-123">O Visual Studio Team Services só suporta implantações de CI de aplicativos Web do Visual Studio no momento.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-123">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="3e8ca-124">Projetos de Site estão fora do escopo.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-124">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="3e8ca-125">Abra o menu de contexto da solução e selecione **Adicionar solução ao controle do código-fonte**.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-125">Open the context menu for the solution, and choose **Add Solution to Source Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="3e8ca-126">Aceite ou altere os padrões e escolha o botão **OK** .</span><span class="sxs-lookup"><span data-stu-id="3e8ca-126">Accept or change the defaults and choose the **OK** button.</span></span> <span data-ttu-id="3e8ca-127">Quando o processo estiver concluído, os ícones do controle do código-fonte aparecerão no **Gerenciador de Soluções**.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-127">Once the process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="3e8ca-128">Abra o menu de atalho da solução e escolha **Fazer Check-In**.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-128">Open the shortcut menu for the solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="3e8ca-129">Na área **Alterações Pendentes** do **Team Explorer**, digite um comentário para o check-in e escolha o botão **Check-In**.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-129">In the **Pending Changes** area of **Team Explorer**, type a comment for the check-in and choose the **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="3e8ca-130">Observe as opções para incluir ou excluir alterações específicas ao fazer check-in.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-130">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="3e8ca-131">Se desejar que as alterações sejam excluídas, escolha o link **Incluir Tudo** .</span><span class="sxs-lookup"><span data-stu-id="3e8ca-131">If desired changes are excluded, choose the **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="3e8ca-132">3: Conectar o projeto ao Azure</span><span class="sxs-lookup"><span data-stu-id="3e8ca-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="3e8ca-133">Agora que você tem um projeto da equipe do VS Team Services com algum código-fonte nele, você está pronto para conectar seu projeto da equipe ao Azure.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-133">Now that you have a VS Team Services team project with some source code in it, you are ready to connect your team project to Azure.</span></span>  <span data-ttu-id="3e8ca-134">No [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), selecione seu aplicativo Web ou serviço de nuvem, ou crie um novo escolhendo o ícone **+** à esquerda inferior e **Serviço de Nuvem** ou **Aplicativo Web**, então, **Criação Rápida**.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the **+** icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="3e8ca-135">Escolha o link **Configurar a publicação com o Visual Studio Team Services** .</span><span class="sxs-lookup"><span data-stu-id="3e8ca-135">Choose the **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="3e8ca-136">No assistente, digite o nome da sua conta do Visual Studio Team Services na caixa de texto e clique no link **Autorizar agora** .</span><span class="sxs-lookup"><span data-stu-id="3e8ca-136">In the wizard, type the name of your Visual Studio Team Services account in the textbox and click the **Authorize Now** link.</span></span> <span data-ttu-id="3e8ca-137">Você pode ser solicitado a entrar.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-137">You might be asked to sign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="3e8ca-138">Na caixa de diálogo pop-up **Solicitação de Conexão**, escolha o botão **Aceitar** para autorizar o Azure a configurar seu projeto de equipe no VS Team Services.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-138">In the **Connection Request** pop-up dialog, choose the **Accept** button to authorize Azure to configure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="3e8ca-139">Quando a autorização for bem-sucedida, você verá uma lista suspensa que contém uma lista de seus projetos de equipe do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-139">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="3e8ca-140">Escolha o nome do projeto de equipe criado nas etapas anteriores e escolha o botão da marca de seleção do assistente.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-140">Choose  the name of team project that you created in the previous steps, and then choose the wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="3e8ca-141">Quando seu projeto estiver vinculado, você verá algumas instruções para fazer check-in das alterações em seu projeto de equipe do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-141">After your project is linked, you will see some instructions for checking in changes to your Visual Studio Team Services team project.</span></span>  <span data-ttu-id="3e8ca-142">Em seu próximo check-in, o Visual Studio Team Services criará e implantará o projeto no Azure.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-142">On your next check-in, Visual Studio Team Services will build and deploy your project to Azure.</span></span>  <span data-ttu-id="3e8ca-143">Experimente isso agora clicando no link **Check-In no Visual Studio** e no link **Iniciar o Visual Studio** (ou o botão equivalente do **Visual Studio** na parte inferior da tela do portal).</span><span class="sxs-lookup"><span data-stu-id="3e8ca-143">Try this now by clicking the **Check In from Visual Studio** link, and then the **Launch Visual Studio** link (or the equivalent **Visual Studio** button at the bottom of the portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="3e8ca-144">4: Disparar uma recompilação e reimplantar seu projeto</span><span class="sxs-lookup"><span data-stu-id="3e8ca-144">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="3e8ca-145">No Team Explorer do **Visual Studio**, escolha o link **Gerenciador de Controle da Fonte**.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-145">In Visual Studio's **Team Explorer**, choose the **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="3e8ca-146">Navegue para seu arquivo de solução e abra-o.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-146">Navigate to your solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="3e8ca-147">No **Gerenciador de Soluções**, abra um arquivo e altere-o.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-147">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="3e8ca-148">Por exemplo, altere o arquivo `_Layout.cshtml` na pasta Exibições\\Compartilhadas em uma função Web do MVC.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-148">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="3e8ca-149">Edite o logotipo do site e pressione **Ctrl+S** para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-149">Edit the logo for the site and choose **Ctrl+S** to save the file.</span></span>
   
    ![][18]
5. <span data-ttu-id="3e8ca-150">No **Team Explorer**, escolha o link **Alterações Pendentes**.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-150">In **Team Explorer**, choose the **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="3e8ca-151">Digite um comentário e escolha o botão **Fazer Check-In** .</span><span class="sxs-lookup"><span data-stu-id="3e8ca-151">Enter a comment and then choose the **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="3e8ca-152">Escolha o botão **Início** para retornar à home page do **Team Explorer**.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-152">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="3e8ca-153">Escolha o link **Compilações** para exibir as compilações em andamento.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-153">Choose the **Builds** link to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="3e8ca-154">**Team Explorer** mostra que uma compilação foi disparada para seu check-in.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="3e8ca-155">Clique duas vezes no nome da compilação em andamento para exibir um log detalhado enquanto a compilação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-155">Double-click the name of the build in progress to view a detailed log as the build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="3e8ca-156">Enquanto a compilação estiver em andamento, examine a definição da compilação que foi criada quando você vinculou o TFS no Azure usando o assistente.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-156">While the build is in-progress, take a look at the build definition that was created when you linked TFS to Azure by using the wizard.</span></span>  <span data-ttu-id="3e8ca-157">Abra o menu de atalho da definição de compilação e escolha **Editar Definição de Compilação**.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-157">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="3e8ca-158">Na guia **Gatilho** , você verá que a definição de compilação está definida, por padrão, para compilar em cada check-in.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-158">In the **Trigger** tab, you will see that the build definition is set to build on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="3e8ca-159">Na guia **Processo** , você pode ver que o ambiente de implantação está definido como o nome do seu serviço de nuvem ou aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-159">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span> <span data-ttu-id="3e8ca-160">Se estiver trabalhando com aplicativos Web, as propriedades que você verá serão diferentes daquelas mostradas aqui.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-160">If you are working with web apps, the properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="3e8ca-161">Especifique valores para as propriedades se você desejar valores diferentes dos padrões.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-161">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="3e8ca-162">As propriedades de publicação no Azure ficam na seção **Implantação** .</span><span class="sxs-lookup"><span data-stu-id="3e8ca-162">The properties for Azure publishing are in the **Deployment** section.</span></span>
    
     <span data-ttu-id="3e8ca-163">A tabela a seguir mostra as propriedades disponíveis na seção **Implantação** :</span><span class="sxs-lookup"><span data-stu-id="3e8ca-163">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="3e8ca-164">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3e8ca-164">Property</span></span> | <span data-ttu-id="3e8ca-165">Valor Padrão</span><span class="sxs-lookup"><span data-stu-id="3e8ca-165">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="3e8ca-166">Permitir certificados não confiáveis</span><span class="sxs-lookup"><span data-stu-id="3e8ca-166">Allow Untrusted Certificates</span></span> |<span data-ttu-id="3e8ca-167">Se falso, os certificados SSL deve ser assinados por uma autoridade raiz.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-167">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="3e8ca-168">Permitir Atualização</span><span class="sxs-lookup"><span data-stu-id="3e8ca-168">Allow Upgrade</span></span> |<span data-ttu-id="3e8ca-169">Permite que a implantação atualize uma implantação existente em vez de criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-169">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="3e8ca-170">Preserve o endereço IP.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-170">Preserves the IP address.</span></span> |
    | <span data-ttu-id="3e8ca-171">Não exclua</span><span class="sxs-lookup"><span data-stu-id="3e8ca-171">Do Not Delete</span></span> |<span data-ttu-id="3e8ca-172">Se verdadeiro, não substitua uma implantação não relacionada existente (a atualização é permitida).</span><span class="sxs-lookup"><span data-stu-id="3e8ca-172">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="3e8ca-173">Caminho para Configurações de Implantação</span><span class="sxs-lookup"><span data-stu-id="3e8ca-173">Path to Deployment Settings</span></span> |<span data-ttu-id="3e8ca-174">O caminho para seu arquivo .pubxml para um aplicativo Web, relacionado à pasta raiz do repositório.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-174">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="3e8ca-175">Ignorado para serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-175">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="3e8ca-176">Ambiente de implantação do Sharepoint</span><span class="sxs-lookup"><span data-stu-id="3e8ca-176">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="3e8ca-177">O mesmo que o nome do serviço.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-177">The same as the service name.</span></span> |
    | <span data-ttu-id="3e8ca-178">Ambiente de implantação do Azure</span><span class="sxs-lookup"><span data-stu-id="3e8ca-178">Azure Deployment Environment</span></span> |<span data-ttu-id="3e8ca-179">O nome do aplicativo Web ou do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-179">The web app or cloud service name.</span></span> |
12. <span data-ttu-id="3e8ca-180">Se está usando configurações de serviço múltipla (arquivos .cscfg), você pode especificar a configuração do serviço desejado na configuração **Compilar, Avançado argumentos MSBuild** .</span><span class="sxs-lookup"><span data-stu-id="3e8ca-180">If you are using multiple service configurations (.cscfg files), you can specify the desired service configuration in the **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="3e8ca-181">Por exemplo, para usar ServiceConfiguration.Test.cscfg, defina opções de linha de argumentos MSBuild `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-181">For example, to use ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="3e8ca-182">A essa altura, sua compilação deve estar concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-182">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="3e8ca-183">Se você clicar duas vezes no nome da compilação, o Visual Studio mostrará um **Resumo da Compilação**, incluindo qualquer resultado de teste de projetos de teste de unidade associados.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-183">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="3e8ca-184">No [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), você poderá exibir a implantação associada na guia **Implantações** quando o ambiente de preparo estiver selecionado.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-184">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="3e8ca-185">Navegue até a URL do site.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-185">Browse to your site's URL.</span></span> <span data-ttu-id="3e8ca-186">Para um aplicativo Web, basta clicar no botão **Procurar** na barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-186">For a web app, just click the **Browse** button on the command bar.</span></span> <span data-ttu-id="3e8ca-187">Para ver um serviço de nuvem, escolha a URL na seção **Visão Rápida** da página **Painel** que mostra o Ambiente de preparo de um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-187">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment for a cloud service.</span></span> <span data-ttu-id="3e8ca-188">Por padrão, as implantações de integração contínua para serviços de nuvem são publicadas no ambiente de preparo.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-188">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="3e8ca-189">Você pode alterar isso definindo a propriedade **Alternate Cloud Service Environment** para **Production**.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-189">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="3e8ca-190">Esta captura de tela mostra onde a URL do site está na página do painel do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-190">This screenshot shows where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="3e8ca-191">Uma nova guia do navegador será aberta para revelar seu site em execução.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-191">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="3e8ca-192">Para serviços de nuvem, se você fizer outras alterações em seu projeto, você disparará mais compilações e acumulará várias implantações.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-192">For cloud services, if you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="3e8ca-193">A última marcada como Ativa.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-193">The latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="3e8ca-194">5: Reimplantar um build anterior</span><span class="sxs-lookup"><span data-stu-id="3e8ca-194">5: Redeploy an earlier build</span></span>
<span data-ttu-id="3e8ca-195">Esta etapa se aplica aos serviços de nuvem e é opcional.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-195">This step applies to cloud services and is optional.</span></span> <span data-ttu-id="3e8ca-196">No portal clássico do Azure, selecione uma implantação anterior e clique no botão **Reimplantar** para retroceder seu site para um check-in anterior.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-196">In the Azure classic portal, choose an earlier deployment and then choose the **Redeploy** button to rewind your site to an earlier check-in.</span></span>  <span data-ttu-id="3e8ca-197">Observe que isso vai disparar uma nova compilação no TFS e criará uma nova entrada em seu histórico de implantação.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-197">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="3e8ca-198">6: Alterar a implantação de Produção</span><span class="sxs-lookup"><span data-stu-id="3e8ca-198">6: Change the Production deployment</span></span>
<span data-ttu-id="3e8ca-199">Esta etapa se aplica somente aos serviços de nuvem, não aos aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-199">This step applies only to cloud services, not web apps.</span></span> <span data-ttu-id="3e8ca-200">Quando estiver pronto, você pode promover o ambiente de preparo para o ambiente de produção escolhendo o botão **Permutar** no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-200">When you are ready, you can promote the Staging environment to the production environment by choosing the **Swap** button in the Azure classic portal.</span></span> <span data-ttu-id="3e8ca-201">O ambiente de preparo recém-implantado é promovido para a produção e o ambiente de produção anterior, se houver, torna-se um ambiente de preparo.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-201">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="3e8ca-202">A implantação Ativa pode ser diferente dos ambientes de preparo e de produção, mas o histórico de implantação de compilações recentes é o mesmo, independentemente do ambiente.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-202">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="3e8ca-203">7: Executar testes de unidade</span><span class="sxs-lookup"><span data-stu-id="3e8ca-203">7: Run unit tests</span></span>
<span data-ttu-id="3e8ca-204">Esta etapa se aplica somente aos aplicativo Web, não serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-204">This step applies only to web apps, not cloud services.</span></span> <span data-ttu-id="3e8ca-205">Para colocar um portão de qualidade em suas implantações, você pode executar testes da unidade e se eles falhares, você pode parar a implantação.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-205">To put a quality gate on your deployment, you can run unit tests and if they fail, you can stop the deployment.</span></span>

1. <span data-ttu-id="3e8ca-206">No Visual Studio, adicione um projeto de teste de unidade.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-206">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="3e8ca-207">Adicione as referências do projeto aos projetos que deseja testar.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-207">Add project references to the project you want to test.</span></span>
   
   ![][40]
3. <span data-ttu-id="3e8ca-208">Adicione alguns testes de unidade.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-208">Add some unit tests.</span></span> <span data-ttu-id="3e8ca-209">Para começar, tente um teste fictício que sempre passará.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-209">To get started, try a dummy test that will always pass.</span></span>
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. <span data-ttu-id="3e8ca-210">Editar a definição de compilação, escolha a guia **Processo**, em seguida, expanda o nó **Teste**.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-210">Edit the build definition, choose the **Process** tab, and expand the **Test** node.</span></span>
5. <span data-ttu-id="3e8ca-211">Defina o **Compilação falha na falha de teste** para Verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-211">Set the **Fail build on test failure** to True.</span></span> <span data-ttu-id="3e8ca-212">Isso significa que a implantação não ocorre, a menos que passe no teste.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-212">This means that the deployment won't occur unless the tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="3e8ca-213">Fila de uma nova compilação.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-213">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="3e8ca-214">Enquanto a compilação está em processamento, verifique seu progresso.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-214">While the build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="3e8ca-215">Quando a compilação está concluída, verifique os resultados de teste.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-215">When the build is done, check the test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="3e8ca-216">Tente criar um teste que falhará.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-216">Try creating a test that will fail.</span></span> <span data-ttu-id="3e8ca-217">Adicione um novo teste copiando o primeiro, renomeando-o e comentando a linha de código que afirma que NotImplementedException é uma exceção esperada.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-217">Add a new test by copying the first one, rename it, and comment out the line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="3e8ca-218">Faça check-in das alterações para a fila de uma nova compilação.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-218">Check in the change to queue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="3e8ca-219">Exina os resultados de teste para ver detalhes sobre a falha.</span><span class="sxs-lookup"><span data-stu-id="3e8ca-219">View the test results to see details about the failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="3e8ca-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3e8ca-220">Next steps</span></span>
<span data-ttu-id="3e8ca-221">Para obter mais informações sobre o teste de unidade no Visual Studio Team Services, consulte [Executar testes de unidade em sua compilação](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span><span class="sxs-lookup"><span data-stu-id="3e8ca-221">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="3e8ca-222">Se você estiver usando o Git, consulte [Compartilhar seu código no Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) e [Implantação contínua para o Serviço de Aplicativo do Azure](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="3e8ca-222">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="3e8ca-223">Para obter mais informações sobre o Visual Studio Team Services, consulte [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="3e8ca-223">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
