---
title: "aaaHow toouse Olá Maven plug-in para aplicativos Web do Azure toodeploy um tooAzure do aplicativo de inicialização de Spring"
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
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a><span data-ttu-id="21a96-103">Como toouse hello Maven plug-in para aplicativos Web do Azure toodeploy um tooAzure do aplicativo de inicialização de Spring</span><span class="sxs-lookup"><span data-stu-id="21a96-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure</span></span>

<span data-ttu-id="21a96-104">Olá [Maven plug-in para aplicativos Web do Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) para [Apache Maven](http://maven.apache.org/) fornece integração perfeita de serviço de aplicativo do Azure em projetos Maven e simplifica o processo de saudação para desenvolvedores toodeploy web aplicativos tooAzure do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="21a96-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service.</span></span>

<span data-ttu-id="21a96-105">Este artigo demonstra como usar Olá Maven plug-in para aplicativos Web do Azure toodeploy tooAzure de aplicativo de inicialização de Spring um exemplo serviços de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="21a96-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="21a96-106">Olá Maven plug-in para aplicativos Web do Azure está disponível como uma visualização.</span><span class="sxs-lookup"><span data-stu-id="21a96-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="21a96-107">Por enquanto, somente a publicação FTP tem suporte, embora recursos adicionais foram planejados para Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="21a96-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="21a96-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="21a96-108">Prerequisites</span></span>

<span data-ttu-id="21a96-109">Em ordem toocomplete Olá etapas deste tutorial, você precisa toohave Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="21a96-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="21a96-110">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="21a96-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="21a96-111">Olá [Azure Interface de linha de comando (CLI)].</span><span class="sxs-lookup"><span data-stu-id="21a96-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="21a96-112">Um JDK (Java Development Kit) versão 1.7 ou posterior atualizado.</span><span class="sxs-lookup"><span data-stu-id="21a96-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="21a96-113">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="21a96-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="21a96-114">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="21a96-114">A [Git] client.</span></span>

## <a name="clone-hello-sample-spring-boot-web-app"></a><span data-ttu-id="21a96-115">Aplicativo web do clone Olá exemplo inicialização Spring</span><span class="sxs-lookup"><span data-stu-id="21a96-115">Clone hello sample Spring Boot web app</span></span>

<span data-ttu-id="21a96-116">Nesta seção, você clonará um aplicativo Spring Boot concluído e o testará localmente.</span><span class="sxs-lookup"><span data-stu-id="21a96-116">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="21a96-117">Abra um prompt de comando ou a janela do terminal e criar um diretório local toohold seu aplicativo de inicialização de Spring e altere o diretório toothat; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="21a96-117">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="21a96-118">-- ou --</span><span class="sxs-lookup"><span data-stu-id="21a96-118">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="21a96-119">Saudação de clone [Spring inicialização Introdução] projeto de exemplo no diretório Olá criado; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="21a96-119">Clone hello [Spring Boot Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="21a96-120">Alterar diretório toohello concluída projeto; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="21a96-120">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="21a96-121">Criar arquivo JAR de saudação usando Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="21a96-121">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="21a96-122">Quando o aplicativo da web de saudação tiver sido criado, iniciar Olá web app usando Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="21a96-122">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="21a96-123">Testar o aplicativo da web de saudação navegando tooit localmente usando um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="21a96-123">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="21a96-124">Por exemplo, você pode usar o hello comando a seguir se você tiver ondulação disponível:</span><span class="sxs-lookup"><span data-stu-id="21a96-124">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="21a96-125">Você deve ver Olá mensagem exibida a seguir: **saudações de inicialização Spring!**</span><span class="sxs-lookup"><span data-stu-id="21a96-125">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="21a96-126">Criar uma entidade de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="21a96-126">Create an Azure service principal</span></span>

<span data-ttu-id="21a96-127">Nesta seção, você criará um Azure entidade de serviço que Olá usos de plug-in Maven ao implantar o tooAzure de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="21a96-127">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="21a96-128">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="21a96-128">Open a command prompt.</span></span>

1. <span data-ttu-id="21a96-129">Entre em sua conta do Azure usando Olá CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="21a96-129">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="21a96-130">Siga Olá instruções toocomplete Olá processo de entrada.</span><span class="sxs-lookup"><span data-stu-id="21a96-130">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="21a96-131">Crie uma entidade de serviço do Azure:</span><span class="sxs-lookup"><span data-stu-id="21a96-131">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="21a96-132">Onde `uuuuuuuu` é o nome de usuário hello e `pppppppp` é a senha Olá Olá entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="21a96-132">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="21a96-133">Azure responde com JSON que é semelhante a saudação de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="21a96-133">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="21a96-134">Quando você configura Olá Maven plug-in toodeploy seu tooAzure de aplicativo web, você usará valores hello essa resposta JSON.</span><span class="sxs-lookup"><span data-stu-id="21a96-134">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your web app tooAzure.</span></span> <span data-ttu-id="21a96-135">Olá `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, e `tttttttt` são valores de espaço reservado, que são usados em toomake Este exemplo-toomap mais fácil esses elementos de respectivos do tootheir valores quando você configura o Maven `settings.xml` arquivo hello lado seção.</span><span class="sxs-lookup"><span data-stu-id="21a96-135">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="21a96-136">Configurar Maven toouse a entidade de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="21a96-136">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="21a96-137">Nesta seção, você pode usar valores de saudação da autenticação de saudação de tooconfigure principal de serviço do Azure Maven usa ao implantar o tooAzure de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="21a96-137">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="21a96-138">Abra o Maven `settings.xml` arquivo em um editor de texto; este arquivo pode estar em um caminho como Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="21a96-138">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="21a96-139">Adicionar suas configurações de serviço do Azure principal da seção anterior Olá este tutorial toohello `<servers>` coleção em Olá *settings.xml* arquivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="21a96-139">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="21a96-140">Em que:</span><span class="sxs-lookup"><span data-stu-id="21a96-140">Where:</span></span>
   <span data-ttu-id="21a96-141">Elemento</span><span class="sxs-lookup"><span data-stu-id="21a96-141">Element</span></span> | <span data-ttu-id="21a96-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="21a96-142">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="21a96-143">Especifica um nome exclusivo que Maven usa toolook suas configurações de segurança quando você implanta seu tooAzure de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="21a96-143">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="21a96-144">Contém Olá `appId` valor da sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="21a96-144">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="21a96-145">Contém Olá `tenant` valor da sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="21a96-145">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="21a96-146">Contém Olá `password` valor da sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="21a96-146">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="21a96-147">Define o ambiente de nuvem do Azure de destino hello, que é `AZURE` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="21a96-147">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="21a96-148">(Uma lista completa dos ambientes está disponível no hello [Maven plug-in para aplicativos Web do Azure] documentação)</span><span class="sxs-lookup"><span data-stu-id="21a96-148">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="21a96-149">Salve e feche o hello *settings.xml* arquivo.</span><span class="sxs-lookup"><span data-stu-id="21a96-149">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a><span data-ttu-id="21a96-150">OPCIONAL: Personalizar sua pom.xml antes de implantar seu tooAzure de aplicativo web</span><span class="sxs-lookup"><span data-stu-id="21a96-150">OPTIONAL: Customize your pom.xml before deploying your web app tooAzure</span></span>

<span data-ttu-id="21a96-151">Olá abrir `pom.xml` de arquivo para o seu aplicativo de inicialização de Spring em um editor de texto e localize Olá `<plugin>` elemento para `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="21a96-151">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="21a96-152">Esse elemento deve ser semelhante a saudação de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="21a96-152">This element should resemble hello following example:</span></span>

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
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="21a96-153">Há vários valores que você pode modificar para plug-in do hello Maven e uma descrição detalhada de cada um desses elementos está disponível no hello [Maven plug-in para aplicativos Web do Azure] documentação.</span><span class="sxs-lookup"><span data-stu-id="21a96-153">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="21a96-154">Dito isso, vale a pena destacar diversos valores neste artigo:</span><span class="sxs-lookup"><span data-stu-id="21a96-154">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="21a96-155">Elemento</span><span class="sxs-lookup"><span data-stu-id="21a96-155">Element</span></span> | <span data-ttu-id="21a96-156">Descrição</span><span class="sxs-lookup"><span data-stu-id="21a96-156">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="21a96-157">Especifica a versão de saudação do hello [Maven plug-in para aplicativos Web do Azure].</span><span class="sxs-lookup"><span data-stu-id="21a96-157">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="21a96-158">Você deve verificar a versão Olá listado no hello [repositório Central Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) Olá tooensure que você está usando a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="21a96-158">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="21a96-159">Especifica as informações de autenticação de saudação do Azure, que neste exemplo contém um `<serverId>` elemento que contém `azure-auth`; Maven usa toolook esse valor valores principal de serviço do Azure Olá em seu Maven *settings.xml* arquivo, que você definiu em uma seção anterior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="21a96-159">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="21a96-160">Especifica o grupo de recursos de destino hello, que é `maven-plugin` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="21a96-160">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="21a96-161">grupo de recursos de saudação é criado durante a implantação, se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="21a96-161">hello resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="21a96-162">Especifica o nome do destino de saudação para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="21a96-162">Specifies hello target name for your web app.</span></span> <span data-ttu-id="21a96-163">Neste exemplo, o nome de destino de saudação é `maven-web-app-${maven.build.timestamp}`, onde hello `${maven.build.timestamp}` sufixo é acrescentado em conflito de tooavoid neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="21a96-163">In this example, hello target name is `maven-web-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="21a96-164">(Olá timestamp é opcional; você pode especificar qualquer cadeia de caracteres exclusiva para o nome do aplicativo hello.)</span><span class="sxs-lookup"><span data-stu-id="21a96-164">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="21a96-165">Especifica a região de destino hello, que neste exemplo é `westus`.</span><span class="sxs-lookup"><span data-stu-id="21a96-165">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="21a96-166">(Uma lista completa está em Olá [Maven plug-in para aplicativos Web do Azure] documentação.)</span><span class="sxs-lookup"><span data-stu-id="21a96-166">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="21a96-167">Especifica a versão de tempo de execução do Java Olá para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="21a96-167">Specifies hello Java runtime version for your web app.</span></span> <span data-ttu-id="21a96-168">(Uma lista completa está em Olá [Maven plug-in para aplicativos Web do Azure] documentação.)</span><span class="sxs-lookup"><span data-stu-id="21a96-168">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="21a96-169">Especifica o tipo de implantação para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="21a96-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="21a96-170">Por enquanto, somente o `ftp` tem suporte, embora o suporte para outros tipos de implantação esteja em desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="21a96-170">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="21a96-171">Especifica os recursos e os destinos que Maven usa ao implantar o tooAzure de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="21a96-171">Specifies resources and target destinations which Maven uses when deploying your web app tooAzure.</span></span> <span data-ttu-id="21a96-172">Neste exemplo, dois `<resource>` especificam que Maven implantará o arquivo JAR de saudação para seu aplicativo web e Olá *Web. config* arquivo de projeto de inicialização Spring hello.</span><span class="sxs-lookup"><span data-stu-id="21a96-172">In this example, two `<resource>` elements specify that Maven will deploy hello JAR file for your web app and hello *web.config* file from hello Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-tooazure"></a><span data-ttu-id="21a96-173">Criar e implantar seu tooAzure de aplicativo web</span><span class="sxs-lookup"><span data-stu-id="21a96-173">Build and deploy your web app tooAzure</span></span>

<span data-ttu-id="21a96-174">Depois de configurar todas as configurações de saudação em Olá anterior seções deste artigo, você está pronto toodeploy seu tooAzure de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="21a96-174">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your web app tooAzure.</span></span> <span data-ttu-id="21a96-175">Assim, o toodo use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="21a96-175">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="21a96-176">No prompt de comando hello ou janela de terminal que você estava usando anteriormente, recriar o arquivo de JAR de hello usando Maven se você tiver feito qualquer toohello alterações *pom.xml* arquivo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="21a96-176">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="21a96-177">Implantar seu tooAzure de aplicativo web usando Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="21a96-177">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="21a96-178">Maven implantará seu tooAzure de aplicativo da web; Se o aplicativo da web de saudação ainda não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="21a96-178">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

<span data-ttu-id="21a96-179">Quando sua web tiver sido implantada, você será capaz de toomanage usando Olá [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="21a96-179">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="21a96-180">Seu aplicativo Web será listado nos **Serviços de Aplicativos**:</span><span class="sxs-lookup"><span data-stu-id="21a96-180">Your web app will be listed in **App Services**:</span></span>

   ![Aplicativo Web listado nos Serviços de Aplicativos do portal do Azure][AP01]

* <span data-ttu-id="21a96-182">E Olá URL para seu aplicativo web será listado no hello **visão geral** para seu aplicativo web:</span><span class="sxs-lookup"><span data-stu-id="21a96-182">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="21a96-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="21a96-184">Next steps</span></span>

<span data-ttu-id="21a96-185">Para obter mais informações sobre Olá diversas tecnologias abordadas neste artigo, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="21a96-185">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="21a96-186">[Maven plug-in para aplicativos Web do Azure]</span><span class="sxs-lookup"><span data-stu-id="21a96-186">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="21a96-187">Faça logon no tooAzure de saudação CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="21a96-187">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="21a96-188">Como toouse hello Maven plug-in para aplicativos Web do Azure toodeploy um tooAzure de aplicativo de inicialização de Spring em contêineres</span><span class="sxs-lookup"><span data-stu-id="21a96-188">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="21a96-189">Criar uma entidade de serviço do Azure com a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="21a96-189">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="21a96-190">Referência de configurações do Maven</span><span class="sxs-lookup"><span data-stu-id="21a96-190">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure Interface de linha de comando (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portal do Azure]: https://portal.azure.com/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring inicialização Introdução]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven plug-in para aplicativos Web do Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
