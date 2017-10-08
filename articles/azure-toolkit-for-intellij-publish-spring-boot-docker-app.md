---
title: "um aplicativo de inicialização Spring como um contêiner do Docker por meio de aaaPublish hello Kit de ferramentas do Azure para IntelliJ | Microsoft Docs"
description: "Saiba como toopublish uma tooMicrosoft de aplicativo web do Azure como um contêiner do Docker usando hello o Kit de ferramentas do Azure para IntelliJ."
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
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="8493c-103">Publicar um aplicativo de inicialização de Spring como um contêiner do Docker usando Olá Kit de ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="8493c-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="8493c-104">Olá [Spring Framework] é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="8493c-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="8493c-105">Um dos projetos mais populares de saudação que é criado em cima dessa plataforma é [Spring inicialização], que fornece um método simplificado para criação de aplicativos Java autônomo.</span><span class="sxs-lookup"><span data-stu-id="8493c-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="8493c-106">[Docker] é uma solução de software livre que ajuda os desenvolvedores a automatizar a implantação de hello, o dimensionamento e o gerenciamento de seus aplicativos que são executados em contêineres.</span><span class="sxs-lookup"><span data-stu-id="8493c-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="8493c-107">Este tutorial orienta Olá etapas toodeploy um aplicativo de inicialização de Spring como um contêiner de Docker tooMicrosoft do Azure usando Olá Kit de ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="8493c-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a><span data-ttu-id="8493c-108">Clone saudação padrão Spring inicialização Docker repositório</span><span class="sxs-lookup"><span data-stu-id="8493c-108">Clone hello default Spring Boot Docker repo</span></span>

