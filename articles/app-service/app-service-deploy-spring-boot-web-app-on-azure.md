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
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a>Implantar um toohello Spring aplicativo de inicialização do serviço de aplicativo do Azure

Olá  **[Spring Framework]**  é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial e um dos projetos mais populares hello, que é criada sobre essa plataforma é [Spring inicialização], que fornece um método simplificado para a criação de aplicativos Java autônomos.

Este tutorial irá orientá-lo a criar embora Spring inicialização Introdução aplicativo de web de exemplo hello e implantá-lo muito[do serviço de aplicativo do Azure].

### <a name="prerequisites"></a>Pré-requisitos

Em ordem toocomplete Olá etapas deste tutorial, você precisa fazer toohave Olá seguinte:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].
* Um [JDK (Java Developer Kit)] atualizado.
* A ferramenta de compilação [Maven] do Apache (Versão 3).
* Um cliente [Git].

## <a name="create-hello-spring-boot-getting-started-web-app"></a>Criar aplicativo web e guia de Introdução do Spring inicialização Olá

Olá etapas a seguir orientará você pelas etapas de saudação toocreate necessário um aplicativo de web Spring inicialização simples e testá-lo localmente.

1. Abra um prompt de comando e criar um diretório local toohold seu aplicativo e altere o diretório toothat; Por exemplo:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- ou --
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Saudação de clone [Spring inicialização Introdução] projeto de exemplo no diretório Olá recém-criada; por exemplo:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. Alterar diretório toohello concluída projeto; Por exemplo:
   ```
   cd gs-spring-boot
   cd complete
   ```

1. Criar arquivo JAR de saudação usando Maven; Por exemplo:
   ```
   mvn package
   ```

1. Quando Olá web aplicativo tiver sido criado, alterar diretório toohello JAR arquivo e iniciar o aplicativo da web de saudação; Por exemplo:
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. Testar o aplicativo web de saudação navegando toohttp://localhost:8080 usando um navegador da web, ou usar a sintaxe de saudação como Olá exemplo a seguir se você tiver ondulação disponível:
   ```
   curl http://localhost:8080
   ```

1. Você deve ver Olá mensagem exibida a seguir: **saudações de inicialização Spring!**

   ![Pesquisar aplicativo de exemplo][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a>Criar um aplicativo Web do Azure para uso com Java

Olá etapas a seguir orientará Olá etapas toocreate um aplicativo Web do Azure, Olá necessário configurar para Java e configurar suas credenciais FTP.

1. Procurar toohello [portal do Azure] e faça logon.

1. Depois de fazer logon na sua conta em Olá portal do Azure, clique o ícone do menu de saudação para **serviços de aplicativos**:
   
   ![Portal do Azure][AZ01]

1. Olá quando **serviços de aplicativos** página é exibida, clique em **+ adicionar** toocreate um novo serviço de aplicativo.

   ![Criar Serviço de Aplicativo][AZ02]

1. Quando Olá lista de modelos de aplicativo da web é exibida, clique em link Olá Olá básica aplicativo Web do Microsoft.

   ![Modelos de aplicativo Web][AZ03]

1. Quando a página de informações de Olá para o modelo de aplicativo Web hello for exibida, clique em **criar**.

   ![Criar um aplicativo Web][AZ04]

1. Forneça um nome exclusivo para o aplicativo Web, especifique configurações adicionais e **Criar**.

   ![Criar Configurações de Aplicativo Web][AZ05]

1. Quando seu aplicativo web tiver sido criado, clique em ícone do menu Olá para **serviços de aplicativos**e, em seguida, clique em seu aplicativo web criado recentemente:

   ![Listar Aplicativos Web][AZ06]

1. Quando seu aplicativo web é exibido, especifique a versão do Java Olá usando Olá etapas a seguir:

   a. Clique em Olá **configurações de aplicativo** item de menu.

   b. Escolha **Java 8** para a versão do Java hello.

   c. Escolha **Newest** para a versão secundária do Java de saudação.

   d. Escolha **8.5 mais recente do Tomcat** para o contêiner da web de saudação. (Esse contêiner não será realmente usado; Azure usará o contêiner de saudação do seu aplicativo de inicialização de Spring.)

   e. Clique em **Salvar**.

   ![Configurações do aplicativo][AZ07]

1. Especifique suas credenciais de implantação de FTP usando Olá etapas a seguir:

   a. Clique em Olá **credenciais de implantação** item de menu.

   b. Especifique o nome de usuário e a senha.

   c. Clique em **Salvar**.

   ![Especificar Credenciais de Implantação][AZ08]

1. Recupere as informações de conexão de FTP usando Olá etapas a seguir:

   a. Clique em Olá **credenciais de implantação** item de menu.

   b. Copie o seu nome de usuário FTP completo e a URL e salvá-las para a próxima seção Olá deste tutorial.

   ![URL FTP e Credenciais][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a>Implantar seu tooAzure de aplicativo web inicialização Spring

Olá, as etapas a seguir explicará Olá etapas toodeploy seu tooAzure de aplicativo web Spring inicialização.

1. Abra um editor de texto como o bloco de notas do Windows e cole Olá texto a seguir em um novo documento e salve o arquivo hello como *Web. config*:
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

1. Depois que você salvou Olá *Web. config* tooyour sistema de arquivos, conecte-se o aplicativo da web de tooyour por meio de FTP usando Olá URL, nome de usuário e senha da saudação anterior seção deste tutorial. Por exemplo:
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. Pasta de raiz de toohello alteração Olá diretório remoto do seu aplicativo web, (que está no */site/wwwroot*) e copie o arquivo JAR de saudação do seu aplicativo de inicialização de Spring e Olá *Web. config* anteriores. Por exemplo:
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. Depois que você implantou seu JAR e *Web. config* arquivos tooyour web app, você precisa toorestart seu aplicativo web usando Olá portal do Azure:

   ![][AZ10]

1. Testar o aplicativo de web de saudação navegando URL do aplicativo da web tooyour usando um navegador da web, ou usar a sintaxe de saudação como Olá exemplo a seguir se você tiver ondulação disponível:
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. Você deve ver Olá mensagem exibida a seguir: **saudações de inicialização Spring!**

   ![Pesquisar aplicativo de exemplo][SB02]

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar aplicativos de inicialização Spring no Azure, consulte Olá artigos a seguir:

* [Implantar um aplicativo de inicialização Spring em Linux em hello Azure serviço de contêiner](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [Implantar um aplicativo de inicialização Spring em um Cluster de Kubernetes no hello Azure serviço de contêiner](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].

Para obter informações adicionais sobre depoying tooAzure de aplicativos de web usando FTP, consulte [implantar tooAzure seu aplicativo do serviço de aplicativo usando o FTP/S].

Para obter mais detalhes sobre o projeto de exemplo hello Spring inicialização, consulte [Spring inicialização Introdução].

Para obter ajuda com a guia de Introdução com seus próprios aplicativos de inicialização Spring, consulte Olá **Initializr Spring** em https://start.spring.io/.

Para obter mais informações sobre como definir configurações adicionais para o aplicativo Web, confira [Configurar aplicativos Web no Serviço de Aplicativo do Azure].

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
