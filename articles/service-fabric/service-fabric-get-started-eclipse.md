---
title: Plug-in do Service Fabric do Azure para Eclipse | Microsoft Docs
description: Comece a usar o plug-in do Service Fabric para Eclipse.
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
ms.openlocfilehash: 98c1b99972b9ad7a396d72b98e727286f6822e42
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="8015c-103">Plug-in do Service Fabric para o desenvolvimento de aplicativos Eclipse Java</span><span class="sxs-lookup"><span data-stu-id="8015c-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="8015c-104">O Eclipse é um dos IDEs (ambientes de desenvolvimento integrado) mais amplamente usados para desenvolvedores de Java.</span><span class="sxs-lookup"><span data-stu-id="8015c-104">Eclipse is one of the most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="8015c-105">Neste artigo, descreveremos como configurar seu ambiente de desenvolvimento do Eclipse para trabalhar com o Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8015c-105">In this article, we describe how to set up your Eclipse development environment to work with Azure Service Fabric.</span></span> <span data-ttu-id="8015c-106">Saiba como instalar o plug-in do Service Fabric, criar um aplicativo do Service Fabric e implantar o aplicativo do Service Fabric em um cluster do Service Fabric local ou remoto no Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="8015c-106">Learn how to install the Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application to a local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-the-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="8015c-107">Instalar ou atualizar o plug-in do Service Fabric no Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="8015c-107">Install or update the Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="8015c-108">Você pode instalar um plug-in do Service Fabric no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8015c-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="8015c-109">O plug-in pode ajudar a simplificar o processo de criação e implantação de serviços Java.</span><span class="sxs-lookup"><span data-stu-id="8015c-109">The plug-in can help simplify the process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="8015c-110">Verifique se você tem a versão mais recente do Eclipse Neon e a versão mais recente do Buildship (1.0.17 ou uma versão posterior) instalado:</span><span class="sxs-lookup"><span data-stu-id="8015c-110">Ensure that you have the latest version of Eclipse Neon and the latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="8015c-111">Para verificar as versões dos componentes instalados, no Eclipse Neon, acesse **Ajuda** > **Detalhes da Instalação**.</span><span class="sxs-lookup"><span data-stu-id="8015c-111">To check the versions of installed components, in Eclipse Neon, go to **Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="8015c-112">Para atualizar o Buildship, confira [Eclipse Buildship: plug-ins do Eclipse para Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="8015c-112">To update Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="8015c-113">Para verificar e instalar atualizações para o Eclipse Neon, acesse **Ajuda** > **Verificar se Há Atualizações**.</span><span class="sxs-lookup"><span data-stu-id="8015c-113">To check for and install updates for Eclipse Neon, go to **Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="8015c-114">Para instalar o plug-in do Service Fabric, no Eclipse Neon, acesse **Ajuda** > **Instalar Novo Software**.</span><span class="sxs-lookup"><span data-stu-id="8015c-114">To install the Service Fabric plug-in, in Eclipse Neon, go to **Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="8015c-115">Na caixa de texto **Trabalhar com**, digite: **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="8015c-115">In the **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="8015c-116">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8015c-116">Click **Add**.</span></span>

         ![Plug-in do Service Fabric para Eclipse Neon][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="8015c-118">Selecione o plug-in do Service Fabric e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8015c-118">Select the Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="8015c-119">Conclua as etapas de instalação e aceite os Termos de Licença de Software da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8015c-119">Complete the installation steps, and then accept the Microsoft Software License Terms.</span></span>

<span data-ttu-id="8015c-120">Se já tiver o plug-in do Service Fabric instalado, verifique se você tem a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="8015c-120">If you already have the Service Fabric plug-in installed, make sure that you have the latest version.</span></span> <span data-ttu-id="8015c-121">Para verificar se há atualizações disponíveis, acesse **Ajuda** > **Detalhes da Instalação**.</span><span class="sxs-lookup"><span data-stu-id="8015c-121">To check for available updates, go to **Help** > **Installation Details**.</span></span> <span data-ttu-id="8015c-122">Na lista de plug-ins instalados, selecione o Service Fabric e clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="8015c-122">In the list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="8015c-123">As atualizações disponíveis serão instaladas.</span><span class="sxs-lookup"><span data-stu-id="8015c-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="8015c-124">Se a instalação ou atualização do plug-in do Service Fabric estiver lenta, isso poderá ser devido a uma configuração do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8015c-124">If installing or updating the Service Fabric plug-in is slow, it might be due to an Eclipse setting.</span></span> <span data-ttu-id="8015c-125">O Eclipse coleta metadados sobre todas as alterações para atualizar sites que estão registrados com a instância do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8015c-125">Eclipse collects metadata on all changes to update sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="8015c-126">Para acelerar o processo de verificar e instalar uma atualização de plug-in do Service Fabric, acesse **Sites de Software Disponível**.</span><span class="sxs-lookup"><span data-stu-id="8015c-126">To speed up the process of checking for and installing a Service Fabric plug-in update, go to **Available Software Sites**.</span></span> <span data-ttu-id="8015c-127">Desmarque as caixas de seleção de todos os sites, exceto aquele que aponta para o local do plug-in do Service Fabric (http://dl.microsoft.com/eclipse/azure/servicefabric).</span><span class="sxs-lookup"><span data-stu-id="8015c-127">Clear the check boxes for all sites except for the one that points to the Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="8015c-128">Criar um aplicativo do Service Fabric no Eclipse</span><span class="sxs-lookup"><span data-stu-id="8015c-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="8015c-129">No Eclipse Neon, acesse **Arquivo** > **Novo** > **Outros**.</span><span class="sxs-lookup"><span data-stu-id="8015c-129">In Eclipse Neon, go to **File** > **New** > **Other**.</span></span> <span data-ttu-id="8015c-130">Selecione **Projeto do Service Fabric** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8015c-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Novo Projeto do Service Fabric página 1][create-application/p1]

2.  <span data-ttu-id="8015c-132">Insira um nome para o projeto e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8015c-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Novo Projeto do Service Fabric página 2][create-application/p2]

