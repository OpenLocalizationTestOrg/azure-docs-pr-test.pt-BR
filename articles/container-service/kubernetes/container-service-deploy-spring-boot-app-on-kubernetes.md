---
title: "aaaDeploy um aplicativo de inicialização Spring em Kubernetes no serviço de contêiner do Azure | Microsoft Docs"
description: "Este tutorial irá orientá-lo embora Olá etapas toodeploy um aplicativo de inicialização de Spring em um cluster Kubernetes no Microsoft Azure."
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
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a><span data-ttu-id="727c4-103">Implantar um aplicativo de inicialização Spring em um Cluster de Kubernetes no hello Azure serviço de contêiner</span><span class="sxs-lookup"><span data-stu-id="727c4-103">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>

<span data-ttu-id="727c4-104">Olá  **[Spring Framework]**  é uma estrutura de código-fonte aberto popular que ajuda os desenvolvedores Java criar web, móveis e aplicativos de API.</span><span class="sxs-lookup"><span data-stu-id="727c4-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="727c4-105">Este tutorial usa um aplicativo de exemplo criado usando [Spring inicialização], uma abordagem orientada a convenção para usar Spring tooget iniciado rapidamente.</span><span class="sxs-lookup"><span data-stu-id="727c4-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="727c4-106">**[Kubernetes]**  e  **[Docker]**  são soluções de código-fonte aberto que ajudam os desenvolvedores automatizar a implantação de hello, escala e gerenciamento de seus aplicativos em execução em contêineres.</span><span class="sxs-lookup"><span data-stu-id="727c4-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate hello deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="727c4-107">Este tutorial orienta você embora combinar essas duas tecnologias populares, código-fonte aberto toodevelop e implantar um aplicativo de inicialização de Spring tooMicrosoft do Azure.</span><span class="sxs-lookup"><span data-stu-id="727c4-107">This tutorial walks you though combining these two popular, open-source technologies toodevelop and deploy a Spring Boot application tooMicrosoft Azure.</span></span> <span data-ttu-id="727c4-108">Mais especificamente, você usa  *[Spring inicialização]*  para desenvolvimento de aplicativos,  *[Kubernetes]*  para implantação do contêiner e hello [Serviço de contêiner do azure (ACS)] toohost seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="727c4-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and hello [Azure Container Service (ACS)] toohost your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="727c4-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="727c4-109">Prerequisites</span></span>

* <span data-ttu-id="727c4-110">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="727c4-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="727c4-111">Olá [Azure Interface de linha de comando (CLI)].</span><span class="sxs-lookup"><span data-stu-id="727c4-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="727c4-112">Um [JDK (Java Developer Kit)] atualizado.</span><span class="sxs-lookup"><span data-stu-id="727c4-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="727c4-113">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="727c4-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="727c4-114">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="727c4-114">A [Git] client.</span></span>
* <span data-ttu-id="727c4-115">Um cliente do [Docker].</span><span class="sxs-lookup"><span data-stu-id="727c4-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="727c4-116">Devido a requisitos de virtualização toohello deste tutorial, você não conseguir seguir etapas Olá neste artigo em uma máquina virtual. Você deve usar um computador físico com recursos de virtualização habilitados.</span><span class="sxs-lookup"><span data-stu-id="727c4-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="727c4-117">Criar hello Spring inicialização no aplicativo web do guia de Introdução do Docker</span><span class="sxs-lookup"><span data-stu-id="727c4-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="727c4-118">Olá etapas a seguir orientam você durante a criação de um aplicativo da web de inicialização Spring e testá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="727c4-118">hello following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="727c4-119">Abra um prompt de comando e criar um diretório local toohold seu aplicativo e altere o diretório toothat; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="727c4-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="727c4-120">-- ou --</span><span class="sxs-lookup"><span data-stu-id="727c4-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="727c4-121">Saudação de clone [inicialização Spring no guia de Introdução do Docker] projeto de exemplo no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="727c4-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="727c4-122">Alterar o projeto do diretório toohello concluída.</span><span class="sxs-lookup"><span data-stu-id="727c4-122">Change directory toohello completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="727c4-123">Use toobuild Maven e o aplicativo de exemplo hello execução.</span><span class="sxs-lookup"><span data-stu-id="727c4-123">Use Maven toobuild and run hello sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="727c4-124">Teste Olá web aplicativo navegando toohttp://localhost:8080 ou com os seguintes Olá `curl` comando:</span><span class="sxs-lookup"><span data-stu-id="727c4-124">Test hello web app by browsing toohttp://localhost:8080, or with hello following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="727c4-125">Você deve ver Olá mensagem exibida a seguir: **Docker Olá, mundo**</span><span class="sxs-lookup"><span data-stu-id="727c4-125">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Procurar aplicativo de exemplo localmente][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="727c4-127">Criar um registro de contêiner do Azure usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="727c4-127">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="727c4-128">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="727c4-128">Open a command prompt.</span></span>

