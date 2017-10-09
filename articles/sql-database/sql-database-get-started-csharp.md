---
title: "C#: introdução ao Banco de Dados SQL do Azure | Microsoft Docs"
description: "Testar o banco de dados SQL para desenvolver aplicativos SQL e c# e criar um banco de dados do SQL Azure com c# usando Olá biblioteca de banco de dados SQL para .NET."
keywords: Experimente o sql, sql c#
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: cfff2299-a474-4054-8d99-759af1ae5188
ms.service: sql-database
ms.custom: develop apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: csharp
ms.workload: data-management
ms.date: 10/04/2016
ms.author: sstein
ms.openlocfilehash: e880ebabd53546bea37a13186b0f1a13db35b684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-toocreate-a-sql-database-with-hello-sql-database-library-for-net"></a><span data-ttu-id="fa229-104">Usar o c# toocreate um banco de dados do SQL com hello biblioteca de banco de dados SQL para .NET</span><span class="sxs-lookup"><span data-stu-id="fa229-104">Use C# toocreate a SQL database with hello SQL Database Library for .NET</span></span>

<span data-ttu-id="fa229-105">Saiba como toouse c# toocreate um SQL Azure banco de dados com hello [biblioteca de gerenciamento de SQL do Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span><span class="sxs-lookup"><span data-stu-id="fa229-105">Learn how toouse C# toocreate an Azure SQL database with hello [Microsoft Azure SQL Management Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span> <span data-ttu-id="fa229-106">Este artigo descreve como toocreate um único banco de dados SQL e c#.</span><span class="sxs-lookup"><span data-stu-id="fa229-106">This article describes how toocreate a single database with SQL and C#.</span></span> <span data-ttu-id="fa229-107">pools Elásticos de toocreate, consulte [criar um pool Elástico](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="fa229-107">toocreate elastic pools, see [Create an elastic pool](sql-database-elastic-pool-manage-csharp.md).</span></span>

