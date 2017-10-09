---
title: aaaHow toocreate um aplicativo Web com Redis Cache | Microsoft Docs
description: Saiba como toocreate um aplicativo Web com o Cache Redis
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 454e23d7-a99b-4e6e-8dd7-156451d2da7c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: hero-article
ms.date: 05/09/2017
ms.author: sdanie
ms.openlocfilehash: d3e6df97b06fdf9032570dc360944be4bd7715de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-web-app-with-redis-cache"></a>Como toocreate um aplicativo Web com o Cache Redis
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Este tutorial mostra como toocreate e implantar um aplicativo de web de tooa de aplicativo da web do ASP.NET no serviço de aplicativo do Azure usando o Visual Studio de 2017. aplicativo de exemplo Hello exibe uma lista de estatísticas de banco de dados e mostra diferentes maneiras toouse Cache Redis do Azure toostore e recuperar dados do cache de saudação. Quando você concluir o tutorial hello, você terá um aplicativo web em execução que lê e grava o banco de dados de tooa, otimizada com Cache Redis do Azure e hospedado no Azure.

Você aprenderá a:

* Como toocreate um ASP.NET MVC 5 aplicativo da web no Visual Studio.
* Como tooaccess dados de um banco de dados usando o Entity Framework.
* Como tooimprove taxa de transferência de dados e reduzir a carga do banco de dados, armazenar e recuperar dados usando o Cache Redis do Azure.
* Como toouse uma Redis classificados conjunto tooretrieve Olá top 5 equipes.
* Como tooprovision Olá recursos do Azure para o aplicativo hello usando um modelo do Gerenciador de recursos.
* Como toopublish Olá tooAzure de aplicativo usando o Visual Studio.

## <a name="prerequisites"></a>Pré-requisitos
tutorial de saudação toocomplete, você deve ter Olá pré-requisitos a seguir.

