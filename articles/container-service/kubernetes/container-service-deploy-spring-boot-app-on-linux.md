---
title: "aaaDeploy um aplicativo de Web de inicialização Spring no Linux no serviço de contêiner do Azure | Microsoft Docs"
description: "Este tutorial orienta você embora Olá etapas toodeploy um aplicativo de inicialização de Spring como um aplicativo web do Linux no Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2c44be1c7f66a38f48239001f0be9e90c7e6edef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a><span data-ttu-id="a78cc-103">Implantar um aplicativo de inicialização Spring em Linux em hello Azure serviço de contêiner</span><span class="sxs-lookup"><span data-stu-id="a78cc-103">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>

<span data-ttu-id="a78cc-104">Olá  **[Spring Framework]**  é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="a78cc-104">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="a78cc-105">Um dos projetos mais populares de saudação que é criado em cima dessa plataforma é [Spring inicialização], que fornece um método simplificado para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="a78cc-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="a78cc-106">**[Docker]**  é soluções de código-fonte aberto que ajuda os desenvolvedores a automatizar a implantação hello, escala e gerenciamento de seus aplicativos que são executados em contêineres.</span><span class="sxs-lookup"><span data-stu-id="a78cc-106">**[Docker]** is open-source solutions that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="a78cc-107">Este tutorial orienta você pelo usando Docker toodevelop e implantar um host Spring inicialização aplicativo tooa Linux Olá [serviço de contêiner do Azure (ACS)].</span><span class="sxs-lookup"><span data-stu-id="a78cc-107">This tutorial walks you through using Docker toodevelop and deploy a Spring Boot application tooa Linux host in hello [Azure Container Service (ACS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a78cc-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a78cc-108">Prerequisites</span></span>