1. <span data-ttu-id="727c4-129">Faça logon no tooyour conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="727c4-129">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="727c4-130">Crie um grupo de recursos para Olá recursos do Azure usados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="727c4-130">Create a resource group for hello Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="727c4-131">Crie um registro de contêiner do Azure privada no grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="727c4-131">Create a private Azure container registry in hello resource group.</span></span> <span data-ttu-id="727c4-132">tutorial de saudação envia o aplicativo de exemplo hello como um registro de toothis de imagem do Docker em etapas posteriores.</span><span class="sxs-lookup"><span data-stu-id="727c4-132">hello tutorial pushes hello sample app as a Docker image toothis registry in later steps.</span></span> <span data-ttu-id="727c4-133">Substitua `wingtiptoysregistry` por um nome exclusivo para o registro.</span><span class="sxs-lookup"><span data-stu-id="727c4-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a><span data-ttu-id="727c4-134">Enviar por push o seu registro de contêiner do aplicativo toohello</span><span class="sxs-lookup"><span data-stu-id="727c4-134">Push your app toohello container registry</span></span>

1. <span data-ttu-id="727c4-135">Navegue toohello diretório de configuração para sua instalação Maven (~/.m2/ padrão ou C:\Users\username\.m2) e abra hello *settings.xml* arquivo com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="727c4-135">Navigate toohello configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="727c4-136">Recupere senha Olá para o registro de contêiner de saudação CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="727c4-136">Retrieve hello password for your container registry from hello Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="727c4-137">Adicionar o novo de tooa registro de contêiner do Azure id e senha `<server>` coleção em Olá *settings.xml* arquivo.</span><span class="sxs-lookup"><span data-stu-id="727c4-137">Add your Azure Container Registry id and password tooa new `<server>` collection in hello *settings.xml* file.</span></span>
<span data-ttu-id="727c4-138">Olá `id` e `username` são Olá nome do registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="727c4-138">hello `id` and `username` are hello name of hello registry.</span></span> <span data-ttu-id="727c4-139">Saudação de uso `password` valor do comando anterior de saudação (sem aspas).</span><span class="sxs-lookup"><span data-stu-id="727c4-139">Use hello `password` value from hello previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="727c4-140">Navegue de diretório do projeto toohello concluída para o seu aplicativo de inicialização de Spring (por exemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*"ou"*/users/robert/SpringBoot/gs-spring-boot-docker / concluída*") e abra hello *pom.xml* arquivo com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="727c4-140">Navigate toohello completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="727c4-141">Saudação de atualização `<properties>` coleção em Olá *pom.xml* arquivo com o valor de servidor de logon Olá para o registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="727c4-141">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="727c4-142">Saudação de atualização `<plugins>` coleção em Olá *pom.xml* arquivo de forma que Olá `<plugin>` contém Olá logon endereço e o registro do nome do servidor para o registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="727c4-142">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="727c4-143">Navegue de diretório do projeto toohello concluída para o seu aplicativo de inicialização de Spring e execute Olá comando toobuild Olá Docker contêiner e enviar por push Olá toohello registro da imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="727c4-143">Navigate toohello completed project directory for your Spring Boot application and run hello following command toobuild hello Docker container and push hello image toohello registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="727c4-144">Você receberá uma mensagem de erro é semelhante tooone seguinte hello quando Maven envia Olá tooAzure de imagem:</span><span class="sxs-lookup"><span data-stu-id="727c4-144">You may receive an error message that is similar tooone of hello following when Maven pushes hello image tooAzure:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="727c4-145">Se você receber esse erro, faça logon tooAzure da linha de comando do Docker hello.</span><span class="sxs-lookup"><span data-stu-id="727c4-145">If you get this error, log in tooAzure from hello Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="727c4-146">Em seguida, envie por push o seu contêiner:</span><span class="sxs-lookup"><span data-stu-id="727c4-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a><span data-ttu-id="727c4-147">Criar um Kubernetes Cluster no ACS usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="727c4-147">Create a Kubernetes Cluster on ACS using hello Azure CLI</span></span>

1. <span data-ttu-id="727c4-148">Crie um cluster Kubernetes no Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="727c4-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="727c4-149">Hello comando a seguir cria um *kubernetes* cluster Olá *wingtiptoys kubernetes* recurso grupo com *containerservice wingtiptoys* como cluster Olá nome, e *kubernetes wingtiptoys* como prefixo DNS hello:</span><span class="sxs-lookup"><span data-stu-id="727c4-149">hello following command creates a *kubernetes* cluster in hello *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as hello cluster name, and *wingtiptoys-kubernetes* as hello DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="727c4-150">Este comando pode demorar um pouco toocomplete.</span><span class="sxs-lookup"><span data-stu-id="727c4-150">This command may take a while toocomplete.</span></span>

1. <span data-ttu-id="727c4-151">Instalar `kubectl` usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="727c4-151">Install `kubectl` using hello Azure CLI.</span></span> <span data-ttu-id="727c4-152">Os usuários do Linux podem ter tooprefix esse comando com `sudo` desde que implanta Olá Kubernetes CLI muito`/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="727c4-152">Linux users may have tooprefix this command with `sudo` since it deploys hello Kubernetes CLI too`/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="727c4-153">Baixar informações de configuração de cluster Olá, portanto, você pode gerenciar seu cluster de interface de web Kubernetes hello e `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="727c4-153">Download hello cluster configuration information so you can manage your cluster from hello Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a><span data-ttu-id="727c4-154">Implantar Olá imagem tooyour Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="727c4-154">Deploy hello image tooyour Kubernetes cluster</span></span>

<span data-ttu-id="727c4-155">Este tutorial implanta usando o aplicativo hello `kubectl`, em seguida, permitir você tooexplore Olá implantação por meio da interface web hello Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="727c4-155">This tutorial deploys hello app using `kubectl`, then allow you tooexplore hello deployment through hello Kubernetes web interface.</span></span>

### <a name="deploy-with-hello-kubernetes-web-interface"></a><span data-ttu-id="727c4-156">Implantar a interface do hello Kubernetes da web</span><span class="sxs-lookup"><span data-stu-id="727c4-156">Deploy with hello Kubernetes web interface</span></span>

1. <span data-ttu-id="727c4-157">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="727c4-157">Open a command prompt.</span></span>

1. <span data-ttu-id="727c4-158">Abra o site de configuração de saudação para seu cluster Kubernetes no navegador padrão:</span><span class="sxs-lookup"><span data-stu-id="727c4-158">Open hello configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="727c4-159">Quando o site de configuração Kubernetes Olá abre no navegador, clique em link Olá muito**implantar um aplicativo em contêineres**:</span><span class="sxs-lookup"><span data-stu-id="727c4-159">When hello Kubernetes configuration website opens in your browser, click hello link too**deploy a containerized app**:</span></span>

   ![Site de configuração do Kubernetes][KB01]

1. <span data-ttu-id="727c4-161">Olá quando **implantar um aplicativo em contêineres** página é exibida, especifique Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="727c4-161">When hello **Deploy a containerized app** page is displayed, specify hello following options:</span></span>

   <span data-ttu-id="727c4-162">a.</span><span class="sxs-lookup"><span data-stu-id="727c4-162">a.</span></span> <span data-ttu-id="727c4-163">Selecione **Especificar detalhes do aplicativo abaixo**.</span><span class="sxs-lookup"><span data-stu-id="727c4-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="727c4-164">b.</span><span class="sxs-lookup"><span data-stu-id="727c4-164">b.</span></span> <span data-ttu-id="727c4-165">Insira o nome do aplicativo de inicialização de Spring para Olá **nome do aplicativo**; por exemplo: "*gs spring-inicialização docker*".</span><span class="sxs-lookup"><span data-stu-id="727c4-165">Enter your Spring Boot application name for hello **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="727c4-166">c.</span><span class="sxs-lookup"><span data-stu-id="727c4-166">c.</span></span> <span data-ttu-id="727c4-167">Insira sua imagem de contêiner e de servidor de logon do anteriormente para Olá **imagem de contêiner**; por exemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="727c4-167">Enter your login server and container image from earlier for hello **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="727c4-168">d.</span><span class="sxs-lookup"><span data-stu-id="727c4-168">d.</span></span> <span data-ttu-id="727c4-169">Escolha **externo** para Olá **Service**.</span><span class="sxs-lookup"><span data-stu-id="727c4-169">Choose **External** for hello **Service**.</span></span>

   <span data-ttu-id="727c4-170">e.</span><span class="sxs-lookup"><span data-stu-id="727c4-170">e.</span></span> <span data-ttu-id="727c4-171">Especifique as portas internas e externas no hello **porta** e **porta de destino** caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="727c4-171">Specify your external and internal ports in hello **Port** and **Target port** text boxes.</span></span>

   ![Site de configuração do Kubernetes][KB02]


1. <span data-ttu-id="727c4-173">Clique em **implantar** toodeploy contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="727c4-173">Click **Deploy** toodeploy hello container.</span></span>

   ![Implantar o contêiner][KB05]

1. <span data-ttu-id="727c4-175">Após a implantação de seu aplicativo, você verá o aplicativo Spring Boot listado em **Serviços**.</span><span class="sxs-lookup"><span data-stu-id="727c4-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Serviços Kubernetes][KB06]

1. <span data-ttu-id="727c4-177">Se você clicar em links Olá para **pontos de extremidade externos**, você pode ver o aplicativo de inicialização Spring em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="727c4-177">If you click hello link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Serviços Kubernetes][KB07]

   ![Procurar aplicativo de exemplo no Azure][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="727c4-180">Implantar com kubectl</span><span class="sxs-lookup"><span data-stu-id="727c4-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="727c4-181">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="727c4-181">Open a command prompt.</span></span>

1. <span data-ttu-id="727c4-182">Executar seu contêiner no cluster de Kubernetes hello usando Olá `kubectl run` comando.</span><span class="sxs-lookup"><span data-stu-id="727c4-182">Run your container in hello Kubernetes cluster by using hello `kubectl run` command.</span></span> <span data-ttu-id="727c4-183">Forneça um nome de serviço para seu aplicativo em Kubernetes e o nome de imagem completa de saudação.</span><span class="sxs-lookup"><span data-stu-id="727c4-183">Give a service name for your app in Kubernetes and hello full image name.</span></span> <span data-ttu-id="727c4-184">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="727c4-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="727c4-185">Neste comando:</span><span class="sxs-lookup"><span data-stu-id="727c4-185">In this command:</span></span>

   * <span data-ttu-id="727c4-186">nome do contêiner Olá `gs-spring-boot-docker` é especificada imediatamente após Olá `run` comando</span><span class="sxs-lookup"><span data-stu-id="727c4-186">hello container name `gs-spring-boot-docker` is specified immediately after hello `run` command</span></span>

   * <span data-ttu-id="727c4-187">Olá `--image` parâmetro especifica Olá combinados server de logon e o nome da imagem como`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="727c4-187">hello `--image` parameter specifies hello combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="727c4-188">Expor seu cluster Kubernetes externamente usando Olá `kubectl expose` comando.</span><span class="sxs-lookup"><span data-stu-id="727c4-188">Expose your Kubernetes cluster externally by using hello `kubectl expose` command.</span></span> <span data-ttu-id="727c4-189">Especifique o nome do serviço, Olá público TCP porta usada tooaccess Olá aplicativo e a porta de destino interno Olá em que seu aplicativo escuta.</span><span class="sxs-lookup"><span data-stu-id="727c4-189">Specify your service name, hello public-facing TCP port used tooaccess hello app, and hello internal target port your app listens on.</span></span> <span data-ttu-id="727c4-190">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="727c4-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="727c4-191">Neste comando:</span><span class="sxs-lookup"><span data-stu-id="727c4-191">In this command:</span></span>

   * <span data-ttu-id="727c4-192">nome do contêiner Olá `gs-spring-boot-docker` é especificada imediatamente após Olá `expose deployment` comando</span><span class="sxs-lookup"><span data-stu-id="727c4-192">hello container name `gs-spring-boot-docker` is specified immediately after hello `expose deployment` command</span></span>

   * <span data-ttu-id="727c4-193">Olá `--type` parâmetro especifica esse cluster Olá usa o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="727c4-193">hello `--type` parameter specifies that hello cluster uses load balancer</span></span>

   * <span data-ttu-id="727c4-194">Olá `--port` parâmetro especifica Olá público porta TCP 80.</span><span class="sxs-lookup"><span data-stu-id="727c4-194">hello `--port` parameter specifies hello public-facing TCP port of 80.</span></span> <span data-ttu-id="727c4-195">Acessar o aplicativo hello nesta porta.</span><span class="sxs-lookup"><span data-stu-id="727c4-195">You access hello app on this port.</span></span>

   * <span data-ttu-id="727c4-196">Olá `--target-port` parâmetro especifica Olá interno TCP porta 8080.</span><span class="sxs-lookup"><span data-stu-id="727c4-196">hello `--target-port` parameter specifies hello internal TCP port of 8080.</span></span> <span data-ttu-id="727c4-197">o balanceador de carga Olá encaminha solicitações tooyour aplicativo nesta porta.</span><span class="sxs-lookup"><span data-stu-id="727c4-197">hello load balancer forwards requests tooyour app on this port.</span></span>

1. <span data-ttu-id="727c4-198">Depois que o aplicativo hello é implantado toohello cluster, endereço IP externo de saudação de consulta e abri-lo no seu navegador da web:</span><span class="sxs-lookup"><span data-stu-id="727c4-198">Once hello app is deployed toohello cluster, query hello external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Procurar aplicativo de exemplo no Azure][SB02]


