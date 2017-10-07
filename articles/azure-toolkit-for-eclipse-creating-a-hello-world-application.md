---
title: "aaaCreate um Hello World serviço de nuvem do Azure no Eclipse"
description: "Saiba como toocreate um aplicativo Hello World simples usando Olá Kit de ferramentas do Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 7262e705-59d6-43ce-b888-29a21c8e0cb7
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: dfb81374aaf78e933c0bf83a1dbd98023801491a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-hello-world-cloud-service-for-azure-in-eclipse"></a>Criar um Serviço de Nuvem Hello World para o Azure no Eclipse
Olá etapas a seguir mostram como toocreate e implantar um tooAzure de aplicativo básico do JSP usando Olá Kit de ferramentas do Azure para Eclipse. Um exemplo de JSP é exibido para manter a simplicidade, mas etapas muito semelhantes podem ser apropriadas para um servlet Java quando o assunto é a implantação do Azure.

aplicativo Hello terá aparência a seguir toohello semelhante:

![][ic600360]

## <a name="prerequisites"></a>Pré-requisitos
* Um JDK (Java Developer Kit) versão 1.7 ou posterior.
* Um IDE do Eclipse para desenvolvedores do Java EE, Indigo ou posterior. Isso pode ser baixado em <http://www.eclipse.org/downloads/>.
* Uma distribuição de um servidor Web baseado em Java ou servidor de aplicativo, como o Apache Tomcat, o GlassFish, o JBoss Application Server, o Jetty ou o IBM® WebSphere® Application Server Liberty Core
* Uma assinatura do Azure, que pode ser adquirida em <http://azure.microsoft.com/pricing/purchase-options/>.
* saudação do Kit de ferramentas do Azure para Eclipse. Para obter mais informações, consulte [Olá instalando o Kit de ferramentas do Azure para Eclipse][Installing hello Azure Toolkit for Eclipse].

## <a name="toocreate-a-hello-world-application"></a>toocreate um aplicativo Hello World
Primeiro, vamos começar com a criação de um projeto Java.

1. Inicie o Eclipse e no menu de saudação clique **arquivo**, clique em **novo**e, em seguida, clique em **projeto Web dinâmico**. (Se você não vir **projeto Web dinâmico** listado como um projeto disponível depois de clicar em **arquivo**, **novo**, em seguida, Olá a seguir: clique em **arquivo**, clique em **novo**, clique em **projeto... **, expanda **Web**, clique em **projeto Web dinâmico**e clique em **próximo**.)

1. Para fins deste tutorial, nomeie o projeto de saudação **MyHelloWorld**. (Certifique-se de usar esse nome, as etapas subsequentes neste tutorial esperam sua toobe de arquivo WAR nomeado MyHelloWorld). Sua tela será exibido a seguir toohello semelhante:

   ![][ic589576]

1. Clique em **Concluir**.

1. No modo de exibição do Gerenciador de Projeto do Eclipse, expanda **MyHelloWorld**. Clique com o botão direito do mouse em **WebContent**, clique em **Novo** e, em seguida, clique em **Arquivo JSP**.

1. Em Olá **novo arquivo JSP** caixa de diálogo, o arquivo de saudação do nome **index.jsp**. Mantenha a pasta pai Olá **MyHelloWorld/WebContent**, conforme mostrado na seguinte hello:

   ![][ic659262]

1. Em Olá **Selecionar modelo JSP** caixa de diálogo, para fins deste tutorial, selecione **novo arquivo JSP (html)** e clique em **concluir**.

1. Quando o arquivo do hello index.jsp for aberto no Eclipse, adicione na exibição do texto toodynamically **Olá, mundo!** dentro de saudação existente `<body>` elemento. Seu atualizada `<body>` conteúdo deve aparecer da seguinte hello:
   ```
   <body>
   <b><% out.println("Hello World!"); %></b>
   </body>
   ```
1. Salve o index.jsp.

## <a name="toodeploy-your-application-tooazure-hello-quick-and-simple-way"></a>toodeploy seu aplicativo tooAzure, Olá maneira rápida e simple
Assim que você tiver um tootest do Java web aplicativo pronto, você pode usar o hello atalho tootry-out diretamente no hello Azure na nuvem a seguir.

