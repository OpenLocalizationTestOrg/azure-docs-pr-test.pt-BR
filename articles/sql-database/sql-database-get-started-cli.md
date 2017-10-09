---
title: 'CLI do Azure: Criar um banco de dados SQL | Microsoft Docs'
description: "Saiba como toocreate um servidor lógico do banco de dados SQL, a regra de firewall de nível de servidor e bancos de dados usando Olá CLI do Azure."
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
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 9b1ffb17eabeb70a000ff0c997128832b07aa4fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a><span data-ttu-id="bb391-104">Criar um único banco de dados SQL do Azure usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="bb391-104">Create a single Azure SQL database using hello Azure CLI</span></span>

<span data-ttu-id="bb391-105">Olá CLI do Azure é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="bb391-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="bb391-106">Este guia de detalhes usando Olá CLI do Azure toodeploy um banco de dados do SQL Azure em uma [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) em uma [servidor lógico do banco de dados SQL](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="bb391-106">This guide details using hello Azure CLI toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="bb391-107">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="bb391-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bb391-108">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="bb391-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="bb391-109">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb391-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="bb391-110">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bb391-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="bb391-111">Definir variáveis</span><span class="sxs-lookup"><span data-stu-id="bb391-111">Define variables</span></span>

<span data-ttu-id="bb391-112">Defina variáveis para uso em scripts Olá esse início rápido.</span><span class="sxs-lookup"><span data-stu-id="bb391-112">Define variables for use in hello scripts in this quick start.</span></span>

```azurecli-interactive
# hello data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# hello ip address range that you want tooallow tooaccess your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# hello database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a><span data-ttu-id="bb391-113">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="bb391-113">Create a resource group</span></span>

<span data-ttu-id="bb391-114">Criar um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) usando Olá [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="bb391-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="bb391-115">Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados em grupo.</span><span class="sxs-lookup"><span data-stu-id="bb391-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="bb391-116">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westeurope` local.</span><span class="sxs-lookup"><span data-stu-id="bb391-116">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="bb391-117">Criar um servidor lógico</span><span class="sxs-lookup"><span data-stu-id="bb391-117">Create a logical server</span></span>

<span data-ttu-id="bb391-118">Criar um [servidor lógico do banco de dados do Azure SQL](sql-database-features.md) usando Olá [az sql server criar](/cli/azure/sql/server#create) comando.</span><span class="sxs-lookup"><span data-stu-id="bb391-118">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="bb391-119">Um servidor lógico contém um grupo de bancos de dados gerenciados conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="bb391-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="bb391-120">Olá exemplo a seguir cria um servidor nomeado aleatoriamente em seu grupo de recursos com um logon de administrador denominado `ServerAdmin` e uma senha de `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="bb391-120">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="bb391-121">Substitua esses valores predefinidos como desejado.</span><span class="sxs-lookup"><span data-stu-id="bb391-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="bb391-122">Configurar uma regra de firewall de servidor</span><span class="sxs-lookup"><span data-stu-id="bb391-122">Configure a server firewall rule</span></span>

<span data-ttu-id="bb391-123">Criar um [regra de firewall de nível de servidor de banco de dados do Azure SQL](sql-database-firewall-configure.md) usando Olá [firewall do servidor sql az criar](/cli/azure/sql/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="bb391-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="bb391-124">Uma regra de firewall de nível de servidor permite que um aplicativo externo, como SQL Server Management Studio ou hello SQLCMD utilitário tooconnect tooa banco de dados SQL por meio do firewall do serviço de banco de dados SQL hello.</span><span class="sxs-lookup"><span data-stu-id="bb391-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="bb391-125">No hello exemplo a seguir, o firewall Olá só é aberto para outros recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb391-125">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="bb391-126">conectividade externa tooenable, change Olá IP endereço tooan apropriado para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="bb391-126">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="bb391-127">tooopen todos os endereços IP, use 0.0.0.0 como Olá Iniciando endereço IP e 255.255.255.255 como Olá endereço final.</span><span class="sxs-lookup"><span data-stu-id="bb391-127">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="bb391-128">O Banco de Dados SQL se comunica pela porta 1433.</span><span class="sxs-lookup"><span data-stu-id="bb391-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="bb391-129">Se você estiver tentando tooconnect de dentro de uma rede corporativa, o tráfego de saída pela porta 1433 talvez não consigam pelo firewall da rede.</span><span class="sxs-lookup"><span data-stu-id="bb391-129">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="bb391-130">Nesse caso, não será tooconnect capaz de servidor de banco de dados SQL de tooyour, a menos que o departamento de TI abre a porta 1433.</span><span class="sxs-lookup"><span data-stu-id="bb391-130">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="bb391-131">Criar um banco de dados no servidor de saudação com dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="bb391-131">Create a database in hello server with sample data</span></span>

<span data-ttu-id="bb391-132">Criar um banco de dados com um [nível de desempenho S0](sql-database-service-tiers.md) no servidor de saudação usando Olá [criar banco de dados de sql az](/cli/azure/sql/db#create) comando.</span><span class="sxs-lookup"><span data-stu-id="bb391-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="bb391-133">Olá, exemplo a seguir cria um banco de dados chamado `mySampleDatabase` e carrega Olá dados de exemplo AdventureWorksLT para este banco de dados.</span><span class="sxs-lookup"><span data-stu-id="bb391-133">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="bb391-134">Substituir essas predefinidos valores conforme desejado (outros inícios rápidos nesta compilação da coleção após valores hello esse início rápido).</span><span class="sxs-lookup"><span data-stu-id="bb391-134">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="bb391-135">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="bb391-135">Clean up resources</span></span>

<span data-ttu-id="bb391-136">Outros inícios rápidos nessa coleção aproveitam esse início rápido.</span><span class="sxs-lookup"><span data-stu-id="bb391-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="bb391-137">Se você planeja toocontinue toowork com inícios rápidos subsequentes, não limpar os recursos de saudação criados nesse rápido inicie.</span><span class="sxs-lookup"><span data-stu-id="bb391-137">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="bb391-138">Se você não planeja toocontinue, use Olá seguindo as etapas toodelete todos os recursos criados por esse início rápido no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb391-138">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="bb391-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb391-139">Next steps</span></span>

<span data-ttu-id="bb391-140">Agora que você tem um banco de dados, você pode se conectar e consultar usando suas ferramentas favoritas.</span><span class="sxs-lookup"><span data-stu-id="bb391-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="bb391-141">Saiba mais escolhendo sua ferramenta abaixo:</span><span class="sxs-lookup"><span data-stu-id="bb391-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="bb391-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="bb391-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="bb391-143">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="bb391-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="bb391-144">.NET</span><span class="sxs-lookup"><span data-stu-id="bb391-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="bb391-145">PHP</span><span class="sxs-lookup"><span data-stu-id="bb391-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="bb391-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="bb391-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="bb391-147">Java</span><span class="sxs-lookup"><span data-stu-id="bb391-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="bb391-148">Python</span><span class="sxs-lookup"><span data-stu-id="bb391-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="bb391-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="bb391-149">Ruby</span></span>](sql-database-connect-query-ruby.md)