<span data-ttu-id="8493c-109">Olá seguinte orientá-lo através da clonagem do repositório de Spring inicialização Docker hello usando IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="8493c-109">hello following steps walk you through cloning hello Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="8493c-110">Se você quiser toouse uma linha de comando, consulte [implantar um aplicativo de inicialização de Spring no Linux no serviço de contêiner do Azure][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="8493c-110">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="8493c-111">Abra o IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="8493c-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="8493c-112">Na tela de boas-vindas hello, selecione Olá **GitHub** opção Olá **Check-out do controle de versão** lista.</span><span class="sxs-lookup"><span data-stu-id="8493c-112">On hello welcome screen, select hello **GitHub** option in hello **Check out from Version Control** list.</span></span>

   ![Opção do GitHub para controle de versão][CL01]

1. <span data-ttu-id="8493c-114">Se você for solicitado toolog em, insira suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="8493c-114">Enter your credentials if you are prompted toolog in.</span></span>

   * <span data-ttu-id="8493c-115">Se você estiver usando um nome de usuário/senha toolog em tooGitHub:</span><span class="sxs-lookup"><span data-stu-id="8493c-115">If you are using a username/password toolog in tooGitHub:</span></span>

      ![Caixa de diálogo para inserir o nome de usuário e a senha do GitHub][CL02a]

   * <span data-ttu-id="8493c-117">Se você estiver usando um token toolog em tooGitHub:</span><span class="sxs-lookup"><span data-stu-id="8493c-117">If you are using a token toolog in tooGitHub:</span></span>

      ![Caixa de diálogo para inserção de um token do GitHub][CL02b]

1. <span data-ttu-id="8493c-119">Digite **https://github.com/spring-guides/gs-spring-boot-docker.git** para URL do repositório hello, especifique o caminho local e informações de pasta e, em seguida, clique em **Clone**.</span><span class="sxs-lookup"><span data-stu-id="8493c-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for hello repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Caixa de diálogo Clonar Repositório][CL03]

1. <span data-ttu-id="8493c-121">Quando for solicitado toocreate um projeto IntelliJ, selecione **não**.</span><span class="sxs-lookup"><span data-stu-id="8493c-121">When you're prompted toocreate an IntelliJ project, select **No**.</span></span>

   ![Recusar toocreate um projeto IntelliJ][CL04]

1. <span data-ttu-id="8493c-123">Na página de boas-vindas hello, clique em **Importar projeto**.</span><span class="sxs-lookup"><span data-stu-id="8493c-123">On hello welcome page, click **Import Project**.</span></span>

   ![Seleção Importar Projeto][CL05]

1. <span data-ttu-id="8493c-125">Localizar Olá caminho onde você clonar o repositório de inicialização Spring Olá, selecione Olá **completa** pasta sob a raiz de saudação e clique **Okey**.</span><span class="sxs-lookup"><span data-stu-id="8493c-125">Locate hello path where you cloned hello Spring Boot repo, select hello **complete** folder under hello root, and then click **OK**.</span></span>

   ![Selecionar uma pasta para importação][CL06]

1. <span data-ttu-id="8493c-127">Quando solicitado, selecione **Criar projeto com base nas fontes existentes**.</span><span class="sxs-lookup"><span data-stu-id="8493c-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Opção toocreate um projeto de código-fonte existente][CL07]

1. <span data-ttu-id="8493c-129">Especifique o nome do projeto ou aceite o padrão de saudação, verificar Olá caminho correto toohello **completa** pasta e depois clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="8493c-129">Specify your project name or accept hello default, verify hello correct path toohello **complete** folder, and then click **Next**.</span></span>

   ![Especifique o nome do projeto Olá][CL08]

1. <span data-ttu-id="8493c-131">Personalize quaisquer diretórios para importação e, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="8493c-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Escolher diretórios][CL09]

1. <span data-ttu-id="8493c-133">Examine Olá bibliotecas tooimport e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="8493c-133">Review hello libraries tooimport, and then click **Next**.</span></span>

   ![Examine as bibliotecas do projeto][CL10]

1. <span data-ttu-id="8493c-135">Examine a estrutura do módulo hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="8493c-135">Review hello module structure, and then click **Next**.</span></span>

   ![Examinar a estrutura do módulo][CL11]

1. <span data-ttu-id="8493c-137">Especifique o seu JDK e, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="8493c-137">Specify your JDK, and then click **Next**.</span></span>

   ![Especificar um JDK][CL12]

1. <span data-ttu-id="8493c-139">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="8493c-139">Click **Finish**.</span></span>

   ![Botão Concluir][CL13]

<span data-ttu-id="8493c-141">IntelliJ importa Olá Spring inicialização aplicativo como um projeto e exibe a estrutura de saudação quando Olá importação foi concluída.</span><span class="sxs-lookup"><span data-stu-id="8493c-141">IntelliJ imports hello Spring Boot app as a project and displays hello structure when hello import has finished.</span></span>

![Aplicativo Spring Boot no IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="8493c-143">Criar seu aplicativo Spring Boot</span><span class="sxs-lookup"><span data-stu-id="8493c-143">Build your Spring Boot app</span></span>

### <a name="build-hello-app-by-using-hello-maven-pom"></a><span data-ttu-id="8493c-144">Criar o aplicativo hello usando Olá POM Maven</span><span class="sxs-lookup"><span data-stu-id="8493c-144">Build hello app by using hello Maven POM</span></span>

1. <span data-ttu-id="8493c-145">Abra a janela da ferramenta Maven Olá se já não estiver aberto.</span><span class="sxs-lookup"><span data-stu-id="8493c-145">Open hello Maven tool window if it is not already opened.</span></span> <span data-ttu-id="8493c-146">Clique em **Exibir** > **Janelas de Ferramentas** > **Projetos do Maven**.</span><span class="sxs-lookup"><span data-stu-id="8493c-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Comandos da Janela de Ferramentas e Projetos do Maven][BU01]

1. <span data-ttu-id="8493c-148">Na janela de ferramenta Maven hello, clique com botão direito **pacote** e selecione **executar Maven criar**.</span><span class="sxs-lookup"><span data-stu-id="8493c-148">In hello Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="8493c-149">(Se seu projeto Maven não aparecer automaticamente, clique em Olá **reimportar** ícone na barra de ferramentas do hello Maven.)</span><span class="sxs-lookup"><span data-stu-id="8493c-149">(If your Maven project does not show up automatically, click hello **Reimport** icon on hello Maven toolbar.)</span></span>

   ![Executar o comando de Build do Maven][BU02]

1. <span data-ttu-id="8493c-151">O IntelliJ deverá exibir uma mensagem **ÊXITO NO BUILD** quando o aplicativo Spring Boot for criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="8493c-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![Mensagem ÊXITO NO BUILD][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="8493c-153">Criar um artefato pronto para implantação</span><span class="sxs-lookup"><span data-stu-id="8493c-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="8493c-154">toopublish seu aplicativo de inicialização de Spring, você precisa toocreate um artefato pronto para implantação.</span><span class="sxs-lookup"><span data-stu-id="8493c-154">toopublish your Spring Boot app, you need toocreate a deployment-ready artifact.</span></span> <span data-ttu-id="8493c-155">Olá Use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8493c-155">Use hello following steps:</span></span>

1. <span data-ttu-id="8493c-156">Abra seu projeto de aplicativo Web no IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="8493c-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="8493c-157">Clique em **Arquivo** e depois em **Estrutura do Projeto**.</span><span class="sxs-lookup"><span data-stu-id="8493c-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Comando Estrutura do Projeto][ART01]

1. <span data-ttu-id="8493c-159">Clique em Olá verde mais (**+**) tooadd um artefato do símbolo, clique em **JAR**e, em seguida, clique em **vazio**.</span><span class="sxs-lookup"><span data-stu-id="8493c-159">Click hello green plus (**+**) symbol tooadd an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Adicionar um artefato][ART02]

