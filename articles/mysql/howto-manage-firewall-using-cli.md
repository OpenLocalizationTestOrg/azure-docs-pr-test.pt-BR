---
title: Criar e gerenciar regras de firewall do Banco de Dados do Azure para MySQL usando a CLI do Azure | Microsoft Docs
description: Este artigo descreve como criar e gerenciar Banco de Dados do Azure para regras de firewall do MySQL usando a linha de comando CLI do Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 9a03722e9f71be307bdbf0b846a4cbf7b34cd7ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="4c56d-103">Criar e gerenciar regras de firewall do Banco de Dados do Azure para MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4c56d-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="4c56d-104">As regras de firewall no nível de servidor permitem que os administradores gerenciem o acesso a um servidor de Banco de Dados do Azure para MySQL de um endereço IP específico ou intervalo de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="4c56d-104">Server-level firewall rules enable administrators to manage access to an Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="4c56d-105">Usando comandos convenientes da CLI do Azure, você pode criar, atualizar, excluir, listar e mostrar as regras de firewall para gerenciar o servidor.</span><span class="sxs-lookup"><span data-stu-id="4c56d-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="4c56d-106">Para obter uma visão geral dos firewalls do Banco de Dados do Azure para MySQL, confira [Regras de firewall do servidor de Banco de Dados do Azure para MySQL](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="4c56d-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c56d-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4c56d-107">Prerequisites</span></span>
* [<span data-ttu-id="4c56d-108">Instalar a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="4c56d-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="4c56d-109">Instalar o SDK do Azure Python para os serviços PostgreSQL e MySQL</span><span class="sxs-lookup"><span data-stu-id="4c56d-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="4c56d-110">Instalar o componente de CLI do Azure para os serviços PostgreSQL e MySQL</span><span class="sxs-lookup"><span data-stu-id="4c56d-110">Install the Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="4c56d-111">Criar um servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="4c56d-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="4c56d-112">Comandos de regra de firewall:</span><span class="sxs-lookup"><span data-stu-id="4c56d-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="4c56d-113">O comando **az mysql server firewall-rule** é usado na CLI do Azure para criar, excluir, listar, exibir e atualizar regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="4c56d-113">The **az mysql server firewall-rule** command is used from Azure CLI to create, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="4c56d-114">Comandos:</span><span class="sxs-lookup"><span data-stu-id="4c56d-114">Commands:</span></span>
- <span data-ttu-id="4c56d-115">**create**: crie uma regra de firewall de servidor MySQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c56d-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="4c56d-116">**delete**: exclua uma regra de firewall de servidor MySQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c56d-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="4c56d-117">**list**: liste as regras de firewall de servidor MySQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c56d-117">**list** : List the Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="4c56d-118">**show**: mostre os detalhes de uma regra de firewall de servidor MySQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c56d-118">**show** : Show the details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="4c56d-119">**update**: atualize uma regra de firewall de servidor MySQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c56d-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-to-azure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="4c56d-120">Fazer logon no Azure e listar os servidores de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="4c56d-120">Login to Azure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="4c56d-121">Conecte com segurança à CLI do Azure com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c56d-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="4c56d-122">Use o comando **az login** para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="4c56d-122">Use the **az login** command to do this.</span></span>

1. <span data-ttu-id="4c56d-123">Execute o comando a seguir na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="4c56d-123">Run the following command from the command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="4c56d-124">Esse comando retornará um código para usar na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="4c56d-124">This command will output a code to use in the next step.</span></span>

2. <span data-ttu-id="4c56d-125">Use um navegador da Web para abrir a página [https://aka.ms/devicelogin](https://aka.ms/devicelogin) e insira o código.</span><span class="sxs-lookup"><span data-stu-id="4c56d-125">Use a web browser to open the page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter the code.</span></span>

3. <span data-ttu-id="4c56d-126">No prompt, entre utilizando suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c56d-126">At the prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="4c56d-127">Após a autorização do logon, uma lista de assinaturas será impressa no console.</span><span class="sxs-lookup"><span data-stu-id="4c56d-127">Once your login is authorized, a list of subscriptions will be printed in the console.</span></span> <span data-ttu-id="4c56d-128">Copie a id da assinatura desejada para definir a assinatura atual a ser usada da pra frente.</span><span class="sxs-lookup"><span data-stu-id="4c56d-128">Copy the id of the desired subscription to set the current subscription to be used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="4c56d-129">Liste os servidores de Bancos de Dados do Azure para MySQL para sua assinatura e grupo de recursos, se você não tiver certeza dos nomes.</span><span class="sxs-lookup"><span data-stu-id="4c56d-129">List the Azure Databases for MySQL servers for your subscription and resource group if you are unsure of the names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="4c56d-130">Anote o atributo name na lista, que será usado para especificar em qual servidor MySQL trabalhar.</span><span class="sxs-lookup"><span data-stu-id="4c56d-130">Note the name attribute in the listing, which will be used to specify which MySQL server to work on.</span></span> <span data-ttu-id="4c56d-131">Se for necessário, confirme os detalhes desse servidor usando o atributo name para confirmar se o nome está correto:</span><span class="sxs-lookup"><span data-stu-id="4c56d-131">If needed, confirm the details for that server to using the name attribute to confirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="4c56d-132">Listar regras de firewall no servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="4c56d-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="4c56d-133">Usando o nome do servidor e o nome do grupo de recursos, liste as regras de firewall do servidor existentes no servidor.</span><span class="sxs-lookup"><span data-stu-id="4c56d-133">Using the server name and the resource group name, list the existing server firewall rules on the server.</span></span> <span data-ttu-id="4c56d-134">Observe que o atributo de nome do servidor é especificado na opção **-server** e não na opção **-name**.</span><span class="sxs-lookup"><span data-stu-id="4c56d-134">Notice that the server name attribute is specified in the **--server** switch and not the **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="4c56d-135">A saída listará as regras, se houver, por padrão, no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="4c56d-135">The output will list the rules if any, by default in JSON format.</span></span> <span data-ttu-id="4c56d-136">Você pode usar a opção **-output table** para obter um formato de tabela mais legível como saída.</span><span class="sxs-lookup"><span data-stu-id="4c56d-136">You may use the switch **--output table** for a more readable table format as the output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="4c56d-137">Criar uma regra de firewall no servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="4c56d-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="4c56d-138">Usando o nome de servidor MySQL do Azure e o nome do grupo de recursos, crie uma nova regra de firewall no servidor.</span><span class="sxs-lookup"><span data-stu-id="4c56d-138">Using the Azure MySQL server name and the resource group name, create a new firewall rule on the server.</span></span> <span data-ttu-id="4c56d-139">Forneça um nome para a regra, os IPs inicial e final para a regra abranger um intervalo de endereços IP aos quais permitir o acesso.</span><span class="sxs-lookup"><span data-stu-id="4c56d-139">Provide a name for the rule, the start IP, and end IP for the rule to cover a range of IP addresses to allow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="4c56d-140">Para permitir o acesso de um endereço IP único, fornece o mesmo endereço como o IP Inicial e IP Final, como neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="4c56d-140">For a singular IP address to be allowed access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="4c56d-141">Após o êxito, a saída do comando listará os detalhes da regra do firewall que você criou, em formato JSON por padrão.</span><span class="sxs-lookup"><span data-stu-id="4c56d-141">Upon success, the command output will list the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="4c56d-142">Se houver uma falha, a saída mostrará o texto da mensagem de erro em vez disso.</span><span class="sxs-lookup"><span data-stu-id="4c56d-142">If there is a failure, the output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="4c56d-143">Atualizar uma regra de firewall no servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="4c56d-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="4c56d-144">Usando o nome de servidor MySQL do Azure e o nome do grupo de recursos, atualize uma regra de firewall existente no servidor.</span><span class="sxs-lookup"><span data-stu-id="4c56d-144">Using the Azure MySQL server name and the resource group name, update an existing firewall rule on the server.</span></span> <span data-ttu-id="4c56d-145">Forneça o nome da regra de firewall existente como entrada, e os atributos IP inicial e IP final para atualizar.</span><span class="sxs-lookup"><span data-stu-id="4c56d-145">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="4c56d-146">Após o êxito, a saída do comando listará os detalhes da regra do firewall que você atualizou, em formato JSON por padrão.</span><span class="sxs-lookup"><span data-stu-id="4c56d-146">Upon success, the command output will list the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="4c56d-147">Se houver uma falha, a saída mostrará o texto da mensagem de erro em vez disso.</span><span class="sxs-lookup"><span data-stu-id="4c56d-147">If there is a failure, the output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="4c56d-148">Se a regra de firewall não existir, ela será criada pelo comando de atualização.</span><span class="sxs-lookup"><span data-stu-id="4c56d-148">If the firewall rule does not exist, it will be created by the update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="4c56d-149">Mostrar detalhes de uma regra de firewall no servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="4c56d-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="4c56d-150">Usando o nome de servidor MySQL do Azure e o nome do grupo de recursos, mostre os detalhes da regra de firewall existente no servidor.</span><span class="sxs-lookup"><span data-stu-id="4c56d-150">Using the Azure MySQL server name and the resource group name, show the existing firewall rule details from the server.</span></span> <span data-ttu-id="4c56d-151">Forneça o nome da regra de firewall existente como entrada.</span><span class="sxs-lookup"><span data-stu-id="4c56d-151">Provide the name of the existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="4c56d-152">Após o êxito, a saída do comando listará os detalhes da regra do firewall que você especificou, em formato JSON por padrão.</span><span class="sxs-lookup"><span data-stu-id="4c56d-152">Upon success, the command output will list the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="4c56d-153">Se houver uma falha, a saída mostrará o texto da mensagem de erro em vez disso.</span><span class="sxs-lookup"><span data-stu-id="4c56d-153">If there is a failure, the output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="4c56d-154">Excluir uma regra de firewall no servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="4c56d-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="4c56d-155">Usando o nome de servidor MySQL do Azure e o nome do grupo de recursos, remova uma regra de firewall existente do servidor.</span><span class="sxs-lookup"><span data-stu-id="4c56d-155">Using the Azure MySQL server name and the resource group name, remove an existing firewall rule from the server.</span></span> <span data-ttu-id="4c56d-156">Forneça o nome da regra de firewall existente.</span><span class="sxs-lookup"><span data-stu-id="4c56d-156">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="4c56d-157">Após o êxito, não haverá saída.</span><span class="sxs-lookup"><span data-stu-id="4c56d-157">Upon success, there is no output.</span></span> <span data-ttu-id="4c56d-158">Em caso de falha, o texto da mensagem de erro retornará.</span><span class="sxs-lookup"><span data-stu-id="4c56d-158">Upon failure, the error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c56d-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4c56d-159">Next steps</span></span>
- <span data-ttu-id="4c56d-160">Entenda mais sobre [Regras de firewall do servidor de Banco de Dados do Azure para MySQL](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="4c56d-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="4c56d-161">Criar e gerenciar regras de firewall do Banco de Dados do Azure para MySQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4c56d-161">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
