---
title: Como criar um Aplicativo Web com o Cache Redis | Microsoft Docs
description: Saiba como criar um aplicativo Web com o Cache Redis
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
ms.openlocfilehash: f23f71cc01eccf17d36885f786de9a7517606803
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-web-app-with-redis-cache"></a><span data-ttu-id="1006f-103">Como criar um aplicativo Web com o Cache Redis</span><span class="sxs-lookup"><span data-stu-id="1006f-103">How to create a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1006f-104">.NET</span><span class="sxs-lookup"><span data-stu-id="1006f-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="1006f-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1006f-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="1006f-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="1006f-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="1006f-107">Java</span><span class="sxs-lookup"><span data-stu-id="1006f-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="1006f-108">Python</span><span class="sxs-lookup"><span data-stu-id="1006f-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="1006f-109">Este tutorial mostra como criar e implantar um aplicativo Web ASP.NET em um aplicativo Web no Serviço de Aplicativo do Azure usando o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1006f-109">This tutorial shows how to create and deploy an ASP.NET web application to a web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="1006f-110">O aplicativo de exemplo exibe uma lista de estatísticas da equipe de um banco de dados e mostra diferentes maneiras de usar o Cache Redis do Azure para armazenar e recuperar dados do cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-110">The sample application displays a list of team statistics from a database and shows different ways to use Azure Redis Cache to store and retrieve data from the cache.</span></span> <span data-ttu-id="1006f-111">Ao concluir o tutorial, você terá um aplicativo Web em execução que lê e grava em um banco de dados, otimizado com o Cache Redis do Azure e hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="1006f-111">When you complete the tutorial you'll have a running web app that reads and writes to a database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="1006f-112">O que você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="1006f-112">You'll learn:</span></span>

* <span data-ttu-id="1006f-113">Como criar um aplicativo MVC 5 ASP.NET no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1006f-113">How to create an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="1006f-114">Como acessar dados de um banco de dados usando o Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="1006f-114">How to access data from a database using Entity Framework.</span></span>
* <span data-ttu-id="1006f-115">Como melhorar a taxa de transferência de dados e reduzir a carga do banco de dados armazenando e recuperando dados com o Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="1006f-115">How to improve data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="1006f-116">Como usar um conjunto classificado do Redis para recuperar as cinco equipes principais.</span><span class="sxs-lookup"><span data-stu-id="1006f-116">How to use a Redis sorted set to retrieve the top 5 teams.</span></span>
* <span data-ttu-id="1006f-117">Como provisionar os recursos do Azure para o aplicativo usando um modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1006f-117">How to provision the Azure resources for the application using a Resource Manager template.</span></span>
* <span data-ttu-id="1006f-118">Como publicar o aplicativo no Azure usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1006f-118">How to publish the application to Azure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1006f-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1006f-119">Prerequisites</span></span>
<span data-ttu-id="1006f-120">Para concluir o tutorial, você deve ter os pré-requisitos a seguir.</span><span class="sxs-lookup"><span data-stu-id="1006f-120">To complete the tutorial, you must have the following prerequisites.</span></span>

