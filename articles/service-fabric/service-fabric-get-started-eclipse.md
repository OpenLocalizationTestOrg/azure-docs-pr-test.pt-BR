---
title: aaaAzure Service Fabric plug-in para Eclipse | Microsoft Docs
description: "Introdução ao Olá Service Fabric plug-in para Eclipse."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a>Plug-in do Service Fabric para o desenvolvimento de aplicativos Eclipse Java
Eclipse é uma saudação usada amplamente integrado (IDEs) ambientes de desenvolvimento para desenvolvedores de Java. Neste artigo, descreveremos como tooset a sua toowork de ambiente de desenvolvimento do Eclipse com o Azure Service Fabric. Saiba como tooinstall Olá Service Fabric plug-in, criar um aplicativo de malha do serviço e implantar seu cluster do Service Fabric application tooa local ou remoto do Service Fabric no Eclipse Neon.

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a>Instalar ou atualizar Olá plug-in Eclipse Neon do Service Fabric
Você pode instalar um plug-in do Service Fabric no Eclipse. Olá plug-in pode ajudar a simplificar o processo de saudação da criação e implantação dos serviços de Java.

1.  Verifique se você tem a versão mais recente de saudação do Eclipse Neon e a versão mais recente de saudação do Buildship (1.0.17 ou uma versão posterior) instalado:
    -   versões de saudação toocheck dos componentes instalados, no Eclipse Neon, ir muito**ajuda** > **detalhes da instalação**.
    -   tooupdate Buildship, consulte [Buildship Eclipse: Plug-ins do Eclipse para Gradle][buildship-update].
    -   toocheck para e instale atualizações para o Eclipse Neon, ir muito**ajuda** > **verificar se há atualizações**.

2.  Olá tooinstall Service Fabric plug-in no Eclipse Neon, ir muito**ajuda** > **instalar novo Software**.
  1.    Em Olá **trabalhar com** , digite **http://dl.microsoft.com/eclipse**.
  2.    Clique em **Adicionar**.

         ![Plug-in do Service Fabric para Eclipse Neon][sf-eclipse-plugin-install]
  3.    Selecione Olá Service Fabric plug-in e, em seguida, clique em **próximo**.
  4.    Conclua as etapas de instalação hello e aceite Olá Microsoft Software License Terms.

Se você já tiver Olá instalado plug-in do Service Fabric, certifique-se de que você tenha a versão mais recente do hello. toocheck atualizações disponíveis, vá muito**ajuda** > **detalhes da instalação**. Na lista de saudação de plug-ins instalados, selecione Serviço de malha e, em seguida, clique em **atualização**. As atualizações disponíveis serão instaladas.