3.  <span data-ttu-id="8015c-134">Na lista de modelos, selecione **Modelo de Serviço**.</span><span class="sxs-lookup"><span data-stu-id="8015c-134">In the list of templates, select **Service Template**.</span></span> <span data-ttu-id="8015c-135">Selecione o tipo de modelo de serviço (Ator, Sem Monitoração de Estado, Contêiner ou Convidado Binário) e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8015c-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Novo Projeto do Service Fabric página 3][create-application/p3]

4.  <span data-ttu-id="8015c-137">Insira os detalhes e o nome do serviço e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="8015c-137">Enter the service name and service details, and then click **Finish**.</span></span>

    ![Novo Projeto do Service Fabric página 4][create-application/p4]

5. <span data-ttu-id="8015c-139">Ao criar seu primeiro projeto do Service Fabric, na caixa de diálogo **Abrir Perspectiva Associada**, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="8015c-139">When you create your first Service Fabric project, in the **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Novo Projeto do Service Fabric página 5][create-application/p5]

6.  <span data-ttu-id="8015c-141">O novo projeto tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="8015c-141">Your new project looks like this:</span></span>

    ![Novo Projeto do Service Fabric página 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="8015c-143">Criar e implantar um aplicativo do Service Fabric no Eclipse</span><span class="sxs-lookup"><span data-stu-id="8015c-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="8015c-144">Clique com o botão direito do mouse no novo aplicativo do Service Fabric e selecione **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="8015c-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Menu de atalho do Service Fabric][publish/RightClick]

