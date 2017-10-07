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
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-containerized-spring-boot-app-tooazure"></a>Como toouse hello Maven plug-in para aplicativos Web do Azure toodeploy um tooAzure de aplicativo de inicialização de Spring em contêineres

Olá [Maven plug-in para aplicativos Web do Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) para [Apache Maven](http://maven.apache.org/) fornece integração perfeita de serviço de aplicativo do Azure em projetos Maven e simplifica o processo de saudação para desenvolvedores toodeploy web aplicativos tooAzure do serviço de aplicativo.

Este artigo demonstra como usar Olá Maven plug-in para aplicativos Web do Azure toodeploy um aplicativo de inicialização de Spring de exemplo em um contêiner de Docker tooAzure serviços de aplicativos.

> [!NOTE]
>
> Olá Maven plug-in para aplicativos Web do Azure está disponível como uma visualização. Por enquanto, somente a publicação FTP tem suporte, embora recursos adicionais foram planejados para Olá futuras.
>

## <a name="prerequisites"></a>Pré-requisitos

Em ordem toocomplete Olá etapas deste tutorial, você precisa toohave Olá pré-requisitos a seguir:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].
* Olá [Azure Interface de linha de comando (CLI)].
* Um JDK (Java Development Kit) versão 1.7 ou posterior atualizado.
* A ferramenta de compilação [Maven] do Apache (Versão 3).
* Um cliente [Git].
* Um cliente do [Docker].

> [!NOTE]
>
> Devido a requisitos de virtualização toohello deste tutorial, você não conseguir seguir etapas Olá neste artigo em uma máquina virtual. Você deve usar um computador físico com recursos de virtualização habilitados.
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a>Exemplo de hello clone Spring inicialização no aplicativo web de Docker

Nesta seção, você clonará um aplicativo Spring Boot em contêineres e o testará localmente.

1. Abra um prompt de comando ou a janela do terminal e criar um diretório local toohold seu aplicativo de inicialização de Spring e altere o diretório toothat; Por exemplo:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- ou --
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Saudação de clone [inicialização Spring no guia de Introdução do Docker] projeto de exemplo no diretório Olá criado; por exemplo:
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. Alterar diretório toohello concluída projeto; Por exemplo:
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. Criar arquivo JAR de saudação usando Maven; Por exemplo:
   ```shell
   mvn clean package
   ```

1. Quando o aplicativo da web de saudação tiver sido criado, iniciar Olá web app usando Maven; Por exemplo:
   ```shell
   mvn spring-boot:run
   ```

1. Testar o aplicativo da web de saudação navegando tooit localmente usando um navegador da web. Por exemplo, você pode usar o hello comando a seguir se você tiver ondulação disponível:
   ```shell
   curl http://localhost:8080
   ```

1. Você deve ver Olá mensagem exibida a seguir: **Docker Olá, mundo**

## <a name="create-an-azure-service-principal"></a>Criar uma entidade de serviço do Azure

Nesta seção, você criará um Azure entidade de serviço que Olá usos de plug-in Maven durante a implantação de seu contêiner tooAzure.

1. Abra um prompt de comando.

1. Entre em sua conta do Azure usando Olá CLI do Azure:
   ```shell
   az login
   ```
   Siga Olá instruções toocomplete Olá processo de entrada.

1. Crie uma entidade de serviço do Azure:
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Onde `uuuuuuuu` é o nome de usuário hello e `pppppppp` é a senha Olá Olá entidade de serviço.

