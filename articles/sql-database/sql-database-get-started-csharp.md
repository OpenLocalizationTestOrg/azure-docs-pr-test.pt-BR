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
# <a name="use-c-toocreate-a-sql-database-with-hello-sql-database-library-for-net"></a>Usar o c# toocreate um banco de dados do SQL com hello biblioteca de banco de dados SQL para .NET

Saiba como toouse c# toocreate um SQL Azure banco de dados com hello [biblioteca de gerenciamento de SQL do Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql). Este artigo descreve como toocreate um único banco de dados SQL e c#. pools Elásticos de toocreate, consulte [criar um pool Elástico](sql-database-elastic-pool-manage-csharp.md).

Olá biblioteca de gerenciamento de banco de dados do Azure SQL para .NET fornece um [do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-com base em API que encapsula Olá [com base no Gerenciador de recursos de API de REST de banco de dados do SQL](https://docs.microsoft.com/rest/api/sql/).

> [!NOTE]
> Muitos novos recursos do banco de dados SQL só têm suporte quando você estiver usando Olá [modelo de implantação do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), portanto, você sempre deve usar o hello mais recente **biblioteca de gerenciamento de banco de dados do Azure SQL para .NET ([documentos](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [pacote NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**. Olá antigo [bibliotecas com base em modelo de implantação clássico](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) têm suporte para compatibilidade com versões anteriores somente, portanto, é recomendável usar bibliotecas mais recentes de Gerenciador de recursos com base em hello.
> 
> 

toocomplete Olá etapas neste artigo, você precisa seguir hello:

* Uma assinatura do Azure. Se precisar de uma assinatura do Azure simplesmente clique **conta gratuita** na parte superior da saudação desta página e retornar toofinish neste artigo.
* Visual Studio. Para obter uma cópia gratuita do Visual Studio, consulte Olá [Downloads do Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs) página.

> [!NOTE]
> Este artigo cria um banco de dados SQL em branco. Modificar Olá *CreateOrUpdateDatabase(...)*  método no hello toocopy os bancos de dados a seguir, dimensionar os bancos de dados, crie um banco de dados em um pool, etc.  
> 

## <a name="create-a-console-app-and-install-hello-required-libraries"></a>Criar um aplicativo de console e instalar bibliotecas de saudação necessária
1. Inicie o Visual Studio.
2. Clique em **Arquivo** > **Novo** > **Projeto**.
3. Crie um **Aplicativo de Console** do C# e nomeie-o: *SqlDbConsoleApp*

toocreate um banco de dados do SQL com c#, Olá carga necessária bibliotecas de gerenciamento (usando Olá [console do Gerenciador de pacote](http://docs.nuget.org/Consume/Package-Manager-Console)):

1. Clique em **Ferramentas** > **Gerenciador de Pacotes do NuGet** > **Console do Gerenciador de Pacotes**.
2. Tipo `Install-Package Microsoft.Azure.Management.Sql -Pre` tooinstall hello mais recente [biblioteca de gerenciamento do Microsoft Azure SQL](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).
3. Tipo `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall Olá [Gerenciador de recursos de biblioteca do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).
4. Tipo `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall Olá [biblioteca de autenticação comuns do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication). 

> [!NOTE]
> Hello exemplos neste artigo usam um formulário síncrono de cada solicitação de API e o bloco até a conclusão da chamada REST de saudação em Olá serviço subjacente. Há métodos assíncronos disponíveis.
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a>Criar um servidor do Banco de Dados SQL, regra de firewall e banco de dados SQL - exemplo de C#
saudação de exemplo a seguir cria um grupo de recursos e um banco de dados SQL, regra de firewall e servidor. Consulte, [criar um tooaccess principal do serviço recursos](#create-a-service-principal-to-access-resources) tooget Olá `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` variáveis.

Substitua o conteúdo de saudação do **Program.cs** com hello seguinte e atualização Olá `{variables}` com seus valores de aplicativo (não inclua Olá `{}`).

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





## <a name="create-a-service-principal-tooaccess-resources"></a>Criar um tooaccess principal do serviço de recursos
Olá seguinte script do PowerShell cria aplicativo do Active Directory (AD) hello e serviço Olá principal que precisamos tooauthenticate nosso aplicativo c#. script Hello gera valores que é necessário para Olá anterior c# de amostra. Para obter informações detalhadas, consulte [toocreate de usar o Azure PowerShell uma entidade de serviço tooaccess recursos](../azure-resource-manager/resource-group-authenticate-service-principal.md).

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



## <a name="next-steps"></a>Próximas etapas
Agora que você tentou banco de dados SQL e configurar um banco de dados com c#, você está pronto para Olá artigos a seguir:

* [Conecte-se tooSQL banco de dados com o SQL Server Management Studio e executar um exemplo de consulta T-SQL](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a>Recursos adicionais
* [Banco de Dados SQL](https://azure.microsoft.com/documentation/services/sql-database/)
* [Classe de Banco de Dados](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

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
