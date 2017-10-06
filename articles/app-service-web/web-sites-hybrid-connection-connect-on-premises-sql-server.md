---
title: "aaaConnect tooon local SQL Server de um aplicativo web no serviço de aplicativo do Azure usando conexões híbridas"
description: Criar um aplicativo web no Microsoft Azure e conecte-o banco de dados do SQL Server tooan no local
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a>Conecte-se o SQL Server local tooon de um aplicativo web no serviço de aplicativo do Azure usando conexões híbridas
Conexões híbridas podem se conectar [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) recursos de tooon locais de aplicativos Web que usam uma porta TCP estática. Os recursos com suporte incluem Microsoft SQL Server, MySQL, APIs Web HTTP, Serviço de Aplicativo e os serviços Web mais personalizados.

Neste tutorial, você aprenderá como toocreate um aplicativo de serviço web app Olá [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715), conectar Olá web aplicativo tooyour local no local do SQL Server banco de dados usando o novo recurso de Conexão híbrida hello, criar um simples ASP.NET aplicativo que usar conexão de híbrida hello e implantar Olá aplicativo toohello aplicativo do serviço de aplicativo web. Olá concluída web app no Azure armazena as credenciais do usuário em um banco de dados de associação que é local. tutorial de saudação não assume nenhuma experiência anterior com o Azure ou o ASP.NET.

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> parte de aplicativos Web de saudação do recurso de conexões híbridas hello está disponível apenas no hello [Portal do Azure](https://portal.azure.com). toocreate uma conexão nos serviços do BizTalk, consulte [conexões híbridas](http://go.microsoft.com/fwlink/p/?LinkID=397274).  
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você precisará Olá produtos a seguir. Todos estão disponíveis em versões gratuitas, portanto, é possível começar a desenvolver para o Azure de maneira totalmente gratuita.

* **Assinatura do Azure** - para uma assinatura gratuita, consulte [Avaliação Gratuita do Azure](/pricing/free-trial/).
* **Visual Studio 2013** -toodownload uma versão de avaliação gratuita do Visual Studio 2013, consulte [Downloads do Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs). Instale isso antes de continuar.
* **Microsoft .NET Framework 3.5 Service Pack 1** – Se o seu sistema operacional for Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 ou Windows Server 2008 R2, você pode habilitar esse item em Painel de Controle > Programas e Recursos > Ativar ou desativar recursos do Windows. Caso contrário, você pode baixá-lo do hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).
* **SQL Server 2014 Express com ferramentas** -baixar o Microsoft SQL Server Express gratuitamente em Olá [página de banco de dados do Microsoft Web Platform](http://www.microsoft.com/web/platform/database.aspx). Escolha Olá **Express** (não LocalDB) versão. Olá **Express with Tools** versão inclui o SQL Server Management Studio, você usará neste tutorial.
* **SQL Server Management Studio Express** - isso é incluído com o SQL Server 2014 Express de saudação com download de ferramentas mencionado acima, mas se você precisar tooinstall-lo separadamente, você pode baixar e instalá-lo de saudação [SQL Server Express página de download](http://www.microsoft.com/web/platform/database.aspx).

tutorial de saudação pressupõe que você tenha uma assinatura do Azure, que você tenha instalado o Visual Studio 2013, e que você tenha instalado ou habilitado do .NET Framework 3.5. tutorial de saudação mostra como tooinstall SQL Server 2014 Express em uma configuração que funciona bem com hello Azure híbrido conexões recurso (uma instância padrão com uma porta TCP estática). Antes de iniciar o tutorial hello, baixe o SQL Server 2014 Express com ferramentas de local de saudação mencionado acima, se você não tiver o SQL Server instalado.

### <a name="notes"></a>Observações
toouse um SQL Server no local ou no banco de dados do SQL Server Express com uma conexão híbrida, TCP/IP precisa toobe habilitado em uma porta estática. As instâncias padrão no SQL Server usam a porta estática 1433, ao passo que instâncias nomeadas não.

computador Olá no qual você instala o agente de Gerenciador de Conexão híbrida local hello:

* Deve ter conectividade de saída tooAzure sobre:

| Porta | Porque |
| --- | --- |
| 80 |**Necessária** para porta HTTP para validação de certificado e, opcionalmente, para conectividade de dados. |
| 443 |**Opcional** para conectividade de dados. Se a conectividade de saída too443 não estiver disponível, a porta TCP 80 é usada. |
| 5671 e 9352 |**Recomendada** , mas opcional para conectividade de dados. Observe que esse modo costuma produzir uma taxa de transferência maior. Se portas de toothese de conectividade de saída não estiver disponível, a porta TCP 443 será usada. |

* Deve ser capaz de tooreach Olá *hostname*:*portnumber* do recurso local.

Olá etapas neste artigo presumem que você está usando o navegador de saudação do computador Olá que hospedará o agente de conexão híbrida do hello local.

Se você já tiver o SQL Server instalado em uma configuração e em um ambiente que atenda às condições de saudação descritas acima, você pode ignorá-la e começar com [criar um banco de dados do SQL Server local](#CreateSQLDB).

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a>R. Instalar o SQL Server Express, habilitar TCP/IP e criar um banco de dados SQL Server local
Esta seção mostra como tooinstall SQL Server Express, habilite o TCP/IP e criar um banco de dados para que seu aplicativo web trabalhará com hello Portal do Azure.

### <a name="install-sql-server-express"></a>Instalar SQL Server Express
1. tooinstall SQL Server Express, execute Olá **SQLEXPRWT_x64_ENU.exe** ou **SQLEXPR_x86_ENU.exe** arquivo que você baixou. Olá Central de instalação do SQL Server Assistente é exibido.
   
    ![Instalar SQL Server][SQLServerInstall]
2. Escolha **instalação autônoma do novo SQL Server ou adicionar recursos tooan existente instalação**. Siga as instruções do hello, aceitando as opções padrão hello e configurações, até chegar toohello **configuração da instância** página.
3. Em Olá **configuração da instância** escolha **instância padrão**.
   
    ![Selecione Instância padrão][ChooseDefaultInstance]
   
    Por padrão, instância padrão de saudação do SQL Server escuta para solicitações de clientes do SQL Server na porta estática 1433, que é o hello recurso exige que as conexões híbridas. Instâncias nomeadas utilizam portas dinâmicas e UDP, que não têm suporte em Conexões Híbridas.
4. Aceite os padrões Olá Olá **configuração do servidor** página.
5. Em Olá **configuração do mecanismo de banco de dados** página em **modo de autenticação**, escolha **modo misto (autenticação do SQL Server e autenticação do Windows)**e fornecer uma senha.
   
    ![Selecione Modo Misto][ChooseMixedMode]
   
    Neste tutorial, você irá utilizar autenticação de SQL Server. Ser senha de saudação tooremember-se de que você fornecer, pois você precisará dele mais tarde.
6. Percorra o restante da saudação da instalação de Olá Olá Assistente toocomplete.

### <a name="enable-tcpip"></a>Habilitar TCP/IP
tooenable TCP/IP, você usará a SQL Server Configuration Manager, que foi instalado quando você instalou o SQL Server Express. Siga as etapas de saudação em [habilitar o protocolo de rede TCP/IP para o SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) antes de continuar.

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a>Criar um banco de dados SQL Server local
Seu aplicativo Web do Visual Studio exige um banco de dados de associação que possa ser acessado pelo Azure. Isso exige um SQL Server ou SQL Server Express banco de dados (não Olá LocalDB que Olá MVC modelo usa por padrão), portanto, você vai criar banco de dados de associação de saudação lado.

1. No SQL Server Management Studio, conecte-se toohello recém-instalada do SQL Server. (Se hello **conectar tooServer** caixa de diálogo não for exibido automaticamente, navegue muito**Pesquisador de objetos** no painel esquerdo do hello, clique em **conectar**e, em seguida, clique em **Mecanismo de banco de dados**.) ![Conecte-se tooServer][SSMSConnectToServer]
   
    Para **Tipo de servidor**, selecione **Mecanismo de Banco de Dados**. Para **nome do servidor**, você pode usar **localhost** ou nome de saudação do computador de saudação que você está usando. Escolha **autenticação do SQL Server**e, em seguida, faça logon com nome de usuário do hello sa e a senha de saudação que você criou anteriormente.
2. toocreate um novo banco de dados usando o SQL Server Management Studio, clique com botão direito **bancos de dados** no Pesquisador de objetos e, em seguida, clique em **novo banco de dados**.
   
    ![Criar novo banco de dados][SSMScreateNewDB]
3. Em Olá **novo banco de dados** caixa de diálogo, digite MembershipDB para o nome do banco de dados de saudação e, em seguida, clique em **Okey**.
   
    ![Fornecer nome de banco de dados][SSMSprovideDBname]
   
    Observe que você não faça qualquer banco de dados de toohello alterações neste momento. informações de associação de saudação serão adicionadas automaticamente mais tarde pelo aplicativo web quando você executá-lo.
4. No Pesquisador de objetos, se você expandir **bancos de dados**, você verá esse banco de dados de associação de saudação foi criado.
   
    ![MembershipDB criado][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a>B. Criar um aplicativo web no hello Portal do Azure
> [!NOTE]
> Se você já tiver criado um aplicativo web no hello Portal do Azure que você deseja toouse para este tutorial, você poderá pular muito[criar uma Conexão híbrida e um BizTalk Service](#CreateHC) e continuar a partir daí.
> 
> 

1. Em Olá [Portal do Azure](https://portal.azure.com), clique em **novo** > **Web + móvel** > **aplicativo Web**.
   
    ![Novo botão][New]
2. Configure o aplicativo Web e, em seguida, clique em **Criar**.
   
    ![Nome do site][WebsiteCreationBlade]
3. Após alguns instantes, Olá web app é criado e aparece de folha do aplicativo web. folha de saudação é um painel rolável verticalmente que permite que você gerencie o seu aplicativo web.
   
    ![Website executando][WebSiteRunningBlade]
   
    tooverify Olá web aplicativo estiver ativo, você pode clicar em Olá **procurar** página padrão do ícone toodisplay hello.

Em seguida, você criará uma conexão híbrida e um serviço BizTalk para o aplicativo web de saudação.

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a>C. Criar uma Conexão Híbrida e um Serviço do BizTalk
1. No Portal do hello, vá toosettings novamente e clique em **rede** > **configurar seus pontos de extremidade de conexão híbrida**.
   
    ![Conexões Híbridas][CreateHCHCIcon]
2. Na folha de conexões do hello híbrida, clique em **adicionar** > **nova conexão de híbrida**.
3. Em Olá **criar conexão híbrida** folha:
   
   * Para **nome**, forneça um nome para a conexão de saudação.
   * Para **Hostname**, digite nome do computador de saudação do computador host do SQL Server.
   * Para **porta**, digite 1433 (porta de saudação padrão para o SQL Server).
   * Clique em **BizTalk Service** > **novo serviço BizTalk** e insira um nome para o serviço BizTalk da saudação.
     
     ![Criar uma Conexão Híbrida][TwinCreateHCBlades]
4. Clique em **OK** duas vezes.
   
    Quando Olá processo for concluído, hello **notificações** área pisca uma verde **êxito** e hello **conexão híbrida** folha mostrará a nova conexão de híbrida Olá com Olá status como **não conectado**.
   
    ![Uma conexão híbrida criada][CreateHCOneConnectionCreated]

Neste ponto, você concluiu uma parte importante da infraestrutura de conexão Olá nuvem híbrida. Em seguida, você criará uma parte local correspondente.

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>D. Instalar Olá conexão do Gerenciador de Conexão híbrida toocomplete Olá local
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

Essa infra-estrutura de conexão híbrida Olá é concluída, você criará um aplicativo web que utiliza.

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a>E. Criar um projeto de web do ASP.NET básico, editar cadeia de conexão de banco de dados de saudação e executar o projeto Olá localmente
### <a name="create-a-basic-aspnet-project"></a>Criar um projeto ASP.NET básico
1. No Visual Studio, no hello **arquivo** menu, crie um novo projeto:
   
    ![Novo projeto de Visual Studio][HCVSNewProject]
2. Em Olá **modelos** seção Olá **novo projeto** caixa de diálogo, selecione **Web** e escolha **aplicativo Web ASP.NET**e, em seguida, clique em  **Okey**.
   
    ![Selecione Aplicativo Web ASP.NET][HCVSChooseASPNET]
3. Em Olá **novo projeto ASP.NET** caixa de diálogo, escolha **MVC**e, em seguida, clique em **Okey**.
   
    ![Selecione MVC][HCVSChooseMVC]
4. Quando Olá projeto foi criado, Olá aplicativo Leiame página será exibida. Não execute Olá web projeto ainda.
   
    ![Página Leia-me][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a>Editar cadeia de conexão de banco de dados Olá para o aplicativo hello
Nesta etapa, você editar cadeia de caracteres de conexão de saudação que informa ao seu aplicativo onde toofind seu local do SQL Server Express banco de dados. cadeia de caracteres de conexão Hello está no arquivo de Web. config do aplicativo hello, que contém informações de configuração para o aplicativo hello.

> [!NOTE]
> tooensure que seu aplicativo usa o banco de dados de saudação que você criou no SQL Server Express e não hello um padrão do Visual Studio LocalDB, é importante que você concluir esta etapa antes de executar seu projeto.
> 
> 

1. No Solution Explorer, clique duas vezes no arquivo Web. config de saudação.
   
    ![Web.config][HCVSChooseWebConfig]
2. Editar saudação **connectionStrings** seção toopoint toohello banco de dados SQL em seu computador local, o que segue a sintaxe da saudação em Olá exemplo a seguir:
   
    ![Cadeia de conexão][HCVSConnectionString]
   
    Ao compor a cadeia de caracteres de conexão Olá, lembre-se no seguinte de saudação mente:
   
   * Se você estiver se conectando tooa chamado instância em vez de uma instância padrão (por exemplo, YourServer\SQLEXPRESS), você deve configurar as portas de estático toouse do SQL Server. Para obter informações sobre como configurar portas estáticas, consulte [como tooconfigure toolisten de SQL Server em uma porta específica](http://support.microsoft.com/kb/823938). Por padrão, instâncias nomeadas utilizam UDP e portas dinâmicas, que não têm suporte em Conexões Híbridas.
   * É recomendável que você especifique Olá porta (1433 por padrão, conforme mostrado no exemplo hello) na cadeia de caracteres de conexão Olá para que você pode ter certeza de que o SQL Server local tem TCP habilitado e está usando a porta correta hello.
   * Lembre-se de toouse tooconnect de autenticação do SQL Server, especificando Olá ID de usuário e senha na cadeia de caracteres de conexão.
3. Clique em **salvar** no arquivo Web. config do Visual Studio toosave hello.

### <a name="run-hello-project-locally-and-register-a-new-user"></a>Execute o projeto de saudação localmente e registrar um novo usuário
1. Agora, execute o novo projeto web localmente clicando o botão Olá em depuração. Este exemplo usa o Internet Explorer.
   
    ![Executar projeto][HCVSRunProject]
2. Superior direito da página de web padrão Olá Olá, escolha **registrar** tooregister uma nova conta:
   
    ![Registrar uma nova conta][HCVSRegisterLocally]
3. Digite um nome de usuário e uma senha:
   
    ![Digite nome de usuário e senha][HCVSCreateNewAccount]
   
    Isso cria automaticamente um banco de dados no SQL Server local que contém informações de associação de saudação para seu aplicativo. Uma das tabelas de saudação (**dbo. AspNetUsers**) mantém web credenciais de usuário do aplicativo como Olá aqueles que você acabou de digitar. Você verá essa tabela mais tarde no tutorial de saudação.
4. Feche a janela do navegador de saudação da página de web saudação padrão. Isso impede que o aplicativo hello no Visual Studio.

Você agora está pronto para Olá próxima etapa, que é toopublish Olá aplicativo tooAzure e testá-lo.

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a>F. Publicar Olá web aplicativo tooAzure e testá-lo
Agora, você publicar seu aplicativo tooyour aplicativo do serviço de aplicativo web e testá-lo toosee como conexão híbrida de saudação configurados anteriormente está sendo usado tooconnect seu banco de dados do toohello de aplicativo da web em seu computador local.

### <a name="publish-hello-web-application"></a>Publicar o aplicativo da web hello
1. Você pode baixar o perfil de publicação para Olá aplicativo do serviço de aplicativo web de saudação Portal do Azure. Na folha de saudação para seu aplicativo web, clique em **obter perfil de publicação**e, em seguida, salve o computador de tooyour arquivo hello.
   
    ![Baixar perfil de publicação][PortalDownloadPublishProfile]
   
    Em seguida, você importará esse arquivo em seu aplicativo Web do Visual Studio.
2. No Visual Studio, clique em nome do projeto Olá no Gerenciador de soluções e selecione **publicar**.
   
    ![Selecionar Publicar][HCVSRightClickProjectSelectPublish]
3. Em Olá **Publicar Web** caixa de diálogo, no hello **perfil** guia, escolha **importação**.
   
    ![Importar][HCVSPublishWebDialogImport]
4. Procurar tooyour baixado o perfil de publicação, selecioná-lo e, em seguida, clique em **Okey**.
   
    ![Procurar tooprofile][HCVSBrowseToImportPubProfile]
5. As informações de publicação são importadas e exibe no hello **Conexão** guia da caixa de diálogo de saudação.
   
    ![Clicar em Publicar][HCVSClickPublish]
   
    Clique em **Publicar**.
   
    Quando a publicação for concluído, o navegador iniciará e mostrar seu aplicativo ASP.NET já conhecido - exceto que agora ele está ativo no hello nuvem do Azure!

Em seguida, você usará o toosee de aplicativo da web dinâmico sua Conexão híbrida na ação.

### <a name="test-hello-completed-web-application-on-azure"></a>Saudação de teste concluído o aplicativo web no Azure
1. Na parte superior de saudação à direita da página da web no Azure, escolha **login**.
   
    ![Logon Para Teste][HCTestLogIn]
2. Seu serviço de aplicativo web aplicativo agora está conectado banco de dados de associação do aplicativo da web tooyour em seu computador local. tooverify isso, faça logon com hello mesmas credenciais que você inseriu no local de saudação do banco de dados anterior.
   
    ![Olá saudação][HCTestHelloContoso]
3. toofurther testar sua conexão híbrida novo, sair de seu aplicativo web do Azure e registrar-se como outro usuário. Forneça nome de usuário e senha novos e depois clique em **Registrar**.
   
    ![Testar registro de um outro usuário][HCTestRegisterRelecloud]
4. tooverify que as credenciais de saudação do novo usuário foram armazenadas no banco de dados local por meio de sua conexão híbrida, abra o SQL Management Studio no computador local. No Pesquisador de objetos, expanda Olá **MembershipDB** banco de dados e, em seguida, expanda **tabelas**. Saudação de atalho **dbo. AspNetUsers** associação de tabela e escolha **selecionar 1000 linhas superiores** tooview resultados de saudação.
   
    ![Exibir resultados da saudação][HCTestSSMSTree]
5. A tabela de associação local agora mostra ambas as contas - Olá que foi criada localmente e Olá que você criou no hello nuvem do Azure. Olá que você criou na nuvem Olá foi salvo tooyour banco de dados no local por meio do recurso de Conexão híbrida do Azure.
   
    ![Usuários registrados em banco de dados local][HCTestShowMemberDb]

Agora você criou e implantou um aplicativo web ASP.NET que usa uma conexão híbrida entre um aplicativo web no hello nuvem do Azure e um banco de dados do SQL Server local. Parabéns!

## <a name="see-also"></a>Consulte também
[Visão geral de Conexões Híbridas](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Josh Twist apresenta conexões híbridas (vídeo no Channel 9)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Visão geral de Conexões Híbridas](/services/biztalk-services/)

[Serviços BizTalk: guias Painel, Monitor, Escala, Configurar e Conexão Híbrida](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Criando uma nuvem híbrida no mundo real com portabilidade perfeita com aplicativo (vídeo no Channel 9)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Acessar os recursos locais usando conexões híbridas no Serviço de Aplicativo do Azure](web-sites-hybrid-connection-get-started.md)

[Visão geral de Identidade ASP.NET](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
