---
title: 'Azure PowerShell: criar um Banco de Dados SQL | Microsoft Docs'
description: "Aprenda a criar um servidor lógico do Banco de Dados SQL, uma regra de firewall no nível de servidor e bancos de dados com o portal do Azure."
keywords: tutorial do banco de dados SQL, criar um banco de dados SQL
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 44ed4a603977617c898315c4fc0b2d3dd3a8f16a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="58d6c-104">Criar um único Banco de Dados SQL do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="58d6c-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="58d6c-105">O PowerShell é usado para criar e gerenciar recursos do Azure da linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="58d6c-105">PowerShell is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="58d6c-106">Este guia detalha o uso do PowerShell para implantar um Banco de Dados SQL do Azure em um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) em um [servidor lógico do Banco de Dados SQL do Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="58d6c-106">This guide details using PowerShell to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="58d6c-107">Se você não tiver uma assinatura do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="58d6c-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="58d6c-108">Este tutorial requer o módulo do Azure PowerShell, versão 4.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="58d6c-108">This tutorial requires the Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="58d6c-109">Execute ` Get-Module -ListAvailable AzureRM` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="58d6c-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="58d6c-110">Se você precisa instalar ou atualizar, confira [Instalar o módulo do Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="58d6c-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="58d6c-111">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="58d6c-111">Log in to Azure</span></span>

