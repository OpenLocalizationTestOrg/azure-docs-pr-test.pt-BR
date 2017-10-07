---
title: "aaaDeploy um aplicativo de inicialização Spring em Kubernetes no serviço de contêiner do Azure | Microsoft Docs"
description: "Este tutorial irá orientá-lo embora Olá etapas toodeploy um aplicativo de inicialização de Spring em um cluster Kubernetes no Microsoft Azure."
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
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a>Implantar um aplicativo de inicialização Spring em um Cluster de Kubernetes no hello Azure serviço de contêiner

Olá  **[Spring Framework]**  é uma estrutura de código-fonte aberto popular que ajuda os desenvolvedores Java criar web, móveis e aplicativos de API. Este tutorial usa um aplicativo de exemplo criado usando [Spring inicialização], uma abordagem orientada a convenção para usar Spring tooget iniciado rapidamente.

**[Kubernetes]**  e  **[Docker]**  são soluções de código-fonte aberto que ajudam os desenvolvedores automatizar a implantação de hello, escala e gerenciamento de seus aplicativos em execução em contêineres.

Este tutorial orienta você embora combinar essas duas tecnologias populares, código-fonte aberto toodevelop e implantar um aplicativo de inicialização de Spring tooMicrosoft do Azure. Mais especificamente, você usa  *[Spring inicialização]*  para desenvolvimento de aplicativos,  *[Kubernetes]*  para implantação do contêiner e hello [Serviço de contêiner do azure (ACS)] toohost seu aplicativo.

### <a name="prerequisites"></a>Pré-requisitos

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

Olá etapas a seguir orientam você durante a criação de um aplicativo da web de inicialização Spring e testá-lo localmente.

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

1. Saudação de clone [inicialização Spring no guia de Introdução do Docker] projeto de exemplo no diretório de saudação.
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Alterar o projeto do diretório toohello concluída.
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. Use toobuild Maven e o aplicativo de exemplo hello execução.
   ```
   mvn package spring-boot:run
   ```

1. Teste Olá web aplicativo navegando toohttp://localhost:8080 ou com os seguintes Olá `curl` comando:
   ```
   curl http://localhost:8080
   ```

