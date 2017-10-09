---
title: "aaaHow toouse Olá Maven plug-in para aplicativos Web do Azure toodeploy um aplicativo de inicialização Spring no registro de contêiner do Azure tooAzure do serviço de aplicativo"
description: "Este tutorial irá orientá-lo embora Olá etapas toodeploy um aplicativo de inicialização de Spring no registro de contêiner do Azure tooAzure tooAzure do serviço de aplicativo usando um plug-in Maven."
services: 
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
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a>Como toouse hello Maven plug-in para aplicativos Web do Azure toodeploy um aplicativo de inicialização Spring no registro de contêiner do Azure tooAzure do serviço de aplicativo

Olá  **[Spring Framework]**  é uma estrutura de código-fonte aberto popular que ajuda os desenvolvedores Java criar web, móveis e aplicativos de API. Este tutorial usa um aplicativo de exemplo criado usando [Spring inicialização], uma abordagem orientada a convenção para usar Spring tooget iniciado rapidamente.

Este artigo demonstra como toodeploy tooAzure de aplicativo de inicialização Spring um exemplo do registro do contêiner e, em seguida, use hello Maven plug-in para aplicativos Web do Azure toodeploy tooAzure seu aplicativo do serviço de aplicativo.

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
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
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

   ![Procurar aplicativo de exemplo localmente][SB01]

## <a name="create-an-azure-service-principal"></a>Criar uma entidade de serviço do Azure

Nesta seção, você criará um Azure entidade de serviço que Olá usos de plug-in Maven durante a implantação de seu contêiner tooAzure.

1. Abra um prompt de comando.

1. Entre em sua conta do Azure usando Olá CLI do Azure:
   ```azurecli
   az login
   ```
   Siga Olá instruções toocomplete Olá processo de entrada.