1. <span data-ttu-id="8493c-161">Nome de seu artefato enquanto se certifica-se de que não tooadd Olá ". jar" extensão e especifique a pasta de destino de saudação para Olá Maven de saída.</span><span class="sxs-lookup"><span data-stu-id="8493c-161">Name your artifact while making sure not tooadd hello ".jar" extension, and then specify hello target folder for hello Maven output.</span></span>

   ![Especificar as propriedades do artefato][ART03]

1. <span data-ttu-id="8493c-163">Crie um manifesto para o artefato (opcional):</span><span class="sxs-lookup"><span data-stu-id="8493c-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="8493c-164">a.</span><span class="sxs-lookup"><span data-stu-id="8493c-164">a.</span></span> <span data-ttu-id="8493c-165">Clique em **Criar Manifesto**.</span><span class="sxs-lookup"><span data-stu-id="8493c-165">Click **Create Manifest**.</span></span>

      ![Botão Olá criar manifesto][ART04a]

   <span data-ttu-id="8493c-167">b.</span><span class="sxs-lookup"><span data-stu-id="8493c-167">b.</span></span> <span data-ttu-id="8493c-168">Escolha saudação padrão caminho para artefato hello e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="8493c-168">Choose hello default path for hello artifact, and then click **OK**.</span></span>

      ![Especificar o caminho do artefato][ART04b]

   <span data-ttu-id="8493c-170">c.</span><span class="sxs-lookup"><span data-stu-id="8493c-170">c.</span></span> <span data-ttu-id="8493c-171">Clique nas reticências da saudação (**...** ) classe principal do toolocate hello.</span><span class="sxs-lookup"><span data-stu-id="8493c-171">Click hello ellipsis (**...**) toolocate hello main class.</span></span>

      ![Localizar a classe principal][ART04c]

   <span data-ttu-id="8493c-173">d.</span><span class="sxs-lookup"><span data-stu-id="8493c-173">d.</span></span> <span data-ttu-id="8493c-174">Escolha sua classe principal e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8493c-174">Choose your main class, and then click **OK**.</span></span>

      ![Especificar a classe principal][ART04d]

1. <span data-ttu-id="8493c-176">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8493c-176">Click **OK**.</span></span>

   ![Fechar a caixa de diálogo Olá estrutura do projeto][ART05]

> [!NOTE]
> <span data-ttu-id="8493c-178">Para obter mais informações sobre como criar artefatos no IntelliJ, consulte [artefatos configurando] no site de JetBrains hello.</span><span class="sxs-lookup"><span data-stu-id="8493c-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on hello JetBrains website.</span></span>
>

### <a name="build-hello-artifact-for-deployment"></a><span data-ttu-id="8493c-179">Criar artefato Olá para implantação</span><span class="sxs-lookup"><span data-stu-id="8493c-179">Build hello artifact for deployment</span></span>

1. <span data-ttu-id="8493c-180">Clique em **Criar** e, em seguida, clique em **Artefatos**.</span><span class="sxs-lookup"><span data-stu-id="8493c-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Comando Criar Artefatos][BU04]

1. <span data-ttu-id="8493c-182">Olá quando **criar artefato** menu de contexto for exibida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="8493c-182">When hello **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Menu de contexto Criar Artefato][BU05]

