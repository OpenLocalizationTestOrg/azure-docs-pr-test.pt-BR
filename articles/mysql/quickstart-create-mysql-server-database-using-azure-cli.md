---
title: "Início rápido: criar um servidor do Banco de Dados do Azure para MySQL – CLI do Azure | Microsoft Docs"
description: "Este guia de início rápido descreve como toouse Olá CLI do Azure toocreate um banco de dados do Azure para o MySQL server em um grupo de recursos do Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="48bce-103">Criar um servidor de Banco de Dados do Azure para MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="48bce-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="48bce-104">Este guia de início rápido descreve como toouse Olá CLI do Azure toocreate um banco de dados do Azure para o MySQL server em um grupo de recursos do Azure em cerca de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="48bce-104">This quickstart describes how toouse hello Azure CLI toocreate an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="48bce-105">Olá CLI do Azure é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="48bce-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span>

<span data-ttu-id="48bce-106">Se você não tiver uma assinatura do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="48bce-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="48bce-107">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="48bce-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="48bce-108">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="48bce-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="48bce-109">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="48bce-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="48bce-110">Se você tiver várias assinaturas, escolha Olá a assinatura de apropriado no qual o recurso de saudação existe ou é cobrado por.</span><span class="sxs-lookup"><span data-stu-id="48bce-110">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="48bce-111">Selecione uma ID da assinatura específica em sua conta usando o comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="48bce-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="48bce-112">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="48bce-112">Create a resource group</span></span>
<span data-ttu-id="48bce-113">Criar um [grupo de recursos do Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) usando Olá [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="48bce-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="48bce-114">Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados em grupo.</span><span class="sxs-lookup"><span data-stu-id="48bce-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="48bce-115">Olá, exemplo a seguir cria um grupo de recursos denominado `myresourcegroup` em Olá `westus` local.</span><span class="sxs-lookup"><span data-stu-id="48bce-115">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="48bce-116">Criar um servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="48bce-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="48bce-117">Criar um banco de dados do Azure para o MySQL server com hello **az mysql server criar** comando.</span><span class="sxs-lookup"><span data-stu-id="48bce-117">Create an Azure Database for MySQL server with hello **az mysql server create** command.</span></span> <span data-ttu-id="48bce-118">Um servidor pode gerenciar vários bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="48bce-118">A server can manage multiple databases.</span></span> <span data-ttu-id="48bce-119">Normalmente, um banco de dados separado é usado para cada projeto ou para cada usuário.</span><span class="sxs-lookup"><span data-stu-id="48bce-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="48bce-120">Olá, exemplo a seguir cria um banco de dados do Azure para o MySQL server localizado em `westus` no grupo de recursos de saudação `myresourcegroup` com o nome `myserver4demo`.</span><span class="sxs-lookup"><span data-stu-id="48bce-120">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="48bce-121">servidor de saudação tem um logon de administrador denominado `myadmin` e a senha `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="48bce-121">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="48bce-122">servidor de saudação é criado com **básica** nível de desempenho e **50** unidades compartilhadas entre todos os bancos de dados de Olá no servidor de saudação de computação.</span><span class="sxs-lookup"><span data-stu-id="48bce-122">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="48bce-123">Você pode escalonar a computação e armazenamento para cima ou para baixo dependendo das necessidades do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="48bce-123">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="48bce-124">Configurar regra de firewall</span><span class="sxs-lookup"><span data-stu-id="48bce-124">Configure firewall rule</span></span>
<span data-ttu-id="48bce-125">Criar um banco de dados do Azure para a regra de firewall no nível do servidor MySQL usando Olá **criar regra de firewall de servidor de mysql de az** comando.</span><span class="sxs-lookup"><span data-stu-id="48bce-125">Create an Azure Database for MySQL server-level firewall rule using hello **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="48bce-126">Uma regra de firewall de nível de servidor permite que um aplicativo externo, como Olá **mysql.exe** ferramenta de linha de comando ou o servidor de tooyour de tooconnect do MySQL Workbench através do firewall de serviço do Azure MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="48bce-126">A server-level firewall rule allows an external application, such as hello **mysql.exe** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="48bce-127">Olá, exemplo a seguir cria uma regra de firewall para um intervalo de endereços predefinido, que neste exemplo é Olá todo possíveis intervalo de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="48bce-127">hello following example creates a firewall rule for a predefined address range, which in this example is hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="48bce-128">Configurar definições de SSL</span><span class="sxs-lookup"><span data-stu-id="48bce-128">Configure SSL settings</span></span>
<span data-ttu-id="48bce-129">Por padrão, as conexões SSL entre o servidor e os aplicativos cliente são impostas.</span><span class="sxs-lookup"><span data-stu-id="48bce-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="48bce-130">Isso garante a segurança de "em movimento" Olá de dados criptografando o fluxo de dados Olá através da internet.</span><span class="sxs-lookup"><span data-stu-id="48bce-130">This ensures security of "in-motion" data by encrypting hello data stream over hello internet.</span></span>  <span data-ttu-id="48bce-131">toomake esse rápido iniciar mais fácil, Desabilitaremos conexões SSL para o servidor.</span><span class="sxs-lookup"><span data-stu-id="48bce-131">toomake this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="48bce-132">Isso não é recomendável para servidores de produção.</span><span class="sxs-lookup"><span data-stu-id="48bce-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="48bce-133">Para obter mais informações, consulte [conectividade de configurar SSL em seu aplicativo toosecurely tooAzure banco de dados de conexão para MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="48bce-133">For more information, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="48bce-134">Olá, exemplo a seguir desabilita impor SSL em seu servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="48bce-134">hello following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a><span data-ttu-id="48bce-135">Obter informações de conexão Olá</span><span class="sxs-lookup"><span data-stu-id="48bce-135">Get hello connection information</span></span>

<span data-ttu-id="48bce-136">tooconnect tooyour server, você precisa ter credenciais de acesso e informações de host de tooprovide.</span><span class="sxs-lookup"><span data-stu-id="48bce-136">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="48bce-137">resultado de saudação está no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="48bce-137">hello result is in JSON format.</span></span> <span data-ttu-id="48bce-138">Anote Olá **fullyQualifiedDomainName** e **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="48bce-138">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a><span data-ttu-id="48bce-139">Conectar usando a ferramenta de linha de comando de mysql.exe de saudação do servidor de toohello</span><span class="sxs-lookup"><span data-stu-id="48bce-139">Connect toohello server using hello mysql.exe command-line tool</span></span>
<span data-ttu-id="48bce-140">Conectar usando a saudação do servidor de tooyour **mysql.exe** ferramenta de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="48bce-140">Connect tooyour server using hello **mysql.exe** command-line tool.</span></span> <span data-ttu-id="48bce-141">Você pode baixar o MySQL [daqui](https://dev.mysql.com/downloads/) e instalá-lo em seu computador.</span><span class="sxs-lookup"><span data-stu-id="48bce-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="48bce-142">Em vez disso, você também pode clicar Olá **Experimente** botão exemplos de código ou Olá `>_` botão de Olá superior direita barra de ferramentas do hello portal do Azure e inicialização Olá **Shell de nuvem do Azure**.</span><span class="sxs-lookup"><span data-stu-id="48bce-142">Instead you may also click hello **Try It** button on code samples, or hello  `>_` button from hello upper right toolbar in hello Azure portal, and launch hello **Azure Cloud Shell**.</span></span>

<span data-ttu-id="48bce-143">Digite os comandos a próxima hello:</span><span class="sxs-lookup"><span data-stu-id="48bce-143">Type hello next commands:</span></span> 

1. <span data-ttu-id="48bce-144">Conecte-se usando o servidor toohello **mysql** ferramenta de linha de comando:</span><span class="sxs-lookup"><span data-stu-id="48bce-144">Connect toohello server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="48bce-145">Exibir o status do servidor:</span><span class="sxs-lookup"><span data-stu-id="48bce-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="48bce-146">Se tudo correr bem, a ferramenta de linha de comando Olá deve gerar Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="48bce-146">If everything goes well, hello command-line tool should output hello following text:</span></span>

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> <span data-ttu-id="48bce-147">Para saber mais sobre outros comandos, veja [Manual de Referência do MySQL 5.7 – Capítulo 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span><span class="sxs-lookup"><span data-stu-id="48bce-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a><span data-ttu-id="48bce-148">Conecte-se o servidor toohello usando a ferramenta de GUI do MySQL Workbench Olá</span><span class="sxs-lookup"><span data-stu-id="48bce-148">Connect toohello server using hello MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="48bce-149">Inicie Olá aplicativo MySQL Workbench no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="48bce-149">Launch hello MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="48bce-150">É possível baixar e instalar o MySQL Workbench [aqui](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="48bce-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="48bce-151">Em Olá **Conexão nova instalação** caixa de diálogo, digite Olá seguintes informações sobre **parâmetros** guia:</span><span class="sxs-lookup"><span data-stu-id="48bce-151">In hello **Setup New Connection** dialog box, enter hello following information on **Parameters** tab:</span></span>

   ![configurar nova conexão](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="48bce-153">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="48bce-153">**Setting**</span></span> | <span data-ttu-id="48bce-154">**Valor Sugerido**</span><span class="sxs-lookup"><span data-stu-id="48bce-154">**Suggested Value**</span></span> | <span data-ttu-id="48bce-155">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="48bce-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="48bce-156">Nome da Conexão</span><span class="sxs-lookup"><span data-stu-id="48bce-156">Connection Name</span></span> | <span data-ttu-id="48bce-157">Minha Conexão</span><span class="sxs-lookup"><span data-stu-id="48bce-157">My Connection</span></span> | <span data-ttu-id="48bce-158">Especifique um nome para essa conexão (pode ser qualquer nome)</span><span class="sxs-lookup"><span data-stu-id="48bce-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="48bce-159">Método de Conexão</span><span class="sxs-lookup"><span data-stu-id="48bce-159">Connection Method</span></span> | <span data-ttu-id="48bce-160">escolha o Padrão (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="48bce-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="48bce-161">Usar o TCP/IP protocolo tooconnect tooAzure banco de dados para MySQL ></span><span class="sxs-lookup"><span data-stu-id="48bce-161">Use TCP/IP protocol tooconnect tooAzure Database for MySQL></span></span> |
| <span data-ttu-id="48bce-162">Nome do host</span><span class="sxs-lookup"><span data-stu-id="48bce-162">Hostname</span></span> | <span data-ttu-id="48bce-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="48bce-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="48bce-164">O nome do servidor que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="48bce-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="48bce-165">Porta</span><span class="sxs-lookup"><span data-stu-id="48bce-165">Port</span></span> | <span data-ttu-id="48bce-166">3306</span><span class="sxs-lookup"><span data-stu-id="48bce-166">3306</span></span> | <span data-ttu-id="48bce-167">porta padrão Olá MySQL é usada.</span><span class="sxs-lookup"><span data-stu-id="48bce-167">hello default port for MySQL is used.</span></span> |
| <span data-ttu-id="48bce-168">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="48bce-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="48bce-169">logon de administrador de servidor Olá observado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="48bce-169">hello server admin login you previously noted.</span></span> |
| <span data-ttu-id="48bce-170">Senha</span><span class="sxs-lookup"><span data-stu-id="48bce-170">Password</span></span> | **** | <span data-ttu-id="48bce-171">Use a senha de conta de administrador Olá configurados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="48bce-171">Use hello admin account password you configured earlier.</span></span> |

<span data-ttu-id="48bce-172">Clique em **Conexão de teste** tootest se todos os parâmetros estão configurados corretamente.</span><span class="sxs-lookup"><span data-stu-id="48bce-172">Click **Test Connection** tootest if all parameters are correctly configured.</span></span>
<span data-ttu-id="48bce-173">Agora, você pode clicar em conexão Olá toosuccessfully conectar toohello server.</span><span class="sxs-lookup"><span data-stu-id="48bce-173">Now, you can click hello connection toosuccessfully connect toohello server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="48bce-174">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="48bce-174">Clean up resources</span></span>
<span data-ttu-id="48bce-175">Se você não precisa desses recursos para outro/tutorial de início rápido, você pode excluí-los fazendo Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="48bce-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing hello following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="48bce-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48bce-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="48bce-177">Como criar um banco de dados MySQL com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="48bce-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