1. Crie uma entidade de serviço do Azure:
   ```azurecli
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

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Criar um registro de contêiner do Azure usando Olá CLI do Azure

1. Abra um prompt de comando.

1. Faça logon no tooyour conta do Azure:
   ```azurecli
   az login
   ```

1. Crie um grupo de recursos de saudação recursos do Azure, que você usará neste artigo:
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   Substitua `wingtiptoysresources` neste exemplo por um nome exclusivo para o grupo de recursos.

1. Crie um registro de contêiner do Azure privada no grupo de recursos de saudação para seu aplicativo de inicialização de Spring: 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   Substitua `wingtiptoysregistry` neste exemplo por um nome exclusivo para seu registro de contêiner.

1. Recupere a senha de saudação para o registro de contêiner:
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   O Azure responderá com sua senha; por exemplo:
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a>Adicione seu registro de contêiner do Azure e configurações do serviço do Azure tooyour principal Maven

1. Abra o Maven `settings.xml` arquivo em um editor de texto; este arquivo pode estar em um caminho como Olá exemplos a seguir:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Adicionar as configurações de acesso de registro de contêiner do Azure da seção anterior Olá este artigo toohello `<servers>` coleção em Olá *settings.xml* arquivo; por exemplo:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   Em que:
   Elemento | Descrição
   ---|---|---
   `<id>` | Contém o nome de saudação do registro do contêiner do Azure privado.
   `<username>` | Contém o nome de saudação do registro do contêiner do Azure privado.
   `<password>` | Contém a senha de saudação recuperada na seção anterior Olá deste artigo.

1. Adicionar as configurações de serviço do Azure principal de uma seção anterior de toohello este artigo `<servers>` coleção em Olá *settings.xml* arquivo; por exemplo:

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

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a>Criar imagem de contêiner de seu Docker e enviar por push-tooyour registro de contêiner do Azure

1. Navegue de diretório do projeto toohello concluída para o seu aplicativo de inicialização de Spring (por exemplo "*C:\SpringBoot\gs-spring-boot-docker\complete*"ou"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") e abra hello *pom.xml* arquivo com um editor de texto.

1. Saudação de atualização `<properties>` coleção em Olá *pom.xml* arquivo com valor de servidor de logon Olá para o registro de contêiner do Azure na seção anterior de saudação deste tutorial; por exemplo:

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   Em que:
   Elemento | Descrição
   ---|---|---
   `<azure.containerRegistry>` | Especifica o nome de saudação do registro do contêiner do Azure privado.
   `<docker.image.prefix>` | Especifica a URL de saudação do registro do contêiner do Azure privada, que é derivado acrescentando ". azurecr.io" toohello nome do registro do contêiner privado.

1. Verifique `<plugin>` Olá plug-in de Docker em seu *pom.xml* arquivo contém propriedades correto Olá Olá servidor endereço e o registro do nome de logon da etapa anterior Olá neste tutorial. Por exemplo:

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   Em que:
   Elemento | Descrição
   ---|---|---
   `<serverId>` | Especifica a propriedade Olá que contém o nome do registro do contêiner do Azure privado.
   `<registryUrl>` | Especifica a propriedade Olá que contém a URL de saudação do registro do contêiner do Azure privado.

1. Navegue toohello concluída diretório do projeto para o aplicativo de inicialização de Spring e executar Olá após o aplicativo do comando toorebuild hello e enviar por push Olá contêiner tooyour registro de contêiner do Azure:

   ```
   mvn package docker:build -DpushImage 
   ```

1. OPCIONAL: Procurar toohello [portal do Azure] e verifique se não há imagem de contêiner do Docker chamada **gs spring-inicialização docker** no registro do contêiner.

   ![Verificar o contêiner no Portal do Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a>Personalizar sua pom.xml, em seguida, compilar e implantar seu contêiner tooAzure

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
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
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
`<resourceGroup>` | Especifica o grupo de recursos de destino hello, que é `wingtiptoysresources` neste exemplo. grupo de recursos de saudação será criado durante a implantação se ele ainda não existir.
`<appName>` | Especifica o nome do destino de saudação para seu aplicativo web. Neste exemplo, o nome de destino de saudação é `maven-linux-app-${maven.build.timestamp}`, onde hello `${maven.build.timestamp}` sufixo é acrescentado em conflito de tooavoid neste exemplo. (Olá timestamp é opcional; você pode especificar qualquer cadeia de caracteres exclusiva para o nome do aplicativo hello.)
`<region>` | Especifica a região de destino hello, que neste exemplo é `westus`. (Uma lista completa está em Olá [Maven plug-in para aplicativos Web do Azure] documentação.)
`<containerSettings>` | Especifica as propriedades de saudação que contêm o nome de saudação e a URL do seu contêiner.
`<appSettings>` | Especifica qualquer configurações exclusivas para Maven toouse ao implantar seu tooAzure de aplicativo web. Neste exemplo, um `<property>` elemento contém um par de nome/valor de elementos filho que especifique a porta Olá para seu aplicativo.

> [!NOTE]
>
> número de porta de Olá Olá configurações toochange neste exemplo somente são necessárias quando você estiver alterando a porta de saudação do padrão de saudação.
>

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

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá diversas tecnologias abordadas neste artigo, consulte Olá artigos a seguir:

* [Maven plug-in para aplicativos Web do Azure]

* [Faça logon no tooAzure de saudação CLI do Azure](/azure/xplat-cli-connect)

* [Criar uma entidade de serviço do Azure com a CLI 2.0 do Azure](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Referência de configurações do Maven](https://maven.apache.org/settings.html)

* [Plug-in do Docker para o Maven]

<!-- URL List -->

[Azure Interface de linha de comando (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portal do Azure]: https://portal.azure.com/
[Maven plug-in para aplicativos Web do Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Plug-in do Docker para o Maven]: https://github.com/spotify/docker-maven-plugin
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring inicialização]: http://projects.spring.io/spring-boot/
[inicialização Spring no guia de Introdução do Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
