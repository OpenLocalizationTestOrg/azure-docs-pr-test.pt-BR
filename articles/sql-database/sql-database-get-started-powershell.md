---
title: 'Azure PowerShell: criar um Banco de Dados SQL | Microsoft Docs'
description: "Saiba como toocreate um servidor lógico do banco de dados SQL, regra de firewall de nível de servidor e bancos de dados em Olá portal do Azure."
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
ms.openlocfilehash: e89f68b44083a3b64e61f95117dbbedfa6647ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="394b3-104">Criar um único Banco de Dados SQL do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="394b3-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="394b3-105">PowerShell é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="394b3-105">PowerShell is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="394b3-106">Este guia de detalhes usando o PowerShell toodeploy um banco de dados do SQL Azure em um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) em uma [servidor lógico do banco de dados do Azure SQL](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="394b3-106">This guide details using PowerShell toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="394b3-107">Se você não tiver uma assinatura do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="394b3-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="394b3-108">Este tutorial requer hello Azure PowerShell versão 4.0 ou posterior do módulo.</span><span class="sxs-lookup"><span data-stu-id="394b3-108">This tutorial requires hello Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="394b3-109">Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="394b3-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="394b3-110">Se você precisar tooinstall ou atualização, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="394b3-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="394b3-111">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="394b3-111">Log in tooAzure</span></span>

<span data-ttu-id="394b3-112">Login tooyour assinatura do Azure usando Olá [AzureRmAccount adicionar](/powershell/module/azurerm.profile/add-azurermaccount) de comando e siga o hello instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="394b3-112">Log in tooyour Azure subscription using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="394b3-113">Criar variáveis</span><span class="sxs-lookup"><span data-stu-id="394b3-113">Create variables</span></span>

<span data-ttu-id="394b3-114">Defina variáveis para uso em scripts Olá esse início rápido.</span><span class="sxs-lookup"><span data-stu-id="394b3-114">Define variables for use in hello scripts in this quick start.</span></span>

```powershell
# hello data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# hello login information for hello server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# hello ip address range that you want tooallow tooaccess your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# hello database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="394b3-115">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="394b3-115">Create a resource group</span></span>

<span data-ttu-id="394b3-116">Criar um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) usando Olá [AzureRmResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando.</span><span class="sxs-lookup"><span data-stu-id="394b3-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="394b3-117">Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados em grupo.</span><span class="sxs-lookup"><span data-stu-id="394b3-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="394b3-118">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westeurope` local.</span><span class="sxs-lookup"><span data-stu-id="394b3-118">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="394b3-119">Criar um servidor lógico</span><span class="sxs-lookup"><span data-stu-id="394b3-119">Create a logical server</span></span>

<span data-ttu-id="394b3-120">Criar um [servidor lógico do banco de dados do Azure SQL](sql-database-features.md) usando Olá [AzureRmSqlServer novo](/powershell/module/azurerm.sql/new-azurermsqlserver) comando.</span><span class="sxs-lookup"><span data-stu-id="394b3-120">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="394b3-121">Um servidor lógico contém um grupo de bancos de dados gerenciados conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="394b3-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="394b3-122">Olá exemplo a seguir cria um servidor nomeado aleatoriamente em seu grupo de recursos com um logon de administrador denominado `ServerAdmin` e uma senha de `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="394b3-122">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="394b3-123">Substitua esses valores predefinidos como desejado.</span><span class="sxs-lookup"><span data-stu-id="394b3-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="394b3-124">Configurar uma regra de firewall de servidor</span><span class="sxs-lookup"><span data-stu-id="394b3-124">Configure a server firewall rule</span></span>

