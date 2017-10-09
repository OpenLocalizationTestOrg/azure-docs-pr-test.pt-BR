---
title: "aaaCI/CD com o serviço de contêiner do Azure e por nuvem | Microsoft Docs"
description: "Usar serviço de contêiner do Azure com o Docker Swarm, um registro de contêiner do Azure e do Visual Studio Team Services toodeliver continuamente um aplicativo do .NET Core vários contêiner"
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Swarm, Azure, Visual Studio Team Services, DevOps"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a>CI/CD completo pipeline toodeploy um aplicativo de multi-contêiner no serviço de contêiner do Azure com o Docker Swarm usando o Visual Studio Team Services

Um dos Olá maiores desafios ao desenvolvimento de aplicativos modernos para nuvem hello está sendo toodeliver capaz desses aplicativos continuamente. Neste artigo, saiba como criar a tooimplement uma integração contínua total e pipeline de implantação (CI/CD) usando o serviço de contêiner do Azure com o Docker Swarm, o registro de contêiner do Azure e o Visual Studio Team Services e gerenciamento de liberações.

Este artigo se baseia em um aplicativo simples, disponível no [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), desenvolvido com o ASP.NET Core. aplicativo Hello é composto de quatro diferentes serviços: três web APIs e um web front-end:

![Aplicativo de exemplo MyShop](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

o objetivo de saudação é toodeliver esse aplicativo continuamente em um cluster de Docker Swarm, usando o Visual Studio Team Services. a figura de saudação a seguir detalhes esse pipeline entrega contínua:

![Aplicativo de exemplo MyShop](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

Aqui está uma breve explicação das etapas de saudação:

1. Alterações de código são o repositório de código fonte toohello confirmada (aqui, GitHub) 
2. O GitHub dispara uma compilação no Visual Studio Team Services 
3. Visual Studio Team Services obtém a versão mais recente de saudação do fontes hello e cria todas as imagens de saudação que compõem o aplicativo hello 
4. Visual Studio Team Services envia cada registro da imagem tooa Docker criado usando o serviço de registro de contêiner do Azure Olá 
5. O Visual Studio Team Services dispara uma nova versão 
6. versão Olá executa alguns comandos usando o SSH no nó do contêiner do Azure serviço cluster mestre Olá 
7. Por nuvem de docker Olá cluster recebe Olá versão mais recente das imagens de saudação 
8. Olá nova versão do aplicativo hello é implantada usando o Docker Compose 

## <a name="prerequisites"></a>Pré-requisitos

Antes de iniciar este tutorial, você precisa toocomplete Olá tarefas a seguir:

- [Criar um Cluster Swarm no Serviço de Contêiner do Azure](container-service-deployment.md)
- [Conecte-se com o cluster de por nuvem Olá no serviço de contêiner do Azure](../container-service-connect.md)
- [Criar um registro de contêiner do Azure](../../container-registry/container-registry-get-started-portal.md)
- [Ter uma conta do Visual Studio Team Services e projeto de equipe criados](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Bifurcação Olá GitHub repositório tooyour conta do GitHub](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Você também precisa de um computador Ubuntu (14.04 ou 16.04) com o Docker instalado. Este computador é usado pelo Visual Studio Team Services durante a saudação de compilação e processos de versão. Uma maneira toocreate essa máquina é imagem de saudação toouse disponível no hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/). 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>Etapa 1: Configurar sua conta do Visual Studio Team Services 

Nesta seção, você configura sua conta do Visual Studio Team Services.

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a>Configurar um agente de compilação Linux do Visual Studio Team Services

imagens do Docker toocreate e enviar por push que criar essas imagens em um registro de contêiner do Azure do Visual Studio Team Services, você precisa tooregister um agente do Linux. Você tem estas opções de instalação:

* [Implantar um agente no Linux](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [Use o Docker toorun Olá VSTS agent](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a>Instalar a extensão de Docker integração VSTS Olá

A Microsoft fornece uma extensão VSTS toowork com o Docker na compilação e processos de versão. Essa extensão está disponível em Olá [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker). Clique em **instalar** tooadd essa conta do VSTS de tooyour extensão:

![Instalar Olá integração de Docker](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

Conta VSTS tooyour tooconnect usando suas credenciais serão solicitadas. 

### <a name="connect-visual-studio-team-services-and-github"></a>Conectar o Visual Studio Team Services e o GitHub

Configure uma conexão entre seu projeto VSTS e sua conta GitHub.

1. No seu projeto do Visual Studio Team Services, clique em Olá **configurações** ícone na barra de ferramentas hello e selecione **serviços**.

    ![Visual Studio Team Services - Conexão Externa](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. Olá esquerda, clique em **novo ponto de extremidade de serviço** > **GitHub**.

    ![Visual Studio Team Services - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. tooauthorize VSTS toowork com sua conta do GitHub, clique em **autorizar** e siga o procedimento Olá na janela de saudação que é aberta.

    ![Visual Studio Team Services - Autorizar GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a>Conecte-se o registro do VSTS tooyour contêiner do Azure e o cluster do serviço de contêiner do Azure

últimas etapas Olá antes de entrar no pipeline de CI/CD Olá são registro de contêiner de tooyour tooconfigure conexões externas e o cluster Docker Swarm no Azure. 

1. Em Olá **serviços** configurações do seu projeto do Visual Studio Team Services, adicione um ponto de extremidade de serviço do tipo **Docker registro**. 

2. No hello pop-up que é aberta, digite o URL de hello e credenciais de saudação do registro do contêiner do Azure.

    ![Visual Studio Team Services - Registro do Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. Para o cluster Docker Swarm hello, adicione um ponto de extremidade do tipo **SSH**. Em seguida, insira informações de conexão SSH saudação do cluster por nuvem.

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

Todas as configurações de saudação é feito agora. Próximas etapas de Olá, você criará um pipeline de CI/CD Olá que compila e implanta Olá aplicativo toohello Docker Swarm. 

## <a name="step-2-create-hello-build-definition"></a>Etapa 2: Criar a definição de compilação Olá

Nesta etapa, você configurar seu projeto VSTS definitionfor uma compilação e define o fluxo de trabalho de compilação de saudação para as imagens de contêiner

### <a name="initial-definition-setup"></a>Configuração da definição inicial

1. toocreate uma definição de compilação, conecte-se tooyour do Visual Studio Team Services do projeto e clique em **Build e versão**. 

2. Em Olá **definições de compilação** seção, clique em **+ novo**. Selecione Olá **vazio** modelo.

    ![Visual Studio Team Services - Nova Definição da Compilação](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. Configurar nova compilação do hello com uma fonte de repositório do GitHub, seleção **integração contínua**e a fila de agente hello selecione onde você registrou seu agente do Linux. Clique em **criar** toocreate Olá definição de compilação.

    ![Visual Studio Team Services - Criar Definição da Compilação](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. Em Olá **definições de compilação** página, primeiro abra Olá **repositório** guia e configurar a bifurcação de saudação de toouse Olá compilação do projeto de MyShop Olá que você criou nos pré-requisitos Olá. Certifique-se de que você selecione *acs documentos* como Olá **branch padrão**.

    ![Visual Studio Team Services - Configuração do Repositório de Compilação](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. Em Olá **gatilhos** guia, defina Olá compilação toobe acionado após cada confirmação. Selecione **Integração contínua** e **Alterações de lote**.

    ![Visual Studio Team Services - Configuração do Gatilho de Compilação](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a>Definir o fluxo de trabalho de compilação de saudação
as próximas etapas Olá definem o fluxo de trabalho de compilação de saudação. Há cinco toobuild de imagens de contêiner para Olá *MyShop* aplicativo. Cada imagem é criada usando Olá que dockerfile localizado em pastas de projeto hello:

* ProductsApi
* Proxy
* RatingsApi
* RecommendationsApi
* ShopFront

Você precisa de duas etapas de Docker tooadd de cada imagem, uma imagem de saudação toobuild e uma imagem de saudação toopush no registro do contêiner do Azure hello. 

1. Clique em tooadd uma etapa no fluxo de trabalho de compilação hello, **+ adicionar a etapa de compilação** e selecione **Docker**.

    ![Visual Studio Team Services - Adicionar Etapas da Compilação](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. Para cada imagem, configure uma etapa que usa Olá `docker build` comando.

    ![Visual Studio Team Services - Compilação do Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    Operação de criação para hello, selecione o registro de contêiner do Azure, hello **criar uma imagem** ação e Olá Dockerfile que define cada imagem. Saudação de conjunto **contexto de compilação** como Olá Dockerfile diretório raiz e definir Olá **nome da imagem**. 
    
    Conforme mostrado no hello antes da tela, inicie o nome de imagem de Olá com hello URI do registro do contêiner do Azure. (Você também pode usar uma marca de saudação tooparameterize variável build de imagem de hello, como o identificador de compilação Olá neste exemplo).

3. Para cada imagem, configurar uma segunda etapa que usa Olá `docker push` comando.

    ![Visual Studio Team Services - Envio do Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    Para a operação de envio por push hello, selecione o registro de contêiner do Azure, hello **enviar por Push uma imagem** ação e digite Olá **nome da imagem** que é criado na etapa anterior hello.

4. Depois de configurar o build hello e enviar por push as etapas para cada uma das imagens de cinco hello, adicione que mais duas etapas no hello criar fluxo de trabalho.

    a. Uma tarefa de linha de comando que usa uma saudação do bash script tooreplace *BuildNumber* ocorrência no arquivo de docker compose.yml Olá com hello atual criar ID. Consulte Olá após a tela para obter detalhes.

    ![Visual Studio Team Services - Atualizar arquivo de composição](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    b. Uma tarefa que descarta Olá atualizou o arquivo de composição como um artefato de compilação para que ele pode ser usado na versão de saudação. Consulte Olá após a tela para obter detalhes.

    ![Visual Studio Team Services - Publicar arquivo de composição](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. Clique em **Salvar** e nomeie sua definição de compilação.

## <a name="step-3-create-hello-release-definition"></a>Etapa 3: Criar a definição de versão Olá

Visual Studio Team Services permite que você muito[gerenciar versões em ambientes](https://www.visualstudio.com/team-services/release-management/). Você pode habilitar a implantação contínua toomake-se de que seu aplicativo é implantado em seus ambientes diferentes (como desenvolvimento, teste, pré-produção e produção) de forma suave. Você pode criar um novo ambiente que representa o cluster Docker Swarm do Serviço de Contêiner do Azure.

![Visual Studio Team Services - versão tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Configuração da versão inicial

1. toocreate uma definição de versão, clique em **versões** > **+ versão**

2. fonte de artefato Olá tooconfigure, clique em **artefatos** > **vincular a uma fonte de artefato**. Vincule aqui, esta nova compilação de toohello de definição de versão definido na etapa anterior hello. Ao fazer isso, o arquivo de docker compose.yml de saudação está disponível no processo de liberação de saudação.

    ![Visual Studio Team Services - Artefatos da Versão](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. gatilho de versão de hello tooconfigure, clique em **gatilhos** e selecione **implantação contínua**. Gatilho de saudação do conjunto em Olá mesma fonte de artefato. Essa configuração garante que uma nova versão começa assim que a compilação de saudação for concluído com êxito.

    ![Visual Studio Team Services - Gatilhos da Versão](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a>Definir o fluxo de trabalho do hello versão

fluxo de trabalho de versão de saudação é composto de duas tarefas que você adicionar.

1. Configurar uma saudação de cópia de toosecurely tarefa compor arquivo tooa *implantar* pasta Olá Docker Swarm nó mestre, usando a conexão SSH de saudação foi configurado anteriormente. Consulte Olá após a tela para obter detalhes.

    ![Visual Studio Team Services - SCP da Versão](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. Configurar uma segunda tooexecute de tarefa um toorun de comando bash `docker` e `docker-compose` comandos no nó mestre hello. Consulte Olá após a tela para obter detalhes.

    ![Visual Studio Team Services - Bash da Versão](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    comando Olá executado em Olá use mestre Olá CLI do Docker e Olá Olá de toodo de CLI do Docker Compose tarefas a seguir:

    - Registro de contêiner do Azure toohello login (ele usa três variab'les de compilação que são definidos em Olá **variáveis** guia)
    - Definir Olá **DOCKER_HOST** toowork variável com o ponto de extremidade do hello por nuvem (: 2375)
    - Navegue toohello *implantar* pasta que foi criado por Olá anterior a tarefa de cópia seguro e que contém o arquivo de docker compose.yml Olá 
    - Executar `docker-compose` comandos pull novas imagens de Olá, interromper serviços hello, remover serviços hello e criar contêineres de saudação.

    >[!IMPORTANT]
    > Conforme mostrado no hello antes da tela, deixe Olá **falhar em STDERR** caixa de seleção está desmarcada. Esta é uma configuração importante, porque `docker-compose` imprime várias mensagens de diagnósticas, como contêineres de interrupção ou excluído, na saída de erro padrão de saudação. Se você marcar a caixa de seleção hello, Visual Studio Team Services informa que ocorreram erros durante a versão de hello, mesmo se tudo correr bem.
    >
3. Salve a nova definição da versão.


>[!NOTE]
>Essa implantação inclui algum tempo de inatividade porque estamos Parando serviços antigo hello e executando Olá um novo. Ele é possível tooavoid isso fazendo uma implantação de verde e azul.
>

## <a name="step-4-test-hello-cicd-pipeline"></a>Etapa 4. Pipeline de CI/CD de saudação do teste

Agora que você concluir configuração Olá, é hora tootest esse novo pipeline de CI/CD. Olá tootest de maneira mais fácil é tooupdate Olá Olá de código e a confirmação do código-fonte é alterado para o repositório do GitHub. Alguns segundos depois que você enviar por push código hello, você verá uma nova compilação em execução no Visual Studio Team Services. Depois de concluído com êxito, uma nova versão será disparada e implantará a nova versão saudação do aplicativo hello no cluster do serviço de contêiner do Azure hello.

## <a name="next-steps"></a>Próximas etapas

* Para obter mais informações sobre CI/CD com o Visual Studio Team Services, consulte Olá [visão geral do VSTS criar](https://www.visualstudio.com/docs/build/overview).
