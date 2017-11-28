---
title: "aaaHow tooconfigure toouse de aplicativo um inicializador de inicialização Spring Cache Redis"
description: "Saiba como tooconfigure um aplicativo de inicialização de Spring criados com hello Spring Initializr toouse Cache Redis do Azure."
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: Spring, Spring Boot Starter, Cache Redis
ms.assetid: 
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: java
ms.topic: article
ms.date: 7/21/2017
ms.author: robmcm;zhijzhao;yidon
ms.openlocfilehash: ad532c88d2d67b97079eeb0e0e392add29ac365b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a><span data-ttu-id="efa82-104">Como tooconfigure um aplicativo de inicializador de inicialização Spring toouse Cache Redis</span><span class="sxs-lookup"><span data-stu-id="efa82-104">How tooconfigure a Spring Boot Initializer app toouse Redis Cache</span></span>

## <a name="overview"></a><span data-ttu-id="efa82-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="efa82-105">Overview</span></span>

<span data-ttu-id="efa82-106">Olá  **[Spring Framework]**  é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="efa82-106">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="efa82-107">Um dos projetos mais populares hello, que é criado em cima dessa plataforma é [Spring inicialização], que fornece um método simplificado para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="efa82-107">One of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="efa82-108">os desenvolvedores de toohelp começar com a inicialização de Spring, vários pacotes de inicialização de Spring de exemplo estão disponíveis em <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="efa82-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="efa82-109">Além disso toochoosing de lista de saudação de inicialização Spring básica projetos, hello  **[Spring Initializr]**  ajuda os desenvolvedores a começar a criar aplicativos personalizados de inicialização de Spring.</span><span class="sxs-lookup"><span data-stu-id="efa82-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="efa82-110">Este artigo orienta a criação de um cache Redis usando Olá portal do Azure, em seguida, usando Olá **Initializr Spring** toocreate um aplicativo personalizado e, em seguida, criando um Java web um aplicativo que armazena e recupera dados usando o Cache redis.</span><span class="sxs-lookup"><span data-stu-id="efa82-110">This article walks you through creating a Redis cache using hello Azure portal, then using hello **Spring Initializr** toocreate a custom application, and then creating a Java web application which stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efa82-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="efa82-111">Prerequisites</span></span>

<span data-ttu-id="efa82-112">Olá pré-requisitos a seguir é necessários na ordem toofollow Olá etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="efa82-112">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="efa82-113">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="efa82-113">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="efa82-114">Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="efa82-114">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="efa82-115">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="efa82-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="efa82-116">Criar um cache Redis no Azure</span><span class="sxs-lookup"><span data-stu-id="efa82-116">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="efa82-117">Procurar toohello Azure portal em <https://portal.azure.com/> e clique em item Olá para **+ novo**.</span><span class="sxs-lookup"><span data-stu-id="efa82-117">Browse toohello Azure portal at <https://portal.azure.com/> and click hello item for **+New**.</span></span>

   ![Portal do Azure][AZ01]

1. <span data-ttu-id="efa82-119">Clique em **Banco de Dados**e, em seguida, clique em **Cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="efa82-119">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Portal do Azure][AZ02]

1. <span data-ttu-id="efa82-121">Em Olá **novo Cache Redis** insira Olá **nome DNS** para seu cache, em seguida, especifique o **assinatura**, **grupo de recursos**,  **Local**, e **preço**.</span><span class="sxs-lookup"><span data-stu-id="efa82-121">On hello **New Redis Cache** page, enter hello **DNS name** for your cache, then specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span> <span data-ttu-id="efa82-122">Quando você especificar essas opções, clique em **criar** toocreate seu cache.</span><span class="sxs-lookup"><span data-stu-id="efa82-122">When you have specified these options, click **Create** toocreate your cache.</span></span>

   ![Portal do Azure][AZ03]

1. <span data-ttu-id="efa82-124">Depois que o cache foi concluído, você verá ele listado no seu Azure **painel**, bem como em Olá **todos os recursos**, e **Caches Redis** páginas.</span><span class="sxs-lookup"><span data-stu-id="efa82-124">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under hello **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="efa82-125">Você pode clicar em seu cache em qualquer um desses locais tooopen Olá da página de propriedades para seu cache.</span><span class="sxs-lookup"><span data-stu-id="efa82-125">You can click on your cache on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Portal do Azure][AZ04]