1. Você deve ver Olá mensagem exibida a seguir: **Docker Olá, mundo**

   ![Procurar aplicativo de exemplo localmente][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Criar um registro de contêiner do Azure usando Olá CLI do Azure

1. Abra um prompt de comando.

1. Faça logon no tooyour conta do Azure:
   ```azurecli
   az login
   ```

1. Crie um grupo de recursos para Olá recursos do Azure usados neste tutorial.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Crie um registro de contêiner do Azure privada no grupo de recursos de saudação. tutorial de saudação envia o aplicativo de exemplo hello como um registro de toothis de imagem do Docker em etapas posteriores. Substitua `wingtiptoysregistry` por um nome exclusivo para o registro.
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a>Enviar por push o seu registro de contêiner do aplicativo toohello

1. Navegue toohello diretório de configuração para sua instalação Maven (~/.m2/ padrão ou C:\Users\username\.m2) e abra hello *settings.xml* arquivo com um editor de texto.

1. Recupere senha Olá para o registro de contêiner de saudação CLI do Azure.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. Adicionar o novo de tooa registro de contêiner do Azure id e senha `<server>` coleção em Olá *settings.xml* arquivo.
Olá `id` e `username` são Olá nome do registro de saudação. Saudação de uso `password` valor do comando anterior de saudação (sem aspas).

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Navegue de diretório do projeto toohello concluída para o seu aplicativo de inicialização de Spring (por exemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*"ou"*/users/robert/SpringBoot/gs-spring-boot-docker / concluída*") e abra hello *pom.xml* arquivo com um editor de texto.

1. Saudação de atualização `<properties>` coleção em Olá *pom.xml* arquivo com o valor de servidor de logon Olá para o registro de contêiner do Azure.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Saudação de atualização `<plugins>` coleção em Olá *pom.xml* arquivo de forma que Olá `<plugin>` contém Olá logon endereço e o registro do nome do servidor para o registro de contêiner do Azure.

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

1. Navegue de diretório do projeto toohello concluída para o seu aplicativo de inicialização de Spring e execute Olá comando toobuild Olá Docker contêiner e enviar por push Olá toohello registro da imagem a seguir:

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  Você receberá uma mensagem de erro é semelhante tooone seguinte hello quando Maven envia Olá tooAzure de imagem:
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Se você receber esse erro, faça logon tooAzure da linha de comando do Docker hello.
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Em seguida, envie por push o seu contêiner:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a>Criar um Kubernetes Cluster no ACS usando Olá CLI do Azure

1. Crie um cluster Kubernetes no Serviço de Contêiner do Azure. Hello comando a seguir cria um *kubernetes* cluster Olá *wingtiptoys kubernetes* recurso grupo com *containerservice wingtiptoys* como cluster Olá nome, e *kubernetes wingtiptoys* como prefixo DNS hello:
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   Este comando pode demorar um pouco toocomplete.

1. Instalar `kubectl` usando Olá CLI do Azure. Os usuários do Linux podem ter tooprefix esse comando com `sudo` desde que implanta Olá Kubernetes CLI muito`/usr/local/bin`.
   ```azurecli
   az acs kubernetes install-cli
   ```

1. Baixar informações de configuração de cluster Olá, portanto, você pode gerenciar seu cluster de interface de web Kubernetes hello e `kubectl`. 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a>Implantar Olá imagem tooyour Kubernetes cluster

Este tutorial implanta usando o aplicativo hello `kubectl`, em seguida, permitir você tooexplore Olá implantação por meio da interface web hello Kubernetes.

### <a name="deploy-with-hello-kubernetes-web-interface"></a>Implantar a interface do hello Kubernetes da web

1. Abra um prompt de comando.

1. Abra o site de configuração de saudação para seu cluster Kubernetes no navegador padrão:
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. Quando o site de configuração Kubernetes Olá abre no navegador, clique em link Olá muito**implantar um aplicativo em contêineres**:

   ![Site de configuração do Kubernetes][KB01]

1. Olá quando **implantar um aplicativo em contêineres** página é exibida, especifique Olá as opções a seguir:

   a. Selecione **Especificar detalhes do aplicativo abaixo**.

   b. Insira o nome do aplicativo de inicialização de Spring para Olá **nome do aplicativo**; por exemplo: "*gs spring-inicialização docker*".

   c. Insira sua imagem de contêiner e de servidor de logon do anteriormente para Olá **imagem de contêiner**; por exemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".

   d. Escolha **externo** para Olá **Service**.

   e. Especifique as portas internas e externas no hello **porta** e **porta de destino** caixas de texto.

   ![Site de configuração do Kubernetes][KB02]


1. Clique em **implantar** toodeploy contêiner de saudação.

   ![Implantar o contêiner][KB05]

1. Após a implantação de seu aplicativo, você verá o aplicativo Spring Boot listado em **Serviços**.

   ![Serviços Kubernetes][KB06]

1. Se você clicar em links Olá para **pontos de extremidade externos**, você pode ver o aplicativo de inicialização Spring em execução no Azure.

   ![Serviços Kubernetes][KB07]

   ![Procurar aplicativo de exemplo no Azure][SB02]


### <a name="deploy-with-kubectl"></a>Implantar com kubectl

1. Abra um prompt de comando.

1. Executar seu contêiner no cluster de Kubernetes hello usando Olá `kubectl run` comando. Forneça um nome de serviço para seu aplicativo em Kubernetes e o nome de imagem completa de saudação. Por exemplo:
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   Neste comando:

   * nome do contêiner Olá `gs-spring-boot-docker` é especificada imediatamente após Olá `run` comando

   * Olá `--image` parâmetro especifica Olá combinados server de logon e o nome da imagem como`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`

1. Expor seu cluster Kubernetes externamente usando Olá `kubectl expose` comando. Especifique o nome do serviço, Olá público TCP porta usada tooaccess Olá aplicativo e a porta de destino interno Olá em que seu aplicativo escuta. Por exemplo:
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   Neste comando:

   * nome do contêiner Olá `gs-spring-boot-docker` é especificada imediatamente após Olá `expose deployment` comando

   * Olá `--type` parâmetro especifica esse cluster Olá usa o balanceador de carga

   * Olá `--port` parâmetro especifica Olá público porta TCP 80. Acessar o aplicativo hello nesta porta.

   * Olá `--target-port` parâmetro especifica Olá interno TCP porta 8080. o balanceador de carga Olá encaminha solicitações tooyour aplicativo nesta porta.

1. Depois que o aplicativo hello é implantado toohello cluster, endereço IP externo de saudação de consulta e abri-lo no seu navegador da web:

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Procurar aplicativo de exemplo no Azure][SB02]


## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar a inicialização de Spring no Azure, consulte Olá artigos a seguir:

* [Implantar um toohello Spring aplicativo de inicialização do serviço de aplicativo do Azure](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Implantar um aplicativo de inicialização Spring em Linux em hello Azure serviço de contêiner](container-service-deploy-spring-boot-app-on-linux.md)

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].

Para obter mais informações sobre Olá Spring inicialização no projeto de exemplo do Docker, consulte [inicialização Spring no guia de Introdução do Docker].

Olá links a seguir fornece informações adicionais sobre como criar aplicativos de inicialização Spring:

* Para obter mais informações sobre como criar um aplicativo de inicialização de Spring simples, consulte Olá Spring Initializr em https://start.spring.io/.

Olá, links a seguir fornecem informações adicionais sobre como usar Kubernetes com o Azure:

* [Introdução ao cluster Kubernetes no Serviço de Contêiner](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [Usando Olá Kubernetes web da interface do usuário com o serviço de contêiner do Azure](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

Para obter mais informações sobre como usar a interface de linha de comando Kubernetes estão disponíveis no hello **kubectl** guia do usuário em <https://kubernetes.io/docs/user-guide/kubectl/>.

site de Kubernetes Olá tem vários artigos que abordam o uso de imagens em registros privados:

* [Configurar contas de serviço para Pods]
* [Namespaces]
* [Extrair uma imagem de um registro privado]

Para obter exemplos adicionais para como toouse Docker personalizado imagens com o Azure, consulte [usando uma imagem personalizada do Docker para o aplicativo Web do Azure no Linux].

<!-- URL List -->

[Azure Interface de linha de comando (CLI)]: /cli/azure/overview
[Serviço de contêiner do azure (ACS)]: https://azure.microsoft.com/services/container-service/
[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[usando uma imagem personalizada do Docker para o aplicativo Web do Azure no Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[ferramentas Java para o Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring inicialização]: http://projects.spring.io/spring-boot/
[inicialização Spring no guia de Introdução do Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configurar contas de serviço para Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Extrair uma imagem de um registro privado]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
