---
title: "C#: introdução ao Banco de Dados SQL do Azure | Microsoft Docs"
description: Experimente o banco de dados SQL para o desenvolvimento de aplicativos SQL e C# e crie um banco de dados SQL do Azure com o C# usando a Biblioteca do Banco de Dados SQL para .NET.
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
ms.openlocfilehash: c8a2703da1ee3687f8d134e768dd8d31dc4f316b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-c-to-create-a-sql-database-with-the-sql-database-library-for-net"></a><span data-ttu-id="c0134-104">Use o C# para criar um banco de dados SQL com a Biblioteca do Banco de Dados SQL para .NET</span><span class="sxs-lookup"><span data-stu-id="c0134-104">Use C# to create a SQL database with the SQL Database Library for .NET</span></span>

<span data-ttu-id="c0134-105">Saiba como usar o C# para criar um banco de dados SQL do Azure com a [Biblioteca de Gerenciamento do Banco de Dados do Microsoft Azure SQL para .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span><span class="sxs-lookup"><span data-stu-id="c0134-105">Learn how to use C# to create an Azure SQL database with the [Microsoft Azure SQL Management Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span> <span data-ttu-id="c0134-106">Este artigo descreve como criar um banco de dados individual com o SQL e C#.</span><span class="sxs-lookup"><span data-stu-id="c0134-106">This article describes how to create a single database with SQL and C#.</span></span> <span data-ttu-id="c0134-107">Para criar os pools elásticos, veja [Criar um pool elástico](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="c0134-107">To create elastic pools, see [Create an elastic pool](sql-database-elastic-pool-manage-csharp.md).</span></span>