* [Conta do Azure](#azure-account)
* [Visual Studio de 2017 com hello Azure SDK para .NET](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a>Conta do Azure
Você precisa de um tutorial de saudação toocomplete conta do Azure. Você pode:

* [Abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). Você obtém créditos que podem ser usado tootry out paga serviços do Azure. Mesmo depois de saudação créditos são esgotados, você pode manter Olá conta e usar os recursos e serviços do Azure gratuitos.
* [Ativar benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). Todos os meses, sua assinatura do MSDN lhe oferece créditos que podem ser usados para serviços pagos do Azure.

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a>Visual Studio de 2017 com hello Azure SDK para .NET
Olá tutorial destina 2017 do Visual Studio com hello [SDK do Azure para .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools). Olá 2.9.5 do SDK do Azure está incluído no instalador do Visual Studio hello.

Se você tiver o Visual Studio 2015, você pode seguir o tutorial Olá Olá [SDK do Azure para .NET](../dotnet-sdk.md) 2.8.2 ou posterior. [Download hello SDK mais recente do Azure para Visual Studio 2015 aqui](http://go.microsoft.com/fwlink/?linkid=518003). O Visual Studio é instalado automaticamente com hello SDK se você ainda não o fez. Algumas telas podem parecer diferentes das ilustrações Olá mostradas neste tutorial.

Se você tiver o Visual Studio 2013, você pode [download hello SDK mais recente do Azure para Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322). Algumas telas podem parecer diferentes das ilustrações Olá mostradas neste tutorial.

## <a name="create-hello-visual-studio-project"></a>Criar o projeto do Visual Studio Olá
1. Abra o Visual Studio e clique em **Arquivo**, **Novo**, **Projeto**.
2. Expanda Olá **Visual C#** nó Olá **modelos** lista, selecione **nuvem**e clique em **aplicativo Web ASP.NET**. Verifique se **.NET Framework 4.5.2** ou superior está selecionado.  Tipo **ContosoTeamStats** em Olá **nome** caixa de texto e clique em **Okey**.
   
    ![Criar projeto][cache-create-project]
3. Selecione **MVC** como o tipo de projeto hello. 

    Certifique-se de que **sem autenticação** é especificado para Olá **autenticação** configurações. Dependendo de sua versão do Visual Studio, o padrão de saudação pode ser definido toosomething else. toochange-la, clique em **alterar autenticação** e selecione **sem autenticação**.

    Se você estiver seguindo junto com o Visual Studio 2015, desmarque Olá **Host na nuvem Olá** caixa de seleção. Você vai [provisionar Olá recursos do Azure](#provision-the-azure-resources) e [publicar Olá aplicativo tooAzure](#publish-the-application-to-azure) nas etapas subsequentes no tutorial de saudação. Para obter um exemplo de provisionamento de um aplicativo da web do serviço de aplicativo do Visual Studio, deixando **Host na nuvem Olá** marcada, consulte [começar com aplicativos Web no serviço de aplicativo do Azure, usando ASP.NET e Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).
   
    ![Selecionar modelo de projeto][cache-select-template]
4. Clique em **Okey** toocreate projeto de saudação.

## <a name="create-hello-aspnet-mvc-application"></a>Criar hello aplicativo ASP.NET MVC
Essa seção do tutorial hello, você criará Olá básica o aplicativo que lê e exibe estatísticas de banco de dados.

* [Adicionar o pacote do NuGet do Entity Framework Olá](#add-the-entity-framework-nuget-package)
* [Adicionar modelo Olá](#add-the-model)
* [Adicionar controlador Olá](#add-the-controller)
* [Configurar os modos de exibição de saudação](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a>Adicionar o pacote do NuGet do Entity Framework Olá

1. Clique em **NuGet Package Manager**, **Package Manager Console** de saudação **ferramentas** menu.
2. Execução hello seguinte comando do hello **Package Manager Console** janela.
    
    ```
    Install-Package EntityFramework
    ```

Para obter mais informações sobre este pacote, consulte Olá [EntityFramework](https://www.nuget.org/packages/EntityFramework/) página NuGet.

### <a name="add-hello-model"></a>Adicionar modelo Olá
1. Clique com o botão direito do mouse em **Modelos** no **Gerenciador de Soluções** e escolha **Adicionar**, **Classe**. 
   
    ![Adicionar modelo][cache-model-add-class]
2. Digite `Team` para o nome da classe hello e clique em **adicionar**.
   
    ![Adicionar classe de modelo][cache-model-add-class-dialog]
3. Substituir saudação `using` instruções na parte superior de saudação do hello `Team.cs` arquivo com os seguintes Olá `using` instruções.

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. Substituir a definição de saudação do hello `Team` classe com hello seguindo o trecho de código que contém atualizada `Team` classe definição, bem como outras classes de auxiliar de Entity Framework. Para obter mais informações sobre a abordagem tooEntity primeiro Olá código do Framework que é usado neste tutorial, consulte [código primeiro tooa novo banco de dados](https://msdn.microsoft.com/data/jj193542).

    ```c#
    public class Team
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public int Wins { get; set; }
        public int Losses { get; set; }
        public int Ties { get; set; }
    
        static public void PlayGames(IEnumerable<Team> teams)
        {
            // Simple random generation of statistics.
            Random r = new Random();
    
            foreach (var t in teams)
            {
                t.Wins = r.Next(33);
                t.Losses = r.Next(33);
                t.Ties = r.Next(0, 5);
            }
        }
    }
    
    public class TeamContext : DbContext
    {
        public TeamContext()
            : base("TeamContext")
        {
        }
    
        public DbSet<Team> Teams { get; set; }
    }
    
    public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
    {
        protected override void Seed(TeamContext context)
        {
            var teams = new List<Team>
            {
                new Team{Name="Adventure Works Cycles"},
                new Team{Name="Alpine Ski House"},
                new Team{Name="Blue Yonder Airlines"},
                new Team{Name="Coho Vineyard"},
                new Team{Name="Contoso, Ltd."},
                new Team{Name="Fabrikam, Inc."},
                new Team{Name="Lucerne Publishing"},
                new Team{Name="Northwind Traders"},
                new Team{Name="Consolidated Messenger"},
                new Team{Name="Fourth Coffee"},
                new Team{Name="Graphic Design Institute"},
                new Team{Name="Nod Publishers"}
            };
    
            Team.PlayGames(teams);
    
            teams.ForEach(t => context.Teams.Add(t));
            context.SaveChanges();
        }
    }
    
    public class TeamConfiguration : DbConfiguration
    {
        public TeamConfiguration()
        {
            SetExecutionStrategy("System.Data.SqlClient", () => new SqlAzureExecutionStrategy());
        }
    }
    ```


1. Em **Solution Explorer**, clique duas vezes em **Web. config** tooopen-lo.
   
    ![Web.config][cache-web-config]
2. Adicione o seguinte Olá `connectionStrings` seção. nome Hello de cadeia de caracteres de conexão Olá deve corresponder o nome de saudação do hello classe de contexto de banco de dados do Entity Framework que é `TeamContext`.

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Você pode adicionar Olá novo `connectionStrings` seção para que ele segue `configSections`, conforme mostrado no exemplo a seguir de saudação.

    ```xml
    <configuration>
      <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
      </configSections>
      <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
      </connectionStrings>
      ...
      ```

    > [!NOTE]
    > A cadeia de caracteres de conexão pode ser diferente dependendo da versão de saudação do Visual Studio e SQL Server Express edition usado toocomplete tutorial de saudação. modelo de Web. config Olá deve ser configurado toomatch sua instalação e pode conter `Data Source` como entradas `(LocalDB)\v11.0` (a partir do SQL Server Express 2012) ou `Data Source=(LocalDB)\MSSQLLocalDB` (do SQL Server Express 2014 e mais recente). Para saber mais sobre cadeias de caracteres de conexão e versões do SQL Express, veja [LocalDB do SQL Server 2016 Express](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).

### <a name="add-hello-controller"></a>Adicionar controlador Olá
1. Pressione **F6** toobuild projeto de saudação. 
2. Em **Solution Explorer**, Olá do botão direito do mouse **controladores** pasta e escolha **adicionar**, **controlador**.
   
    ![Adicionar controlador][cache-add-controller]
3. Escolha **Controlador MVC 5 com modos de exibição, usando o Entity Framework** e clique em **Adicionar**. Se você receber um erro depois de clicar em **adicionar**, certifique-se de que você criou Olá projeto primeiro.
   
    ![Adicionar classe de controlador][cache-add-controller-class]
4. Selecione **Team (ContosoTeamStats.Models)** de saudação **classe modelo** lista suspensa. Selecione **TeamContext (ContosoTeamStats.Models)** de saudação **classe de contexto de dados** lista suspensa. Tipo `TeamsController` em Olá **controlador** texto de nome (se ele não será preenchido automaticamente). Clique em **adicionar** toocreate Olá classe do controlador e adicionar exibições da saudação padrão.
   
    ![Configurar o controlador][cache-configure-controller]
5. Em **Solution Explorer**, expanda **global. asax** e clique duas vezes em **Global.asax.cs** tooopen-lo.
   
    ![Global.asax.cs][cache-global-asax]
6. Adicionar Olá após dois `using` instruções na parte superior de saudação do arquivo hello em outros Olá `using` instruções.

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. Adicionar Olá a seguinte linha de código final Olá Olá `Application_Start` método.

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. No **Gerenciador de Soluções**, expanda `App_Start` e clique duas vezes em `RouteConfig.cs`.
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. Substituir `controller = "Home"` em Olá Olá código a seguir `RegisterRoutes` método com `controller = "Teams"` conforme mostrado no exemplo a seguir de saudação.

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a>Configurar os modos de exibição de saudação
1. Em **Solution Explorer**, expanda Olá **exibições** pasta e, em seguida, hello **compartilhado** pasta e clique duas vezes em **cshtml**. 
   
    ![_Layout.cshtml.][cache-layout-cshtml]
2. Alterar o conteúdo Olá Olá `title` elemento e substituir `My ASP.NET Application` com `Contoso Team Stats` conforme mostrado no exemplo a seguir de saudação.

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. Em Olá `body` seção, atualize primeiro o hello `Html.ActionLink` instrução e substituir `Application name` com `Contoso Team Stats` e substitua `Home` com `Teams`.
   
   * Antes: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`
   * Após: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`
     
     ![Alterações de código][cache-layout-cshtml-code]
2. Pressione **Ctrl + F5** toobuild e executar o aplicativo hello. Esta versão do aplicativo hello lê resultados Olá diretamente do banco de dados de saudação. Saudação de Observação **criar novo**, **editar**, **detalhes**, e **excluir** as ações que foram automaticamente adicionadas toohello aplicativo por Olá **Controlador MVC 5 com modos de exibição usando o Entity Framework** scaffold. Na próxima seção Olá tutorial Olá adicionará o acesso a dados do Cache Redis toooptimize hello e fornecem recursos adicionais de aplicativo toohello.

![Aplicativo de início][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a>Configurar Olá aplicativo toouse Cache Redis
Nesta seção do tutorial Olá, você vai configurar toostore de aplicativo de exemplo hello e recuperar estatísticas da Contoso de uma instância de Cache Redis do Azure usando Olá [Stackexchange](https://github.com/StackExchange/StackExchange.Redis) cliente de cache.

* [Configurar Olá aplicativo toouse stackexchange. Redis](#configure-the-application-to-use-stackexchangeredis)
* [Atualizar Olá TeamsController classe tooreturn resultados do cache de saudação ou de banco de dados de saudação](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [Atualizar Olá criar, editar e excluir toowork métodos com cache Olá](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [Atualizar Olá equipes índice exibição toowork com cache Olá](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a>Configurar Olá aplicativo toouse stackexchange. Redis
1. tooconfigure um aplicativo cliente no Visual Studio usando Olá pacote NuGet stackexchange. Redis, clique em **NuGet Package Manager**, **Package Manager Console** de saudação **ferramentas** menu.
2. Execução hello seguinte comando do hello `Package Manager Console` janela.
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    Olá NuGet pacote baixa e adiciona Olá necessárias referências de assembly para tooaccess seu aplicativo de cliente Cache Redis do Azure com o cliente de cache Stackexchange hello. Se você preferir toouse uma versão de nome forte do hello `StackExchange.Redis` biblioteca de cliente, instale Olá `StackExchange.Redis.StrongName` pacote.
3. Em **Solution Explorer**, expanda Olá **controladores** pasta e clique duas vezes em **TeamsController.cs** tooopen-lo.
   
    ![Controlador de equipes][cache-teamscontroller]
4. Adicionar Olá após dois `using` instruções muito**TeamsController.cs**.

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. Adicionar Olá toohello de duas propriedades a seguir `TeamsController` classe.

    ```c#   
    // Redis Connection string info
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

6. Criar um arquivo em seu computador denominado `WebAppPlusCacheAppSecrets.config` e colocá-lo em um local que não verificado com o código-fonte saudação do seu aplicativo de exemplo, se você decidir toocheck em algum lugar. Em Olá Este exemplo `AppSettingsSecrets.config` arquivo está localizado em `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.
   
    Editar saudação `WebAppPlusCacheAppSecrets.config` e adicione Olá conteúdo a seguir. Se você executar o aplicativo hello localmente essa informação é instância de Cache Redis do Azure tooyour tooconnect usado. Mais tarde no tutorial Olá você provisionar uma instância de Cache Redis do Azure e atualize a senha e o nome do cache de saudação. Se você não planejar o aplicativo de exemplo hello toorun localmente, você pode ignorar a criação desse arquivo hello e etapas subsequentes de saudação que fazem referência a arquivo hello, pois quando você implanta o aplicativo de hello tooAzure recupera informações de conexão de cache de saudação do aplicativo hello a configuração para Olá Web App e não a partir desse arquivo. Desde Olá `WebAppPlusCacheAppSecrets.config` não está implantado tooAzure com seu aplicativo, você não é necessária a menos que você vai toorun aplicativo de hello localmente.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. Em **Solution Explorer**, clique duas vezes em **Web. config** tooopen-lo.
   
    ![Web.config][cache-web-config]
2. Adicione o seguinte Olá `file` atributo toohello `appSettings` elemento. Se você usou um nome de arquivo diferente ou local, substitua os valores para Olá aqueles mostrado no exemplo hello.
   
   * Antes: `<appSettings>`
   * Após: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`
     
   tempo de execução do ASP.NET Olá mescla o conteúdo de saudação de arquivo externo de saudação com marcações Olá Olá `<appSettings>` elemento. tempo de execução Olá ignora o atributo de arquivo hello se Olá especificado não foi encontrado. Seus segredos (cache de tooyour de cadeia de caracteres de conexão Olá) não são incluídos como parte do código-fonte para o aplicativo hello hello. Quando você implanta seu tooAzure de aplicativo web, Olá `WebAppPlusCacheAppSecrests.config` arquivo não será implantado (ou seja, o que você deseja). Há várias toospecify de maneiras desses segredos no Azure e neste tutorial estão configurados automaticamente para você quando você [provisionar Olá recursos do Azure](#provision-the-azure-resources) em uma etapa posterior do tutorial. Para obter mais informações sobre como trabalhar com segredos no Azure, consulte [práticas recomendadas para a implantação de senhas e outros dados confidenciais tooASP.NET e o serviço de aplicativo do Azure](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a>Atualizar Olá TeamsController classe tooreturn resultados do cache de saudação ou de banco de dados de saudação
Neste exemplo, estatísticas podem ser recuperadas do banco de dados de saudação ou de cache de saudação. Estatísticas de equipe são armazenadas no cache de saudação como um serializado `List<Team>`e também como um conjunto classificado usando tipos de dados do Redis. Ao recuperar itens de um conjunto ordenado, você pode recuperar alguns ou todos os itens ou consultar determinados itens. Neste exemplo, você vai consultar conjunto Olá classificado para 5 equipes principais Olá classificados pelo número de wins.

> [!NOTE]
> Não é necessário toostore Olá estatísticas em vários formatos em cache de saudação na ordem toouse Cache Redis do Azure. Este tutorial usa vários toodemonstrate de formatos de algumas maneiras diferentes de saudação e tipos de dados diferentes, você pode usar dados de toocache.
> 
> 

1. Adicione o seguinte Olá `using` toohello instruções `TeamsController.cs` arquivo na parte superior da saudação com hello outros `using` instruções.

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. Substituir saudação atual `public ActionResult Index()` implementação de método com hello implementação a seguir.

    ```c#
    // GET: Teams
    public ActionResult Index(string actionType, string resultType)
    {
        List<Team> teams = null;

        switch(actionType)
        {
            case "playGames": // Play a new season of games.
                PlayGames();
                break;

            case "clearCache": // Clear hello results from hello cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild hello database with sample data.
                RebuildDB();
                break;
        }

        // Measure hello time it takes tooretrieve hello results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve hello top 5 teams from hello sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from hello cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from hello database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add hello elapsed time of hello operation toohello ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. Adicionar Olá toohello de três métodos a seguir `TeamsController` Olá de tooimplement classe `playGames`, `clearCache`, e `rebuildDB` tipos de ação de saudação alternar instrução adicionada no trecho de código anterior hello.
   
    Olá `PlayGames` método atualiza estatísticas Olá simulando uma estação de jogos, salva Olá banco de dados de toohello resultados e Olá limpa dados de cache Olá obsoletas.

    ```c#
    void PlayGames()
    {
        ViewBag.msg += "Updating team statistics. ";
        // Play a "season" of games.
        var teams = from t in db.Teams
                    select t;

        Team.PlayGames(teams);

        db.SaveChanges();

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    Olá `RebuildDB` Olá método reinicializar banco de dados com o conjunto padrão de saudação de equipes, gera estatísticas para eles, e limpa Olá obsoletas dados do cache de saudação.

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize hello database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    Olá `ClearCachedTeams` método Remove todas as estatísticas de equipe em cache do cache de saudação.

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. Adicionar Olá toohello de quatro métodos a seguir `TeamsController` Olá tooimplement de classe várias maneiras de recuperar estatísticas da saudação do cache hello e banco de dados de saudação. Cada um desses métodos retorna um `List<Team>` que é exibido pelo modo de exibição de saudação.
   
    Olá `GetFromDB` método lê estatísticas da saudação do banco de dados de saudação.
   
    ```c#
    List<Team> GetFromDB()
    {
        ViewBag.msg += "Results read from DB. ";
        var results = from t in db.Teams
            orderby t.Wins descending
            select t; 

        return results.ToList<Team>();
    }
    ```

    Olá `GetFromList` método leituras de estatísticas da saudação do cache como um serializado `List<Team>`. Se houver um erro de cache, Olá estatísticas são de leitura do banco de dados de saudação e armazenadas em cache Olá na próxima vez. Neste exemplo estamos usando JSON.NET serialização tooserialize Olá .NET objetos tooand do cache de saudação. Para obter mais informações, consulte [como toowork com .NET objetos no Cache Redis do Azure](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

    ```c#
    List<Team> GetFromList()
    {
        List<Team> teams = null;

        IDatabase cache = Connection.GetDatabase();
        string serializedTeams = cache.StringGet("teamsList");
        if (!String.IsNullOrEmpty(serializedTeams))
        {
            teams = JsonConvert.DeserializeObject<List<Team>>(serializedTeams);

            ViewBag.msg += "List read from cache. ";
        }
        else
        {
            ViewBag.msg += "Teams list cache miss. ";
            // Get from database and store in cache
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    Olá `GetFromSortedSet` método lê estatísticas da saudação de um conjunto classificado em cache. Se houver um erro de cache, Olá estatísticas são de leitura do banco de dados de saudação e armazenadas em cache de saudação como um conjunto ordenado.

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", order: Order.Descending);
        if (teamsSortedSet.Count() > 0)
        {
            ViewBag.msg += "Reading sorted set from cache. ";
            teams = new List<Team>();
            foreach (var t in teamsSortedSet)
            {
                Team tt = JsonConvert.DeserializeObject<Team>(t.Element);
                teams.Add(tt);
            }
        }
        else
        {
            ViewBag.msg += "Teams sorted set cache miss. ";

            // Read from DB
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding toosorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    Olá `GetFromSortedSetTop5` método lê conjunto superior de 5 equipes de saudação em cache classificados hello. Ele começa pela verificando existência Olá Olá Olá cache `teamsSortedSet` chave. Se essa chave não estiver presente, Olá `GetFromSortedSet` método é chamado estatísticas Olá tooread e armazená-los no cache de saudação. Em seguida, hello conjunto classificado em cache é consultado para Olá top 5 equipes que são retornadas.

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load hello entire sorted set into hello cache.
            GetFromSortedSet();

            // Retrieve hello top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get hello top 5 teams from hello sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a>Atualizar Olá criar, editar e excluir toowork métodos com cache Olá
código de scaffolding Olá gerado como parte deste exemplo inclui métodos tooadd, editar e excluir equipes. Sempre que uma equipe é adicionada, editada ou removida, dados de saudação no cache de saudação ficarão desatualizados. Nesta seção, que você modificará a saudação de tooclear esses três métodos armazenados em cache equipes para que o cache de saudação não estar fora de sincronia com o banco de dados de saudação.

1. Procurar toohello `Create(Team team)` método hello `TeamsController` classe. Adicionar uma chamada toohello `ClearCachedTeams` método, conforme mostrado no exemplo a seguir de saudação.

    ```c#
    // POST: Teams/Create
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. Procurar toohello `Edit(Team team)` método hello `TeamsController` classe. Adicionar uma chamada toohello `ClearCachedTeams` método, conforme mostrado no exemplo a seguir de saudação.

    ```c#
    // POST: Teams/Edit/5
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. Procurar toohello `DeleteConfirmed(int id)` método hello `TeamsController` classe. Adicionar uma chamada toohello `ClearCachedTeams` método, conforme mostrado no exemplo a seguir de saudação.

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, hello cache is out of date.
        // Clear hello cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a>Atualizar Olá equipes índice exibição toowork com cache Olá
1. Em **Solution Explorer**, expanda Olá **exibições** pasta e, em seguida, Olá **equipes** pasta e clique duas vezes em **cshtml**.
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. Superior saudação do arquivo hello, procure Olá elemento parágrafo a seguir.
   
    ![Tabela de ação][cache-teams-index-table]
   
    Isso é Olá link toocreate um novo agrupamento. Substitua o elemento de parágrafo Olá Olá a tabela a seguir. Esta tabela tem links de ação para criar uma nova equipe, executar uma nova estação de jogos, limpando o cache de saudação, recuperando equipes de saudação do cache de saudação em vários formatos, recuperando equipes de saudação do banco de dados de saudação e recompilar Olá banco de dados com dados de exemplo atualizado.

    ```html
    <table class="table">
        <tr>
            <td>
                @Html.ActionLink("Create New", "Create")
            </td>
            <td>
                @Html.ActionLink("Play Season", "Index", new { actionType = "playGames" })
            </td>
            <td>
                @Html.ActionLink("Clear Cache", "Index", new { actionType = "clearCache" })
            </td>
            <td>
                @Html.ActionLink("List from Cache", "Index", new { resultType = "teamsList" })
            </td>
            <td>
                @Html.ActionLink("Sorted Set from Cache", "Index", new { resultType = "teamsSortedSet" })
            </td>
            <td>
                @Html.ActionLink("Top 5 Teams from Cache", "Index", new { resultType = "teamsSortedSetTop5" })
            </td>
            <td>
                @Html.ActionLink("Load from DB", "Index", new { resultType = "fromDB" })
            </td>
            <td>
                @Html.ActionLink("Rebuild DB", "Index", new { actionType = "rebuildDB" })
            </td>
        </tr>    
    </table>
    ```


1. Rolar para o fim da saudação toohello **cshtml** de arquivo e adicione o seguinte Olá `tr` elemento para que ele seja a última linha Olá Olá última tabela no arquivo hello.
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    Esta linha exibe o valor de saudação do `ViewBag.Msg` que contém um relatório de status sobre a operação atual de saudação. Olá `ViewBag.Msg` é definido quando você clicar em qualquer um dos links de ação de saudação da etapa anterior hello.   
   
    ![Mensagem de status][cache-status-message]
2. Pressione **F6** toobuild projeto de saudação.

## <a name="provision-hello-azure-resources"></a>Provisionar Olá recursos do Azure
toohost seu aplicativo no Azure, você deve primeiro provisionar Olá serviços do Azure que seu aplicativo requer. aplicativo de exemplo Hello neste tutorial usa Olá seguindo os serviços do Azure.

* Cache Redis do Azure
* Aplicativo Web do Serviço de Aplicativo
* Banco de dados SQL

toodeploy essas serviços tooa recursos novos ou existentes do grupo de sua escolha, clique em Olá após **implantar tooAzure** botão.

[! [Implantar tooAzure] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)

Isso **implantar tooAzure** botão usa Olá [criar um aplicativo Web mais o Cache Redis mais o banco de dados SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [início rápido do Azure](https://github.com/Azure/azure-quickstart-templates) modelo tooprovision esses serviços e o conjunto Olá cadeia de caracteres de conexão para a configuração do aplicativo de banco de dados SQL e hello do Olá para Olá cadeia de caracteres de conexão de Cache Redis do Azure.

> [!NOTE]
> Se não tiver uma conta do Azure, você poderá [criar uma conta gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) em apenas alguns minutos.
> 
> 

Olá clicando em **implantar tooAzure** botão leva toohello portal do Azure e inicia Olá o processo de criação de recursos Olá descritos pelo modelo de saudação.

![Implantar tooAzure][cache-deploy-to-azure-step-1]

1. Em Olá **Noções básicas de** seção, selecione Olá toouse de assinatura do Azure, selecione um grupo de recursos existente ou crie um novo e especifique o local do grupo de recursos de saudação.
2. Em Olá **configurações** seção, especifique um **logon de administrador** (não use **admin**), **senha de logon de administrador**e  **Nome do banco de dados**. Olá outros parâmetros são configurados para um serviço de aplicativo gratuito hospedagem plano e as opções de baixo custo para hello banco de dados SQL e o Cache Redis do Azure, que não vêm com uma camada gratuita.

    ![Implantar tooAzure][cache-deploy-to-azure-step-2]

3. Depois de configurar as configurações de saudação desejada, role toohello final da página hello, Olá leitura termos e as condições e verificar Olá **concordo toohello termos e condições declaradas acima** caixa de seleção.
4. provisionar recursos de saudação toobegin, clique em **compra**.

progresso de saudação tooview de sua implantação, clique o ícone de notificação hello e clique em **implantação iniciada**.

![Implantação iniciada][cache-deployment-started]

Você pode exibir o status de saudação da sua implantação em Olá **Microsoft.Template** folha.

![Implantar tooAzure][cache-deploy-to-azure-step-3]

Quando o provisionamento for concluído, você pode publicar seu tooAzure de aplicativo do Visual Studio.

> [!NOTE]
> Os erros que podem ocorrer durante o processo de provisionamento de saudação são exibidos em Olá **Microsoft.Template** folha. Alguns erros comuns são muitos Servidores SQL ou muitos planos de hospedagem do Serviço de Aplicativo gratuitos por assinatura. Resolva quaisquer erros e reiniciar o processo de saudação clicando **reimplantar** em Olá **Microsoft.Template** folha ou hello **implantar tooAzure** botão neste tutorial.
> 
> 

## <a name="publish-hello-application-tooazure"></a>Publicar Olá aplicativo tooAzure
Nesta etapa do tutorial hello, você publicar Olá tooAzure de aplicativo e executá-lo na nuvem hello.

1. Saudação de atalho **ContosoTeamStats** do projeto no Visual Studio e escolha **publicar**.
   
    ![Publicar][cache-publish-app]
2. Clique em **Serviço de Aplicativo do Microsoft Azure**, escolha **Selecionar Existente** e clique em **Publicar**.
   
    ![Publicar][cache-publish-to-app-service]
3. Selecione a assinatura Olá usada quando criar hello recursos do Azure, expanda o grupo de recursos de saudação contendo os recursos de saudação e selecione Olá desejado de aplicativo Web. Se você usou Olá **implantar tooAzure** botão, o nome do aplicativo Web começa com **site** seguido por alguns caracteres adicionais.
   
    ![Selecionar aplicativo Web][cache-select-web-app]
4. Clique em **Okey** toobegin Olá processo de publicação. Após alguns instantes Olá processo de publicação for concluída e um navegador é iniciado com hello executando o aplicativo de exemplo. Se você receber um erro ao validar ou publicação de DNS e Olá processo para o provisionamento hello recursos do Azure para o aplicativo hello recentemente concluiu, aguarde um momento e tente novamente.
   
    ![Cache adicionado][cache-added-to-application]

Olá tabela a seguir descreve cada link de ação do aplicativo de exemplo hello.

| Ação | Descrição |
| --- | --- |
| Criar Novo |Criar uma nova Equipe. |
| Reproduzir Temporada |Reproduzir uma estação de jogos, atualização de estatísticas de equipe Olá, e desmarque qualquer desatualizadas dados da equipe do cache de saudação. |
| Limpar Cache |Estatísticas de equipe Olá clara do cache de saudação. |
| Listar do Cache |Recupere estatísticas da equipe de saudação do cache de saudação. Se houver um erro de cache, carregar estatísticas de saudação do banco de dados de saudação e salvar toohello cache na próxima vez. |
| Conjunto Ordenado do Cache |Recupere estatísticas da equipe de saudação do cache de saudação usando um conjunto ordenado. Se houver um erro de cache, estatísticas de saudação do banco de dados de saudação e salva toohello cache usando um conjunto ordenado. |
| Cinco Principais Equipes do Cache |Recupere 5 equipes principais de saudação do cache de saudação usando um conjunto ordenado. Se houver um erro de cache, estatísticas de saudação do banco de dados de saudação e salva toohello cache usando um conjunto ordenado. |
| Carregar do banco de dados |Recupere estatísticas da equipe de saudação do banco de dados de saudação. |
| Recriar o banco de dados |Recriar o banco de dados de saudação e recarregá-lo com dados da equipe de exemplo. |
| Editar/Detalhes/Excluir |Editar uma equipe, exibir detalhes de uma equipe, excluir uma equipe. |

Clique em algumas das ações de saudação e fazer experiências com a recuperação de dados de saudação de origens diferentes hello. Não Olá as diferenças no hello tempo Olá toocomplete várias maneiras de recuperar dados de saudação do banco de dados de saudação e cache de saudação.

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a>Excluir recursos de hello quando você tiver terminado com o aplicativo hello
Quando tiver terminado com aplicativo tutorial do exemplo hello, você pode excluir hello Azure recursos usados em ordem tooconserve custo e recursos. Se você usar o hello **implantar tooAzure** botão Olá [provisionar Olá recursos do Azure](#provision-the-azure-resources) seção e todos os recursos estão contidos em Olá mesmo grupo de recursos, você pode excluí-los juntos em um operação, excluindo o grupo de recursos de saudação.

1. Entrar toohello [portal do Azure](https://portal.azure.com) e clique em **grupos de recursos**.
2. Nome de saudação do tipo do seu grupo de recursos em hello **filtrar itens...**  caixa de texto.
3. Clique em **...**  toohello direita do seu grupo de recursos.
4. Clique em **Excluir**.
   
    ![Exclusão][cache-delete-resource-group]
5. Nome do tipo saudação do seu grupo de recursos e clique em **excluir**.
   
    ![Confirmar exclusão][cache-delete-confirm]

Depois de alguns recursos de saudação momentos grupo e todos os seus recursos contidos são excluídos.

> [!IMPORTANT]
> Observe que a exclusão de um grupo de recursos é irreversível e grupo de recursos de saudação e todos os recursos de saudação nela são excluídos permanentemente. Certifique-se de que você não acidentalmente excluir grupo de recurso incorreto hello ou recursos. Se você criou recursos Olá para hospedar este exemplo dentro de um grupo de recursos existente, você pode excluir individualmente cada recurso de seus respectivas folhas.
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a>Execute o aplicativo de exemplo hello em seu computador local
aplicativo de hello toorun localmente no seu computador, você precisa de um Cache Redis do Azure da instância na qual toocache seus dados. 

* Se você tiver publicado seu aplicativo tooAzure conforme descrito na seção anterior hello, você pode usar a instância de Cache Redis do Azure de saudação que estava provisionada durante essa etapa.
* Se você tiver outra instância existente do Cache Redis do Azure, você pode usar esse toorun Este exemplo localmente.
* Se você precisar toocreate uma instância de Cache Redis do Azure, você pode seguir etapas Olá [criar um cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

Depois que você selecionar ou criar hello cache toouse, procurar toohello cache no portal do Azure de saudação e recuperar Olá [nome de host](cache-configure.md#properties) e [chaves de acesso](cache-configure.md#access-keys) para seu cache. Para obter instruções, confira [Definir configurações de cache Redis](cache-configure.md#configure-redis-cache-settings).

1. Olá abrir `WebAppPlusCacheAppSecrets.config` arquivo criado durante a saudação [configurar Olá aplicativo toouse Cache Redis](#configure-the-application-to-use-redis-cache) etapa deste tutorial, usando o editor de saudação de sua escolha.
2. Editar saudação `value` de atributos e substitua `MyCache.redis.cache.windows.net` com hello [nome de host](cache-configure.md#properties) do cache e especifique a saudação [chave primária ou secundária](cache-configure.md#access-keys) do cache como senha hello.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. Pressione **Ctrl + F5** aplicativo hello de toorun.

> [!NOTE]
> Observe que o cache de Olá porque o aplicativo hello, incluindo o banco de dados hello, está em execução localmente e hello Redis Cache está hospedado no Azure, pode aparecer toounder-executar Olá banco de dados. Para melhor desempenho, Olá aplicativo cliente e a instância de Cache Redis do Azure deve estar no hello mesmo local. 
> 
> 

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [guia de Introdução ao ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) em Olá [ASP.NET](http://asp.net/) site.
* Para obter mais exemplos de criação de um aplicativo Web ASP.NET no serviço de aplicativo, consulte [criar e implantar um aplicativo da web ASP.NET no serviço de aplicativo do Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) de saudação [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 conectar [demonstração](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).
  * Para mais guias de início rápido de demonstração de HealthClinic.biz hello, consulte [início rápido do Azure Developer Tools](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).
* Saiba mais sobre Olá [código primeiro tooa novo banco de dados](https://msdn.microsoft.com/data/jj193542) abordagem tooEntity do Framework que é usado neste tutorial.
* Saiba mais sobre [aplicativos Web no Serviço de Aplicativo do Azure](../app-service-web/app-service-web-overview.md).
* Saiba como muito[monitor](cache-how-to-monitor.md) o cache do hello portal do Azure.
* Explore os recursos premium do Cache Redis do Azure
  
  * [Como tooconfigure persistência para um Premium do Azure Redis Cache](cache-how-to-premium-persistence.md)
  * [Como tooconfigure clustering para um Premium do Azure Redis Cache](cache-how-to-premium-clustering.md)
  * [Como o suporte a tooconfigure rede Virtual para um Premium do Azure Redis Cache](cache-how-to-premium-vnet.md)
  * Consulte Olá [perguntas Frequentes de Cache Redis do Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) para obter mais detalhes sobre o tamanho, a taxa de transferência e a largura de banda com caches premium.

<!-- IMAGES -->
[cache-starter-application]: ./media/cache-web-app-howto/cache-starter-application.png
[cache-added-to-application]: ./media/cache-web-app-howto/cache-added-to-application.png
[cache-create-project]: ./media/cache-web-app-howto/cache-create-project.png
[cache-select-template]: ./media/cache-web-app-howto/cache-select-template.png
[cache-model-add-class]: ./media/cache-web-app-howto/cache-model-add-class.png
[cache-model-add-class-dialog]: ./media/cache-web-app-howto/cache-model-add-class-dialog.png
[cache-add-controller]: ./media/cache-web-app-howto/cache-add-controller.png
[cache-add-controller-class]: ./media/cache-web-app-howto/cache-add-controller-class.png
[cache-configure-controller]: ./media/cache-web-app-howto/cache-configure-controller.png
[cache-global-asax]: ./media/cache-web-app-howto/cache-global-asax.png
[cache-RouteConfig-cs]: ./media/cache-web-app-howto/cache-RouteConfig-cs.png
[cache-layout-cshtml]: ./media/cache-web-app-howto/cache-layout-cshtml.png
[cache-layout-cshtml-code]: ./media/cache-web-app-howto/cache-layout-cshtml-code.png
[redis-cache-manage-nuget-menu]: ./media/cache-web-app-howto/redis-cache-manage-nuget-menu.png
[redis-cache-stack-exchange-nuget]: ./media/cache-web-app-howto/redis-cache-stack-exchange-nuget.png
[cache-teamscontroller]: ./media/cache-web-app-howto/cache-teamscontroller.png
[cache-web-config]: ./media/cache-web-app-howto/cache-web-config.png
[cache-views-teams-index-cshtml]: ./media/cache-web-app-howto/cache-views-teams-index-cshtml.png
[cache-teams-index-table]: ./media/cache-web-app-howto/cache-teams-index-table.png
[cache-status-message]: ./media/cache-web-app-howto/cache-status-message.png
[deploybutton]: ./media/cache-web-app-howto/deploybutton.png
[cache-deploy-to-azure-step-1]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-1.png
[cache-deploy-to-azure-step-2]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-2.png
[cache-deploy-to-azure-step-3]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-3.png
[cache-deployment-started]: ./media/cache-web-app-howto/cache-deployment-started.png
[cache-publish-app]: ./media/cache-web-app-howto/cache-publish-app.png
[cache-publish-to-app-service]: ./media/cache-web-app-howto/cache-publish-to-app-service.png
[cache-select-web-app]: ./media/cache-web-app-howto/cache-select-web-app.png
[cache-publish]: ./media/cache-web-app-howto/cache-publish.png
[cache-delete-resource-group]: ./media/cache-web-app-howto/cache-delete-resource-group.png
[cache-delete-confirm]: ./media/cache-web-app-howto/cache-delete-confirm.png

