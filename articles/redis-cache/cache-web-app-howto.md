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
# <a name="how-toocreate-a-web-app-with-redis-cache"></a><span data-ttu-id="e53b4-103">Como toocreate um aplicativo Web com o Cache Redis</span><span class="sxs-lookup"><span data-stu-id="e53b4-103">How toocreate a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e53b4-104">.NET</span><span class="sxs-lookup"><span data-stu-id="e53b4-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="e53b4-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e53b4-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="e53b4-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="e53b4-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="e53b4-107">Java</span><span class="sxs-lookup"><span data-stu-id="e53b4-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="e53b4-108">Python</span><span class="sxs-lookup"><span data-stu-id="e53b4-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="e53b4-109">Este tutorial mostra como toocreate e implantar um aplicativo de web de tooa de aplicativo da web do ASP.NET no serviço de aplicativo do Azure usando o Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="e53b4-109">This tutorial shows how toocreate and deploy an ASP.NET web application tooa web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="e53b4-110">aplicativo de exemplo Hello exibe uma lista de estatísticas de banco de dados e mostra diferentes maneiras toouse Cache Redis do Azure toostore e recuperar dados do cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-110">hello sample application displays a list of team statistics from a database and shows different ways toouse Azure Redis Cache toostore and retrieve data from hello cache.</span></span> <span data-ttu-id="e53b4-111">Quando você concluir o tutorial hello, você terá um aplicativo web em execução que lê e grava o banco de dados de tooa, otimizada com Cache Redis do Azure e hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="e53b4-111">When you complete hello tutorial you'll have a running web app that reads and writes tooa database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="e53b4-112">Você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="e53b4-112">You'll learn:</span></span>

* <span data-ttu-id="e53b4-113">Como toocreate um ASP.NET MVC 5 aplicativo da web no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e53b4-113">How toocreate an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="e53b4-114">Como tooaccess dados de um banco de dados usando o Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="e53b4-114">How tooaccess data from a database using Entity Framework.</span></span>
* <span data-ttu-id="e53b4-115">Como tooimprove taxa de transferência de dados e reduzir a carga do banco de dados, armazenar e recuperar dados usando o Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="e53b4-115">How tooimprove data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="e53b4-116">Como toouse uma Redis classificados conjunto tooretrieve Olá top 5 equipes.</span><span class="sxs-lookup"><span data-stu-id="e53b4-116">How toouse a Redis sorted set tooretrieve hello top 5 teams.</span></span>
* <span data-ttu-id="e53b4-117">Como tooprovision Olá recursos do Azure para o aplicativo hello usando um modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="e53b4-117">How tooprovision hello Azure resources for hello application using a Resource Manager template.</span></span>
* <span data-ttu-id="e53b4-118">Como toopublish Olá tooAzure de aplicativo usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e53b4-118">How toopublish hello application tooAzure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e53b4-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e53b4-119">Prerequisites</span></span>
<span data-ttu-id="e53b4-120">tutorial de saudação toocomplete, você deve ter Olá pré-requisitos a seguir.</span><span class="sxs-lookup"><span data-stu-id="e53b4-120">toocomplete hello tutorial, you must have hello following prerequisites.</span></span>

