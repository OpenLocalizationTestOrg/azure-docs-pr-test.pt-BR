---
title: "aaaDeploy toohello um Spring aplicativo de inicialização do serviço de aplicativo do Azure | Microsoft Docs"
description: "Este tutorial serve como guia desenvolvedores Olá etapas toodeploy Olá Spring inicialização Introdução web aplicativo tooAzure do serviço de aplicativo."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 69f9c4903fd740125194402cdb4b4db46a1f2773
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a><span data-ttu-id="a1aed-103">Implantar um toohello Spring aplicativo de inicialização do serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="a1aed-103">Deploy a Spring Boot Application toohello Azure App Service</span></span>

<span data-ttu-id="a1aed-104">Olá  **[Spring Framework]**  é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial e um dos projetos mais populares hello, que é criada sobre essa plataforma é [Spring inicialização], que fornece um método simplificado para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="a1aed-104">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="a1aed-105">Este tutorial irá orientá-lo a criar embora Spring inicialização Introdução aplicativo de web de exemplo hello e implantá-lo muito[do serviço de aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="a1aed-105">This tutorial will walk you though creating hello sample Spring Boot Getting Started web app and deploying it too[Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a1aed-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a1aed-106">Prerequisites</span></span>

<span data-ttu-id="a1aed-107">Em ordem toocomplete Olá etapas deste tutorial, você precisa fazer toohave Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="a1aed-107">In order toocomplete hello steps in this tutorial, you need toohave hello following:</span></span>

* <span data-ttu-id="a1aed-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="a1aed-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="a1aed-109">Um [JDK (Java Developer Kit)] atualizado.</span><span class="sxs-lookup"><span data-stu-id="a1aed-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="a1aed-110">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="a1aed-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="a1aed-111">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="a1aed-111">A [Git] client.</span></span>

## <a name="create-hello-spring-boot-getting-started-web-app"></a><span data-ttu-id="a1aed-112">Criar aplicativo web e guia de Introdução do Spring inicialização Olá</span><span class="sxs-lookup"><span data-stu-id="a1aed-112">Create hello Spring Boot Getting Started web app</span></span>

<span data-ttu-id="a1aed-113">Olá etapas a seguir orientará você pelas etapas de saudação toocreate necessário um aplicativo de web Spring inicialização simples e testá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="a1aed-113">hello following steps will walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="a1aed-114">Abra um prompt de comando e criar um diretório local toohold seu aplicativo e altere o diretório toothat; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1aed-114">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="a1aed-115">-- ou --</span><span class="sxs-lookup"><span data-stu-id="a1aed-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="a1aed-116">Saudação de clone [Spring inicialização Introdução] projeto de exemplo no diretório Olá recém-criada; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1aed-116">Clone hello [Spring Boot Getting Started] sample project into hello directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="a1aed-117">Alterar diretório toohello concluída projeto; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1aed-117">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="a1aed-118">Criar arquivo JAR de saudação usando Maven; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1aed-118">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="a1aed-119">Quando Olá web aplicativo tiver sido criado, alterar diretório toohello JAR arquivo e iniciar o aplicativo da web de saudação; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1aed-119">Once hello web app has been created, change directory toohello JAR file and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="a1aed-120">Testar o aplicativo web de saudação navegando toohttp://localhost:8080 usando um navegador da web, ou usar a sintaxe de saudação como Olá exemplo a seguir se você tiver ondulação disponível:</span><span class="sxs-lookup"><span data-stu-id="a1aed-120">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="a1aed-121">Você deve ver Olá mensagem exibida a seguir: **saudações de inicialização Spring!**</span><span class="sxs-lookup"><span data-stu-id="a1aed-121">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Pesquisar aplicativo de exemplo][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="a1aed-123">Criar um aplicativo Web do Azure para uso com Java</span><span class="sxs-lookup"><span data-stu-id="a1aed-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="a1aed-124">Olá etapas a seguir orientará Olá etapas toocreate um aplicativo Web do Azure, Olá necessário configurar para Java e configurar suas credenciais FTP.</span><span class="sxs-lookup"><span data-stu-id="a1aed-124">hello following steps will walk you through hello steps toocreate an Azure Web App, configure hello required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="a1aed-125">Procurar toohello [portal do Azure] e faça logon.</span><span class="sxs-lookup"><span data-stu-id="a1aed-125">Browse toohello [Azure portal] and log in.</span></span>

1. <span data-ttu-id="a1aed-126">Depois de fazer logon na sua conta em Olá portal do Azure, clique o ícone do menu de saudação para **serviços de aplicativos**:</span><span class="sxs-lookup"><span data-stu-id="a1aed-126">Once you have logged into your account on hello Azure portal, click hello menu icon for **App Services**:</span></span>
   
   ![Portal do Azure][AZ01]

1. <span data-ttu-id="a1aed-128">Olá quando **serviços de aplicativos** página é exibida, clique em **+ adicionar** toocreate um novo serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a1aed-128">When hello **App Services** page is displayed, click **+ Add** toocreate a new App Service.</span></span>

   ![Criar Serviço de Aplicativo][AZ02]

1. <span data-ttu-id="a1aed-130">Quando Olá lista de modelos de aplicativo da web é exibida, clique em link Olá Olá básica aplicativo Web do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a1aed-130">When hello list of web app templates is displayed, click hello link for hello basic Microsoft Web App.</span></span>

   ![Modelos de aplicativo Web][AZ03]

1. <span data-ttu-id="a1aed-132">Quando a página de informações de Olá para o modelo de aplicativo Web hello for exibida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="a1aed-132">When hello information page for hello Web App template is displayed, click **Create**.</span></span>

   ![Criar um aplicativo Web][AZ04]

1. <span data-ttu-id="a1aed-134">Forneça um nome exclusivo para o aplicativo Web, especifique configurações adicionais e **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a1aed-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Criar Configurações de Aplicativo Web][AZ05]

1. <span data-ttu-id="a1aed-136">Quando seu aplicativo web tiver sido criado, clique em ícone do menu Olá para **serviços de aplicativos**e, em seguida, clique em seu aplicativo web criado recentemente:</span><span class="sxs-lookup"><span data-stu-id="a1aed-136">Once your web app has been created, click hello menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Listar Aplicativos Web][AZ06]

