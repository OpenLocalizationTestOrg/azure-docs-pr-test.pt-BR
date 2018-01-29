---
title: "CI/CD com o Mecanismo do Serviço de Contêiner do Azure e o modo Swarm"
description: "Usar o Mecanismo do Serviço de Contêiner do Azure com o modo Swarm, um Registro de Contêiner do Azure e o Visual Studio Team Services para fornecer continuamente um aplicativo .NET Core com vários contêineres"
services: container-service
author: diegomrtnzg
manager: timlt
ms.service: container-service
ms.topic: article
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 6aa690ff7ec0689db78ff1225d36171adb30ee2c
ms.sourcegitcommit: 5d3e99478a5f26e92d1e7f3cec6b0ff5fbd7cedf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/06/2017
---
# <a name="full-cicd-pipeline-to-deploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a>Pipeline de CI/CD completo para implantar um aplicativo com vários contêineres no Serviço de Contêiner do Azure com Mecanismo do ACS e modo Docker Swarm usando o Visual Studio Team Services

*Este artigo tem base na documentação [Pipeline de CI/CD completo para implantar um aplicativo com vários contêineres no Serviço de Contêiner do Azure com Docker Swarm usando o Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md)*

Hoje, um dos maiores desafios ao desenvolver aplicativos modernos para a nuvem é ser capaz de fornecer esses aplicativos continuamente. Neste artigo, você aprenderá a implementar uma integração contínua completa e o pipeline de implantação (CI/CD) usando: 
* Mecanismo do Serviço de Contêiner do Azure com o modo Docker Swarm
* Registro de Contêiner do Azure
* Visual Studio Team Services

Este artigo se baseia em um aplicativo simples, disponível no [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), desenvolvido com o ASP.NET Core. O aplicativo é composto de quatro serviços diferentes: três APIs da Web e um front-end da Web:

![Aplicativo de exemplo MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

O objetivo é fornecer esse aplicativo continuamente em um cluster no modo Docker Swarm usando o Visual Studio Team Services. A figura a seguir fornece detalhes sobre esse pipeline de entrega contínua:

![Aplicativo de exemplo MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

Uma breve explicação das etapas:

1. As alterações do código são confirmadas no repositório do código-fonte (aqui, GitHub) 
2. O GitHub dispara uma compilação no Visual Studio Team Services 
3. O Visual Studio Team Services obtém a versão mais recente das fontes e compila todas as imagens que compõem o aplicativo 
4. O Visual Studio Team Services envia cada imagem para um registro do Docker criado usando o serviço do Registro de Contêiner do Azure 
5. O Visual Studio Team Services dispara uma nova versão 
6. A versão executa alguns comandos usando o SSH no nó mestre do cluster do serviço de contêiner do Azure 
7. O modo Docker Swarm no cluster obtém a versão mais recente das imagens 
8. A nova versão do aplicativo é implantada usando o Docker Stack 

## <a name="prerequisites"></a>Pré-requisitos

Antes de iniciar este tutorial, você precisa concluir as seguintes tarefas:

- [Criar um cluster no modo Swarm no Serviço de Contêiner do Azure com o Mecanismo do ACS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [Conectar-se ao cluster Swarm no Serviço de Contêiner do Azure](../container-service-connect.md)
- [Criar um registro de contêiner do Azure](../../container-registry/container-registry-get-started-portal.md)
- [Ter uma conta do Visual Studio Team Services e projeto de equipe criados](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Dividir o repositório GitHub para sua conta do GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> O orquestrador Docker Swarm no Serviço de Contêiner do Azure usa um Swarm autônomo herdado. Atualmente, o [modo Swarm](https://docs.docker.com/engine/swarm/) integrado (no Docker 1.12 e superior) não é um orquestrador com suporte no Serviço de Contêiner do Azure. Por esse motivo, estamos usando o [Mecanismo do ACS](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), um [modelo de início rápido](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/) de contribuição da comunidade, ou uma solução Docker no [Azure Marketplace](https://azuremarketplace.microsoft.com).
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>Etapa 1: Configurar sua conta do Visual Studio Team Services 

Nesta seção, você configura sua conta do Visual Studio Team Services. Para configurar os Pontos de extremidade de serviço do VSTS em seu projeto do Visual Studio Team Services, clique no ícone **Configurações** na barra de ferramentas e selecione **Serviços**.

![Abra o Ponto de extremidade de serviço](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a>Conectar o Visual Studio Team Services e a conta o Azure

Configure uma conexão entre seu projeto do VSTS e sua conta do Azure.

1. À esquerda, clique em **Novo Ponto de Extremidade de Serviço** > **Azure Resource Manager**.
2. Para autorizar o VSTS a trabalhar com sua conta do Azure, selecione sua **Assinatura** e clique em **OK**.

    ![Visual Studio Team Services – Autorizar Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a>Conectar o Visual Studio Team Services e o GitHub

Configure uma conexão entre seu projeto VSTS e sua conta GitHub.

1. À esquerda, clique em **Novo Ponto de Extremidade de Serviço** > **GitHub**.
2. Para autorizar o VSTS a trabalhar com sua conta GitHub, clique em **Autorizar** e siga o procedimento na janela aberta.

    ![Visual Studio Team Services - Autorizar GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-to-your-azure-container-service-cluster"></a>Conectar o VSTS ao seu cluster do Serviço de Contêiner do Azure

As últimas etapas antes de entrar no pipeline de CI/CD servem para configurar as conexões externas com seu cluster do Docker Swarm no Azure. 

1. Para o cluster Docker Swarm, adicione um ponto de extremidade do tipo **SSH**. Depois, insira as informações de conexão SSH de seu cluster Swarm (nó mestre).

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

Toda a configuração é concluída agora. As próximas etapas, você criará o pipeline de CI/CD que compila e implanta o aplicativo no cluster Docker Swarm. 

## <a name="step-2-create-the-build-definition"></a>Etapa 2: Criar a definição da compilação

Nesta etapa, você configura uma definição da compilação para seu projeto VSTS e define o fluxo de trabalho da compilação para suas imagens de contêiner

### <a name="initial-definition-setup"></a>Configuração da definição inicial

1. Para criar uma definição da compilação, conecte seu projeto do Visual Studio Team Services e clique em **Compilação e Versão**. Na seção **Definições da compilação**, clique em **+ Novo**. 

    ![Visual Studio Team Services - Nova Definição da Compilação](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. Selecione o **Processo vazio**.

    ![Visual Studio Team Services – Nova Definição de Compilação Vazia](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. Depois, clique na guia **Variáveis** e crie duas novas variáveis: **RegistryURL** e **AgentURL**. Cole os valores de seu Registro e do DNS de Agentes do Cluster.

    ![Visual Studio Team Services – Configuração de Variáveis de Compilação](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. Na página **Definições da Compilação**, abra a guia **Gatilhos** e configure a compilação para usar a integração contínua com a bifurcação do projeto MyShop que você criou nos pré-requisitos. Em seguida, selecione **Alterações em lote**. Selecione *docker-linux* como a **Especificação de branch**.

    ![Visual Studio Team Services - Configuração do Repositório de Compilação](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. Por fim, clique na guia **Opções** e configure a fila do Agente padrão para **Versão Prévia do Linux Hospedada**.

    ![Visual Studio Team Services – Configuração do Agente de Host](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-the-build-workflow"></a>Definir o fluxo de trabalho da compilação
As próximas etapas definem o fluxo de trabalho da compilação. Primeiro, você precisa configurar a origem do código. Para fazer isso, selecione **GitHub**, o **repositório** e o **branch** (docker-linux).

![Visual Studio Team Services – Configurar o código-fonte](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

Há cinco imagens de contêiner a compilar para o aplicativo *MyShop*. Cada imagem é compilada usando o arquivo Docker localizado nas pastas do projeto:

* ProductsApi
* Proxy
* RatingsApi
* RecommendationsApi
* ShopFront

Você precisa de duas etapas do Docker para cada imagem, uma para compilar a imagem e outra para enviar a imagem no registro de contêiner do Azure. 

1. Para adicionar uma etapa no fluxo de trabalho da compilação, clique em **+ Adicionar etapa de compilação** e selecione **Docker**.

    ![Visual Studio Team Services - Adicionar Etapas da Compilação](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. Para cada imagem, configure uma etapa que usa o comando `docker build`.

    ![Visual Studio Team Services - Compilação do Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    Para a operação de compilação, selecione o Registro de Contêiner do Azure, a ação **Criar uma imagem** e o Dockerfile que define cada imagem. Defina o **Diretório de Trabalho** como o diretório raiz do Dockerfile, defina o **Nome da Imagem** e selecione **Incluir Marca mais Recente**.
    
    O Nome da Imagem deve estar neste formato: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```. Substitua **[NAME]** pelo nome da imagem:
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. Para cada imagem, configure uma segunda etapa que usa o comando `docker push`.

    ![Visual Studio Team Services - Envio do Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    Para a operação de envio, selecione o registro de contêiner do Azure, a ação **Enviar uma imagem**, insira o **Nome da Imagem** compilado na etapa anterior e selecione **Incluir Marca mais Recente**.

4. Depois de configurar as etapas de compilação e envio para cada uma das cinco imagens, adicione mais três etapas do fluxo de trabalho de compilação.

   ![Visual Studio Team Services – Adicionar Tarefa de Linha de Comando](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. Uma tarefa da linha de comando que usa um script bash para substituir a ocorrência *RegistryURL* no arquivo docker-compose.yml pela variável RegistryURL. 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services – Atualizar arquivo de composição com a URL do Registro](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. Uma tarefa da linha de comando que usa um script bash para substituir a ocorrência *AgentURL* no arquivo docker-compose.yml pela variável AgentURL.
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. Uma tarefa que cancela o arquivo de Composição atualizado como um artefato de compilação para que ele possa ser usado na versão. Consulte a tela a seguir para obter detalhes.

         ![Visual Studio Team Services – Publicar Artefato](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - Publicar arquivo de composição](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. Clique em **Salvar e enfileirar** para testar sua definição de compilação.

   ![Visual Studio Team Services – Salvar e enfileirar](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services – Nova Fila](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. Se o **Build** estiver correto, você verá esta tela:

  ![Visual Studio Team Services – Compilação bem-sucedida](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-the-release-definition"></a>Etapa 3: Criar a definição da versão

O Visual Studio Team Services permite que você [gerencie as versões nos ambientes](https://www.visualstudio.com/team-services/release-management/). Você pode habilitar uma implantação contínua para verificar se seu aplicativo é implantado em seus ambientes diferentes (como de desenvolvimento, teste, pré-produção e produção) de forma suave. Você pode criar um ambiente que representa seu cluster do Serviço de Contêiner do Azure no modo Docker Swarm.

![Visual Studio Team Services - Versão para o ACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Configuração da versão inicial

1. Para criar uma definição da versão, clique em **Versões** > **+ Versão**

2. Para configurar a fonte do artefato, clique em **Artefatos** > **Vincular uma fonte do artefato**. Aqui, vincule essa nova definição da versão à compilação definida na etapa anterior. Depois disso, o arquivo docker-compose.yml fica disponível no processo da versão.

    ![Visual Studio Team Services - Artefatos da Versão](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. Para configurar o gatilho da versão, clique em **Gatilhos** e selecione **Implantação Contínua**. Defina o gatilho na mesma fonte do artefato. Essa configuração garante que uma nova versão comece assim que a compilação for concluída com êxito.

    ![Visual Studio Team Services - Gatilhos da Versão](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. Para configurar as variáveis de versão, clique em **Variáveis** e selecione **+Variável** para criar três novas variáveis com as informações do Registro: **docker.username**, **docker.password** e **docker.registry**. Cole os valores de seu Registro e do DNS de Agentes do Cluster.

    ![Visual Studio Team Services - Configuração do Repositório de Compilação](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > Conforme exibido na tela anterior, clique na caixa de seleção **Bloqueio** em docker.password. Essa configuração é importante para restringir a senha.
    >

### <a name="define-the-release-workflow"></a>Definir o fluxo de trabalho da versão

A versão do fluxo de trabalho é composta de duas tarefas que você adiciona.

1. Configure uma tarefa para copiar com segurança o arquivo de composição para uma pasta de *implantação* no nó mestre Docker Swarm usando a conexão SSH configurada anteriormente. Consulte a tela a seguir para obter detalhes.
    
    Pasta de origem: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```

    ![Visual Studio Team Services - SCP da Versão](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. Configure uma segunda tarefa para executar um comando bash e os comandos `docker` e `docker stack deploy` no nó mestre. Consulte a tela a seguir para obter detalhes.

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services - Bash da Versão](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    O comando executado no mestre usa a CLI do Docker e a CLI do Docker Compose para realizar as seguintes tarefas:

    - Logon no registro de contêiner do Azure (usa três variáveis de compilação definidas na guia **Variáveis**)
    - Definir a variável **DOCKER_HOST** para trabalhar com o ponto de extremidade Swarm (:2375)
    - Navegue até a pasta de *implantação* criada pela tarefa da cópia de segurança anterior e que contém o arquivo docker-compose.yml 
    - Execute os comandos `docker stack deploy` que recebem as novas imagens e criam os contêineres.

    >[!IMPORTANT]
    > Conforme mostrado na tela anterior, deixe a caixa de seleção **Falha no STDERR** desmarcada. Esta configuração nos permite concluir o processo de versão, pois o `docker-compose` imprime várias mensagens de diagnóstico, como os contêineres estão parando ou sendo excluídos, na saída de erro padrão. Se você marcar a caixa de seleção, o Visual Studio Team Services informará que ocorreram erros durante a versão, mesmo que tudo tenha corrido bem.
    >
3. Salve a nova definição da versão.

## <a name="step-4-test-the-cicd-pipeline"></a>Etapa 4: Testar o pipeline de CI/CD

Agora que você concluiu a configuração, é hora de testar esse novo pipeline de CI/CD. A maneira mais fácil de testá-lo é atualizar o código-fonte e confirmar as alterações no repositório GitHub. Alguns segundos depois de enviar o código, você verá uma nova compilação em execução no Visual Studio Team Services. Depois de concluído com êxito, uma nova versão será disparada e implantará a nova versão do aplicativo no cluster Serviço de Contêiner do Azure.

## <a name="next-steps"></a>Próximas etapas

* Para obter mais informações sobre a CI/CD com o Visual Studio Team Services, consulte a [Visão geral da Compilação do VSTS](https://www.visualstudio.com/docs/build/overview).
* Para saber mais sobre o Mecanismo do ACS, veja o [repositório do GitHub do Mecanismo do ACS](https://github.com/Azure/acs-engine).
* Para saber mais sobre o modo Docker Swarm, veja a [Visão geral do modo Docker Swarm](https://docs.docker.com/engine/swarm/).