<span data-ttu-id="a78cc-109">Em ordem toocomplete Olá etapas deste tutorial, você precisa toohave Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a78cc-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="a78cc-110">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="a78cc-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="a78cc-111">Olá [Azure Interface de linha de comando (CLI)].</span><span class="sxs-lookup"><span data-stu-id="a78cc-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="a78cc-112">Um [JDK (Java Developer Kit)] atualizado.</span><span class="sxs-lookup"><span data-stu-id="a78cc-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="a78cc-113">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="a78cc-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="a78cc-114">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="a78cc-114">A [Git] client.</span></span>
* <span data-ttu-id="a78cc-115">Um cliente do [Docker].</span><span class="sxs-lookup"><span data-stu-id="a78cc-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="a78cc-116">Devido a requisitos de virtualização toohello deste tutorial, você não conseguir seguir etapas Olá neste artigo em uma máquina virtual. Você deve usar um computador físico com recursos de virtualização habilitados.</span><span class="sxs-lookup"><span data-stu-id="a78cc-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="a78cc-117">Criar hello Spring inicialização no aplicativo web do guia de Introdução do Docker</span><span class="sxs-lookup"><span data-stu-id="a78cc-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="a78cc-118">Olá etapas a seguir mostram Olá etapas que são necessária toocreate um aplicativo simples da web Spring inicialização e testá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="a78cc-118">hello following steps walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="a78cc-119">Abra um prompt de comando e criar um diretório local toohold seu aplicativo e altere o diretório toothat; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a78cc-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="a78cc-120">-- ou --</span><span class="sxs-lookup"><span data-stu-id="a78cc-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="a78cc-121">Saudação de clone [inicialização Spring no guia de Introdução do Docker] projeto de exemplo no diretório Olá criado; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a78cc-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="a78cc-122">Alterar diretório toohello concluída projeto; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a78cc-122">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="a78cc-123">Criar arquivo JAR de saudação usando Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a78cc-123">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="a78cc-124">Quando Olá web aplicativo tiver sido criado, alterar diretório toohello `target` diretório onde o arquivo JAR do hello está localizado e iniciar o aplicativo da web de saudação; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a78cc-124">Once hello web app has been created, change directory toohello `target` directory where hello JAR file is located and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="a78cc-125">Testar o aplicativo da web de saudação navegando tooit localmente usando um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="a78cc-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="a78cc-126">Por exemplo, se você tiver ondulação disponível e configurado Olá Tomcat server toorun na porta 80:</span><span class="sxs-lookup"><span data-stu-id="a78cc-126">For example, if you have curl available and you configured hello Tomcat server toorun on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="a78cc-127">Você deve ver Olá mensagem exibida a seguir: **Docker Olá, mundo!**</span><span class="sxs-lookup"><span data-stu-id="a78cc-127">You should see hello following message displayed: **Hello Docker World!**</span></span>

   ![Procurar aplicativo de exemplo localmente][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a><span data-ttu-id="a78cc-129">Criar um registro de contêiner do Azure toouse como um registro de Docker privada</span><span class="sxs-lookup"><span data-stu-id="a78cc-129">Create an Azure Container Registry toouse as a Private Docker Registry</span></span>

<span data-ttu-id="a78cc-130">Olá etapas a seguir orientam você durante usando Olá toocreate portal do Azure um registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="a78cc-130">hello following steps walk you through using hello Azure portal toocreate an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="a78cc-131">Se você quiser toouse Olá CLI do Azure em vez da saudação portal do Azure, siga as etapas de saudação em [criar um registro de contêiner do Docker privado usando hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a78cc-131">If you want toouse hello Azure CLI instead of hello Azure portal, follow hello steps in [Create a private Docker container registry using hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span></span>
>

1. <span data-ttu-id="a78cc-132">Procurar toohello [portal do Azure] e entrar.</span><span class="sxs-lookup"><span data-stu-id="a78cc-132">Browse toohello [Azure portal] and sign in.</span></span>

   <span data-ttu-id="a78cc-133">Depois de ter entrado na conta de tooyour no hello portal do Azure, você pode seguir etapas Olá Olá [criar um registro de contêiner do Docker privado usando o portal do Azure de saudação] artigo, que são traduzido em Olá seguindo as etapas para Olá bem de eficiência.</span><span class="sxs-lookup"><span data-stu-id="a78cc-133">Once you have signed in tooyour account on hello Azure portal, you can follow hello steps in hello [Create a private Docker container registry using hello Azure portal] article, which are paraphrased in hello following steps for hello sake of expediency.</span></span>

1. <span data-ttu-id="a78cc-134">Clique ícone menu Olá **+ novo**, em seguida, clique em **contêineres**e, em seguida, clique em **registro de contêiner do Azure**.</span><span class="sxs-lookup"><span data-stu-id="a78cc-134">Click hello menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Criar um novo Registro de Contêiner do Azure][AR01]

1. <span data-ttu-id="a78cc-136">Quando a página de informações de Olá para o modelo de registro de contêiner do Azure Olá for exibida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="a78cc-136">When hello information page for hello Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Criar um novo Registro de Contêiner do Azure][AR02]

1. <span data-ttu-id="a78cc-138">Olá quando **criar registro de contêiner** página é exibida, insira seu **nome do registro** e **grupo de recursos**, escolha **habilitar** para Olá **usuário administrador**e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="a78cc-138">When hello **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for hello **Admin user**, and then click **Create**.</span></span>

   ![Definir configurações do registro de contêiner do Azure][AR03]