* [<span data-ttu-id="e53b4-121">Conta do Azure</span><span class="sxs-lookup"><span data-stu-id="e53b4-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="e53b4-122">Visual Studio de 2017 com hello Azure SDK para .NET</span><span class="sxs-lookup"><span data-stu-id="e53b4-122">Visual Studio 2017 with hello Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="e53b4-123">Conta do Azure</span><span class="sxs-lookup"><span data-stu-id="e53b4-123">Azure account</span></span>
<span data-ttu-id="e53b4-124">Você precisa de um tutorial de saudação toocomplete conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="e53b4-124">You need an Azure account toocomplete hello tutorial.</span></span> <span data-ttu-id="e53b4-125">Você pode:</span><span class="sxs-lookup"><span data-stu-id="e53b4-125">You can:</span></span>

* <span data-ttu-id="e53b4-126">[Abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="e53b4-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="e53b4-127">Você obtém créditos que podem ser usado tootry out paga serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="e53b4-127">You get credits that can be used tootry out paid Azure services.</span></span> <span data-ttu-id="e53b4-128">Mesmo depois de saudação créditos são esgotados, você pode manter Olá conta e usar os recursos e serviços do Azure gratuitos.</span><span class="sxs-lookup"><span data-stu-id="e53b4-128">Even after hello credits are used up, you can keep hello account and use free Azure services and features.</span></span>
* <span data-ttu-id="e53b4-129">[Ativar benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="e53b4-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="e53b4-130">Todos os meses, sua assinatura do MSDN lhe oferece créditos que podem ser usados para serviços pagos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e53b4-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a><span data-ttu-id="e53b4-131">Visual Studio de 2017 com hello Azure SDK para .NET</span><span class="sxs-lookup"><span data-stu-id="e53b4-131">Visual Studio 2017 with hello Azure SDK for .NET</span></span>
<span data-ttu-id="e53b4-132">Olá tutorial destina 2017 do Visual Studio com hello [SDK do Azure para .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span><span class="sxs-lookup"><span data-stu-id="e53b4-132">hello tutorial is written for Visual Studio 2017 with hello [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="e53b4-133">Olá 2.9.5 do SDK do Azure está incluído no instalador do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="e53b4-133">hello Azure SDK 2.9.5 is included with hello Visual Studio installer.</span></span>

<span data-ttu-id="e53b4-134">Se você tiver o Visual Studio 2015, você pode seguir o tutorial Olá Olá [SDK do Azure para .NET](../dotnet-sdk.md) 2.8.2 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e53b4-134">If you have Visual Studio 2015, you can follow hello tutorial with hello [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="e53b4-135">[Download hello SDK mais recente do Azure para Visual Studio 2015 aqui](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="e53b4-135">[Download hello latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="e53b4-136">O Visual Studio é instalado automaticamente com hello SDK se você ainda não o fez.</span><span class="sxs-lookup"><span data-stu-id="e53b4-136">Visual Studio is automatically installed with hello SDK if you don't already have it.</span></span> <span data-ttu-id="e53b4-137">Algumas telas podem parecer diferentes das ilustrações Olá mostradas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="e53b4-137">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

<span data-ttu-id="e53b4-138">Se você tiver o Visual Studio 2013, você pode [download hello SDK mais recente do Azure para Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span><span class="sxs-lookup"><span data-stu-id="e53b4-138">If you have Visual Studio 2013, you can [download hello latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="e53b4-139">Algumas telas podem parecer diferentes das ilustrações Olá mostradas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="e53b4-139">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

## <a name="create-hello-visual-studio-project"></a><span data-ttu-id="e53b4-140">Criar o projeto do Visual Studio Olá</span><span class="sxs-lookup"><span data-stu-id="e53b4-140">Create hello Visual Studio project</span></span>
1. <span data-ttu-id="e53b4-141">Abra o Visual Studio e clique em **Arquivo**, **Novo**, **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="e53b4-142">Expanda Olá **Visual C#** nó Olá **modelos** lista, selecione **nuvem**e clique em **aplicativo Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-142">Expand hello **Visual C#** node in hello **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="e53b4-143">Verifique se **.NET Framework 4.5.2** ou superior está selecionado.</span><span class="sxs-lookup"><span data-stu-id="e53b4-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="e53b4-144">Tipo **ContosoTeamStats** em Olá **nome** caixa de texto e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-144">Type **ContosoTeamStats** into hello **Name** textbox and click **OK**.</span></span>
   
    ![Criar projeto][cache-create-project]
3. <span data-ttu-id="e53b4-146">Selecione **MVC** como o tipo de projeto hello.</span><span class="sxs-lookup"><span data-stu-id="e53b4-146">Select **MVC** as hello project type.</span></span> 

    <span data-ttu-id="e53b4-147">Certifique-se de que **sem autenticação** é especificado para Olá **autenticação** configurações.</span><span class="sxs-lookup"><span data-stu-id="e53b4-147">Ensure that **No Authentication** is specified for hello **Authentication** settings.</span></span> <span data-ttu-id="e53b4-148">Dependendo de sua versão do Visual Studio, o padrão de saudação pode ser definido toosomething else.</span><span class="sxs-lookup"><span data-stu-id="e53b4-148">Depending on your version of Visual Studio, hello default may be set toosomething else.</span></span> <span data-ttu-id="e53b4-149">toochange-la, clique em **alterar autenticação** e selecione **sem autenticação**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-149">toochange it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="e53b4-150">Se você estiver seguindo junto com o Visual Studio 2015, desmarque Olá **Host na nuvem Olá** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="e53b4-150">If you are following along with Visual Studio 2015, clear hello **Host in hello cloud** checkbox.</span></span> <span data-ttu-id="e53b4-151">Você vai [provisionar Olá recursos do Azure](#provision-the-azure-resources) e [publicar Olá aplicativo tooAzure](#publish-the-application-to-azure) nas etapas subsequentes no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-151">You'll [provision hello Azure resources](#provision-the-azure-resources) and [publish hello application tooAzure](#publish-the-application-to-azure) in subsequent steps in hello tutorial.</span></span> <span data-ttu-id="e53b4-152">Para obter um exemplo de provisionamento de um aplicativo da web do serviço de aplicativo do Visual Studio, deixando **Host na nuvem Olá** marcada, consulte [começar com aplicativos Web no serviço de aplicativo do Azure, usando ASP.NET e Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e53b4-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in hello cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![Selecionar modelo de projeto][cache-select-template]
4. <span data-ttu-id="e53b4-154">Clique em **Okey** toocreate projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-154">Click **OK** toocreate hello project.</span></span>

## <a name="create-hello-aspnet-mvc-application"></a><span data-ttu-id="e53b4-155">Criar hello aplicativo ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="e53b4-155">Create hello ASP.NET MVC application</span></span>
<span data-ttu-id="e53b4-156">Essa seção do tutorial hello, você criará Olá básica o aplicativo que lê e exibe estatísticas de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e53b4-156">In this section of hello tutorial, you'll create hello basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="e53b4-157">Adicionar o pacote do NuGet do Entity Framework Olá</span><span class="sxs-lookup"><span data-stu-id="e53b4-157">Add hello Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="e53b4-158">Adicionar modelo Olá</span><span class="sxs-lookup"><span data-stu-id="e53b4-158">Add hello model</span></span>](#add-the-model)
* [<span data-ttu-id="e53b4-159">Adicionar controlador Olá</span><span class="sxs-lookup"><span data-stu-id="e53b4-159">Add hello controller</span></span>](#add-the-controller)
* [<span data-ttu-id="e53b4-160">Configurar os modos de exibição de saudação</span><span class="sxs-lookup"><span data-stu-id="e53b4-160">Configure hello views</span></span>](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a><span data-ttu-id="e53b4-161">Adicionar o pacote do NuGet do Entity Framework Olá</span><span class="sxs-lookup"><span data-stu-id="e53b4-161">Add hello Entity Framework NuGet package</span></span>

1. <span data-ttu-id="e53b4-162">Clique em **NuGet Package Manager**, **Package Manager Console** de saudação **ferramentas** menu.</span><span class="sxs-lookup"><span data-stu-id="e53b4-162">Click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="e53b4-163">Execução hello seguinte comando do hello **Package Manager Console** janela.</span><span class="sxs-lookup"><span data-stu-id="e53b4-163">Run hello following command from hello **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="e53b4-164">Para obter mais informações sobre este pacote, consulte Olá [EntityFramework](https://www.nuget.org/packages/EntityFramework/) página NuGet.</span><span class="sxs-lookup"><span data-stu-id="e53b4-164">For more information about this package, see hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-hello-model"></a><span data-ttu-id="e53b4-165">Adicionar modelo Olá</span><span class="sxs-lookup"><span data-stu-id="e53b4-165">Add hello model</span></span>
1. <span data-ttu-id="e53b4-166">Clique com o botão direito do mouse em **Modelos** no **Gerenciador de Soluções** e escolha **Adicionar**, **Classe**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![Adicionar modelo][cache-model-add-class]
2. <span data-ttu-id="e53b4-168">Digite `Team` para o nome da classe hello e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-168">Enter `Team` for hello class name and click **Add**.</span></span>
   
    ![Adicionar classe de modelo][cache-model-add-class-dialog]
3. <span data-ttu-id="e53b4-170">Substituir saudação `using` instruções na parte superior de saudação do hello `Team.cs` arquivo com os seguintes Olá `using` instruções.</span><span class="sxs-lookup"><span data-stu-id="e53b4-170">Replace hello `using` statements at hello top of hello `Team.cs` file with hello following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="e53b4-171">Substituir a definição de saudação do hello `Team` classe com hello seguindo o trecho de código que contém atualizada `Team` classe definição, bem como outras classes de auxiliar de Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="e53b4-171">Replace hello definition of hello `Team` class with hello following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="e53b4-172">Para obter mais informações sobre a abordagem tooEntity primeiro Olá código do Framework que é usado neste tutorial, consulte [código primeiro tooa novo banco de dados](https://msdn.microsoft.com/data/jj193542).</span><span class="sxs-lookup"><span data-stu-id="e53b4-172">For more information on hello code first approach tooEntity Framework that's used in this tutorial, see [Code first tooa new database](https://msdn.microsoft.com/data/jj193542).</span></span>

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


1. <span data-ttu-id="e53b4-173">Em **Solution Explorer**, clique duas vezes em **Web. config** tooopen-lo.</span><span class="sxs-lookup"><span data-stu-id="e53b4-173">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="e53b4-175">Adicione o seguinte Olá `connectionStrings` seção.</span><span class="sxs-lookup"><span data-stu-id="e53b4-175">Add hello following `connectionStrings` section.</span></span> <span data-ttu-id="e53b4-176">nome Hello de cadeia de caracteres de conexão Olá deve corresponder o nome de saudação do hello classe de contexto de banco de dados do Entity Framework que é `TeamContext`.</span><span class="sxs-lookup"><span data-stu-id="e53b4-176">hello name of hello connection string must match hello name of hello Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="e53b4-177">Você pode adicionar Olá novo `connectionStrings` seção para que ele segue `configSections`, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-177">You can add hello new `connectionStrings` section so that it follows `configSections`, as shown in hello following example.</span></span>

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
    > <span data-ttu-id="e53b4-178">A cadeia de caracteres de conexão pode ser diferente dependendo da versão de saudação do Visual Studio e SQL Server Express edition usado toocomplete tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-178">Your connection string may be different depending on hello version of Visual Studio and SQL Server Express edition used toocomplete hello tutorial.</span></span> <span data-ttu-id="e53b4-179">modelo de Web. config Olá deve ser configurado toomatch sua instalação e pode conter `Data Source` como entradas `(LocalDB)\v11.0` (a partir do SQL Server Express 2012) ou `Data Source=(LocalDB)\MSSQLLocalDB` (do SQL Server Express 2014 e mais recente).</span><span class="sxs-lookup"><span data-stu-id="e53b4-179">hello web.config template should be configured toomatch your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="e53b4-180">Para saber mais sobre cadeias de caracteres de conexão e versões do SQL Express, veja [LocalDB do SQL Server 2016 Express](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span><span class="sxs-lookup"><span data-stu-id="e53b4-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-hello-controller"></a><span data-ttu-id="e53b4-181">Adicionar controlador Olá</span><span class="sxs-lookup"><span data-stu-id="e53b4-181">Add hello controller</span></span>
1. <span data-ttu-id="e53b4-182">Pressione **F6** toobuild projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-182">Press **F6** toobuild hello project.</span></span> 
2. <span data-ttu-id="e53b4-183">Em **Solution Explorer**, Olá do botão direito do mouse **controladores** pasta e escolha **adicionar**, **controlador**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-183">In **Solution Explorer**, right-click hello **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![Adicionar controlador][cache-add-controller]
3. <span data-ttu-id="e53b4-185">Escolha **Controlador MVC 5 com modos de exibição, usando o Entity Framework** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="e53b4-186">Se você receber um erro depois de clicar em **adicionar**, certifique-se de que você criou Olá projeto primeiro.</span><span class="sxs-lookup"><span data-stu-id="e53b4-186">If you get an error after clicking **Add**, ensure that you have built hello project first.</span></span>
   
    ![Adicionar classe de controlador][cache-add-controller-class]
4. <span data-ttu-id="e53b4-188">Selecione **Team (ContosoTeamStats.Models)** de saudação **classe modelo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="e53b4-188">Select **Team (ContosoTeamStats.Models)** from hello **Model class** drop-down list.</span></span> <span data-ttu-id="e53b4-189">Selecione **TeamContext (ContosoTeamStats.Models)** de saudação **classe de contexto de dados** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="e53b4-189">Select **TeamContext (ContosoTeamStats.Models)** from hello **Data context class** drop-down list.</span></span> <span data-ttu-id="e53b4-190">Tipo `TeamsController` em Olá **controlador** texto de nome (se ele não será preenchido automaticamente).</span><span class="sxs-lookup"><span data-stu-id="e53b4-190">Type `TeamsController` in hello **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="e53b4-191">Clique em **adicionar** toocreate Olá classe do controlador e adicionar exibições da saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="e53b4-191">Click **Add** toocreate hello controller class and add hello default views.</span></span>
   
    ![Configurar o controlador][cache-configure-controller]
5. <span data-ttu-id="e53b4-193">Em **Solution Explorer**, expanda **global. asax** e clique duas vezes em **Global.asax.cs** tooopen-lo.</span><span class="sxs-lookup"><span data-stu-id="e53b4-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** tooopen it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="e53b4-195">Adicionar Olá após dois `using` instruções na parte superior de saudação do arquivo hello em outros Olá `using` instruções.</span><span class="sxs-lookup"><span data-stu-id="e53b4-195">Add hello following two `using` statements at hello top of hello file under hello other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="e53b4-196">Adicionar Olá a seguinte linha de código final Olá Olá `Application_Start` método.</span><span class="sxs-lookup"><span data-stu-id="e53b4-196">Add hello following line of code at hello end of hello `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="e53b4-197">No **Gerenciador de Soluções**, expanda `App_Start` e clique duas vezes em `RouteConfig.cs`.</span><span class="sxs-lookup"><span data-stu-id="e53b4-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="e53b4-199">Substituir `controller = "Home"` em Olá Olá código a seguir `RegisterRoutes` método com `controller = "Teams"` conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-199">Replace `controller = "Home"` in hello following code in hello `RegisterRoutes` method with `controller = "Teams"` as shown in hello following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a><span data-ttu-id="e53b4-200">Configurar os modos de exibição de saudação</span><span class="sxs-lookup"><span data-stu-id="e53b4-200">Configure hello views</span></span>
1. <span data-ttu-id="e53b4-201">Em **Solution Explorer**, expanda Olá **exibições** pasta e, em seguida, hello **compartilhado** pasta e clique duas vezes em **cshtml**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-201">In **Solution Explorer**, expand hello **Views** folder and then hello **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml.][cache-layout-cshtml]
2. <span data-ttu-id="e53b4-203">Alterar o conteúdo Olá Olá `title` elemento e substituir `My ASP.NET Application` com `Contoso Team Stats` conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-203">Change hello contents of hello `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in hello following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="e53b4-204">Em Olá `body` seção, atualize primeiro o hello `Html.ActionLink` instrução e substituir `Application name` com `Contoso Team Stats` e substitua `Home` com `Teams`.</span><span class="sxs-lookup"><span data-stu-id="e53b4-204">In hello `body` section, update hello first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="e53b4-205">Antes: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="e53b4-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="e53b4-206">Após: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="e53b4-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![Alterações de código][cache-layout-cshtml-code]
2. <span data-ttu-id="e53b4-208">Pressione **Ctrl + F5** toobuild e executar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e53b4-208">Press **Ctrl+F5** toobuild and run hello application.</span></span> <span data-ttu-id="e53b4-209">Esta versão do aplicativo hello lê resultados Olá diretamente do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-209">This version of hello application reads hello results directly from hello database.</span></span> <span data-ttu-id="e53b4-210">Saudação de Observação **criar novo**, **editar**, **detalhes**, e **excluir** as ações que foram automaticamente adicionadas toohello aplicativo por Olá **Controlador MVC 5 com modos de exibição usando o Entity Framework** scaffold.</span><span class="sxs-lookup"><span data-stu-id="e53b4-210">Note hello **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added toohello application by hello **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="e53b4-211">Na próxima seção Olá tutorial Olá adicionará o acesso a dados do Cache Redis toooptimize hello e fornecem recursos adicionais de aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="e53b4-211">In hello next section of hello tutorial you'll add Redis Cache toooptimize hello data access and provide additional features toohello application.</span></span>

![Aplicativo de início][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a><span data-ttu-id="e53b4-213">Configurar Olá aplicativo toouse Cache Redis</span><span class="sxs-lookup"><span data-stu-id="e53b4-213">Configure hello application toouse Redis Cache</span></span>
<span data-ttu-id="e53b4-214">Nesta seção do tutorial Olá, você vai configurar toostore de aplicativo de exemplo hello e recuperar estatísticas da Contoso de uma instância de Cache Redis do Azure usando Olá [Stackexchange](https://github.com/StackExchange/StackExchange.Redis) cliente de cache.</span><span class="sxs-lookup"><span data-stu-id="e53b4-214">In this section of hello tutorial, you'll configure hello sample application toostore and retrieve Contoso team statistics from an Azure Redis Cache instance by using hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="e53b4-215">Configurar Olá aplicativo toouse stackexchange. Redis</span><span class="sxs-lookup"><span data-stu-id="e53b4-215">Configure hello application toouse StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="e53b4-216">Atualizar Olá TeamsController classe tooreturn resultados do cache de saudação ou de banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="e53b4-216">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="e53b4-217">Atualizar Olá criar, editar e excluir toowork métodos com cache Olá</span><span class="sxs-lookup"><span data-stu-id="e53b4-217">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="e53b4-218">Atualizar Olá equipes índice exibição toowork com cache Olá</span><span class="sxs-lookup"><span data-stu-id="e53b4-218">Update hello Teams Index view toowork with hello cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a><span data-ttu-id="e53b4-219">Configurar Olá aplicativo toouse stackexchange. Redis</span><span class="sxs-lookup"><span data-stu-id="e53b4-219">Configure hello application toouse StackExchange.Redis</span></span>
1. <span data-ttu-id="e53b4-220">tooconfigure um aplicativo cliente no Visual Studio usando Olá pacote NuGet stackexchange. Redis, clique em **NuGet Package Manager**, **Package Manager Console** de saudação **ferramentas** menu.</span><span class="sxs-lookup"><span data-stu-id="e53b4-220">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="e53b4-221">Execução hello seguinte comando do hello `Package Manager Console` janela.</span><span class="sxs-lookup"><span data-stu-id="e53b4-221">Run hello following command from hello `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="e53b4-222">Olá NuGet pacote baixa e adiciona Olá necessárias referências de assembly para tooaccess seu aplicativo de cliente Cache Redis do Azure com o cliente de cache Stackexchange hello.</span><span class="sxs-lookup"><span data-stu-id="e53b4-222">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span> <span data-ttu-id="e53b4-223">Se você preferir toouse uma versão de nome forte do hello `StackExchange.Redis` biblioteca de cliente, instale Olá `StackExchange.Redis.StrongName` pacote.</span><span class="sxs-lookup"><span data-stu-id="e53b4-223">If you prefer toouse a strong-named version of hello `StackExchange.Redis` client library, install hello `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="e53b4-224">Em **Solution Explorer**, expanda Olá **controladores** pasta e clique duas vezes em **TeamsController.cs** tooopen-lo.</span><span class="sxs-lookup"><span data-stu-id="e53b4-224">In **Solution Explorer**, expand hello **Controllers** folder and double-click **TeamsController.cs** tooopen it.</span></span>
   
    ![Controlador de equipes][cache-teamscontroller]
4. <span data-ttu-id="e53b4-226">Adicionar Olá após dois `using` instruções muito**TeamsController.cs**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-226">Add hello following two `using` statements too**TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="e53b4-227">Adicionar Olá toohello de duas propriedades a seguir `TeamsController` classe.</span><span class="sxs-lookup"><span data-stu-id="e53b4-227">Add hello following two properties toohello `TeamsController` class.</span></span>

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

6. <span data-ttu-id="e53b4-228">Criar um arquivo em seu computador denominado `WebAppPlusCacheAppSecrets.config` e colocá-lo em um local que não verificado com o código-fonte saudação do seu aplicativo de exemplo, se você decidir toocheck em algum lugar.</span><span class="sxs-lookup"><span data-stu-id="e53b4-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with hello source code of your sample application, should you decide toocheck it in somewhere.</span></span> <span data-ttu-id="e53b4-229">Em Olá Este exemplo `AppSettingsSecrets.config` arquivo está localizado em `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span><span class="sxs-lookup"><span data-stu-id="e53b4-229">In this example hello `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="e53b4-230">Editar saudação `WebAppPlusCacheAppSecrets.config` e adicione Olá conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="e53b4-230">Edit hello `WebAppPlusCacheAppSecrets.config` file and add hello following contents.</span></span> <span data-ttu-id="e53b4-231">Se você executar o aplicativo hello localmente essa informação é instância de Cache Redis do Azure tooyour tooconnect usado.</span><span class="sxs-lookup"><span data-stu-id="e53b4-231">If you run hello application locally this information is used tooconnect tooyour Azure Redis Cache instance.</span></span> <span data-ttu-id="e53b4-232">Mais tarde no tutorial Olá você provisionar uma instância de Cache Redis do Azure e atualize a senha e o nome do cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-232">Later in hello tutorial you'll provision an Azure Redis Cache instance and update hello cache name and password.</span></span> <span data-ttu-id="e53b4-233">Se você não planejar o aplicativo de exemplo hello toorun localmente, você pode ignorar a criação desse arquivo hello e etapas subsequentes de saudação que fazem referência a arquivo hello, pois quando você implanta o aplicativo de hello tooAzure recupera informações de conexão de cache de saudação do aplicativo hello a configuração para Olá Web App e não a partir desse arquivo.</span><span class="sxs-lookup"><span data-stu-id="e53b4-233">If you don't plan toorun hello sample application locally you can skip hello creation of this file and hello subsequent steps that reference hello file, because when you deploy tooAzure hello application retrieves hello cache connection information from hello app setting for hello Web App and not from this file.</span></span> <span data-ttu-id="e53b4-234">Desde Olá `WebAppPlusCacheAppSecrets.config` não está implantado tooAzure com seu aplicativo, você não é necessária a menos que você vai toorun aplicativo de hello localmente.</span><span class="sxs-lookup"><span data-stu-id="e53b4-234">Since hello `WebAppPlusCacheAppSecrets.config` is not deployed tooAzure with your application, you don't need it unless you are going toorun hello application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="e53b4-235">Em **Solution Explorer**, clique duas vezes em **Web. config** tooopen-lo.</span><span class="sxs-lookup"><span data-stu-id="e53b4-235">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="e53b4-237">Adicione o seguinte Olá `file` atributo toohello `appSettings` elemento.</span><span class="sxs-lookup"><span data-stu-id="e53b4-237">Add hello following `file` attribute toohello `appSettings` element.</span></span> <span data-ttu-id="e53b4-238">Se você usou um nome de arquivo diferente ou local, substitua os valores para Olá aqueles mostrado no exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="e53b4-238">If you used a different file name or location, substitute those values for hello ones shown in hello example.</span></span>
   
   * <span data-ttu-id="e53b4-239">Antes: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="e53b4-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="e53b4-240">Após: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="e53b4-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="e53b4-241">tempo de execução do ASP.NET Olá mescla o conteúdo de saudação de arquivo externo de saudação com marcações Olá Olá `<appSettings>` elemento.</span><span class="sxs-lookup"><span data-stu-id="e53b4-241">hello ASP.NET runtime merges hello contents of hello external file with hello markup in hello `<appSettings>` element.</span></span> <span data-ttu-id="e53b4-242">tempo de execução Olá ignora o atributo de arquivo hello se Olá especificado não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="e53b4-242">hello runtime ignores hello file attribute if hello specified file cannot be found.</span></span> <span data-ttu-id="e53b4-243">Seus segredos (cache de tooyour de cadeia de caracteres de conexão Olá) não são incluídos como parte do código-fonte para o aplicativo hello hello.</span><span class="sxs-lookup"><span data-stu-id="e53b4-243">Your secrets (hello connection string tooyour cache) are not included as part of hello source code for hello application.</span></span> <span data-ttu-id="e53b4-244">Quando você implanta seu tooAzure de aplicativo web, Olá `WebAppPlusCacheAppSecrests.config` arquivo não será implantado (ou seja, o que você deseja).</span><span class="sxs-lookup"><span data-stu-id="e53b4-244">When you deploy your web app tooAzure, hello `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="e53b4-245">Há várias toospecify de maneiras desses segredos no Azure e neste tutorial estão configurados automaticamente para você quando você [provisionar Olá recursos do Azure](#provision-the-azure-resources) em uma etapa posterior do tutorial.</span><span class="sxs-lookup"><span data-stu-id="e53b4-245">There are several ways toospecify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision hello Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="e53b4-246">Para obter mais informações sobre como trabalhar com segredos no Azure, consulte [práticas recomendadas para a implantação de senhas e outros dados confidenciais tooASP.NET e o serviço de aplicativo do Azure](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span><span class="sxs-lookup"><span data-stu-id="e53b4-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data tooASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a><span data-ttu-id="e53b4-247">Atualizar Olá TeamsController classe tooreturn resultados do cache de saudação ou de banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="e53b4-247">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>
<span data-ttu-id="e53b4-248">Neste exemplo, estatísticas podem ser recuperadas do banco de dados de saudação ou de cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-248">In this sample, team statistics can be retrieved from hello database or from hello cache.</span></span> <span data-ttu-id="e53b4-249">Estatísticas de equipe são armazenadas no cache de saudação como um serializado `List<Team>`e também como um conjunto classificado usando tipos de dados do Redis.</span><span class="sxs-lookup"><span data-stu-id="e53b4-249">Team statistics are stored in hello cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="e53b4-250">Ao recuperar itens de um conjunto ordenado, você pode recuperar alguns ou todos os itens ou consultar determinados itens.</span><span class="sxs-lookup"><span data-stu-id="e53b4-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="e53b4-251">Neste exemplo, você vai consultar conjunto Olá classificado para 5 equipes principais Olá classificados pelo número de wins.</span><span class="sxs-lookup"><span data-stu-id="e53b4-251">In this sample you'll query hello sorted set for hello top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="e53b4-252">Não é necessário toostore Olá estatísticas em vários formatos em cache de saudação na ordem toouse Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="e53b4-252">It is not required toostore hello team statistics in multiple formats in hello cache in order toouse Azure Redis Cache.</span></span> <span data-ttu-id="e53b4-253">Este tutorial usa vários toodemonstrate de formatos de algumas maneiras diferentes de saudação e tipos de dados diferentes, você pode usar dados de toocache.</span><span class="sxs-lookup"><span data-stu-id="e53b4-253">This tutorial uses multiple formats toodemonstrate some of hello different ways and different data types you can use toocache data.</span></span>
> 
> 

1. <span data-ttu-id="e53b4-254">Adicione o seguinte Olá `using` toohello instruções `TeamsController.cs` arquivo na parte superior da saudação com hello outros `using` instruções.</span><span class="sxs-lookup"><span data-stu-id="e53b4-254">Add hello following `using` statements toohello `TeamsController.cs` file at hello top with hello other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="e53b4-255">Substituir saudação atual `public ActionResult Index()` implementação de método com hello implementação a seguir.</span><span class="sxs-lookup"><span data-stu-id="e53b4-255">Replace hello current `public ActionResult Index()` method implementation with hello following implementation.</span></span>

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


1. <span data-ttu-id="e53b4-256">Adicionar Olá toohello de três métodos a seguir `TeamsController` Olá de tooimplement classe `playGames`, `clearCache`, e `rebuildDB` tipos de ação de saudação alternar instrução adicionada no trecho de código anterior hello.</span><span class="sxs-lookup"><span data-stu-id="e53b4-256">Add hello following three methods toohello `TeamsController` class tooimplement hello `playGames`, `clearCache`, and `rebuildDB` action types from hello switch statement added in hello previous code snippet.</span></span>
   
    <span data-ttu-id="e53b4-257">Olá `PlayGames` método atualiza estatísticas Olá simulando uma estação de jogos, salva Olá banco de dados de toohello resultados e Olá limpa dados de cache Olá obsoletas.</span><span class="sxs-lookup"><span data-stu-id="e53b4-257">hello `PlayGames` method updates hello team statistics by simulating a season of games, saves hello results toohello database, and clears hello now outdated data from hello cache.</span></span>

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

    <span data-ttu-id="e53b4-258">Olá `RebuildDB` Olá método reinicializar banco de dados com o conjunto padrão de saudação de equipes, gera estatísticas para eles, e limpa Olá obsoletas dados do cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-258">hello `RebuildDB` method reinitializes hello database with hello default set of teams, generates statistics for them, and clears hello now outdated data from hello cache.</span></span>

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

    <span data-ttu-id="e53b4-259">Olá `ClearCachedTeams` método Remove todas as estatísticas de equipe em cache do cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-259">hello `ClearCachedTeams` method removes any cached team statistics from hello cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="e53b4-260">Adicionar Olá toohello de quatro métodos a seguir `TeamsController` Olá tooimplement de classe várias maneiras de recuperar estatísticas da saudação do cache hello e banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-260">Add hello following four methods toohello `TeamsController` class tooimplement hello various ways of retrieving hello team statistics from hello cache and hello database.</span></span> <span data-ttu-id="e53b4-261">Cada um desses métodos retorna um `List<Team>` que é exibido pelo modo de exibição de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-261">Each of these methods returns a `List<Team>` which is then displayed by hello view.</span></span>
   
    <span data-ttu-id="e53b4-262">Olá `GetFromDB` método lê estatísticas da saudação do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-262">hello `GetFromDB` method reads hello team statistics from hello database.</span></span>
   
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

    <span data-ttu-id="e53b4-263">Olá `GetFromList` método leituras de estatísticas da saudação do cache como um serializado `List<Team>`.</span><span class="sxs-lookup"><span data-stu-id="e53b4-263">hello `GetFromList` method reads hello team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="e53b4-264">Se houver um erro de cache, Olá estatísticas são de leitura do banco de dados de saudação e armazenadas em cache Olá na próxima vez.</span><span class="sxs-lookup"><span data-stu-id="e53b4-264">If there is a cache miss, hello team statistics are read from hello database and then stored in hello cache for next time.</span></span> <span data-ttu-id="e53b4-265">Neste exemplo estamos usando JSON.NET serialização tooserialize Olá .NET objetos tooand do cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-265">In this sample we're using JSON.NET serialization tooserialize hello .NET objects tooand from hello cache.</span></span> <span data-ttu-id="e53b4-266">Para obter mais informações, consulte [como toowork com .NET objetos no Cache Redis do Azure](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span><span class="sxs-lookup"><span data-stu-id="e53b4-266">For more information, see [How toowork with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

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

    <span data-ttu-id="e53b4-267">Olá `GetFromSortedSet` método lê estatísticas da saudação de um conjunto classificado em cache.</span><span class="sxs-lookup"><span data-stu-id="e53b4-267">hello `GetFromSortedSet` method reads hello team statistics from a cached sorted set.</span></span> <span data-ttu-id="e53b4-268">Se houver um erro de cache, Olá estatísticas são de leitura do banco de dados de saudação e armazenadas em cache de saudação como um conjunto ordenado.</span><span class="sxs-lookup"><span data-stu-id="e53b4-268">If there is a cache miss, hello team statistics are read from hello database and stored in hello cache as a sorted set.</span></span>

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

    <span data-ttu-id="e53b4-269">Olá `GetFromSortedSetTop5` método lê conjunto superior de 5 equipes de saudação em cache classificados hello.</span><span class="sxs-lookup"><span data-stu-id="e53b4-269">hello `GetFromSortedSetTop5` method reads hello top 5 teams from hello cached sorted set.</span></span> <span data-ttu-id="e53b4-270">Ele começa pela verificando existência Olá Olá Olá cache `teamsSortedSet` chave.</span><span class="sxs-lookup"><span data-stu-id="e53b4-270">It starts by checking hello cache for hello existence of hello `teamsSortedSet` key.</span></span> <span data-ttu-id="e53b4-271">Se essa chave não estiver presente, Olá `GetFromSortedSet` método é chamado estatísticas Olá tooread e armazená-los no cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-271">If this key is not present, hello `GetFromSortedSet` method is called tooread hello team statistics and store them in hello cache.</span></span> <span data-ttu-id="e53b4-272">Em seguida, hello conjunto classificado em cache é consultado para Olá top 5 equipes que são retornadas.</span><span class="sxs-lookup"><span data-stu-id="e53b4-272">Next, hello cached sorted set is queried for hello top 5 teams which are returned.</span></span>

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

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a><span data-ttu-id="e53b4-273">Atualizar Olá criar, editar e excluir toowork métodos com cache Olá</span><span class="sxs-lookup"><span data-stu-id="e53b4-273">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>
<span data-ttu-id="e53b4-274">código de scaffolding Olá gerado como parte deste exemplo inclui métodos tooadd, editar e excluir equipes.</span><span class="sxs-lookup"><span data-stu-id="e53b4-274">hello scaffolding code that was generated as part of this sample includes methods tooadd, edit, and delete teams.</span></span> <span data-ttu-id="e53b4-275">Sempre que uma equipe é adicionada, editada ou removida, dados de saudação no cache de saudação ficarão desatualizados.</span><span class="sxs-lookup"><span data-stu-id="e53b4-275">Anytime a team is added, edited, or removed, hello data in hello cache becomes outdated.</span></span> <span data-ttu-id="e53b4-276">Nesta seção, que você modificará a saudação de tooclear esses três métodos armazenados em cache equipes para que o cache de saudação não estar fora de sincronia com o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-276">In this section you'll modify these three methods tooclear hello cached teams so that hello cache won't be out of sync with hello database.</span></span>

1. <span data-ttu-id="e53b4-277">Procurar toohello `Create(Team team)` método hello `TeamsController` classe.</span><span class="sxs-lookup"><span data-stu-id="e53b4-277">Browse toohello `Create(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="e53b4-278">Adicionar uma chamada toohello `ClearCachedTeams` método, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-278">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

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


1. <span data-ttu-id="e53b4-279">Procurar toohello `Edit(Team team)` método hello `TeamsController` classe.</span><span class="sxs-lookup"><span data-stu-id="e53b4-279">Browse toohello `Edit(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="e53b4-280">Adicionar uma chamada toohello `ClearCachedTeams` método, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-280">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

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


1. <span data-ttu-id="e53b4-281">Procurar toohello `DeleteConfirmed(int id)` método hello `TeamsController` classe.</span><span class="sxs-lookup"><span data-stu-id="e53b4-281">Browse toohello `DeleteConfirmed(int id)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="e53b4-282">Adicionar uma chamada toohello `ClearCachedTeams` método, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-282">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

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


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a><span data-ttu-id="e53b4-283">Atualizar Olá equipes índice exibição toowork com cache Olá</span><span class="sxs-lookup"><span data-stu-id="e53b4-283">Update hello Teams Index view toowork with hello cache</span></span>
1. <span data-ttu-id="e53b4-284">Em **Solution Explorer**, expanda Olá **exibições** pasta e, em seguida, Olá **equipes** pasta e clique duas vezes em **cshtml**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-284">In **Solution Explorer**, expand hello **Views** folder, then hello **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="e53b4-286">Superior saudação do arquivo hello, procure Olá elemento parágrafo a seguir.</span><span class="sxs-lookup"><span data-stu-id="e53b4-286">Near hello top of hello file, look for hello following paragraph element.</span></span>
   
    ![Tabela de ação][cache-teams-index-table]
   
    <span data-ttu-id="e53b4-288">Isso é Olá link toocreate um novo agrupamento.</span><span class="sxs-lookup"><span data-stu-id="e53b4-288">This is hello link toocreate a new team.</span></span> <span data-ttu-id="e53b4-289">Substitua o elemento de parágrafo Olá Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="e53b4-289">Replace hello paragraph element with hello following table.</span></span> <span data-ttu-id="e53b4-290">Esta tabela tem links de ação para criar uma nova equipe, executar uma nova estação de jogos, limpando o cache de saudação, recuperando equipes de saudação do cache de saudação em vários formatos, recuperando equipes de saudação do banco de dados de saudação e recompilar Olá banco de dados com dados de exemplo atualizado.</span><span class="sxs-lookup"><span data-stu-id="e53b4-290">This table has action links for creating a new team, playing a new season of games, clearing hello cache, retrieving hello teams from hello cache in several formats, retrieving hello teams from hello database, and rebuilding hello database with fresh sample data.</span></span>

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


1. <span data-ttu-id="e53b4-291">Rolar para o fim da saudação toohello **cshtml** de arquivo e adicione o seguinte Olá `tr` elemento para que ele seja a última linha Olá Olá última tabela no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="e53b4-291">Scroll toohello bottom of hello **Index.cshtml** file and add hello following `tr` element so that it is hello last row in hello last table in hello file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="e53b4-292">Esta linha exibe o valor de saudação do `ViewBag.Msg` que contém um relatório de status sobre a operação atual de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-292">This row displays hello value of `ViewBag.Msg` which contains a status report about hello current operation.</span></span> <span data-ttu-id="e53b4-293">Olá `ViewBag.Msg` é definido quando você clicar em qualquer um dos links de ação de saudação da etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="e53b4-293">hello `ViewBag.Msg` is set when you click any of hello action links from hello previous step.</span></span>   
   
    ![Mensagem de status][cache-status-message]
2. <span data-ttu-id="e53b4-295">Pressione **F6** toobuild projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-295">Press **F6** toobuild hello project.</span></span>

## <a name="provision-hello-azure-resources"></a><span data-ttu-id="e53b4-296">Provisionar Olá recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="e53b4-296">Provision hello Azure resources</span></span>
<span data-ttu-id="e53b4-297">toohost seu aplicativo no Azure, você deve primeiro provisionar Olá serviços do Azure que seu aplicativo requer.</span><span class="sxs-lookup"><span data-stu-id="e53b4-297">toohost your application in Azure, you must first provision hello Azure services that your application requires.</span></span> <span data-ttu-id="e53b4-298">aplicativo de exemplo Hello neste tutorial usa Olá seguindo os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="e53b4-298">hello sample application in this tutorial uses hello following Azure services.</span></span>

* <span data-ttu-id="e53b4-299">Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="e53b4-299">Azure Redis Cache</span></span>
* <span data-ttu-id="e53b4-300">Aplicativo Web do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="e53b4-300">App Service Web App</span></span>
* <span data-ttu-id="e53b4-301">Banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="e53b4-301">SQL Database</span></span>

<span data-ttu-id="e53b4-302">toodeploy essas serviços tooa recursos novos ou existentes do grupo de sua escolha, clique em Olá após **implantar tooAzure** botão.</span><span class="sxs-lookup"><span data-stu-id="e53b4-302">toodeploy these services tooa new or existing resource group of your choice, click hello following **Deploy tooAzure** button.</span></span>

<span data-ttu-id="e53b4-303">[! [Implantar tooAzure] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="e53b4-303">[![Deploy tooAzure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="e53b4-304">Isso **implantar tooAzure** botão usa Olá [criar um aplicativo Web mais o Cache Redis mais o banco de dados SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [início rápido do Azure](https://github.com/Azure/azure-quickstart-templates) modelo tooprovision esses serviços e o conjunto Olá cadeia de caracteres de conexão para a configuração do aplicativo de banco de dados SQL e hello do Olá para Olá cadeia de caracteres de conexão de Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="e53b4-304">This **Deploy tooAzure** button uses hello [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template tooprovision these services and set hello connection string for hello SQL Database and hello application setting for hello Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="e53b4-305">Se não tiver uma conta do Azure, você poderá [criar uma conta gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="e53b4-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="e53b4-306">Olá clicando em **implantar tooAzure** botão leva toohello portal do Azure e inicia Olá o processo de criação de recursos Olá descritos pelo modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-306">Clicking hello **Deploy tooAzure** button takes you toohello Azure portal and initiates hello process of creating hello resources described by hello template.</span></span>

![Implantar tooAzure][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="e53b4-308">Em Olá **Noções básicas de** seção, selecione Olá toouse de assinatura do Azure, selecione um grupo de recursos existente ou crie um novo e especifique o local do grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-308">In hello **Basics** section, select hello Azure subscription toouse, and select an existing resource group or create a new one, and specify hello resource group location.</span></span>
2. <span data-ttu-id="e53b4-309">Em Olá **configurações** seção, especifique um **logon de administrador** (não use **admin**), **senha de logon de administrador**e  **Nome do banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-309">In hello **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="e53b4-310">Olá outros parâmetros são configurados para um serviço de aplicativo gratuito hospedagem plano e as opções de baixo custo para hello banco de dados SQL e o Cache Redis do Azure, que não vêm com uma camada gratuita.</span><span class="sxs-lookup"><span data-stu-id="e53b4-310">hello other parameters are configured for a free App Service hosting plan, and lower-cost options for hello SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![Implantar tooAzure][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="e53b4-312">Depois de configurar as configurações de saudação desejada, role toohello final da página hello, Olá leitura termos e as condições e verificar Olá **concordo toohello termos e condições declaradas acima** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="e53b4-312">After configuring hello desired settings, scroll toohello end of hello page, read hello terms and conditions, and check hello **I agree toohello terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="e53b4-313">provisionar recursos de saudação toobegin, clique em **compra**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-313">toobegin provisioning hello resources, click **Purchase**.</span></span>

<span data-ttu-id="e53b4-314">progresso de saudação tooview de sua implantação, clique o ícone de notificação hello e clique em **implantação iniciada**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-314">tooview hello progress of your deployment, click hello notification icon and click **Deployment started**.</span></span>

![Implantação iniciada][cache-deployment-started]

<span data-ttu-id="e53b4-316">Você pode exibir o status de saudação da sua implantação em Olá **Microsoft.Template** folha.</span><span class="sxs-lookup"><span data-stu-id="e53b4-316">You can view hello status of your deployment on hello **Microsoft.Template** blade.</span></span>

![Implantar tooAzure][cache-deploy-to-azure-step-3]

<span data-ttu-id="e53b4-318">Quando o provisionamento for concluído, você pode publicar seu tooAzure de aplicativo do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e53b4-318">When provisioning is complete, you can publish your application tooAzure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="e53b4-319">Os erros que podem ocorrer durante o processo de provisionamento de saudação são exibidos em Olá **Microsoft.Template** folha.</span><span class="sxs-lookup"><span data-stu-id="e53b4-319">Any errors that may occur during hello provisioning process are displayed on hello **Microsoft.Template** blade.</span></span> <span data-ttu-id="e53b4-320">Alguns erros comuns são muitos Servidores SQL ou muitos planos de hospedagem do Serviço de Aplicativo gratuitos por assinatura.</span><span class="sxs-lookup"><span data-stu-id="e53b4-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="e53b4-321">Resolva quaisquer erros e reiniciar o processo de saudação clicando **reimplantar** em Olá **Microsoft.Template** folha ou hello **implantar tooAzure** botão neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="e53b4-321">Resolve any errors and restart hello process by clicking **Redeploy** on hello **Microsoft.Template** blade or hello **Deploy tooAzure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-hello-application-tooazure"></a><span data-ttu-id="e53b4-322">Publicar Olá aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="e53b4-322">Publish hello application tooAzure</span></span>
<span data-ttu-id="e53b4-323">Nesta etapa do tutorial hello, você publicar Olá tooAzure de aplicativo e executá-lo na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="e53b4-323">In this step of hello tutorial, you'll publish hello application tooAzure and run it in hello cloud.</span></span>

1. <span data-ttu-id="e53b4-324">Saudação de atalho **ContosoTeamStats** do projeto no Visual Studio e escolha **publicar**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-324">Right-click hello **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![Publicar][cache-publish-app]
2. <span data-ttu-id="e53b4-326">Clique em **Serviço de Aplicativo do Microsoft Azure**, escolha **Selecionar Existente** e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![Publicar][cache-publish-to-app-service]
3. <span data-ttu-id="e53b4-328">Selecione a assinatura Olá usada quando criar hello recursos do Azure, expanda o grupo de recursos de saudação contendo os recursos de saudação e selecione Olá desejado de aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e53b4-328">Select hello subscription used when creating hello Azure resources, expand hello resource group containing hello resources, and select hello desired Web App.</span></span> <span data-ttu-id="e53b4-329">Se você usou Olá **implantar tooAzure** botão, o nome do aplicativo Web começa com **site** seguido por alguns caracteres adicionais.</span><span class="sxs-lookup"><span data-stu-id="e53b4-329">If you used hello **Deploy tooAzure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![Selecionar aplicativo Web][cache-select-web-app]
4. <span data-ttu-id="e53b4-331">Clique em **Okey** toobegin Olá processo de publicação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-331">Click **OK** toobegin hello publishing process.</span></span> <span data-ttu-id="e53b4-332">Após alguns instantes Olá processo de publicação for concluída e um navegador é iniciado com hello executando o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="e53b4-332">After a few moments hello publishing process completes and a browser is launched with hello running sample application.</span></span> <span data-ttu-id="e53b4-333">Se você receber um erro ao validar ou publicação de DNS e Olá processo para o provisionamento hello recursos do Azure para o aplicativo hello recentemente concluiu, aguarde um momento e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="e53b4-333">If you get a DNS error when validating or publishing, and hello provisioning process for hello Azure resources for hello application has just recently completed, wait a moment and try again.</span></span>
   
    ![Cache adicionado][cache-added-to-application]

<span data-ttu-id="e53b4-335">Olá tabela a seguir descreve cada link de ação do aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="e53b4-335">hello following table describes each action link from hello sample application.</span></span>

| <span data-ttu-id="e53b4-336">Ação</span><span class="sxs-lookup"><span data-stu-id="e53b4-336">Action</span></span> | <span data-ttu-id="e53b4-337">Descrição</span><span class="sxs-lookup"><span data-stu-id="e53b4-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e53b4-338">Criar Novo</span><span class="sxs-lookup"><span data-stu-id="e53b4-338">Create New</span></span> |<span data-ttu-id="e53b4-339">Criar uma nova Equipe.</span><span class="sxs-lookup"><span data-stu-id="e53b4-339">Create a new Team.</span></span> |
| <span data-ttu-id="e53b4-340">Reproduzir Temporada</span><span class="sxs-lookup"><span data-stu-id="e53b4-340">Play Season</span></span> |<span data-ttu-id="e53b4-341">Reproduzir uma estação de jogos, atualização de estatísticas de equipe Olá, e desmarque qualquer desatualizadas dados da equipe do cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-341">Play a season of games, update hello team stats, and clear any outdated team data from hello cache.</span></span> |
| <span data-ttu-id="e53b4-342">Limpar Cache</span><span class="sxs-lookup"><span data-stu-id="e53b4-342">Clear Cache</span></span> |<span data-ttu-id="e53b4-343">Estatísticas de equipe Olá clara do cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-343">Clear hello team stats from hello cache.</span></span> |
| <span data-ttu-id="e53b4-344">Listar do Cache</span><span class="sxs-lookup"><span data-stu-id="e53b4-344">List from Cache</span></span> |<span data-ttu-id="e53b4-345">Recupere estatísticas da equipe de saudação do cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-345">Retrieve hello team stats from hello cache.</span></span> <span data-ttu-id="e53b4-346">Se houver um erro de cache, carregar estatísticas de saudação do banco de dados de saudação e salvar toohello cache na próxima vez.</span><span class="sxs-lookup"><span data-stu-id="e53b4-346">If there is a cache miss, load hello stats from hello database and save toohello cache for next time.</span></span> |
| <span data-ttu-id="e53b4-347">Conjunto Ordenado do Cache</span><span class="sxs-lookup"><span data-stu-id="e53b4-347">Sorted Set from Cache</span></span> |<span data-ttu-id="e53b4-348">Recupere estatísticas da equipe de saudação do cache de saudação usando um conjunto ordenado.</span><span class="sxs-lookup"><span data-stu-id="e53b4-348">Retrieve hello team stats from hello cache using a sorted set.</span></span> <span data-ttu-id="e53b4-349">Se houver um erro de cache, estatísticas de saudação do banco de dados de saudação e salva toohello cache usando um conjunto ordenado.</span><span class="sxs-lookup"><span data-stu-id="e53b4-349">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="e53b4-350">Cinco Principais Equipes do Cache</span><span class="sxs-lookup"><span data-stu-id="e53b4-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="e53b4-351">Recupere 5 equipes principais de saudação do cache de saudação usando um conjunto ordenado.</span><span class="sxs-lookup"><span data-stu-id="e53b4-351">Retrieve hello top 5 teams from hello cache using a sorted set.</span></span> <span data-ttu-id="e53b4-352">Se houver um erro de cache, estatísticas de saudação do banco de dados de saudação e salva toohello cache usando um conjunto ordenado.</span><span class="sxs-lookup"><span data-stu-id="e53b4-352">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="e53b4-353">Carregar do banco de dados</span><span class="sxs-lookup"><span data-stu-id="e53b4-353">Load from DB</span></span> |<span data-ttu-id="e53b4-354">Recupere estatísticas da equipe de saudação do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-354">Retrieve hello team stats from hello database.</span></span> |
| <span data-ttu-id="e53b4-355">Recriar o banco de dados</span><span class="sxs-lookup"><span data-stu-id="e53b4-355">Rebuild DB</span></span> |<span data-ttu-id="e53b4-356">Recriar o banco de dados de saudação e recarregá-lo com dados da equipe de exemplo.</span><span class="sxs-lookup"><span data-stu-id="e53b4-356">Rebuild hello database and reload it with sample team data.</span></span> |
| <span data-ttu-id="e53b4-357">Editar/Detalhes/Excluir</span><span class="sxs-lookup"><span data-stu-id="e53b4-357">Edit / Details / Delete</span></span> |<span data-ttu-id="e53b4-358">Editar uma equipe, exibir detalhes de uma equipe, excluir uma equipe.</span><span class="sxs-lookup"><span data-stu-id="e53b4-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="e53b4-359">Clique em algumas das ações de saudação e fazer experiências com a recuperação de dados de saudação de origens diferentes hello.</span><span class="sxs-lookup"><span data-stu-id="e53b4-359">Click some of hello actions and experiment with retrieving hello data from hello different sources.</span></span> <span data-ttu-id="e53b4-360">Não Olá as diferenças no hello tempo Olá toocomplete várias maneiras de recuperar dados de saudação do banco de dados de saudação e cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-360">Not hello differences in hello time it takes toocomplete hello various ways of retrieving hello data from hello database and hello cache.</span></span>

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a><span data-ttu-id="e53b4-361">Excluir recursos de hello quando você tiver terminado com o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="e53b4-361">Delete hello resources when you are finished with hello application</span></span>
<span data-ttu-id="e53b4-362">Quando tiver terminado com aplicativo tutorial do exemplo hello, você pode excluir hello Azure recursos usados em ordem tooconserve custo e recursos.</span><span class="sxs-lookup"><span data-stu-id="e53b4-362">When you are finished with hello sample tutorial application, you can delete hello Azure resources used in order tooconserve cost and resources.</span></span> <span data-ttu-id="e53b4-363">Se você usar o hello **implantar tooAzure** botão Olá [provisionar Olá recursos do Azure](#provision-the-azure-resources) seção e todos os recursos estão contidos em Olá mesmo grupo de recursos, você pode excluí-los juntos em um operação, excluindo o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e53b4-363">If you use hello **Deploy tooAzure** button in hello [Provision hello Azure resources](#provision-the-azure-resources) section and all of your resources are contained in hello same resource group, you can delete them together in one operation by deleting hello resource group.</span></span>

1. <span data-ttu-id="e53b4-364">Entrar toohello [portal do Azure](https://portal.azure.com) e clique em **grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-364">Sign in toohello [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="e53b4-365">Nome de saudação do tipo do seu grupo de recursos em hello **filtrar itens...**  caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="e53b4-365">Type hello name of your resource group into hello **Filter items...** textbox.</span></span>
3. <span data-ttu-id="e53b4-366">Clique em **...**  toohello direita do seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e53b4-366">Click **...** toohello right of your resource group.</span></span>
4. <span data-ttu-id="e53b4-367">Clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-367">Click **Delete**.</span></span>
   
    ![Exclusão][cache-delete-resource-group]
5. <span data-ttu-id="e53b4-369">Nome do tipo saudação do seu grupo de recursos e clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="e53b4-369">Type hello name of your resource group and click **Delete**.</span></span>
   
    ![Confirmar exclusão][cache-delete-confirm]

<span data-ttu-id="e53b4-371">Depois de alguns recursos de saudação momentos grupo e todos os seus recursos contidos são excluídos.</span><span class="sxs-lookup"><span data-stu-id="e53b4-371">After a few moments hello resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e53b4-372">Observe que a exclusão de um grupo de recursos é irreversível e grupo de recursos de saudação e todos os recursos de saudação nela são excluídos permanentemente.</span><span class="sxs-lookup"><span data-stu-id="e53b4-372">Note that deleting a resource group is irreversible and that hello resource group and all hello resources in it are permanently deleted.</span></span> <span data-ttu-id="e53b4-373">Certifique-se de que você não acidentalmente excluir grupo de recurso incorreto hello ou recursos.</span><span class="sxs-lookup"><span data-stu-id="e53b4-373">Make sure that you do not accidentally delete hello wrong resource group or resources.</span></span> <span data-ttu-id="e53b4-374">Se você criou recursos Olá para hospedar este exemplo dentro de um grupo de recursos existente, você pode excluir individualmente cada recurso de seus respectivas folhas.</span><span class="sxs-lookup"><span data-stu-id="e53b4-374">If you created hello resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a><span data-ttu-id="e53b4-375">Execute o aplicativo de exemplo hello em seu computador local</span><span class="sxs-lookup"><span data-stu-id="e53b4-375">Run hello sample application on your local machine</span></span>
<span data-ttu-id="e53b4-376">aplicativo de hello toorun localmente no seu computador, você precisa de um Cache Redis do Azure da instância na qual toocache seus dados.</span><span class="sxs-lookup"><span data-stu-id="e53b4-376">toorun hello application locally on your machine, you need an Azure Redis Cache instance in which toocache your data.</span></span> 

* <span data-ttu-id="e53b4-377">Se você tiver publicado seu aplicativo tooAzure conforme descrito na seção anterior hello, você pode usar a instância de Cache Redis do Azure de saudação que estava provisionada durante essa etapa.</span><span class="sxs-lookup"><span data-stu-id="e53b4-377">If you have published your application tooAzure as described in hello previous section, you can use hello Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="e53b4-378">Se você tiver outra instância existente do Cache Redis do Azure, você pode usar esse toorun Este exemplo localmente.</span><span class="sxs-lookup"><span data-stu-id="e53b4-378">If you have another existing Azure Redis Cache instance, you can use that toorun this sample locally.</span></span>
* <span data-ttu-id="e53b4-379">Se você precisar toocreate uma instância de Cache Redis do Azure, você pode seguir etapas Olá [criar um cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="e53b4-379">If you need toocreate an Azure Redis Cache instance, you can follow hello steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="e53b4-380">Depois que você selecionar ou criar hello cache toouse, procurar toohello cache no portal do Azure de saudação e recuperar Olá [nome de host](cache-configure.md#properties) e [chaves de acesso](cache-configure.md#access-keys) para seu cache.</span><span class="sxs-lookup"><span data-stu-id="e53b4-380">Once you have selected or created hello cache toouse, browse toohello cache in hello Azure portal and retrieve hello [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="e53b4-381">Para obter instruções, confira [Definir configurações de cache Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="e53b4-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="e53b4-382">Olá abrir `WebAppPlusCacheAppSecrets.config` arquivo criado durante a saudação [configurar Olá aplicativo toouse Cache Redis](#configure-the-application-to-use-redis-cache) etapa deste tutorial, usando o editor de saudação de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="e53b4-382">Open hello `WebAppPlusCacheAppSecrets.config` file that you created during hello [Configure hello application toouse Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using hello editor of your choice.</span></span>
2. <span data-ttu-id="e53b4-383">Editar saudação `value` de atributos e substitua `MyCache.redis.cache.windows.net` com hello [nome de host](cache-configure.md#properties) do cache e especifique a saudação [chave primária ou secundária](cache-configure.md#access-keys) do cache como senha hello.</span><span class="sxs-lookup"><span data-stu-id="e53b4-383">Edit hello `value` attribute and replace `MyCache.redis.cache.windows.net` with hello [host name](cache-configure.md#properties) of your cache, and specify either hello [primary or secondary key](cache-configure.md#access-keys) of your cache as hello password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="e53b4-384">Pressione **Ctrl + F5** aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="e53b4-384">Press **Ctrl+F5** toorun hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="e53b4-385">Observe que o cache de Olá porque o aplicativo hello, incluindo o banco de dados hello, está em execução localmente e hello Redis Cache está hospedado no Azure, pode aparecer toounder-executar Olá banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e53b4-385">Note that because hello application, including hello database, is running locally and hello Redis Cache is hosted in Azure, hello cache may appear toounder-perform hello database.</span></span> <span data-ttu-id="e53b4-386">Para melhor desempenho, Olá aplicativo cliente e a instância de Cache Redis do Azure deve estar no hello mesmo local.</span><span class="sxs-lookup"><span data-stu-id="e53b4-386">For best performance, hello client application and Azure Redis Cache instance should be in hello same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e53b4-387">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e53b4-387">Next steps</span></span>
* <span data-ttu-id="e53b4-388">Saiba mais sobre [guia de Introdução ao ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) em Olá [ASP.NET](http://asp.net/) site.</span><span class="sxs-lookup"><span data-stu-id="e53b4-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on hello [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="e53b4-389">Para obter mais exemplos de criação de um aplicativo Web ASP.NET no serviço de aplicativo, consulte [criar e implantar um aplicativo da web ASP.NET no serviço de aplicativo do Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) de saudação [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 conectar [demonstração](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="e53b4-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="e53b4-390">Para mais guias de início rápido de demonstração de HealthClinic.biz hello, consulte [início rápido do Azure Developer Tools](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="e53b4-390">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="e53b4-391">Saiba mais sobre Olá [código primeiro tooa novo banco de dados](https://msdn.microsoft.com/data/jj193542) abordagem tooEntity do Framework que é usado neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="e53b4-391">Learn more about hello [Code first tooa new database](https://msdn.microsoft.com/data/jj193542) approach tooEntity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="e53b4-392">Saiba mais sobre [aplicativos Web no Serviço de Aplicativo do Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e53b4-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="e53b4-393">Saiba como muito[monitor](cache-how-to-monitor.md) o cache do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e53b4-393">Learn how too[monitor](cache-how-to-monitor.md) your cache in hello Azure portal.</span></span>
* <span data-ttu-id="e53b4-394">Explore os recursos premium do Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="e53b4-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="e53b4-395">Como tooconfigure persistência para um Premium do Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="e53b4-395">How tooconfigure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="e53b4-396">Como tooconfigure clustering para um Premium do Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="e53b4-396">How tooconfigure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="e53b4-397">Como o suporte a tooconfigure rede Virtual para um Premium do Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="e53b4-397">How tooconfigure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="e53b4-398">Consulte Olá [perguntas Frequentes de Cache Redis do Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) para obter mais detalhes sobre o tamanho, a taxa de transferência e a largura de banda com caches premium.</span><span class="sxs-lookup"><span data-stu-id="e53b4-398">See hello [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

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

