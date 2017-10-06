---
title: entrega de aaaContinuous com o Visual Studio Team Services no Azure | Microsoft Docs
description: "Saiba como tooconfigure o Visual Studio Team Services projetos da equipe tooautomatically compilar e implantar o recurso de aplicativo Web toohello nos serviços de nuvem ou do serviço de aplicativo do Azure."
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
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a><span data-ttu-id="c239a-103">Fornecimento contínuo tooAzure usando o Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="c239a-103">Continuous delivery tooAzure using Visual Studio Team Services</span></span>
<span data-ttu-id="c239a-104">Você pode configurar sua compilação de tooautomatically de projetos de equipe do Visual Studio Team Services e implantar aplicativos da web de tooAzure ou serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c239a-104">You can configure your Visual Studio Team Services team projects tooautomatically build and deploy tooAzure web apps or cloud services.</span></span>  <span data-ttu-id="c239a-105">(Para obter informações sobre como tooset até uma compilação contínua e implantar o sistema usando uma *local* Team Foundation Server, consulte [entrega contínua para serviços de nuvem no Azure](cloud-services-dotnet-continuous-delivery.md).)</span><span class="sxs-lookup"><span data-stu-id="c239a-105">(For information on how tooset up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="c239a-106">Este tutorial presume que você tenha o Visual Studio 2013 e hello SDK do Azure instalado.</span><span class="sxs-lookup"><span data-stu-id="c239a-106">This tutorial assumes you have Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="c239a-107">Se você ainda não tiver o Visual Studio 2013, baixá-lo escolhendo Olá **comece gratuitamente** link [www.visualstudio.com](http://www.visualstudio.com). Instalar Olá SDK do Azure na [aqui](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="c239a-107">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="c239a-108">É necessário um toocomplete de conta do Visual Studio Team Services este tutorial: você pode [abrir uma conta do Visual Studio Team Services gratuitamente](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="c239a-108">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="c239a-109">tooset a um tooautomatically de serviço de nuvem compilar e implantar tooAzure usando o Visual Studio Team Services, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="c239a-109">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="c239a-110">1: Criar um projeto de equipe</span><span class="sxs-lookup"><span data-stu-id="c239a-110">1: Create a team project</span></span>
<span data-ttu-id="c239a-111">Siga as instruções de saudação [aqui](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate sua equipe de projeto e vinculá-lo tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="c239a-111">Follow hello instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate your team project and link it tooVisual Studio.</span></span> <span data-ttu-id="c239a-112">Este passo a passo pressupõe que você está usando oo Controle de Versão do Team Foundation (TFVC).</span><span class="sxs-lookup"><span data-stu-id="c239a-112">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="c239a-113">Se você quiser toouse Git para controle de versão, consulte [versão de Git Olá deste passo a passo](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="c239a-113">If you want toouse Git for version control, see [hello Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-toosource-control"></a><span data-ttu-id="c239a-114">2: check-in de controle de toosource um projeto</span><span class="sxs-lookup"><span data-stu-id="c239a-114">2: Check in a project toosource control</span></span>
1. <span data-ttu-id="c239a-115">No Visual Studio, abra a solução de saudação desejado toodeploy ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="c239a-115">In Visual Studio, open hello solution you want toodeploy, or create a new one.</span></span>
   <span data-ttu-id="c239a-116">Você pode implantar um aplicativo web ou um serviço de nuvem (aplicativo do Azure) pelo Olá seguir as etapas neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="c239a-116">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span>
   <span data-ttu-id="c239a-117">Se você quiser toocreate uma nova solução, crie um novo projeto de serviço de nuvem do Azure ou um novo projeto ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="c239a-117">If you want toocreate a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="c239a-118">Certifique-se de que Olá destinos do projeto do .NET Framework 4 ou 4.5 e se você estiver criando um projeto de serviço de nuvem, adicionar uma função web do ASP.NET MVC e uma função de trabalho e escolha o aplicativo de Internet para a função da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="c239a-118">Make sure that hello project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for hello web role.</span></span> <span data-ttu-id="c239a-119">Quando solicitado, escolha **Aplicativo da Internet**.</span><span class="sxs-lookup"><span data-stu-id="c239a-119">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="c239a-120">Se você quiser toocreate um aplicativo web, escolha o modelo de projeto de aplicativo Web ASP.NET hello e escolha MVC.</span><span class="sxs-lookup"><span data-stu-id="c239a-120">If you want toocreate a web app, choose hello ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="c239a-121">Consulte [Criar um aplicativo web ASP.NET no Serviço de Aplicativo do Azure](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c239a-121">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c239a-122">O Visual Studio Team Services só suporta implantações de CI de aplicativos Web do Visual Studio no momento.</span><span class="sxs-lookup"><span data-stu-id="c239a-122">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="c239a-123">Projetos de Site estão fora do escopo.</span><span class="sxs-lookup"><span data-stu-id="c239a-123">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="c239a-124">Abra o menu de contexto de saudação para solução de saudação e escolha **tooSource adicionar solução controle**.</span><span class="sxs-lookup"><span data-stu-id="c239a-124">Open hello context menu for hello solution, and choose **Add Solution tooSource Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="c239a-125">Aceitar ou alterar os padrões de saudação e escolha Olá **Okey** botão.</span><span class="sxs-lookup"><span data-stu-id="c239a-125">Accept or change hello defaults and choose hello **OK** button.</span></span> <span data-ttu-id="c239a-126">Após a conclusão do processo de hello, ícones do controle de origem aparecem na **Gerenciador de soluções**.</span><span class="sxs-lookup"><span data-stu-id="c239a-126">Once hello process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="c239a-127">Abra Olá menu de atalho Olá solução e escolha **Check-In**.</span><span class="sxs-lookup"><span data-stu-id="c239a-127">Open hello shortcut menu for hello solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="c239a-128">Em Olá **alterações pendentes** área de **Team Explorer**, digite um comentário para check-in hello e escolha Olá **Check-In** botão.</span><span class="sxs-lookup"><span data-stu-id="c239a-128">In hello **Pending Changes** area of **Team Explorer**, type a comment for hello check-in and choose hello **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="c239a-129">Observação: Olá opções tooinclude ou excluir alterações específicas ao fazer check-in.</span><span class="sxs-lookup"><span data-stu-id="c239a-129">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="c239a-130">Se desejar que as alterações são excluídas, escolha Olá **incluir tudo** link.</span><span class="sxs-lookup"><span data-stu-id="c239a-130">If desired changes are excluded, choose hello **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="c239a-131">3: conectar Olá projeto tooAzure</span><span class="sxs-lookup"><span data-stu-id="c239a-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="c239a-132">Agora que você tiver um projeto de equipe do VS Team Services com algum código-fonte nela, você está pronto tooconnect tooAzure de projeto de equipe.</span><span class="sxs-lookup"><span data-stu-id="c239a-132">Now that you have a VS Team Services team project with some source code in it, you are ready tooconnect your team project tooAzure.</span></span>  <span data-ttu-id="c239a-133">Em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), selecione o aplicativo web ou serviço de nuvem ou crie um novo escolhendo Olá  **+**  ícone na esquerda inferior hello e escolhendo **doserviçodenuvem** ou **aplicativo da Web** e **criação rápida**.</span><span class="sxs-lookup"><span data-stu-id="c239a-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello **+** icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="c239a-134">Escolha Olá **configurar a publicação com o Visual Studio Team Services** link.</span><span class="sxs-lookup"><span data-stu-id="c239a-134">Choose hello **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="c239a-135">No Assistente de Olá, digite o nome de saudação da sua conta do Visual Studio Team Services na caixa de texto de saudação e clique em Olá **autorizar agora** link.</span><span class="sxs-lookup"><span data-stu-id="c239a-135">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and click hello **Authorize Now** link.</span></span> <span data-ttu-id="c239a-136">Você pode ser solicitado toosign no.</span><span class="sxs-lookup"><span data-stu-id="c239a-136">You might be asked toosign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="c239a-137">Em Olá **solicitação de Conexão** caixa de diálogo pop-up, escolha Olá **aceitar** botão tooauthorize tooconfigure do Azure que sua equipe de projeto no VS Team Services.</span><span class="sxs-lookup"><span data-stu-id="c239a-137">In hello **Connection Request** pop-up dialog, choose hello **Accept** button tooauthorize Azure tooconfigure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="c239a-138">Quando a autorização for bem-sucedida, você verá uma lista suspensa que contém uma lista de seus projetos de equipe do Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="c239a-138">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="c239a-139">Escolher nome de saudação do projeto de equipe que você criou nas etapas anteriores hello e, em seguida, escolha o botão de marca de seleção do Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="c239a-139">Choose  hello name of team project that you created in hello previous steps, and then choose hello wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="c239a-140">Depois que o projeto está vinculado, você verá algumas instruções para fazer check-in do projeto de equipe do Visual Studio Team Services de tooyour de alterações.</span><span class="sxs-lookup"><span data-stu-id="c239a-140">After your project is linked, you will see some instructions for checking in changes tooyour Visual Studio Team Services team project.</span></span>  <span data-ttu-id="c239a-141">No próximo check-in, o Visual Studio Team Services criará e implantará tooAzure seu projeto.</span><span class="sxs-lookup"><span data-stu-id="c239a-141">On your next check-in, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>  <span data-ttu-id="c239a-142">Tente agora clicando Olá **Check-In do Visual Studio** link e, em seguida, Olá **iniciar o Visual Studio** link (ou hello equivalente **Visual Studio** botão na parte inferior de saudação do portal tela Hello).</span><span class="sxs-lookup"><span data-stu-id="c239a-142">Try this now by clicking hello **Check In from Visual Studio** link, and then hello **Launch Visual Studio** link (or hello equivalent **Visual Studio** button at hello bottom of hello portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="c239a-143">4: Disparar uma recompilação e reimplantar seu projeto</span><span class="sxs-lookup"><span data-stu-id="c239a-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="c239a-144">No Visual Studio **Team Explorer**, escolha Olá **Gerenciador de controle do código-fonte** link.</span><span class="sxs-lookup"><span data-stu-id="c239a-144">In Visual Studio's **Team Explorer**, choose hello **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="c239a-145">Navegue tooyour o arquivo de solução e abri-lo.</span><span class="sxs-lookup"><span data-stu-id="c239a-145">Navigate tooyour solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="c239a-146">No **Gerenciador de Soluções**, abra um arquivo e altere-o.</span><span class="sxs-lookup"><span data-stu-id="c239a-146">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="c239a-147">Por exemplo, altere o arquivo hello `_Layout.cshtml` em modos de exibição de saudação\\pasta compartilhada em uma função da web MVC.</span><span class="sxs-lookup"><span data-stu-id="c239a-147">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="c239a-148">Editar saudação logotipo para o site de saudação e escolha **Ctrl + S** toosave arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c239a-148">Edit hello logo for hello site and choose **Ctrl+S** toosave hello file.</span></span>
   
    ![][18]
5. <span data-ttu-id="c239a-149">Em **Team Explorer**, escolha Olá **alterações pendentes** link.</span><span class="sxs-lookup"><span data-stu-id="c239a-149">In **Team Explorer**, choose hello **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="c239a-150">Insira um comentário e, em seguida, escolha Olá **Check-In** botão.</span><span class="sxs-lookup"><span data-stu-id="c239a-150">Enter a comment and then choose hello **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="c239a-151">Escolha Olá **inicial** botão tooreturn toohello **Team Explorer** página inicial.</span><span class="sxs-lookup"><span data-stu-id="c239a-151">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="c239a-152">Escolha Olá **cria** saudação do link tooview compilações em andamento.</span><span class="sxs-lookup"><span data-stu-id="c239a-152">Choose hello **Builds** link tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="c239a-153">**Team Explorer** mostra que uma compilação foi disparada para seu check-in.</span><span class="sxs-lookup"><span data-stu-id="c239a-153">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="c239a-154">À medida que avança de compilação Olá, clique duas vezes em nome de saudação do hello compilação em andamento tooview um log detalhado.</span><span class="sxs-lookup"><span data-stu-id="c239a-154">Double-click hello name of hello build in progress tooview a detailed log as hello build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="c239a-155">Enquanto a compilação de saudação está em andamento, dê uma olhada na definição de compilação de saudação que foi criada quando você vinculou tooAzure TFS usando o Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="c239a-155">While hello build is in-progress, take a look at hello build definition that was created when you linked TFS tooAzure by using hello wizard.</span></span>  <span data-ttu-id="c239a-156">Abra o menu de atalho Olá Olá para definição de compilação e escolha **editar definição de compilação**.</span><span class="sxs-lookup"><span data-stu-id="c239a-156">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="c239a-157">Em Olá **gatilho** guia, você verá que definição de compilação de saudação é definida toobuild em cada check-in por padrão.</span><span class="sxs-lookup"><span data-stu-id="c239a-157">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="c239a-158">Em Olá **processo** guia, você pode ver o ambiente de implantação Olá é definido toohello nome do seu aplicativo web ou serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c239a-158">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span> <span data-ttu-id="c239a-159">Se você estiver trabalhando com aplicativos web, propriedades de saudação que verá serão diferentes daqueles mostrados aqui.</span><span class="sxs-lookup"><span data-stu-id="c239a-159">If you are working with web apps, hello properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="c239a-160">Especifica valores para propriedades de saudação se você quiser que os valores diferentes de padrões de saudação.</span><span class="sxs-lookup"><span data-stu-id="c239a-160">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="c239a-161">Olá propriedades de publicação do Azure estão em Olá **implantação** seção.</span><span class="sxs-lookup"><span data-stu-id="c239a-161">hello properties for Azure publishing are in hello **Deployment** section.</span></span>
    
     <span data-ttu-id="c239a-162">Olá tabela a seguir mostra propriedades disponíveis Olá em Olá **implantação** seção:</span><span class="sxs-lookup"><span data-stu-id="c239a-162">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="c239a-163">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c239a-163">Property</span></span> | <span data-ttu-id="c239a-164">Valor Padrão</span><span class="sxs-lookup"><span data-stu-id="c239a-164">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="c239a-165">Permitir certificados não confiáveis</span><span class="sxs-lookup"><span data-stu-id="c239a-165">Allow Untrusted Certificates</span></span> |<span data-ttu-id="c239a-166">Se falso, os certificados SSL deve ser assinados por uma autoridade raiz.</span><span class="sxs-lookup"><span data-stu-id="c239a-166">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="c239a-167">Permitir Atualização</span><span class="sxs-lookup"><span data-stu-id="c239a-167">Allow Upgrade</span></span> |<span data-ttu-id="c239a-168">Olá implantação tooupdate permite que uma implantação existente em vez de criar um novo.</span><span class="sxs-lookup"><span data-stu-id="c239a-168">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="c239a-169">Preserva o endereço IP hello.</span><span class="sxs-lookup"><span data-stu-id="c239a-169">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="c239a-170">Não exclua</span><span class="sxs-lookup"><span data-stu-id="c239a-170">Do Not Delete</span></span> |<span data-ttu-id="c239a-171">Se verdadeiro, não substitua uma implantação não relacionada existente (a atualização é permitida).</span><span class="sxs-lookup"><span data-stu-id="c239a-171">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="c239a-172">Caminho tooDeployment configurações</span><span class="sxs-lookup"><span data-stu-id="c239a-172">Path tooDeployment Settings</span></span> |<span data-ttu-id="c239a-173">Olá caminho tooyour. pubxml arquivo para um aplicativo web, a pasta raiz de toohello relativo do repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="c239a-173">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="c239a-174">Ignorado para serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c239a-174">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="c239a-175">Ambiente de implantação do Sharepoint</span><span class="sxs-lookup"><span data-stu-id="c239a-175">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="c239a-176">Olá mesmo como o nome do serviço hello.</span><span class="sxs-lookup"><span data-stu-id="c239a-176">hello same as hello service name.</span></span> |
    | <span data-ttu-id="c239a-177">Ambiente de implantação do Azure</span><span class="sxs-lookup"><span data-stu-id="c239a-177">Azure Deployment Environment</span></span> |<span data-ttu-id="c239a-178">Olá aplicativo ou nuvem nome do serviço web.</span><span class="sxs-lookup"><span data-stu-id="c239a-178">hello web app or cloud service name.</span></span> |
12. <span data-ttu-id="c239a-179">Se você estiver usando várias configurações de serviço (arquivos. cscfg), você pode especificar a configuração de serviço desejado de saudação em Olá **compilar, Avançado, argumentos de MSBuild** configuração.</span><span class="sxs-lookup"><span data-stu-id="c239a-179">If you are using multiple service configurations (.cscfg files), you can specify hello desired service configuration in hello **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="c239a-180">Por exemplo, toouse ServiceConfiguration.Test.cscfg, defina os argumentos de MSBuild opção de linha de `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="c239a-180">For example, toouse ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="c239a-181">A essa altura, sua compilação deve estar concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="c239a-181">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="c239a-182">Se você clicar duas vezes nome de compilação hello, o Visual Studio mostra uma **Resumo da compilação**, incluindo os resultados dos testes de associadas a projetos de teste de unidade.</span><span class="sxs-lookup"><span data-stu-id="c239a-182">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="c239a-183">Em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), você pode exibir a implantação de saudação associada em Olá **implantações** guia quando Olá ambiente de preparo é selecionado.</span><span class="sxs-lookup"><span data-stu-id="c239a-183">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="c239a-184">Procure tooyour URL do seu site.</span><span class="sxs-lookup"><span data-stu-id="c239a-184">Browse tooyour site's URL.</span></span> <span data-ttu-id="c239a-185">Para um aplicativo web, basta clicar Olá **procurar** botão na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="c239a-185">For a web app, just click hello **Browse** button on hello command bar.</span></span> <span data-ttu-id="c239a-186">De um serviço de nuvem, escolha URL Olá Olá **rápidos** seção Olá **painel** página que mostra o ambiente de preparo de saudação para um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c239a-186">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment for a cloud service.</span></span> <span data-ttu-id="c239a-187">As implantações de integração contínua para serviços de nuvem são publicados toohello ambiente de preparo por padrão.</span><span class="sxs-lookup"><span data-stu-id="c239a-187">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="c239a-188">Você pode alterar essa configuração Olá **ambiente de serviço de nuvem alternativo** propriedade muito**produção**.</span><span class="sxs-lookup"><span data-stu-id="c239a-188">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="c239a-189">Esta captura de tela mostra onde hello URL do site na página do painel do serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="c239a-189">This screenshot shows where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="c239a-190">Uma nova guia do navegador será aberto tooreveal seu site em execução.</span><span class="sxs-lookup"><span data-stu-id="c239a-190">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="c239a-191">Para serviços de nuvem, se você fizer a outro projeto de tooyour alterações, você gatilho mais cria e acumularão várias implantações.</span><span class="sxs-lookup"><span data-stu-id="c239a-191">For cloud services, if you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="c239a-192">Hello mais recente marcado como ativo.</span><span class="sxs-lookup"><span data-stu-id="c239a-192">hello latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="c239a-193">5: Reimplantar um build anterior</span><span class="sxs-lookup"><span data-stu-id="c239a-193">5: Redeploy an earlier build</span></span>
<span data-ttu-id="c239a-194">Essa etapa se aplica a serviços toocloud e é opcional.</span><span class="sxs-lookup"><span data-stu-id="c239a-194">This step applies toocloud services and is optional.</span></span> <span data-ttu-id="c239a-195">Em Olá portal clássico do Azure, escolha uma implantação anterior e Olá **reimplantar** botão toorewind tooan seu site anteriormente check-in.</span><span class="sxs-lookup"><span data-stu-id="c239a-195">In hello Azure classic portal, choose an earlier deployment and then choose hello **Redeploy** button toorewind your site tooan earlier check-in.</span></span>  <span data-ttu-id="c239a-196">Observe que isso vai disparar uma nova compilação no TFS e criará uma nova entrada em seu histórico de implantação.</span><span class="sxs-lookup"><span data-stu-id="c239a-196">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="c239a-197">6: alterar a implantação de produção de hello</span><span class="sxs-lookup"><span data-stu-id="c239a-197">6: Change hello Production deployment</span></span>
<span data-ttu-id="c239a-198">Essa etapa se aplica apenas o toocloud serviços, não os aplicativos web.</span><span class="sxs-lookup"><span data-stu-id="c239a-198">This step applies only toocloud services, not web apps.</span></span> <span data-ttu-id="c239a-199">Quando estiver pronto, você pode promover Olá preparo toohello ambiente de produção, escolhendo Olá **trocar** botão Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="c239a-199">When you are ready, you can promote hello Staging environment toohello production environment by choosing hello **Swap** button in hello Azure classic portal.</span></span> <span data-ttu-id="c239a-200">ambiente de preparo Olá implantado recentemente é promovida tooProduction e ambiente de produção anterior hello, se houver, torna-se um ambiente de preparo.</span><span class="sxs-lookup"><span data-stu-id="c239a-200">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="c239a-201">Olá implantação ativa pode ser diferente para ambientes de preparo e produção de hello, mas o histórico de implantação de saudação de builds recentes é Olá mesmo independentemente do ambiente.</span><span class="sxs-lookup"><span data-stu-id="c239a-201">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="c239a-202">7: Executar testes de unidade</span><span class="sxs-lookup"><span data-stu-id="c239a-202">7: Run unit tests</span></span>
<span data-ttu-id="c239a-203">Essa etapa se aplica a aplicativos de tooweb apenas, não os serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c239a-203">This step applies only tooweb apps, not cloud services.</span></span> <span data-ttu-id="c239a-204">tooput um portão de qualidade na sua implantação, você pode executar testes de unidade e se elas falharem, você pode interromper a implantação hello.</span><span class="sxs-lookup"><span data-stu-id="c239a-204">tooput a quality gate on your deployment, you can run unit tests and if they fail, you can stop hello deployment.</span></span>

1. <span data-ttu-id="c239a-205">No Visual Studio, adicione um projeto de teste de unidade.</span><span class="sxs-lookup"><span data-stu-id="c239a-205">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="c239a-206">Adicione projeto de toohello de referências de projeto você deseja tootest.</span><span class="sxs-lookup"><span data-stu-id="c239a-206">Add project references toohello project you want tootest.</span></span>
   
   ![][40]
3. <span data-ttu-id="c239a-207">Adicione alguns testes de unidade.</span><span class="sxs-lookup"><span data-stu-id="c239a-207">Add some unit tests.</span></span> <span data-ttu-id="c239a-208">tooget iniciado, tente um teste fictício que sempre seja aprovado.</span><span class="sxs-lookup"><span data-stu-id="c239a-208">tooget started, try a dummy test that will always pass.</span></span>
   
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
4. <span data-ttu-id="c239a-209">Editar definição de compilação hello, escolha Olá **processo** guia e, em seguida, expanda Olá **teste** nó.</span><span class="sxs-lookup"><span data-stu-id="c239a-209">Edit hello build definition, choose hello **Process** tab, and expand hello **Test** node.</span></span>
5. <span data-ttu-id="c239a-210">Saudação de conjunto **falhar compilação em caso de falha do teste** tooTrue.</span><span class="sxs-lookup"><span data-stu-id="c239a-210">Set hello **Fail build on test failure** tooTrue.</span></span> <span data-ttu-id="c239a-211">Isso significa que a implantação de Olá não ocorreu, a menos que Olá testes foram bem-sucedidos.</span><span class="sxs-lookup"><span data-stu-id="c239a-211">This means that hello deployment won't occur unless hello tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="c239a-212">Fila de uma nova compilação.</span><span class="sxs-lookup"><span data-stu-id="c239a-212">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="c239a-213">Enquanto está procedendo compilação hello, verifica seu andamento.</span><span class="sxs-lookup"><span data-stu-id="c239a-213">While hello build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="c239a-214">Quando terminar de compilação hello, verifique os resultados de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="c239a-214">When hello build is done, check hello test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="c239a-215">Tente criar um teste que falhará.</span><span class="sxs-lookup"><span data-stu-id="c239a-215">Try creating a test that will fail.</span></span> <span data-ttu-id="c239a-216">Adicione um novo teste copiando Olá primeiro, renomeá-lo e comentar a linha hello de código que afirma que NotImplementedException é uma exceção não esperada.</span><span class="sxs-lookup"><span data-stu-id="c239a-216">Add a new test by copying hello first one, rename it, and comment out hello line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="c239a-217">Check-in Olá alterar tooqueue uma nova compilação.</span><span class="sxs-lookup"><span data-stu-id="c239a-217">Check in hello change tooqueue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="c239a-218">Exibir detalhes toosee dos resultados do teste Olá sobre falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="c239a-218">View hello test results toosee details about hello failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="c239a-219">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c239a-219">Next steps</span></span>
<span data-ttu-id="c239a-220">Para obter mais informações sobre o teste de unidade no Visual Studio Team Services, consulte [Executar testes de unidade em sua compilação](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span><span class="sxs-lookup"><span data-stu-id="c239a-220">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="c239a-221">Se você estiver usando o Git, consulte [compartilhar seu código no Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) e [tooAzure implantação contínua do serviço de aplicativo](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="c239a-221">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="c239a-222">Para obter mais informações sobre o Visual Studio Team Services, consulte [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="c239a-222">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
