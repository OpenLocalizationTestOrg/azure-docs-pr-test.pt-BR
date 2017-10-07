---
title: "aaaCI/CD com o mecanismo do serviço de contêiner do Azure e o modo Swarm | Microsoft Docs"
description: "Usar o mecanismo do serviço de contêiner do Azure com o Docker Swarm modo, um registro de contêiner do Azure e o Visual Studio Team Services toodeliver continuamente um aplicativo do .NET Core multi-contêiner"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: "Docker, Contêineres, Microsserviços, Swarm, Azure, Visual Studio Team Services, DevOps, Mecanismo do ACS"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a>CI/CD completo pipeline toodeploy um aplicativo de multi-contêiner no serviço de contêiner do Azure com o mecanismo do ACS e o modo de Swarm de Docker usando o Visual Studio Team Services

*Este artigo se baseia em [CI/CD completo pipeline toodeploy um aplicativo de multi-contêiner no serviço de contêiner do Azure com o Docker Swarm usando o Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentação*

Hoje em dia, um dos Olá maiores desafios ao desenvolvimento de aplicativos modernos para nuvem hello está sendo toodeliver capaz desses aplicativos continuamente. Neste artigo, você aprenderá como tooimplement uma integração completa contínua e implantação (CI/CD) pipeline usando: 
* Mecanismo do Serviço de Contêiner do Azure com o modo Docker Swarm
* Registro de Contêiner do Azure
* Visual Studio Team Services

Este artigo se baseia em um aplicativo simples, disponível no [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), desenvolvido com o ASP.NET Core. aplicativo Hello é composto de quatro diferentes serviços: três web APIs e um web front-end:

![Aplicativo de exemplo MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

o objetivo de saudação é toodeliver este aplicativo continuamente em um cluster de Docker Swarm modo, usando o Visual Studio Team Services. a figura de saudação a seguir detalhes esse pipeline entrega contínua:

![Aplicativo de exemplo MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

Aqui está uma breve explicação das etapas de saudação:

1. Alterações de código são o repositório de código fonte toohello confirmada (aqui, GitHub) 
2. O GitHub dispara uma compilação no Visual Studio Team Services 
3. Visual Studio Team Services obtém a versão mais recente de saudação do fontes hello e cria todas as imagens de saudação que compõem o aplicativo hello 
4. Visual Studio Team Services envia cada registro da imagem tooa Docker criado usando o serviço de registro de contêiner do Azure Olá 
5. O Visual Studio Team Services dispara uma nova versão 
6. versão Olá executa alguns comandos usando o SSH no nó do contêiner do Azure serviço cluster mestre Olá 
7. Modo de docker Swarm no cluster Olá extrai versão mais recente de saudação de imagens de saudação 
8. Olá nova versão do aplicativo hello é implantada usando a pilha de Docker 

## <a name="prerequisites"></a>Pré-requisitos

Antes de iniciar este tutorial, você precisa toocomplete Olá tarefas a seguir:

- [Criar um cluster no modo Swarm no Serviço de Contêiner do Azure com o Mecanismo do ACS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [Conecte-se com o cluster de por nuvem Olá no serviço de contêiner do Azure](../container-service-connect.md)
- [Criar um registro de contêiner do Azure](../../container-registry/container-registry-get-started-portal.md)
- [Ter uma conta do Visual Studio Team Services e projeto de equipe criados](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Bifurcação Olá GitHub repositório tooyour conta do GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> o orchestrator Docker Swarm Olá no serviço de contêiner do Azure usa autônomo herdado por nuvem. Atualmente, a saudação integrado [por nuvem modo](https://docs.docker.com/engine/swarm/) (no Docker 1.12 e superior) não é um orquestrador com suporte no serviço de contêiner do Azure. Por esse motivo, estamos usando [ACS mecanismo](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), um contribuído pela comunidade [quickstart modelo](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), ou uma solução de Docker em Olá [Azure Marketplace](https://azuremarketplace.microsoft.com).
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>Etapa 1: Configurar sua conta do Visual Studio Team Services 

Nesta seção, você configura sua conta do Visual Studio Team Services. tooconfigure VSTS serviços pontos de extremidade, no seu projeto do Visual Studio Team Services, clique em Olá **configurações** ícone na barra de ferramentas hello e selecione **serviços**.

![Abra o Ponto de extremidade de serviço](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a>Conectar o Visual Studio Team Services e a conta o Azure

Configure uma conexão entre seu projeto do VSTS e sua conta do Azure.

1. Olá esquerda, clique em **novo ponto de extremidade de serviço** > **do Azure Resource Manager**.
2. tooauthorize VSTS toowork com sua conta do Azure, selecione seu **assinatura** e clique em **Okey**.

    ![Visual Studio Team Services – Autorizar Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a>Conectar o Visual Studio Team Services e o GitHub

Configure uma conexão entre seu projeto VSTS e sua conta GitHub.

1. Olá esquerda, clique em **novo ponto de extremidade de serviço** > **GitHub**.
2. tooauthorize VSTS toowork com sua conta do GitHub, clique em **autorizar** e siga o procedimento Olá na janela de saudação que é aberta.

    ![Visual Studio Team Services - Autorizar GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a>Conecte-se o cluster do VSTS tooyour serviço de contêiner do Azure

últimas etapas Olá antes de entrar no pipeline de CI/CD Olá são tooconfigure conexões externas tooyour Docker Swarm cluster do Azure. 

1. Para o cluster Docker Swarm hello, adicione um ponto de extremidade do tipo **SSH**. Em seguida, insira informações de conexão SSH saudação do cluster por nuvem (nó mestre).

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

Todas as configurações de saudação é feito agora. Próximas etapas de Olá, você criará um pipeline de CI/CD Olá que compila e implanta Olá aplicativo toohello Docker Swarm. 

## <a name="step-2-create-hello-build-definition"></a>Etapa 2: Criar a definição de compilação Olá

Nesta etapa, você pode configurar uma definição de compilação para o seu projeto do VSTS e define o fluxo de trabalho de compilação de saudação para as imagens de contêiner

### <a name="initial-definition-setup"></a>Configuração da definição inicial

1. toocreate uma definição de compilação, conecte-se tooyour do Visual Studio Team Services do projeto e clique em **Build e versão**. Em Olá **definições de compilação** seção, clique em **+ novo**. 

    ![Visual Studio Team Services - Nova Definição da Compilação](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. Selecione Olá **vazio processo**.

    ![Visual Studio Team Services – Nova Definição de Compilação Vazia](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. Em seguida, clique em Olá **variáveis** guia e crie duas novas variáveis: **RegistryURL** e **AgentURL**. Colar valores de saudação do registro e DNS de agentes do Cluster.

    ![Visual Studio Team Services – Configuração de Variáveis de Compilação](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. Em Olá **definições de compilação** page, abra Olá **gatilhos** guia e configurar a integração contínua da saudação compilação toouse com bifurcação de saudação do projeto de MyShop Olá que você criou nos pré-requisitos Olá. Em seguida, selecione **Alterações em lote**. Certifique-se de que você selecione *docker linux* como Olá **Branch especificação**.

    ![Visual Studio Team Services - Configuração do Repositório de Compilação](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. Por fim, clique em Olá **opções** guia e configurar a fila de agente padrão Olá muito**hospedado Linux visualização**.

    ![Visual Studio Team Services – Configuração do Agente de Host](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a>Definir o fluxo de trabalho de compilação de saudação
as próximas etapas Olá definem o fluxo de trabalho de compilação de saudação. Primeiro, é necessário tooconfigure fonte de saudação do código de saudação. toodo-la, marque **GitHub** e **repositório** e **ramificação** (docker-linux).

![Visual Studio Team Services – Configurar o código-fonte](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

Há cinco toobuild de imagens de contêiner para Olá *MyShop* aplicativo. Cada imagem é criada usando Olá que dockerfile localizado em pastas de projeto hello:

* ProductsApi
* Proxy
* RatingsApi
* RecommendationsApi
* ShopFront

Você precisa de duas etapas de Docker para cada imagem, uma imagem de saudação toobuild e uma imagem de saudação toopush no registro do contêiner do Azure hello. 

1. Clique em tooadd uma etapa no fluxo de trabalho de compilação hello, **+ adicionar a etapa de compilação** e selecione **Docker**.

    ![Visual Studio Team Services - Adicionar Etapas da Compilação](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. Para cada imagem, configure uma etapa que usa Olá `docker build` comando.

    ![Visual Studio Team Services - Compilação do Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    Operação de criação para hello, selecione o registro de contêiner do Azure, hello **criar uma imagem** ação e Olá Dockerfile que define cada imagem. Olá conjunto **diretório de trabalho** como diretório de raiz de Dockerfile hello, definir Olá **nome da imagem**e selecione **incluir mais recente marca**.
    
    Olá, nome da imagem tem toobe neste formato: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```. Substituir **[nome]** com o nome da imagem hello:
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. Para cada imagem, configurar uma segunda etapa que usa Olá `docker push` comando.

    ![Visual Studio Team Services - Envio do Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    Para a operação de envio por push hello, selecione o registro de contêiner do Azure, hello **enviar por Push uma imagem** ação, digite Olá **nome da imagem** que é criado na etapa anterior hello e selecione **incluem marca mais recente **.

4. Depois de configurar o build hello e enviar por push as etapas para cada uma das imagens de cinco hello, adicione que três etapas mais Olá criar fluxo de trabalho.

   ![Visual Studio Team Services – Adicionar Tarefa de Linha de Comando](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. Uma tarefa de linha de comando que usa uma saudação do bash script tooreplace *RegistryURL* ocorrência no arquivo de docker compose.yml Olá com variável de RegistryURL hello. 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services – Atualizar arquivo de composição com a URL do Registro](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. Uma tarefa de linha de comando que usa uma saudação do bash script tooreplace *AgentURL* ocorrência no arquivo de docker compose.yml Olá com variável de AgentURL hello.
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. Uma tarefa que descarta Olá atualizou o arquivo de composição como um artefato de compilação para que ele pode ser usado na versão de saudação. Consulte Olá após a tela para obter detalhes.

         ![Visual Studio Team Services – Publicar Artefato](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - Publicar arquivo de composição](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. Clique em **Salvar & fila** tootest sua definição de compilação.

   ![Visual Studio Team Services – Salvar e enfileirar](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services – Nova Fila](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. Se hello **criar** está correto, você tem toosee esta tela:

  ![Visual Studio Team Services – Compilação bem-sucedida](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a>Etapa 3: Criar a definição de versão Olá

Visual Studio Team Services permite que você muito[gerenciar versões em ambientes](https://www.visualstudio.com/team-services/release-management/). Você pode habilitar a implantação contínua toomake-se de que seu aplicativo é implantado em seus ambientes diferentes (como desenvolvimento, teste, pré-produção e produção) de forma suave. Você pode criar um ambiente que representa seu cluster do Serviço de Contêiner do Azure no modo Docker Swarm.

![Visual Studio Team Services - versão tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Configuração da versão inicial

1. toocreate uma definição de versão, clique em **versões** > **+ versão**

2. fonte de artefato Olá tooconfigure, clique em **artefatos** > **vincular a uma fonte de artefato**. Vincule aqui, esta nova compilação de toohello de definição de versão definido na etapa anterior hello. Depois disso, o arquivo de docker compose.yml de saudação está disponível no processo de liberação de saudação.

    ![Visual Studio Team Services - Artefatos da Versão](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. gatilho de versão de hello tooconfigure, clique em **gatilhos** e selecione **implantação contínua**. Gatilho de saudação do conjunto em Olá mesma fonte de artefato. Essa configuração garante que uma nova versão inicia quando a compilação de saudação for concluído com êxito.

    ![Visual Studio Team Services - Gatilhos da Versão](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. Clique em variáveis de versão do tooconfigure Olá, **variáveis** e selecione **+ variável** toocreate três novas variáveis com informações de saudação do registro Olá: **docker.username**, **docker.password**, e **docker.registry**. Colar valores de saudação do registro e DNS de agentes do Cluster.

    ![Visual Studio Team Services - Configuração do Repositório de Compilação](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > Conforme mostrado na tela anterior hello, clique em Olá **bloqueio** caixa de seleção no docker.password. Essa configuração é a senha de saudação do toorestrict importantes.
    >

### <a name="define-hello-release-workflow"></a>Definir o fluxo de trabalho do hello versão

fluxo de trabalho de versão de saudação é composto de duas tarefas que você adicionar.

1. Configurar uma saudação de cópia de toosecurely tarefa compor arquivo tooa *implantar* pasta Olá Docker Swarm nó mestre, usando a conexão SSH de saudação foi configurado anteriormente. Consulte Olá após a tela para obter detalhes.
    
    Pasta de origem: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```

    ![Visual Studio Team Services - SCP da Versão](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. Configurar uma segunda tooexecute de tarefa um toorun de comando bash `docker` e `docker stack deploy` comandos no nó mestre hello. Consulte Olá após a tela para obter detalhes.

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services - Bash da Versão](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    comando Olá executado no mestre de saudação usa hello CLI do Docker e Olá Olá de toodo de CLI do Docker Compose tarefas a seguir:

    - Faça logon no registro de contêiner do Azure toohello (ele usa três variáveis de compilação que são definidas em Olá **variáveis** guia)
    - Definir Olá **DOCKER_HOST** toowork variável com o ponto de extremidade do hello por nuvem (: 2375)
    - Navegue toohello *implantar* pasta que foi criado por Olá anterior a tarefa de cópia seguro e que contém o arquivo de docker compose.yml Olá 
    - Executar `docker stack deploy` comandos pull novas imagens de saudação e criar contêineres de saudação.

    >[!IMPORTANT]
    > Conforme mostrado na tela anterior hello, deixe Olá **falhar em STDERR** caixa de seleção está desmarcada. Essa configuração permite que nós toocomplete Olá versão processo devido muito`docker-compose` imprime várias mensagens de diagnósticas, como contêineres de interrupção ou excluído, na saída de erro padrão de saudação. Se você marcar a caixa de seleção hello, Visual Studio Team Services informa que ocorreram erros durante a versão de hello, mesmo se tudo correr bem.
    >
3. Salve a nova definição da versão.

## <a name="step-4-test-hello-cicd-pipeline"></a>Etapa 4: Testar o pipeline de CI/CD Olá

Agora que você concluir configuração Olá, é hora tootest esse novo pipeline de CI/CD. Olá tootest de maneira mais fácil é tooupdate Olá Olá de código e a confirmação do código-fonte é alterado para o repositório do GitHub. Alguns segundos depois que você enviar por push código hello, você verá uma nova compilação em execução no Visual Studio Team Services. Depois de concluído com êxito, uma nova versão é disparada e implantado a nova versão saudação do aplicativo hello no cluster do serviço de contêiner do Azure hello.

## <a name="next-steps"></a>Próximas etapas

* Para obter mais informações sobre CI/CD com o Visual Studio Team Services, consulte Olá [visão geral do VSTS criar](https://www.visualstudio.com/docs/build/overview).
* Para obter mais informações sobre o mecanismo do ACS, consulte Olá [repositório GitHub do mecanismo de ACS](https://github.com/Azure/acs-engine).
* Para obter mais informações sobre o modo de Docker Swarm, consulte Olá [Docker Swarm visão geral do modo](https://docs.docker.com/engine/swarm/).