<span data-ttu-id="394b3-125">Criar um [regra de firewall de nível de servidor de banco de dados do Azure SQL](sql-database-firewall-configure.md) usando Olá [AzureRmSqlServerFirewallRule novo](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) comando.</span><span class="sxs-lookup"><span data-stu-id="394b3-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="394b3-126">Uma regra de firewall de nível de servidor permite que um aplicativo externo, como SQL Server Management Studio ou hello SQLCMD utilitário tooconnect tooa banco de dados SQL por meio do firewall do serviço de banco de dados SQL hello.</span><span class="sxs-lookup"><span data-stu-id="394b3-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="394b3-127">No hello exemplo a seguir, o firewall Olá só é aberto para outros recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="394b3-127">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="394b3-128">conectividade externa tooenable, change Olá IP endereço tooan apropriado para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="394b3-128">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="394b3-129">tooopen todos os endereços IP, use 0.0.0.0 como Olá Iniciando endereço IP e 255.255.255.255 como Olá endereço final.</span><span class="sxs-lookup"><span data-stu-id="394b3-129">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="394b3-130">O Banco de Dados SQL se comunica pela porta 1433.</span><span class="sxs-lookup"><span data-stu-id="394b3-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="394b3-131">Se você estiver tentando tooconnect de dentro de uma rede corporativa, o tráfego de saída pela porta 1433 talvez não consigam pelo firewall da rede.</span><span class="sxs-lookup"><span data-stu-id="394b3-131">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="394b3-132">Nesse caso, não será tooconnect capaz de servidor de banco de dados SQL de tooyour, a menos que o departamento de TI abre a porta 1433.</span><span class="sxs-lookup"><span data-stu-id="394b3-132">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="394b3-133">Criar um banco de dados no servidor de saudação com dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="394b3-133">Create a database in hello server with sample data</span></span>

<span data-ttu-id="394b3-134">Criar um banco de dados com um [nível de desempenho S0](sql-database-service-tiers.md) no servidor de saudação usando Olá [AzureRmSqlDatabase novo](/powershell/module/azurerm.sql/new-azurermsqldatabase) comando.</span><span class="sxs-lookup"><span data-stu-id="394b3-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="394b3-135">Olá, exemplo a seguir cria um banco de dados chamado `mySampleDatabase` e carrega Olá dados de exemplo AdventureWorksLT para este banco de dados.</span><span class="sxs-lookup"><span data-stu-id="394b3-135">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="394b3-136">Substituir essas predefinidos valores conforme desejado (outros inícios rápidos nesta compilação da coleção após valores hello esse início rápido).</span><span class="sxs-lookup"><span data-stu-id="394b3-136">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="394b3-137">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="394b3-137">Clean up resources</span></span>

<span data-ttu-id="394b3-138">Outros inícios rápidos nessa coleção aproveitam esse início rápido.</span><span class="sxs-lookup"><span data-stu-id="394b3-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="394b3-139">Se você planeja toocontinue toowork com inícios rápidos subsequentes, não limpar os recursos de saudação criados nesse rápido inicie.</span><span class="sxs-lookup"><span data-stu-id="394b3-139">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="394b3-140">Se você não planeja toocontinue, use Olá seguindo as etapas toodelete todos os recursos criados por esse início rápido no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="394b3-140">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="394b3-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="394b3-141">Next steps</span></span>

<span data-ttu-id="394b3-142">Agora que você tem um banco de dados, você pode se conectar e consultar usando suas ferramentas favoritas.</span><span class="sxs-lookup"><span data-stu-id="394b3-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="394b3-143">Saiba mais escolhendo sua ferramenta abaixo:</span><span class="sxs-lookup"><span data-stu-id="394b3-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="394b3-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="394b3-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="394b3-145">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="394b3-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="394b3-146">.NET</span><span class="sxs-lookup"><span data-stu-id="394b3-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="394b3-147">PHP</span><span class="sxs-lookup"><span data-stu-id="394b3-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="394b3-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="394b3-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="394b3-149">Java</span><span class="sxs-lookup"><span data-stu-id="394b3-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="394b3-150">Python</span><span class="sxs-lookup"><span data-stu-id="394b3-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="394b3-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="394b3-151">Ruby</span></span>](sql-database-connect-query-ruby.md)