1. No Gerenciador de Projeto do Eclipse, clique em **MyHelloWorld**.

2. Na barra de ferramentas do Eclipse hello, clique em Olá **publicar** botão suspenso e, em seguida, clique em **Publicar como serviço de nuvem do Azure**

   ![][publishDropdownButton]

3. Se você estiver publicando tooAzure esse aplicativo para Olá primeira vez e você não tiver criado um projeto de implantação do Azure para este aplicativo antes, um projeto de implantação do Azure criado para você automaticamente. Você deve ver Olá seguir prompt, que também lista Olá JDK pacote e aplicativo servidor que será automaticamente implantado toorun seu aplicativo.

   ![][ic789598]
   
   Essa abordagem de atalho permite uma maneira rápida e fácil tootest seu aplicativo no Azure sem ter tooconfigure um servidor específico ou JDK diferente dos padrões de saudação. Se você estiver satisfeito com os padrões de saudação, você pode clicar em **Okey** toocontinue com hello etapas a seguir.
   No entanto, se você quiser toochange Olá JDK ou toouse de servidor de aplicativo para seu aplicativo, você pode fazer isso mais tarde editando Olá projeto de implantação do Azure que foi criado automaticamente para você, ou você pode clicar em **Cancelar** agora e leia Olá **seção de projetos de implantação do Azure sobre** deste tutorial.

4. Em Olá **publicar tooAzure** caixa de diálogo:

   1. Se não houver nenhum tooselect de assinaturas no hello **assinatura** liste ainda, siga essas etapas tooimport suas informações de assinatura:
      1. Clique em **Importar do arquivo PUBLISH-SETTINGS**.
      2. Em Olá **importar informações de assinatura** caixa de diálogo, clique em **baixar o arquivo de configurações de publicação**. Se você ainda não está conectados à sua conta do Azure, será solicitado toolog no. Em seguida, será solicitado que você toosave do Azure publica o arquivo de configurações. Salve-o computador local tooyour.
      3. Ainda no hello **importar informações de assinatura** caixa de diálogo, clique em Olá **procurar** botão, selecione Olá publicar o arquivo de configurações que você salvou localmente na etapa anterior hello e, em seguida, clique em ** Abra**. Sua tela deve ser a seguir toohello semelhante:![][ic644267]
      4. Clique em **OK**.
   2. Para **assinatura**, selecione Olá assinatura que você deseja usar para sua implantação.
   3. Para **conta de armazenamento**, selecione Olá conta de armazenamento que você deseja toouse ou clique em **novo** toocreate uma nova conta de armazenamento.
   4. Para **nome do serviço**, selecione Serviço de nuvem Olá que você deseja toouse ou clique em **novo** toocreate um novo serviço de nuvem.
   5. Para **sistema operacional de destino**, selecione Olá versão de hello sistema operacional que você deseja toouse para sua implantação.
   6. Em **Ambiente de destino**, para o objetivo deste tutorial, selecione **Preparo**. (Quando você estiver pronto toodeploy site de produção de tooyour, mude isso muito**produção**.)
   7. Opcional: Certifique-se de que **substituir implantação anterior** é verificado se você quiser que seu novo tooautomatically de implantação substituir Olá implantação anterior. Quando você habilitar essa opção, você vai não os problemas "409 Conflito" ao publicar toohello mesmo local.
      Observe que Olá **publicar tooAzure** caixa de diálogo contém uma seção para **acesso remoto**. Por padrão, o Acesso Remoto não está habilitado, e não habilitaremos ele para este exemplo. tooenable acesso remoto, você deve inserir um toouse de nome e a senha do usuário ao fazer logon remotamente. Para saber mais sobre o Acesso Remoto, confira [Habilitar o Acesso Remoto para Implantações do Azure no Eclipse][Enabling Remote Access for Azure Deployments in Eclipse].
      O **publicar tooAzure** caixa de diálogo será exibida a seguir toohello semelhante:![][ic719488]