## <a name="next-steps"></a><span data-ttu-id="727c4-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="727c4-200">Next steps</span></span>

<span data-ttu-id="727c4-201">Para obter mais informações sobre como usar a inicialização de Spring no Azure, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="727c4-201">For more information about using Spring Boot on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="727c4-202">Implantar um toohello Spring aplicativo de inicialização do serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="727c4-202">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="727c4-203">Implantar um aplicativo de inicialização Spring em Linux em hello Azure serviço de contêiner</span><span class="sxs-lookup"><span data-stu-id="727c4-203">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="727c4-204">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="727c4-204">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="727c4-205">Para obter mais informações sobre Olá Spring inicialização no projeto de exemplo do Docker, consulte [inicialização Spring no guia de Introdução do Docker].</span><span class="sxs-lookup"><span data-stu-id="727c4-205">For more information about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="727c4-206">Olá links a seguir fornece informações adicionais sobre como criar aplicativos de inicialização Spring:</span><span class="sxs-lookup"><span data-stu-id="727c4-206">hello following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="727c4-207">Para obter mais informações sobre como criar um aplicativo de inicialização de Spring simples, consulte Olá Spring Initializr em https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="727c4-207">For more information about creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="727c4-208">Olá, links a seguir fornecem informações adicionais sobre como usar Kubernetes com o Azure:</span><span class="sxs-lookup"><span data-stu-id="727c4-208">hello following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="727c4-209">Introdução ao cluster Kubernetes no Serviço de Contêiner</span><span class="sxs-lookup"><span data-stu-id="727c4-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="727c4-210">Usando Olá Kubernetes web da interface do usuário com o serviço de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="727c4-210">Using hello Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="727c4-211">Para obter mais informações sobre como usar a interface de linha de comando Kubernetes estão disponíveis no hello **kubectl** guia do usuário em <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="727c4-211">More information about using Kubernetes command-line interface is available in hello **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="727c4-212">site de Kubernetes Olá tem vários artigos que abordam o uso de imagens em registros privados:</span><span class="sxs-lookup"><span data-stu-id="727c4-212">hello Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="727c4-213">[Configurar contas de serviço para Pods]</span><span class="sxs-lookup"><span data-stu-id="727c4-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="727c4-214">[Namespaces]</span><span class="sxs-lookup"><span data-stu-id="727c4-214">[Namespaces]</span></span>
* <span data-ttu-id="727c4-215">[Extrair uma imagem de um registro privado]</span><span class="sxs-lookup"><span data-stu-id="727c4-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="727c4-216">Para obter exemplos adicionais para como toouse Docker personalizado imagens com o Azure, consulte [usando uma imagem personalizada do Docker para o aplicativo Web do Azure no Linux].</span><span class="sxs-lookup"><span data-stu-id="727c4-216">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure Interface de linha de comando (CLI)]: /cli/azure/overview
[Serviço de contêiner do azure (ACS)]: https://azure.microsoft.com/services/container-service/
[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[usando uma imagem personalizada do Docker para o aplicativo Web do Azure no Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[ferramentas Java para o Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring inicialização]: http://projects.spring.io/spring-boot/
[inicialização Spring no guia de Introdução do Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configurar contas de serviço para Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Extrair uma imagem de um registro privado]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