1. <span data-ttu-id="a78cc-140">Quando o registro de contêiner tiver sido criado, navegar o registro de contêiner tooyour no hello portal do Azure e, em seguida, clique em **chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="a78cc-140">Once your container registry has been created, navigate tooyour container registry in hello Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="a78cc-141">Anote Olá nome de usuário e senha para as próximas etapas hello.</span><span class="sxs-lookup"><span data-stu-id="a78cc-141">Take note of hello username and password for hello next steps.</span></span>

   ![Chaves de acesso do Registro de Contêiner do Azure][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a><span data-ttu-id="a78cc-143">Configurar Maven toouse suas chaves de acesso de registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="a78cc-143">Configure Maven toouse your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="a78cc-144">Navegue toohello diretório de configuração para sua instalação Maven e abra Olá *settings.xml* arquivo com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="a78cc-144">Navigate toohello configuration directory for your Maven installation and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="a78cc-145">Adicionar as configurações de acesso de registro de contêiner do Azure da seção anterior Olá este tutorial toohello `<servers>` coleção em Olá *settings.xml* arquivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a78cc-145">Add your Azure Container Registry access settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="a78cc-146">Navegue toohello concluída diretório do projeto para o seu aplicativo de inicialização de Spring (por exemplo: "*C:\SpringBoot\gs-spring-boot-docker\complete*"ou"*/users/robert/SpringBoot/gs-spring-boot-docker / concluída*") e abra hello *pom.xml* arquivo com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="a78cc-146">Navigate toohello completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="a78cc-147">Saudação de atualização `<properties>` coleção em Olá *pom.xml* arquivo com valor de servidor de logon Olá para o registro de contêiner do Azure na seção anterior de saudação deste tutorial; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a78cc-147">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="a78cc-148">Saudação de atualização `<plugins>` coleção em Olá *pom.xml* arquivo de forma que Olá `<plugin>` contém Olá logon endereço e o registro do nome do servidor para o registro de contêiner do Azure na seção anterior de saudação deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="a78cc-148">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry from hello previous section of this tutorial.</span></span> <span data-ttu-id="a78cc-149">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a78cc-149">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. <span data-ttu-id="a78cc-150">Navegue toohello concluída diretório do projeto para o aplicativo de inicialização de Spring e executar Olá após o aplicativo do comando toorebuild hello e enviar por push Olá contêiner tooyour registro de contêiner do Azure:</span><span class="sxs-lookup"><span data-stu-id="a78cc-150">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="a78cc-151">Quando são enviar seu tooAzure de contêiner do Docker, você receberá uma mensagem de erro é semelhante tooone de saudação seguindo o mesmo que seu contêiner de Docker foi criado com êxito:</span><span class="sxs-lookup"><span data-stu-id="a78cc-151">When you are pushing your Docker container tooAzure, you may receive an error message that is similar tooone of hello following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="a78cc-152">Se isso acontecer, talvez seja necessário toosign em tooyour conta do Azure da linha de comando do Docker Olá; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a78cc-152">If this happens, you may need toosign in tooyour Azure account from hello Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="a78cc-153">Você pode enviar seu contêiner de linha de comando Olá; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a78cc-153">You can then push your container from hello command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="a78cc-154">Criar um aplicativo Web no Linux no Serviço de Aplicativo do Azure usando a imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="a78cc-154">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="a78cc-155">Procurar toohello [portal do Azure] e entrar.</span><span class="sxs-lookup"><span data-stu-id="a78cc-155">Browse toohello [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="a78cc-156">Clique ícone menu Olá **+ novo**, em seguida, clique em **Web + móvel**e, em seguida, clique em **Web App no Linux**.</span><span class="sxs-lookup"><span data-stu-id="a78cc-156">Click hello menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Criar um novo aplicativo web no hello portal do Azure][LX01]

1. <span data-ttu-id="a78cc-158">Olá quando **Web App no Linux** página é exibida, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="a78cc-158">When hello **Web App on Linux** page is displayed, enter hello following information:</span></span>

   <span data-ttu-id="a78cc-159">a.</span><span class="sxs-lookup"><span data-stu-id="a78cc-159">a.</span></span> <span data-ttu-id="a78cc-160">Insira um nome exclusivo para Olá **nome do aplicativo**; por exemplo: "*wingtiptoyslinux*."</span><span class="sxs-lookup"><span data-stu-id="a78cc-160">Enter a unique name for hello **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="a78cc-161">b.</span><span class="sxs-lookup"><span data-stu-id="a78cc-161">b.</span></span> <span data-ttu-id="a78cc-162">Escolha seu **assinatura** da lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="a78cc-162">Choose your **Subscription** from hello drop-down list.</span></span>

   <span data-ttu-id="a78cc-163">c.</span><span class="sxs-lookup"><span data-stu-id="a78cc-163">c.</span></span> <span data-ttu-id="a78cc-164">Escolher um existente **grupo de recursos**, ou especifique um nome toocreate um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a78cc-164">Choose an existing **Resource Group**, or specify a name toocreate a new resource group.</span></span>

   <span data-ttu-id="a78cc-165">d.</span><span class="sxs-lookup"><span data-stu-id="a78cc-165">d.</span></span> <span data-ttu-id="a78cc-166">Clique em **configurar contêiner** e digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="a78cc-166">Click **Configure container** and enter hello following information:</span></span>

      * <span data-ttu-id="a78cc-167">Escolha **Registro particular**.</span><span class="sxs-lookup"><span data-stu-id="a78cc-167">Choose **Private registry**.</span></span>

      * <span data-ttu-id="a78cc-168">**Marca de imagem e opcional**: especifique o nome do contêiner de antes. Por exemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span><span class="sxs-lookup"><span data-stu-id="a78cc-168">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="a78cc-169">**URL do servidor**: especifique a URL de registro de antes; por exemplo: "*https://wingtiptoysregistry.azurecr.io*"</span><span class="sxs-lookup"><span data-stu-id="a78cc-169">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="a78cc-170">**Nome de usuário de logon** e **Senha**: especifique suas credenciais de logon das **Chaves de Acesso** usadas nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="a78cc-170">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="a78cc-171">e.</span><span class="sxs-lookup"><span data-stu-id="a78cc-171">e.</span></span> <span data-ttu-id="a78cc-172">Depois que você inseriu todos Olá acima informações, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="a78cc-172">Once you have entered all of hello above information, click **OK**.</span></span>

   ![Definir configurações do aplicativo Web][LX02]

1. <span data-ttu-id="a78cc-174">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a78cc-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="a78cc-175">O Azure mapeará automaticamente solicitações tooembedded Tomcat servidor da Internet que está em execução em portas de saudação padrão de 80 ou 8080.</span><span class="sxs-lookup"><span data-stu-id="a78cc-175">Azure will automatically map Internet requests tooembedded Tomcat server that is running on hello standard ports of 80 or 8080.</span></span> <span data-ttu-id="a78cc-176">No entanto, se você configurou seu toorun de servidor Tomcat inserido em uma porta personalizada, você precisa tooadd um aplicativo web tooyour variável de ambiente que define a porta de saudação para seu servidor Tomcat inserido.</span><span class="sxs-lookup"><span data-stu-id="a78cc-176">However, if you configured your embedded Tomcat server toorun on a custom port, you need tooadd an environment variable tooyour web app that defines hello port for your embedded Tomcat server.</span></span> <span data-ttu-id="a78cc-177">Assim, o toodo use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a78cc-177">toodo so, use hello following steps:</span></span>
>
> 1. <span data-ttu-id="a78cc-178">Procurar toohello [portal do Azure] e entrar.</span><span class="sxs-lookup"><span data-stu-id="a78cc-178">Browse toohello [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="a78cc-179">Clique ícone Olá **serviços de aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a78cc-179">Click hello icon for **App Services**.</span></span> <span data-ttu-id="a78cc-180">(Consulte o item #1 na imagem de saudação abaixo).</span><span class="sxs-lookup"><span data-stu-id="a78cc-180">(See item #1 in hello image below.)</span></span>
>
> 3. <span data-ttu-id="a78cc-181">Selecione o aplicativo web na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="a78cc-181">Select your web app from hello list.</span></span> <span data-ttu-id="a78cc-182">(Item &#2; na imagem de saudação abaixo).</span><span class="sxs-lookup"><span data-stu-id="a78cc-182">(Item #2 in hello image below.)</span></span>
>
> 4. <span data-ttu-id="a78cc-183">Clique em **Configurações do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="a78cc-183">Click **Application Settings**.</span></span> <span data-ttu-id="a78cc-184">(Item #3 na imagem de saudação abaixo).</span><span class="sxs-lookup"><span data-stu-id="a78cc-184">(Item #3 in hello image below.)</span></span>
>
> 5. <span data-ttu-id="a78cc-185">Em Olá **configurações do aplicativo** seção, adicione uma nova variável de ambiente denominada **porta** e insira seu número de porta personalizada para o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="a78cc-185">In hello **App settings** section, add a new environment variable named **PORT** and enter your custom port number for hello value.</span></span> <span data-ttu-id="a78cc-186">(Item #4 na imagem de saudação abaixo).</span><span class="sxs-lookup"><span data-stu-id="a78cc-186">(Item #4 in hello image below.)</span></span>
>
> 6. <span data-ttu-id="a78cc-187">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a78cc-187">Click **Save**.</span></span> <span data-ttu-id="a78cc-188">(Item #5 na imagem de saudação abaixo).</span><span class="sxs-lookup"><span data-stu-id="a78cc-188">(Item #5 in hello image below.)</span></span>
>
> ![Salvando um número de porta personalizado em Olá portal do Azure][LX03]
>

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="a78cc-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a78cc-190">Next steps</span></span>

<span data-ttu-id="a78cc-191">Para obter mais informações sobre como usar aplicativos de inicialização Spring no Azure, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a78cc-191">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="a78cc-192">Implantar um toohello Spring aplicativo de inicialização do serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="a78cc-192">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="a78cc-193">Implantar um aplicativo de inicialização Spring em um Cluster de Kubernetes no hello Azure serviço de contêiner</span><span class="sxs-lookup"><span data-stu-id="a78cc-193">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="a78cc-194">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="a78cc-194">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="a78cc-195">Para obter mais detalhes sobre Olá Spring inicialização no projeto de exemplo do Docker, consulte [inicialização Spring no guia de Introdução do Docker].</span><span class="sxs-lookup"><span data-stu-id="a78cc-195">For further details about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="a78cc-196">Para obter ajuda com a guia de Introdução com seus próprios aplicativos de inicialização Spring, consulte Olá **Initializr Spring** em https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="a78cc-196">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="a78cc-197">Para obter mais informações sobre como começar com a criação de um aplicativo de inicialização de Spring simples, consulte Olá Spring Initializr em https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="a78cc-197">For more information about getting started with creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="a78cc-198">Para obter exemplos adicionais para como toouse Docker personalizado imagens com o Azure, consulte [usando uma imagem personalizada do Docker para o aplicativo Web do Azure no Linux].</span><span class="sxs-lookup"><span data-stu-id="a78cc-198">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure Interface de linha de comando (CLI)]: /cli/azure/overview
[serviço de contêiner do Azure (ACS)]: https://azure.microsoft.com/services/container-service/
[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[portal do Azure]: https://portal.azure.com/
[criar um registro de contêiner do Docker privado usando o portal do Azure de saudação]: /azure/container-registry/container-registry-get-started-portal
[usando uma imagem personalizada do Docker para o aplicativo Web do Azure no Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[ferramentas Java para o Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring inicialização]: http://projects.spring.io/spring-boot/
[inicialização Spring no guia de Introdução do Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-linux/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-linux/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-linux/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-linux/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-linux/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-linux/AR04.png

[LX01]: ./media/container-service-deploy-spring-boot-app-on-linux/LX01.png
[LX02]: ./media/container-service-deploy-spring-boot-app-on-linux/LX02.png
[LX03]: ./media/container-service-deploy-spring-boot-app-on-linux/LX03.png
