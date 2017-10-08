---
title: "aaaGet iniciado com serviços de nuvem do Azure e ASP.NET | Microsoft Docs"
description: "Saiba como toocreate um aplicativo de várias camado usando o ASP.NET MVC e o Azure. saudação de aplicativo é executado em um serviço de nuvem, com a função web e função de trabalho. Ele utiliza Entity Framework, o Banco de Dados SQL e filas e blobs de Armazenamento do Azure."
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a>Introdução aos Serviços de Nuvem do Azure e ao ASP.NET

## <a name="overview"></a>Visão geral
Este tutorial mostra como toocreate um aplicativo .NET de multicamadas com um front-end, o ASP.NET MVC e implantá-lo tooan [serviço de nuvem do Azure](cloud-services-choose-me.md). Olá aplicativo usa [banco de dados do SQL Azure](http://msdn.microsoft.com/library/azure/ee336279), Olá [serviço Blob do Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)e hello [serviço de fila do Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern). Você pode [baixar o projeto do Visual Studio Olá](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) de saudação Galeria de códigos do MSDN.

Olá tutorial mostra como aplicativo hello toobuild e executar localmente, como toodeploy-tooAzure e hello execução na nuvem e como toobuild-lo a partir do zero. Você pode iniciar Compilando a partir do zero Olá teste e implante etapas posteriormente se você preferir.

## <a name="contoso-ads-application"></a>O aplicativo Contoso Ads
aplicativo Hello é um quadro de avisos de publicidade. Os usuários criam um anúncio inserindo texto e carregando uma imagem. Eles podem ver uma lista de anúncios com imagens em miniatura e eles podem ver imagem em tamanho normal hello quando eles selecionam um ad toosee Olá os detalhes.

![Lista de anúncios](./media/cloud-services-dotnet-get-started/list.png)

usa o aplicativo Hello Olá [centrado em fila de trabalho padrão](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff carga trabalho de saudação com uso intensivo de CPU de criação de processo de back-end tooa miniaturas.

## <a name="alternative-architecture-websites-and-webjobs"></a>Arquitetura alternativa: sites e trabalhos Web
Este tutorial mostra como toorun front-end e back-end em um Azure cloud service. Uma alternativa é toorun Olá front-end em um [site do Azure](/services/web-sites/) e usar Olá [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) recurso (atualmente na visualização) para Olá back-end. Para obter um tutorial que usa trabalhos Web, consulte [Introdução ao SDK do Azure WebJobs de saudação](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md). Para obter informações sobre como toochoose Olá os serviços que melhor se ajustar seu cenário, consulte [comparação de sites do Azure, serviços de nuvem e máquinas virtuais](../app-service-web/choose-web-site-cloud-service-vm.md).

## <a name="what-youll-learn"></a>O que você aprenderá
* Como tooenable sua máquina de desenvolvimento do Azure instalando Olá SDK do Azure.
* Como toocreate um Visual Studio nuvem projeto de serviço com uma função web do ASP.NET MVC e uma função de trabalho.
* Como tootest Olá nuvem projeto de serviço localmente, usando o emulador de armazenamento do Azure hello.
* Como o tooan de projeto em nuvem toopublish hello Azure serviço de nuvem e teste usando uma conta de armazenamento do Azure.
* Como tooupload arquivos e armazená-los no serviço de Blob do Azure hello.
* Como toouse Olá serviço de fila do Azure para comunicação entre camadas.

## <a name="prerequisites"></a>Pré-requisitos
Olá tutorial assume que você entende [serviços de nuvem de conceitos básicos sobre o Azure](cloud-services-choose-me.md) como *função web* e *função de trabalho* terminologia.  Ele também pressupõe que você sabe como toowork com [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) ou [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projetos no Visual Studio. aplicativo de exemplo Hello usa MVC, mas a maioria das tutorial Olá também se aplica a formulários tooWeb.

Você pode executar o aplicativo hello localmente sem uma assinatura do Azure, mas você precisará de uma nuvem de toohello toodeploy Olá aplicativo. Se não tem uma conta, você pode [ativar os benefícios de assinante MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) ou [inscrever-se em uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).

instruções de tutorial Olá trabalham com uma saudação produtos a seguir:

* Visual Studio 2013
* Visual Studio 2015
* Visual Studio 2017

Se você não tiver um desses, Visual Studio pode ser instalado automaticamente quando você instala o SDK do Azure de saudação.

## <a name="application-architecture"></a>Arquitetura do aplicativo
aplicativo Hello armazena anúncios em um banco de dados SQL, usando tabelas de saudação do Entity Framework Code First toocreate e acessar dados de saudação. Para cada anúncio Olá banco de dados armazena duas URLs, uma para Olá imagem em tamanho normal e outra para a miniatura de saudação.

![Tabela de anúncios](./media/cloud-services-dotnet-get-started/adtable.png)

Quando um usuário carrega uma imagem, Olá front-end em execução em uma função web armazena a imagem de saudação em uma [BLOBs do Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), e armazena informações de ad Olá no banco de dados de saudação com uma URL que aponta toohello blob. AT Olá mesmo tempo, ele grava um tooan de mensagem da fila do Azure. Um processo de back-end em execução em uma função de trabalho periodicamente sonda fila Olá novas mensagens. Quando uma nova mensagem for exibida, função de trabalho Olá cria uma miniatura para essa imagem e atualizações Olá campo de banco de dados em miniatura do URL para que o ad. Olá diagrama a seguir mostra como partes de saudação do aplicativo hello interagem.

![Arquitetura do Contoso Ads](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a>Baixe e execute a solução de saudação concluída
1. Baixe e descompacte Olá [concluído solução](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).
2. Inicie o Visual Studio.
3. De saudação **arquivo** menu escolha **Abrir projeto**, navegue toowhere baixado solução hello e, em seguida, abra o arquivo de solução de saudação.
4. Pressione a solução de saudação toobuild CTRL + SHIFT + B.

    Por padrão, o Visual Studio automaticamente restaura Olá NuGet conteúdo do pacote, que não foi incluído no hello *. zip* arquivo. Se não restaurar os pacotes de saudação, instalá-los manualmente por vai toohello **gerenciar pacotes NuGet para solução** caixa de diálogo e clicar em Olá **restaurar** botão na parte superior de saudação à direita.
5. Em **Solution Explorer**, certifique-se de que **ContosoAdsCloudService** é selecionado como projeto de inicialização de saudação.
6. Se você estiver usando o Visual Studio 2015 ou superior, altere a cadeia de conexão do SQL Server Olá no aplicativo hello *Web. config* arquivo de projeto de ContosoAdsWeb hello e em Olá *ServiceConfiguration* arquivo de projeto de ContosoAdsCloudService hello. Em cada caso, altere "(localdb) \v11.0" muito "(localdb) \MSSQLLocalDB".
7. Pressione CTRL + F5 aplicativo de hello de toorun.

    Quando você executar um projeto de serviço de nuvem localmente, o Visual Studio automaticamente invoca hello Azure *emulador de computação* e o Azure *emulador de armazenamento*. Olá compute emulator usa função web do seu computador recursos toosimulate hello e ambientes de função de trabalho. emulador de armazenamento Olá usa um [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) toosimulate armazenamento em nuvem do Azure do banco de dados.

    Olá primeira vez que executar um projeto de serviço de nuvem, que leva cerca de um minuto para Olá emuladores toostart backup. Quando a inicialização do emulador for concluída, o navegador de padrão de saudação abre toohello home page do aplicativo.

    ![Arquitetura do Contoso Ads](./media/cloud-services-dotnet-get-started/home.png)
8. Clique em **Criar um Anúncio**.
9. Insira alguns dados de teste e selecione um *. jpg* tooupload da imagem e, em seguida, clique em **criar**.

    ![Criar página](./media/cloud-services-dotnet-get-started/create.png)

    aplicativo Hello vai toohello página de índice, mas ela não mostra uma miniatura para ad novo Olá porque não foi feito ainda que o processamento.
10. Aguarde um momento e, em seguida, atualize Olá índice toosee Olá miniatura.

     ![Página de índice](./media/cloud-services-dotnet-get-started/list.png)
11. Clique em **detalhes** para a imagem em tamanho normal do ad toosee hello.

     ![Página de detalhes](./media/cloud-services-dotnet-get-started/details.png)

Executa aplicativo hello inteiramente no computador local, sem nuvem toohello de conexão. emulador de armazenamento Olá armazena fila hello e dados blob em um banco de dados do SQL Server Express LocalDB e o aplicativo hello armazena dados do ad de saudação em outro banco de dados LocalDB. Entity Framework Code First Olá recém-criados banco de dados ad Olá primeira vez Olá web aplicativo tentou tooaccess-lo.

Olá seção a seguir, você configurará recursos da nuvem do Azure toouse Olá solução para filas, blobs e banco de dados de aplicativo hello quando ele é executado na nuvem hello. Se você quisesse toocontinue toorun localmente, mas usa os recursos de armazenamento e o banco de dados de nuvem, você pode fazer isso. Ele é apenas uma questão de configuração de cadeias de caracteres de conexão, você verá como toodo.

## <a name="deploy-hello-application-tooazure"></a>Implantar Olá aplicativo tooAzure
Isso será feito Olá aplicativo de hello toorun etapas na nuvem Olá a seguir:

* Criar um serviço de nuvem do Azure.
* Criar um banco de dados SQL do Azure.
* Crie uma conta de armazenamento do Azure.
* Configure Olá solução toouse seu banco de dados SQL do Azure quando ele é executado no Azure.
* Configure Olá solução toouse sua conta de armazenamento do Azure quando ele é executado no Azure.
* Implante o serviço de nuvem do Azure Olá projeto tooyour.

### <a name="create-an-azure-cloud-service"></a>Criar um serviço de nuvem do Azure
Um serviço de nuvem do Azure é Olá ambiente Olá aplicativo será executado.

1. No navegador, abra Olá [portal do Azure](https://portal.azure.com).
2. Clique em **Novo > Computação > Serviço de Nuvem**.

3. Na caixa entrada do nome do DNS de hello, digite um prefixo de URL para serviço de nuvem hello.

    Esse URL tem toobe exclusivo.  Você obterá uma mensagem de erro se você escolher de prefixo de saudação já está em uso.
4. Especifique um novo grupo de recursos para o serviço de saudação. Clique em **criar novo** e, em seguida, digite um nome na Olá recurso grupo caixa de entrada, como CS_contososadsRG.

5. Escolha a região Olá onde você deseja que o aplicativo de hello toodeploy.

    Este campo especifica em qual datacenter seu serviço de nuvem será hospedado. Para um aplicativo de produção, você escolheria Olá região mais próxima tooyour os clientes. Para este tutorial, escolha Olá região mais próxima tooyou.
5. Clique em **Criar**.

    Em Olá a imagem a seguir, um serviço de nuvem é criado com hello CSvccontosoads.cloudapp.net de URL.

    ![Novo serviço de nuvem](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a>Criar um banco de dados SQL do Azure
Quando o aplicativo hello é executado na nuvem hello, ele usará um banco de dados baseado em nuvem.

1. Em Olá [portal do Azure](https://portal.azure.com), clique em **Novo > bancos de dados > banco de dados SQL**.
2. Em Olá **nome do banco de dados** , digite *contosoads*.
3. Em Olá **grupo de recursos**, clique em **usar existente** Olá selecione grupo de recursos usados para o serviço de nuvem hello e.
4. No hello após a imagem, clique em **Server - definir configurações obrigatórias** e **criar um novo servidor**.

    ![Servidor de encapsulamento de toodatabase](./media/cloud-services-dotnet-get-started/newdb.png)

    Como alternativa, se a sua assinatura já tem um servidor, você pode selecionar o servidor da lista suspensa de saudação.
5. Em Olá **nome do servidor** , digite *csvccontosodbserver*.

6. Insira um **Nome de Logon** e **Senha** de administrador.

    Se você selecionou **Criar um novo servidor**, não digitará um nome e senha existentes aqui. Você está inserindo um novo nome e uma senha que você está definindo agora toouse posterior ao acessar o banco de dados de saudação. Se você tiver selecionado um servidor que você criou anteriormente, você será solicitado a fornecer as conta de usuário administrativo toohello senha Olá já criado.
7. Escolha Olá mesmo **local** que você escolheu para o serviço de nuvem hello.

    Quando o serviço de nuvem hello e banco de dados estão em diferentes datacenters (regiões diferentes), a latência aumentará e você será cobrado por largura de banda fora Olá data center. A largura de banda em um data center é gratuita.
8. Verificar **permitir servidor de tooaccess de serviços do azure**.
9. Clique em **selecione** para novo servidor de saudação.

    ![Novo servidor do Banco de Dados SQL](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. Clique em **Criar**.

### <a name="create-an-azure-storage-account"></a>Criar uma conta de armazenamento do Azure
Uma conta de armazenamento do Azure fornece recursos para armazenar dados blob e fila na nuvem hello.

Em um aplicativo do mundo real, geralmente você cria contas separadas para dados de aplicativos e dados de log, e contas separadas para dados de teste e dados de produção. Neste tutorial você usará apenas uma conta.

1. Em Olá [portal do Azure](https://portal.azure.com), clique em **Novo > armazenamento > conta de armazenamento - blob, arquivo, tabela, fila**.
2. Em Olá **nome** , digite um prefixo de URL.

    Esse texto de prefixo mais Olá que consulte caixa Olá será Olá exclusivos URL tooyour armazenamento de conta. Se o prefixo Olá que inserir já foi usado por outra pessoa, você terá toochoose um prefixo diferente.
3. Saudação de conjunto **modelo de implantação** muito*clássico*.

4. Saudação de conjunto **replicação** suspensa lista muito**armazenamento redundante localmente**.

    Quando a replicação geográfica é habilitada para uma conta de armazenamento, o conteúdo de Olá armazenado é replicado tooa datacenter secundário tooenable failover se ocorrer um desastre grave no local primário hello. A replicação geográfica pode incorrer em custos adicionais. Para contas de teste e desenvolvimento, geralmente você não quiser toopay para replicação geográfica. Para saber mais, confira [Criar, gerenciar ou excluir uma conta de armazenamento](../storage/common/storage-create-storage-account.md).

5. Em Olá **grupo de recursos**, clique em **usar existente** Olá selecione grupo de recursos usados para o serviço de nuvem hello e.
6. Saudação de conjunto **local** toohello da lista suspensa mesma região que você escolheu para o serviço de nuvem hello.

    Quando a conta de serviço e armazenamento de nuvem Olá estão em data centers diferentes (regiões diferentes), a latência aumentará e você será cobrado por largura de banda fora Olá data center. A largura de banda em um data center é gratuita.

    Grupos de afinidade do Azure fornecem uma distância de saudação do mecanismo toominimize entre os recursos em um data center, que pode reduzir a latência. Este tutorial não usa grupos de afinidade. Para obter mais informações, consulte [como tooCreate uma grupo de afinidade no Azure](http://msdn.microsoft.com/library/jj156209.aspx).
7. Clique em **Criar**.

    ![Nova conta de armazenamento](./media/cloud-services-dotnet-get-started/newstorage.png)

    Na imagem hello, uma conta de armazenamento é criada com a URL de saudação `csvccontosoads.core.windows.net`.

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a>Configurar Olá solução toouse seu banco de dados SQL do Azure quando ele é executado no Azure
Olá projeto web e trabalhador projeto de função de cada hello tem sua própria cadeia de caracteres de conexão do banco de dados, e cada precisa de banco de dados do SQL Azure toopoint toohello quando o aplicativo hello é executado no Azure.

Você usará um [transformação do Web. config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) para função de web hello e uma configuração de ambiente de serviço de nuvem para função de trabalho hello.

> [!NOTE]
> Nesta seção e a próxima seção do hello, você armazenar credenciais em arquivos de projeto. [Não armazene dados confidenciais em repositórios de código-fonte público](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).
>
>

1. No projeto de ContosoAdsWeb Olá, abra Olá *Web.Release.config* arquivo de transformação para o aplicativo hello *Web. config* de arquivos, excluir o bloco de comentário hello que contém um `<connectionStrings>` elemento e colar Olá seguindo o código em seu lugar.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    Deixe o arquivo hello abertos para edição.
2. Em Olá [portal do Azure](https://portal.azure.com), clique em **bancos de dados SQL** no painel esquerdo do hello, clique Olá banco de dados criado para este tutorial e, em seguida, clique em **Mostrar cadeias de conexão**.

    ![Mostrar cadeias de conexão](./media/cloud-services-dotnet-get-started/showcs.png)

    o portal de saudação exibe cadeias de caracteres de conexão, com um espaço reservado para senha hello.

    ![Cadeias de conexão](./media/cloud-services-dotnet-get-started/connstrings.png)
3. Em Olá *Web.Release.config* arquivo de transformação, exclua `{connectionstring}` e colar no seu Olá local cadeia de conexão ADO.NET do hello portal do Azure.
4. Na cadeia de caracteres de conexão de saudação que você colou no hello *Web.Release.config* transformar o arquivo, substitua `{your_password_here}` com senha Olá criada para o novo SQL database hello.
5. Salve o arquivo hello.  
6. Selecione e copie a cadeia de caracteres de conexão de saudação (sem Olá ao redor aspas) para uso em Olá seguindo as etapas para configurar o projeto de função de trabalho de saudação.
7. Em **Solution Explorer**, em **funções** no projeto de serviço de nuvem hello, clique com botão direito **ContosoAdsWorker** e, em seguida, clique em **propriedades**.

    ![Propriedades da função](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. Clique em Olá **configurações** guia.
9. Alterar **configuração do serviço** muito**nuvem**.
10. Selecione Olá **valor** campo Olá `ContosoAdsDbConnectionString` configuração e, em seguida, cole a cadeia de caracteres de conexão de saudação que você copiou da seção anterior de saudação do tutorial de saudação.

     ![Cadeia de conexão de banco de dados para função de trabalho](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. Salve suas alterações.  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a>Configurar Olá solução toouse sua conta de armazenamento do Azure quando ele é executado no Azure
Cadeias de caracteres de conexão conta de armazenamento do Azure para o projeto de função web hello e projeto de função de trabalho Olá são armazenadas nas configurações do ambiente no projeto de serviço de nuvem hello. Para cada projeto, há um conjunto separado de configurações toobe usado quando o aplicativo hello é executado localmente e quando ele é executado na nuvem hello. Você atualizará as configurações de ambiente de nuvem Olá para projetos de função da web e de trabalho.

1. Em **Solution Explorer**, clique com botão direito **ContosoAdsWeb** em **funções** em hello **ContosoAdsCloudService** do projeto e, em seguida, clique em **Propriedades**.

    ![Propriedades da função](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. Clique em Olá **configurações** guia. Em Olá **configuração do serviço** suspensa caixa, escolha **nuvem**.

    ![Configuração de nuvem](./media/cloud-services-dotnet-get-started/sccloud.png)
3. Selecione Olá **StorageConnectionString** entrada e você verá um botão de reticências (**...** ) botão final saudação à direita da linha de saudação. Clique em Olá Olá de tooopen do botão de reticências **criar cadeia de Conexão de conta de armazenamento** caixa de diálogo.

    ![Abra a caixa Criar Cadeia de Conexão](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. Em Olá **criar cadeia de Conexão de armazenamento** caixa de diálogo, clique em **sua assinatura**, escolha a conta de armazenamento Olá que você criou anteriormente e, em seguida, clique em **Okey**. Se você não tiver feito logon, suas credenciais da conta do Azure serão solicitadas.

    ![Criar cadeia de conexão de armazenamento](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. Salve suas alterações.
6. Siga Olá mesmo procedimento usado para Olá `StorageConnectionString` Olá de tooset de cadeia de caracteres de conexão `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` cadeia de caracteres de conexão.

    Essa cadeia de conexão é usada para o log.
7. Siga Olá mesmo procedimento usado para Olá **ContosoAdsWeb** tooset função ambas as cadeias de caracteres de conexão para Olá **ContosoAdsWorker** função. Não se esqueça de tooset **configuração do serviço** muito**nuvem**.

configurações de ambiente de função Hello que você configurou usando Olá IU do Visual Studio são armazenadas no hello arquivos Olá ContosoAdsCloudService projeto a seguir:

* *Servicedefinition. Csdef* -define os nomes de configuração de saudação.
* *ServiceConfiguration* -fornece valores para quando o aplicativo hello é executado na nuvem de saudação.
* *ServiceConfiguration* -fornece valores para quando o aplicativo hello é executado localmente.

Por exemplo, Olá servicedefinition. Csdef inclui Olá definições a seguir:

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

E hello *ServiceConfiguration* arquivo inclui valores hello inserido para essas configurações no Visual Studio.

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

Olá `<Instances>` configuração especifica o número de saudação de máquinas virtuais Azure executará o trabalho Olá código da função no. Olá [próximas etapas](#next-steps) seção inclui links toomore informações sobre como dimensionar um serviço de nuvem

### <a name="deploy-hello-project-tooazure"></a>Implantar Olá projeto tooAzure
1. No **Solution Explorer**, Olá atalho **ContosoAdsCloudService** projeto em nuvem e, em seguida, selecione **publicar**.

   ![Menu Publicar](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. Em Olá **entrar** etapa Olá **publicar aplicativo do Azure** assistente, clique em **próximo**.

    ![Etapa de entrada](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. Em Olá **configurações** etapa do Assistente de saudação, clique em **próximo**.

    ![Etapa configurações](./media/cloud-services-dotnet-get-started/pubsettings.png)

    Olá configurações padrão do hello **avançado** guia são permitidas para este tutorial. Para obter informações sobre a guia Avançado hello, consulte [Assistente de aplicativo do Azure publicação](http://msdn.microsoft.com/library/hh535756.aspx).
4. Em Olá **resumo** etapa, clique em **publicar**.

    ![Etapa de resumo](./media/cloud-services-dotnet-get-started/pubsummary.png)

   Olá **o Log de atividades do Azure** janela será aberta no Visual Studio.
5. Clique em detalhes da implantação do hello ícone tooexpand Olá seta para a direita.

    implantação de saudação pode demorar até too5 minutos ou mais toocomplete.

    ![Janela Log de atividade do Azure](./media/cloud-services-dotnet-get-started/waal.png)
6. Quando o status da implantação Olá for concluída, clique em Olá **URL do aplicativo Web** aplicativo hello de toostart.
7. Agora você pode testar o aplicativo hello por criar, exibir e editar alguns anúncios, como você fez quando você executou o aplicativo hello localmente.

> [!NOTE]
> Quando concluir teste, excluir ou parar serviço de nuvem hello. Mesmo se você não estiver usando o serviço de nuvem hello, ele é acúmulo de encargos porque os recursos de máquina virtual são reservados para ele. E se você deixá-lo em execução, qualquer um que encontrar sua URL poderá criar e exibir anúncios. Em Olá [portal do Azure](https://portal.azure.com), vá toohello **visão geral** guia para seu serviço de nuvem e, em seguida, clique em hello **excluir** botão na parte superior de saudação da página de saudação. Se você quiser apenas tootemporarily impedir que outros usuários acessem o site de saudação, clique em **parar** em vez disso. Nesse caso, os encargos continuarão tooaccrue. Você pode seguir uma saudação de toodelete procedimento semelhante conta de armazenamento e de banco de dados SQL quando você não precisa mais deles.
>
>

## <a name="create-hello-application-from-scratch"></a>Criar aplicativo hello a partir do zero
Se você ainda não tiver baixado [aplicativo hello concluída](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), faça isso agora. Você vai copiar arquivos de projeto Olá baixado no novo projeto de saudação.

Criando aplicativo da Contoso anúncios hello envolve Olá etapas a seguir:

* Criar um serviço de nuvem na solução Visual Studio.
* Atualizar e adicionar pacotes NuGet.
* Definir referências de projeto.
* Configurar cadeias de conexão.
* Adicionar arquivos de código.

Após a solução Olá é criada, você revisará código Olá projetos de serviço exclusivo toocloud e blobs do Azure e filas.

### <a name="create-a-cloud-service-visual-studio-solution"></a>Criar um serviço de nuvem na solução Visual Studio
1. No Visual Studio, escolha **novo projeto** de saudação **arquivo** menu.
2. No painel esquerdo de saudação do hello **novo projeto** caixa de diálogo caixa, expanda **Visual C#** e escolha **nuvem** modelos e, em seguida, escolha Olá **serviço de nuvem do Azure** modelo.
3. Nome do projeto hello e solução ContosoAdsCloudService e, em seguida, clique em **Okey**.

    ![Novo Projeto](./media/cloud-services-dotnet-get-started/newproject.png)
4. Em Olá **novo serviço de nuvem do Azure** caixa de diálogo caixa, adicione uma função web e uma função de trabalho. Nome de função de web hello ContosoAdsWeb e nome de função de trabalho Olá ContosoAdsWorker. (Use o ícone de lápis Olá em nomes de padrão de Olá Olá painel direito toochange das funções hello.)

    ![Novo Projeto de Serviço de Nuvem](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. Quando você vir Olá **novo projeto ASP.NET** caixa de diálogo função de web hello, escolha o modelo MVC hello e, em seguida, clique em **alterar autenticação**.

    ![Alterar Autenticação](./media/cloud-services-dotnet-get-started/chgauth.png)
6. Em Olá **alterar autenticação** caixa de diálogo caixa, escolha **sem autenticação**e, em seguida, clique em **Okey**.

    ![Sem Autenticação](./media/cloud-services-dotnet-get-started/noauth.png)
7. Em Olá **novo projeto ASP.NET** caixa de diálogo, clique em **Okey**.
8. Em **Solution Explorer**, com o botão direito solução hello (não um dos projetos de saudação) e escolha **Add - novo projeto**.
9. Em Olá **adicionar novo projeto** caixa de diálogo caixa, escolha **Windows** em **Visual C#** em Olá painel esquerdo e clique em Olá **biblioteca de classes** modelo.  
10. Projeto de saudação do nome *ContosoAdsCommon*e, em seguida, clique em **Okey**.

    É necessário tooreference saudação do Entity Framework contexto e hello modelo de dados de projetos de função da web e de trabalho. Como alternativa, você poderia definir classes de relacionada ao EF Olá no projeto de função web hello e referência de projeto do projeto de função de trabalho hello. Mas na abordagem alternativa de saudação, seu projeto de função de trabalho terá uma referência tooweb os assemblies que não precisa.

### <a name="update-and-add-nuget-packages"></a>Atualizar e adicionar pacotes NuGet
1. Olá abrir **gerenciar pacotes NuGet** caixa de diálogo de solução de saudação.
2. Na parte superior de saudação da janela hello, selecione **atualizações**.
3. Procure Olá *windowsazure* do pacote e se ele estiver na lista de Olá, selecioná-la e escolha tooupdate de projetos da web e de trabalho Olá nele e clique **atualização**.

    biblioteca de cliente de armazenamento Olá é atualizada com mais frequência do que os modelos de projeto do Visual Studio, você geralmente encontrará versão Olá toobe de necessidades de um projeto recém-criado atualizado.
4. Na parte superior de saudação da janela hello, selecione **procurar**.
5. Localize Olá *EntityFramework* NuGet do pacote e instalá-lo em todos os três projetos.
6. Localize Olá *Microsoft.WindowsAzure.ConfigurationManager* NuGet empacotar e instale-o no projeto de função de trabalho hello.

### <a name="set-project-references"></a>Definir referências de projeto
1. No projeto de ContosoAdsWeb de saudação, defina uma referência de projeto do ContosoAdsCommon toohello. Clique com botão direito Olá ContosoAdsWeb e, em seguida, clique em **referências** - **adicionar referências**. Em Olá **Gerenciador de referências** caixa de diálogo, selecione **solução – projetos** no painel esquerdo do hello, selecione **ContosoAdsCommon**e, em seguida, clique em **Okey**.
2. No projeto de ContosoAdsWorker de saudação, defina uma referência de projeto do ContosAdsCommon toohello.

    ContosoAdsCommon conterá saudação do Entity Framework dados modelo e o contexto de classe, que será usado por ambos os Olá front-end e back-end.
3. No projeto de ContosoAdsWorker hello, defina uma referência muito`System.Drawing`.

    Este assembly é usado pelo toothumbnails de imagens do hello tooconvert de back-end.

### <a name="configure-connection-strings"></a>Configurar cadeias de conexão
Nesta seção iremos configurar o Armazenamento do Azure e as cadeias de conexão do SQL para o teste local. instruções de implantação Olá anteriormente no tutorial Olá explicam como tooset a conexão Olá cadeias de caracteres para quando hello aplicativo é executado na nuvem hello.

1. No projeto de ContosoAdsWeb hello, Olá Abrir aplicativo Web. config e inserir a seguir Olá `connectionStrings` elemento após Olá `configSections` elemento.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Se você estiver usando o Visual Studio 2015 ou superior, substitua "v11.0" por "MSSQLLocalDB".
2. Salve suas alterações.
3. No projeto de ContosoAdsCloudService hello, clique com botão direito ContosoAdsWeb em **funções**e, em seguida, clique em **propriedades**.

    ![Propriedades da função](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. Em Olá **ContosAdsWeb [função]** janela Propriedades, clique em Olá **configurações** guia e, em seguida, clique em **Adicionar configuração**.

    Deixe **configuração do serviço** definido muito**todas as configurações de**.
5. Adicione uma configuração chamada *StorageConnectionString*. Definir **tipo** muito*ConnectionString*e defina **valor** muito*UseDevelopmentStorage = true*.

    ![Nova cadeia de conexão](./media/cloud-services-dotnet-get-started/scall.png)
6. Salve suas alterações.
7. Siga Olá tooadd do mesmo procedimento uma cadeia de caracteres de conexão de armazenamento nas propriedades da função ContosoAdsWorker hello.
8. Ainda no hello **ContosoAdsWorker [função]** janela Propriedades, adicione outra cadeia de caracteres de conexão:

   * Nome: ContosoAdsDbConnectionString
   * Tipo: String
   * Valor: Colar Olá a mesma cadeia de caracteres de conexão usada para o projeto de função web hello. (Olá exemplo a seguir é para Visual Studio 2013. Não se esqueça de saudação toochange fonte de dados se você copiar esse exemplo e você estiver usando o Visual Studio 2015 ou superior.)

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a>Adicionar arquivos de código
Nesta seção, você copiar arquivos de código da solução Olá baixado em nova solução de saudação. Olá seções a seguir mostrará e explicar as principais partes do código.

tooadd arquivos tooa projeto ou uma pasta, projeto de saudação do botão direito do mouse ou pasta e clique em **adicionar** - **Item existente**. Selecione os arquivos de saudação desejado e, em seguida, clique em **adicionar**. Se for perguntado se deseja tooreplace os arquivos existentes, clique em **Sim**.

1. No projeto de ContosoAdsCommon hello, exclua Olá *Class1. CS* de arquivos e adicionar em seu lugar Olá *Ad.cs* e *ContosoAdscontext.cs* arquivos de saudação baixou o projeto.
2. No projeto de ContosoAdsWeb Olá, adicione Olá seguintes arquivos de projeto Olá baixado.

   * *Global.asax.cs*  
   * Em Olá *exibições \ compartilhadas* pasta:  *\_cshtml*.
   * Em Olá *Views\Home* pasta: *cshtml*.
   * Em Olá *controladores* pasta: *AdController.cs*.
   * Em Olá *Views\Ad* pasta (criar pasta Olá primeiro): cinco *. cshtml* arquivos.
3. No projeto de ContosoAdsWorker hello, adicione *WorkerRole.cs* de saudação baixou o projeto.

Você agora pode compilar e executar o aplicativo hello conforme instruído anteriormente no tutorial hello e aplicativo hello usará recursos de emulador de armazenamento e de banco de dados local.

Olá, seções a seguir explicam o código de Olá Olá de tooworking relacionado com o ambiente do Azure, blobs e filas. Este tutorial não explica como controladores MVC toocreate e modos de exibição usando o scaffolding, como toowrite código do Entity Framework que funciona com bancos de dados do SQL Server ou Noções básicas de saudação de programação assíncrona no ASP.NET 4.5. Para obter informações sobre esses tópicos, consulte Olá recursos a seguir:

* [Introdução ao MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Introdução ao EF 6 e ao MVC 5](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* [Programação de tooasynchronous de Introdução no .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
arquivo de Ad.cs de saudação define um enum de categorias do ad e uma classe de entidade POCO para obter informações do ad.

```csharp
public enum Category
{
    Cars,
    [Display(Name="Real Estate")]
    RealEstate,
    [Display(Name = "Free Stuff")]
    FreeStuff
}

public class Ad
{
    public int AdId { get; set; }

    [StringLength(100)]
    public string Title { get; set; }

    public int Price { get; set; }

    [StringLength(1000)]
    [DataType(DataType.MultilineText)]
    public string Description { get; set; }

    [StringLength(1000)]
    [DisplayName("Full-size Image")]
    public string ImageURL { get; set; }

    [StringLength(1000)]
    [DisplayName("Thumbnail")]
    public string ThumbnailURL { get; set; }

    [DataType(DataType.Date)]
    [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
    public DateTime PostedDate { get; set; }

    public Category? Category { get; set; }
    [StringLength(12)]
    public string Phone { get; set; }
}
```

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
Olá classe ContosoAdsContext Especifica que a classe de Ad de saudação é usada em uma coleção de DbSet, que armazena em um banco de dados SQL do Entity Framework.

```csharp
public class ContosoAdsContext : DbContext
{
    public ContosoAdsContext() : base("name=ContosoAdsContext")
    {
    }
    public ContosoAdsContext(string connString)
        : base(connString)
    {
    }
    public System.Data.Entity.DbSet<Ad> Ads { get; set; }
}
```

classe de saudação tem dois construtores. Olá primeiro deles é usado pelo projeto da web de saudação e especifica o nome de saudação de uma cadeia de conexão que é armazenada no arquivo Web. config de saudação. construtor segundo Olá permite que você toopass na cadeia de caracteres de conexão real Olá usada pelo projeto de função de trabalho hello, pois ele não tem um arquivo Web. config. Você viu anteriormente em que essa cadeia de caracteres de conexão foi armazenada, e você verá posteriormente como código Olá recupera a cadeia de caracteres de conexão de saudação quando ele cria a classe DbContext de saudação.

### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Código que é chamado de hello `Application_Start` método cria um *imagens* contêiner de blob e uma *imagens* fila se ainda não existirem. Isso garante que sempre que você começar a usar uma nova conta de armazenamento, ou começar a usar o emulador de armazenamento Olá em um novo computador, fila e o contêiner de blob necessários Olá serão criados automaticamente.

Olá conta de armazenamento do código obtém acesso toohello usando a cadeia de conexão de armazenamento de saudação do hello *. cscfg* arquivo.

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

Em seguida, ele obtém uma referência toohello *imagens* contêiner de blob, cria o contêiner de saudação se ele ainda não existir, conjuntos de permissões e acesso no novo contêiner de saudação. Por padrão, novos contêineres somente permitir que os clientes com a conta de armazenamento blobs de tooaccess de credenciais. site de saudação precisa Olá blobs toobe público para que ele possa exibir imagens usando URLs que blobs de imagem toohello ponto.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

Um código semelhante obtém uma referência toohello *imagens* fila e cria uma nova fila. Nesse caso, nenhuma alteração de permissão é necessária.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb – \_Layout.cshtml
Olá *cshtml* arquivo define o nome do aplicativo Olá Olá cabeçalho e rodapé e cria uma entrada de menu "Anúncios".

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
Olá *Views\Home\Index.cshtml* arquivo exibe links de categoria na home page do hello. Olá links passam o valor inteiro Olá Olá `Category` enum em uma página de índice de anúncios de toohello variável de querystring.

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
Em Olá *AdController.cs* arquivo, chamadas de construtor Olá Olá `InitializeStorage` objetos de biblioteca de cliente de armazenamento do Azure do método toocreate que fornecem uma API para trabalhar com blobs e filas.

Em seguida, o código de saudação obtém uma referência toohello *imagens* contêiner de blob que você viu anteriormente na *Global.asax.cs*. Enquanto faz isso ele define uma [política de recuperação](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) padrão apropriada para um aplicativo Web. política de repetição de retirada exponencial saudação padrão pode travar Olá web app para mais de um minuto em várias tentativas para uma falha temporária. política de repetição de saudação especificada aqui aguarda três segundos após cada tente para backup toothree tentativas.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

Um código semelhante obtém uma referência toohello *imagens* fila.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

A maioria do código do controlador Olá é comum para trabalhar com um modelo de dados do Entity Framework usando uma classe DbContext. Uma exceção é hello HttpPost `Create` método, que carrega um arquivo e o salva no armazenamento de blob. associador de modelo Olá fornece um [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello método do objeto.

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

Se o usuário Olá selecionado tooupload um arquivo, código Olá carrega o arquivo hello, salva-o em um blob e atualiza o registro de banco de dados do Ad Olá com uma URL que aponta toohello blob.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

Olá código Olá carregamento está em Olá `UploadAndSaveBlobAsync` método. Ele cria um nome GUID para o blob de hello, carrega e salva Olá arquivo e retorna um blob de referência toohello salvada.

```csharp
private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
{
    string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
    CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
    using (var fileStream = imageFile.InputStream)
    {
        await imageBlob.UploadFromStreamAsync(fileStream);
    }
    return imageBlob;
}
```

Depois de saudação HttpPost `Create` método carrega um blob e atualizações Olá banco de dados, ele cria um tooinform de mensagem da fila desse processo de back-end que uma imagem está pronta para a miniatura de tooa de conversão.

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

Olá código para hello HttpPost `Edit` método é semelhante, exceto que se o usuário Olá seleciona um novo arquivo de imagem devem ser excluídos todos os blobs que já existem.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

Olá próximo exemplo mostra o código de saudação que exclui os blobs quando você exclui um anúncio.

```csharp
private async Task DeleteAdBlobsAsync(Ad ad)
{
    if (!string.IsNullOrWhiteSpace(ad.ImageURL))
    {
        Uri blobUri = new Uri(ad.ImageURL);
        await DeleteAdBlobAsync(blobUri);
    }
    if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
    {
        Uri blobUri = new Uri(ad.ThumbnailURL);
        await DeleteAdBlobAsync(blobUri);
    }
}
private static async Task DeleteAdBlobAsync(Uri blobUri)
{
    string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
    CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
    await blobToDelete.DeleteAsync();
}
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml e Details.cshtml
Olá *cshtml* arquivo exibe miniaturas com hello outros dados do ad.

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

Olá *Details.cshtml* arquivo exibe a imagem em tamanho normal hello.

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml e Edit.cshtml
Olá *Create.cshtml* e *Edit.cshtml* arquivos especificam que habilita Olá Olá do controlador tooget de codificação de formulário `HttpPostedFileBase` objeto.

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

Um `<input>` elemento informa Olá navegador tooprovide uma caixa de diálogo de seleção de arquivo.

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a>ContosoAdsWorker - WorkerRole.cs - Método OnStart
ambiente de função de trabalho do Azure Olá chama Olá `OnStart` método hello `WorkerRole` classe quando a função de trabalho Olá é Introdução e chama Olá `Run` método quando hello `OnStart` conclusão do método.

Olá `OnStart` método obtém a cadeia de conexão de banco de dados de saudação do hello *. cscfg* de arquivo e o transmite toohello Entity Framework DbContext classe. provedor de SQLClient Olá é usado por padrão, portanto Olá provedor não tem toobe especificado.

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

Depois disso, o método hello obtém uma conta de armazenamento do toohello de referência e cria a fila e o contêiner de blob Olá se não existirem. saudação de código que está toowhat semelhante que já vimos na função de web hello `Application_Start` método.

### <a name="contosoadsworker---workerrolecs---run-method"></a>ContosoAdsWorker - WorkerRole.cs - Método de execução
Olá `Run` método é chamado quando hello `OnStart` método termina o trabalho de inicialização. método Hello executa um loop infinito que observa para novas mensagens de fila e processa-os quando elas chegam.

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

Após cada iteração do loop Olá, não se foi encontrada nenhuma mensagem de fila, o programa hello suspenso por um segundo. Isso impede que funções de trabalho Olá incorrer em custos de transações de armazenamento e tempo excessivos do CPU. Olá Microsoft Customer Advisory Team informa uma história sobre um desenvolvedor que esqueceu tooinclude isso, implantado tooproduction e à esquerda para férias. Quando ele foi retornado, sua supervisão custo mais de férias hello.

Às vezes, conteúdo de saudação de uma mensagem da fila causa um erro no processamento. Isso é chamado de um *mensagem suspeita*, e se você acabou de registrou um erro e reiniciado loop hello, infinitamente tente tooprocess essa mensagem.  Portanto o bloco catch de saudação inclui um se instrução que verifica toosee quantas vezes Olá aplicativo tentou tooprocess Olá mensagem atual e se foram mais de 5 vezes, mensagem de saudação será excluída da fila de saudação.

`ProcessQueueMessage` é chamado quando uma mensagem em fila é encontrada.

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

Esse código lê a URL da imagem Olá Olá banco de dados tooget, converte a miniatura da saudação imagem tooa, salva a miniatura de saudação em um blob, atualiza o banco de dados de saudação com URL de blob em miniatura hello e exclui a mensagem da fila de saudação.

> [!NOTE]
> Olá código Olá `ConvertImageToThumbnailJPG` método usa classes no namespace System Drawing Olá para manter a simplicidade. No entanto, as classes nesse namespace Olá foram projetados para uso com o Windows Forms. Elas não têm suporte para uso em um serviço Windows ou ASP.NET. Para obter mais informações sobre opções de processamento de imagem, consulte [Geração dinâmica de imagem](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) e [Visão aprofundada de redimensionamento de imagens](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).
>
>

## <a name="troubleshooting"></a>Solucionar problemas
Caso algo não funciona enquanto você estiver seguindo as instruções de saudação neste tutorial, aqui estão alguns erros comuns e como tooresolve-los.

### <a name="serviceruntimeroleenvironmentexception"></a>ServiceRuntime.RoleEnvironmentException
Olá `RoleEnvironment` objeto é fornecido pelo Azure quando você executar um aplicativo no Azure ou ao executar localmente usando o emulador de computação do Azure hello.  Se você receber esse erro quando você estiver executando localmente, certifique-se de que você definiu o projeto de ContosoAdsCloudService hello como projeto de inicialização de saudação. Isso configura Olá toorun de projeto usando o emulador de computação do Azure hello.

Uma das coisas Olá Olá usada pelo aplicativo hello Azure RoleEnvironment para é tooget Olá conexão valores de cadeia que são armazenados no hello *. cscfg* arquivos, portanto, outra causa dessa exceção é uma cadeia de caracteres de conexão ausente. Certifique-se de que você criou configuração StorageConnectionString Olá tanto de nuvem e configurações locais no projeto de ContosoAdsWeb hello e que você criou duas cadeias de caracteres de conexão para ambas as configurações no projeto de ContosoAdsWorker hello. Se você fizer uma **Localizar tudo** pesquisa para StorageConnectionString na solução inteira hello, você verá ele 9 vezes nos arquivos de 6.

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a>Não é possível substituir tooport xxx. O valor abaixo do mínimo permitido para a nova porta é de 8080 para o protocolo http
Tente alterar o número da porta Olá usado pelo projeto da web de saudação. Clique com botão direito Olá ContosoAdsWeb e, em seguida, clique em **propriedades**. Clique em Olá **Web** guia e, em seguida, altere o número da porta de saudação em Olá **Url do projeto** configuração.

Para outra alternativa que pode resolver o problema de hello, consulte Olá seção a seguir.

### <a name="other-errors-when-running-locally"></a>Outros erros que podem ocorrer ao executar localmente
Por nuvem novo padrão projetos de serviço usam Olá computação do Azure emulator express toosimulate Olá ambiente do Azure. Esta é uma versão leve do emulador de computação completo hello e em Olá algumas condições emulador completo funcionará quando a versão express Olá não.  

toochange Olá emulador completo do projeto toouse hello, clique com botão direito Olá ContosoAdsCloudService e, em seguida, clique em **propriedades**. Em Olá **propriedades** clique Olá **Web** guia e, em seguida, clique em Olá **emulador completo Use** botão de opção.

No aplicativo de hello ordem toorun com o emulador completo hello, você tem tooopen Visual Studio com privilégios de administrador.

## <a name="next-steps"></a>Próximas etapas
Olá aplicativo Contoso anúncios intencionalmente foi mantida simple para obter um tutorial de Introdução. Por exemplo, ele não implementa [injeção de dependência](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) ou hello [repositório e unidade de trabalho padrões](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), não [usam uma interface para registro em log](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), ele não use [ Migrações do Code First EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) alterações do modelo de dados de toomanage ou [resiliência de Conexão EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transitório erros de rede e assim por diante.

Aqui estão alguns aplicativos de exemplo de serviço de nuvem que demonstram mais práticas de codificação reais, listadas do menos complexo toomore complexo:

* [PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31). Semelhante ao conceito tooContoso anúncios mas implementa recursos mais e mais práticas de codificação do mundo real.
* [Aplicativo multicamada de serviço de nuvem do Azure com tabelas, filas e blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36). Introduz as tabelas do Armazenamento do Azure, bem como blobs e filas. Com base em uma versão anterior de saudação do SDK do Azure para .NET, exigirá toowork algumas modificações com a versão atual do hello.
* [Noções Básicas sobre Serviço de Nuvem no Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Um exemplo abrangente que demonstra uma ampla variedade de práticas recomendadas, produzido pelo grupo Microsoft Patterns e práticas recomendadas de saudação.

Para obter informações gerais sobre o desenvolvimento para a nuvem hello, consulte [criando aplicativos de nuvem do mundo Real com o Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).

Para um vídeo de Introdução tooAzure armazenamento práticas recomendadas e padrões, consulte [armazenamento do Microsoft Azure – o que há de novo, práticas recomendadas e padrões](http://channel9.msdn.com/Events/Build/2014/3-628).

Para obter mais informações, consulte Olá recursos a seguir:

* [Serviços de nuvem do Azure Parte 1: Introdução](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [Como os serviços de nuvem toomanage](cloud-services-how-to-manage.md)
* [Armazenamento do Azure](/documentation/services/storage/)
* [Como o provedor de serviço toochoose uma nuvem](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
