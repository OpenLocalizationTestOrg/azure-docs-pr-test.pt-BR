---
title: aaaCI/CD de tooAzure Jenkins VMs com Team Services | Microsoft Docs
description: "Configurar a integração contínua (CI) e a implantação contínua (CD) de um aplicativo Node. js usando Jenkins tooAzure VMs do gerenciamento de versão no Visual Studio Team Services (VSTS) ou o Microsoft Team Foundation Server (TFS)"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a>Implantar seu aplicativo tooLinux VMs usando Jenkins e do Team Services

CI (integração contínua) e CD (implantação contínua) é um pipeline por meio do qual você pode compilar, lançar e implantar seu código. Team Services fornece um conjunto de ferramentas de automação de CI/CD completo, repleto para tooAzure de implantação. Jenkins é uma ferramenta de terceiros popular baseada em servidor de CI/CD que também fornece a automação de CI/CD. Você pode usar ambos os toocustomize juntos como entregar seu aplicativo na nuvem ou serviço.

Neste tutorial, você use Jenkins toobuild um **aplicativo web Node.js**e o Visual Studio Team Services toodeploy-tooa [grupo de implantação](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) que contém máquinas virtuais Linux.

Você vai:

> [!div class="checklist"]
> * Compilar seu aplicativo no Jenkins
> * Configurar o Jenkins para integração com o Team Services
> * Criar um grupo de implantação para Olá máquinas virtuais do Azure
> * Criar uma definição de lançamento que configura Olá VMs e implanta o aplicativo hello

## <a name="before-you-begin"></a>Antes de começar

