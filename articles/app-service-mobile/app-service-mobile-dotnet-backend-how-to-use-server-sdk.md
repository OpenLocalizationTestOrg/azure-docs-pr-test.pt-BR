---
title: "toowork aaaHow com o servidor de back-end .NET Olá SDK para aplicativos móveis | Microsoft Docs"
description: "Saiba como toowork com hello o SDK do servidor de back-end do .NET para aplicativos de celular do serviço de aplicativo do Azure."
keywords: "serviço de aplicativo, serviço de aplicativo do azure, aplicativo móvel, serviço móvel, escala, escalonável, implantação de aplicativo, implantação de aplicativo do azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a>Trabalhar com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

Este tópico mostra como toouse Olá servidor de back-end .NET SDK no principais cenários de aplicativos de celular do serviço de aplicativo do Azure. Olá SDK de aplicativos móveis do Azure ajuda você a trabalhar com clientes móveis do seu aplicativo ASP.NET.

> [!TIP]
> Olá [server .NET SDK para aplicativos móveis do Azure] [ 2] é o código-fonte aberto no GitHub. repositório de saudação contém todo o código fonte incluindo o conjunto de testes de unidade do hello todo servidor SDK e alguns projetos de exemplo.
>
>

## <a name="reference-documentation"></a>Documentação de referência
documentação de referência Olá para o servidor de saudação SDK está localizada aqui: [referência do .NET de aplicativos do Azure Mobile][1].

## <a name="create-app"></a>Como criar um back-end do aplicativo móvel do .NET
Se você estiver iniciando um novo projeto, você pode criar um aplicativo de serviço de aplicativo usando o hello [portal do Azure] ou o Visual Studio. Você pode executar Olá aplicativo de serviço de aplicativo localmente ou publicar Olá projeto tooyour baseado em nuvem do serviço de aplicativo aplicativo móvel.

