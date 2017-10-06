---
title: "recursos de locais de aaaAccess usando conexões híbridas no serviço de aplicativo do Azure"
description: "Criar uma conexão entre um aplicativo Web no Serviço de Aplicativo do Azure e um recurso local que usa uma porta TCP estática"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a>Acessar os recursos locais usando conexões híbridas no Serviço de Aplicativo do Azure
Você pode se conectar a um recurso de local de tooany de aplicativo do serviço de aplicativo do Azure que usa uma porta TCP estática, como SQL Server, MySQL, APIs da Web de HTTP e a maioria dos serviços da Web personalizados. Este artigo mostra como toocreate uma conexão híbrida entre o serviço de aplicativo e um banco de dados do SQL Server local.

> [!NOTE]
> parte de aplicativos Web de saudação do recurso de conexões híbridas hello está disponível apenas no hello [Portal do Azure](https://portal.azure.com). toocreate uma conexão nos serviços do BizTalk, consulte [conexões híbridas](http://go.microsoft.com/fwlink/p/?LinkID=397274). 
> 
> Este conteúdo também se aplica a aplicativos tooMobile no serviço de aplicativo do Azure. 
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
* Uma assinatura do Azure. Para uma assinatura gratuita, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
  
    Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
* toouse um SQL Server no local ou no banco de dados do SQL Server Express com uma conexão híbrida, TCP/IP precisa toobe habilitado em uma porta estática. É recomendado usar uma instância padrão no SQL Server porque ele usa a porta estática 1433. Para obter informações sobre como instalar e configurar o SQL Server Express para uso com conexões híbridas, consulte [tooan de conexão local do SQL Server de um site do Azure usando conexões híbridas](http://go.microsoft.com/fwlink/?LinkID=397979).
* computador Olá no qual você instalar agente de Gerenciador de Conexão híbrida local Olá descrito neste artigo:
  
  * Deve ser capaz de tooconnect tooAzure pela porta 5671
  * Deve ser capaz de tooreach Olá *hostname*:*portnumber* do recurso local. 

> [!NOTE]
> Olá etapas neste artigo presumem que você está usando o navegador de saudação do computador Olá que hospedará o agente de conexão híbrida do hello local.
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Criar um aplicativo web no hello Portal do Azure
> [!NOTE]
> Se você já tiver criado um aplicativo web ou aplicativo móvel back-end em Olá Portal do Azure que você deseja toouse para este tutorial, você poderá pular muito[criar uma Conexão híbrida e um BizTalk Service](#CreateHC) e iniciar de lá.
> 
> 

1. No canto superior esquerdo de saudação da saudação [Portal do Azure](https://portal.azure.com), clique em **novo** > **Web + móvel** > **aplicativo Web**.
   
    ![Novo aplicativo Web][NewWebsite]
2. Em Olá **aplicativo Web** folha, forneça uma URL e clique em **criar**. 
   
    ![Nome do site][WebsiteCreationBlade]
3. Após alguns instantes, Olá web app é criado e aparece de folha do aplicativo web. folha de saudação é um painel rolável verticalmente que lhe permite gerenciar seu site.
   
    ![Website executando][WebSiteRunningBlade]
4. site de saudação tooverify está ativo, você pode clicar em Olá **procurar** página padrão do ícone toodisplay hello.
   
    ![Clique em Procurar toosee seu aplicativo web][Browse]
   
    ![Página de aplicativo Web padrão][DefaultWebSitePage]

Em seguida, você criará uma conexão híbrida e um serviço BizTalk para o aplicativo web de saudação.

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a>Criar uma Conexão Híbrida e um Serviço do BizTalk
1. Na folha do seu aplicativo Web, clique em **Todas as configurações** > **Rede** > **Configurar seus pontos de extremidade de conexão híbrida**.
   
    ![Conexões Híbridas][CreateHCHCIcon]
2. Na folha de conexões do hello híbrida, clique em **adicionar**.
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. Olá **adicionar uma conexão híbrida** folha é aberta.  Como esta é sua primeira conexão de híbrida, Olá **nova conexão de híbrida** opção é pré-selecionada e Olá **criar conexão híbrida** folha é aberto para você.
   
    ![Criar uma Conexão Híbrida][TwinCreateHCBlades]
   
    Em Olá **folha de conexão híbrida criar**:
   
   * Para **nome**, forneça um nome para a conexão de saudação.
   * Para **Hostname**, insira nome de saudação do computador local Olá que hospeda o recurso.
   * Para **porta**, digite Olá número da porta que o recurso local (1433 para uma instância do SQL Server padrão).
   * Clique em **Serviço Biz Talk**
4. Olá **criar serviço de BizTalk** folha é aberta. Insira um nome para Olá serviço BizTalk e, em seguida, clique em **Okey**.
   
    ![Criar serviço BizTalk][CreateHCCreateBTS]
   
    Olá **criar serviço de BizTalk** folha fecha e você retorna toohello **criar conexão híbrida** folha.
5. Na folha de conexão híbrida do criar hello, clique em **Okey**. 
   
    ![Clique em OK][CreateBTScomplete]
6. Quando Olá processo for concluído, área de notificações de saudação em Olá Portal informa conexão Olá foi criado com êxito.
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. Na folha de seu aplicativo da web Olá Olá **conexões híbridas** ícone agora mostra que 1 conexão de híbrida foi criado.
   
    ![Uma conexão híbrida criada][CreateHCOneConnectionCreated]

Neste ponto, você concluiu uma parte importante da infraestrutura de conexão Olá nuvem híbrida. Em seguida, você criará uma parte local correspondente.

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>Instalar Olá conexão do Gerenciador de Conexão híbrida toocomplete Olá local
1. Na folha do seu aplicativo da web hello, clique em **todas as configurações** > **rede** > **configurar seus pontos de extremidade de conexão híbrida**. 
   
    ![Ícone Conexões Híbridas][HCIcon]
2. Em Olá **conexões híbridas** folha, Olá **Status** coluna Olá adicionado recentemente mostra de ponto de extremidade **não conectado**. Clique em Olá conexão tooconfigure-lo.
   
    ![Não conectado][NotConnected]
   
    Abre a folha de conexão híbrida Hello.
   
    ![NotConnectedBlade][NotConnectedBlade]
3. Na folha de saudação, clique em **configuração de ouvinte**.
   
    ![Clique em Configuração do Ouvinte][ClickListenerSetup]
4. Olá **propriedades da conexão híbrida** folha é aberta. Em **Gerenciador de Conexão híbrida local**, escolha **clique aqui tooinstall**.
   
    ![Clique aqui tooinstall][ClickToInstallHCM]
5. Olá aplicativo executado segurança aviso caixa de diálogo, escolha **executar** toocontinue.
   
    ![Escolha Executar toocontinue][ApplicationRunWarning]
6. Em Olá **User Account Control** caixa de diálogo, escolha **Sim**.
   
   ![Selecione Sim][UAC]
7. Olá Gerenciador de Conexão híbrida é baixado e instalado para você. 
   
    ![Instalando][HCMInstalling]
8. Quando a saudação instalação for concluída, clique em **fechar**.
   
    ![Clique em Fechar][HCMInstallComplete]
   
    Em Olá **conexões híbridas** folha, Olá **Status** coluna agora mostra **conectado**. 
   
    ![Status Conectado][HCStatusConnected]

Essa infra-estrutura de conexão híbrida Olá é concluída, você pode criar um aplicativo híbrido que utiliza. 

> [!NOTE]
> Olá seções a seguir mostram como toouse uma conexão híbrida com um projeto de back-end .NET de aplicativos móveis.
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a>Configurar Olá .NET de aplicativo móvel back-end projeto tooconnect toohello banco de dados SQL
No Serviço de Aplicativo, um projeto de back-end .NET dos Aplicativos Móveis é apenas um aplicativo Web ASP.NET com um SDK de Aplicativos Móveis adicional instalado e inicializado. toouse seu aplicativo da web como um back-end de aplicativos móveis, você deve [baixar e inicializar o back-end .NET de aplicativos móveis Olá SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).  

Para aplicativos móveis, você também precisa toodefine uma cadeia de caracteres de conexão para o banco de dados de local de saudação e modificar Olá back-end toouse essa conexão. 

1. No Gerenciador de soluções do Visual Studio, o arquivo Web. config Olá abrir seu back-end .NET de aplicativo móvel, localize Olá **connectionStrings** seção, adicione uma nova entrada SqlClient como Olá seguintes, quais pontos toohello SQL local Banco de dados do servidor:
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    Lembre-se de tooreplace `<**secure_password**>` na cadeia de caracteres com senha Olá criada para *HybridConnectionLogin*.
2. Clique em **salvar** no arquivo Web. config do Visual Studio toosave hello.
   
   > [!NOTE]
   > Essa configuração de conexão é usada quando em execução no computador local hello. Quando em execução no Azure, essa configuração é substituída pela configuração de conexão Olá definida no portal de saudação.
   > 
   > 
3. Expanda Olá **modelos** pasta e arquivo de modelo de dados Olá abertos, que termina em *Context.cs*.
4. Modificar Olá **DbContext** toopass do construtor de instância Olá valor `OnPremisesDBConnection` toohello base **DbContext** construtor, toohello semelhante trecho de código a seguir:
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    serviço de saudação agora usará o banco de dados do hello nova conexão toohello do SQL Server.

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a>Atualizar a cadeia de conexão Olá aplicativo móvel back-end toouse Olá local
Em seguida, você precisa tooadd uma configuração de aplicativo para essa nova cadeia de caracteres de conexão para que ele pode ser usado do Azure.  

1. Em Olá [portal do Azure](https://portal.azure.com) no código de back-end Olá web app para o seu aplicativo móvel, clique em **todas as configurações**, em seguida, **configurações de aplicativo**.
2. Em Olá **configurações de aplicativo da Web** folha, role para baixo demais**cadeias de caracteres de Conexão** e adicione um novo **do SQL Server** cadeia de caracteres de conexão denominada `OnPremisesDBConnection` com um valor como `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.
   
    Substituir `<**secure_password**>` com a senha segura Olá para seu banco de dados local.
   
    ![Cadeia de conexão para banco de dados local](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. Pressione **salvar** conexão do toosave Olá híbrida e a cadeia de caracteres de conexão que acabou de criar.

Neste ponto, você pode republicar o projeto do servidor de saudação e testar conexão nova Olá com os clientes de aplicativos móveis existentes. Dados serão leiam e gravados o banco de dados local toohello usando a conexão do hello híbrida.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Próximas etapas
* Para obter informações sobre como criar um aplicativo web ASP.NET que usa uma conexão híbrida, consulte [tooan de conexão local do SQL Server de um site do Azure usando conexões híbridas](http://go.microsoft.com/fwlink/?LinkID=397979). 

### <a name="additional-resources"></a>Recursos adicionais
[Visão geral de Conexões Híbridas](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Josh Twist apresenta conexões híbridas (vídeo do Channel 9)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Site de Conexões Híbridas](https://azure.microsoft.com/services/biztalk-services/)

[Serviços BizTalk: guias Painel, Monitor, Escala, Configurar e Conexão Híbrida](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Criando uma nuvem híbrida no mundo real com portabilidade perfeita com aplicativo (vídeo no Channel 9)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Conecte-se tooan do SQL Server de serviços móveis do Azure usando conexões híbridas (vídeo do Channel 9) local](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