1. <span data-ttu-id="a1aed-138">Quando seu aplicativo web é exibido, especifique a versão do Java Olá usando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1aed-138">When your web app is displayed, specify hello Java version by using hello following steps:</span></span>

   <span data-ttu-id="a1aed-139">a.</span><span class="sxs-lookup"><span data-stu-id="a1aed-139">a.</span></span> <span data-ttu-id="a1aed-140">Clique em Olá **configurações de aplicativo** item de menu.</span><span class="sxs-lookup"><span data-stu-id="a1aed-140">Click hello **Application Settings** menu item.</span></span>

   <span data-ttu-id="a1aed-141">b.</span><span class="sxs-lookup"><span data-stu-id="a1aed-141">b.</span></span> <span data-ttu-id="a1aed-142">Escolha **Java 8** para a versão do Java hello.</span><span class="sxs-lookup"><span data-stu-id="a1aed-142">Choose **Java 8** for hello Java version.</span></span>

   <span data-ttu-id="a1aed-143">c.</span><span class="sxs-lookup"><span data-stu-id="a1aed-143">c.</span></span> <span data-ttu-id="a1aed-144">Escolha **Newest** para a versão secundária do Java de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1aed-144">Choose **Newest** for hello minor Java version.</span></span>

   <span data-ttu-id="a1aed-145">d.</span><span class="sxs-lookup"><span data-stu-id="a1aed-145">d.</span></span> <span data-ttu-id="a1aed-146">Escolha **8.5 mais recente do Tomcat** para o contêiner da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1aed-146">Choose **Newest Tomcat 8.5** for hello web container.</span></span> <span data-ttu-id="a1aed-147">(Esse contêiner não será realmente usado; Azure usará o contêiner de saudação do seu aplicativo de inicialização de Spring.)</span><span class="sxs-lookup"><span data-stu-id="a1aed-147">(This container will not actually be used; Azure will use hello container from your Spring Boot application.)</span></span>

   <span data-ttu-id="a1aed-148">e.</span><span class="sxs-lookup"><span data-stu-id="a1aed-148">e.</span></span> <span data-ttu-id="a1aed-149">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a1aed-149">Click **Save**.</span></span>

   ![Configurações do aplicativo][AZ07]

