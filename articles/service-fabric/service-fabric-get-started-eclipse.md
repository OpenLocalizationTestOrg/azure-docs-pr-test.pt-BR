---
title: aaaAzure Service Fabric plug-in para Eclipse | Microsoft Docs
description: "Introdução ao Olá Service Fabric plug-in para Eclipse."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="6e98f-103">Plug-in do Service Fabric para o desenvolvimento de aplicativos Eclipse Java</span><span class="sxs-lookup"><span data-stu-id="6e98f-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="6e98f-104">Eclipse é uma saudação usada amplamente integrado (IDEs) ambientes de desenvolvimento para desenvolvedores de Java.</span><span class="sxs-lookup"><span data-stu-id="6e98f-104">Eclipse is one of hello most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="6e98f-105">Neste artigo, descreveremos como tooset a sua toowork de ambiente de desenvolvimento do Eclipse com o Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e98f-105">In this article, we describe how tooset up your Eclipse development environment toowork with Azure Service Fabric.</span></span> <span data-ttu-id="6e98f-106">Saiba como tooinstall Olá Service Fabric plug-in, criar um aplicativo de malha do serviço e implantar seu cluster do Service Fabric application tooa local ou remoto do Service Fabric no Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="6e98f-106">Learn how tooinstall hello Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application tooa local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="6e98f-107">Instalar ou atualizar Olá plug-in Eclipse Neon do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6e98f-107">Install or update hello Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="6e98f-108">Você pode instalar um plug-in do Service Fabric no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="6e98f-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="6e98f-109">Olá plug-in pode ajudar a simplificar o processo de saudação da criação e implantação dos serviços de Java.</span><span class="sxs-lookup"><span data-stu-id="6e98f-109">hello plug-in can help simplify hello process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="6e98f-110">Verifique se você tem a versão mais recente de saudação do Eclipse Neon e a versão mais recente de saudação do Buildship (1.0.17 ou uma versão posterior) instalado:</span><span class="sxs-lookup"><span data-stu-id="6e98f-110">Ensure that you have hello latest version of Eclipse Neon and hello latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="6e98f-111">versões de saudação toocheck dos componentes instalados, no Eclipse Neon, ir muito**ajuda** > **detalhes da instalação**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-111">toocheck hello versions of installed components, in Eclipse Neon, go too**Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="6e98f-112">tooupdate Buildship, consulte [Buildship Eclipse: Plug-ins do Eclipse para Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="6e98f-112">tooupdate Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="6e98f-113">toocheck para e instale atualizações para o Eclipse Neon, ir muito**ajuda** > **verificar se há atualizações**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-113">toocheck for and install updates for Eclipse Neon, go too**Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="6e98f-114">Olá tooinstall Service Fabric plug-in no Eclipse Neon, ir muito**ajuda** > **instalar novo Software**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-114">tooinstall hello Service Fabric plug-in, in Eclipse Neon, go too**Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="6e98f-115">Em Olá **trabalhar com** , digite **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-115">In hello **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="6e98f-116">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-116">Click **Add**.</span></span>

         ![Plug-in do Service Fabric para Eclipse Neon][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="6e98f-118">Selecione Olá Service Fabric plug-in e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-118">Select hello Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="6e98f-119">Conclua as etapas de instalação hello e aceite Olá Microsoft Software License Terms.</span><span class="sxs-lookup"><span data-stu-id="6e98f-119">Complete hello installation steps, and then accept hello Microsoft Software License Terms.</span></span>

<span data-ttu-id="6e98f-120">Se você já tiver Olá instalado plug-in do Service Fabric, certifique-se de que você tenha a versão mais recente do hello.</span><span class="sxs-lookup"><span data-stu-id="6e98f-120">If you already have hello Service Fabric plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="6e98f-121">toocheck atualizações disponíveis, vá muito**ajuda** > **detalhes da instalação**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-121">toocheck for available updates, go too**Help** > **Installation Details**.</span></span> <span data-ttu-id="6e98f-122">Na lista de saudação de plug-ins instalados, selecione Serviço de malha e, em seguida, clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-122">In hello list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="6e98f-123">As atualizações disponíveis serão instaladas.</span><span class="sxs-lookup"><span data-stu-id="6e98f-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="6e98f-124">Se instalar ou atualizar Olá plug-in do Service Fabric estiver lenta, pode ser devido a configuração do Eclipse tooan.</span><span class="sxs-lookup"><span data-stu-id="6e98f-124">If installing or updating hello Service Fabric plug-in is slow, it might be due tooan Eclipse setting.</span></span> <span data-ttu-id="6e98f-125">Eclipse coleta metadados em todos os sites de tooupdate alterações que estão registrados com sua instância do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="6e98f-125">Eclipse collects metadata on all changes tooupdate sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="6e98f-126">toospeed processo Olá de verificar e instalar uma atualização de plug-in do Service Fabric, vá muito**locais disponíveis do Software**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-126">toospeed up hello process of checking for and installing a Service Fabric plug-in update, go too**Available Software Sites**.</span></span> <span data-ttu-id="6e98f-127">Desmarque as caixas de seleção de Olá para todos os sites, exceto Olá que aponta local plug-in do Service Fabric do toohello (http://dl.microsoft.com/eclipse/azure/servicefabric).</span><span class="sxs-lookup"><span data-stu-id="6e98f-127">Clear hello check boxes for all sites except for hello one that points toohello Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="6e98f-128">Criar um aplicativo do Service Fabric no Eclipse</span><span class="sxs-lookup"><span data-stu-id="6e98f-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="6e98f-129">No Eclipse Neon, vá muito**arquivo** > **novo** > **outros**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-129">In Eclipse Neon, go too**File** > **New** > **Other**.</span></span> <span data-ttu-id="6e98f-130">Selecione **Projeto do Service Fabric** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Novo Projeto do Service Fabric página 1][create-application/p1]

2.  <span data-ttu-id="6e98f-132">Insira um nome para o projeto e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Novo Projeto do Service Fabric página 2][create-application/p2]

3.  <span data-ttu-id="6e98f-134">Na lista de saudação de modelos, selecione **modelo de serviço**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-134">In hello list of templates, select **Service Template**.</span></span> <span data-ttu-id="6e98f-135">Selecione o tipo de modelo de serviço (Ator, Sem Monitoração de Estado, Contêiner ou Convidado Binário) e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Novo Projeto do Service Fabric página 3][create-application/p3]

4.  <span data-ttu-id="6e98f-137">Insira o nome do serviço hello e detalhes de serviço e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-137">Enter hello service name and service details, and then click **Finish**.</span></span>

    ![Novo Projeto do Service Fabric página 4][create-application/p4]

5. <span data-ttu-id="6e98f-139">Ao criar seu primeiro projeto de serviço de malha, no hello **abrir perspectiva associados** caixa de diálogo, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-139">When you create your first Service Fabric project, in hello **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Novo Projeto do Service Fabric página 5][create-application/p5]

6.  <span data-ttu-id="6e98f-141">O novo projeto tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="6e98f-141">Your new project looks like this:</span></span>

    ![Novo Projeto do Service Fabric página 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="6e98f-143">Criar e implantar um aplicativo do Service Fabric no Eclipse</span><span class="sxs-lookup"><span data-stu-id="6e98f-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="6e98f-144">Clique com o botão direito do mouse no novo aplicativo do Service Fabric e selecione **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Menu de atalho do Service Fabric][publish/RightClick]

2. <span data-ttu-id="6e98f-146">No submenu hello, selecione a opção de saudação desejada:</span><span class="sxs-lookup"><span data-stu-id="6e98f-146">In hello submenu, select hello option you want:</span></span>
    -   <span data-ttu-id="6e98f-147">aplicativo de hello toobuild sem limpeza, clique em **criar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-147">toobuild hello application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="6e98f-148">Clique em toodo uma compilação limpa de aplicativo hello, **recompilar o aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-148">toodo a clean build of hello application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="6e98f-149">aplicativo de hello tooclean de artefatos internos, clique em **aplicativo limpa**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-149">tooclean hello application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="6e98f-150">Nesse menu, você também pode implantar, desimplantar e publicar o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="6e98f-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="6e98f-151">toodeploy tooyour o cluster local, clique em **implantar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-151">toodeploy tooyour local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="6e98f-152">Em Olá **publicar aplicativo** caixa de diálogo, selecione um perfil de publicação:</span><span class="sxs-lookup"><span data-stu-id="6e98f-152">In hello **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="6e98f-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="6e98f-153">**Local.json**</span></span>
        -  <span data-ttu-id="6e98f-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="6e98f-154">**Cloud.json**</span></span>

     <span data-ttu-id="6e98f-155">Esses arquivos de notação JSON (JavaScript Object) armazenam informações (como pontos de extremidade de conexão e informações de segurança) que é necessário tooconnect tooyour local ou cluster de nuvem (Azure).</span><span class="sxs-lookup"><span data-stu-id="6e98f-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required tooconnect tooyour local or cloud (Azure) cluster.</span></span>

  ![Menu Publicar do Service Fabric][publish/Publish]

<span data-ttu-id="6e98f-157">Uma maneira alternativa toodeploy seu aplicativo de malha do serviço está usando o Eclipse executar configurações.</span><span class="sxs-lookup"><span data-stu-id="6e98f-157">An alternate way toodeploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="6e98f-158">Vá muito**executar** > **executar configurações**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-158">Go too**Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="6e98f-159">Em **Gradle projeto**, selecione Olá **ServiceFabricDeployer** configuração de execução.</span><span class="sxs-lookup"><span data-stu-id="6e98f-159">Under **Gradle Project**, select hello **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="6e98f-160">No painel direito hello, em Olá **argumentos** guia, para **publishProfile**, selecione **local** ou **nuvem**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-160">In hello right pane, on hello **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="6e98f-161">saudação padrão é **local**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-161">hello default is **local**.</span></span> <span data-ttu-id="6e98f-162">toodeploy tooa remoto ou cluster de nuvem, selecione **nuvem**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-162">toodeploy tooa remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="6e98f-163">tooensure que informações adequadas de saudação são populadas em Olá perfis de publicação, edite **Local.json** ou **Cloud.json** conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="6e98f-163">tooensure that hello proper information is populated in hello publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="6e98f-164">Você pode adicionar ou atualizar detalhes de ponto de extremidade e credenciais de segurança.</span><span class="sxs-lookup"><span data-stu-id="6e98f-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="6e98f-165">Certifique-se de que **Working Directory** pontos toohello aplicativo deseja toodeploy.</span><span class="sxs-lookup"><span data-stu-id="6e98f-165">Ensure that **Working Directory** points toohello application you want toodeploy.</span></span> <span data-ttu-id="6e98f-166">toochange Olá aplicativo, clique em Olá **espaço de trabalho** botão e, em seguida, selecione o aplicativo hello desejado.</span><span class="sxs-lookup"><span data-stu-id="6e98f-166">toochange hello application, click hello **Workspace** button, and then select hello application you want.</span></span>
  6.    <span data-ttu-id="6e98f-167">Clique em **Aplicar** e em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="6e98f-168">Seu aplicativo será compilado e implantado em poucos instantes.</span><span class="sxs-lookup"><span data-stu-id="6e98f-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="6e98f-169">Você pode monitorar o status da implantação Olá no Gerenciador do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e98f-169">You can monitor hello deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a><span data-ttu-id="6e98f-170">Adicionar um serviço de malha do serviço tooyour aplicativo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6e98f-170">Add a Service Fabric service tooyour Service Fabric application</span></span>

<span data-ttu-id="6e98f-171">Olá tooadd um Service Fabric tooan existente do Service Fabric aplicativo de serviço, as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6e98f-171">tooadd a Service Fabric service tooan existing Service Fabric application, do hello following steps:</span></span>

1.  <span data-ttu-id="6e98f-172">Projeto de Olá atalho você deseja tooadd um serviço e, em seguida, clique em **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-172">Right-click hello project you want tooadd a service to, and then click **Service Fabric**.</span></span>

    ![Adicionar Serviço do Service Fabric Página 1][add-service/p1]

2.  <span data-ttu-id="6e98f-174">Clique em **Adicionar serviço do Service Fabric**, e Olá completo conjunto de etapas tooadd um projeto de toohello de serviço.</span><span class="sxs-lookup"><span data-stu-id="6e98f-174">Click **Add Service Fabric Service**, and complete hello set of steps tooadd a service toohello project.</span></span>
3.  <span data-ttu-id="6e98f-175">Modelo de serviço selecione Olá você deseja tooadd tooyour projeto e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-175">Select hello service template you want tooadd tooyour project, and then click **Next**.</span></span>

    ![Adicionar Serviço do Service Fabric Página 2][add-service/p2]

4.  <span data-ttu-id="6e98f-177">Insira o nome do serviço de saudação (e outros detalhes, conforme necessário) e clique em Olá **Adicionar serviço** botão.</span><span class="sxs-lookup"><span data-stu-id="6e98f-177">Enter hello service name (and other details, as needed), and then click hello **Add Service** button.</span></span>  

    ![Adicionar Serviço do Service Fabric Página 3][add-service/p3]

5.  <span data-ttu-id="6e98f-179">Depois que o serviço Olá é adicionado, a estrutura geral do projeto é semelhante toohello projeto a seguir:</span><span class="sxs-lookup"><span data-stu-id="6e98f-179">After hello service is added, your overall project structure looks similar toohello following project:</span></span>

    ![Adicionar Serviço do Service Fabric Página 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="6e98f-181">Editar versões de manifesto do aplicativo Java do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6e98f-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="6e98f-182">versões de manifesto tooedit, clique com o botão direito do mouse no projeto de Olá, vá muito**Service Fabric** e selecione **editar versões de manifesto...**  de saudação menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="6e98f-182">tooedit manifest versions, right click on hello project, go too**Service Fabric** and select **Edit Manifest Versions...** from hello menu dropdown.</span></span> <span data-ttu-id="6e98f-183">No Assistente de saudação, você pode atualizar Olá versões de manifesto de aplicativo, serviço manifesto e Olá para **código**, **Config** e **dados** pacotes.</span><span class="sxs-lookup"><span data-stu-id="6e98f-183">In hello wizard, you can update hello manifest versions for application manifest, service manifest and hello versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="6e98f-184">Se você marcar a opção de saudação **atualizar automaticamente o aplicativo e as versões de serviço** e, em seguida, uma versão de atualização, versões de manifesto Olá serão atualizadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6e98f-184">If you check hello option **Automatically update application and service versions** and then update a version, then hello manifest versions will be automatically updated.</span></span> <span data-ttu-id="6e98f-185">toogive um exemplo, você primeiro selecionar caixa de seleção hello, em seguida, versão de saudação de atualização do **código** versão de 0.0.0 too0.0.1 e clique em **concluir**, versão do manifesto e o manifesto do aplicativo de serviço, em seguida, versão será too0.0.1 atualizadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6e98f-185">toogive an example, you first select hello check-box, then update hello version of **Code** version from 0.0.0 too0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated too0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="6e98f-186">Atualizar seu aplicativo Java do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6e98f-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="6e98f-187">Para um cenário de atualização, digamos que você criou Olá **App1** projeto usando Olá plug-in Eclipse do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e98f-187">For an upgrade scenario, say you created hello **App1** project by using hello Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="6e98f-188">Você implantá-lo usando toocreate plug-in Olá um aplicativo chamado **fabric: / App1Application**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-188">You deployed it by using hello plug-in toocreate an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="6e98f-189">tipo de aplicativo Hello **App1AppicationType**, e a versão do aplicativo hello é 1.0.</span><span class="sxs-lookup"><span data-stu-id="6e98f-189">hello application type is **App1AppicationType**, and hello application version is 1.0.</span></span> <span data-ttu-id="6e98f-190">Agora, você deseja tooupgrade seu aplicativo sem interromper a disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="6e98f-190">Now, you want tooupgrade your application without interrupting availability.</span></span>

<span data-ttu-id="6e98f-191">Primeiro, faça as alterações de aplicativo tooyour e, em seguida, Olá de reconstrução modificado serviço.</span><span class="sxs-lookup"><span data-stu-id="6e98f-191">First, make any changes tooyour application, and then rebuild hello modified service.</span></span> <span data-ttu-id="6e98f-192">Saudação de atualização modificado (ServiceManifest.xml) do arquivo de manifesto do serviço com versões Olá atualizado para serviço de saudação (e código, configuração ou dados, como relevante).</span><span class="sxs-lookup"><span data-stu-id="6e98f-192">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="6e98f-193">Além disso, modifique o manifesto do aplicativo hello (ApplicationManifest.xml) com número de versão de hello atualizado para o aplicativo hello e Olá serviço modificado.</span><span class="sxs-lookup"><span data-stu-id="6e98f-193">Also, modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application and hello modified service.</span></span>  

<span data-ttu-id="6e98f-194">tooupgrade seu aplicativo usando o Eclipse Neon, você pode criar um perfil de configuração de execução duplicada.</span><span class="sxs-lookup"><span data-stu-id="6e98f-194">tooupgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="6e98f-195">Em seguida, use tooupgrade seu aplicativo conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="6e98f-195">Then, use it tooupgrade your application as needed.</span></span>

1.  <span data-ttu-id="6e98f-196">Vá muito**executar** > **executar configurações**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-196">Go too**Run** > **Run Configurations**.</span></span> <span data-ttu-id="6e98f-197">No painel esquerdo do hello, clique em Olá pequena seta toohello esquerda **Gradle projeto**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-197">In hello left pane, click hello small arrow toohello left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="6e98f-198">Clique com o botão direito do mouse em **ServiceFabricDeployer**e selecione **Duplicar**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="6e98f-199">Digite um novo nome para essa configuração, por exemplo, **ServiceFabricUpgrader**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="6e98f-200">No painel direito hello, em Olá **argumentos** , altere **- Pconfig = 'implantar'** muito**- Pconfig = 'Atualizar'**e, em seguida, clique em **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="6e98f-200">In hello right panel, on hello **Arguments** tab, change **-Pconfig='deploy'** too**-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="6e98f-201">Esse processo cria e salva um perfil de configuração de execução você pode usar em qualquer tempo tooupgrade seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6e98f-201">This process creates and saves a run configuration profile you can use at any time tooupgrade your application.</span></span> <span data-ttu-id="6e98f-202">Ele também obtém última versão de tipo de aplicativo atualizado saudação do arquivo de manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6e98f-202">It also gets hello latest updated application type version from hello application manifest file.</span></span>

<span data-ttu-id="6e98f-203">atualização do aplicativo Hello leva alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="6e98f-203">hello application upgrade takes a few minutes.</span></span> <span data-ttu-id="6e98f-204">Você pode monitorar a atualização do aplicativo hello no Gerenciador do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e98f-204">You can monitor hello application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="6e98f-205">Migrando toobe antigo de aplicativos Java de malha do serviço usado com o Maven</span><span class="sxs-lookup"><span data-stu-id="6e98f-205">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="6e98f-206">Podemos recentemente moveu bibliotecas Java de malha do serviço de repositório de tooMaven do Java SDK do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e98f-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="6e98f-207">Enquanto você gerar usando o Eclipse, novos aplicativos de saudação gerará projetos atualizados mais recente (que serão capaz de toowork com o Maven), você pode atualizar sua malha de serviço existente sem monitoração de estado ou aplicativos Java de ator, que estavam usando Olá SDK de Java do Service Fabric versões anteriores, toouse Olá Java de malha do serviço dependências do Maven.</span><span class="sxs-lookup"><span data-stu-id="6e98f-207">While hello new applications you generate using Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="6e98f-208">Siga as etapas de saudação mencionadas [aqui](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure seu aplicativo mais antigo funciona com o Maven.</span><span class="sxs-lookup"><span data-stu-id="6e98f-208">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
