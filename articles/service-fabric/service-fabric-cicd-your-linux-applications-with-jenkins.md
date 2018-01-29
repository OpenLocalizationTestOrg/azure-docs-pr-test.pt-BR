---
title: "Integração e build contínuo para seus aplicativos do Linux do Azure Service Fabric usando o Jenkins | Microsoft Docs"
description: "Integração e build contínuo para seu aplicativo do Linux do Service Fabric usando o Jenkins"
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/27/2017
ms.author: saysa
ms.openlocfilehash: 80c52cfeab007030203b6af4bb220f1a847e9426
ms.sourcegitcommit: c87e036fe898318487ea8df31b13b328985ce0e1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2017
---
# <a name="use-jenkins-to-build-and-deploy-your-linux-applications"></a>Usar o Jenkins para criar e implantar seus aplicativos do Linux
Jenkins é uma ferramenta popular para implantação e integração contínua de seus aplicativos. Veja como criar e implantar o aplicativo do Service Fabric do Azure usando o Jenkins.

## <a name="general-prerequisites"></a>Pré-requisitos gerais
- Ter o Git instalado localmente. Você pode instalar a versão apropriada do Git da [página de downloads do Git](https://git-scm.com/downloads), com base no seu sistema operacional. Se for novo no Git, saiba mais sobre ele na [documentação do Git](https://git-scm.com/docs).

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a>Configurar o Jenkins em um cluster do Service Fabric

Você pode configurar o Jenkins dentro ou fora de um cluster do Service Fabric. As próximas seções mostram como configurá-lo em um cluster usando uma conta de armazenamento do Azure para salvar o estado da instância do contêiner.

### <a name="prerequisites"></a>pré-requisitos
1. Ter um cluster Linux do Service Fabric pronto. Um cluster do Service Fabric criado no portal do Azure já tem o Docker instalado. Se estiver realizando a execução localmente no cluster, verifique se o Docker está instalado usando o comando ``docker info``. Se não estiver instalado, instale-o adequadamente usando os seguintes comandos:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ``` 

   > [!NOTE]
   > Verifique se a porta 8081 foi especificada como um ponto de extremidade personalizado no cluster.
   >

2. Clone o aplicativo usando as seguintes etapas:
  ```sh
  git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
  cd service-fabric-java-getting-started/Services/JenkinsDocker/
  ```

3. Mantenha o estado do contêiner Jenkins em um compartilhamento de arquivos:
  * Crie uma conta de armazenamento do Azure na **mesma região** do que o seu cluster com um nome como ``sfjenkinsstorage1``.
  * Crie um **Compartilhamento de Arquivos** na Conta de Armazenamento com um nome como ``sfjenkins``.
  * Clique em **Conectar** no compartilhamento de arquivos e observe os valores exibidos em **Conectando por meio do Linux**, o valor deve ser semelhantes a este:
  ```sh
  sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
  ```

  > [!NOTE]
  > Para montar compartilhamentos de cifs, é necessário ter o pacote cifs-utils instalado nos nós do cluster.       
  >

4. Atualize os valores de espaço reservado no script ```setupentrypoint.sh``` com os detalhes correspondentes do armazenamento do Azure da etapa 3.
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
  * Substitua ``[REMOTE_FILE_SHARE_LOCATION]`` pelo valor ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` do resultado da conexão da etapa 3 acima.
  * Substitua ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` pelo valor ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` da etapa 3 acima.

5. **Apenas cluster seguro:** para configurar a implantação de aplicativos em um cluster seguro do Jenkins, o certificado deve ser acessível dentro do contêiner do Jenkins. Nos clusters do Linux, os certificados (PEM) simplesmente são copiados do repositório especificado pelo X509StoreName para o contêiner. No ApplicationManifest em ContainerHostPolicies, adicione essa referência de certificado e atualize o valor de impressão digital. O valor de impressão digital deve ser o de um certificado localizado no nó.
  ```xml
  <CertificateRef Name="MyCert" X509FindValue="[Thumbprint]"/>
  ```
  > [!NOTE]
  > O valor de impressão digital deve ser o mesmo que o certificado usado para se conectar ao cluster seguro. 
  >

6. Conecte-se ao cluster e instale o aplicativo contêiner.

  **Cluster seguro**
  ```sh
  sfctl cluster select --endpoint https://PublicIPorFQDN:19080  --pem [Pem] --no-verify # cluster connect command
  bash Scripts/install.sh
  ```

  **Cluster não seguro**
  ```sh
  sfctl cluster select --endpoint http://PublicIPorFQDN:19080 # cluster connect command
  bash Scripts/install.sh
  ```

  Isso instala um contêiner Jenkins no cluster e pode ser monitorado usando o Service Fabric Explorer.

    > [!NOTE]
    > O download da imagem do Jenkins no cluster pode demorar alguns minutos.
    >

### <a name="steps"></a>Etapas
1. No navegador, acesse ``http://PublicIPorFQDN:8081``. Ela fornece o caminho da senha de administrador inicial necessária para entrar. 
2. Examine o Service Fabric Explorer para determinar em qual nó o contêiner Jenkins está em execução. Entre com SSH (Secure Shell) neste nó.
```sh
ssh user@PublicIPorFQDN -p [port]
``` 
3. Obter a ID de instância do contêiner usando ``docker ps -a``.
4. Entre com SSH (Secure Shell) no contêiner e cole o caminho exibido no portal do Jenkins. Por exemplo, se o portal mostrar o caminho `PATH_TO_INITIAL_ADMIN_PASSWORD`, execute o seguinte:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  ```
  ```sh
  cat PATH_TO_INITIAL_ADMIN_PASSWORD # This displays the pasword value
  ```
5. Na página introdução ao Jenkins, escolha a opção Selecionar plug-ins para instalação, marque a caixa de seleção **Nenhum** e clique em instalar.
6. Crie um usuário ou selecione para continuar como um administrador.

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a>Configurar o Jenkins fora de um cluster do Service Fabric

Você pode configurar o Jenkins dentro ou fora de um cluster do Service Fabric. As seções a seguir mostram como configurá-lo fora de um cluster.

### <a name="prerequisites"></a>pré-requisitos
Você precisa ter o Docker instalado. Os comandos abaixo podem ser usados para instalar o Docker do terminal:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

Agora, ao executar ``docker info`` no terminal, você deve ver a saída executada pelo serviço Docker.

### <a name="steps"></a>Etapas
  1. Baixar a imagem de contêiner Jenkins do Service Fabric: ``docker pull rapatchi/jenkins:v10``. Esta imagem é fornecida com o plug-in do Service Fabric Jenkins pré-instalado.
  2. Executar a imagem de contêiner:``docker run -itd -p 8080:8080 rapatchi/jenkins:v10``
  3. Obter a ID de instância de imagem de contêiner. Você pode listar todos os contêineres do Docker com o comando ``docker ps –a``
  4. Entre no portal do Jenkins usando as seguintes etapas:

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    Se a ID do contêiner for 2d24a73b5964, use 2d 24.
    * Esta senha é necessária para entrar no painel do Jenkins do portal, que é ``http://<HOST-IP>:8080``
    * Depois de entrar pela primeira vez, você pode criar a própria conta de usuário e usá-la futuramente ou pode continuar a usar a conta de administrador. Após criar um usuário, você precisa continuar com ele.
  5. Configure o GitHub para trabalhar com o Jenkins, usando as etapas mencionadas em [Gerando uma nova chave SSH e adicionando-a ao agente SSH](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
        * Usar as instruções fornecidas no GitHub para gerar uma chave SSH e adicionar a chave SSH à conta do GitHub que está hospedando o repositório.
        * Execute os comandos mencionados no link anterior no shell Jenkins Docker (e não no host).
      * Para fazer logon no shell Jenkins do host, use os seguintes comandos:

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

Verifique se o cluster ou a máquina em que a imagem de contêiner Jenkins está hospedada tem um IP público. Isso permite que a instância do Jenkins receba notificações do GitHub.


## <a name="create-and-configure-a-jenkins-job"></a>Criar e configurar um trabalho do Jenkins

1. Criar um **novo item** no painel.
2. Insira um nome de item (por exemplo, **MyJob**). Selecione **projeto em estilo livre**e clique em **OK**.
3. Acesse a página do trabalho e clique em **Configurar**.

   a. Na seção geral, marque a caixa de seleção **Proejto GitHub** e especifique a URL do project GitHub. Essa URL hospeda o aplicativo Java do Service Fabric que você deseja integrar à integração contínua do Jenkins, no fluxo de implantação contínua (CI/CD) (por exemplo, ``https://github.com/sayantancs/SFJenkins``).

   b. Na seção **Gerenciamento de Código-Fonte**, selecione **Git**. Especifique a URL do repositório que hospeda o aplicativo Java do Service Fabric que você deseja integrar ao fluxo CI/CD do Jenkins (por exemplo, ``https://github.com/sayantancs/SFJenkins.git``). Você também pode especificar aqui quais ramificações devem ser criadas (por exemplo, **/mestre**).
4. Configure seu *GitHub* (que está hospedando o repositório) para que ele seja capaz de se comunicar com o Jenkins. Use as seguintes etapas:

   a. Vá para sua página do repositório GitHub. Vá para **Configurações** > **Integrações e Serviços**.

   b. Selecione **Adicionar Serviço**, digite **Jenkins** e selecione o **plug-in Jenkins-Github**.

   c. Insira a URL do webhook Jenkins (por padrão, ele deve ser ``http://<PublicIPorFQDN>:8081/github-webhook/``). Clique em **adicionar/atualizar serviço**.

   d. Um evento de teste é enviado para a instância do Jenkins. Você verá uma marca de seleção verde ao lado do webhook no GitHub, e o projeto será criado.

   e. Na seção **Criar Gatilhos**, selecione a opção de compilação desejada. Para este exemplo, você deseja disparar uma compilação sempre que ocorrer alguma envio para o repositório. Portanto, você seleciona **Gatilho de gancho do GitHub para sondagem GITScm**. (Anteriormente, essa opção se chamava **Compilar quando uma alteração for enviada ao GitHub**.)

   f. **Seção de build para aplicativos Java:** Na **Seção de build**, no menu suspenso **Adicionar etapa de build**, selecione a opção **Invocar script Gradle**. No widget que aparecer, abra o menu avançado, especifique o caminho para **Script do build raiz** para o aplicativo. Ele obtém o build.gradle no caminho especificado e funciona de maneira correspondente. Se você criar um projeto chamado ``MyActor``(usando o plug-in Eclipse ou gerador Yeoman), o script da build raiz deverá conter ``${WORKSPACE}/MyActor``. Confira a seguinte captura de tela para obter um exemplo dessa aparência:

    ![Ação Compilar do Jenkins no Service Fabric][build-step]

   g. **Seção de build para aplicativos .Net Core:** Na **Seção de build**, no menu suspenso **Adicionar etapa de build**, selecione a opção **Executar Shell**. Na caixa de comando exibida, o diretório precisa primeiro ser alterado para o caminho em que o arquivo build.sh está localizado. Quando o diretório tiver sido alterado, o script build.sh poderá ser executado e criará o aplicativo.

      ```sh
      cd /var/jenkins_home/workspace/[Job Name]/[Path to build.sh]  # change directory to location of build.sh file
      ./build.sh
      ```

    Abaixo há um exemplo dos comandos usados para criar o exemplo [Serviço de contador](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started/tree/master/Services/CounterService) com um nome de trabalho de Jenkins de CounterServiceApplication.

    ![Ação Compilar do Jenkins no Service Fabric][build-step-dotnet]
  
   h. No menu suspenso **Ações Pós-Compilação**, selecione **Implantar Projeto do Service Fabric**. Aqui, você precisa fornecer detalhes do cluster em que o aplicativo do Service Fabric compilado para o Jenkins deve ser implantado. O caminho para o certificado pode ser encontrado fazendo-se o eco do valor da variável de ambiente Certificates_JenkinsOnSF_Code_MyCert_PEM do eco dentro do contêiner. Esse caminho pode ser usado para os campos Chave de cliente e Certificado de cliente.

      ```sh
      echo $Certificates_JenkinsOnSF_Code_MyCert_PEM
      ```
   
    Você também pode fornecer detalhes adicionais de aplicativos usados para implantar o aplicativo. Confira a seguinte captura de tela para obter um exemplo dessa aparência:

    ![Ação Compilar do Jenkins no Service Fabric][post-build-step]

      > [!NOTE]
      > Aqui, o cluster pode ser o mesmo que hospeda o aplicativo de contêiner Jenkins caso você esteja usando o Service Fabric para implantar a imagem de contêiner Jenkins.
      >

## <a name="next-steps"></a>Próximas etapas
O GitHub e o Jenkins agora estão configurados. Considere fazer algumas alterações de exemplo em seu projeto ``MyActor`` no repositório de exemplo, https://github.com/sayantancs/SFJenkins. Envie por push as alterações à ramificação ``master`` remota (ou a qualquer ramificação que você configurou para o trabalho). Isso dispara o trabalho do Jenkins, ``MyJob``, que você configurou. Busca as alterações do GitHub, compila-as e implanta o aplicativo no ponto de extremidade do cluster especificado nas ações pós-compilação.  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-application-with-jenkins/build-step.png
  [build-step-dotnet]: ./media/service-fabric-cicd-your-linux-application-with-jenkins/build-step-dotnet.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-application-with-jenkins/post-build-step.png