5. Clique em **publicar** ambiente de preparo toohello toopublish.

   Quando solicitada tooperform uma compilação completa, clique em **Sim**. Isso pode levar vários minutos para compilação de saudação primeiro.
   Um **Log de Atividades do Azure** será exibido na seção de modos de exibição com guias do Eclipse.
   ![][ic719489]Você pode usar esse log, bem como Olá **Console** exibir progresso de saudação toosee da sua implantação. Uma alternativa é toolog em toohello [Portal de gerenciamento][Azure Management Portal]e usar o hello **serviços de nuvem** seção toomonitor status de saudação.

6. Quando a implantação é implantada com êxito, Olá **o Log de atividades do Azure** mostrará um status de **publicado**. Clique em **publicado**, conforme mostrado no hello seguintes imagem e seu navegador abrirá uma instância de sua implantação.

   ![][ic719490]

Como essa era uma tooa implantação ambiente de preparo, o nome DNS de saudação será Olá formato http://&lt;*guid*&gt;. c e a URL de saudação conterá o nome de DNS hello e um sufixo para seu aplicativo. Por exemplo, http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld. (Olá **MyHelloWorld** parte diferencia maiusculas de minúsculas.) Você também pode ver Olá DNS nome se você clicar em nome da implantação Olá no Portal de gerenciamento de plataforma da saudação (na parte de serviços de nuvem Olá Olá do portal de gerenciamento).

Embora este passo a passo para um toohello implantação ambiente de preparo, uma implantação tooproduction segue Olá mesmas etapas, exceto em Olá **publicar tooAzure** caixa de diálogo, selecione **produção** em vez de **preparo** para Olá **ambiente de destino**. Uma implantação tooproduction resulta em uma URL baseada no nome DNS de saudação de sua escolha, em vez de um GUID como foi usado para a preparação.

> [!WARNING]
> Neste ponto, você implantou sua nuvem de toohello de aplicativo do Azure. No entanto, antes de continuar, observe que um aplicativo implantado, mesmo se ele não está em execução, continuará tooaccrue horas faturáveis para sua assinatura. Portanto, é extremamente importante que você exclua as implantações indesejadas de sua assinatura do Azure.
> 
> 

## <a name="about-azure-deployment-projects"></a>Sobre projetos de implantação do Azure
Em ordem toodeploy um ou mais tooAzure de aplicativos Java, é necessário um projeto de implantação do Azure. Ele desempenha a função de saudação de hello "pacote" que seus aplicativos precisam toobe encapsulada em ordem toobe publicado no Azure.

Além de informações de saudação sobre seus aplicativos, um projeto de implantação do Azure também contém informações sobre outros componentes-chave de sua implantação, o mais importante: Olá toorun de contêiner do servidor de aplicativo em seu aplicativo web e Olá Java runtime toorun-lo no. O Azure suporta uma ampla seleção de tempos de execução Java e servidores de aplicativos Java para sua escolha.

Embora o exemplo hello usado aqui seja bastante simplificado para fins educacionais, um projeto de implantação do Azure também pode conter outras informações importantes de configuração que permite que você toocreate quase arbitrariamente complexo, escalonável, altamente disponível Serviços de nuvem de várias camadas com seus aplicativos. Você pode habilitar a **afinidade de sessão ("sessões temporárias")**, o **cache rápido**, o **descarregamento de SSL**, o **firewall/roteamento de porta**, o **acesso remoto** e várias outras funcionalidades avançadas.

Se você concluiu a seção anterior Olá deste tutorial ("toodeploy seu aplicativo tooAzure, Olá maneira rápida e simple"), agora você verá um novo projeto de implantação do Azure no Explorador de projeto gerado automaticamente para você e nomeado de saudação "** MyHelloWorld_onAzure**".

Você também pode ter começado este tutorial criando primeiro um projeto de implantação do Azure em branco por conta própria e adicionando tooit seu aplicativo (s). É mais um longo processo, mas oferece mais controle sobre a configuração inicial desde o início de Olá Olá.

toocreate um novo projeto de implantação do Azure do zero, clique em Olá **novo projeto de implantação do Azure** botão ![][ic710876].