* É necessário acesso tooa Jenkins conta. Se você ainda não tiver criado um servidor Jenkins, confira a [Documentação do Jenkins](https://jenkins.io/doc/). 

* Entrar na conta do Team Services do tooyour (`https://{youraccount}.visualstudio.com`). 
  Você pode obter uma [conta gratuita do Team Services](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).

  > [!NOTE]
  > Para obter mais informações, consulte [conectar os serviços de tooTeam](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).

* Crie um PAT (token de acesso pessoal) em sua conta do Team Services se você ainda não tiver um. Jenkins requer essa tooaccess informações sobre sua conta do Team Services.
  Leitura [como criar um token de acesso pessoal para Team Services e o TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn como toogenerate um.

## <a name="get-hello-sample-app"></a>Obter o aplicativo de exemplo hello

É necessário um toodeploy aplicativo armazenado em um repositório Git.
Para este tutorial, recomendamos o uso [deste aplicativo de exemplo disponível no GitHub](https://github.com/azooinmyluggage/fabrikam-node).

1. Crie uma bifurcação deste aplicativo e anote o local de saudação (URL) para uso em etapas posteriores deste tutorial.

1. Verifique a bifurcação de saudação **pública** toosimplify se tooGitHub mais tarde.

> [!NOTE]
> Para saber mais, confira [Criar bifurcação de um repositório](https://help.github.com/articles/fork-a-repo/) e [Transformar em público um repositório privado](https://help.github.com/articles/making-a-private-repository-public/).

> [!NOTE]
> Olá aplicativo foi criado usando [Yeoman](http://yeoman.io/learning/index.html); ele usa **Express**, **bower**, e **grunt**; e tem algumas **npm**pacotes como dependências.
> aplicativo de exemplo Hello contém um conjunto de [modelos do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) que são usada toodynamically criar máquinas virtuais de saudação para implantação no Azure. Esses modelos são usados por tarefas no hello [definição de versão do Team Services](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).
> modelo principal Olá cria um grupo de segurança de rede, uma máquina virtual e uma rede virtual. Ele atribui um endereço IP público e abre a porta 80 de entrada. Ele também adiciona uma marca que é usada pela implantação de saudação do hello implantação grupo Olá muito selecione máquinas tooreceive.
>
> exemplo Hello também contém um script que define o Nginx e implanta o aplicativo hello. Ele é executado em cada uma das máquinas virtuais de saudação. Especificamente, o script hello instala nó, Nginx e PM2; Configura Nginx e PM2; em seguida, inicia o aplicativo de nó de saudação.

## <a name="configure-jenkins-plugins"></a>Configurar os plug-ins do Jenkins

Primeiro, você deve configurar dois plug-ins Jenkins para **NodeJS** e **Integração com o Team Services**.

1. Abra sua conta do Jenkins e escolha **Gerenciar Jenkins**.

1. Em Olá **Jenkins gerenciar** escolha **gerenciar plug-ins**.

1. Filtro Olá lista toolocate Olá **NodeJS** plug-in e instalá-lo sem reinicialização.

   ![Adicionando Olá NodeJS plug-in tooJenkins](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. Filtro Olá lista toofind Olá **Team Foundation Server** plug-in e instalá-lo. (Esse plug-in funciona para Team Services e Team Foundation Server.) Não é necessário reiniciar o Jenkins.

## <a name="configure-jenkins-build-for-nodejs"></a>Configurar o build do Jenkins para Node.js

No Jenkins, crie um novo projeto de build e configure-o da seguinte maneira:

1. Em Olá **geral** , insira um nome para seu projeto de compilação.

1. Em Olá **código-fonte gerenciamento** guia, selecione **Git** e insira os detalhes de saudação do repositório de saudação e ramificação Olá que contém o código do aplicativo.

   ![Adicionar uma construção de tooyour do repositório](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > Se o repositório não é público, escolha **adicionar** e forneça credenciais tooconnect tooit.

1. Em Olá **criar gatilhos** guia, selecione **sondagem SCM** e digite Olá agendamento `H/03 * * * *` repositório do Git Olá toopoll para que as alterações a cada três minutos. 

1. Em Olá **ambiente de compilação** guia, selecione **fornecer nó &amp; npm bin / caminho da pasta** e digite `NodeJS` para Olá valor do nó JS instalação. Deixe o **arquivo npmrc** definido como "usar padrão do sistema".

1. Em Olá **criar** , insira o comando Olá `npm install` tooensure todas as dependências são atualizadas.

## <a name="configure-jenkins-for-team-services-integration"></a>Configurar o Jenkins para integração com o Team Services

1. Em Olá **ações de pós-compilação** guia, para **arquivos tooarchive**, digite `**/*` tooinclude todos os arquivos.

1. Para **disparar versão no TFS/Team Services**, digite a URL completa Olá da sua conta (como `https://your-account-name.visualstudio.com`), Olá nome do projeto, um nome para a definição de versão de saudação (criada posteriormente), e Olá credenciais tooconnect tooyour conta.
   É necessário o nome de usuário e a saudação PAT criado anteriormente. 

   ![Configuração de ações pós-build do Jenkins](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. Salve o projeto de compilação de saudação.

## <a name="create-a-jenkins-service-endpoint"></a>Criar um ponto de extremidade de serviço do Jenkins

Um ponto de extremidade de serviço permite Team Services tooconnect tooJenkins.

1. Olá abrir **serviços** página no Team Services, abra Olá **novo ponto de extremidade de serviço** lista e escolha **Jenkins**.

   ![Adicionar um ponto de extremidade do Jenkins](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. Insira um nome que você usará toorefer toothis conexão.

1. Insira a URL de saudação do servidor Jenkins e escala Olá **aceitar certificados não confiáveis do SSL** opção.

1. Digite hello nome de usuário e senha para sua conta Jenkins.

1. Escolha **verificar conexão** toocheck que Olá informação está correta.

1. Escolha **Okey** toocreate ponto de extremidade de serviço de saudação.

## <a name="create-a-deployment-group"></a>Criar um grupo de implantação

É necessário um [o grupo de implantação](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) muito contêm máquinas virtuais de saudação.

1. Olá abrir **versões** guia da saudação **criar &amp; versão** hub, em seguida, abra Olá **grupos de implantação** guia e escolha **+ novo**.

1. Insira um nome para o grupo de implantação hello e uma descrição opcional.
   Depois, escolha **Criar**.

tarefa de implantação de grupo de recursos do Azure Olá cria e registra VMs hello quando ele é executado usando o modelo do Azure Resource Manager hello.
Você não precisa toocreate e registrar máquinas virtuais de saudação por conta própria.

## <a name="create-a-release-definition"></a>Criar uma definição de versão

Uma definição de versão Especifica que o processo de saudação do Team Services será executado toodeploy Olá aplicativo.
definição de versão toocreate Olá no Team Services:

1. Olá abrir **versões** guia da saudação **criar &amp; versão** hub, abra Olá  **+**  suspensa na lista de saudação de definições de versão e escolha Olá **criar definição de versão**. 

1. Selecione Olá **vazio** modelo e escolha **próximo**.

1. Em Olá **artefatos** seção, clique em **vincular um artefato** e escolha **Jenkins**. Selecione sua conexão de ponto de extremidade de serviço do Jenkins. Em seguida, selecione o trabalho de origem Jenkins hello e escolha **criar**. 

1. Em Olá nova definição de versão, escolha **+ adicionar tarefas** e adicione um **implantação de grupo de recursos do Azure** ambiente de padrão de toohello de tarefas.

1. Escolha Olá suspensa toohello próxima seta **+ adicionar tarefas** link e adicionar uma definição de toohello de fase de grupo de implantação.

   ![Adicionar uma fase de grupo de implantação](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. No catálogo de tarefa hello, abra Olá **utilitário** seção e adicionar uma instância de saudação **Script do Shell** tarefa.

1. modelo de parâmetros de saudação usado na tarefa de implantação de grupo de recursos do Azure Olá define Olá administrador senha usada tooconnect toohello VMs.
   Fornecer essa senha com variável Olá **$(adminpassword)**:
   
   - Olá abrir **variáveis** guia e, em Olá **variáveis** seção, insira o nome da saudação `adminpassword`.

   - Insira a senha de administrador de saudação.

   - Escolha hello "cadeado" ícone próximo toohello valor textbox tooprotect Olá senha. 

## <a name="configure-hello-azure-resource-group-deployment-task"></a>Configurar tarefas de implantação de grupo de recursos do Azure Olá

Olá **implantação de grupo de recursos do Azure** tarefa é o grupo de implantação de saudação toocreate usado. Configure-o da seguinte maneira:

* **Assinatura do Azure:** selecione uma conexão na lista de saudação em **conexões de serviço do Azure disponíveis**. 
  Se nenhuma conexão aparecer, escolha **gerenciar**, selecione **novo ponto de extremidade de serviço** , em seguida, **do Azure Resource Manager**e siga os prompts de saudação.
  Retornar tooyour versão definição, Olá atualização **AzureRM assinatura** lista e conexão Olá selecione que você criou.

* **Grupo de recursos**: insira um nome de grupo de recursos de saudação criado anteriormente.

* **Local**: selecione uma região para a implantação de saudação.

  ![Criar um novo grupo de recursos](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* **Local do modelo**: `URL of hello file`

* **Link do modelo**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`

* **Link de parâmetros de modelo**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`

* **Substituir parâmetros de modelo**: uma lista de saudação substituem os valores, por exemplo: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.<br />Insira seus próprios valores específicos de Olá {espaços reservados}. 

* **Habilitar os pré-requisitos**: `Configure with Deployment Group agent`

* **Ponto de extremidade do TFS para o VSTS**: escolha **adicionar** e, no diálogo "Adicionar novo Team Foundation Server/Team Services Conexão" Olá, selecione **Token de autenticação com base em**. Insira um nome de conexão hello e URL de saudação do seu projeto de equipe. Em seguida, gerar e insira um [Token de acesso pessoal (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) o projeto de equipe do tooauthenticate Olá conexão tooyour.

  ![Criar um token de acesso pessoal](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* **Projeto de equipe**: selecione o projeto atual.

* **Grupo de implantação**: insira Olá o mesmo nome de grupo de implantação que você usou para Olá **grupo de recursos** parâmetro.

as configurações padrão de saudação para tarefas de implantação de grupo de recursos do Azure Olá são toocreate ou atualizar um recurso e toodo assim incrementalmente. tarefa de saudação cria Olá VMs Olá primeira vez que ele é executado e subsequentemente apenas atualizá-los.

## <a name="configure-hello-shell-script-task"></a>Configurar a tarefa de Script do Shell Olá

Olá **Script do Shell** tarefa é uma configuração de saudação do tooprovide usado para toorun um script no aplicativo de saudação cada servidor tooinstall Node. js e iniciar. Configure-o da seguinte maneira:

* **Caminho do Script**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`

* **Especificar Diretório de Trabalho**: `Checked`

* **Diretório de Trabalho**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`
   
## <a name="rename-and-save-hello-release-definition"></a>Renomear e salvar a definição de versão Olá

1. Editar nome Olá Olá versão toohello nome de definição de especificado no **ações de pós-compilação** guia de compilação Olá Jenkins. Jenkins requer esse nome toobe capaz de tootrigger uma nova versão quando artefatos de origem Olá são atualizados.

1. Opcionalmente, altere o nome de saudação do ambiente Olá clicando no nome da saudação. 

1. Escolha **Salvar** e depois **OK**.

## <a name="start-a-manual-deployment"></a>Iniciar uma implantação manual

1. Escolha **+ Versão** e selecione **Criar Versão**.

1. Selecione a compilação Olá é concluída na lista suspensa da realçado hello e escolha **criar**.

1. Escolha o link de versão de saudação na mensagem de saudação do pop-up. Por exemplo: "A versão **Release-1** foi criada".

1. Olá abrir **Logs** guia saída de console toowatch hello versão.

1. No navegador, abra Olá URL de um dos servidores de saudação você adicionou o grupo de implantação tooyour. Por exemplo, insira: `http://{your-server-ip-address}`

## <a name="start-a-cicd-deployment"></a>Iniciar uma implantação de CI/CD

1. Em Olá versão definição, desmarque Olá **habilitado** caixa de seleção no hello **opções de controle** seção de configurações de saudação para tarefas de implantação de grupo de recursos do Azure hello.
   Para o grupo de implantação existente toohello de implantações futuras, você não precisa toore-executar essa tarefa.

1. Vá toohello repositório do Git de origem e modificar o conteúdo de saudação do hello **h1** no arquivo hello [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).

1. Confirme a alteração.

1. Depois de alguns minutos, você verá uma nova versão criada no hello **versões** página do Team Services ou o TFS. Abra a implantação de Olá Olá versão toosee ocorrendo. Parabéns!

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você Olá a implantação automatizada de um tooAzure de aplicativo usando compilação Jenkins e Team Services para versão. Você aprendeu como:

> [!div class="checklist"]
> * Compilar seu aplicativo no Jenkins
> * Configurar o Jenkins para integração com o Team Services
> * Criar um grupo de implantação para Olá máquinas virtuais do Azure
> * Criar uma definição de lançamento que configura Olá VMs e implanta o aplicativo hello

Mais informações sobre como toodeploy uma LÂMPADA (Linux, Apache, MySQL e PHP) de pilha avança toohello toolearn de tutorial Avançar.

> [!div class="nextstepaction"]
> [Implantar a pilha LAMP](tutorial-lamp-stack.md)