---
title: "aaaHow toouse Olá Maven plug-in para aplicativos Web do Azure toodeploy um tooAzure de aplicativo de inicialização de Spring em contêineres"
description: "Saiba como toouse hello Maven plug-in para aplicativos Web do Azure toodeploy um tooAzure do aplicativo de inicialização de Spring."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: e7e760d4ef5bd4c92a4126a50a2b12e5c8f2b4a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-containerized-spring-boot-app-tooazure"></a><span data-ttu-id="0ba66-103">Como toouse hello Maven plug-in para aplicativos Web do Azure toodeploy um tooAzure de aplicativo de inicialização de Spring em contêineres</span><span class="sxs-lookup"><span data-stu-id="0ba66-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>

<span data-ttu-id="0ba66-104">Olá [Maven plug-in para aplicativos Web do Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) para [Apache Maven](http://maven.apache.org/) fornece integração perfeita de serviço de aplicativo do Azure em projetos Maven e simplifica o processo de saudação para desenvolvedores toodeploy web aplicativos tooAzure do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ba66-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service .</span></span>

<span data-ttu-id="0ba66-105">Este artigo demonstra como usar Olá Maven plug-in para aplicativos Web do Azure toodeploy um aplicativo de inicialização de Spring de exemplo em um contêiner de Docker tooAzure serviços de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0ba66-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application in a Docker container tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="0ba66-106">Olá Maven plug-in para aplicativos Web do Azure está disponível como uma visualização.</span><span class="sxs-lookup"><span data-stu-id="0ba66-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="0ba66-107">Por enquanto, somente a publicação FTP tem suporte, embora recursos adicionais foram planejados para Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="0ba66-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="0ba66-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0ba66-108">Prerequisites</span></span>

<span data-ttu-id="0ba66-109">Em ordem toocomplete Olá etapas deste tutorial, você precisa toohave Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ba66-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="0ba66-110">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="0ba66-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="0ba66-111">Olá [Azure Interface de linha de comando (CLI)].</span><span class="sxs-lookup"><span data-stu-id="0ba66-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="0ba66-112">Um JDK (Java Development Kit) versão 1.7 ou posterior atualizado.</span><span class="sxs-lookup"><span data-stu-id="0ba66-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="0ba66-113">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="0ba66-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="0ba66-114">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="0ba66-114">A [Git] client.</span></span>
* <span data-ttu-id="0ba66-115">Um cliente do [Docker].</span><span class="sxs-lookup"><span data-stu-id="0ba66-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="0ba66-116">Devido a requisitos de virtualização toohello deste tutorial, você não conseguir seguir etapas Olá neste artigo em uma máquina virtual. Você deve usar um computador físico com recursos de virtualização habilitados.</span><span class="sxs-lookup"><span data-stu-id="0ba66-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="0ba66-117">Exemplo de hello clone Spring inicialização no aplicativo web de Docker</span><span class="sxs-lookup"><span data-stu-id="0ba66-117">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="0ba66-118">Nesta seção, você clonará um aplicativo Spring Boot em contêineres e o testará localmente.</span><span class="sxs-lookup"><span data-stu-id="0ba66-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="0ba66-119">Abra um prompt de comando ou a janela do terminal e criar um diretório local toohold seu aplicativo de inicialização de Spring e altere o diretório toothat; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ba66-119">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="0ba66-120">-- ou --</span><span class="sxs-lookup"><span data-stu-id="0ba66-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="0ba66-121">Saudação de clone [inicialização Spring no guia de Introdução do Docker] projeto de exemplo no diretório Olá criado; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ba66-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="0ba66-122">Alterar diretório toohello concluída projeto; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ba66-122">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="0ba66-123">Criar arquivo JAR de saudação usando Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ba66-123">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="0ba66-124">Quando o aplicativo da web de saudação tiver sido criado, iniciar Olá web app usando Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ba66-124">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="0ba66-125">Testar o aplicativo da web de saudação navegando tooit localmente usando um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="0ba66-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="0ba66-126">Por exemplo, você pode usar o hello comando a seguir se você tiver ondulação disponível:</span><span class="sxs-lookup"><span data-stu-id="0ba66-126">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="0ba66-127">Você deve ver Olá mensagem exibida a seguir: **Docker Olá, mundo**</span><span class="sxs-lookup"><span data-stu-id="0ba66-127">You should see hello following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="0ba66-128">Criar uma entidade de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="0ba66-128">Create an Azure service principal</span></span>

<span data-ttu-id="0ba66-129">Nesta seção, você criará um Azure entidade de serviço que Olá usos de plug-in Maven durante a implantação de seu contêiner tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0ba66-129">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="0ba66-130">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="0ba66-130">Open a command prompt.</span></span>

1. <span data-ttu-id="0ba66-131">Entre em sua conta do Azure usando Olá CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="0ba66-131">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="0ba66-132">Siga Olá instruções toocomplete Olá processo de entrada.</span><span class="sxs-lookup"><span data-stu-id="0ba66-132">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="0ba66-133">Crie uma entidade de serviço do Azure:</span><span class="sxs-lookup"><span data-stu-id="0ba66-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="0ba66-134">Onde `uuuuuuuu` é o nome de usuário hello e `pppppppp` é a senha Olá Olá entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="0ba66-134">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="0ba66-135">Azure responde com JSON que é semelhante a saudação de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ba66-135">Azure responds with JSON that resembles hello following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="0ba66-136">Você usará os valores de saudação dessa resposta JSON quando você configura Olá Maven plug-in toodeploy tooAzure seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="0ba66-136">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="0ba66-137">Olá `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, e `tttttttt` são valores de espaço reservado, que são usados em toomake Este exemplo-toomap mais fácil esses elementos de respectivos do tootheir valores quando você configura o Maven `settings.xml` arquivo hello lado seção.</span><span class="sxs-lookup"><span data-stu-id="0ba66-137">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="0ba66-138">Configurar Maven toouse a entidade de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="0ba66-138">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="0ba66-139">Nesta seção, você pode usar valores de saudação da autenticação de saudação de tooconfigure principal de serviço do Azure Maven usará ao implantar seu contêiner tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0ba66-139">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven will use when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="0ba66-140">Abra o Maven `settings.xml` arquivo em um editor de texto; este arquivo pode estar em um caminho como Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ba66-140">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="0ba66-141">Adicionar suas configurações de serviço do Azure principal da seção anterior Olá este tutorial toohello `<servers>` coleção em Olá *settings.xml* arquivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ba66-141">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="0ba66-142">Em que:</span><span class="sxs-lookup"><span data-stu-id="0ba66-142">Where:</span></span>
   <span data-ttu-id="0ba66-143">Elemento</span><span class="sxs-lookup"><span data-stu-id="0ba66-143">Element</span></span> | <span data-ttu-id="0ba66-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="0ba66-144">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="0ba66-145">Especifica um nome exclusivo que Maven usa toolook suas configurações de segurança quando você implanta seu tooAzure de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="0ba66-145">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="0ba66-146">Contém Olá `appId` valor da sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="0ba66-146">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="0ba66-147">Contém Olá `tenant` valor da sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="0ba66-147">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="0ba66-148">Contém Olá `password` valor da sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="0ba66-148">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="0ba66-149">Define o ambiente de nuvem do Azure de destino hello, que é `AZURE` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="0ba66-149">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="0ba66-150">(Uma lista completa dos ambientes está disponível no hello [Maven plug-in para aplicativos Web do Azure] documentação)</span><span class="sxs-lookup"><span data-stu-id="0ba66-150">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="0ba66-151">Salve e feche o hello *settings.xml* arquivo.</span><span class="sxs-lookup"><span data-stu-id="0ba66-151">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-toodocker-hub"></a><span data-ttu-id="0ba66-152">OPCIONAL: Implantar o seu local tooDocker de arquivo Docker Hub</span><span class="sxs-lookup"><span data-stu-id="0ba66-152">OPTIONAL: Deploy your local Docker file tooDocker Hub</span></span>

<span data-ttu-id="0ba66-153">Se você tiver uma conta do Docker, você pode criar seu Docker imagem de contêiner localmente e envie tooDocker Hub.</span><span class="sxs-lookup"><span data-stu-id="0ba66-153">If you have a Docker account, you can build your Docker container image locally and push it tooDocker Hub.</span></span> <span data-ttu-id="0ba66-154">Assim, o toodo usar Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="0ba66-154">toodo so, use hello following steps.</span></span>

1. <span data-ttu-id="0ba66-155">Olá abrir `pom.xml` arquivo para seu aplicativo de inicialização de Spring em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="0ba66-155">Open hello `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="0ba66-156">Localizar Olá `<imageName>` elemento filho do hello `<containerSettings>` elemento.</span><span class="sxs-lookup"><span data-stu-id="0ba66-156">Locate hello `<imageName>` child element of hello `<containerSettings>` element.</span></span>

1. <span data-ttu-id="0ba66-157">Saudação de atualização `${docker.image.prefix}` valor com o nome da sua conta de Docker:</span><span class="sxs-lookup"><span data-stu-id="0ba66-157">Update hello `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="0ba66-158">Escolha uma saudação métodos de implantação a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ba66-158">Choose one of hello following deployment methods:</span></span>

   * <span data-ttu-id="0ba66-159">Criar sua imagem de contêiner localmente com o Maven e então use Docker toopush tooDocker seu contêiner Hub:</span><span class="sxs-lookup"><span data-stu-id="0ba66-159">Build your container image locally with Maven, and then use Docker toopush your container tooDocker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="0ba66-160">Se você tiver Olá [Docker plug-in para Maven] instalado, você pode criar automaticamente e tooDocker sua imagem de contêiner Hub usando Olá `-DpushImage` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="0ba66-160">If you have hello [Docker plugin for Maven] installed, you can automatically build and your container image tooDocker Hub by using hello `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-tooazure"></a><span data-ttu-id="0ba66-161">OPCIONAL: Personalizar sua pom.xml antes de implantar seu tooAzure de contêiner</span><span class="sxs-lookup"><span data-stu-id="0ba66-161">OPTIONAL: Customize your pom.xml before deploying your container tooAzure</span></span>

<span data-ttu-id="0ba66-162">Olá abrir `pom.xml` de arquivo para o seu aplicativo de inicialização de Spring em um editor de texto e localize Olá `<plugin>` elemento para `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="0ba66-162">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="0ba66-163">Esse elemento deve ser semelhante a saudação de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ba66-163">This element should resemble hello following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="0ba66-164">Há vários valores que você pode modificar para plug-in do hello Maven e uma descrição detalhada de cada um desses elementos está disponível no hello [Maven plug-in para aplicativos Web do Azure] documentação.</span><span class="sxs-lookup"><span data-stu-id="0ba66-164">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="0ba66-165">Dito isso, vale a pena destacar diversos valores neste artigo:</span><span class="sxs-lookup"><span data-stu-id="0ba66-165">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="0ba66-166">Elemento</span><span class="sxs-lookup"><span data-stu-id="0ba66-166">Element</span></span> | <span data-ttu-id="0ba66-167">Descrição</span><span class="sxs-lookup"><span data-stu-id="0ba66-167">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="0ba66-168">Especifica a versão de saudação do hello [Maven plug-in para aplicativos Web do Azure].</span><span class="sxs-lookup"><span data-stu-id="0ba66-168">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="0ba66-169">Você deve verificar a versão Olá listado no hello [repositório Central Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) Olá tooensure que você está usando a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="0ba66-169">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="0ba66-170">Especifica as informações de autenticação de saudação do Azure, que neste exemplo contém um `<serverId>` elemento que contém `azure-auth`; Maven usa toolook esse valor valores principal de serviço do Azure Olá em seu Maven *settings.xml* arquivo, que você definiu em uma seção anterior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="0ba66-170">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="0ba66-171">Especifica o grupo de recursos de destino hello, que é `maven-plugin` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="0ba66-171">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="0ba66-172">grupo de recursos de saudação será criado durante a implantação se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="0ba66-172">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="0ba66-173">Especifica o nome do destino de saudação para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="0ba66-173">Specifies hello target name for your web app.</span></span> <span data-ttu-id="0ba66-174">Neste exemplo, o nome de destino de saudação é `maven-linux-app-${maven.build.timestamp}`, onde hello `${maven.build.timestamp}` sufixo é acrescentado em conflito de tooavoid neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="0ba66-174">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="0ba66-175">(Olá timestamp é opcional; você pode especificar qualquer cadeia de caracteres exclusiva para o nome do aplicativo hello.)</span><span class="sxs-lookup"><span data-stu-id="0ba66-175">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="0ba66-176">Especifica a região de destino hello, que neste exemplo é `westus`.</span><span class="sxs-lookup"><span data-stu-id="0ba66-176">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="0ba66-177">(Uma lista completa está em Olá [Maven plug-in para aplicativos Web do Azure] documentação.)</span><span class="sxs-lookup"><span data-stu-id="0ba66-177">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<appSettings>` | <span data-ttu-id="0ba66-178">Especifica qualquer configurações exclusivas para Maven toouse ao implantar seu tooAzure de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="0ba66-178">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="0ba66-179">Neste exemplo, um `<property>` elemento contém um par de nome/valor de elementos filho que especifique a porta Olá para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ba66-179">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="0ba66-180">número de porta de Olá Olá configurações toochange neste exemplo somente são necessárias quando você estiver alterando a porta de saudação do padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ba66-180">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

## <a name="build-and-deploy-your-container-tooazure"></a><span data-ttu-id="0ba66-181">Criar e implantar seu tooAzure de contêiner</span><span class="sxs-lookup"><span data-stu-id="0ba66-181">Build and deploy your container tooAzure</span></span>

<span data-ttu-id="0ba66-182">Depois de configurar todas as configurações de saudação em Olá anterior seções deste artigo, você está pronto toodeploy tooAzure seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="0ba66-182">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your container tooAzure.</span></span> <span data-ttu-id="0ba66-183">Assim, o toodo use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ba66-183">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="0ba66-184">No prompt de comando hello ou janela de terminal que você estava usando anteriormente, recriar o arquivo de JAR de hello usando Maven se você tiver feito qualquer toohello alterações *pom.xml* arquivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ba66-184">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="0ba66-185">Implantar seu tooAzure de aplicativo web usando Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ba66-185">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="0ba66-186">Maven implantará seu tooAzure de aplicativo da web; Se o aplicativo da web de saudação ainda não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="0ba66-186">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="0ba66-187">Se região Olá que você especifica no hello `<region>` elemento da sua *pom.xml* arquivo não tem servidores suficientes disponíveis quando você inicia a implantação, você poderá ver um toohello semelhante erro exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ba66-187">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="0ba66-188">Se isso acontecer, você pode especificar que outra região e execute novamente Olá Maven comando toodeploy seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ba66-188">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="0ba66-189">Quando sua web tiver sido implantada, você será capaz de toomanage usando Olá [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="0ba66-189">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="0ba66-190">Seu aplicativo Web será listado nos **Serviços de Aplicativos**:</span><span class="sxs-lookup"><span data-stu-id="0ba66-190">Your web app will be listed in **App Services**:</span></span>

   ![Aplicativo Web listado nos Serviços de Aplicativos do portal do Azure][AP01]

* <span data-ttu-id="0ba66-192">E Olá URL para seu aplicativo web será listado no hello **visão geral** para seu aplicativo web:</span><span class="sxs-lookup"><span data-stu-id="0ba66-192">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Determinando Olá URL para seu aplicativo web][AP02]

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

## <a name="next-steps"></a><span data-ttu-id="0ba66-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0ba66-194">Next steps</span></span>

<span data-ttu-id="0ba66-195">Para obter mais informações sobre Olá diversas tecnologias abordadas neste artigo, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ba66-195">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="0ba66-196">[Maven plug-in para aplicativos Web do Azure]</span><span class="sxs-lookup"><span data-stu-id="0ba66-196">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="0ba66-197">Faça logon no tooAzure de saudação CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0ba66-197">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="0ba66-198">Como toouse hello Maven plug-in para aplicativos Web do Azure toodeploy um aplicativo de inicialização de Spring tooAzure do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="0ba66-198">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure App Service </span></span>](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="0ba66-199">Criar uma entidade de serviço do Azure com a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="0ba66-199">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="0ba66-200">Referência de configurações do Maven</span><span class="sxs-lookup"><span data-stu-id="0ba66-200">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="0ba66-201">[Docker plug-in para Maven]</span><span class="sxs-lookup"><span data-stu-id="0ba66-201">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure Interface de linha de comando (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portal do Azure]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[Docker plug-in para Maven]: https://github.com/spotify/docker-maven-plugin
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[inicialização Spring no guia de Introdução do Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Maven plug-in para aplicativos Web do Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP02.png