<span data-ttu-id="8493c-184">IntelliJ deve exibir o artefato Olá concluída para o aplicativo de inicialização de Spring na janela de ferramenta do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="8493c-184">IntelliJ should display hello completed artifact for your Spring Boot app in hello project tool window.</span></span>

   ![Artefato criado][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="8493c-186">Publicar seu tooAzure de aplicativo web usando um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="8493c-186">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="8493c-187">Se você não estiver inscrito no tooyour conta do Azure, siga as etapas de saudação em [instruções entrar para hello Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="8493c-187">If you have not signed in tooyour Azure account, follow hello steps in [Sign-in instructions for hello Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="8493c-188">Na janela de ferramenta do hello Explorador de projeto, clique com botão direito hello e, em seguida, selecione **Azure** > **Publicar como contêiner Docker**.</span><span class="sxs-lookup"><span data-stu-id="8493c-188">In hello Project Explorer tool window, right-click hello project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Comando Publicar como Contêiner do Docker][PU01]

1. <span data-ttu-id="8493c-190">Olá quando **implantar o contêiner do Docker no Azure** caixa de diálogo é exibida, quaisquer hosts de Docker existentes são exibidas.</span><span class="sxs-lookup"><span data-stu-id="8493c-190">When hello **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="8493c-191">Se você escolher toodeploy tooan do host existente, você poderá ignorar toostep 4.</span><span class="sxs-lookup"><span data-stu-id="8493c-191">If you choose toodeploy tooan existing host, you can skip toostep 4.</span></span> <span data-ttu-id="8493c-192">Caso contrário, use Olá etapas toocreate um host a seguir:</span><span class="sxs-lookup"><span data-stu-id="8493c-192">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="8493c-193">a.</span><span class="sxs-lookup"><span data-stu-id="8493c-193">a.</span></span> <span data-ttu-id="8493c-194">Clique em Olá verde mais (**+**) símbolo.</span><span class="sxs-lookup"><span data-stu-id="8493c-194">Click hello green plus (**+**) symbol.</span></span>

      ![Adicionar um novo host do Docker][PU02]

   <span data-ttu-id="8493c-196">b.</span><span class="sxs-lookup"><span data-stu-id="8493c-196">b.</span></span> <span data-ttu-id="8493c-197">Olá quando **criar Host do Docker** caixa de diálogo é exibida, você pode escolher os padrões de saudação tooaccept ou você pode especificar quaisquer configurações personalizadas para o novo host do Docker.</span><span class="sxs-lookup"><span data-stu-id="8493c-197">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="8493c-198">(Para obter descrições detalhadas de saudação várias configurações, consulte [publicar um aplicativo web como um contêiner do Docker usando Olá Kit de ferramentas do Azure para IntelliJ][Publish Container with Azure Toolkit].) Clique em **próximo** quando você especificou qual toouse configurações.</span><span class="sxs-lookup"><span data-stu-id="8493c-198">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Especificar opções de host do Docker][PU03a]

   <span data-ttu-id="8493c-200">c.</span><span class="sxs-lookup"><span data-stu-id="8493c-200">c.</span></span> <span data-ttu-id="8493c-201">Você pode escolher toouse credenciais de logon existente de um cofre de chaves do Azure, ou você pode escolher tooenter novas credenciais de logon do Docker.</span><span class="sxs-lookup"><span data-stu-id="8493c-201">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="8493c-202">Clique em **Concluir** quando tiver especificado suas opções.</span><span class="sxs-lookup"><span data-stu-id="8493c-202">Click **Finish** when you have specified your options.</span></span>

      ![Especificar as credenciais de host do Docker][PU03b]

1. <span data-ttu-id="8493c-204">Selecione o host do Docker e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8493c-204">Select your Docker host, and then click **Next**.</span></span>

   ![Selecione Olá Docker host toouse][PU04]

1. <span data-ttu-id="8493c-206">Na última página Olá Olá **implantar o contêiner do Docker no Azure** caixa de diálogo, especifique Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="8493c-206">On hello last page of hello **Deploy Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="8493c-207">a.</span><span class="sxs-lookup"><span data-stu-id="8493c-207">a.</span></span> <span data-ttu-id="8493c-208">Você pode escolher um nome personalizado para o contêiner de saudação que hospedará o contêiner do Docker toospecify, ou você pode aceitar o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="8493c-208">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="8493c-209">b.</span><span class="sxs-lookup"><span data-stu-id="8493c-209">b.</span></span> <span data-ttu-id="8493c-210">Insira as portas TCP Olá para o host do docker usando Olá sintaxe a seguir: *[porta externa]*:*[porta interna]*.</span><span class="sxs-lookup"><span data-stu-id="8493c-210">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="8493c-211">Por exemplo, **80:8080** Especifica uma porta externa de 80 e saudação padrão interno Spring inicialização porta 8080.</span><span class="sxs-lookup"><span data-stu-id="8493c-211">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="8493c-212">Se você tiver personalizado sua porta interna (por exemplo, editando o arquivo de application.yml Olá), você precisa número da porta toospecify Olá para Olá toooccur correto de roteamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="8493c-212">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="8493c-213">c.</span><span class="sxs-lookup"><span data-stu-id="8493c-213">c.</span></span> <span data-ttu-id="8493c-214">Depois de configurar essas opções, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="8493c-214">After you have configured these options, click **Finish**.</span></span>

   ![Implantar um contêiner do Docker no Azure][PU05]

1. <span data-ttu-id="8493c-216">Quando termina a publicação Olá Kit de ferramentas do Azure, Olá exibe o Log de atividades do Azure **publicado** status hello.</span><span class="sxs-lookup"><span data-stu-id="8493c-216">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Host do Docker implantado com êxito][PU06]

## <a name="next-steps"></a><span data-ttu-id="8493c-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8493c-218">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="8493c-219">toolearn sobre métodos adicionais para a criação de aplicativos de inicialização Spring usando IntelliJ, consulte [criar projetos de inicialização Spring](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) no site de JetBrains hello.</span><span class="sxs-lookup"><span data-stu-id="8493c-219">toolearn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on hello JetBrains website.</span></span>

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[artefatos configurando]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring inicialização]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
