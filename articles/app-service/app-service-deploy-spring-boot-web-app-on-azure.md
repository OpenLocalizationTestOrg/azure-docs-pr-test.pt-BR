---
title: "Implantar um aplicativo Spring Boot para o Serviço de Aplicativo do Azure | Microsoft Docs"
description: "Este tutorial orientará os desenvolvedores sobre as etapas para implantar o aplicativo Web Spring Boot Getting Started para o Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: 0c388862d927a1492745832225c686670c071f86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-to-the-azure-app-service"></a><span data-ttu-id="aa79d-103">Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="aa79d-103">Deploy a Spring Boot Application to the Azure App Service</span></span>

<span data-ttu-id="aa79d-104">O **[Spring Framework]** é uma solução de software livre que ajuda os desenvolvedores de Java a criar aplicativos de nível empresarial. Um dos projetos mais populares que se baseia nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="aa79d-104">The **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of the more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="aa79d-105">Este tutorial o orientará durante a criação do aplicativo Web de exemplo Spring Boot Getting Started e o implantará no [Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="aa79d-105">This tutorial will walk you though creating the sample Spring Boot Getting Started web app and deploying it to [Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="aa79d-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aa79d-106">Prerequisites</span></span>

<span data-ttu-id="aa79d-107">Para concluir as etapas deste tutorial, você precisa ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="aa79d-107">In order to complete the steps in this tutorial, you need to have the following:</span></span>

* <span data-ttu-id="aa79d-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="aa79d-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="aa79d-109">Um [JDK (Java Developer Kit)] atualizado.</span><span class="sxs-lookup"><span data-stu-id="aa79d-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="aa79d-110">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="aa79d-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="aa79d-111">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="aa79d-111">A [Git] client.</span></span>

## <a name="create-the-spring-boot-getting-started-web-app"></a><span data-ttu-id="aa79d-112">Criar o aplicativo Web Spring Boot Getting Started</span><span class="sxs-lookup"><span data-stu-id="aa79d-112">Create the Spring Boot Getting Started web app</span></span>

<span data-ttu-id="aa79d-113">As etapas a seguir explicarão as etapas necessárias para criar um aplicativo Web simples Spring Boot e testá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="aa79d-113">The following steps will walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="aa79d-114">Abra um prompt de comando, crie um diretório local para conter o aplicativo e altere para o diretório. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aa79d-114">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="aa79d-115">-- ou --</span><span class="sxs-lookup"><span data-stu-id="aa79d-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="aa79d-116">Clone o projeto de exemplo [Spring Boot Getting Started] para o diretório que você acabou de criar. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aa79d-116">Clone the [Spring Boot Getting Started] sample project into the directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="aa79d-117">Altere o diretório para o projeto concluído. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aa79d-117">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="aa79d-118">Crie o arquivo JAR usando o Maven. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aa79d-118">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="aa79d-119">Quando o aplicativo Web tiver sido criado, altere o diretório para o arquivo JAR e inicie o aplicativo Web. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aa79d-119">Once the web app has been created, change directory to the JAR file and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="aa79d-120">Teste o aplicativo Web navegando até http://localhost:8080 com um navegador da Web ou use a sintaxe semelhante ao seguinte exemplo, se você tiver o curl disponível:</span><span class="sxs-lookup"><span data-stu-id="aa79d-120">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="aa79d-121">Você verá a seguinte mensagem exibida: **Saudações do Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="aa79d-121">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Pesquisar aplicativo de exemplo][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="aa79d-123">Criar um aplicativo Web do Azure para uso com Java</span><span class="sxs-lookup"><span data-stu-id="aa79d-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="aa79d-124">As etapas a seguir explicarão as etapas para criar um aplicativo Web do Azure, definir as configurações necessárias para Java e configurar as credenciais de FTP.</span><span class="sxs-lookup"><span data-stu-id="aa79d-124">The following steps will walk you through the steps to create an Azure Web App, configure the required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="aa79d-125">Navegue até o [Portal do Azure] e faça logon.</span><span class="sxs-lookup"><span data-stu-id="aa79d-125">Browse to the [Azure portal] and log in.</span></span>

1. <span data-ttu-id="aa79d-126">Depois de fazer logon em sua conta no Portal do Azure, clique no ícone de menu dos **Serviços de Aplicativos**:</span><span class="sxs-lookup"><span data-stu-id="aa79d-126">Once you have logged into your account on the Azure portal, click the menu icon for **App Services**:</span></span>
   
   ![Portal do Azure][AZ01]

1. <span data-ttu-id="aa79d-128">Quando a página **Serviços de Aplicativos** for exibida, clique em **+Adicionar** para criar um novo Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aa79d-128">When the **App Services** page is displayed, click **+ Add** to create a new App Service.</span></span>

   ![Criar Serviço de Aplicativo][AZ02]

1. <span data-ttu-id="aa79d-130">Quando a lista de modelos de aplicativos Web for exibida, clique no link do Aplicativo Web da Microsoft básico.</span><span class="sxs-lookup"><span data-stu-id="aa79d-130">When the list of web app templates is displayed, click the link for the basic Microsoft Web App.</span></span>

   ![Modelos de aplicativo Web][AZ03]

1. <span data-ttu-id="aa79d-132">Quando a página de informações do modelo de Aplicativo Web for exibida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="aa79d-132">When the information page for the Web App template is displayed, click **Create**.</span></span>

   ![Criar um aplicativo Web][AZ04]

1. <span data-ttu-id="aa79d-134">Forneça um nome exclusivo para o aplicativo Web, especifique configurações adicionais e **Criar**.</span><span class="sxs-lookup"><span data-stu-id="aa79d-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Criar Configurações de Aplicativo Web][AZ05]

1. <span data-ttu-id="aa79d-136">Quando o aplicativo Web tiver sido criado, clique no ícone de menu dos **Serviços de Aplicativos**e clique no aplicativo Web recém-criado:</span><span class="sxs-lookup"><span data-stu-id="aa79d-136">Once your web app has been created, click the menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Listar Aplicativos Web][AZ06]

1. <span data-ttu-id="aa79d-138">Quando o aplicativo Web for exibido, especifique a versão do Java usando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="aa79d-138">When your web app is displayed, specify the Java version by using the following steps:</span></span>

   <span data-ttu-id="aa79d-139">a.</span><span class="sxs-lookup"><span data-stu-id="aa79d-139">a.</span></span> <span data-ttu-id="aa79d-140">Clique no item de menu **Configurações do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="aa79d-140">Click the **Application Settings** menu item.</span></span>

   <span data-ttu-id="aa79d-141">b.</span><span class="sxs-lookup"><span data-stu-id="aa79d-141">b.</span></span> <span data-ttu-id="aa79d-142">Escolha **Java 8** para a versão do Java.</span><span class="sxs-lookup"><span data-stu-id="aa79d-142">Choose **Java 8** for the Java version.</span></span>

   <span data-ttu-id="aa79d-143">c.</span><span class="sxs-lookup"><span data-stu-id="aa79d-143">c.</span></span> <span data-ttu-id="aa79d-144">Escolha **Mais recente** para a versão secundária do Java.</span><span class="sxs-lookup"><span data-stu-id="aa79d-144">Choose **Newest** for the minor Java version.</span></span>

   <span data-ttu-id="aa79d-145">d.</span><span class="sxs-lookup"><span data-stu-id="aa79d-145">d.</span></span> <span data-ttu-id="aa79d-146">Escolha **Tomcat 8.5 mais recente** para o contêiner da Web.</span><span class="sxs-lookup"><span data-stu-id="aa79d-146">Choose **Newest Tomcat 8.5** for the web container.</span></span> <span data-ttu-id="aa79d-147">(Esse contêiner não será realmente usado; o Azure usa o contêiner do aplicativo Spring Boot.)</span><span class="sxs-lookup"><span data-stu-id="aa79d-147">(This container will not actually be used; Azure will use the container from your Spring Boot application.)</span></span>

   <span data-ttu-id="aa79d-148">e.</span><span class="sxs-lookup"><span data-stu-id="aa79d-148">e.</span></span> <span data-ttu-id="aa79d-149">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="aa79d-149">Click **Save**.</span></span>

   ![Configurações do aplicativo][AZ07]

1. <span data-ttu-id="aa79d-151">Especifique suas credenciais de implantação de FTP usando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="aa79d-151">Specify your FTP deployment credentials by using the following steps:</span></span>

   <span data-ttu-id="aa79d-152">a.</span><span class="sxs-lookup"><span data-stu-id="aa79d-152">a.</span></span> <span data-ttu-id="aa79d-153">Clique no item de menu **Credenciais de Implantação**.</span><span class="sxs-lookup"><span data-stu-id="aa79d-153">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="aa79d-154">b.</span><span class="sxs-lookup"><span data-stu-id="aa79d-154">b.</span></span> <span data-ttu-id="aa79d-155">Especifique o nome de usuário e a senha.</span><span class="sxs-lookup"><span data-stu-id="aa79d-155">Specify your username and password.</span></span>

   <span data-ttu-id="aa79d-156">c.</span><span class="sxs-lookup"><span data-stu-id="aa79d-156">c.</span></span> <span data-ttu-id="aa79d-157">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="aa79d-157">Click **Save**.</span></span>

   ![Especificar Credenciais de Implantação][AZ08]

1. <span data-ttu-id="aa79d-159">Recupere as informações de conexão FTP usando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="aa79d-159">Retrieve your FTP connection information by using the following steps:</span></span>

   <span data-ttu-id="aa79d-160">a.</span><span class="sxs-lookup"><span data-stu-id="aa79d-160">a.</span></span> <span data-ttu-id="aa79d-161">Clique no item de menu **Credenciais de Implantação**.</span><span class="sxs-lookup"><span data-stu-id="aa79d-161">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="aa79d-162">b.</span><span class="sxs-lookup"><span data-stu-id="aa79d-162">b.</span></span> <span data-ttu-id="aa79d-163">Copie o nome de usuário de FTP completo e a URL e salve-os para a próxima seção deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="aa79d-163">Copy your full FTP username and URL and save them for the next section of this tutorial.</span></span>

   ![URL FTP e Credenciais][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a><span data-ttu-id="aa79d-165">Implantar o aplicativo Web Spring Boot no Azure</span><span class="sxs-lookup"><span data-stu-id="aa79d-165">Deploy your Spring Boot web app to Azure</span></span>

<span data-ttu-id="aa79d-166">As etapas a seguir explicarão as etapas para implantar o aplicativo Web Spring Boot no Azure.</span><span class="sxs-lookup"><span data-stu-id="aa79d-166">The following steps will walk you through the steps to deploy your Spring Boot web app to Azure.</span></span>

1. <span data-ttu-id="aa79d-167">Abra um editor de texto como o Bloco de Notas do Windows, cole o seguinte texto em um novo documento e salve o arquivo como *web.config*:</span><span class="sxs-lookup"><span data-stu-id="aa79d-167">Open a text editor such as Windows Notepad and paste the following text into a new document, then save the file as *web.config*:</span></span>
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

1. <span data-ttu-id="aa79d-168">Depois de salvar o arquivo *web.config* no sistema e conecte-se ao aplicativo Web por meio do FTP usando a URL, o nome de usuário e a senha da seção anterior deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="aa79d-168">After you have saved the *web.config* file to your system, connect to your web app via FTP using the URL, username, and password from the preceding section of this tutorial.</span></span> <span data-ttu-id="aa79d-169">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aa79d-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="aa79d-170">Altere o diretório remoto para a pasta raiz do aplicativo Web (em */site/wwwroot*), copie o arquivo JAR do aplicativo Spring Boot e o *web.config* anteriores.</span><span class="sxs-lookup"><span data-stu-id="aa79d-170">Change the remote directory to the root folder of your web app, (which is at */site/wwwroot*), then copy the JAR file from your Spring Boot application and the *web.config* from earlier.</span></span> <span data-ttu-id="aa79d-171">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aa79d-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="aa79d-172">Depois de implantar os arquivos JAR e *web.config* no aplicativo Web, você precisa reiniciar o aplicativo Web usando o Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="aa79d-172">After you have deployed your JAR and *web.config* files to your web app, you need to restart your web app using the Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="aa79d-173">Teste o aplicativo Web navegando até a URL do aplicativo Web com um navegador da Web ou use a sintaxe semelhante ao seguinte exemplo, se você tiver o curl disponível:</span><span class="sxs-lookup"><span data-stu-id="aa79d-173">Test the web app by browsing to your web app's URL using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="aa79d-174">Você verá a seguinte mensagem exibida: **Saudações do Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="aa79d-174">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Pesquisar aplicativo de exemplo][SB02]

## <a name="next-steps"></a><span data-ttu-id="aa79d-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aa79d-176">Next steps</span></span>

<span data-ttu-id="aa79d-177">Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="aa79d-177">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="aa79d-178">Implantar um aplicativo Spring Boot no Linux no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="aa79d-178">Deploy a Spring Boot Application on Linux in the Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="aa79d-179">Implantar um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="aa79d-179">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="aa79d-180">Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="aa79d-180">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="aa79d-181">Para obter informações adicionais sobre a implantação dos aplicativos Web no Azure usando o FTP, confira [Implantar o aplicativo no Serviço de Aplicativo do Azure usando FTP/S].</span><span class="sxs-lookup"><span data-stu-id="aa79d-181">For additional information about depoying web apps to Azure using FTP, see [Deploy your app to Azure App Service using FTP/S].</span></span>

<span data-ttu-id="aa79d-182">Para obter mais detalhes sobre o projeto de exemplo Spring Boot, confira [Spring Boot Getting Started].</span><span class="sxs-lookup"><span data-stu-id="aa79d-182">For further details about the Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="aa79d-183">Para obter ajuda na introdução a seus próprios aplicativos Spring Boot, confira **Spring Initializr** em https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="aa79d-183">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="aa79d-184">Para obter mais informações sobre como definir configurações adicionais para o aplicativo Web, confira [Configurar aplicativos Web no Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="aa79d-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

<span data-ttu-id="aa79d-185">[Serviço de Aplicativo do Azure]: https://azure.microsoft.com/services/app-service/</span><span class="sxs-lookup"><span data-stu-id="aa79d-185">[Azure App Service]: https://azure.microsoft.com/services/app-service/</span></span>
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
<span data-ttu-id="aa79d-186">[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="aa79d-186">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="aa79d-187">[Portal do Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="aa79d-187">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="aa79d-188">[Configurar aplicativos Web no Serviço de Aplicativo do Azure]: /azure/app-service-web/web-sites-configure</span><span class="sxs-lookup"><span data-stu-id="aa79d-188">[Configure web apps in Azure App Service]: /azure/app-service-web/web-sites-configure</span></span>
<span data-ttu-id="aa79d-189">[Implantar o aplicativo no Serviço de Aplicativo do Azure usando FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp</span><span class="sxs-lookup"><span data-stu-id="aa79d-189">[Deploy your app to Azure App Service using FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp</span></span>
<span data-ttu-id="aa79d-190">[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="aa79d-190">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="aa79d-191">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="aa79d-191">[Git]: https://github.com/</span></span>
<span data-ttu-id="aa79d-192">[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="aa79d-192">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="aa79d-193">[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="aa79d-193">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="aa79d-194">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="aa79d-194">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="aa79d-195">[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="aa79d-195">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="aa79d-196">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="aa79d-196">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="aa79d-197">[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot</span><span class="sxs-lookup"><span data-stu-id="aa79d-197">[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot</span></span>
<span data-ttu-id="aa79d-198">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="aa79d-198">[Spring Framework]: https://spring.io/</span></span>

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
