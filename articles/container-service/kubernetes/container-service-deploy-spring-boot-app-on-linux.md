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
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a>Implantar um aplicativo de inicialização Spring em Linux em hello Azure serviço de contêiner

Olá  **[Spring Framework]**  é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial. Um dos projetos mais populares de saudação que é criado em cima dessa plataforma é [Spring inicialização], que fornece um método simplificado para a criação de aplicativos Java autônomos.

**[Docker]**  é soluções de código-fonte aberto que ajuda os desenvolvedores a automatizar a implantação hello, escala e gerenciamento de seus aplicativos que são executados em contêineres.

Este tutorial orienta você pelo usando Docker toodevelop e implantar um host Spring inicialização aplicativo tooa Linux Olá [serviço de contêiner do Azure (ACS)].

## <a name="prerequisites"></a>Pré-requisitos

Em ordem toocomplete Olá etapas deste tutorial, você precisa toohave Olá pré-requisitos a seguir:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].
* Olá [Azure Interface de linha de comando (CLI)].
* Um [JDK (Java Developer Kit)] atualizado.
* A ferramenta de compilação [Maven] do Apache (Versão 3).
* Um cliente [Git].
* Um cliente do [Docker].

> [!NOTE]
>
> Devido a requisitos de virtualização toohello deste tutorial, você não conseguir seguir etapas Olá neste artigo em uma máquina virtual. Você deve usar um computador físico com recursos de virtualização habilitados.
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a>Criar hello Spring inicialização no aplicativo web do guia de Introdução do Docker

Olá etapas a seguir mostram Olá etapas que são necessária toocreate um aplicativo simples da web Spring inicialização e testá-lo localmente.

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

1. Saudação de clone [inicialização Spring no guia de Introdução do Docker] projeto de exemplo no diretório Olá criado; por exemplo:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Alterar diretório toohello concluída projeto; Por exemplo:
   ```
   cd gs-spring-boot-docker/complete
   ```

1. Criar arquivo JAR de saudação usando Maven; Por exemplo:
   ```
   mvn package
   ```

1. Quando Olá web aplicativo tiver sido criado, alterar diretório toohello `target` diretório onde o arquivo JAR do hello está localizado e iniciar o aplicativo da web de saudação; por exemplo:
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. Testar o aplicativo da web de saudação navegando tooit localmente usando um navegador da web. Por exemplo, se você tiver ondulação disponível e configurado Olá Tomcat server toorun na porta 80:
   ```
   curl http://localhost
   ```

