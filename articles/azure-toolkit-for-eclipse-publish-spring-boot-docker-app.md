---
title: "Olá de aaaPublish um aplicativo de inicialização de Spring como um contêiner do Docker usando o Kit de ferramentas do Azure para Eclipse | Microsoft Docs"
description: "Saiba como toopublish uma tooMicrosoft de aplicativo web do Azure como um contêiner do Docker usando Olá Kit de ferramentas do Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="a0902-103">Publicar um aplicativo de inicialização de Spring como um contêiner do Docker usando Olá Kit de ferramentas do Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="a0902-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="a0902-104">Olá [Spring Framework] é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="a0902-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="a0902-105">Um dos projetos mais populares de saudação que é criado em cima dessa plataforma é [Spring inicialização], que fornece um método simplificado para criação de aplicativos Java autônomo.</span><span class="sxs-lookup"><span data-stu-id="a0902-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="a0902-106">[Docker] é uma solução de software livre que ajuda os desenvolvedores a automatizar a implantação de hello, o dimensionamento e o gerenciamento de seus aplicativos que são executados em contêineres.</span><span class="sxs-lookup"><span data-stu-id="a0902-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="a0902-107">Este tutorial orienta Olá etapas toodeploy um aplicativo de inicialização de Spring como um contêiner de Docker tooMicrosoft do Azure usando Olá Kit de ferramentas do Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a0902-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a><span data-ttu-id="a0902-108">Clonar saudação padrão Spring inicialização Docker repositório</span><span class="sxs-lookup"><span data-stu-id="a0902-108">Clone hello default Spring Boot Docker repository</span></span>

### <a name="import-hello-public-repository"></a><span data-ttu-id="a0902-109">Repositório público de saudação de importação</span><span class="sxs-lookup"><span data-stu-id="a0902-109">Import hello public repository</span></span>