<span data-ttu-id="fa229-108">Olá biblioteca de gerenciamento de banco de dados do Azure SQL para .NET fornece um [do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-com base em API que encapsula Olá [com base no Gerenciador de recursos de API de REST de banco de dados do SQL](https://docs.microsoft.com/rest/api/sql/).</span><span class="sxs-lookup"><span data-stu-id="fa229-108">hello Azure SQL Database Management Library for .NET provides an [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-based API that wraps hello [Resource Manager-based SQL Database REST API](https://docs.microsoft.com/rest/api/sql/).</span></span>

> [!NOTE]
> <span data-ttu-id="fa229-109">Muitos novos recursos do banco de dados SQL só têm suporte quando você estiver usando Olá [modelo de implantação do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), portanto, você sempre deve usar o hello mais recente **biblioteca de gerenciamento de banco de dados do Azure SQL para .NET ([documentos](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [pacote NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**.</span><span class="sxs-lookup"><span data-stu-id="fa229-109">Many new features of SQL Database are only supported when you are using hello [Azure Resource Manager deployment model](../azure-resource-manager/resource-group-overview.md), so you should always use hello latest **Azure SQL Database Management Library for .NET ([docs](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet Package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**.</span></span> <span data-ttu-id="fa229-110">Olá antigo [bibliotecas com base em modelo de implantação clássico](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) têm suporte para compatibilidade com versões anteriores somente, portanto, é recomendável usar bibliotecas mais recentes de Gerenciador de recursos com base em hello.</span><span class="sxs-lookup"><span data-stu-id="fa229-110">hello older [classic deployment model based libraries](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) are supported for backward compatibility only, so we recommend you use hello newer Resource Manager based libraries.</span></span>
> 
> 

<span data-ttu-id="fa229-111">toocomplete Olá etapas neste artigo, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="fa229-111">toocomplete hello steps in this article, you need hello following:</span></span>

* <span data-ttu-id="fa229-112">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa229-112">An Azure subscription.</span></span> <span data-ttu-id="fa229-113">Se precisar de uma assinatura do Azure simplesmente clique **conta gratuita** na parte superior da saudação desta página e retornar toofinish neste artigo.</span><span class="sxs-lookup"><span data-stu-id="fa229-113">If you need an Azure subscription simply click **FREE ACCOUNT** at hello top of this page, and then come back toofinish this article.</span></span>
* <span data-ttu-id="fa229-114">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fa229-114">Visual Studio.</span></span> <span data-ttu-id="fa229-115">Para obter uma cópia gratuita do Visual Studio, consulte Olá [Downloads do Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs) página.</span><span class="sxs-lookup"><span data-stu-id="fa229-115">For a free copy of Visual Studio, see hello [Visual Studio Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) page.</span></span>

> [!NOTE]
> <span data-ttu-id="fa229-116">Este artigo cria um banco de dados SQL em branco.</span><span class="sxs-lookup"><span data-stu-id="fa229-116">This article creates a new, blank SQL database.</span></span> <span data-ttu-id="fa229-117">Modificar Olá *CreateOrUpdateDatabase(...)*  método no hello toocopy os bancos de dados a seguir, dimensionar os bancos de dados, crie um banco de dados em um pool, etc.</span><span class="sxs-lookup"><span data-stu-id="fa229-117">Modify hello *CreateOrUpdateDatabase(...)* method in hello following sample toocopy databases, scale databases, create a database in a pool, etc.</span></span>  
> 

## <a name="create-a-console-app-and-install-hello-required-libraries"></a><span data-ttu-id="fa229-118">Criar um aplicativo de console e instalar bibliotecas de saudação necessária</span><span class="sxs-lookup"><span data-stu-id="fa229-118">Create a console app and install hello required libraries</span></span>
1. <span data-ttu-id="fa229-119">Inicie o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fa229-119">Start Visual Studio.</span></span>
2. <span data-ttu-id="fa229-120">Clique em **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="fa229-120">Click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="fa229-121">Crie um **Aplicativo de Console** do C# e nomeie-o: *SqlDbConsoleApp*</span><span class="sxs-lookup"><span data-stu-id="fa229-121">Create a C# **Console Application** and name it: *SqlDbConsoleApp*</span></span>

<span data-ttu-id="fa229-122">toocreate um banco de dados do SQL com c#, Olá carga necessária bibliotecas de gerenciamento (usando Olá [console do Gerenciador de pacote](http://docs.nuget.org/Consume/Package-Manager-Console)):</span><span class="sxs-lookup"><span data-stu-id="fa229-122">toocreate a SQL database with C#, load hello required management libraries (using hello [package manager console](http://docs.nuget.org/Consume/Package-Manager-Console)):</span></span>

1. <span data-ttu-id="fa229-123">Clique em **Ferramentas** > **Gerenciador de Pacotes do NuGet** > **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="fa229-123">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="fa229-124">Tipo `Install-Package Microsoft.Azure.Management.Sql -Pre` tooinstall hello mais recente [biblioteca de gerenciamento do Microsoft Azure SQL](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span><span class="sxs-lookup"><span data-stu-id="fa229-124">Type `Install-Package Microsoft.Azure.Management.Sql -Pre` tooinstall hello latest [Microsoft Azure SQL Management Library](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span>
3. <span data-ttu-id="fa229-125">Tipo `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall Olá [Gerenciador de recursos de biblioteca do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).</span><span class="sxs-lookup"><span data-stu-id="fa229-125">Type `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall hello [Microsoft Azure Resource Manager Library](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).</span></span>
4. <span data-ttu-id="fa229-126">Tipo `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall Olá [biblioteca de autenticação comuns do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication).</span><span class="sxs-lookup"><span data-stu-id="fa229-126">Type `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall hello [Microsoft Azure Common Authentication Library](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication).</span></span> 

> [!NOTE]
> <span data-ttu-id="fa229-127">Hello exemplos neste artigo usam um formulário síncrono de cada solicitação de API e o bloco até a conclusão da chamada REST de saudação em Olá serviço subjacente.</span><span class="sxs-lookup"><span data-stu-id="fa229-127">hello examples in this article use a synchronous form of each API request and block until completion of hello REST call on hello underlying service.</span></span> <span data-ttu-id="fa229-128">Há métodos assíncronos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="fa229-128">There are async methods available.</span></span>
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a><span data-ttu-id="fa229-129">Criar um servidor do Banco de Dados SQL, regra de firewall e banco de dados SQL - exemplo de C#</span><span class="sxs-lookup"><span data-stu-id="fa229-129">Create a SQL Database server, firewall rule, and SQL database - C# example</span></span>
<span data-ttu-id="fa229-130">saudação de exemplo a seguir cria um grupo de recursos e um banco de dados SQL, regra de firewall e servidor.</span><span class="sxs-lookup"><span data-stu-id="fa229-130">hello following sample creates a resource group, server, firewall rule, and a SQL database.</span></span> <span data-ttu-id="fa229-131">Consulte, [criar um tooaccess principal do serviço recursos](#create-a-service-principal-to-access-resources) tooget Olá `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` variáveis.</span><span class="sxs-lookup"><span data-stu-id="fa229-131">See, [Create a service principal tooaccess resources](#create-a-service-principal-to-access-resources) tooget hello `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` variables.</span></span>

<span data-ttu-id="fa229-132">Substitua o conteúdo de saudação do **Program.cs** com hello seguinte e atualização Olá `{variables}` com seus valores de aplicativo (não inclua Olá `{}`).</span><span class="sxs-lookup"><span data-stu-id="fa229-132">Replace hello contents of **Program.cs** with hello following, and update hello `{variables}` with your app values (do not include hello `{}`).</span></span>

    using Microsoft.Azure;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.Azure.Management.Sql;
    using Microsoft.Azure.Management.Sql.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System;

    namespace SqlDbConsoleApp
    {
    class Program
       {
        // For details about these four (4) values, see
        // https://azure.microsoft.com/documentation/articles/resource-group-authenticate-service-principal/
        static string _subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _tenantId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationSecret = "{your-password}";

        // Create management clients for hello Azure resources your app needs toowork with.
        // This app works with Resource Groups, and Azure SQL Database.
        static ResourceManagementClient _resourceMgmtClient;
        static SqlManagementClient _sqlMgmtClient;

        // Authentication token
        static AuthenticationResult _token;

        // Azure resource variables
        static string _resourceGroupName = "{resource-group-name}";
        static string _resourceGrouplocation = "{Azure-region}";

        static string _serverlocation = _resourceGrouplocation;
        static string _serverName = "{server-name}";
        static string _serverAdmin = "{server-admin-login}";
        static string _serverAdminPassword = "{server-admin-password}";

        static string _firewallRuleName = "{firewall-rule-name}";
        static string _startIpAddress = "{0.0.0.0}";
        static string _endIpAddress = "{255.255.255.255}";

        static string _databaseName = "{dbfromcsarticle}";
        static string _databaseEdition = DatabaseEditions.Basic;
        static string _databasePerfLevel = ""; // "S0", "S1", and so on here for other tiers


        static void Main(string[] args)
        {
            // Authenticate:
            _token = GetToken(_tenantId, _applicationId, _applicationSecret);
            Console.WriteLine("Token acquired. Expires on:" + _token.ExpiresOn);

            // Instantiate management clients:
            _resourceMgmtClient = new ResourceManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken));
            _sqlMgmtClient = new SqlManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken)) { SubscriptionId = _subscriptionId };

            Console.WriteLine("Resource group...");
            ResourceGroup rg = CreateOrUpdateResourceGroup(_resourceMgmtClient, _subscriptionId, _resourceGroupName, _resourceGrouplocation);
            Console.WriteLine("Resource group: " + rg.Id);


            Console.WriteLine("Server...");
            Server sgr = CreateOrUpdateServer(_sqlMgmtClient, _resourceGroupName, _serverlocation, _serverName, _serverAdmin, _serverAdminPassword);
            Console.WriteLine("Server: " + sgr.Id);

            Console.WriteLine("Server firewall...");
            FirewallRule fwr = CreateOrUpdateFirewallRule(_sqlMgmtClient, _resourceGroupName, _serverName, _firewallRuleName, _startIpAddress, _endIpAddress);
            Console.WriteLine("Server firewall: " + fwr.Id);

            Console.WriteLine("Database...");
            Database dbr = CreateOrUpdateDatabase(_sqlMgmtClient, _resourceGroupName, _serverName, _databaseName, _databaseEdition, _databasePerfLevel);
            Console.WriteLine("Database: " + dbr.Id);


            Console.WriteLine("Press any key toocontinue...");
            Console.ReadKey();
        }

        static ResourceGroup CreateOrUpdateResourceGroup(ResourceManagementClient resourceMgmtClient, string subscriptionId, string resourceGroupName, string resourceGroupLocation)
        {
            ResourceGroup resourceGroupParameters = new ResourceGroup()
            {
                Location = resourceGroupLocation,
            };
            resourceMgmtClient.SubscriptionId = subscriptionId;
            ResourceGroup resourceGroupResult = resourceMgmtClient.ResourceGroups.CreateOrUpdate(resourceGroupName, resourceGroupParameters);
            return resourceGroupResult;
        }

        static Server CreateOrUpdateServer(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverLocation, string serverName, string serverAdmin, string serverAdminPassword)
        {
            Server serverParameters = new Server()
            {
                Location = serverLocation,
                AdministratorLogin = serverAdmin,
                AdministratorLoginPassword = serverAdminPassword,
                Version = "12.0"
            };
            Server serverResult = sqlMgmtClient.Servers.CreateOrUpdate(resourceGroupName, serverName, serverParameters);
            return serverResult;
        }

        static FirewallRule CreateOrUpdateFirewallRule(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string firewallRuleName, string startIpAddress, string endIpAddress)
        {
            FirewallRule firewallParameters = new FirewallRule()
            {
                StartIpAddress = startIpAddress,
                EndIpAddress = endIpAddress
            };
            FirewallRule firewallResult = sqlMgmtClient.FirewallRules.CreateOrUpdate(resourceGroupName, serverName, firewallRuleName, firewallParameters);
            return firewallResult;
        }

        static Database CreateOrUpdateDatabase(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string databaseName, string databaseEdition, string databasePerfLevel)
        {
            // Retrieve hello server that will host this database
            Server currentServer = sqlMgmtClient.Servers.Get(resourceGroupName, serverName);

            // Create a database: configure create or update parameters and properties explicitly
            Database newDatabaseParameters = new Database()
            {
                Location = currentServer.Location,
                CreateMode = CreateMode.Default,
                Edition = databaseEdition,
                RequestedServiceObjectiveName = databasePerfLevel

            };
            Database dbResponse = sqlMgmtClient.Databases.CreateOrUpdate(resourceGroupName, serverName, databaseName, newDatabaseParameters);
            return dbResponse;
        }



        private static AuthenticationResult GetToken(string tenantId, string applicationId, string applicationSecret)
        {
            AuthenticationContext authContext = new AuthenticationContext("https://login.windows.net/" + tenantId);
            _token = authContext.AcquireToken("https://management.core.windows.net/", new ClientCredential(applicationId, applicationSecret));
            return _token;
        }
      }
    }





## <a name="create-a-service-principal-tooaccess-resources"></a><span data-ttu-id="fa229-133">Criar um tooaccess principal do serviço de recursos</span><span class="sxs-lookup"><span data-stu-id="fa229-133">Create a service principal tooaccess resources</span></span>
<span data-ttu-id="fa229-134">Olá seguinte script do PowerShell cria aplicativo do Active Directory (AD) hello e serviço Olá principal que precisamos tooauthenticate nosso aplicativo c#.</span><span class="sxs-lookup"><span data-stu-id="fa229-134">hello following PowerShell script creates hello Active Directory (AD) application and hello service principal that we need tooauthenticate our C# app.</span></span> <span data-ttu-id="fa229-135">script Hello gera valores que é necessário para Olá anterior c# de amostra.</span><span class="sxs-lookup"><span data-stu-id="fa229-135">hello script outputs values we need for hello preceding C# sample.</span></span> <span data-ttu-id="fa229-136">Para obter informações detalhadas, consulte [toocreate de usar o Azure PowerShell uma entidade de serviço tooaccess recursos](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="fa229-136">For detailed information, see [Use Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    # Sign in tooAzure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set toohello subscription you want toowork with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is hello display name for your app, must be unique in your directory.
    # $uri does not need toobe a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for hello app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # tooavoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun hello following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output hello values we need for our C# application toosuccessfully authenticate

    Write-Output "Copy these values into hello C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret



## <a name="next-steps"></a><span data-ttu-id="fa229-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fa229-137">Next steps</span></span>
<span data-ttu-id="fa229-138">Agora que você tentou banco de dados SQL e configurar um banco de dados com c#, você está pronto para Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa229-138">Now that you've tried SQL Database and set up a database with C#, you're ready for hello following articles:</span></span>

* [<span data-ttu-id="fa229-139">Conecte-se tooSQL banco de dados com o SQL Server Management Studio e executar um exemplo de consulta T-SQL</span><span class="sxs-lookup"><span data-stu-id="fa229-139">Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query</span></span>](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a><span data-ttu-id="fa229-140">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="fa229-140">Additional Resources</span></span>
* [<span data-ttu-id="fa229-141">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="fa229-141">SQL Database</span></span>](https://azure.microsoft.com/documentation/services/sql-database/)
* [<span data-ttu-id="fa229-142">Classe de Banco de Dados</span><span class="sxs-lookup"><span data-stu-id="fa229-142">Database Class</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

<!--Image references-->
[1]: ./media/sql-database-get-started-csharp/aad.png
[2]: ./media/sql-database-get-started-csharp/permissions.png
[3]: ./media/sql-database-get-started-csharp/getdomain.png
[4]: ./media/sql-database-get-started-csharp/aad2.png
[5]: ./media/sql-database-get-started-csharp/aad-applications.png
[6]: ./media/sql-database-get-started-csharp/add.png
[7]: ./media/sql-database-get-started-csharp/add-application.png
[8]: ./media/sql-database-get-started-csharp/add-application2.png
[9]: ./media/sql-database-get-started-csharp/clientid.png