2. <span data-ttu-id="8015c-146">No submenu, selecione a opção desejada:</span><span class="sxs-lookup"><span data-stu-id="8015c-146">In the submenu, select the option you want:</span></span>
    -   <span data-ttu-id="8015c-147">Para compilar o aplicativo sem limpeza, clique em **Compilar Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="8015c-147">To build the application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="8015c-148">Para fazer uma compilação limpa do aplicativo, clique em **Recompilar o Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="8015c-148">To do a clean build of the application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="8015c-149">Para limpar a aplicação de artefatos compilados, clique em **Limpar Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="8015c-149">To clean the application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="8015c-150">Nesse menu, você também pode implantar, desimplantar e publicar o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="8015c-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="8015c-151">Para implantar no cluster local, clique em **Implantar Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="8015c-151">To deploy to your local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="8015c-152">Na caixa de diálogo **Publicar Aplicativo**, selecione um perfil de publicação:</span><span class="sxs-lookup"><span data-stu-id="8015c-152">In the **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="8015c-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="8015c-153">**Local.json**</span></span>
        -  <span data-ttu-id="8015c-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="8015c-154">**Cloud.json**</span></span>

     <span data-ttu-id="8015c-155">Esses arquivos JSON (JavaScript Object Notation) armazenam informações (como pontos de extremidade de conexão e informações de segurança) que são necessárias para se conectar ao cluster local ou de nuvem (Azure).</span><span class="sxs-lookup"><span data-stu-id="8015c-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required to connect to your local or cloud (Azure) cluster.</span></span>

  ![Menu Publicar do Service Fabric][publish/Publish]

<span data-ttu-id="8015c-157">Uma maneira alternativa de implantar o aplicativo do Service Fabric é usar as configurações de execução do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8015c-157">An alternate way to deploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="8015c-158">Acesse **Executar** > **Configurações de Execução**.</span><span class="sxs-lookup"><span data-stu-id="8015c-158">Go to **Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="8015c-159">Em **Projeto do Gradle**, selecione a configuração de execução **ServiceFabricDeployer**.</span><span class="sxs-lookup"><span data-stu-id="8015c-159">Under **Gradle Project**, select the **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="8015c-160">No painel direito, na guia **Argumentos**, para **publishProfile**, selecione **local** ou **nuvem**.</span><span class="sxs-lookup"><span data-stu-id="8015c-160">In the right pane, on the **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="8015c-161">O padrão é **local**.</span><span class="sxs-lookup"><span data-stu-id="8015c-161">The default is **local**.</span></span> <span data-ttu-id="8015c-162">Para implantar em um computador remoto ou cluster de nuvem, selecione **nuvem**.</span><span class="sxs-lookup"><span data-stu-id="8015c-162">To deploy to a remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="8015c-163">Para garantir que as informações adequadas sejam preenchidas nos perfis de publicação, edite **Local.json** ou **Cloud.json** conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="8015c-163">To ensure that the proper information is populated in the publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="8015c-164">Você pode adicionar ou atualizar detalhes de ponto de extremidade e credenciais de segurança.</span><span class="sxs-lookup"><span data-stu-id="8015c-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="8015c-165">Verifique se **Diretório de Trabalho** aponta para o aplicativo que você deseja implantar.</span><span class="sxs-lookup"><span data-stu-id="8015c-165">Ensure that **Working Directory** points to the application you want to deploy.</span></span> <span data-ttu-id="8015c-166">Para alterar o aplicativo, clique no botão **Espaço de trabalho** e selecione o aplicativo desejado.</span><span class="sxs-lookup"><span data-stu-id="8015c-166">To change the application, click the **Workspace** button, and then select the application you want.</span></span>
  6.    <span data-ttu-id="8015c-167">Clique em **Aplicar** e em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="8015c-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="8015c-168">Seu aplicativo será compilado e implantado em poucos instantes.</span><span class="sxs-lookup"><span data-stu-id="8015c-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="8015c-169">Você pode monitorar o status da implantação no Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="8015c-169">You can monitor the deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-to-your-service-fabric-application"></a><span data-ttu-id="8015c-170">Adicionar um serviço do Service Fabric ao aplicativo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8015c-170">Add a Service Fabric service to your Service Fabric application</span></span>

<span data-ttu-id="8015c-171">Para adicionar um serviço do Service Fabric a um aplicativo do Service Fabric existente, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="8015c-171">To add a Service Fabric service to an existing Service Fabric application, do the following steps:</span></span>

1.  <span data-ttu-id="8015c-172">Clique com o botão direito do mouse no projeto ao qual você deseja adicionar um serviço e clique no **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="8015c-172">Right-click the project you want to add a service to, and then click **Service Fabric**.</span></span>

    ![Adicionar Serviço do Service Fabric Página 1][add-service/p1]

