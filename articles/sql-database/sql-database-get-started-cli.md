---
title: 'CLI do Azure: Criar um banco de dados SQL | Microsoft Docs'
description: "Aprenda a criar um servidor lógico do Banco de Dados SQL, uma regra de firewall de nível de servidor e bancos de dados usando a CLI do Azure."
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
ms.openlocfilehash: a735f7e6aa65ac36dc4e5a49c5a9a834be43d71a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-single-azure-sql-database-using-the-azure-cli"></a><span data-ttu-id="ccf24-104">Criar um único banco de dados SQL do Azure usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ccf24-104">Create a single Azure SQL database using the Azure CLI</span></span>

<span data-ttu-id="ccf24-105">A CLI do Azure é usada para criar e gerenciar recursos do Azure da linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="ccf24-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="ccf24-106">Este guia detalha o uso da CLI do Azure para implantar um banco de dados SQL do Azure em um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) em um [servidor lógico de banco de dados SQL do Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="ccf24-106">This guide details using the Azure CLI to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="ccf24-107">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="ccf24-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ccf24-108">Se você optar por instalar e usar a CLI localmente, este tópico requer que você execute a CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ccf24-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ccf24-109">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="ccf24-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="ccf24-110">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ccf24-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="ccf24-111">Definir variáveis</span><span class="sxs-lookup"><span data-stu-id="ccf24-111">Define variables</span></span>

<span data-ttu-id="ccf24-112">Defina as variáveis para usar nos scripts neste início rápido.</span><span class="sxs-lookup"><span data-stu-id="ccf24-112">Define variables for use in the scripts in this quick start.</span></span>

```azurecli-interactive
# The data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# The logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# The ip address range that you want to allow to access your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# The database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a><span data-ttu-id="ccf24-113">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ccf24-113">Create a resource group</span></span>

<span data-ttu-id="ccf24-114">Crie um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) usando o comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ccf24-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="ccf24-115">Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados em grupo.</span><span class="sxs-lookup"><span data-stu-id="ccf24-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="ccf24-116">O exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` no local `westeurope`.</span><span class="sxs-lookup"><span data-stu-id="ccf24-116">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="ccf24-117">Criar um servidor lógico</span><span class="sxs-lookup"><span data-stu-id="ccf24-117">Create a logical server</span></span>

<span data-ttu-id="ccf24-118">Crie um [servidor lógico de banco de dados SQL do Azure](sql-database-features.md) usando o comando [az sql server create](/cli/azure/sql/server#create) .</span><span class="sxs-lookup"><span data-stu-id="ccf24-118">Create an [Azure SQL Database logical server](sql-database-features.md) using the [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="ccf24-119">Um servidor lógico contém um grupo de bancos de dados gerenciados conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="ccf24-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="ccf24-120">O exemplo a seguir cria um servidor nomeado aleatoriamente no seu grupo de recursos com logon de administrador `ServerAdmin` e senha `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="ccf24-120">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="ccf24-121">Substitua esses valores predefinidos como desejado.</span><span class="sxs-lookup"><span data-stu-id="ccf24-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="ccf24-122">Configurar uma regra de firewall de servidor</span><span class="sxs-lookup"><span data-stu-id="ccf24-122">Configure a server firewall rule</span></span>

<span data-ttu-id="ccf24-123">Crie uma [ regra de firewall no nível de servidor de banco de dados SQL do Azure](sql-database-firewall-configure.md) usando o comando [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="ccf24-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="ccf24-124">Uma regra de firewall no nível de servidor permite que um aplicativo externo, como o SQL Server Management Studio ou o utilitário SQLCMD, se conecte ao banco de dados SQL através do firewall do serviço de Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="ccf24-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span></span> <span data-ttu-id="ccf24-125">No exemplo a seguir, o firewall está aberto somente para os outros recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf24-125">In the following example, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="ccf24-126">Para habilitar a conectividade externa, altere o endereço IP para um endereço apropriado para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="ccf24-126">To enable external connectivity, change the IP address to an appropriate address for your environment.</span></span> <span data-ttu-id="ccf24-127">Para abrir todos os endereços IP, use 0.0.0.0 como o endereço IP inicial e 255.255.255.255 como o endereço final.</span><span class="sxs-lookup"><span data-stu-id="ccf24-127">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="ccf24-128">O Banco de Dados SQL se comunica pela porta 1433.</span><span class="sxs-lookup"><span data-stu-id="ccf24-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="ccf24-129">Se você estiver tentando conectar-se a partir de uma rede corporativa, o tráfego de saída pela porta 1433 poderá não ser permitido pelo firewall de sua rede.</span><span class="sxs-lookup"><span data-stu-id="ccf24-129">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="ccf24-130">Se isto acontecer, você não conseguirá conectar seu servidor do Banco de Dados SQL do Azure, a menos que o departamento de TI abra a porta 1433.</span><span class="sxs-lookup"><span data-stu-id="ccf24-130">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-the-server-with-sample-data"></a><span data-ttu-id="ccf24-131">Criar um banco de dados no servidor com dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="ccf24-131">Create a database in the server with sample data</span></span>

<span data-ttu-id="ccf24-132">Crie um banco de dados com [nível de desempenho S0](sql-database-service-tiers.md) no servidor usando o comando [az sql db create](/cli/azure/sql/db#create).</span><span class="sxs-lookup"><span data-stu-id="ccf24-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="ccf24-133">O exemplo a seguir cria um banco de dados denominado `mySampleDatabase` e carrega os dados de exemplo AdventureWorksLT nesse banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ccf24-133">The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="ccf24-134">Substitua os valores predefinidos conforme desejado (outros inícios rápidos nesta coleção aproveitam os valores neste início rápido).</span><span class="sxs-lookup"><span data-stu-id="ccf24-134">Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="ccf24-135">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="ccf24-135">Clean up resources</span></span>

<span data-ttu-id="ccf24-136">Outros inícios rápidos nessa coleção aproveitam esse início rápido.</span><span class="sxs-lookup"><span data-stu-id="ccf24-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="ccf24-137">Se você planeja continuar trabalhando com os inícios rápidos subsequentes, não limpe os recursos criados nesse início rápido.</span><span class="sxs-lookup"><span data-stu-id="ccf24-137">If you plan to continue on to work with subsequent quick starts, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="ccf24-138">Caso contrário, siga estas etapas para excluir todos os recursos criados por esse início rápido no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf24-138">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="ccf24-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ccf24-139">Next steps</span></span>

<span data-ttu-id="ccf24-140">Agora que você tem um banco de dados, você pode se conectar e consultar usando suas ferramentas favoritas.</span><span class="sxs-lookup"><span data-stu-id="ccf24-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="ccf24-141">Saiba mais escolhendo sua ferramenta abaixo:</span><span class="sxs-lookup"><span data-stu-id="ccf24-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="ccf24-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="ccf24-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="ccf24-143">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ccf24-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="ccf24-144">.NET</span><span class="sxs-lookup"><span data-stu-id="ccf24-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="ccf24-145">PHP</span><span class="sxs-lookup"><span data-stu-id="ccf24-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="ccf24-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="ccf24-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="ccf24-147">Java</span><span class="sxs-lookup"><span data-stu-id="ccf24-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="ccf24-148">Python</span><span class="sxs-lookup"><span data-stu-id="ccf24-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="ccf24-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="ccf24-149">Ruby</span></span>](sql-database-connect-query-ruby.md)