1. <span data-ttu-id="a1aed-151">Especifique suas credenciais de implantação de FTP usando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1aed-151">Specify your FTP deployment credentials by using hello following steps:</span></span>

   <span data-ttu-id="a1aed-152">a.</span><span class="sxs-lookup"><span data-stu-id="a1aed-152">a.</span></span> <span data-ttu-id="a1aed-153">Clique em Olá **credenciais de implantação** item de menu.</span><span class="sxs-lookup"><span data-stu-id="a1aed-153">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="a1aed-154">b.</span><span class="sxs-lookup"><span data-stu-id="a1aed-154">b.</span></span> <span data-ttu-id="a1aed-155">Especifique o nome de usuário e a senha.</span><span class="sxs-lookup"><span data-stu-id="a1aed-155">Specify your username and password.</span></span>

   <span data-ttu-id="a1aed-156">c.</span><span class="sxs-lookup"><span data-stu-id="a1aed-156">c.</span></span> <span data-ttu-id="a1aed-157">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a1aed-157">Click **Save**.</span></span>

   ![Especificar Credenciais de Implantação][AZ08]

1. <span data-ttu-id="a1aed-159">Recupere as informações de conexão de FTP usando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1aed-159">Retrieve your FTP connection information by using hello following steps:</span></span>

   <span data-ttu-id="a1aed-160">a.</span><span class="sxs-lookup"><span data-stu-id="a1aed-160">a.</span></span> <span data-ttu-id="a1aed-161">Clique em Olá **credenciais de implantação** item de menu.</span><span class="sxs-lookup"><span data-stu-id="a1aed-161">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="a1aed-162">b.</span><span class="sxs-lookup"><span data-stu-id="a1aed-162">b.</span></span> <span data-ttu-id="a1aed-163">Copie o seu nome de usuário FTP completo e a URL e salvá-las para a próxima seção Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="a1aed-163">Copy your full FTP username and URL and save them for hello next section of this tutorial.</span></span>

   ![URL FTP e Credenciais][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a><span data-ttu-id="a1aed-165">Implantar seu tooAzure de aplicativo web inicialização Spring</span><span class="sxs-lookup"><span data-stu-id="a1aed-165">Deploy your Spring Boot web app tooAzure</span></span>

<span data-ttu-id="a1aed-166">Olá, as etapas a seguir explicará Olá etapas toodeploy seu tooAzure de aplicativo web Spring inicialização.</span><span class="sxs-lookup"><span data-stu-id="a1aed-166">hello following steps will walk you through hello steps toodeploy your Spring Boot web app tooAzure.</span></span>

1. <span data-ttu-id="a1aed-167">Abra um editor de texto como o bloco de notas do Windows e cole Olá texto a seguir em um novo documento e salve o arquivo hello como *Web. config*:</span><span class="sxs-lookup"><span data-stu-id="a1aed-167">Open a text editor such as Windows Notepad and paste hello following text into a new document, then save hello file as *web.config*:</span></span>
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. <span data-ttu-id="a1aed-168">Depois que você salvou Olá *Web. config* tooyour sistema de arquivos, conecte-se o aplicativo da web de tooyour por meio de FTP usando Olá URL, nome de usuário e senha da saudação anterior seção deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="a1aed-168">After you have saved hello *web.config* file tooyour system, connect tooyour web app via FTP using hello URL, username, and password from hello preceding section of this tutorial.</span></span> <span data-ttu-id="a1aed-169">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1aed-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="a1aed-170">Pasta de raiz de toohello alteração Olá diretório remoto do seu aplicativo web, (que está no */site/wwwroot*) e copie o arquivo JAR de saudação do seu aplicativo de inicialização de Spring e Olá *Web. config* anteriores.</span><span class="sxs-lookup"><span data-stu-id="a1aed-170">Change hello remote directory toohello root folder of your web app, (which is at */site/wwwroot*), then copy hello JAR file from your Spring Boot application and hello *web.config* from earlier.</span></span> <span data-ttu-id="a1aed-171">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1aed-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="a1aed-172">Depois que você implantou seu JAR e *Web. config* arquivos tooyour web app, você precisa toorestart seu aplicativo web usando Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="a1aed-172">After you have deployed your JAR and *web.config* files tooyour web app, you need toorestart your web app using hello Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="a1aed-173">Testar o aplicativo de web de saudação navegando URL do aplicativo da web tooyour usando um navegador da web, ou usar a sintaxe de saudação como Olá exemplo a seguir se você tiver ondulação disponível:</span><span class="sxs-lookup"><span data-stu-id="a1aed-173">Test hello web app by browsing tooyour web app's URL using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="a1aed-174">Você deve ver Olá mensagem exibida a seguir: **saudações de inicialização Spring!**</span><span class="sxs-lookup"><span data-stu-id="a1aed-174">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Pesquisar aplicativo de exemplo][SB02]

## <a name="next-steps"></a><span data-ttu-id="a1aed-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a1aed-176">Next steps</span></span>

<span data-ttu-id="a1aed-177">Para obter mais informações sobre como usar aplicativos de inicialização Spring no Azure, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1aed-177">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="a1aed-178">Implantar um aplicativo de inicialização Spring em Linux em hello Azure serviço de contêiner</span><span class="sxs-lookup"><span data-stu-id="a1aed-178">Deploy a Spring Boot Application on Linux in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="a1aed-179">Implantar um aplicativo de inicialização Spring em um Cluster de Kubernetes no hello Azure serviço de contêiner</span><span class="sxs-lookup"><span data-stu-id="a1aed-179">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="a1aed-180">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="a1aed-180">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="a1aed-181">Para obter informações adicionais sobre depoying tooAzure de aplicativos de web usando FTP, consulte [implantar tooAzure seu aplicativo do serviço de aplicativo usando o FTP/S].</span><span class="sxs-lookup"><span data-stu-id="a1aed-181">For additional information about depoying web apps tooAzure using FTP, see [Deploy your app tooAzure App Service using FTP/S].</span></span>

<span data-ttu-id="a1aed-182">Para obter mais detalhes sobre o projeto de exemplo hello Spring inicialização, consulte [Spring inicialização Introdução].</span><span class="sxs-lookup"><span data-stu-id="a1aed-182">For further details about hello Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="a1aed-183">Para obter ajuda com a guia de Introdução com seus próprios aplicativos de inicialização Spring, consulte Olá **Initializr Spring** em https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="a1aed-183">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="a1aed-184">Para obter mais informações sobre como definir configurações adicionais para o aplicativo Web, confira [Configurar aplicativos Web no Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="a1aed-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

[do serviço de aplicativo do Azure]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[portal do Azure]: https://portal.azure.com/
[Configurar aplicativos Web no Serviço de Aplicativo do Azure]: /azure/app-service-web/web-sites-configure
[implantar tooAzure seu aplicativo do serviço de aplicativo usando o FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[ferramentas Java para o Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring inicialização]: http://projects.spring.io/spring-boot/
[Spring inicialização Introdução]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB01.png
[SB02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB02.png

[AZ01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ01.png
[AZ02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ02.png
[AZ03]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ03.png
[AZ04]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ04.png
[AZ05]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ05.png
[AZ06]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ06.png
[AZ07]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ07.png
[AZ08]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ08.png
[AZ09]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ09.png
[AZ10]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ10.png