1. Você deve ver Olá mensagem exibida a seguir: **Docker Olá, mundo!**

   ![Procurar aplicativo de exemplo localmente][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a>Criar um registro de contêiner do Azure toouse como um registro de Docker privada

Olá etapas a seguir orientam você durante usando Olá toocreate portal do Azure um registro de contêiner do Azure.

> [!NOTE]
>
> Se você quiser toouse Olá CLI do Azure em vez da saudação portal do Azure, siga as etapas de saudação em [criar um registro de contêiner do Docker privado usando hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).
>

1. Procurar toohello [portal do Azure] e entrar.

   Depois de ter entrado na conta de tooyour no hello portal do Azure, você pode seguir etapas Olá Olá [criar um registro de contêiner do Docker privado usando o portal do Azure de saudação] artigo, que são traduzido em Olá seguindo as etapas para Olá bem de eficiência.

1. Clique ícone menu Olá **+ novo**, em seguida, clique em **contêineres**e, em seguida, clique em **registro de contêiner do Azure**.
   
   ![Criar um novo Registro de Contêiner do Azure][AR01]

1. Quando a página de informações de Olá para o modelo de registro de contêiner do Azure Olá for exibida, clique em **criar**. 

   ![Criar um novo Registro de Contêiner do Azure][AR02]

1. Olá quando **criar registro de contêiner** página é exibida, insira seu **nome do registro** e **grupo de recursos**, escolha **habilitar** para Olá **usuário administrador**e, em seguida, clique em **criar**.

   ![Definir configurações do registro de contêiner do Azure][AR03]

1. Quando o registro de contêiner tiver sido criado, navegar o registro de contêiner tooyour no hello portal do Azure e, em seguida, clique em **chaves de acesso**. Anote Olá nome de usuário e senha para as próximas etapas hello.

   ![Chaves de acesso do Registro de Contêiner do Azure][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a>Configurar Maven toouse suas chaves de acesso de registro de contêiner do Azure

1. Navegue toohello diretório de configuração para sua instalação Maven e abra Olá *settings.xml* arquivo com um editor de texto.

1. Adicionar as configurações de acesso de registro de contêiner do Azure da seção anterior Olá este tutorial toohello `<servers>` coleção em Olá *settings.xml* arquivo; por exemplo:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Navegue toohello concluída diretório do projeto para o seu aplicativo de inicialização de Spring (por exemplo: "*C:\SpringBoot\gs-spring-boot-docker\complete*"ou"*/users/robert/SpringBoot/gs-spring-boot-docker / concluída*") e abra hello *pom.xml* arquivo com um editor de texto.

1. Saudação de atualização `<properties>` coleção em Olá *pom.xml* arquivo com valor de servidor de logon Olá para o registro de contêiner do Azure na seção anterior de saudação deste tutorial; por exemplo:

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Saudação de atualização `<plugins>` coleção em Olá *pom.xml* arquivo de forma que Olá `<plugin>` contém Olá logon endereço e o registro do nome do servidor para o registro de contêiner do Azure na seção anterior de saudação deste tutorial. Por exemplo:

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

1. Navegue toohello concluída diretório do projeto para o aplicativo de inicialização de Spring e executar Olá após o aplicativo do comando toorebuild hello e enviar por push Olá contêiner tooyour registro de contêiner do Azure:

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> Quando são enviar seu tooAzure de contêiner do Docker, você receberá uma mensagem de erro é semelhante tooone de saudação seguindo o mesmo que seu contêiner de Docker foi criado com êxito:
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Se isso acontecer, talvez seja necessário toosign em tooyour conta do Azure da linha de comando do Docker Olá; Por exemplo:
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Você pode enviar seu contêiner de linha de comando Olá; Por exemplo:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>Criar um aplicativo Web no Linux no Serviço de Aplicativo do Azure usando a imagem de contêiner

1. Procurar toohello [portal do Azure] e entrar.

1. Clique ícone menu Olá **+ novo**, em seguida, clique em **Web + móvel**e, em seguida, clique em **Web App no Linux**.
   
   ![Criar um novo aplicativo web no hello portal do Azure][LX01]

1. Olá quando **Web App no Linux** página é exibida, digite Olá informações a seguir:

   a. Insira um nome exclusivo para Olá **nome do aplicativo**; por exemplo: "*wingtiptoyslinux*."

   b. Escolha seu **assinatura** da lista suspensa de saudação.

   c. Escolher um existente **grupo de recursos**, ou especifique um nome toocreate um novo grupo de recursos.

   d. Clique em **configurar contêiner** e digite Olá informações a seguir:

      * Escolha **Registro particular**.

      * **Marca de imagem e opcional**: especifique o nome do contêiner de antes. Por exemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"

      * **URL do servidor**: especifique a URL de registro de antes; por exemplo: "*https://wingtiptoysregistry.azurecr.io*"

      * **Nome de usuário de logon** e **Senha**: especifique suas credenciais de logon das **Chaves de Acesso** usadas nas etapas anteriores.
   
   e. Depois que você inseriu todos Olá acima informações, clique em **Okey**.

   ![Definir configurações do aplicativo Web][LX02]

1. Clique em **Criar**.

> [!NOTE]
>
> O Azure mapeará automaticamente solicitações tooembedded Tomcat servidor da Internet que está em execução em portas de saudação padrão de 80 ou 8080. No entanto, se você configurou seu toorun de servidor Tomcat inserido em uma porta personalizada, você precisa tooadd um aplicativo web tooyour variável de ambiente que define a porta de saudação para seu servidor Tomcat inserido. Assim, o toodo use Olá etapas a seguir:
>
> 1. Procurar toohello [portal do Azure] e entrar.
> 
> 2. Clique ícone Olá **serviços de aplicativos**. (Consulte o item #1 na imagem de saudação abaixo).
>
> 3. Selecione o aplicativo web na lista de saudação. (Item &#2; na imagem de saudação abaixo).
>
> 4. Clique em **Configurações do Aplicativo**. (Item #3 na imagem de saudação abaixo).
>
> 5. Em Olá **configurações do aplicativo** seção, adicione uma nova variável de ambiente denominada **porta** e insira seu número de porta personalizada para o valor de saudação. (Item #4 na imagem de saudação abaixo).
>
> 6. Clique em **Salvar**. (Item #5 na imagem de saudação abaixo).
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

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar aplicativos de inicialização Spring no Azure, consulte Olá artigos a seguir:

* [Implantar um toohello Spring aplicativo de inicialização do serviço de aplicativo do Azure](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Implantar um aplicativo de inicialização Spring em um Cluster de Kubernetes no hello Azure serviço de contêiner](container-service-deploy-spring-boot-app-on-kubernetes.md)

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].

Para obter mais detalhes sobre Olá Spring inicialização no projeto de exemplo do Docker, consulte [inicialização Spring no guia de Introdução do Docker].

Para obter ajuda com a guia de Introdução com seus próprios aplicativos de inicialização Spring, consulte Olá **Initializr Spring** em https://start.spring.io/.

Para obter mais informações sobre como começar com a criação de um aplicativo de inicialização de Spring simples, consulte Olá Spring Initializr em https://start.spring.io/.

Para obter exemplos adicionais para como toouse Docker personalizado imagens com o Azure, consulte [usando uma imagem personalizada do Docker para o aplicativo Web do Azure no Linux].

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