1. <span data-ttu-id="efa82-127">Quando a página de saudação que contém a lista de saudação de propriedades para o cache for exibida, clique em **chaves de acesso** e copie as chaves de acesso para seu cache.</span><span class="sxs-lookup"><span data-stu-id="efa82-127">When hello page which contains hello list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Portal do Azure][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a><span data-ttu-id="efa82-129">Criar um aplicativo personalizado usando Olá Initializr Spring</span><span class="sxs-lookup"><span data-stu-id="efa82-129">Create a custom application using hello Spring Initializr</span></span>

1. <span data-ttu-id="efa82-130">Procurar muito<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="efa82-130">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="efa82-131">Especifique que você deseja toogenerate um **Maven** projeto com **Java**, digite Olá **grupo** e **Aritifact** nomes para o seu aplicativo e, em seguida, clique em link Olá muito**versão completa do comutador toohello** de saudação Initializr Spring.</span><span class="sxs-lookup"><span data-stu-id="efa82-131">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Aritifact** names for your application, and then click hello link too**Switch toohello full version** of hello Spring Initializr.</span></span>

   ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="efa82-133">Olá Spring Initializr usará Olá **grupo** e **Aritifact** nome do pacote de saudação nomes toocreate; por exemplo: *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="efa82-133">hello Spring Initializr will use hello **Group** and **Aritifact** names toocreate hello package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="efa82-134">Role para baixo toohello **Web** seção e marque a caixa de saudação para **Web**, em seguida, role para baixo toohello **NoSQL** seção e marque a caixa de saudação para **Redis**, em seguida, role toohello inferior da página hello e clique botão Olá muito**projeto gerar**.</span><span class="sxs-lookup"><span data-stu-id="efa82-134">Scroll down toohello **Web** section and check hello box for **Web**, then scroll down toohello **NoSQL** section and check hello box for **Redis**, then scroll toohello bottom of hello page and click hello button too**Generate Project**.</span></span>

   ![Opções do Spring Initilializr Completo][SI02]

1. <span data-ttu-id="efa82-136">Quando solicitado, baixe o caminho de tooa Olá projeto em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="efa82-136">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Baixe o projeto personalizado do Spring Boot][SI03]

1. <span data-ttu-id="efa82-138">Depois de extrair arquivos Olá no sistema local, seu aplicativo de inicialização de Spring personalizado estará pronto para edição.</span><span class="sxs-lookup"><span data-stu-id="efa82-138">After you have extracted hello files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Arquivos de projeto Spring Boot personalizados][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a><span data-ttu-id="efa82-140">Configurar seu toouse Spring inicialização personalizada seu Cache Redis</span><span class="sxs-lookup"><span data-stu-id="efa82-140">Configure your custom Spring Boot toouse your Redis Cache</span></span>

1. <span data-ttu-id="efa82-141">Localizar Olá *application.properties* arquivo hello *recursos* diretório de seu aplicativo, ou criar arquivo hello se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="efa82-141">Locate hello *application.properties* file in hello *resources* directory of your app, or create hello file if it does not already exist.</span></span>

   ![Localize o arquivo de application.properties Olá][RE01]

1. <span data-ttu-id="efa82-143">Olá abrir *application.properties* do arquivo em um editor de texto, adicione Olá arquivo toohello de linhas a seguir e substitua os valores de exemplo hello propriedades adequadas de saudação do seu cache:</span><span class="sxs-lookup"><span data-stu-id="efa82-143">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties from your cache:</span></span>

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Editando o arquivo de application.properties Olá][RE02]

1. <span data-ttu-id="efa82-145">Salve e feche o hello *application.properties* arquivo.</span><span class="sxs-lookup"><span data-stu-id="efa82-145">Save and close hello *application.properties* file.</span></span>