* [<span data-ttu-id="1006f-121">Conta do Azure</span><span class="sxs-lookup"><span data-stu-id="1006f-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="1006f-122">Visual Studio 2017 com o SDK do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="1006f-122">Visual Studio 2017 with the Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="1006f-123">Conta do Azure</span><span class="sxs-lookup"><span data-stu-id="1006f-123">Azure account</span></span>
<span data-ttu-id="1006f-124">Você precisa de uma conta do Azure para concluir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="1006f-124">You need an Azure account to complete the tutorial.</span></span> <span data-ttu-id="1006f-125">Você pode:</span><span class="sxs-lookup"><span data-stu-id="1006f-125">You can:</span></span>

* <span data-ttu-id="1006f-126">[Abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="1006f-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="1006f-127">Obtenha créditos que possam ser usados para experimentar os serviços pagos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1006f-127">You get credits that can be used to try out paid Azure services.</span></span> <span data-ttu-id="1006f-128">Mesmo depois que os créditos são usados, você pode manter a conta e usar os serviços e recursos gratuitos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1006f-128">Even after the credits are used up, you can keep the account and use free Azure services and features.</span></span>
* <span data-ttu-id="1006f-129">[Ativar benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="1006f-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="1006f-130">Todos os meses, sua assinatura do MSDN lhe oferece créditos que podem ser usados para serviços pagos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1006f-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-the-azure-sdk-for-net"></a><span data-ttu-id="1006f-131">Visual Studio 2017 com o SDK do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="1006f-131">Visual Studio 2017 with the Azure SDK for .NET</span></span>
<span data-ttu-id="1006f-132">O tutorial é escrito para o Visual Studio 2017 com o [SDK do Azure para .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span><span class="sxs-lookup"><span data-stu-id="1006f-132">The tutorial is written for Visual Studio 2017 with the [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="1006f-133">O SDK do Azure 2.9.5 está incluído com o instalador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1006f-133">The Azure SDK 2.9.5 is included with the Visual Studio installer.</span></span>

<span data-ttu-id="1006f-134">Se você tiver o Visual Studio 2015, siga o tutorial com o [SDK do Azure para .NET](../dotnet-sdk.md) 2.8.2 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1006f-134">If you have Visual Studio 2015, you can follow the tutorial with the [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="1006f-135">[Baixe o SDK mais recente do Azure para Visual Studio 2015 aqui](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="1006f-135">[Download the latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="1006f-136">O Visual Studio será instalado automaticamente com o SDK caso você ainda não o tenha.</span><span class="sxs-lookup"><span data-stu-id="1006f-136">Visual Studio is automatically installed with the SDK if you don't already have it.</span></span> <span data-ttu-id="1006f-137">Algumas telas podem parecer diferentes das ilustrações mostradas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="1006f-137">Some screens may look different from the illustrations shown in this tutorial.</span></span>

<span data-ttu-id="1006f-138">Se tiver o Visual Studio 2013, você poderá [baixar o SDK do Azure mais recente para o Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span><span class="sxs-lookup"><span data-stu-id="1006f-138">If you have Visual Studio 2013, you can [download the latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="1006f-139">Algumas telas podem parecer diferentes das ilustrações mostradas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="1006f-139">Some screens may look different from the illustrations shown in this tutorial.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="1006f-140">Criar o projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1006f-140">Create the Visual Studio project</span></span>
1. <span data-ttu-id="1006f-141">Abra o Visual Studio e clique em **Arquivo**, **Novo**, **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="1006f-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="1006f-142">Expanda o nó **Visual C#** na lista **Modelos**, selecione **Nuvem** e clique em **Aplicativo Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="1006f-142">Expand the **Visual C#** node in the **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="1006f-143">Verifique se **.NET Framework 4.5.2** ou superior está selecionado.</span><span class="sxs-lookup"><span data-stu-id="1006f-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="1006f-144">Digite **ContosoTeamStats** na caixa de texto **Nome** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="1006f-144">Type **ContosoTeamStats** into the **Name** textbox and click **OK**.</span></span>
   
    ![Criar projeto][cache-create-project]
3. <span data-ttu-id="1006f-146">Selecione **MVC** como o tipo de projeto.</span><span class="sxs-lookup"><span data-stu-id="1006f-146">Select **MVC** as the project type.</span></span> 

    <span data-ttu-id="1006f-147">Certifique-se de que a opção **Sem Autenticação** esteja especificada para as configurações **Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="1006f-147">Ensure that **No Authentication** is specified for the **Authentication** settings.</span></span> <span data-ttu-id="1006f-148">Dependendo de sua versão do Visual Studio, o padrão pode ser definido para algo diferente.</span><span class="sxs-lookup"><span data-stu-id="1006f-148">Depending on your version of Visual Studio, the default may be set to something else.</span></span> <span data-ttu-id="1006f-149">Para alterá-lo, clique em **Alterar Autenticação**e selecione **Sem Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="1006f-149">To change it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="1006f-150">Se você estiver acompanhando com o Visual Studio 2015, desmarque a caixa de seleção **Host na nuvem**.</span><span class="sxs-lookup"><span data-stu-id="1006f-150">If you are following along with Visual Studio 2015, clear the **Host in the cloud** checkbox.</span></span> <span data-ttu-id="1006f-151">Você vai [provisionar os recursos do Azure](#provision-the-azure-resources) e [publicar o aplicativo no Azure](#publish-the-application-to-azure) nas etapas subsequentes do tutorial.</span><span class="sxs-lookup"><span data-stu-id="1006f-151">You'll [provision the Azure resources](#provision-the-azure-resources) and [publish the application to Azure](#publish-the-application-to-azure) in subsequent steps in the tutorial.</span></span> <span data-ttu-id="1006f-152">Para obter um exemplo de provisionamento de um aplicativo Web do Serviço de Aplicativo do Visual Studio deixando a opção **Host na nuvem** marcada, confira [Introdução aos aplicativos Web no Serviço de Aplicativo do Azure, usando ASP.NET e Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="1006f-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in the cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![Selecionar modelo de projeto][cache-select-template]
4. <span data-ttu-id="1006f-154">Clique em **OK** para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="1006f-154">Click **OK** to create the project.</span></span>

## <a name="create-the-aspnet-mvc-application"></a><span data-ttu-id="1006f-155">Criar o aplicativo MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1006f-155">Create the ASP.NET MVC application</span></span>
<span data-ttu-id="1006f-156">Nesta seção do tutorial, você criará o aplicativo básico que lê e exibe estatísticas de equipe de um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1006f-156">In this section of the tutorial, you'll create the basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="1006f-157">Adicionar o pacote NuGet do Entity Framework</span><span class="sxs-lookup"><span data-stu-id="1006f-157">Add the Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="1006f-158">Adicionar o modelo</span><span class="sxs-lookup"><span data-stu-id="1006f-158">Add the model</span></span>](#add-the-model)
* [<span data-ttu-id="1006f-159">Adicionar controlador</span><span class="sxs-lookup"><span data-stu-id="1006f-159">Add the controller</span></span>](#add-the-controller)
* [<span data-ttu-id="1006f-160">Configurar os modos de exibição</span><span class="sxs-lookup"><span data-stu-id="1006f-160">Configure the views</span></span>](#configure-the-views)

### <a name="add-the-entity-framework-nuget-package"></a><span data-ttu-id="1006f-161">Adicionar o pacote NuGet do Entity Framework</span><span class="sxs-lookup"><span data-stu-id="1006f-161">Add the Entity Framework NuGet package</span></span>

1. <span data-ttu-id="1006f-162">Clique em **Gerenciador de Pacotes Nuget**, **Console do Gerenciador de Pacotes** no menu **Ferramentas**.</span><span class="sxs-lookup"><span data-stu-id="1006f-162">Click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="1006f-163">Execute o seguinte comando na janela **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="1006f-163">Run the following command from the **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="1006f-164">Para saber mais sobre este pacote, consulte a página do NuGet [EntityFramework](https://www.nuget.org/packages/EntityFramework/).</span><span class="sxs-lookup"><span data-stu-id="1006f-164">For more information about this package, see the [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-the-model"></a><span data-ttu-id="1006f-165">Adicionar o modelo</span><span class="sxs-lookup"><span data-stu-id="1006f-165">Add the model</span></span>
1. <span data-ttu-id="1006f-166">Clique com o botão direito do mouse em **Modelos** no **Gerenciador de Soluções** e escolha **Adicionar**, **Classe**.</span><span class="sxs-lookup"><span data-stu-id="1006f-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![Adicionar modelo][cache-model-add-class]
2. <span data-ttu-id="1006f-168">Insira `Team` como o nome da classe e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1006f-168">Enter `Team` for the class name and click **Add**.</span></span>
   
    ![Adicionar classe de modelo][cache-model-add-class-dialog]
3. <span data-ttu-id="1006f-170">Substitua as instruções `using` na parte superior do arquivo `Team.cs` pelas instruções `using` a seguir.</span><span class="sxs-lookup"><span data-stu-id="1006f-170">Replace the `using` statements at the top of the `Team.cs` file with the following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="1006f-171">Substitua a definição da classe `Team` pelo trecho de código a seguir, que contém uma definição de classe `Team` atualizada, bem como algumas outras classes auxiliares do Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="1006f-171">Replace the definition of the `Team` class with the following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="1006f-172">Para saber mais sobre a abordagem de code first do Entity Framework que é usada neste tutorial, confira [Code first para um novo banco de dados](https://msdn.microsoft.com/data/jj193542).</span><span class="sxs-lookup"><span data-stu-id="1006f-172">For more information on the code first approach to Entity Framework that's used in this tutorial, see [Code first to a new database](https://msdn.microsoft.com/data/jj193542).</span></span>

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


1. <span data-ttu-id="1006f-173">No **Gerenciador de Soluções**, clique duas vezes em **web.config** para abri-lo.</span><span class="sxs-lookup"><span data-stu-id="1006f-173">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="1006f-175">Adicione a seção `connectionStrings` a seguir.</span><span class="sxs-lookup"><span data-stu-id="1006f-175">Add the following `connectionStrings` section.</span></span> <span data-ttu-id="1006f-176">O nome da cadeia de conexão deve corresponder ao nome da classe de contexto de banco de dados do Entity Framework, que é `TeamContext`.</span><span class="sxs-lookup"><span data-stu-id="1006f-176">The name of the connection string must match the name of the Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="1006f-177">Adicione a nova seção `connectionStrings` para que ela siga `configSections`, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="1006f-177">You can add the new `connectionStrings` section so that it follows `configSections`, as shown in the following example.</span></span>

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
    > <span data-ttu-id="1006f-178">A cadeia de conexão pode ser diferente dependendo da versão do Visual Studio e da edição do SQL Server Express usadas para concluir o tutorial.</span><span class="sxs-lookup"><span data-stu-id="1006f-178">Your connection string may be different depending on the version of Visual Studio and SQL Server Express edition used to complete the tutorial.</span></span> <span data-ttu-id="1006f-179">O modelo web.config deve ser configurado para corresponder à sua instalação e pode conter `Data Source` entradas como `(LocalDB)\v11.0` (a partir do SQL Server Express 2012) ou `Data Source=(LocalDB)\MSSQLLocalDB` (do SQL Server 2014 Express e mais recente).</span><span class="sxs-lookup"><span data-stu-id="1006f-179">The web.config template should be configured to match your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="1006f-180">Para saber mais sobre cadeias de caracteres de conexão e versões do SQL Express, veja [LocalDB do SQL Server 2016 Express](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span><span class="sxs-lookup"><span data-stu-id="1006f-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-the-controller"></a><span data-ttu-id="1006f-181">Adicionar controlador</span><span class="sxs-lookup"><span data-stu-id="1006f-181">Add the controller</span></span>
1. <span data-ttu-id="1006f-182">Pressione **F6** para compilar o projeto.</span><span class="sxs-lookup"><span data-stu-id="1006f-182">Press **F6** to build the project.</span></span> 
2. <span data-ttu-id="1006f-183">No **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **Controladores** e escolha **Adicionar**, **Controlador**.</span><span class="sxs-lookup"><span data-stu-id="1006f-183">In **Solution Explorer**, right-click the **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![Adicionar controlador][cache-add-controller]
3. <span data-ttu-id="1006f-185">Escolha **Controlador MVC 5 com modos de exibição, usando o Entity Framework** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1006f-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="1006f-186">Se você receber um erro após clicar em **Adicionar**, verifique se criou o projeto primeiro.</span><span class="sxs-lookup"><span data-stu-id="1006f-186">If you get an error after clicking **Add**, ensure that you have built the project first.</span></span>
   
    ![Adicionar classe de controlador][cache-add-controller-class]
4. <span data-ttu-id="1006f-188">Selecione **Equipe (ContosoTeamStats.Models)** na lista suspensa **Classe de modelo**.</span><span class="sxs-lookup"><span data-stu-id="1006f-188">Select **Team (ContosoTeamStats.Models)** from the **Model class** drop-down list.</span></span> <span data-ttu-id="1006f-189">Selecione **TeamContext (ContosoTeamStats.Models)** na lista suspensa **Classe de contexto de dados**.</span><span class="sxs-lookup"><span data-stu-id="1006f-189">Select **TeamContext (ContosoTeamStats.Models)** from the **Data context class** drop-down list.</span></span> <span data-ttu-id="1006f-190">Digite `TeamsController` na caixa de texto de nome **Controlador** (se ela não for populada automaticamente).</span><span class="sxs-lookup"><span data-stu-id="1006f-190">Type `TeamsController` in the **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="1006f-191">Clique em **Adicionar** para criar a classe de controlador e adicionar os modos de exibição padrão.</span><span class="sxs-lookup"><span data-stu-id="1006f-191">Click **Add** to create the controller class and add the default views.</span></span>
   
    ![Configurar o controlador][cache-configure-controller]
5. <span data-ttu-id="1006f-193">No **Gerenciador de Soluções**, expanda **Global.asax** e clique duas vezes em **Global.asax.cs** para abri-lo.</span><span class="sxs-lookup"><span data-stu-id="1006f-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** to open it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="1006f-195">Adicione as duas seguintes instruções `using` na parte superior do arquivo abaixo das outras instruções `using`.</span><span class="sxs-lookup"><span data-stu-id="1006f-195">Add the following two `using` statements at the top of the file under the other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="1006f-196">Adicione a linha de código a seguir ao fim do método `Application_Start` .</span><span class="sxs-lookup"><span data-stu-id="1006f-196">Add the following line of code at the end of the `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="1006f-197">No **Gerenciador de Soluções**, expanda `App_Start` e clique duas vezes em `RouteConfig.cs`.</span><span class="sxs-lookup"><span data-stu-id="1006f-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="1006f-199">Substitua `controller = "Home"` no código a seguir no método `RegisterRoutes` por `controller = "Teams"`, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="1006f-199">Replace `controller = "Home"` in the following code in the `RegisterRoutes` method with `controller = "Teams"` as shown in the following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-the-views"></a><span data-ttu-id="1006f-200">Configurar os modos de exibição</span><span class="sxs-lookup"><span data-stu-id="1006f-200">Configure the views</span></span>
1. <span data-ttu-id="1006f-201">No **Gerenciador de Soluções**, expanda a pasta **Exibições** e a pasta **Compartilhado** e clique duas vezes em **_Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="1006f-201">In **Solution Explorer**, expand the **Views** folder and then the **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml.][cache-layout-cshtml]
2. <span data-ttu-id="1006f-203">Altere o conteúdo do elemento `title` e substitua `My ASP.NET Application` por `Contoso Team Stats`, conforme é mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="1006f-203">Change the contents of the `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in the following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="1006f-204">Na seção `body`, atualize a primeira instrução `Html.ActionLink`, substitua `Application name` por `Contoso Team Stats` e substitua `Home` por `Teams`.</span><span class="sxs-lookup"><span data-stu-id="1006f-204">In the `body` section, update the first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="1006f-205">Antes: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="1006f-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="1006f-206">Após: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="1006f-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![Alterações de código][cache-layout-cshtml-code]
2. <span data-ttu-id="1006f-208">Pressione **Ctrl+F5** para compilar e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1006f-208">Press **Ctrl+F5** to build and run the application.</span></span> <span data-ttu-id="1006f-209">Essa versão do aplicativo lê os resultados diretamente do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1006f-209">This version of the application reads the results directly from the database.</span></span> <span data-ttu-id="1006f-210">Observe as ações **Criar Novo**, **Editar**, **Detalhes** e **Excluir** que foram adicionadas automaticamente ao aplicativo pelo scaffold Controlador **MVC 5 com modos de exibição, usando o Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="1006f-210">Note the **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added to the application by the **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="1006f-211">Na próxima seção do tutorial, você adicionará o Cache Redis para otimizar o acesso a dados e fornecer recursos adicionais ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1006f-211">In the next section of the tutorial you'll add Redis Cache to optimize the data access and provide additional features to the application.</span></span>

![Aplicativo de início][cache-starter-application]

## <a name="configure-the-application-to-use-redis-cache"></a><span data-ttu-id="1006f-213">Configurar o aplicativo para usar o Cache Redis</span><span class="sxs-lookup"><span data-stu-id="1006f-213">Configure the application to use Redis Cache</span></span>
<span data-ttu-id="1006f-214">Nesta seção do tutorial, você configurará o aplicativo de exemplo para armazenar e recuperar estatísticas de equipe da Contoso de uma instância do Cache Redis do Azure usando o cliente de cache [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .</span><span class="sxs-lookup"><span data-stu-id="1006f-214">In this section of the tutorial, you'll configure the sample application to store and retrieve Contoso team statistics from an Azure Redis Cache instance by using the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="1006f-215">Configurar o aplicativo para usar StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="1006f-215">Configure the application to use StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="1006f-216">Atualizar a classe TeamsController para retornar resultados do cache ou do banco de dados</span><span class="sxs-lookup"><span data-stu-id="1006f-216">Update the TeamsController class to return results from the cache or the database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="1006f-217">Atualizar os métodos Create, Edit e Delete para trabalhar com o cache</span><span class="sxs-lookup"><span data-stu-id="1006f-217">Update the Create, Edit, and Delete methods to work with the cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="1006f-218">Atualizar o modo de exibição de Índice de Equipes para trabalhar com o cache</span><span class="sxs-lookup"><span data-stu-id="1006f-218">Update the Teams Index view to work with the cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-the-application-to-use-stackexchangeredis"></a><span data-ttu-id="1006f-219">Configurar o aplicativo para usar StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="1006f-219">Configure the application to use StackExchange.Redis</span></span>
1. <span data-ttu-id="1006f-220">Para configurar um aplicativo cliente no Visual Studio usando o pacote NuGet do StackExchange.Redis, clique em **Gerenciador de Pacotes NuGet**, **Console do Gerenciador de Pacotes** no menu **Ferramentas**.</span><span class="sxs-lookup"><span data-stu-id="1006f-220">To configure a client application in Visual Studio using the StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="1006f-221">Execute o comando a seguir na janela `Package Manager Console`.</span><span class="sxs-lookup"><span data-stu-id="1006f-221">Run the following command from the `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="1006f-222">Os downloads de pacote NuGet acrescentam as referências de assembly necessárias para o seu aplicativo de cliente para acessar o cache Redis do Azure com o cliente de cache StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="1006f-222">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span></span> <span data-ttu-id="1006f-223">Se você preferir usar uma versão de nome forte da biblioteca de cliente `StackExchange.Redis`, instale o pacote `StackExchange.Redis.StrongName`.</span><span class="sxs-lookup"><span data-stu-id="1006f-223">If you prefer to use a strong-named version of the `StackExchange.Redis` client library, install the `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="1006f-224">No **Gerenciador de Soluções**, expanda a pasta **Controladores** e clique duas vezes em **TeamsController.cs** para abri-lo.</span><span class="sxs-lookup"><span data-stu-id="1006f-224">In **Solution Explorer**, expand the **Controllers** folder and double-click **TeamsController.cs** to open it.</span></span>
   
    ![Controlador de equipes][cache-teamscontroller]
4. <span data-ttu-id="1006f-226">Adicione as duas instruções `using` a seguir a **TeamsController.cs**.</span><span class="sxs-lookup"><span data-stu-id="1006f-226">Add the following two `using` statements to **TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="1006f-227">Adicione as duas propriedades a seguir à classe `TeamsController` .</span><span class="sxs-lookup"><span data-stu-id="1006f-227">Add the following two properties to the `TeamsController` class.</span></span>

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

6. <span data-ttu-id="1006f-228">Crie no computador um arquivo chamado `WebAppPlusCacheAppSecrets.config` e coloque-o em um local do qual não será feito check-in com o código-fonte do aplicativo de exemplo, se você decidir fazer check-in dele em algum lugar.</span><span class="sxs-lookup"><span data-stu-id="1006f-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with the source code of your sample application, should you decide to check it in somewhere.</span></span> <span data-ttu-id="1006f-229">Neste exemplo, o arquivo `AppSettingsSecrets.config` está localizado em `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span><span class="sxs-lookup"><span data-stu-id="1006f-229">In this example the `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="1006f-230">Edite o arquivo `WebAppPlusCacheAppSecrets.config` e adicione o conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="1006f-230">Edit the `WebAppPlusCacheAppSecrets.config` file and add the following contents.</span></span> <span data-ttu-id="1006f-231">Se você executar o aplicativo localmente, essas informações serão usadas para se conectar à instância do Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="1006f-231">If you run the application locally this information is used to connect to your Azure Redis Cache instance.</span></span> <span data-ttu-id="1006f-232">Mais adiante no tutorial, você provisionará uma instância do Cache Redis do Azure e atualizará o nome e a senha do cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-232">Later in the tutorial you'll provision an Azure Redis Cache instance and update the cache name and password.</span></span> <span data-ttu-id="1006f-233">Se você não planeja executar o aplicativo de exemplo localmente, pode ignorar a criação desse arquivo e as etapas subsequentes que fazem referência a ele, pois quando você implanta no Azure, o aplicativo recupera as informações de conexão de cache da configuração do aplicativo Web, não desse arquivo.</span><span class="sxs-lookup"><span data-stu-id="1006f-233">If you don't plan to run the sample application locally you can skip the creation of this file and the subsequent steps that reference the file, because when you deploy to Azure the application retrieves the cache connection information from the app setting for the Web App and not from this file.</span></span> <span data-ttu-id="1006f-234">Como o `WebAppPlusCacheAppSecrets.config` não é implantado no Azure com seu aplicativo, você não precisa dele, a menos que pretenda executar o aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="1006f-234">Since the `WebAppPlusCacheAppSecrets.config` is not deployed to Azure with your application, you don't need it unless you are going to run the application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="1006f-235">No **Gerenciador de Soluções**, clique duas vezes em **web.config** para abri-lo.</span><span class="sxs-lookup"><span data-stu-id="1006f-235">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="1006f-237">Adicione o atributo `file` a seguir ao elemento `appSettings`.</span><span class="sxs-lookup"><span data-stu-id="1006f-237">Add the following `file` attribute to the `appSettings` element.</span></span> <span data-ttu-id="1006f-238">Se você usou um nome de arquivo ou local diferente, substitua esses valores pelos mostrados no exemplo.</span><span class="sxs-lookup"><span data-stu-id="1006f-238">If you used a different file name or location, substitute those values for the ones shown in the example.</span></span>
   
   * <span data-ttu-id="1006f-239">Antes: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="1006f-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="1006f-240">Após: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="1006f-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="1006f-241">O tempo de execução do ASP.NET mescla o conteúdo do arquivo externo com a marcação no elemento `<appSettings>` .</span><span class="sxs-lookup"><span data-stu-id="1006f-241">The ASP.NET runtime merges the contents of the external file with the markup in the `<appSettings>` element.</span></span> <span data-ttu-id="1006f-242">O tempo de execução ignorará o atributo de arquivo se o arquivo especificado não puder ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="1006f-242">The runtime ignores the file attribute if the specified file cannot be found.</span></span> <span data-ttu-id="1006f-243">Seus segredos (a cadeia de conexão do cache) não são incluídos como parte do código-fonte do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1006f-243">Your secrets (the connection string to your cache) are not included as part of the source code for the application.</span></span> <span data-ttu-id="1006f-244">Quando você implantar o aplicativo Web no Azure, o arquivo `WebAppPlusCacheAppSecrests.config` não será implantado (isso é o que você deseja).</span><span class="sxs-lookup"><span data-stu-id="1006f-244">When you deploy your web app to Azure, the `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="1006f-245">Há várias maneiras de especificar os segredos no Azure e, neste tutorial, elas serão configuradas automaticamente quando você [provisionar os recursos do Azure](#provision-the-azure-resources) em uma etapa posterior do tutorial.</span><span class="sxs-lookup"><span data-stu-id="1006f-245">There are several ways to specify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision the Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="1006f-246">Para saber mais sobre como trabalhar com segredos no Azure, confira [Práticas recomendadas para implantar senhas e outros dados confidenciais no ASP.NET e no Serviço de Aplicativo do Azure](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span><span class="sxs-lookup"><span data-stu-id="1006f-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database"></a><span data-ttu-id="1006f-247">Atualizar a classe TeamsController para retornar resultados do cache ou do banco de dados</span><span class="sxs-lookup"><span data-stu-id="1006f-247">Update the TeamsController class to return results from the cache or the database</span></span>
<span data-ttu-id="1006f-248">Neste exemplo, as estatísticas de equipe podem ser recuperadas do banco de dados ou do cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-248">In this sample, team statistics can be retrieved from the database or from the cache.</span></span> <span data-ttu-id="1006f-249">As estatísticas de equipe são armazenadas no cache como um `List<Team>`serializado e também como um conjunto ordenado usando tipos de dados Redis.</span><span class="sxs-lookup"><span data-stu-id="1006f-249">Team statistics are stored in the cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="1006f-250">Ao recuperar itens de um conjunto ordenado, você pode recuperar alguns ou todos os itens ou consultar determinados itens.</span><span class="sxs-lookup"><span data-stu-id="1006f-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="1006f-251">Neste exemplo, você consultará o conjunto ordenado para as cinco equipes principais classificadas pelo número de vitórias.</span><span class="sxs-lookup"><span data-stu-id="1006f-251">In this sample you'll query the sorted set for the top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="1006f-252">Não é necessário armazenar as estatísticas de equipe em vários formatos no cache para usar o Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="1006f-252">It is not required to store the team statistics in multiple formats in the cache in order to use Azure Redis Cache.</span></span> <span data-ttu-id="1006f-253">Este tutorial usa vários formatos para demonstrar algumas das diferentes maneiras e tipos de dados que você pode usar para armazenar dados em cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-253">This tutorial uses multiple formats to demonstrate some of the different ways and different data types you can use to cache data.</span></span>
> 
> 

1. <span data-ttu-id="1006f-254">Adicione as instruções `using` a seguir ao arquivo `TeamsController.cs` na parte superior, com as outras instruções `using`.</span><span class="sxs-lookup"><span data-stu-id="1006f-254">Add the following `using` statements to the `TeamsController.cs` file at the top with the other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="1006f-255">Substitua a implementação do método `public ActionResult Index()` atual pela implementação a seguir.</span><span class="sxs-lookup"><span data-stu-id="1006f-255">Replace the current `public ActionResult Index()` method implementation with the following implementation.</span></span>

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

            case "clearCache": // Clear the results from the cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild the database with sample data.
                RebuildDB();
                break;
        }

        // Measure the time it takes to retrieve the results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve the top 5 teams from the sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from the cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from the database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add the elapsed time of the operation to the ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. <span data-ttu-id="1006f-256">Adicione os três métodos a seguir à classe `TeamsController` para implementar os tipos de ação `playGames`, `clearCache` e `rebuildDB` da instrução switch adicionada no trecho de código anterior.</span><span class="sxs-lookup"><span data-stu-id="1006f-256">Add the following three methods to the `TeamsController` class to implement the `playGames`, `clearCache`, and `rebuildDB` action types from the switch statement added in the previous code snippet.</span></span>
   
    <span data-ttu-id="1006f-257">O método `PlayGames` atualiza as estatísticas de equipe simulando uma temporada de jogos, salva os resultados no banco de dados e limpa os dados agora obsoletos do cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-257">The `PlayGames` method updates the team statistics by simulating a season of games, saves the results to the database, and clears the now outdated data from the cache.</span></span>

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

    <span data-ttu-id="1006f-258">O método `RebuildDB` reinicializa o banco de dados com o conjunto padrão de equipes, gera estatísticas para elas e limpa os dados agora obsoletos do cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-258">The `RebuildDB` method reinitializes the database with the default set of teams, generates statistics for them, and clears the now outdated data from the cache.</span></span>

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize the database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="1006f-259">O método `ClearCachedTeams` remove do cache todas as estatísticas de equipe armazenadas em cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-259">The `ClearCachedTeams` method removes any cached team statistics from the cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="1006f-260">Adicione os quatro métodos a seguir à classe `TeamsController` para implementar as várias maneiras de recuperar as estatísticas de equipe do cache e do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1006f-260">Add the following four methods to the `TeamsController` class to implement the various ways of retrieving the team statistics from the cache and the database.</span></span> <span data-ttu-id="1006f-261">Cada um desses métodos retorna um `List<Team>` , que é exibido pelo modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="1006f-261">Each of these methods returns a `List<Team>` which is then displayed by the view.</span></span>
   
    <span data-ttu-id="1006f-262">O método `GetFromDB` lê as estatísticas de equipe do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1006f-262">The `GetFromDB` method reads the team statistics from the database.</span></span>
   
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

    <span data-ttu-id="1006f-263">O método `GetFromList` lê as estatísticas de equipe do cache como um `List<Team>` serializado.</span><span class="sxs-lookup"><span data-stu-id="1006f-263">The `GetFromList` method reads the team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="1006f-264">Se houver um erro de cache, as estatísticas de equipe serão lidas do banco de dados e, em seguida, armazenadas em cache para a próxima vez.</span><span class="sxs-lookup"><span data-stu-id="1006f-264">If there is a cache miss, the team statistics are read from the database and then stored in the cache for next time.</span></span> <span data-ttu-id="1006f-265">Neste exemplo, usamos a serialização de JSON.NET para serializar os objetos .NET para e do cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-265">In this sample we're using JSON.NET serialization to serialize the .NET objects to and from the cache.</span></span> <span data-ttu-id="1006f-266">Para saber mais, confira [Como trabalhar com objetos .NET no Cache Redis do Azure](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span><span class="sxs-lookup"><span data-stu-id="1006f-266">For more information, see [How to work with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

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

            ViewBag.msg += "Storing results to cache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    <span data-ttu-id="1006f-267">O método `GetFromSortedSet` lê as estatísticas de equipe de um conjunto ordenado armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-267">The `GetFromSortedSet` method reads the team statistics from a cached sorted set.</span></span> <span data-ttu-id="1006f-268">Se houver um erro de cache, as estatísticas de equipe serão lidas do banco de dados e armazenadas no cache como um conjunto ordenado.</span><span class="sxs-lookup"><span data-stu-id="1006f-268">If there is a cache miss, the team statistics are read from the database and stored in the cache as a sorted set.</span></span>

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
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

            ViewBag.msg += "Storing results to cache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding to sorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    <span data-ttu-id="1006f-269">O método `GetFromSortedSetTop5` lê as cinco equipes principais do conjunto ordenado armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-269">The `GetFromSortedSetTop5` method reads the top 5 teams from the cached sorted set.</span></span> <span data-ttu-id="1006f-270">Ele começa verificando a existência da chave `teamsSortedSet` no cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-270">It starts by checking the cache for the existence of the `teamsSortedSet` key.</span></span> <span data-ttu-id="1006f-271">Se a chave não estiver presente, o método `GetFromSortedSet` será chamado para ler as estatísticas de equipe e armazená-las no cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-271">If this key is not present, the `GetFromSortedSet` method is called to read the team statistics and store them in the cache.</span></span> <span data-ttu-id="1006f-272">Em seguida, o conjunto ordenado armazenado em cache é consultado para fornecer as cinco equipes principais, que são retornadas.</span><span class="sxs-lookup"><span data-stu-id="1006f-272">Next, the cached sorted set is queried for the top 5 teams which are returned.</span></span>

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load the entire sorted set into the cache.
            GetFromSortedSet();

            // Retrieve the top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get the top 5 teams from the sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-the-create-edit-and-delete-methods-to-work-with-the-cache"></a><span data-ttu-id="1006f-273">Atualizar os métodos Create, Edit e Delete para trabalhar com o cache</span><span class="sxs-lookup"><span data-stu-id="1006f-273">Update the Create, Edit, and Delete methods to work with the cache</span></span>
<span data-ttu-id="1006f-274">O código de scaffolding gerado como parte do exemplo inclui métodos para adicionar, editar e excluir equipes.</span><span class="sxs-lookup"><span data-stu-id="1006f-274">The scaffolding code that was generated as part of this sample includes methods to add, edit, and delete teams.</span></span> <span data-ttu-id="1006f-275">Sempre que uma equipe é adicionada, editada ou removida, os dados no cache tornam-se desatualizados.</span><span class="sxs-lookup"><span data-stu-id="1006f-275">Anytime a team is added, edited, or removed, the data in the cache becomes outdated.</span></span> <span data-ttu-id="1006f-276">Nesta seção, você modificará esses três métodos para limpar as equipes armazenadas em cache, para que o cache não fique fora de sincronia com o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1006f-276">In this section you'll modify these three methods to clear the cached teams so that the cache won't be out of sync with the database.</span></span>

1. <span data-ttu-id="1006f-277">Navegue até o método `Create(Team team)` na classe `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="1006f-277">Browse to the `Create(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="1006f-278">Adicione uma chamada ao método `ClearCachedTeams` , conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="1006f-278">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Create
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. <span data-ttu-id="1006f-279">Navegue até o método `Edit(Team team)` na classe `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="1006f-279">Browse to the `Edit(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="1006f-280">Adicione uma chamada ao método `ClearCachedTeams` , conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="1006f-280">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Edit/5
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. <span data-ttu-id="1006f-281">Navegue até o método `DeleteConfirmed(int id)` na classe `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="1006f-281">Browse to the `DeleteConfirmed(int id)` method in the `TeamsController` class.</span></span> <span data-ttu-id="1006f-282">Adicione uma chamada ao método `ClearCachedTeams` , conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="1006f-282">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, the cache is out of date.
        // Clear the cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-the-teams-index-view-to-work-with-the-cache"></a><span data-ttu-id="1006f-283">Atualizar o modo de exibição de Índice de Equipes para trabalhar com o cache</span><span class="sxs-lookup"><span data-stu-id="1006f-283">Update the Teams Index view to work with the cache</span></span>
1. <span data-ttu-id="1006f-284">No **Gerenciador de Soluções**, expanda a pasta **Exibições** e a pasta **Equipes** e clique duas vezes em **Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="1006f-284">In **Solution Explorer**, expand the **Views** folder, then the **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="1006f-286">Na parte superior do arquivo, procure o elemento de parágrafo a seguir.</span><span class="sxs-lookup"><span data-stu-id="1006f-286">Near the top of the file, look for the following paragraph element.</span></span>
   
    ![Tabela de ação][cache-teams-index-table]
   
    <span data-ttu-id="1006f-288">Esse é o link para criar uma nova equipe.</span><span class="sxs-lookup"><span data-stu-id="1006f-288">This is the link to create a new team.</span></span> <span data-ttu-id="1006f-289">Substitua o elemento de parágrafo pela tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="1006f-289">Replace the paragraph element with the following table.</span></span> <span data-ttu-id="1006f-290">A tabela contém links de ação para criar uma nova equipe, reproduzir uma nova temporada de jogos, limpar o cache, recuperar as equipes do cache em vários formatos, recuperar as equipes do banco de dados e recriar o banco de dados com dados de exemplo atualizados.</span><span class="sxs-lookup"><span data-stu-id="1006f-290">This table has action links for creating a new team, playing a new season of games, clearing the cache, retrieving the teams from the cache in several formats, retrieving the teams from the database, and rebuilding the database with fresh sample data.</span></span>

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


1. <span data-ttu-id="1006f-291">Role até a parte inferior do arquivo **index.cshtml** e adicione o elemento `tr` a seguir para que ele seja a última linha na última tabela do arquivo.</span><span class="sxs-lookup"><span data-stu-id="1006f-291">Scroll to the bottom of the **Index.cshtml** file and add the following `tr` element so that it is the last row in the last table in the file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="1006f-292">Essa linha exibe o valor de `ViewBag.Msg` que contém um relatório de status sobre a operação atual.</span><span class="sxs-lookup"><span data-stu-id="1006f-292">This row displays the value of `ViewBag.Msg` which contains a status report about the current operation.</span></span> <span data-ttu-id="1006f-293">O `ViewBag.Msg` é definido quando você clica em qualquer um dos links de ação da etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="1006f-293">The `ViewBag.Msg` is set when you click any of the action links from the previous step.</span></span>   
   
    ![Mensagem de status][cache-status-message]
2. <span data-ttu-id="1006f-295">Pressione **F6** para compilar o projeto.</span><span class="sxs-lookup"><span data-stu-id="1006f-295">Press **F6** to build the project.</span></span>

## <a name="provision-the-azure-resources"></a><span data-ttu-id="1006f-296">provisionar os recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="1006f-296">Provision the Azure resources</span></span>
<span data-ttu-id="1006f-297">Para hospedar seu aplicativo no Azure, primeiro você deve provisionar os serviços do Azure que o aplicativo requer.</span><span class="sxs-lookup"><span data-stu-id="1006f-297">To host your application in Azure, you must first provision the Azure services that your application requires.</span></span> <span data-ttu-id="1006f-298">O aplicativo de exemplo deste tutorial usa os serviços do Azure a seguir.</span><span class="sxs-lookup"><span data-stu-id="1006f-298">The sample application in this tutorial uses the following Azure services.</span></span>

* <span data-ttu-id="1006f-299">Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="1006f-299">Azure Redis Cache</span></span>
* <span data-ttu-id="1006f-300">Aplicativo Web do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="1006f-300">App Service Web App</span></span>
* <span data-ttu-id="1006f-301">Banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="1006f-301">SQL Database</span></span>

<span data-ttu-id="1006f-302">Para implantar esses serviços em um grupo de recursos novo ou existente de sua escolha, clique no botão **Implantar no Azure** a seguir.</span><span class="sxs-lookup"><span data-stu-id="1006f-302">To deploy these services to a new or existing resource group of your choice, click the following **Deploy to Azure** button.</span></span>

<span data-ttu-id="1006f-303">[![Implantar no Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="1006f-303">[![Deploy to Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="1006f-304">O botão **Implantar no Azure** usa o modelo [Criar um aplicativo Web e o Cache Redis e o Banco de Dados SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Início Rápido do Azure](https://github.com/Azure/azure-quickstart-templates) para provisionar esses serviços e definir a cadeia de conexão para o Banco de Dados SQL e o aplicativo de configuração para a cadeia de conexão do Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="1006f-304">This **Deploy to Azure** button uses the [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template to provision these services and set the connection string for the SQL Database and the application setting for the Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="1006f-305">Se não tiver uma conta do Azure, você poderá [criar uma conta gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="1006f-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="1006f-306">Se clicar no botão **Implantar no Azure** , você será levado para o portal do Azure, e será iniciado o processo de criação dos recursos descritos pelo modelo.</span><span class="sxs-lookup"><span data-stu-id="1006f-306">Clicking the **Deploy to Azure** button takes you to the Azure portal and initiates the process of creating the resources described by the template.</span></span>

![Implantar no Azure][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="1006f-308">Na folha **Fundamentos** , selecione a assinatura do Azure a ser usada, selecione um grupo de recursos existente ou crie um novo e especifique o local do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1006f-308">In the **Basics** section, select the Azure subscription to use, and select an existing resource group or create a new one, and specify the resource group location.</span></span>
2. <span data-ttu-id="1006f-309">Na seção **Configurações**, especifique um **Logon de Administrador** (não use **administrador**), **Senha de Logon do Administrador** e o **Nome do Banco de Dados**.</span><span class="sxs-lookup"><span data-stu-id="1006f-309">In the **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="1006f-310">Os outros parâmetros são configurados para um plano de hospedagem do Serviço de Aplicativo gratuito e opções de custo mais baixo para o Banco de Dados SQL e o Cache Redis do Azure, que não vêm com uma camada gratuita.</span><span class="sxs-lookup"><span data-stu-id="1006f-310">The other parameters are configured for a free App Service hosting plan, and lower-cost options for the SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![Implantar no Azure][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="1006f-312">Após definir as configurações desejadas, role até o fim da página, leia os termos e condições e marque a caixa de seleção **Concordo com os termos e condições indicados acima**.</span><span class="sxs-lookup"><span data-stu-id="1006f-312">After configuring the desired settings, scroll to the end of the page, read the terms and conditions, and check the **I agree to the terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="1006f-313">Para iniciar o provisionamento de recursos, clique em **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="1006f-313">To begin provisioning the resources, click **Purchase**.</span></span>

<span data-ttu-id="1006f-314">Para exibir o andamento da implantação, clique no ícone de notificação e clique em **Implantação iniciada**.</span><span class="sxs-lookup"><span data-stu-id="1006f-314">To view the progress of your deployment, click the notification icon and click **Deployment started**.</span></span>

![Implantação iniciada][cache-deployment-started]

<span data-ttu-id="1006f-316">Você pode exibir o status da implantação na folha **Microsoft.Template** .</span><span class="sxs-lookup"><span data-stu-id="1006f-316">You can view the status of your deployment on the **Microsoft.Template** blade.</span></span>

![Implantar no Azure][cache-deploy-to-azure-step-3]

<span data-ttu-id="1006f-318">Quando o provisionamento for concluído, você poderá publicar o aplicativo no Azure por meio do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1006f-318">When provisioning is complete, you can publish your application to Azure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="1006f-319">Os erros que ocorrerem durante o processo de provisionamento serão exibidos na folha **Microsoft.Template** .</span><span class="sxs-lookup"><span data-stu-id="1006f-319">Any errors that may occur during the provisioning process are displayed on the **Microsoft.Template** blade.</span></span> <span data-ttu-id="1006f-320">Alguns erros comuns são muitos Servidores SQL ou muitos planos de hospedagem do Serviço de Aplicativo gratuitos por assinatura.</span><span class="sxs-lookup"><span data-stu-id="1006f-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="1006f-321">Resolva os erros e reinicie o processo clicando em **Reimplantar** na folha **Microsoft.Template** ou no botão **Implantar no Azure** neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="1006f-321">Resolve any errors and restart the process by clicking **Redeploy** on the **Microsoft.Template** blade or the **Deploy to Azure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-the-application-to-azure"></a><span data-ttu-id="1006f-322">Publicar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="1006f-322">Publish the application to Azure</span></span>
<span data-ttu-id="1006f-323">Nesta etapa do tutorial, você publicará o aplicativo no Azure e o executará na nuvem.</span><span class="sxs-lookup"><span data-stu-id="1006f-323">In this step of the tutorial, you'll publish the application to Azure and run it in the cloud.</span></span>

1. <span data-ttu-id="1006f-324">Clique com o botão direito do mouse no projeto **ContosoTeamStats** no Visual Studio e escolha **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="1006f-324">Right-click the **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![Publicar][cache-publish-app]
2. <span data-ttu-id="1006f-326">Clique em **Serviço de Aplicativo do Microsoft Azure**, escolha **Selecionar Existente** e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="1006f-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![Publicar][cache-publish-to-app-service]
3. <span data-ttu-id="1006f-328">Selecione a assinatura usada ao criar os recursos do Azure, expanda o grupo de recursos que contém os recursos, selecione o aplicativo Web desejado.</span><span class="sxs-lookup"><span data-stu-id="1006f-328">Select the subscription used when creating the Azure resources, expand the resource group containing the resources, and select the desired Web App.</span></span> <span data-ttu-id="1006f-329">Se você tiver usado o botão **Implantar no Azure**, o nome do aplicativo Web começará com **webSite**, seguido de alguns caracteres adicionais.</span><span class="sxs-lookup"><span data-stu-id="1006f-329">If you used the **Deploy to Azure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![Selecionar aplicativo Web][cache-select-web-app]
4. <span data-ttu-id="1006f-331">Clique em **OK** para iniciar o processo de publicação.</span><span class="sxs-lookup"><span data-stu-id="1006f-331">Click **OK** to begin the publishing process.</span></span> <span data-ttu-id="1006f-332">Após alguns instantes, o processo de publicação é concluído e um navegador será iniciado com o aplicativo de exemplo em execução.</span><span class="sxs-lookup"><span data-stu-id="1006f-332">After a few moments the publishing process completes and a browser is launched with the running sample application.</span></span> <span data-ttu-id="1006f-333">Se você receber um erro DNS ao validar ou publicar, e o processo de provisionamento de recursos do Azure para o aplicativo tiver sido concluído recentemente, aguarde um momento e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="1006f-333">If you get a DNS error when validating or publishing, and the provisioning process for the Azure resources for the application has just recently completed, wait a moment and try again.</span></span>
   
    ![Cache adicionado][cache-added-to-application]

<span data-ttu-id="1006f-335">A tabela a seguir descreve cada link de ação do aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="1006f-335">The following table describes each action link from the sample application.</span></span>

| <span data-ttu-id="1006f-336">Ação</span><span class="sxs-lookup"><span data-stu-id="1006f-336">Action</span></span> | <span data-ttu-id="1006f-337">Descrição</span><span class="sxs-lookup"><span data-stu-id="1006f-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1006f-338">Criar Novo</span><span class="sxs-lookup"><span data-stu-id="1006f-338">Create New</span></span> |<span data-ttu-id="1006f-339">Criar uma nova Equipe.</span><span class="sxs-lookup"><span data-stu-id="1006f-339">Create a new Team.</span></span> |
| <span data-ttu-id="1006f-340">Reproduzir Temporada</span><span class="sxs-lookup"><span data-stu-id="1006f-340">Play Season</span></span> |<span data-ttu-id="1006f-341">Reproduzir uma temporada de jogos, atualizar as estatísticas de equipes e limpar dados de equipe desatualizados do cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-341">Play a season of games, update the team stats, and clear any outdated team data from the cache.</span></span> |
| <span data-ttu-id="1006f-342">Limpar Cache</span><span class="sxs-lookup"><span data-stu-id="1006f-342">Clear Cache</span></span> |<span data-ttu-id="1006f-343">Limpar as estatísticas de equipes do cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-343">Clear the team stats from the cache.</span></span> |
| <span data-ttu-id="1006f-344">Listar do Cache</span><span class="sxs-lookup"><span data-stu-id="1006f-344">List from Cache</span></span> |<span data-ttu-id="1006f-345">Recuperar as estatísticas de equipe do cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-345">Retrieve the team stats from the cache.</span></span> <span data-ttu-id="1006f-346">Se houver um erro de cache, carregar as estatísticas do banco de dados e salvar no cache para a próxima vez.</span><span class="sxs-lookup"><span data-stu-id="1006f-346">If there is a cache miss, load the stats from the database and save to the cache for next time.</span></span> |
| <span data-ttu-id="1006f-347">Conjunto Ordenado do Cache</span><span class="sxs-lookup"><span data-stu-id="1006f-347">Sorted Set from Cache</span></span> |<span data-ttu-id="1006f-348">Recuperar as estatísticas de equipes do cache usando um conjunto ordenado.</span><span class="sxs-lookup"><span data-stu-id="1006f-348">Retrieve the team stats from the cache using a sorted set.</span></span> <span data-ttu-id="1006f-349">Se houver um erro de cache, carregar as estatísticas do banco de dados e salvar no cache usando um conjunto ordenado.</span><span class="sxs-lookup"><span data-stu-id="1006f-349">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="1006f-350">Cinco Principais Equipes do Cache</span><span class="sxs-lookup"><span data-stu-id="1006f-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="1006f-351">Recuperar as cinco principais equipes do cache usando um conjunto ordenado.</span><span class="sxs-lookup"><span data-stu-id="1006f-351">Retrieve the top 5 teams from the cache using a sorted set.</span></span> <span data-ttu-id="1006f-352">Se houver um erro de cache, carregar as estatísticas do banco de dados e salvar no cache usando um conjunto ordenado.</span><span class="sxs-lookup"><span data-stu-id="1006f-352">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="1006f-353">Carregar do banco de dados</span><span class="sxs-lookup"><span data-stu-id="1006f-353">Load from DB</span></span> |<span data-ttu-id="1006f-354">Recuperar as estatísticas de equipes do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1006f-354">Retrieve the team stats from the database.</span></span> |
| <span data-ttu-id="1006f-355">Recriar o banco de dados</span><span class="sxs-lookup"><span data-stu-id="1006f-355">Rebuild DB</span></span> |<span data-ttu-id="1006f-356">Recriar o banco de dados e recarregá-lo com dados de equipes de exemplo.</span><span class="sxs-lookup"><span data-stu-id="1006f-356">Rebuild the database and reload it with sample team data.</span></span> |
| <span data-ttu-id="1006f-357">Editar/Detalhes/Excluir</span><span class="sxs-lookup"><span data-stu-id="1006f-357">Edit / Details / Delete</span></span> |<span data-ttu-id="1006f-358">Editar uma equipe, exibir detalhes de uma equipe, excluir uma equipe.</span><span class="sxs-lookup"><span data-stu-id="1006f-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="1006f-359">Clique em algumas das ações e experimente recuperar os dados de diferentes fontes.</span><span class="sxs-lookup"><span data-stu-id="1006f-359">Click some of the actions and experiment with retrieving the data from the different sources.</span></span> <span data-ttu-id="1006f-360">Observe as diferenças no tempo necessário para concluir as várias maneiras de recuperar dados do banco de dados e do cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-360">Not the differences in the time it takes to complete the various ways of retrieving the data from the database and the cache.</span></span>

## <a name="delete-the-resources-when-you-are-finished-with-the-application"></a><span data-ttu-id="1006f-361">Exclua os recursos quando tiver terminado de usar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="1006f-361">Delete the resources when you are finished with the application</span></span>
<span data-ttu-id="1006f-362">Ao terminar de usar o aplicativo do tutorial de exemplo, você poderá excluir os recursos do Azure usados para economizar custos e recursos.</span><span class="sxs-lookup"><span data-stu-id="1006f-362">When you are finished with the sample tutorial application, you can delete the Azure resources used in order to conserve cost and resources.</span></span> <span data-ttu-id="1006f-363">Se usar o botão **Implantar no Azure** na seção [Provisionar os recursos do Azure](#provision-the-azure-resources) e todos os recursos estiverem contidos no mesmo grupo de recursos, você poderá excluí-los juntos em uma única operação excluindo o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1006f-363">If you use the **Deploy to Azure** button in the [Provision the Azure resources](#provision-the-azure-resources) section and all of your resources are contained in the same resource group, you can delete them together in one operation by deleting the resource group.</span></span>

1. <span data-ttu-id="1006f-364">Entre no [portal do Azure](https://portal.azure.com) e clique em **Grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="1006f-364">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="1006f-365">Digite o nome do grupo de recursos na caixa de texto **Filtrar itens...** .</span><span class="sxs-lookup"><span data-stu-id="1006f-365">Type the name of your resource group into the **Filter items...** textbox.</span></span>
3. <span data-ttu-id="1006f-366">Clique em **...** à direita do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1006f-366">Click **...** to the right of your resource group.</span></span>
4. <span data-ttu-id="1006f-367">Clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="1006f-367">Click **Delete**.</span></span>
   
    ![Excluir][cache-delete-resource-group]
5. <span data-ttu-id="1006f-369">Digite o nome do grupo de recursos e clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="1006f-369">Type the name of your resource group and click **Delete**.</span></span>
   
    ![Confirmar exclusão][cache-delete-confirm]

<span data-ttu-id="1006f-371">Após alguns instantes, o grupo de recursos e todos os seus recursos contidos serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="1006f-371">After a few moments the resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1006f-372">Observe que a exclusão de um grupo de recursos é irreversível e que o grupo de recursos e todos os recursos contidos nele são excluídos permanentemente.</span><span class="sxs-lookup"><span data-stu-id="1006f-372">Note that deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span></span> <span data-ttu-id="1006f-373">Não exclua acidentalmente o grupo de recursos ou os recursos incorretos.</span><span class="sxs-lookup"><span data-stu-id="1006f-373">Make sure that you do not accidentally delete the wrong resource group or resources.</span></span> <span data-ttu-id="1006f-374">Se tiver criado os recursos para hospedar este exemplo dentro de um grupo de recursos existente, você poderá excluir cada recurso individualmente de suas respectivas folhas.</span><span class="sxs-lookup"><span data-stu-id="1006f-374">If you created the resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-the-sample-application-on-your-local-machine"></a><span data-ttu-id="1006f-375">Executar o aplicativo de exemplo no computador local</span><span class="sxs-lookup"><span data-stu-id="1006f-375">Run the sample application on your local machine</span></span>
<span data-ttu-id="1006f-376">Para executar o aplicativo localmente em seu computador, você precisa de uma instância do Cache Redis do Azure na qual armazenar os dados em cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-376">To run the application locally on your machine, you need an Azure Redis Cache instance in which to cache your data.</span></span> 

* <span data-ttu-id="1006f-377">Se tiver publicado o aplicativo no Azure conforme descrito na seção anterior, você poderá usar a instância do Cache Redis do Azure fornecida naquela etapa.</span><span class="sxs-lookup"><span data-stu-id="1006f-377">If you have published your application to Azure as described in the previous section, you can use the Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="1006f-378">Se tiver outra instância do Cache Redis do Azure existente, você poderá usá-la para executar esse exemplo localmente.</span><span class="sxs-lookup"><span data-stu-id="1006f-378">If you have another existing Azure Redis Cache instance, you can use that to run this sample locally.</span></span>
* <span data-ttu-id="1006f-379">Se precisar criar uma instância do Cache Redis do Azure, você poderá seguir as etapas em [Criar um cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="1006f-379">If you need to create an Azure Redis Cache instance, you can follow the steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="1006f-380">Após selecionar ou criar o cache a ser usado, navegue até o cache no portal do Azure e recupere o [nome do host](cache-configure.md#properties) e as [chaves de acesso](cache-configure.md#access-keys) para o cache.</span><span class="sxs-lookup"><span data-stu-id="1006f-380">Once you have selected or created the cache to use, browse to the cache in the Azure portal and retrieve the [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="1006f-381">Para obter instruções, confira [Definir configurações de cache Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="1006f-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="1006f-382">Abra o arquivo `WebAppPlusCacheAppSecrets.config` criado durante a etapa [Configurar o aplicativo para usar o Cache Redis](#configure-the-application-to-use-redis-cache) deste tutorial usando o editor de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="1006f-382">Open the `WebAppPlusCacheAppSecrets.config` file that you created during the [Configure the application to use Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using the editor of your choice.</span></span>
2. <span data-ttu-id="1006f-383">Edite o atributo `value`, substitua `MyCache.redis.cache.windows.net` pelo [nome do host](cache-configure.md#properties) do cache e especifique a [chave primária ou secundária](cache-configure.md#access-keys) do cache como a senha.</span><span class="sxs-lookup"><span data-stu-id="1006f-383">Edit the `value` attribute and replace `MyCache.redis.cache.windows.net` with the [host name](cache-configure.md#properties) of your cache, and specify either the [primary or secondary key](cache-configure.md#access-keys) of your cache as the password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="1006f-384">Pressione **CTRL+F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1006f-384">Press **Ctrl+F5** to run the application.</span></span>

> [!NOTE]
> <span data-ttu-id="1006f-385">Observe que, como o aplicativo, incluindo o banco de dados, é executado localmente e o Cache Redis é hospedado no Azure, o cache poderá parecer ter desempenho inferior ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1006f-385">Note that because the application, including the database, is running locally and the Redis Cache is hosted in Azure, the cache may appear to under-perform the database.</span></span> <span data-ttu-id="1006f-386">Para obter o melhor desempenho, o aplicativo cliente e a instância do Cache Redis do Azure devem estar no mesmo local.</span><span class="sxs-lookup"><span data-stu-id="1006f-386">For best performance, the client application and Azure Redis Cache instance should be in the same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1006f-387">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1006f-387">Next steps</span></span>
* <span data-ttu-id="1006f-388">Saiba mais na [Introdução ao MVC 5 ASP.NET](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) no site do [ASP.NET](http://asp.net/).</span><span class="sxs-lookup"><span data-stu-id="1006f-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on the [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="1006f-389">Para obter mais exemplos de criação de um aplicativo Web ASP.NET no Serviço de Aplicativo, veja [Criar e implantar um aplicativo Web ASP.NET no Serviço de Aplicativo do Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) na [demonstração](https://github.com/Microsoft/HealthClinic.biz) do [HealthClinic.biz](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/) 2015 Connect.</span><span class="sxs-lookup"><span data-stu-id="1006f-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="1006f-390">Para ver mais guias de início rápido da demonstração do HealthClinic.biz, consulte [Azure Developer Tools Quickstarts (Guias de início rápido das ferramentas de desenvolvedor do Azure)](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="1006f-390">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="1006f-391">Saiba mais sobre a abordagem [Code first para um novo banco de dados](https://msdn.microsoft.com/data/jj193542) para o Entity Framework que é usada neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="1006f-391">Learn more about the [Code first to a new database](https://msdn.microsoft.com/data/jj193542) approach to Entity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="1006f-392">Saiba mais sobre [aplicativos Web no Serviço de Aplicativo do Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1006f-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="1006f-393">Saiba como [monitorar](cache-how-to-monitor.md) o cache no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1006f-393">Learn how to [monitor](cache-how-to-monitor.md) your cache in the Azure portal.</span></span>
* <span data-ttu-id="1006f-394">Explore os recursos premium do Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="1006f-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="1006f-395">Como configurar a persistência para um Cache Redis do Azure Premium</span><span class="sxs-lookup"><span data-stu-id="1006f-395">How to configure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="1006f-396">Como configurar o clustering para um Cache Redis do Azure Premium</span><span class="sxs-lookup"><span data-stu-id="1006f-396">How to configure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="1006f-397">Como configurar o suporte de Rede Virtual para um Cache Redis do Azure Premium</span><span class="sxs-lookup"><span data-stu-id="1006f-397">How to configure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="1006f-398">Confira as [Perguntas frequentes sobre o Cache Redis do Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) para saber mais sobre tamanho, taxa de transferência e largura de banda com caches premium.</span><span class="sxs-lookup"><span data-stu-id="1006f-398">See the [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

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