> [!NOTE]
> Se instalar ou atualizar Olá plug-in do Service Fabric estiver lenta, pode ser devido a configuração do Eclipse tooan. Eclipse coleta metadados em todos os sites de tooupdate alterações que estão registrados com sua instância do Eclipse. toospeed processo Olá de verificar e instalar uma atualização de plug-in do Service Fabric, vá muito**locais disponíveis do Software**. Desmarque as caixas de seleção de Olá para todos os sites, exceto Olá que aponta local plug-in do Service Fabric do toohello (http://dl.microsoft.com/eclipse/azure/servicefabric).

## <a name="create-a-service-fabric-application-in-eclipse"></a>Criar um aplicativo do Service Fabric no Eclipse

1.  No Eclipse Neon, vá muito**arquivo** > **novo** > **outros**. Selecione **Projeto do Service Fabric** e clique em **Avançar**.

    ![Novo Projeto do Service Fabric página 1][create-application/p1]

2.  Insira um nome para o projeto e clique em **Avançar**.

    ![Novo Projeto do Service Fabric página 2][create-application/p2]

3.  Na lista de saudação de modelos, selecione **modelo de serviço**. Selecione o tipo de modelo de serviço (Ator, Sem Monitoração de Estado, Contêiner ou Convidado Binário) e clique em **Avançar**.

    ![Novo Projeto do Service Fabric página 3][create-application/p3]

4.  Insira o nome do serviço hello e detalhes de serviço e, em seguida, clique em **concluir**.

    ![Novo Projeto do Service Fabric página 4][create-application/p4]

5. Ao criar seu primeiro projeto de serviço de malha, no hello **abrir perspectiva associados** caixa de diálogo, clique em **Sim**.

    ![Novo Projeto do Service Fabric página 5][create-application/p5]

6.  O novo projeto tem esta aparência:

    ![Novo Projeto do Service Fabric página 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a>Criar e implantar um aplicativo do Service Fabric no Eclipse

1.  Clique com o botão direito do mouse no novo aplicativo do Service Fabric e selecione **Service Fabric**.

    ![Menu de atalho do Service Fabric][publish/RightClick]

2. No submenu hello, selecione a opção de saudação desejada:
    -   aplicativo de hello toobuild sem limpeza, clique em **criar aplicativo**.
    -   Clique em toodo uma compilação limpa de aplicativo hello, **recompilar o aplicativo**.
    -   aplicativo de hello tooclean de artefatos internos, clique em **aplicativo limpa**.

3.  Nesse menu, você também pode implantar, desimplantar e publicar o aplicativo:
    -   toodeploy tooyour o cluster local, clique em **implantar aplicativo**.
    -   Em Olá **publicar aplicativo** caixa de diálogo, selecione um perfil de publicação:
        -  **Local.json**
        -  **Cloud.json**

     Esses arquivos de notação JSON (JavaScript Object) armazenam informações (como pontos de extremidade de conexão e informações de segurança) que é necessário tooconnect tooyour local ou cluster de nuvem (Azure).

  ![Menu Publicar do Service Fabric][publish/Publish]

Uma maneira alternativa toodeploy seu aplicativo de malha do serviço está usando o Eclipse executar configurações.

  1.    Vá muito**executar** > **executar configurações**.
  2.    Em **Gradle projeto**, selecione Olá **ServiceFabricDeployer** configuração de execução.
  3.    No painel direito hello, em Olá **argumentos** guia, para **publishProfile**, selecione **local** ou **nuvem**.  saudação padrão é **local**. toodeploy tooa remoto ou cluster de nuvem, selecione **nuvem**.
  4.    tooensure que informações adequadas de saudação são populadas em Olá perfis de publicação, edite **Local.json** ou **Cloud.json** conforme necessário. Você pode adicionar ou atualizar detalhes de ponto de extremidade e credenciais de segurança.
  5.    Certifique-se de que **Working Directory** pontos toohello aplicativo deseja toodeploy. toochange Olá aplicativo, clique em Olá **espaço de trabalho** botão e, em seguida, selecione o aplicativo hello desejado.
  6.    Clique em **Aplicar** e em **Executar**.

Seu aplicativo será compilado e implantado em poucos instantes. Você pode monitorar o status da implantação Olá no Gerenciador do Service Fabric.  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a>Adicionar um serviço de malha do serviço tooyour aplicativo do Service Fabric

Olá tooadd um Service Fabric tooan existente do Service Fabric aplicativo de serviço, as etapas a seguir:

1.  Projeto de Olá atalho você deseja tooadd um serviço e, em seguida, clique em **Service Fabric**.

    ![Adicionar Serviço do Service Fabric Página 1][add-service/p1]

2.  Clique em **Adicionar serviço do Service Fabric**, e Olá completo conjunto de etapas tooadd um projeto de toohello de serviço.
3.  Modelo de serviço selecione Olá você deseja tooadd tooyour projeto e, em seguida, clique em **próximo**.

    ![Adicionar Serviço do Service Fabric Página 2][add-service/p2]

4.  Insira o nome do serviço de saudação (e outros detalhes, conforme necessário) e clique em Olá **Adicionar serviço** botão.  

    ![Adicionar Serviço do Service Fabric Página 3][add-service/p3]

5.  Depois que o serviço Olá é adicionado, a estrutura geral do projeto é semelhante toohello projeto a seguir:

    ![Adicionar Serviço do Service Fabric Página 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a>Editar versões de manifesto do aplicativo Java do Service Fabric

versões de manifesto tooedit, clique com o botão direito do mouse no projeto de Olá, vá muito**Service Fabric** e selecione **editar versões de manifesto...**  de saudação menu suspenso. No Assistente de saudação, você pode atualizar Olá versões de manifesto de aplicativo, serviço manifesto e Olá para **código**, **Config** e **dados** pacotes.

Se você marcar a opção de saudação **atualizar automaticamente o aplicativo e as versões de serviço** e, em seguida, uma versão de atualização, versões de manifesto Olá serão atualizadas automaticamente. toogive um exemplo, você primeiro selecionar caixa de seleção hello, em seguida, versão de saudação de atualização do **código** versão de 0.0.0 too0.0.1 e clique em **concluir**, versão do manifesto e o manifesto do aplicativo de serviço, em seguida, versão será too0.0.1 atualizadas automaticamente.

## <a name="upgrade-your-service-fabric-java-application"></a>Atualizar seu aplicativo Java do Service Fabric

Para um cenário de atualização, digamos que você criou Olá **App1** projeto usando Olá plug-in Eclipse do Service Fabric. Você implantá-lo usando toocreate plug-in Olá um aplicativo chamado **fabric: / App1Application**. tipo de aplicativo Hello **App1AppicationType**, e a versão do aplicativo hello é 1.0. Agora, você deseja tooupgrade seu aplicativo sem interromper a disponibilidade.

Primeiro, faça as alterações de aplicativo tooyour e, em seguida, Olá de reconstrução modificado serviço. Saudação de atualização modificado (ServiceManifest.xml) do arquivo de manifesto do serviço com versões Olá atualizado para serviço de saudação (e código, configuração ou dados, como relevante). Além disso, modifique o manifesto do aplicativo hello (ApplicationManifest.xml) com número de versão de hello atualizado para o aplicativo hello e Olá serviço modificado.  

tooupgrade seu aplicativo usando o Eclipse Neon, você pode criar um perfil de configuração de execução duplicada. Em seguida, use tooupgrade seu aplicativo conforme necessário.

1.  Vá muito**executar** > **executar configurações**. No painel esquerdo do hello, clique em Olá pequena seta toohello esquerda **Gradle projeto**.
2.  Clique com o botão direito do mouse em **ServiceFabricDeployer**e selecione **Duplicar**. Digite um novo nome para essa configuração, por exemplo, **ServiceFabricUpgrader**.
3.  No painel direito hello, em Olá **argumentos** , altere **- Pconfig = 'implantar'** muito**- Pconfig = 'Atualizar'**e, em seguida, clique em **aplicar**.

Esse processo cria e salva um perfil de configuração de execução você pode usar em qualquer tempo tooupgrade seu aplicativo. Ele também obtém última versão de tipo de aplicativo atualizado saudação do arquivo de manifesto de aplicativo hello.

atualização do aplicativo Hello leva alguns minutos. Você pode monitorar a atualização do aplicativo hello no Gerenciador do Service Fabric.

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Migrando toobe antigo de aplicativos Java de malha do serviço usado com o Maven
Podemos recentemente moveu bibliotecas Java de malha do serviço de repositório de tooMaven do Java SDK do Service Fabric. Enquanto você gerar usando o Eclipse, novos aplicativos de saudação gerará projetos atualizados mais recente (que serão capaz de toowork com o Maven), você pode atualizar sua malha de serviço existente sem monitoração de estado ou aplicativos Java de ator, que estavam usando Olá SDK de Java do Service Fabric versões anteriores, toouse Olá Java de malha do serviço dependências do Maven. Siga as etapas de saudação mencionadas [aqui](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure seu aplicativo mais antigo funciona com o Maven.

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