Independentemente de se você estiver trabalhando com um projeto de implantação do Azure já existente ou criar uma nova, você está toochange capaz de suas configurações e componentes, como Olá JDK ou Olá o servidor de aplicativos, com a mesma facilidade a qualquer momento.

Olá toochange JDK, ou o servidor de aplicativo hello ou lista de aplicativos de saudação em um projeto de implantação do Azure existente:

1. Expanda o nó do projeto hello (por exemplo, **MyHelloWorld_onAzure**) no hello Explorador de projeto

2. Clique com o botão direito do mouse em **WorkerRole1**

3. Expanda Olá **Azure** submenu no menu de contexto de saudação

4. Clique em **Configuração do Servidor**

Independentemente de se você iniciou essas etapas de configuração do servidor editando um projeto de implantação do Azure existente, como mostrado acima, ou criar um novo a partir do zero, você verá Olá mesmo tipo de caixas de diálogo que permite tooconfigure seu JDK, servidor e aplicativo componentes. toolearn mais como configurações de saudação toochange nessas caixas de diálogo, por exemplo hello toochange JDK, Olá servidor de aplicativos e adicionar ou remover aplicativos em uma implantação, consulte Olá [propriedades de configuração do servidor] [ Server configuration properties] artigo.

## <a name="windows-only-toodeploy-your-application-toohello-compute-emulator"></a>Somente o Windows: toodeploy toohello seu aplicativo o emulador de computação

> [!NOTE]
> Olá emulador do Azure só está disponível no Windows. Ignore esta seção se você estiver usando um sistema operacional diferente do Windows.
> 
> 

Se você tiver criado um novo projeto de implantação do Azure Olá etapas descritas anteriormente, ou seja, implicitamente, publicando tooAzure seu aplicativo, Olá JDK e servidores de aplicativos foram configurados para a nuvem hello, mas não para emulação de local. tooprepare seu projeto para testes no emulador local do hello, siga estas etapas:

1. No Gerenciador de Projeto do Eclipse, clique em **MyHelloWorld_onAzure**.

2. Clique com o botão direito do mouse em **WorkerRole1**.

3. Expanda Olá **Azure** submenu no menu de contexto de saudação.

4. Clique em **Configuração do Servidor**.

5. Em Olá **JDK** guia, verifique se Olá Kit de ferramentas pré-configurou um padrão JDK local para você. Se não, ou se você quiser toochange Olá assumido padrões, certifique-se de que Olá **Olá Use JDK desse caminho de arquivo para testar localmente** caixa de seleção está marcada e Olá local de instalação do JDK que você deseja toouse for especificado. Se você quiser toochange-la, clique em Olá **procurar** botão e usando o controle de navegação de Olá, selecione o local do diretório de saudação do hello JDK toouse.

6. Clique em Olá **Server** guia.

7. Em Olá **caminho de servidor Local** caixa de texto na parte inferior de Olá Olá da caixa de diálogo, digite o caminho de saudação de um servidor instalado localmente que corresponde ao tipo de saudação e número de versão principal do servidor de saudação selecionado na parte superior de Olá Olá da caixa de diálogo, em Olá **implantar um servidor deste tipo** caixa de seleção. Se você quiser toouse um tipo diferente ou a versão principal saudação do servidor de aplicativos, altere a seleção de saudação nessa caixa de seleção pela primeira vez.

8. Clique em **OK**.

9. Na barra de ferramentas do Eclipse hello, clique em Olá **executar no emulador do Azure** botão, ![][ic710879]. Se hello **executar no emulador do Azure** botão não estiver habilitado, certifique-se de que **MyHelloWorld_onAzure** está selecionado no Explorador de projeto do Eclipse e certifique-se de que o Explorador de projeto do Eclipse esteja como Olá janela atual. Isso inicia pela primeira vez uma compilação completa do seu projeto e, em seguida, inicie o aplicativo de web de Java no emulador de computação hello. (Observe que, dependendo das características de desempenho do seu computador, Olá primeira compilação pode levar entre alguns segundos tooa alguns minutos, mas as compilações subsequentes receberá mais rápido.) Após a conclusão Olá a primeira etapa de compilação, você será solicitado pelo controle de conta do usuário (UAC) do Windows tooallow toomake esse comando altera tooyour computador. Clique em **Sim**.

