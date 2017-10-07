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
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a>Como tooconfigure um aplicativo de inicializador de inicialização Spring toouse Cache Redis

## <a name="overview"></a>Visão geral

Olá  **[Spring Framework]**  é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial. Um dos projetos mais populares hello, que é criado em cima dessa plataforma é [Spring inicialização], que fornece um método simplificado para a criação de aplicativos Java autônomos. os desenvolvedores de toohelp começar com a inicialização de Spring, vários pacotes de inicialização de Spring de exemplo estão disponíveis em <https://github.com/spring-guides/>. Além disso toochoosing de lista de saudação de inicialização Spring básica projetos, hello  **[Spring Initializr]**  ajuda os desenvolvedores a começar a criar aplicativos personalizados de inicialização de Spring.

Este artigo orienta a criação de um cache Redis usando Olá portal do Azure, em seguida, usando Olá **Initializr Spring** toocreate um aplicativo personalizado e, em seguida, criando um Java web um aplicativo que armazena e recupera dados usando o Cache redis.

## <a name="prerequisites"></a>Pré-requisitos

Olá pré-requisitos a seguir é necessários na ordem toofollow Olá etapas neste artigo:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].

* Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versão 1.7 ou posterior.

* [Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.

## <a name="create-a-redis-cache-on-azure"></a>Criar um cache Redis no Azure

1. Procurar toohello Azure portal em <https://portal.azure.com/> e clique em item Olá para **+ novo**.

   ![Portal do Azure][AZ01]

1. Clique em **Banco de Dados**e, em seguida, clique em **Cache Redis**.

   ![Portal do Azure][AZ02]

1. Em Olá **novo Cache Redis** insira Olá **nome DNS** para seu cache, em seguida, especifique o **assinatura**, **grupo de recursos**,  **Local**, e **preço**. Quando você especificar essas opções, clique em **criar** toocreate seu cache.

   ![Portal do Azure][AZ03]

1. Depois que o cache foi concluído, você verá ele listado no seu Azure **painel**, bem como em Olá **todos os recursos**, e **Caches Redis** páginas. Você pode clicar em seu cache em qualquer um desses locais tooopen Olá da página de propriedades para seu cache.

   ![Portal do Azure][AZ04]

1. Quando a página de saudação que contém a lista de saudação de propriedades para o cache for exibida, clique em **chaves de acesso** e copie as chaves de acesso para seu cache.

   ![Portal do Azure][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a>Criar um aplicativo personalizado usando Olá Initializr Spring

1. Procurar muito<https://start.spring.io/>.

1. Especifique que você deseja toogenerate um **Maven** projeto com **Java**, digite Olá **grupo** e **Aritifact** nomes para o seu aplicativo e, em seguida, clique em link Olá muito**versão completa do comutador toohello** de saudação Initializr Spring.

   ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > Olá Spring Initializr usará Olá **grupo** e **Aritifact** nome do pacote de saudação nomes toocreate; por exemplo: *com.contoso.myazuredemo*.
   >

1. Role para baixo toohello **Web** seção e marque a caixa de saudação para **Web**, em seguida, role para baixo toohello **NoSQL** seção e marque a caixa de saudação para **Redis**, em seguida, role toohello inferior da página hello e clique botão Olá muito**projeto gerar**.

   ![Opções do Spring Initilializr Completo][SI02]

1. Quando solicitado, baixe o caminho de tooa Olá projeto em seu computador local.

   ![Baixe o projeto personalizado do Spring Boot][SI03]

1. Depois de extrair arquivos Olá no sistema local, seu aplicativo de inicialização de Spring personalizado estará pronto para edição.

   ![Arquivos de projeto Spring Boot personalizados][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a>Configurar seu toouse Spring inicialização personalizada seu Cache Redis

1. Localizar Olá *application.properties* arquivo hello *recursos* diretório de seu aplicativo, ou criar arquivo hello se ele ainda não existir.

   ![Localize o arquivo de application.properties Olá][RE01]

1. Olá abrir *application.properties* do arquivo em um editor de texto, adicione Olá arquivo toohello de linhas a seguir e substitua os valores de exemplo hello propriedades adequadas de saudação do seu cache:

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Editando o arquivo de application.properties Olá][RE02]

1. Salve e feche o hello *application.properties* arquivo.

1. Crie uma pasta chamada *controlador* sob a pasta de origem Olá para seu pacote; por exemplo:

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   -ou-

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. Criar um novo arquivo denominado *HelloController.java* em Olá *controlador* pasta. Abra o arquivo hello em um editor de texto e adicione Olá tooit de código a seguir:

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
   
   Onde você precisará tooreplace `com.contoso.myazuredemo` com o nome do pacote de saudação para seu projeto.

1. Salve e feche o hello *HelloController.java* arquivo.

1. Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Testar o aplicativo web de saudação navegando toohttp://localhost:8080 usando um navegador da web, ou usar a sintaxe de saudação como Olá exemplo a seguir se você tiver ondulação disponível:

   ```shell
   curl http://localhost:8080
   ```

   Você deve ver hello "Hello World!" mensagem do seu controlador de exemplo exibido, que está sendo recuperado dinamicamente do seu cache Redis.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar aplicativos de inicialização Spring no Azure, consulte Olá artigos a seguir:

* [Implantar um toohello Spring aplicativo de inicialização do serviço de aplicativo do Azure](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Executando um aplicativo de inicialização de Spring em um Cluster de Kubernetes hello Azure serviço de contêiner](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].

Para obter mais informações sobre como obter iniciado usando o Cache Redis com Java no Azure, consulte [como toouse Cache Redis do Azure com Java][Redis Cache with Java].

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