1. Azure responde com JSON que é semelhante a saudação de exemplo a seguir:
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
   > Você usará os valores de saudação dessa resposta JSON quando você configura Olá Maven plug-in toodeploy tooAzure seu contêiner. Olá `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, e `tttttttt` são valores de espaço reservado, que são usados em toomake Este exemplo-toomap mais fácil esses elementos de respectivos do tootheir valores quando você configura o Maven `settings.xml` arquivo hello lado seção.
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a>Configurar Maven toouse a entidade de serviço do Azure

Nesta seção, você pode usar valores de saudação da autenticação de saudação de tooconfigure principal de serviço do Azure Maven usará ao implantar seu contêiner tooAzure.

1. Abra o Maven `settings.xml` arquivo em um editor de texto; este arquivo pode estar em um caminho como Olá exemplos a seguir:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Adicionar suas configurações de serviço do Azure principal da seção anterior Olá este tutorial toohello `<servers>` coleção em Olá *settings.xml* arquivo; por exemplo:

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
   Em que:
   Elemento | Descrição
   ---|---|---
   `<id>` | Especifica um nome exclusivo que Maven usa toolook suas configurações de segurança quando você implanta seu tooAzure de aplicativo web.
   `<client>` | Contém Olá `appId` valor da sua entidade de serviço.
   `<tenant>` | Contém Olá `tenant` valor da sua entidade de serviço.
   `<key>` | Contém Olá `password` valor da sua entidade de serviço.
   `<environment>` | Define o ambiente de nuvem do Azure de destino hello, que é `AZURE` neste exemplo. (Uma lista completa dos ambientes está disponível no hello [Maven plug-in para aplicativos Web do Azure] documentação)

1. Salve e feche o hello *settings.xml* arquivo.

## <a name="optional-deploy-your-local-docker-file-toodocker-hub"></a>OPCIONAL: Implantar o seu local tooDocker de arquivo Docker Hub

Se você tiver uma conta do Docker, você pode criar seu Docker imagem de contêiner localmente e envie tooDocker Hub. Assim, o toodo usar Olá etapas a seguir.

1. Olá abrir `pom.xml` arquivo para seu aplicativo de inicialização de Spring em um editor de texto.

1. Localizar Olá `<imageName>` elemento filho do hello `<containerSettings>` elemento.

1. Saudação de atualização `${docker.image.prefix}` valor com o nome da sua conta de Docker:
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. Escolha uma saudação métodos de implantação a seguir:

   * Criar sua imagem de contêiner localmente com o Maven e então use Docker toopush tooDocker seu contêiner Hub:
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * Se você tiver Olá [Docker plug-in para Maven] instalado, você pode criar automaticamente e tooDocker sua imagem de contêiner Hub usando Olá `-DpushImage` parâmetro:
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-tooazure"></a>OPCIONAL: Personalizar sua pom.xml antes de implantar seu tooAzure de contêiner

Olá abrir `pom.xml` de arquivo para o seu aplicativo de inicialização de Spring em um editor de texto e localize Olá `<plugin>` elemento para `azure-webapp-maven-plugin`. Esse elemento deve ser semelhante a saudação de exemplo a seguir:

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

Há vários valores que você pode modificar para plug-in do hello Maven e uma descrição detalhada de cada um desses elementos está disponível no hello [Maven plug-in para aplicativos Web do Azure] documentação. Dito isso, vale a pena destacar diversos valores neste artigo:

Elemento | Descrição
---|---|---
`<version>` | Especifica a versão de saudação do hello [Maven plug-in para aplicativos Web do Azure]. Você deve verificar a versão Olá listado no hello [repositório Central Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) Olá tooensure que você está usando a versão mais recente.
`<authentication>` | Especifica as informações de autenticação de saudação do Azure, que neste exemplo contém um `<serverId>` elemento que contém `azure-auth`; Maven usa toolook esse valor valores principal de serviço do Azure Olá em seu Maven *settings.xml* arquivo, que você definiu em uma seção anterior deste artigo.
`<resourceGroup>` | Especifica o grupo de recursos de destino hello, que é `maven-plugin` neste exemplo. grupo de recursos de saudação será criado durante a implantação se ele ainda não existir.
`<appName>` | Especifica o nome do destino de saudação para seu aplicativo web. Neste exemplo, o nome de destino de saudação é `maven-linux-app-${maven.build.timestamp}`, onde hello `${maven.build.timestamp}` sufixo é acrescentado em conflito de tooavoid neste exemplo. (Olá timestamp é opcional; você pode especificar qualquer cadeia de caracteres exclusiva para o nome do aplicativo hello.)
`<region>` | Especifica a região de destino hello, que neste exemplo é `westus`. (Uma lista completa está em Olá [Maven plug-in para aplicativos Web do Azure] documentação.)
`<appSettings>` | Especifica qualquer configurações exclusivas para Maven toouse ao implantar seu tooAzure de aplicativo web. Neste exemplo, um `<property>` elemento contém um par de nome/valor de elementos filho que especifique a porta Olá para seu aplicativo.

> [!NOTE]
>
> número de porta de Olá Olá configurações toochange neste exemplo somente são necessárias quando você estiver alterando a porta de saudação do padrão de saudação.
>

## <a name="build-and-deploy-your-container-tooazure"></a>Criar e implantar seu tooAzure de contêiner

Depois de configurar todas as configurações de saudação em Olá anterior seções deste artigo, você está pronto toodeploy tooAzure seu contêiner. Assim, o toodo use Olá etapas a seguir:

1. No prompt de comando hello ou janela de terminal que você estava usando anteriormente, recriar o arquivo de JAR de hello usando Maven se você tiver feito qualquer toohello alterações *pom.xml* arquivo; por exemplo:
   ```shell
   mvn clean package
   ```

1. Implantar seu tooAzure de aplicativo web usando Maven; Por exemplo:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven implantará seu tooAzure de aplicativo da web; Se o aplicativo da web de saudação ainda não existir, ele será criado.

> [!NOTE]
>
> Se região Olá que você especifica no hello `<region>` elemento da sua *pom.xml* arquivo não tem servidores suficientes disponíveis quando você inicia a implantação, você poderá ver um toohello semelhante erro exemplo a seguir:
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
> Se isso acontecer, você pode especificar que outra região e execute novamente Olá Maven comando toodeploy seu aplicativo.
>
>

Quando sua web tiver sido implantada, você será capaz de toomanage usando Olá [portal do Azure].

* Seu aplicativo Web será listado nos **Serviços de Aplicativos**:

   ![Aplicativo Web listado nos Serviços de Aplicativos do portal do Azure][AP01]

* E Olá URL para seu aplicativo web será listado no hello **visão geral** para seu aplicativo web:

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

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá diversas tecnologias abordadas neste artigo, consulte Olá artigos a seguir:

* [Maven plug-in para aplicativos Web do Azure]

* [Faça logon no tooAzure de saudação CLI do Azure](/azure/xplat-cli-connect)

* [Como toouse hello Maven plug-in para aplicativos Web do Azure toodeploy um aplicativo de inicialização de Spring tooAzure do serviço de aplicativo](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [Criar uma entidade de serviço do Azure com a CLI 2.0 do Azure](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Referência de configurações do Maven](https://maven.apache.org/settings.html)

* [Docker plug-in para Maven]

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