2.  <span data-ttu-id="8015c-174">Clique em **Adicionar Serviço do Service Fabric**e conclua o conjunto de etapas para adicionar um serviço ao projeto.</span><span class="sxs-lookup"><span data-stu-id="8015c-174">Click **Add Service Fabric Service**, and complete the set of steps to add a service to the project.</span></span>
3.  <span data-ttu-id="8015c-175">Selecione o modelo de serviço que você deseja adicionar ao projeto e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8015c-175">Select the service template you want to add to your project, and then click **Next**.</span></span>

    ![Adicionar Serviço do Service Fabric Página 2][add-service/p2]

4.  <span data-ttu-id="8015c-177">Insira o nome do serviço (e outros detalhes, conforme necessário) e clique no botão **Adicionar Serviço**.</span><span class="sxs-lookup"><span data-stu-id="8015c-177">Enter the service name (and other details, as needed), and then click the **Add Service** button.</span></span>  

    ![Adicionar Serviço do Service Fabric Página 3][add-service/p3]

5.  <span data-ttu-id="8015c-179">Depois que o serviço é adicionado, a estrutura geral do projeto é semelhante ao seguinte projeto:</span><span class="sxs-lookup"><span data-stu-id="8015c-179">After the service is added, your overall project structure looks similar to the following project:</span></span>

    ![Adicionar Serviço do Service Fabric Página 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="8015c-181">Editar versões de manifesto do aplicativo Java do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8015c-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="8015c-182">Para editar versões de manifesto, clique o botão direito no projeto, acesse **Service Fabric** e selecione **Editar versões de manifesto...**  do menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="8015c-182">To edit manifest versions, right click on the project, go to **Service Fabric** and select **Edit Manifest Versions...** from the menu dropdown.</span></span> <span data-ttu-id="8015c-183">No assistente, você pode atualizar as versões de manifesto para o manifesto do aplicativo, o manifesto do serviço e as versões para o **código**, **Config** e pacotes de **dados**.</span><span class="sxs-lookup"><span data-stu-id="8015c-183">In the wizard, you can update the manifest versions for application manifest, service manifest and the versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="8015c-184">Se você marcar a opção **atualizar automaticamente o aplicativo e as versões de serviço** e, em seguida, atualizar uma versão, as versões de manifesto serão atualizadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8015c-184">If you check the option **Automatically update application and service versions** and then update a version, then the manifest versions will be automatically updated.</span></span> <span data-ttu-id="8015c-185">Para dar um exemplo, primeiro selecione a caixa de seleção, e atualize a versão do **código** de 0.0.0 para 0.0.1 e clique em **Concluir**, em seguida, a versão do manifesto do serviço e a versão do manifesto do aplicativo serão atualizadas automaticamente para 0.0.1.</span><span class="sxs-lookup"><span data-stu-id="8015c-185">To give an example, you first select the check-box, then update the version of **Code** version from 0.0.0 to 0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated to 0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="8015c-186">Atualizar seu aplicativo Java do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8015c-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="8015c-187">Para um cenário de atualização, digamos que você tenha criado o projeto **App1** usando o plug-in do Service Fabric do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8015c-187">For an upgrade scenario, say you created the **App1** project by using the Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="8015c-188">Você o implantou usando o plug-in para criar um aplicativo chamado **fabric:/App1Application**.</span><span class="sxs-lookup"><span data-stu-id="8015c-188">You deployed it by using the plug-in to create an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="8015c-189">O tipo de aplicativo é **App1AppicationType** e a versão do aplicativo é 1.0.</span><span class="sxs-lookup"><span data-stu-id="8015c-189">The application type is **App1AppicationType**, and the application version is 1.0.</span></span> <span data-ttu-id="8015c-190">Agora, você deseja atualizar o aplicativo sem interromper a disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="8015c-190">Now, you want to upgrade your application without interrupting availability.</span></span>

<span data-ttu-id="8015c-191">Primeiro, faça as alterações no aplicativo e recrie o serviço modificado.</span><span class="sxs-lookup"><span data-stu-id="8015c-191">First, make any changes to your application, and then rebuild the modified service.</span></span> <span data-ttu-id="8015c-192">Atualize o arquivo de manifesto do serviço modificado (ServiceManifest.xml) com as versões atualizadas para o serviço (e Código, Configuração ou Dados, conforme relevante).</span><span class="sxs-lookup"><span data-stu-id="8015c-192">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="8015c-193">Modifique também o manifesto do aplicativo (ApplicationManifest.xml) com o número da versão atualizada do aplicativo e o serviço modificado.</span><span class="sxs-lookup"><span data-stu-id="8015c-193">Also, modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application and the modified service.</span></span>  

<span data-ttu-id="8015c-194">Para atualizar o aplicativo usando o Eclipse Neon, você pode criar um perfil de configuração de execução duplicada.</span><span class="sxs-lookup"><span data-stu-id="8015c-194">To upgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="8015c-195">Em seguida, use-o para atualizar o aplicativo conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="8015c-195">Then, use it to upgrade your application as needed.</span></span>

1.  <span data-ttu-id="8015c-196">Acesse **Executar** > **Configurações de Execução**.</span><span class="sxs-lookup"><span data-stu-id="8015c-196">Go to **Run** > **Run Configurations**.</span></span> <span data-ttu-id="8015c-197">No painel esquerdo, clique na seta pequena à esquerda de **Projeto do Gradle**.</span><span class="sxs-lookup"><span data-stu-id="8015c-197">In the left pane, click the small arrow to the left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="8015c-198">Clique com o botão direito do mouse em **ServiceFabricDeployer**e selecione **Duplicar**.</span><span class="sxs-lookup"><span data-stu-id="8015c-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="8015c-199">Digite um novo nome para essa configuração, por exemplo, **ServiceFabricUpgrader**.</span><span class="sxs-lookup"><span data-stu-id="8015c-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="8015c-200">No painel direito, na guia **Argumentos**, altere **-Pconfig='deploy'** para **-Pconfig='upgrade'**e clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="8015c-200">In the right panel, on the **Arguments** tab, change **-Pconfig='deploy'** to **-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="8015c-201">Esse processo cria e salva um perfil de configuração de execução que você pode usar a qualquer momento para atualizar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8015c-201">This process creates and saves a run configuration profile you can use at any time to upgrade your application.</span></span> <span data-ttu-id="8015c-202">Também obtém a versão mais recente do tipo de aplicativo atualizado do arquivo de manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8015c-202">It also gets the latest updated application type version from the application manifest file.</span></span>

<span data-ttu-id="8015c-203">A atualização do aplicativo leva alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="8015c-203">The application upgrade takes a few minutes.</span></span> <span data-ttu-id="8015c-204">Você pode monitorar a atualização do aplicativo no Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="8015c-204">You can monitor the application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-to-be-used-with-maven"></a><span data-ttu-id="8015c-205">Migrando os antigos aplicativos Java do Service Fabric para serem usados com o Maven</span><span class="sxs-lookup"><span data-stu-id="8015c-205">Migrating old Service Fabric Java applications to be used with Maven</span></span>
<span data-ttu-id="8015c-206">Recentemente, movemos as bibliotecas Java do Service Fabric do SDK Java do Service Fabric para o repositório Maven.</span><span class="sxs-lookup"><span data-stu-id="8015c-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK to Maven repository.</span></span> <span data-ttu-id="8015c-207">Embora os novos aplicativos gerados usando o Eclipse gerem projetos atualizados mais recentes (que serão capazes de trabalhar com o Maven), você poderá atualizar os aplicativos Java sem estado ou do ator existentes do Service Fabric, que estavam usando o SDK Java do Service Fabric antes, para usar as dependências Java do Service Fabric a partir do Maven.</span><span class="sxs-lookup"><span data-stu-id="8015c-207">While the new applications you generate using Eclipse, will generate latest updated projects (which will be able to work with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using the Service Fabric Java SDK earlier, to use the Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="8015c-208">Siga as etapas mencionadas [aqui](service-fabric-migrate-old-javaapp-to-use-maven.md) para garantir o funcionamento do seu aplicativo mais antigo com o Maven.</span><span class="sxs-lookup"><span data-stu-id="8015c-208">Please follow the steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) to ensure your older application works with Maven.</span></span>

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