Se você estiver adicionando um projeto existente do tooan recursos móveis, consulte Olá [baixar e inicializar Olá SDK](#install-sdk) seção.

### <a name="create-a-net-backend-using-hello-azure-portal"></a>Criar um back-end .NET usando Olá portal do Azure
toocreate um back-end móvel do serviço de aplicativo, o execute Olá [tutorial de início rápido] [ 3] ou siga estas etapas:

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

Em Olá *começar* folha, em **criar uma tabela API**, escolha **c#** como seu **idioma de back-end**. Clique em **baixar**, extraia o computador local do projeto compactado arquivos tooyour e abra a solução Olá no Visual Studio.

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a>Criar um back-end do .NET usando o Visual Studio 2013 e o Visual Studio 2015
Instalar Olá [SDK do Azure para .NET] [ 4] (versão 2.9.0 ou posterior) toocreate um projeto de aplicativos do Azure Mobile no Visual Studio. Depois de instalar o SDK do hello, crie um aplicativo ASP.NET usando Olá etapas a seguir:

1. Olá abrir **novo projeto** caixa de diálogo (de *arquivo* > **novo** > **projeto...** ).
2. Expanda **Modelos** > **Visual C#** e selecione **Web**.
3. Selecione **Aplicativo Web do ASP.NET**.
4. Preencha o nome do projeto hello. Em seguida, clique em **OK**.
5. Em *Modelos do ASP.NET 4.5.2*, selecione **Aplicativo Móvel do Azure**. Verificar **Host na nuvem Olá** toocreate um back-end móvel em Olá toowhich pode publicar esse projeto em nuvem.
6. Clique em **OK**.

## <a name="install-sdk"></a>Como: baixar e inicializar Olá SDK
Olá SDK está disponível em [NuGet.org]. Este pacote inclui Olá funcionalidade básica necessária tooget iniciado usando Olá SDK. tooinitialize Olá SDK, você precisa tooperform ações Olá **HttpConfiguration** objeto.

### <a name="install-hello-sdk"></a>Instalar o SDK de saudação
Olá tooinstall SDK, com o botão direito no projeto do servidor de saudação no Visual Studio, selecione **gerenciar pacotes NuGet**, pesquise Olá [Microsoft.Azure.Mobile.Server] do pacote e, em seguida, clique em  **Instalar**.

### <a name="server-project-setup"></a>Inicializar projeto de servidor de saudação
Um projeto do servidor de back-end .NET é inicializado semelhante tooother projetos do ASP.NET, incluindo uma classe de inicialização OWIN. Certifique-se de que você referenciou pacote do NuGet Olá `Microsoft.Owin.Host.SystemWeb`. tooadd dessa classe no Visual Studio, clique com botão direito no projeto do servidor e selecione **adicionar** >
**Novo Item**, em seguida, **Web**  >  ** Geral** > **classe de inicialização OWIN**.  Uma classe é gerada com hello atributos a seguir:

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

Em Olá `Configuration()` método de sua classe de inicialização OWIN, use um **HttpConfiguration** ambiente do objeto tooconfigure Olá os aplicativos móveis do Azure.
saudação de exemplo a seguir inicializa o projeto do servidor de saudação não tem recursos adicionados:

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

tooenable os recursos individuais, você deve chamar os métodos de extensão no hello **MobileAppConfiguration** objeto antes de chamar **ApplyTo**. Por exemplo, Olá código a seguir adiciona padrão Olá roteia controladores tooall API que têm o atributo Olá `[MobileAppController]` durante a inicialização:

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

início rápido do servidor de saudação do hello chamadas portais do Azure **UseDefaultConfiguration()**. Este toohello equivalente após a instalação:

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

métodos de extensão Olá usados são:

* `AddMobileAppHomeController()`fornece a home page do saudação padrão os aplicativos móveis do Azure.
* `MapApiControllers()`fornece recursos personalizados de API para controladores WebAPI decorados com hello `[MobileAppController]` atributo.
* `AddTables()`Fornece um mapeamento de saudação `/tables` controladores tootable pontos de extremidade.
* `AddTablesWithEntityFramework()`é uma abreviada para Olá mapeamento `/tables` controladoras baseadas em pontos de extremidade usando o Entity Framework.
* `AddPushNotifications()` fornece um método simples de registro de dispositivos para Hubs de Notificação.
* `MapLegacyCrossDomainController()` fornece os cabeçalhos de CORS padrão para o desenvolvimento local.

### <a name="sdk-extensions"></a>Extensões SDK
Olá pacotes do NuGet com base em extensão a seguir fornece vários recursos móveis que podem ser usados pelo seu aplicativo. Habilitar extensões durante a inicialização usando Olá **MobileAppConfiguration** objeto.

* [Microsoft.Azure.Mobile.Server.Quickstart] suporta Olá configuração básica de aplicativos móveis. Configuração toohello adicionado por chamada hello **UseDefaultConfiguration** método de extensão durante a inicialização. Essa extensão inclui as seguintes extensões: Notificações, Autenticação, Entidade, Tabelas, pacotes Crossdomain e Home. Este pacote é usado pelo Olá Quickstart de aplicativos móveis disponíveis no hello portal do Azure.
* [Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) implementa o padrão de saudação *este aplicativo móvel estiver em execução página* para a raiz do site hello. Adicionar configuração toohello chamando o **AddMobileAppHomeController** método de extensão.
* [Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) inclui classes para trabalhar com dados e define o pipeline de dados hello. Adicionar configuração toohello Olá chamada **AddTables** método de extensão.
* [Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) permite que os dados de tooaccess saudação do Entity Framework no hello banco de dados SQL. Adicionar configuração toohello Olá chamada **AddTablesWithEntityFramework** método de extensão.
* [Microsoft.Azure.Mobile.Server.Authentication] habilita a autenticação e conjuntos de backup Olá OWIN middleware usado toovalidate tokens. Adicionar configuração toohello Olá chamada **AddAppServiceAuthentication** e **IAppBuilder**. **UseAppServiceAuthentication** métodos de extensão.
* [Microsoft.Azure.Mobile.Server.Notifications] permite as notificações por push e define um ponto de extremidade de registro push. Adicionar configuração toohello Olá chamada **AddPushNotifications** método de extensão.
* [Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) cria um controlador que serve dados toolegacy navegadores da web do seu aplicativo móvel. Adicionar configuração toohello chamando o **MapLegacyCrossDomainController** método de extensão.
* [Microsoft.Azure.Mobile.Server.Login] fornece um método de AppServiceLoginHandler.CreateToken() hello, que é um método estático usado nos cenários de autenticação personalizada.

## <a name="publish-server-project"></a>Como: publicar projeto do servidor de saudação
Esta seção mostra como toopublish seu back-end .NET de projeto do Visual Studio. Você também pode implantar seu projeto de back-end usando Git ou qualquer um dos Olá outros métodos abordados Olá [documentação de implantação do serviço de aplicativo do Azure](../app-service-web/web-sites-deploy.md).

1. No Visual Studio, reconstrua pacotes do NuGet Olá projeto toorestore.
2. No Gerenciador de soluções, projetos de saudação com o botão direito, clique em **publicar**. Olá primeira vez que você publicar, você precisa toodefine um perfil de publicação. Quando já tiver um perfil definido, selecione-o e clique em **Publicar**.
3. Se for solicitado tooselect um destino de publicação, clique em **serviço de aplicativo do Microsoft Azure** > **próximo**, e (se necessário) entrar com suas credenciais do Azure.
   O Visual Studio baixa e armazena suas configurações de publicação com segurança diretamente do Azure.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. Escolha sua **Assinatura**, selecione o **Tipo de Recurso** em **Exibição**, expanda **Aplicativo Móvel**, clique no back-end do Aplicativo Móvel e então clique em **OK**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. Verifique se Olá publicar informações de perfil e clique em **publicar**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    Quando o back-end do aplicativo móvel for publicado com êxito, você verá uma página de aterrissagem indicando êxito.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <a name="define-table-controller"></a> Como definir um controlador de tabela
Defina um controlador de tabela tooexpose os clientes toomobile da tabela de SQL.  A configuração de um Controlador de Tabela exige três etapas:

1. Criar uma classe DTO (Objeto de Transferência de Dados).
2. Configure uma referência de tabela no hello classe DbContext Mobile.
3. Criar um controlador de tabela.

Um DTO (objeto de transferência de dados) é um objeto C# simples que herda de `EntityData`.  Por exemplo:

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

Olá DTO é a tabela de saudação de toodefine usado no banco de dados SQL hello.  Olá toocreate entrada do banco de dados, adicione um `DbSet<>` propriedade à saudação DbContext que você está usando.  No modelo de projeto saudação padrão para aplicativos móveis do Azure, hello DbContext é chamado `Models\MobileServiceContext.cs`:

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

Se você tiver Olá instalado SDK do Azure, agora você pode criar um controlador de tabela do modelo da seguinte maneira:

1. Com o botão direito na pasta de controladores hello e selecione **adicionar** > **controlador...** .
2. Selecione Olá **controlador de tabela em aplicativos do Azure Mobile** opção e, em seguida, clique em **adicionar**.
3. Em Olá **Adicionar controlador** caixa de diálogo:
   * Em Olá **classe modelo** lista suspensa, selecione o novo DTO.
   * Em Olá **DbContext** suspenso, a classe do hello selecione DbContext de serviço móvel.
   * nome do controlador Olá é criado para você.
4. Clique em **Adicionar**.

projeto do servidor de saudação quickstart contém um exemplo de um simples **TodoItemController**.

### <a name="adjust-pagesize"></a>Como: ajustar o tamanho de paginação da tabela de saudação
Por padrão, os Aplicativos Móveis do Azure retornam 50 registros por solicitação.  Paginação garante que o cliente Olá não obstruir o servidor de saudação nem de thread da interface do usuário por muito tempo, garantindo uma boa experiência do usuário. tamanho de paginação da tabela toochange hello, do lado do servidor de saudação do aumento "consulta o tamanho permitido" e hello cliente página tamanho saudação do lado do servidor "tamanho de consulta permitido" é ajustado usando Olá `EnableQuery` atributo:

    [EnableQuery(PageSize = 500)]

Certifique-se de saudação PageSize é hello mesmo ou maior que tamanho Olá solicitado pelo cliente hello.  Consulte a documentação de como de cliente específico de toohello para obter detalhes sobre como alterar o tamanho de página do cliente hello.

## <a name="how-to-define-a-custom-api-controller"></a>Como definir um controlador da API personalizada
controlador de API personalizada Olá fornece hello mais básico funcionalidade tooyour aplicativo móvel backend ao expor um ponto de extremidade. Você pode registrar um controlador de API específicas para dispositivos móveis usando o atributo Olá [MobileAppController]. Olá `MobileAppController` atributo registra rota hello, configura o serializador JSON de aplicativos móveis hello e ativa a [verificação de versão de cliente](app-service-mobile-client-and-server-versioning.md).

1. No Visual Studio, pasta de controladores de saudação com o botão direito, em seguida, clique em **adicionar** > **controlador**, selecione **Web API 2 controlador&mdash;vazio** e Clique em **adicionar**.
2. Forneça um **Nome do controlador**, como `CustomController`, e clique em **Adicionar**.
3. No novo arquivo de classe de controlador hello, adicione o seguinte de saudação usando a instrução:

        using Microsoft.Azure.Mobile.Server.Config;
4. Aplicar Olá **[MobileAppController]** definição de classe do controlador toohello API, como no exemplo a seguir de saudação do atributo:

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. No arquivo de App_Start/Startup.MobileApp.cs, adicione uma chamada toohello **MapApiControllers** método de extensão, como no exemplo a seguir de saudação:

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

Você também pode usar o hello `UseDefaultConfiguration()` método de extensão, em vez de `MapApiControllers()`. Qualquer controlador que não tenha o **MobileAppControllerAttribute** aplicado ainda poderá ser acessado pelos clientes, mas não será consumido corretamente por clientes que usem qualquer SDK do cliente do Aplicativo Móvel.

## <a name="how-to-work-with-authentication"></a>Como trabalhar com autenticação
Aplicativos móveis do Azure usa a autenticação do serviço de aplicativo / autorização toosecure seu móvel back-end.  Esta seção mostra como Olá tooperform tarefas relacionadas à autenticação no seu projeto do servidor de back-end .NET a seguir:

* [Como: adicionar um projeto do servidor de autenticação tooa](#add-auth)
* [Como usar a autenticação personalizada para o seu aplicativo](#custom-auth)
* [Como recuperar informações do usuário autenticado](#user-info)
* [Como restringir o acesso a dados para usuários autorizados](#authorize)

### <a name="add-auth"></a>Como: adicionar um projeto do servidor de autenticação tooa
Você pode adicionar o projeto do servidor de autenticação tooyour estendendo Olá **MobileAppConfiguration** objeto e configurar o middleware OWIN. Quando você instala o hello [Microsoft.Azure.Mobile.Server.Quickstart] Olá de pacote e chame **UseDefaultConfiguration** método de extensão, você pode ignorar toostep 3.

1. No Visual Studio, instalar Olá [Microsoft.Azure.Mobile.Server.Authentication] pacote.
2. No arquivo de projeto Startup.cs hello, adicionar Olá a seguinte linha de código no início de saudação do hello **configuração** método:

        app.UseAppServiceAuthentication(config);

    Este componente de middleware OWIN valida os tokens emitidos pelo gateway do serviço de aplicativo hello associado.
3. Adicionar Olá `[Authorize]` controlador do atributo tooany ou método que requer autenticação.

toolearn sobre como tooauthenticate clientes tooyour back-end de aplicativos móveis, consulte [adicionar autenticação tooyour aplicativo](app-service-mobile-ios-get-started-users.md).

### <a name="custom-auth"></a>Como usar a autenticação personalizada para o seu aplicativo
Se você não desejar toouse um dos provedores de autenticação/autorização do serviço de aplicativo hello, você pode implementar seu próprio sistema de logon. Instalar Olá [Microsoft.Azure.Mobile.Server.Login] tooassist com geração de token de autenticação do pacote.  Forneça seu próprio código para validar as credenciais do usuário. Por exemplo, você pode comparar com senhas com sal e hash aplicados em um banco de dados. O exemplo hello abaixo, Olá `isValidAssertion()` método (definido em outro lugar) é responsável por essas verificações.

autenticação personalizada Olá é exposta pelo criando um ApiController e expondo `register` e `login` ações. cliente de saudação deve usar uma personalizado da interface do usuário toocollect Olá informações Olá usuário.  informações de saudação são chamada de API de toohello enviado com um padrão HTTP POST. Depois que o servidor de saudação valida asserção Olá, é emitido um token usando Olá `AppServiceLoginHandler.CreateToken()` método.  Olá ApiController **não** usar Olá `[MobileAppController]` atributo.

Uma ação `login` de exemplo:

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

No hello anterior de exemplo, LoginResult e LoginResultUser são serializáveis objetos que expõem propriedades necessárias. cliente Olá espera toobe de respostas de logon retornado como objetos JSON do formulário de saudação:

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

Olá `AppServiceLoginHandler.CreateToken()` método inclui um *público* e um *emissor* parâmetro. Ambos os parâmetros são definidos toohello URL da raiz do aplicativo, usando o esquema do hello HTTPS. Da mesma forma, você deve definir *secretKey* toobe valor de saudação do seu aplicativo de autenticação de chave. Não distribua Olá chave em um cliente de assinatura, que pode ser usado toomint chaves e representar usuários. Você pode obter Olá assinatura de chave enquanto hospedado no serviço de aplicativo referenciando Olá *site\_AUTH\_assinatura\_chave* variável de ambiente. Se for necessário em um contexto de depuração local, siga as instruções de Olá Olá [depuração Local com a autenticação](#local-debug) seção chave de saudação tooretrieve e armazená-lo como uma configuração de aplicativo.

token de saudação emitida também pode incluir outras declarações e uma data de expiração.  No mínimo, o token emitida de saudação deve incluir um assunto (**sub**) de declaração.

Você pode dar suporte a cliente padrão Olá `loginAsync()` método sobrecarregando rota de autenticação hello.  Se o cliente Olá chama `client.loginAsync('custom');` toolog no, a rota deve ser `/.auth/login/custom`.  Você pode definir a rota Olá para Olá autenticação personalizada controlador usando `MapHttpRoute()`:

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> Usando Olá `loginAsync()` abordagem garante que está anexado a esse token de autenticação Olá tooevery chamada subsequente toohello serviço.
>
>

### <a name="user-info"></a>Como recuperar informações do usuário autenticado
Quando um usuário é autenticado pelo serviço de aplicativo, você pode acessar Olá atribuída a ID de usuário e outras informações no seu código de back-end do .NET. informações de usuário de saudação podem ser usadas para tomar decisões de autorização na Olá back-end. Olá código a seguir obtém Olá ID de usuário associado a uma solicitação:

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

Olá SID é derivado de ID de usuário específica do provedor hello e é estático para um determinado usuário e o provedor de logon.  Olá SID é nula para tokens de autenticação inválido.

O Serviço de Aplicativo também permite solicitar declarações específicas do provedor de logon. Cada provedor de identidade pode fornecer mais informações usando o SDK do provedor de identidade.  Por exemplo, você pode usar o hello Facebook Graph API para obter informações de amigos.  Você pode especificar as declarações que são solicitadas na folha de provedor de saudação em Olá portal do Azure. Algumas declarações exigem configuração adicional com o provedor de identidade hello.

saudação de chamadas de código a seguir Olá **GetAppServiceIdentityAsync** extensão método tooget Olá credenciais de logon, que incluem solicitações de token toomake necessário acesso Olá contra Olá Graph API do Facebook:

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

Adicione um usando a instrução para `System.Security.Principal` tooprovide Olá **GetAppServiceIdentityAsync** método de extensão.

### <a name="authorize"></a>Como restringir o acesso a dados para usuários autorizados
Na seção anterior do hello, mostramos como tooretrieve Olá ID de usuário de um usuário autenticado. Você pode restringir o acesso toodata e outros recursos com base nesse valor. Por exemplo, adicionando um tootables de coluna de ID de usuário e filtrando resultados de consulta Olá por ID de usuário de saudação são um toolimit de maneira simples retornada dados somente tooauthorized os usuários. Olá código a seguir retorna linhas de dados somente quando Olá SID corresponde ao valor da coluna de ID de usuário Olá na tabela TodoItem de saudação:

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

Olá `Query()` método retorna um `IQueryable` que podem ser manipulados por filtragem de toohandle LINQ.

## <a name="how-to-add-push-notifications-tooa-server-project"></a>Como: adicionar um projeto do servidor de tooa de notificações de push
Adicionar projeto do servidor de tooyour de notificações de push estendendo Olá **MobileAppConfiguration** objeto e a criação de um cliente de Hubs de notificação.

1. No Visual Studio, clique com botão direito Olá servidor e clique em **gerenciar pacotes NuGet**, procure `Microsoft.Azure.Mobile.Server.Notifications`, em seguida, clique em **instalar**.
2. Repita essa saudação de tooinstall etapa `Microsoft.Azure.NotificationHubs` pacote, que inclui a biblioteca de cliente Olá Hubs de notificação.
3. Em App_Start/Startup.MobileApp.cs e adicione uma chamada toohello **AddPushNotifications()** método de extensão durante a inicialização:

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. Adicione Olá código que cria um cliente de Hubs de notificação a seguir:

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

Agora você pode usar o hello Hubs de notificação toosend push notificações tooregistered os dispositivos cliente. Para obter mais informações, consulte [adicionar push notificações tooyour aplicativo](app-service-mobile-ios-get-started-push.md). toolearn mais sobre Hubs de notificação, consulte [visão geral de Hubs de notificação](../notification-hubs/notification-hubs-push-notification-overview.md).

## <a name="tags"></a>Como habilitar envios direcionados por push usando marcações
Hubs de notificação permite enviar notificações destino toospecific registros usando marcas. Várias marcações são criadas automaticamente:

* Olá ID de instalação identifica um dispositivo específico.
* Olá Id de usuário com base em Olá autenticado SID identifica um usuário específico.

Olá instalação ID pode ser acessado de saudação **installationId** propriedade Olá **MobileServiceClient**.  Olá exemplo a seguir mostra como usar um tooadd de ID de instalação uma marca tooa específicas de instalação em Hubs de notificação:

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

Marcas fornecidas pelo cliente Olá durante o registro de notificação por push são ignoradas pelo back-end de saudação durante a criação de instalação de saudação. tooenable tooadd um cliente marcas toohello instalação, você deve criar uma API personalizada que adiciona marcas usando Olá anterior padrão.

Consulte [marcas de notificação por push de cliente adicionado] [ 5] no exemplo de início rápido concluído Olá serviço de aplicativo móvel de aplicativos para obter um exemplo.

## <a name="push-user"></a>Como: enviar por push notificações tooan autenticou o usuário
Quando um usuário autenticado se registra para notificações de push, uma marca de identificação do usuário é adicionada automaticamente toohello registro. Usando essa marca, você pode enviar por push dispositivos de tooall notificações registrados por aquela pessoa. Olá código a seguir obtém Olá SID do usuário que fez a solicitação e envia um registro de dispositivo do modelo push notificação tooevery para essa pessoa:

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

Ao se registrar para notificações por push de um cliente autenticado, verifique se a autenticação foi concluída antes de tentar o registro. Para obter mais informações, consulte [Push toousers] [ 6] no exemplo de início rápido concluído Olá serviço de aplicativo móvel de aplicativos de back-end .NET.

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a>Como: depurar e solucionar problemas de saudação .NET SDK do servidor
O Serviço de Aplicativo do Azure fornece várias técnicas de depuração e de solução de problemas para aplicativos ASP.NET.

* [Monitorando um Serviço de Aplicativo do Azure](../app-service-web/web-sites-monitor.md)
* [Habilitar o registro em log de diagnósticos no Serviço de Aplicativo do Azure](../app-service-web/web-sites-enable-diagnostic-log.md)
* [Solucionar problemas de um Serviço de Aplicativo do Azure no Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a>Registro em log
Você pode escrever tooApp logs de diagnóstico de serviço usando a gravação de rastreamento ASP.NET padrão hello. Antes de você pode gravar logs de toohello, você deve habilitar o diagnóstico em seu back-end do aplicativo móvel.

tooenable logs toohello de diagnóstico e de gravação:

1. Siga as etapas de saudação em [como diagnóstico tooenable](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).
2. Adicione o seguinte Olá usando a instrução no arquivo de código:

        using System.Web.Http.Tracing;
3. Crie um toowrite do gravador de rastreamento de saudação .NET back-end toohello logs de diagnóstico, da seguinte maneira:

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. Republicar o projeto de servidor e acessar Olá aplicativo móvel back-end tooexecute Olá caminho de código com o log de saudação.
5. Baixar e avaliar logs hello, conforme descrito em [como: baixar logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).

### <a name="local-debug"></a>Depuração local com autenticação
Você pode executar o aplicativo localmente tootest alterações antes de publicá-los toohello nuvem. Para a maioria dos back-ends dos Aplicativos Móveis do Azure, pressione *F5* enquanto estiver no Visual Studio. No entanto, há algumas considerações adicionais ao usar a autenticação.

Você deve ter um aplicativo móvel com base em nuvem com o aplicativo autenticação/autorização do serviço configurado, e o cliente deve ter um ponto de extremidade de nuvem Olá especificado como o host de logon alternativo hello. Consulte a documentação de saudação para sua plataforma de cliente para etapas específicas de saudação necessárias.

Verifique se seu back-end móvel tem o [Microsoft.Azure.Mobile.Server.Authentication] instalado. Em seguida, adicione seguinte hello, depois na classe de inicialização do aplicativo OWIN `MobileAppConfiguration` foi aplicada tooyour `HttpConfiguration`:

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

Em Olá anterior de exemplo, você deve configurar Olá *authAudience* e *authIssuer* configurações de aplicativo no Web. config arquivo tooeach ser a URL da raiz do aplicativo, usando Olá HTTPS esquema. Da mesma forma, você deve definir *authSigningKey* toobe valor de saudação do seu aplicativo de autenticação de chave.
chave de assinatura de saudação tooobtain:

1. Navegue tooyour aplicativo dentro Olá [portal do Azure]
2. Clique em **Ferramentas**, **Kudu**, **Ir**.
3. No site de gerenciamento Kudu hello, clique em **ambiente**.
4. Localizar o valor de saudação para *site\_AUTH\_assinatura\_chave*.

Olá usar assinatura de chave para Olá *authSigningKey* parâmetro em sua configuração de aplicativo local.  Seu back-end móvel agora está equipado toovalidate tokens quando em execução localmente, cliente Olá obtém o token de saudação do ponto de extremidade Olá baseado em nuvem.

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[portal do Azure]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
