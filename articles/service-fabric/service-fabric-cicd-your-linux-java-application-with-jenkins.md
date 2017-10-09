---
title: "aaaContinuous integração para o seu aplicativo do Azure Service Fabric Linux Java usando Jenkins e compilação | Microsoft Docs"
description: "Compilação contínua e integração para o aplicativo Java Linux do Azure Service Fabric usando o Jenkins"
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
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 15da2cb8c759233219369ea889550da93748129f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-jenkins-toobuild-and-deploy-your-linux-java-application"></a>Use toobuild Jenkins e implantar seu aplicativo Java do Linux
Jenkins é uma ferramenta popular para implantação e integração contínua de seus aplicativos. Aqui está como toobuild e implantar seu aplicativo do Azure Service Fabric usando Jenkins.

## <a name="general-prerequisites"></a>Pré-requisitos gerais
- Ter o Git instalado localmente. Você pode instalar a versão Git apropriada de saudação do [página de downloads de saudação Git](https://git-scm.com/downloads), com base no seu sistema operacional. Se você for novo tooGit, saiba mais sobre ele de saudação [Git documentação](https://git-scm.com/docs).
- Ter Olá plug-in do serviço de malha Jenkins útil. Você pode baixá-lo de [Downloads do Service Fabric](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi).

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a>Configurar o Jenkins em um cluster do Service Fabric

Você pode configurar o Jenkins dentro ou fora de um cluster do Service Fabric. a seguir Olá seções mostrar como tooset-o dentro de um cluster durante o uso de um armazenamento do Azure conta toosave estado de saudação da instância de contêiner de saudação.

### <a name="prerequisites"></a>Pré-requisitos
1. Ter um cluster Linux do Service Fabric pronto. Um cluster do Service Fabric já criado de saudação portal do Azure tem Docker instalado. Se você estiver executando o cluster Olá localmente, verifique se o Docker é instalado usando o comando Olá ``docker info``. Se não estiver instalado, instalá-lo adequadamente usando Olá comandos a seguir:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. Ter o aplicativo de contêiner do Service Fabric hello implantado em cluster hello, usando Olá etapas a seguir:

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
cd service-fabric-java-getting-started/Services/JenkinsDocker/
```

3. Você precisa Olá conectar detalhes de opção de saudação compartilhamento de arquivos do armazenamento do Azure, onde você deseja que o estado de saudação toopersist da instância de contêiner do hello Jenkins. Se você estiver usando o portal do Microsoft Azure Olá para Olá iguais,. Siga as etapas de saudação - criar uma conta de armazenamento do Azure, digamos que ``sfjenkinsstorage1``. Crie um **Compartilhamento de Arquivos** nessa conta de armazenamento, digamos, ``sfjenkins``. Clique em **conectar** para Olá Olá de compartilhamento de arquivos e observe o valores exibe em **conectando do Linux**, digamos que seria como as seguintes:
```sh
sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
```

4. Atualizar valores de espaço reservado Olá Olá ```setupentrypoint.sh``` script com detalhes correspondentes do armazenamento do azure.
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
Substituir ``[REMOTE_FILE_SHARE_LOCATION]`` com valor de saudação ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` da saída de saudação de saudação conectar-se no ponto 3 acima.
Substituir ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` com valor de saudação ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` de ponto 3 acima.

5. Conecte-se o cluster toohello e instalar o aplicativo de contêiner hello.
```azurecli
sfctl cluster select --endpoint http://PublicIPorFQDN:19080   # cluster connect command
bash Scripts/install.sh
```
Isso instala um contêiner Jenkins no cluster Olá e pode ser monitorado usando Olá Service Fabric Explorer.

### <a name="steps"></a>Etapas
1. Em seu navegador, vá muito``http://PublicIPorFQDN:8081``. Ele fornece o caminho de saudação do toosign de senha necessária Olá administrador inicial no. Você pode continuar toouse Jenkins como um usuário administrativo. Ou você pode criar e alterar usuário hello, depois que você entrar com a conta de administrador inicial hello.

   > [!NOTE]
   > Verifique se a porta 8081 de saudação é especificada como a porta de ponto de extremidade de aplicativo hello enquanto você estiver criando um cluster de saudação.
   >

2. Obter ID de instância de contêiner hello usando ``docker ps -a``.
3. Secure Shell (SSH) de entrada toohello contêiner e, em seguida, cole o caminho Olá que foi exibido no portal do hello Jenkins. Por exemplo, se no portal de saudação mostra o caminho de saudação `PATH_TO_INITIAL_ADMIN_PASSWORD`, execute Olá seguinte:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. Configurar o GitHub toowork com Jenkins, usando as etapas Olá mencionadas [gerar uma nova chave SSH e adicioná-lo toohello SSH agente](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
    * Use instruções Olá fornecidas pela chave SSH do GitHub toogenerate hello e tooadd Olá SSH chave toohello conta do GitHub que está hospedando o seu repositório.
    * Execute comandos Olá mencionados na saudação anterior link Olá shell Jenkins Docker (e não em seu host).
    * toosign em toohello Jenkins shell do seu host, use Olá comando a seguir:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a>Configurar o Jenkins fora de um cluster do Service Fabric

Você pode configurar o Jenkins dentro ou fora de um cluster do Service Fabric. Olá Mostrar seções a seguir como tooset-o fora de um cluster.

### <a name="prerequisites"></a>Pré-requisitos
É necessário toohave Docker instalado. Olá comandos a seguir pode ser usado tooinstall Docker de saudação terminal:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

Agora, quando você executa ``docker info`` no hello terminal, você verá na saída de saudação que Olá Docker serviço está em execução.

### <a name="steps"></a>Etapas
  1. Imagem de contêiner Olá Jenkins de malha do serviço de pull:``docker pull raunakpandya/jenkins:v1``
  2. Execute a imagem de contêiner hello:``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``
  3. Obter ID de saudação da instância de imagem de contêiner de saudação. Você pode listar todos os contêineres do Docker Olá com o comando Olá``docker ps –a``
  4. Entre no toohello Jenkins portal usando Olá etapas a seguir:

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    Se a ID do contêiner for 2d24a73b5964, use 2d 24.
    * Essa senha é necessária para entrar no painel de Jenkins toohello do portal, que é``http://<HOST-IP>:8080``
    * Após se inscrever hello primeira vez, você pode criar sua própria conta de usuário e usá-lo para fins de futuras, ou você pode continuar a conta de administrador toouse hello. Depois de criar um usuário, você precisa toocontinue com isso.
  5. Configurar o GitHub toowork com Jenkins, usando as etapas Olá mencionadas [gerar uma nova chave SSH e adicioná-lo toohello SSH agente](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
        * Use instruções Olá fornecidas pela chave SSH de saudação do GitHub toogenerate e tooadd Olá SSH chave toohello conta do GitHub que está hospedando o repositório de saudação.
        * Execute comandos Olá mencionados na saudação anterior link Olá shell Jenkins Docker (e não em seu host).
      * toosign em toohello Jenkins shell do seu host, use Olá comandos a seguir:

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

Certifique-se de que cluster hello ou máquina onde Olá Jenkins contêiner imagem está hospedada tem um IP público. Isso permite que as notificações do hello Jenkins instância tooreceive do GitHub.

## <a name="install-hello-service-fabric-jenkins-plug-in-from-hello-portal"></a>Instalar Olá Jenkins de malha do serviço Plug-in do portal de saudação

1. Vá muito``http://PublicIPorFQDN:8081``
2. No painel de Jenkins hello, selecione **Jenkins gerenciar** > **gerenciar plug-ins** > **avançado**.
Aqui, você pode carregar um plug-in. Selecione **Escolher arquivo**e, em seguida, selecione Olá **serviceFabric.hpi** arquivo que você baixou em pré-requisitos. Quando você seleciona **carregar**, Jenkins instala automaticamente Olá plug-in. Se solicitado, permita a reinicialização.

## <a name="create-and-configure-a-jenkins-job"></a>Criar e configurar um trabalho do Jenkins

1. Criar um **novo item** no painel.
2. Insira um nome de item (por exemplo, **MyJob**). Selecione **projeto em estilo livre**e clique em **OK**.
3. Acesse a página de saudação do trabalho e clique **configurar**.

   a. Na seção geral de hello, em **GitHub projeto**, especifique a URL do projeto GitHub. Essa URL hosts Olá Service Fabric aplicativo Java que você deseja toointegrate com hello integração contínua Jenkins, implantação contínua (CI/CD) fluxo (por exemplo, ``https://github.com/sayantancs/SFJenkins``).

   b. Em Olá **código-fonte gerenciamento** seção, selecione **Git**. Especifique a URL do repositório Olá que hospeda o aplicativo de serviço do Fabric Java hello que você deseja toointegrate com hello fluxo Jenkins CI/CD (por exemplo, ``https://github.com/sayantancs/SFJenkins.git``). Além disso, você pode especificar aqui quais toobuild ramificação (por exemplo, **/mestre**).
4. Configurar seu *GitHub* (que está hospedando o repositório de saudação) para que ele seja capaz de tootalk tooJenkins. Olá Use as etapas a seguir:

   a. Acesse a página de repositório do GitHub tooyour. Vá muito**configurações** > **integrações e serviços**.

   b. Selecione **Adicionar serviço**, tipo **Jenkins**e selecione hello **Jenkins GitHub plug-in**.

   c. Insira a URL do webhook Jenkins (por padrão, ele deve ser ``http://<PublicIPorFQDN>:8081/github-webhook/``). Clique em **adicionar/atualizar serviço**.

   d. Um evento de teste é enviado tooyour Jenkins instância. Você deve ver uma marca de seleção verde Olá webhook no GitHub e criará seu projeto.

   e. Em Olá **criar gatilhos** seção, selecione a opção desejada de compilação. Neste exemplo, você deseja tootrigger uma compilação sempre que ocorre algum repositório toohello de envio. Portanto, você seleciona **Gatilho de gancho do GitHub para sondagem GITScm**. (Anteriormente, essa opção foi chamada **criar quando uma alteração é enviada por push tooGitHub**.)

   f. Em Olá **criar seção**, na lista suspensa Olá **adicionar a etapa de compilação**, selecione opção Olá **invocar Gradle Script**. No widget de saudação que vem, especifique o caminho de saudação muito**raiz criar script** para seu aplicativo. Ele seleciona gradle do caminho de saudação especificado e funciona adequadamente. Se você criar um projeto chamado ``MyActor`` (usando o gerador de plug-in ou Yeoman Eclipse Olá), o script de compilação Olá raiz deve conter ``${WORKSPACE}/MyActor``. Consulte Olá captura de tela de um exemplo de aparência a seguir:

    ![Ação Compilar do Jenkins no Service Fabric][build-step]

   g. De saudação **ações de pós-compilação** lista suspensa, selecione **implantar projeto do serviço de malha**. Aqui, você deve tooprovide cluster detalhes onde hello Jenkins compilada aplicativo de malha do serviço devem ser implantados. Você também pode fornecer detalhes de aplicativo adicionais usados aplicativo hello de toodeploy. Consulte Olá captura de tela de um exemplo de aparência a seguir:

    ![Ação Compilar do Jenkins no Service Fabric][post-build-step]

   > [!NOTE]
   > cluster de saudação aqui pode ser o mesmo como Olá uma hospedagem Olá Jenkins aplicativo de contêiner, caso você esteja usando imagem de contêiner do Service Fabric toodeploy Olá Jenkins.
   >

## <a name="next-steps"></a>Próximas etapas
O GitHub e o Jenkins agora estão configurados. Considere fazer algum exemplo alterar seu ``MyActor`` projeto no exemplo de repositório hello, https://github.com/sayantancs/SFJenkins. Enviar por push o tooa alterações remoto ``master`` ramificação (ou qualquer que você configurou toowork com). Isso dispara o trabalho de Jenkins hello, ``MyJob``, que você configurou. Busca de alterações de saudação do GitHub, compila-los e implanta Olá aplicativo toohello cluster ponto de extremidade especificado em ações de pós-compilação.  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png