<span data-ttu-id="a0902-110">Olá etapas a seguir orientam você durante a clonagem do computador local do hello Spring inicialização Docker repositório tooyour usando IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="a0902-110">hello following steps walk you through cloning hello Spring Boot Docker repository tooyour local computer by using IntelliJ.</span></span> <span data-ttu-id="a0902-111">Se você quiser toouse uma linha de comando, consulte [implantar um aplicativo de inicialização de Spring no Linux no serviço de contêiner do Azure][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="a0902-111">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="a0902-112">Abra o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a0902-112">Open Eclipse.</span></span>

1. <span data-ttu-id="a0902-113">Clique em **Arquivo** > **Importar**.</span><span class="sxs-lookup"><span data-stu-id="a0902-113">Click **File** > **Import**.</span></span>

   ![Menu de Importação de Arquivo][CL01]

1. <span data-ttu-id="a0902-115">Olá quando **importação** abre a caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="a0902-115">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="a0902-116">a.</span><span class="sxs-lookup"><span data-stu-id="a0902-116">a.</span></span> <span data-ttu-id="a0902-117">Expanda **Git**.</span><span class="sxs-lookup"><span data-stu-id="a0902-117">Expand **Git**.</span></span>

   <span data-ttu-id="a0902-118">b.</span><span class="sxs-lookup"><span data-stu-id="a0902-118">b.</span></span> <span data-ttu-id="a0902-119">Selecione **Projetos do Git**.</span><span class="sxs-lookup"><span data-stu-id="a0902-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="a0902-120">c.</span><span class="sxs-lookup"><span data-stu-id="a0902-120">c.</span></span> <span data-ttu-id="a0902-121">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a0902-121">Click **Next**.</span></span>

   ![Caixa de diálogo de Importação][CL02]

1. <span data-ttu-id="a0902-123">Em Olá **Selecionar origem de repositório** página:</span><span class="sxs-lookup"><span data-stu-id="a0902-123">On hello **Select Repository Source** page:</span></span>

   <span data-ttu-id="a0902-124">a.</span><span class="sxs-lookup"><span data-stu-id="a0902-124">a.</span></span> <span data-ttu-id="a0902-125">Selecione **Clonar URI**.</span><span class="sxs-lookup"><span data-stu-id="a0902-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="a0902-126">b.</span><span class="sxs-lookup"><span data-stu-id="a0902-126">b.</span></span> <span data-ttu-id="a0902-127">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a0902-127">Click **Next**.</span></span>

   ![Página Selecionar Origem do Repositório][CL03]

1. <span data-ttu-id="a0902-129">Em Olá **repositório Git de origem** página:</span><span class="sxs-lookup"><span data-stu-id="a0902-129">On hello **Source Git Repository** page:</span></span>

   <span data-ttu-id="a0902-130">a.</span><span class="sxs-lookup"><span data-stu-id="a0902-130">a.</span></span> <span data-ttu-id="a0902-131">Em **URI**, insira `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span><span class="sxs-lookup"><span data-stu-id="a0902-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="a0902-132">Esta etapa deve preencher automaticamente Olá **Host** e **caminho do repositório** campos com hello corrigir os valores.</span><span class="sxs-lookup"><span data-stu-id="a0902-132">This step should automatically populate hello **Host** and **Repository path** fields with hello correct values.</span></span>
   
   <span data-ttu-id="a0902-133">b.</span><span class="sxs-lookup"><span data-stu-id="a0902-133">b.</span></span> <span data-ttu-id="a0902-134">repositório de inicialização Spring Olá é público, para que você não deve ter tooenter seu nome de usuário do Git e a senha.</span><span class="sxs-lookup"><span data-stu-id="a0902-134">hello Spring Boot repository is public, so you should not have tooenter your Git username and password.</span></span>
   
   <span data-ttu-id="a0902-135">c.</span><span class="sxs-lookup"><span data-stu-id="a0902-135">c.</span></span> <span data-ttu-id="a0902-136">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a0902-136">Click **Next**.</span></span>

   ![Página Repositório Git de Origem][CL04]

1. <span data-ttu-id="a0902-138">Em Olá **seleção ramificação** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="a0902-138">On hello **Branch Selection** page, click **Next**.</span></span>

   ![Página Seleção de Branch][CL05]

1. <span data-ttu-id="a0902-140">Em Olá **destino Local** página:</span><span class="sxs-lookup"><span data-stu-id="a0902-140">On hello **Local Destination** page:</span></span>

   <span data-ttu-id="a0902-141">a.</span><span class="sxs-lookup"><span data-stu-id="a0902-141">a.</span></span> <span data-ttu-id="a0902-142">Especifique Olá pasta local onde você deseja que seu repositório local.</span><span class="sxs-lookup"><span data-stu-id="a0902-142">Specify hello local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="a0902-143">b.</span><span class="sxs-lookup"><span data-stu-id="a0902-143">b.</span></span> <span data-ttu-id="a0902-144">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a0902-144">Click **Next**.</span></span>

   ![Página Destino Local][CL06]

1. <span data-ttu-id="a0902-146">Em Olá **selecione toouse um Assistente para importar projetos** página:</span><span class="sxs-lookup"><span data-stu-id="a0902-146">On hello **Select a wizard toouse for importing projects** page:</span></span>

   <span data-ttu-id="a0902-147">a.</span><span class="sxs-lookup"><span data-stu-id="a0902-147">a.</span></span> <span data-ttu-id="a0902-148">Selecione **Importar como um projeto geral**.</span><span class="sxs-lookup"><span data-stu-id="a0902-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="a0902-149">b.</span><span class="sxs-lookup"><span data-stu-id="a0902-149">b.</span></span> <span data-ttu-id="a0902-150">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a0902-150">Click **Next**.</span></span>

   ![Página "Selecionar toouse um Assistente para importar projetos"][CL07]

1. <span data-ttu-id="a0902-152">Em Olá **importar projetos** página:</span><span class="sxs-lookup"><span data-stu-id="a0902-152">On hello **Import Projects** page:</span></span>

   <span data-ttu-id="a0902-153">a.</span><span class="sxs-lookup"><span data-stu-id="a0902-153">a.</span></span> <span data-ttu-id="a0902-154">Especifique o nome do projeto.</span><span class="sxs-lookup"><span data-stu-id="a0902-154">Specify your project name.</span></span>
   
   <span data-ttu-id="a0902-155">b.</span><span class="sxs-lookup"><span data-stu-id="a0902-155">b.</span></span> <span data-ttu-id="a0902-156">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="a0902-156">Click **Finish**.</span></span>

   ![Página Importar Projetos][CL08]

1. <span data-ttu-id="a0902-158">Quando o repositório Olá for clonado com êxito, você verá todos os arquivos de saudação listados no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a0902-158">When hello repository is cloned successfully, you see all hello files listed in Eclipse.</span></span>

   ![Repositório local][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="a0902-160">Criar um projeto do Maven por meio do repositório local</span><span class="sxs-lookup"><span data-stu-id="a0902-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="a0902-161">repositório de Spring inicialização Docker Olá contém um projeto Maven completo, que você usará para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a0902-161">hello Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="a0902-162">Clique em **Arquivo** > **Importar**.</span><span class="sxs-lookup"><span data-stu-id="a0902-162">Click **File** > **Import**.</span></span>

   ![Comando no menu de arquivo hello importar][CL01]

1. <span data-ttu-id="a0902-164">Olá quando **importação** abre a caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="a0902-164">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="a0902-165">a.</span><span class="sxs-lookup"><span data-stu-id="a0902-165">a.</span></span> <span data-ttu-id="a0902-166">Expanda **Maven**.</span><span class="sxs-lookup"><span data-stu-id="a0902-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="a0902-167">b.</span><span class="sxs-lookup"><span data-stu-id="a0902-167">b.</span></span> <span data-ttu-id="a0902-168">Selecione **Projetos Existentes do Maven**.</span><span class="sxs-lookup"><span data-stu-id="a0902-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="a0902-169">c.</span><span class="sxs-lookup"><span data-stu-id="a0902-169">c.</span></span> <span data-ttu-id="a0902-170">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a0902-170">Click **Next**.</span></span>

   ![Caixa de diálogo de Importação][MV01]

1. <span data-ttu-id="a0902-172">Em Olá **projetos Maven** página:</span><span class="sxs-lookup"><span data-stu-id="a0902-172">On hello **Maven Projects** page:</span></span>

   <span data-ttu-id="a0902-173">a.</span><span class="sxs-lookup"><span data-stu-id="a0902-173">a.</span></span> <span data-ttu-id="a0902-174">Para **diretório raiz**, especifique Olá **completa** pasta no seu repositório local.</span><span class="sxs-lookup"><span data-stu-id="a0902-174">For **Root Directory**, specify hello **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="a0902-175">b.</span><span class="sxs-lookup"><span data-stu-id="a0902-175">b.</span></span> <span data-ttu-id="a0902-176">Expanda Olá **avançado** seção e insira um nome personalizado para **modelo de nome**.</span><span class="sxs-lookup"><span data-stu-id="a0902-176">Expand hello **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="a0902-177">c.</span><span class="sxs-lookup"><span data-stu-id="a0902-177">c.</span></span> <span data-ttu-id="a0902-178">Caixa de seleção Olá Olá **pom.xml** arquivo no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0902-178">Select hello box for hello **pom.xml** file in hello project.</span></span>
   
   <span data-ttu-id="a0902-179">d.</span><span class="sxs-lookup"><span data-stu-id="a0902-179">d.</span></span> <span data-ttu-id="a0902-180">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="a0902-180">Click **Finish**.</span></span>

   ![Página Projetos do Maven][MV02]

1. <span data-ttu-id="a0902-182">Quando o projeto Maven Olá é aberto com êxito, você verá um segundo projeto listado no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a0902-182">When hello Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Projeto do Maven local][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="a0902-184">Criar o aplicativo Spring Boot usando o Maven</span><span class="sxs-lookup"><span data-stu-id="a0902-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="a0902-185">No hello Explorador de projeto do Eclipse, selecione o projeto Maven hello.</span><span class="sxs-lookup"><span data-stu-id="a0902-185">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="a0902-186">Clique em **Executar** > **Executar Como** > **Build do Maven**.</span><span class="sxs-lookup"><span data-stu-id="a0902-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Comandos toorun como build Maven][BU01]

1. <span data-ttu-id="a0902-188">Quando seu aplicativo é criado com êxito, a janela do console de saudação mostra o status de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0902-188">When your application is successfully built, hello console window shows hello status.</span></span>

   ![Build bem-sucedido do Maven][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="a0902-190">Publicar seu tooAzure de aplicativo web usando um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="a0902-190">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="a0902-191">No hello Explorador de projeto do Eclipse, selecione o projeto Maven hello.</span><span class="sxs-lookup"><span data-stu-id="a0902-191">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="a0902-192">Clique em hello Azure **publicar** menu e clique **Publicar como contêiner Docker**.</span><span class="sxs-lookup"><span data-stu-id="a0902-192">Click hello Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Comando Publicar como Contêiner do Docker][PU01]

1. <span data-ttu-id="a0902-194">Olá quando **implantação de contêiner do Docker no Azure** caixa de diálogo aparece:</span><span class="sxs-lookup"><span data-stu-id="a0902-194">When hello **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="a0902-195">a.</span><span class="sxs-lookup"><span data-stu-id="a0902-195">a.</span></span> <span data-ttu-id="a0902-196">Insira um nome de imagem do Docker personalizado.</span><span class="sxs-lookup"><span data-stu-id="a0902-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="a0902-197">b.</span><span class="sxs-lookup"><span data-stu-id="a0902-197">b.</span></span> <span data-ttu-id="a0902-198">Para **artefato toodeploy**, especifique Olá caminho toohello **gs-spring-inicialização-docker-0.1.0.jar** arquivo que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="a0902-198">For **Artifact toodeploy**, specify hello path toohello **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Especificar opções do Docker][PU02]

   <span data-ttu-id="a0902-200">Os hosts existentes do Docker são exibidos.</span><span class="sxs-lookup"><span data-stu-id="a0902-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="a0902-201">Se você escolher toodeploy tooan do host existente, você poderá ignorar toostep 5.</span><span class="sxs-lookup"><span data-stu-id="a0902-201">If you choose toodeploy tooan existing host, you can skip toostep 5.</span></span> <span data-ttu-id="a0902-202">Caso contrário, use Olá etapas toocreate um host a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0902-202">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="a0902-203">a.</span><span class="sxs-lookup"><span data-stu-id="a0902-203">a.</span></span> <span data-ttu-id="a0902-204">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a0902-204">Click **Add**.</span></span>

      ![Adicionar um novo host do Docker][PU03]

   <span data-ttu-id="a0902-206">b.</span><span class="sxs-lookup"><span data-stu-id="a0902-206">b.</span></span> <span data-ttu-id="a0902-207">Olá quando **criar Host do Docker** caixa de diálogo é exibida, você pode escolher os padrões de saudação tooaccept ou você pode especificar quaisquer configurações personalizadas para o novo host do Docker.</span><span class="sxs-lookup"><span data-stu-id="a0902-207">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="a0902-208">(Para obter descrições detalhadas de saudação várias configurações, consulte [publicar um aplicativo web como um contêiner do Docker usando Olá Kit de ferramentas do Azure para IntelliJ][Publish Container with Azure Toolkit].) Clique em **próximo** quando você especificou qual toouse configurações.</span><span class="sxs-lookup"><span data-stu-id="a0902-208">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Especificar opções de host do Docker][PU04]

   <span data-ttu-id="a0902-210">c.</span><span class="sxs-lookup"><span data-stu-id="a0902-210">c.</span></span> <span data-ttu-id="a0902-211">Você pode escolher toouse credenciais de logon existente de um cofre de chaves do Azure, ou você pode escolher tooenter novas credenciais de logon do Docker.</span><span class="sxs-lookup"><span data-stu-id="a0902-211">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="a0902-212">Clique em **Concluir** quando tiver especificado suas opções.</span><span class="sxs-lookup"><span data-stu-id="a0902-212">Click **Finish** when you have specified your options.</span></span>

      ![Especificar as credenciais de host do Docker][PU05]

1. <span data-ttu-id="a0902-214">Selecione o host do Docker e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a0902-214">Select your Docker host, and then click **Next**.</span></span>

   ![Selecione toouse de host do Docker][PU06]

1. <span data-ttu-id="a0902-216">Na última página Olá Olá **implantação de contêiner do Docker no Azure** caixa de diálogo, especifique Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0902-216">On hello last page of hello **Deploying Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="a0902-217">a.</span><span class="sxs-lookup"><span data-stu-id="a0902-217">a.</span></span> <span data-ttu-id="a0902-218">Você pode escolher um nome personalizado para o contêiner de saudação que hospedará o contêiner do Docker toospecify, ou você pode aceitar o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0902-218">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="a0902-219">b.</span><span class="sxs-lookup"><span data-stu-id="a0902-219">b.</span></span> <span data-ttu-id="a0902-220">Insira as portas TCP Olá para o host do docker usando Olá sintaxe a seguir: *[porta externa]*:*[porta interna]*.</span><span class="sxs-lookup"><span data-stu-id="a0902-220">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="a0902-221">Por exemplo, **80:8080** Especifica uma porta externa de 80 e saudação padrão interno Spring inicialização porta 8080.</span><span class="sxs-lookup"><span data-stu-id="a0902-221">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="a0902-222">Se você tiver personalizado sua porta interna (por exemplo, editando o arquivo de application.yml Olá), você precisa número da porta toospecify Olá para Olá toooccur correto de roteamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="a0902-222">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="a0902-223">c.</span><span class="sxs-lookup"><span data-stu-id="a0902-223">c.</span></span> <span data-ttu-id="a0902-224">Depois de configurar essas opções, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="a0902-224">After you configure these options, click **Finish**.</span></span>

   ![Implantar um contêiner do Docker no Azure][PU07]

1. <span data-ttu-id="a0902-226">Quando termina a publicação Olá Kit de ferramentas do Azure, Olá exibe o Log de atividades do Azure **publicado** status hello.</span><span class="sxs-lookup"><span data-stu-id="a0902-226">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Host do Docker implantado com êxito][PU08]

## <a name="next-steps"></a><span data-ttu-id="a0902-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a0902-228">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring inicialização]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