<span data-ttu-id="c0134-108">A Biblioteca de Gerenciamento do Banco de Dados SQL do Azure para .NET fornece uma API baseada no [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) que encapsula a [API REST do Banco de Dados SQL baseada no Resource Manager](https://docs.microsoft.com/rest/api/sql/).</span><span class="sxs-lookup"><span data-stu-id="c0134-108">The Azure SQL Database Management Library for .NET provides an [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-based API that wraps the [Resource Manager-based SQL Database REST API](https://docs.microsoft.com/rest/api/sql/).</span></span>

> [!NOTE]
> <span data-ttu-id="c0134-109">Muitos recursos novos do Banco de Dados SQL só têm suporte quando você está usando o [Modelo de implantação do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), portanto, você sempre deve usar a versão mais recente da **Biblioteca de Gerenciamento do Banco de Dados SQL do Azure para .NET ([documentos](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [Pacote do NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**.</span><span class="sxs-lookup"><span data-stu-id="c0134-109">Many new features of SQL Database are only supported when you are using the [Azure Resource Manager deployment model](../azure-resource-manager/resource-group-overview.md), so you should always use the latest **Azure SQL Database Management Library for .NET ([docs](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet Package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**.</span></span> <span data-ttu-id="c0134-110">As [bibliotecas com base no modelo de implantação clássico](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) mais antigas têm suporte para a compatibilidade com versões anteriores, portanto, é recomendável usar as bibliotecas baseadas no Gerenciador de Recursos mais recentes.</span><span class="sxs-lookup"><span data-stu-id="c0134-110">The older [classic deployment model based libraries](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) are supported for backward compatibility only, so we recommend you use the newer Resource Manager based libraries.</span></span>
> 
> 

<span data-ttu-id="c0134-111">Para concluir as etapas neste artigo, você precisa do seguinte:</span><span class="sxs-lookup"><span data-stu-id="c0134-111">To complete the steps in this article, you need the following:</span></span>

* <span data-ttu-id="c0134-112">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c0134-112">An Azure subscription.</span></span> <span data-ttu-id="c0134-113">Se você precisar de uma assinatura do Azure, basta clicar em **CONTA GRATUITA** na parte superior da página, em seguida, voltar para concluir este artigo.</span><span class="sxs-lookup"><span data-stu-id="c0134-113">If you need an Azure subscription simply click **FREE ACCOUNT** at the top of this page, and then come back to finish this article.</span></span>
* <span data-ttu-id="c0134-114">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c0134-114">Visual Studio.</span></span> <span data-ttu-id="c0134-115">Para obter uma cópia gratuita do Visual Studio, consulte a página [Downloads do Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs) .</span><span class="sxs-lookup"><span data-stu-id="c0134-115">For a free copy of Visual Studio, see the [Visual Studio Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) page.</span></span>

> [!NOTE]
> <span data-ttu-id="c0134-116">Este artigo cria um banco de dados SQL em branco.</span><span class="sxs-lookup"><span data-stu-id="c0134-116">This article creates a new, blank SQL database.</span></span> <span data-ttu-id="c0134-117">Modifique o método *CreateOrUpdateDatabase(...)* no exemplo a seguir para copiar bancos de dados, dimensionar os bancos de dados, criar um banco de dados em um pool etc.</span><span class="sxs-lookup"><span data-stu-id="c0134-117">Modify the *CreateOrUpdateDatabase(...)* method in the following sample to copy databases, scale databases, create a database in a pool, etc.</span></span>  
> 

## <a name="create-a-console-app-and-install-the-required-libraries"></a><span data-ttu-id="c0134-118">Criar um aplicativo de console e instalar as bibliotecas necessárias</span><span class="sxs-lookup"><span data-stu-id="c0134-118">Create a console app and install the required libraries</span></span>
1. <span data-ttu-id="c0134-119">Inicie o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c0134-119">Start Visual Studio.</span></span>
2. <span data-ttu-id="c0134-120">Clique em **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="c0134-120">Click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="c0134-121">Crie um **Aplicativo de Console** do C# e nomeie-o: *SqlDbConsoleApp*</span><span class="sxs-lookup"><span data-stu-id="c0134-121">Create a C# **Console Application** and name it: *SqlDbConsoleApp*</span></span>

<span data-ttu-id="c0134-122">Para criar um banco de dados SQL com o C#, carregue as bibliotecas de gerenciamento necessárias (usando o [console do gerenciador de pacotes](http://docs.nuget.org/Consume/Package-Manager-Console)):</span><span class="sxs-lookup"><span data-stu-id="c0134-122">To create a SQL database with C#, load the required management libraries (using the [package manager console](http://docs.nuget.org/Consume/Package-Manager-Console)):</span></span>

1. <span data-ttu-id="c0134-123">Clique em **Ferramentas** > **Gerenciador de Pacotes do NuGet** > **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="c0134-123">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="c0134-124">Digite `Install-Package Microsoft.Azure.Management.Sql -Pre` para instalar a [Biblioteca de Gerenciamento SQL do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span><span class="sxs-lookup"><span data-stu-id="c0134-124">Type `Install-Package Microsoft.Azure.Management.Sql -Pre` to install the latest [Microsoft Azure SQL Management Library](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span>
3. <span data-ttu-id="c0134-125">Digite `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` para instalar a [Biblioteca do Microsoft Azure Resource Manager](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).</span><span class="sxs-lookup"><span data-stu-id="c0134-125">Type `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` to install the [Microsoft Azure Resource Manager Library](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).</span></span>
4. <span data-ttu-id="c0134-126">Digite `Install-Package Microsoft.Azure.Common.Authentication -Pre` para instalar a [Biblioteca de Autenticação Comum do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication).</span><span class="sxs-lookup"><span data-stu-id="c0134-126">Type `Install-Package Microsoft.Azure.Common.Authentication -Pre` to install the [Microsoft Azure Common Authentication Library](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication).</span></span> 

> [!NOTE]
> <span data-ttu-id="c0134-127">Os exemplos neste artigo usam uma forma síncrona de cada solicitação de API e ficam bloqueados até a conclusão da chamada REST do serviço subjacente.</span><span class="sxs-lookup"><span data-stu-id="c0134-127">The examples in this article use a synchronous form of each API request and block until completion of the REST call on the underlying service.</span></span> <span data-ttu-id="c0134-128">Há métodos assíncronos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c0134-128">There are async methods available.</span></span>
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a><span data-ttu-id="c0134-129">Criar um servidor do Banco de Dados SQL, regra de firewall e banco de dados SQL - exemplo de C#</span><span class="sxs-lookup"><span data-stu-id="c0134-129">Create a SQL Database server, firewall rule, and SQL database - C# example</span></span>
<span data-ttu-id="c0134-130">O exemplo a seguir cria um grupo de recursos, um servidor, uma regra de firewall e um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="c0134-130">The following sample creates a resource group, server, firewall rule, and a SQL database.</span></span> <span data-ttu-id="c0134-131">Confira [Criar uma entidade de serviço para acessar os recursos](#create-a-service-principal-to-access-resources) para obter as variáveis `_subscriptionId, _tenantId, _applicationId, and _applicationSecret`.</span><span class="sxs-lookup"><span data-stu-id="c0134-131">See, [Create a service principal to access resources](#create-a-service-principal-to-access-resources) to get the `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` variables.</span></span>

<span data-ttu-id="c0134-132">Substitua o conteúdo de **Program.cs** pelo seguinte e atualize `{variables}` com seus valores do aplicativo (sem incluir `{}`).</span><span class="sxs-lookup"><span data-stu-id="c0134-132">Replace the contents of **Program.cs** with the following, and update the `{variables}` with your app values (do not include the `{}`).</span></span>

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

        // Create management clients for the Azure resources your app needs to work with.
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


            Console.WriteLine("Press any key to continue...");
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
            // Retrieve the server that will host this database
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





## <a name="create-a-service-principal-to-access-resources"></a><span data-ttu-id="c0134-133">Criar uma entidade de serviço para acessar os recursos</span><span class="sxs-lookup"><span data-stu-id="c0134-133">Create a service principal to access resources</span></span>
<span data-ttu-id="c0134-134">O seguinte script do PowerShell cria o aplicativo do Active Directory (AD) e a entidade de serviço necessária para autenticar nosso aplicativo C#.</span><span class="sxs-lookup"><span data-stu-id="c0134-134">The following PowerShell script creates the Active Directory (AD) application and the service principal that we need to authenticate our C# app.</span></span> <span data-ttu-id="c0134-135">O script gera os valores necessários para o exemplo anterior do C#.</span><span class="sxs-lookup"><span data-stu-id="c0134-135">The script outputs values we need for the preceding C# sample.</span></span> <span data-ttu-id="c0134-136">Para obter informações detalhadas, consulte [usar o Azure PowerShell para criar uma entidade de serviço para acessar os recursos](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="c0134-136">For detailed information, see [Use Azure PowerShell to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    # Sign in to Azure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set to the subscription you want to work with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is the display name for your app, must be unique in your directory.
    # $uri does not need to be a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for the app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # To avoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun the following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output the values we need for our C# application to successfully authenticate

    Write-Output "Copy these values into the C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret



## <a name="next-steps"></a><span data-ttu-id="c0134-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c0134-137">Next steps</span></span>
<span data-ttu-id="c0134-138">Agora que você já experimentou o Banco de Dados SQL e configurou um banco de dados com o C#, está pronto para os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="c0134-138">Now that you've tried SQL Database and set up a database with C#, you're ready for the following articles:</span></span>

* [<span data-ttu-id="c0134-139">Conectar-se ao Banco de Dados SQL com o SQL Server Management Studio e executar um exemplo de consulta T-SQL</span><span class="sxs-lookup"><span data-stu-id="c0134-139">Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query</span></span>](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a><span data-ttu-id="c0134-140">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c0134-140">Additional Resources</span></span>
* [<span data-ttu-id="c0134-141">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="c0134-141">SQL Database</span></span>](https://azure.microsoft.com/documentation/services/sql-database/)
* [<span data-ttu-id="c0134-142">Classe de Banco de Dados</span><span class="sxs-lookup"><span data-stu-id="c0134-142">Database Class</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

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