<span data-ttu-id="58d6c-112">Faça logon em sua assinatura do Azure usando o comando [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) e siga as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="58d6c-112">Log in to your Azure subscription using the [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow the on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="58d6c-113">Criar variáveis</span><span class="sxs-lookup"><span data-stu-id="58d6c-113">Create variables</span></span>

<span data-ttu-id="58d6c-114">Defina as variáveis para usar nos scripts neste início rápido.</span><span class="sxs-lookup"><span data-stu-id="58d6c-114">Define variables for use in the scripts in this quick start.</span></span>

```powershell
# The data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# The logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# The login information for the server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# The ip address range that you want to allow to access your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# The database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="58d6c-115">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="58d6c-115">Create a resource group</span></span>

<span data-ttu-id="58d6c-116">Crie um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) usando o comando [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="58d6c-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="58d6c-117">Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados em grupo.</span><span class="sxs-lookup"><span data-stu-id="58d6c-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="58d6c-118">O exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` no local `westeurope`.</span><span class="sxs-lookup"><span data-stu-id="58d6c-118">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="58d6c-119">Criar um servidor lógico</span><span class="sxs-lookup"><span data-stu-id="58d6c-119">Create a logical server</span></span>

<span data-ttu-id="58d6c-120">Crie um [servidor lógico do Banco de Dados SQL do Azure](sql-database-features.md) usando o comando [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver).</span><span class="sxs-lookup"><span data-stu-id="58d6c-120">Create an [Azure SQL Database logical server](sql-database-features.md) using the [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="58d6c-121">Um servidor lógico contém um grupo de bancos de dados gerenciados conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="58d6c-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="58d6c-122">O exemplo a seguir cria um servidor nomeado aleatoriamente no seu grupo de recursos com logon de administrador `ServerAdmin` e senha `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="58d6c-122">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="58d6c-123">Substitua esses valores predefinidos como desejado.</span><span class="sxs-lookup"><span data-stu-id="58d6c-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="58d6c-124">Configurar uma regra de firewall de servidor</span><span class="sxs-lookup"><span data-stu-id="58d6c-124">Configure a server firewall rule</span></span>

<span data-ttu-id="58d6c-125">Crie uma [regra de firewall no nível do servidor do Banco de Dados SQL do Azure](sql-database-firewall-configure.md) usando o comando [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule).</span><span class="sxs-lookup"><span data-stu-id="58d6c-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="58d6c-126">Uma regra de firewall no nível de servidor permite que um aplicativo externo, como o SQL Server Management Studio ou o utilitário SQLCMD, se conecte ao banco de dados SQL através do firewall do serviço de Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="58d6c-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span></span> <span data-ttu-id="58d6c-127">No exemplo a seguir, o firewall está aberto somente para os outros recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="58d6c-127">In the following example, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="58d6c-128">Para habilitar a conectividade externa, altere o endereço IP para um endereço apropriado para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="58d6c-128">To enable external connectivity, change the IP address to an appropriate address for your environment.</span></span> <span data-ttu-id="58d6c-129">Para abrir todos os endereços IP, use 0.0.0.0 como o endereço IP inicial e 255.255.255.255 como o endereço final.</span><span class="sxs-lookup"><span data-stu-id="58d6c-129">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="58d6c-130">O Banco de Dados SQL se comunica pela porta 1433.</span><span class="sxs-lookup"><span data-stu-id="58d6c-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="58d6c-131">Se você estiver tentando conectar-se a partir de uma rede corporativa, o tráfego de saída pela porta 1433 poderá não ser permitido pelo firewall de sua rede.</span><span class="sxs-lookup"><span data-stu-id="58d6c-131">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="58d6c-132">Se isto acontecer, você não conseguirá conectar seu servidor do Banco de Dados SQL do Azure, a menos que o departamento de TI abra a porta 1433.</span><span class="sxs-lookup"><span data-stu-id="58d6c-132">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-the-server-with-sample-data"></a><span data-ttu-id="58d6c-133">Criar um banco de dados no servidor com dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="58d6c-133">Create a database in the server with sample data</span></span>

<span data-ttu-id="58d6c-134">Crie um banco de dados com um [Nível de desempenho do S0](sql-database-service-tiers.md) no servidor usando o comando [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase).</span><span class="sxs-lookup"><span data-stu-id="58d6c-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="58d6c-135">O exemplo a seguir cria um banco de dados denominado `mySampleDatabase` e carrega os dados de exemplo AdventureWorksLT nesse banco de dados.</span><span class="sxs-lookup"><span data-stu-id="58d6c-135">The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="58d6c-136">Substitua os valores predefinidos conforme desejado (outros inícios rápidos nesta coleção aproveitam os valores neste início rápido).</span><span class="sxs-lookup"><span data-stu-id="58d6c-136">Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="58d6c-137">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="58d6c-137">Clean up resources</span></span>

<span data-ttu-id="58d6c-138">Outros inícios rápidos nessa coleção aproveitam esse início rápido.</span><span class="sxs-lookup"><span data-stu-id="58d6c-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="58d6c-139">Se você planeja continuar trabalhando com os inícios rápidos subsequentes, não limpe os recursos criados nesse início rápido.</span><span class="sxs-lookup"><span data-stu-id="58d6c-139">If you plan to continue on to work with subsequent quick starts, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="58d6c-140">Caso contrário, siga estas etapas para excluir todos os recursos criados por esse início rápido no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="58d6c-140">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="58d6c-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="58d6c-141">Next steps</span></span>

<span data-ttu-id="58d6c-142">Agora que você tem um banco de dados, você pode se conectar e consultar usando suas ferramentas favoritas.</span><span class="sxs-lookup"><span data-stu-id="58d6c-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="58d6c-143">Saiba mais escolhendo sua ferramenta abaixo:</span><span class="sxs-lookup"><span data-stu-id="58d6c-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="58d6c-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="58d6c-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="58d6c-145">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="58d6c-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="58d6c-146">.NET</span><span class="sxs-lookup"><span data-stu-id="58d6c-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="58d6c-147">PHP</span><span class="sxs-lookup"><span data-stu-id="58d6c-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="58d6c-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="58d6c-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="58d6c-149">Java</span><span class="sxs-lookup"><span data-stu-id="58d6c-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="58d6c-150">Python</span><span class="sxs-lookup"><span data-stu-id="58d6c-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="58d6c-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="58d6c-151">Ruby</span></span>](sql-database-connect-query-ruby.md)