1. <span data-ttu-id="efa82-146">Crie uma pasta chamada *controlador* sob a pasta de origem Olá para seu pacote; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="efa82-146">Create a folder named *controller* under hello source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="efa82-147">-ou-</span><span class="sxs-lookup"><span data-stu-id="efa82-147">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="efa82-148">Criar um novo arquivo denominado *HelloController.java* em Olá *controlador* pasta.</span><span class="sxs-lookup"><span data-stu-id="efa82-148">Create a new file named *HelloController.java* in hello *controller* folder.</span></span> <span data-ttu-id="efa82-149">Abra o arquivo hello em um editor de texto e adicione Olá tooit de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="efa82-149">Open hello file in a text editor and add hello following code tooit:</span></span>

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Value;
   import redis.clients.jedis.Jedis;
   import redis.clients.jedis.JedisShardInfo;

   @RestController
   public class HelloController {
   
      // Retrieve hello DNS name for your cache.
      @Value("${spring.redis.host}")
      private String redisHost;

      // Retrieve hello port for your cache.
      @Value("${spring.redis.port}")
      private int redisPort;

      // Retrieve hello access key for your cache.
      @Value("${spring.redis.password}")
      private String redisPassword;

      @RequestMapping("/")
      // Define hello Hello World controller.
      public String hello() {
      
         // Create a JedisShardInfo object tooconnect tooyour Redis cache.
         JedisShardInfo jedisShardInfo = new JedisShardInfo(redisHost, redisPort, true);
         // Specify your access key.
         jedisShardInfo.setPassword(redisPassword);
         // Create a Jedis object toostore/retrieve information from your cache.
         Jedis jedis = new Jedis(jedisShardInfo);

         // Add a Hello World string tooyour cache.
         jedis.set("greeting", "Hello World!");

         // Return hello string from your cache.
         return jedis.get("greeting");
      }
   }
   ```
   
   <span data-ttu-id="efa82-150">Onde você precisará tooreplace `com.contoso.myazuredemo` com o nome do pacote de saudação para seu projeto.</span><span class="sxs-lookup"><span data-stu-id="efa82-150">Where you will need tooreplace `com.contoso.myazuredemo` with hello package name for your project.</span></span>

1. <span data-ttu-id="efa82-151">Salve e feche o hello *HelloController.java* arquivo.</span><span class="sxs-lookup"><span data-stu-id="efa82-151">Save and close hello *HelloController.java* file.</span></span>

1. <span data-ttu-id="efa82-152">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="efa82-152">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="efa82-153">Testar o aplicativo web de saudação navegando toohttp://localhost:8080 usando um navegador da web, ou usar a sintaxe de saudação como Olá exemplo a seguir se você tiver ondulação disponível:</span><span class="sxs-lookup"><span data-stu-id="efa82-153">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="efa82-154">Você deve ver hello "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="efa82-154">You should see hello "Hello World!"</span></span> <span data-ttu-id="efa82-155">mensagem do seu controlador de exemplo exibido, que está sendo recuperado dinamicamente do seu cache Redis.</span><span class="sxs-lookup"><span data-stu-id="efa82-155">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efa82-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="efa82-156">Next steps</span></span>

<span data-ttu-id="efa82-157">Para obter mais informações sobre como usar aplicativos de inicialização Spring no Azure, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="efa82-157">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="efa82-158">Implantar um toohello Spring aplicativo de inicialização do serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="efa82-158">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="efa82-159">Executando um aplicativo de inicialização de Spring em um Cluster de Kubernetes hello Azure serviço de contêiner</span><span class="sxs-lookup"><span data-stu-id="efa82-159">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="efa82-160">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="efa82-160">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="efa82-161">Para obter mais informações sobre como obter iniciado usando o Cache Redis com Java no Azure, consulte [como toouse Cache Redis do Azure com Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="efa82-161">For more information about getting started using Redis Cache with Java on Azure, see [How toouse Azure Redis Cache with Java][Redis Cache with Java].</span></span>

<!-- URL List -->

[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[ferramentas Java para o Visual Studio Team Services]: https://java.visualstudio.com/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring inicialização]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Redis Cache with Java]: cache-java-get-started.md

<!-- IMG List -->

[AZ01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ01.png
[AZ02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ02.png
[AZ03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ03.png
[AZ04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ04.png
[AZ05]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ05.png

[SI01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI01.png
[SI02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI02.png
[SI03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI03.png
[SI04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI04.png

[RE01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE01.png
[RE02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE02.png
