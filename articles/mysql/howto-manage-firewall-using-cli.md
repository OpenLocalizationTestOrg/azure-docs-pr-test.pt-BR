---
title: aaaCreate e gerenciar o banco de dados MySQL para regras de firewall usando a CLI do Azure | Microsoft Docs
description: Este artigo descreve como toocreate e gerenciar o banco de dados MySQL para regras de firewall usando a linha de comando CLI do Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="92243-103">Criar e gerenciar regras de firewall do Banco de Dados do Azure para MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="92243-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="92243-104">Regras de firewall de nível de servidor Habilitar administradores toomanage acesso tooan banco de dados do Azure para MySQL Server de um endereço IP específico ou intervalo de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="92243-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="92243-105">Usando os comandos de CLI do Azure convenientes, você pode criar, atualizar, excluir, lista e mostrar toomanage de regras de firewall em seu servidor.</span><span class="sxs-lookup"><span data-stu-id="92243-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="92243-106">Para obter uma visão geral dos firewalls do Banco de Dados do Azure para MySQL, confira [Regras de firewall do servidor de Banco de Dados do Azure para MySQL](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="92243-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92243-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="92243-107">Prerequisites</span></span>
* [<span data-ttu-id="92243-108">Instalar a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="92243-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="92243-109">Instalar o SDK do Azure Python para os serviços PostgreSQL e MySQL</span><span class="sxs-lookup"><span data-stu-id="92243-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="92243-110">Instalar o componente de CLI do Azure Olá para serviços PostgreSQL e MySQL</span><span class="sxs-lookup"><span data-stu-id="92243-110">Install hello Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="92243-111">Criar um servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="92243-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="92243-112">Comandos de regra de firewall:</span><span class="sxs-lookup"><span data-stu-id="92243-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="92243-113">Olá **regra de firewall de servidor de mysql de az** comando é usado da CLI do Azure toocreate, excluir, listar, mostrar e atualizar regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="92243-113">hello **az mysql server firewall-rule** command is used from Azure CLI toocreate, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="92243-114">Comandos:</span><span class="sxs-lookup"><span data-stu-id="92243-114">Commands:</span></span>
- <span data-ttu-id="92243-115">**create**: crie uma regra de firewall de servidor MySQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="92243-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="92243-116">**delete**: exclua uma regra de firewall de servidor MySQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="92243-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="92243-117">**lista** : lista de regras de firewall de servidor hello Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="92243-117">**list** : List hello Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="92243-118">**Mostrar** : Mostrar detalhes de saudação de um servidor MySQL Azure regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="92243-118">**show** : Show hello details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="92243-119">**update**: atualize uma regra de firewall de servidor MySQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="92243-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="92243-120">Logon tooAzure e lista o banco de dados do Azure para servidores de MySQL</span><span class="sxs-lookup"><span data-stu-id="92243-120">Login tooAzure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="92243-121">Conecte com segurança à CLI do Azure com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="92243-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="92243-122">Saudação de uso **logon az** comando toodo isso.</span><span class="sxs-lookup"><span data-stu-id="92243-122">Use hello **az login** command toodo this.</span></span>

1. <span data-ttu-id="92243-123">Execute Olá comando a seguir na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="92243-123">Run hello following command from hello command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="92243-124">Este comando produzirá um toouse de código na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="92243-124">This command will output a code toouse in hello next step.</span></span>

2. <span data-ttu-id="92243-125">Use um navegador da web página da saudação tooopen [https://aka.ms/devicelogin](https://aka.ms/devicelogin) e insira o código de saudação.</span><span class="sxs-lookup"><span data-stu-id="92243-125">Use a web browser tooopen hello page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter hello code.</span></span>

3. <span data-ttu-id="92243-126">No prompt de hello, faça logon usando suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="92243-126">At hello prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="92243-127">Depois que o seu logon for autorizado, uma lista de assinaturas será impressa no console de saudação.</span><span class="sxs-lookup"><span data-stu-id="92243-127">Once your login is authorized, a list of subscriptions will be printed in hello console.</span></span> <span data-ttu-id="92243-128">Copie a id de saudação do hello desejado assinatura tooset Olá atual assinatura toobe usada no futuro.</span><span class="sxs-lookup"><span data-stu-id="92243-128">Copy hello id of hello desired subscription tooset hello current subscription toobe used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="92243-129">Se você não tiver certeza dos nomes de saudação, lista hello bancos de dados do Azure para servidores de MySQL para sua assinatura e grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="92243-129">List hello Azure Databases for MySQL servers for your subscription and resource group if you are unsure of hello names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="92243-130">Observe o atributo de nome de saudação no hello listando, que será usado toospecify quais toowork do servidor MySQL no.</span><span class="sxs-lookup"><span data-stu-id="92243-130">Note hello name attribute in hello listing, which will be used toospecify which MySQL server toowork on.</span></span> <span data-ttu-id="92243-131">Se necessário, confirme os detalhes de saudação para esse servidor toousing Olá atributo tooconfirm nome está correto:</span><span class="sxs-lookup"><span data-stu-id="92243-131">If needed, confirm hello details for that server toousing hello name attribute tooconfirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="92243-132">Listar regras de firewall no servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="92243-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="92243-133">Usando o nome do servidor de saudação e nome do grupo de recursos hello, lista Olá servidor regras de firewall existentes no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="92243-133">Using hello server name and hello resource group name, list hello existing server firewall rules on hello server.</span></span> <span data-ttu-id="92243-134">Observe que esse atributo de nome de servidor de saudação é especificado no hello **– servidor** alternar e não Olá **– nome** alternar.</span><span class="sxs-lookup"><span data-stu-id="92243-134">Notice that hello server name attribute is specified in hello **--server** switch and not hello **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="92243-135">saída de Hello lista regras Olá se houver, por padrão em JSON de formato.</span><span class="sxs-lookup"><span data-stu-id="92243-135">hello output will list hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="92243-136">Você pode usar o comutador hello **– tabela de saída** para um formato mais legível da tabela como saída de hello.</span><span class="sxs-lookup"><span data-stu-id="92243-136">You may use hello switch **--output table** for a more readable table format as hello output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="92243-137">Criar uma regra de firewall no servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="92243-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="92243-138">Usando o nome do servidor MySQL Azure hello e nome do grupo de recursos hello, crie uma nova regra de firewall no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="92243-138">Using hello Azure MySQL server name and hello resource group name, create a new firewall rule on hello server.</span></span> <span data-ttu-id="92243-139">Forneça um nome para a regra Olá Olá IP de início e IP final para a regra de saudação toocover um acesso de tooallow de endereços IP do intervalo.</span><span class="sxs-lookup"><span data-stu-id="92243-139">Provide a name for hello rule, hello start IP, and end IP for hello rule toocover a range of IP addresses tooallow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="92243-140">Para um único endereço IP toobe permissão de acesso, forneça Olá mesmo endereço como Olá IP inicial e final de IP, como neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="92243-140">For a singular IP address toobe allowed access, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="92243-141">Ao ser bem-sucedido, a saída do comando Olá listará detalhes Olá Olá de regra de firewall criadas por padrão no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="92243-141">Upon success, hello command output will list hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="92243-142">Se houver uma falha, saída de hello mostrará texto da mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="92243-142">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="92243-143">Atualizar uma regra de firewall no servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="92243-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="92243-144">Usando o nome do servidor MySQL Azure hello e nome do grupo de recursos hello, atualize uma regra de firewall existente no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="92243-144">Using hello Azure MySQL server name and hello resource group name, update an existing firewall rule on hello server.</span></span> <span data-ttu-id="92243-145">Forneça o nome de saudação da regra de firewall existente hello como entrada e a saudação inicial IP e término IP atributos tooupdate.</span><span class="sxs-lookup"><span data-stu-id="92243-145">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="92243-146">Ao ser bem-sucedido, a saída do comando Olá listará detalhes Olá Olá de regra de firewall atualizado, por padrão, no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="92243-146">Upon success, hello command output will list hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="92243-147">Se houver uma falha, saída de hello mostrará texto da mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="92243-147">If there is a failure, hello output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="92243-148">Se a regra de firewall de saudação não existir, ele será criado pelo comando de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="92243-148">If hello firewall rule does not exist, it will be created by hello update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="92243-149">Mostrar detalhes de uma regra de firewall no servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="92243-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="92243-150">Usando o nome do servidor MySQL Azure hello e nome do grupo de recursos hello, mostre Olá existente firewall detalhes da regra do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="92243-150">Using hello Azure MySQL server name and hello resource group name, show hello existing firewall rule details from hello server.</span></span> <span data-ttu-id="92243-151">Forneça o nome de saudação da regra de firewall existente hello como entrada.</span><span class="sxs-lookup"><span data-stu-id="92243-151">Provide hello name of hello existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="92243-152">Ao ser bem-sucedido, a saída do comando Olá listará detalhes Olá Olá de regra de firewall especificado, por padrão, no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="92243-152">Upon success, hello command output will list hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="92243-153">Se houver uma falha, saída de hello mostrará texto da mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="92243-153">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="92243-154">Excluir uma regra de firewall no servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="92243-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="92243-155">Usando o nome do servidor MySQL Azure hello e nome do grupo de recursos hello, remova uma regra de firewall existente do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="92243-155">Using hello Azure MySQL server name and hello resource group name, remove an existing firewall rule from hello server.</span></span> <span data-ttu-id="92243-156">Forneça o nome de Olá Olá existente de regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="92243-156">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="92243-157">Após o êxito, não haverá saída.</span><span class="sxs-lookup"><span data-stu-id="92243-157">Upon success, there is no output.</span></span> <span data-ttu-id="92243-158">Em caso de falha, o texto de mensagem de erro de saudação será retornado.</span><span class="sxs-lookup"><span data-stu-id="92243-158">Upon failure, hello error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92243-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="92243-159">Next steps</span></span>
- <span data-ttu-id="92243-160">Entenda mais sobre [Regras de firewall do servidor de Banco de Dados do Azure para MySQL](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="92243-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="92243-161">Criar e gerenciar o banco de dados MySQL para regras de firewall usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="92243-161">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