> [!IMPORTANT]
> Se você não vir seleção prompt do UAC Olá Olá na barra de tarefas do Windows para o ícone do UAC hello e clique nele primeiro. Às vezes, Olá prompt do UAC não aparece como uma janela de nível superior, mas é visível somente como um ícone na barra de tarefas.
> 
> 

1. Examine a saída de saudação do hello toodetermine de interface do usuário de emulador de computação se houver algum problema com o seu projeto. Dependendo do conteúdo da saudação da sua implantação, ele pode levar alguns minutos para que seu toobe aplicativo totalmente iniciado no emulador de computação de saudação.

2. Iniciar o navegador e usar Olá URL `http://localhost:8080/MyHelloWorld` como endereço hello (Olá `MyHelloWorld` parte Olá URL diferencia maiusculas de minúsculas). Você deve ver o aplicativo MyHelloWorld (saída Olá de index.jsp), semelhante toohello imagem a seguir:

   ![][ic589579]

Quando você estiver pronto toostop seu aplicativo seja executado no emulador de computação do hello, na barra de ferramentas do Eclipse hello, clique em Olá **redefinir emulador do Azure** botão, ![][ic710880].

## <a name="toodelete-your-deployment"></a>toodelete sua implantação
toodelete sua implantação em Olá Kit de ferramentas do Azure para Eclipse, certifique-se de que **MyHelloWorld_onAzure** é selecionada no Explorador de projeto do Eclipse, certifique-se de saudação Explorador de projeto do Eclipse tem janela atual Olá foco e, em seguida, clique em Olá **Cancelar publicação** botão, ![][ic710883], na barra de ferramentas do Eclipse hello. (Você pode fazer Olá a mesma operação clicando **MyHelloWorld_onAzure** no Explorador de projeto do Eclipse, clicando em **Azure** e, em seguida, clicando em **desimplantar da nuvem do Azure**.) Isso exibirá Olá **cancelar a publicação de projeto do Azure** caixa de diálogo.

![][ic719491]

Selecione o serviço de assinatura e na nuvem Olá que contém sua implantação, implantação de saudação selecione que você deseja toodelete e, em seguida, clique em **Cancelar publicação**.

(Uma implantação de saudação toousing alternativo Olá toolkit toodelete é Olá toouse **serviços de nuvem** seção Olá Portal de gerenciamento do Azure: Navegue tooyour implantação, selecione-o e clique em Olá **excluir** botão. Isso interromperá e, em seguida, excluir, a implantação de saudação. Se você quiser apenas toostop implantação de saudação e não excluí-la, clique em Olá **parar** botão em vez da saudação **excluir** botão, mas, conforme mencionado acima, se você não excluir a implantação de hello, será encargos faturável Continue tooaccrue para sua implantação mesmo se ele é interrompido).

## <a name="see-also"></a>Consulte também
[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]

[Saudação de instalar o Kit de ferramentas do Azure para Eclipse][Installing hello Azure Toolkit for Eclipse] 

[Novidades no Kit de ferramentas do Azure para Eclipse de saudação][What's New in hello Azure Toolkit for Eclipse]

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Role Properties]: http://go.microsoft.com/fwlink/?LinkID=699525
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Enabling Remote Access for Azure Deployments in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699538
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Server configuration properties]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic589576]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589576.png
[ic589579]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589579.png
[ic600360]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic600360.png
[ic644267]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic644267.png
[ic659262]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic659262.png
[ic710876]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710876.png
[ic710879]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710879.png
[ic710880]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710880.png
[ic710882]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710882.png
[ic710883]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710883.png
[ic719488]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719488.png
[ic719489]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719489.png
[ic719490]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719490.png
[ic719491]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719491.png
[ic789598]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic789598.png
[publishDropdownButton]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/publishDropdownButton.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690944.aspx -->
