---
title: aaaDesign do Azure primeiro banco de dados para o banco de dados MySQL - Portal do Azure | Microsoft Docs
description: Este tutorial explica como toocreate e gerenciar o banco de dados do Azure para o MySQL server e banco de dados usando o Portal do Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="5c404-103">Projetar seu primeiro Banco de Dados do Azure para o banco de dados MySQL</span><span class="sxs-lookup"><span data-stu-id="5c404-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="5c404-104">Banco de dados do Azure para MySQL é um serviço gerenciado que permite que você toorun, gerenciar e dimensionar os bancos de dados MySQL altamente disponíveis na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="5c404-104">Azure Database for MySQL is a managed service that enables you toorun, manage, and scale highly available MySQL databases in hello cloud.</span></span> <span data-ttu-id="5c404-105">Usando Olá portal do Azure, você pode facilmente gerenciar seu servidor e criar um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5c404-105">Using hello Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="5c404-106">Neste tutorial, você usar Olá toolearn portal do Azure como para:</span><span class="sxs-lookup"><span data-stu-id="5c404-106">In this tutorial, you use hello Azure portal toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5c404-107">Criar um Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="5c404-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="5c404-108">Configurar o firewall do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="5c404-108">Configure hello server firewall</span></span>
> * <span data-ttu-id="5c404-109">Usar a ferramenta de linha de comando de mysql toocreate um banco de dados</span><span class="sxs-lookup"><span data-stu-id="5c404-109">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="5c404-110">Carregar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="5c404-110">Load sample data</span></span>
> * <span data-ttu-id="5c404-111">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="5c404-111">Query data</span></span>
> * <span data-ttu-id="5c404-112">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="5c404-112">Update data</span></span>
> * <span data-ttu-id="5c404-113">Restaurar dados</span><span class="sxs-lookup"><span data-stu-id="5c404-113">Restore data</span></span>

## <a name="sign-in-toohello-azure-portal"></a><span data-ttu-id="5c404-114">Entrar toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5c404-114">Sign in toohello Azure portal</span></span>
<span data-ttu-id="5c404-115">Abra seu navegador favorito e visite Olá [portal do Microsoft Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5c404-115">Open your favorite web browser, and visit hello [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="5c404-116">Insira sua credenciais toosign no portal de toohello.</span><span class="sxs-lookup"><span data-stu-id="5c404-116">Enter your credentials toosign in toohello portal.</span></span> <span data-ttu-id="5c404-117">exibição padrão de saudação é seu painel de serviço.</span><span class="sxs-lookup"><span data-stu-id="5c404-117">hello default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="5c404-118">Criar um servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="5c404-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="5c404-119">Um Banco de Dados do Azure para o servidor MySQL é criado com um conjunto definido de recursos de [computação e armazenamento](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="5c404-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="5c404-120">Olá servidor será criado dentro de um [grupo de recursos do Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="5c404-120">hello server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="5c404-121">Navegue muito**bancos de dados** > **banco de dados do Azure para MySQL**.</span><span class="sxs-lookup"><span data-stu-id="5c404-121">Navigate too**Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="5c404-122">Se você não encontrar o servidor MySQL em **bancos de dados** categoria, clique em **ver todos os** tooshow disponível todos os serviços de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5c404-122">If you cannot find MySQL Server under **Databases** category, click **See all** tooshow all available database services.</span></span> <span data-ttu-id="5c404-123">Você também pode digitar **banco de dados do Azure para MySQL** no tooquickly de caixa de pesquisa Olá localizar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c404-123">You can also type **Azure Database for MySQL** in hello search box tooquickly find hello service.</span></span>
<span data-ttu-id="5c404-124">![2-1 Navegue tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="5c404-124">![2-1 Navigate tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="5c404-125">Clique no bloco **Banco de Dados do Azure para MySQL** e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5c404-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="5c404-126">Em nosso exemplo, preencha hello banco de dados do Azure para o formulário do MySQL com hello informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="5c404-126">In our example, fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="5c404-127">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="5c404-127">**Setting**</span></span> | <span data-ttu-id="5c404-128">**Valor sugerido**</span><span class="sxs-lookup"><span data-stu-id="5c404-128">**Suggested value**</span></span> | <span data-ttu-id="5c404-129">**Descrição do Campo**</span><span class="sxs-lookup"><span data-stu-id="5c404-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="5c404-130">*Nome do servidor*</span><span class="sxs-lookup"><span data-stu-id="5c404-130">*Server name*</span></span> | <span data-ttu-id="5c404-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="5c404-131">myserver4demo</span></span>  | <span data-ttu-id="5c404-132">Nome do servidor tem toobe globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="5c404-132">Server name has toobe globally unique.</span></span> |
| <span data-ttu-id="5c404-133">*Assinatura*</span><span class="sxs-lookup"><span data-stu-id="5c404-133">*Subscription*</span></span> | <span data-ttu-id="5c404-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="5c404-134">mysubscription</span></span> | <span data-ttu-id="5c404-135">Selecione sua assinatura na lista suspensa hello.</span><span class="sxs-lookup"><span data-stu-id="5c404-135">Select your subscription from hello drop-down.</span></span> |
| <span data-ttu-id="5c404-136">*Grupo de recursos*</span><span class="sxs-lookup"><span data-stu-id="5c404-136">*Resource group*</span></span> | <span data-ttu-id="5c404-137">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="5c404-137">myresourcegroup</span></span> | <span data-ttu-id="5c404-138">Crie um Grupo de recursos ou use um grupo existente.</span><span class="sxs-lookup"><span data-stu-id="5c404-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="5c404-139">*Logon de administrador do servidor*</span><span class="sxs-lookup"><span data-stu-id="5c404-139">*Server admin login*</span></span> | <span data-ttu-id="5c404-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="5c404-140">myadmin</span></span> | <span data-ttu-id="5c404-141">Nome da conta do administrador de configuração.</span><span class="sxs-lookup"><span data-stu-id="5c404-141">Setup admin account name.</span></span> |
| <span data-ttu-id="5c404-142">*Senha*</span><span class="sxs-lookup"><span data-stu-id="5c404-142">*Password*</span></span> |  | <span data-ttu-id="5c404-143">Defina uma senha de conta de administrador de alta segurança.</span><span class="sxs-lookup"><span data-stu-id="5c404-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="5c404-144">*Confirmar senha*</span><span class="sxs-lookup"><span data-stu-id="5c404-144">*Confirm password*</span></span> |  | <span data-ttu-id="5c404-145">Confirme a senha da conta de administrador hello.</span><span class="sxs-lookup"><span data-stu-id="5c404-145">Confirm hello admin account password.</span></span> |
| <span data-ttu-id="5c404-146">*Localidade*</span><span class="sxs-lookup"><span data-stu-id="5c404-146">*Location*</span></span> |  | <span data-ttu-id="5c404-147">Selecione uma região disponível.</span><span class="sxs-lookup"><span data-stu-id="5c404-147">Select an available region.</span></span> |
| <span data-ttu-id="5c404-148">*Versão*</span><span class="sxs-lookup"><span data-stu-id="5c404-148">*Version*</span></span> | <span data-ttu-id="5c404-149">5.7</span><span class="sxs-lookup"><span data-stu-id="5c404-149">5.7</span></span> | <span data-ttu-id="5c404-150">Escolha a versão mais recente do hello.</span><span class="sxs-lookup"><span data-stu-id="5c404-150">Choose hello latest version.</span></span> |
| <span data-ttu-id="5c404-151">*Configurar o desempenho*</span><span class="sxs-lookup"><span data-stu-id="5c404-151">*Configure performance*</span></span> | <span data-ttu-id="5c404-152">Básico, 50 unidades de computação, 50 GB</span><span class="sxs-lookup"><span data-stu-id="5c404-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="5c404-153">Escolha **Tipo de preço**, **Unidades de Computação**, **Armazenamento (GB)**e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c404-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="5c404-154">*PIN tooDashboard*</span><span class="sxs-lookup"><span data-stu-id="5c404-154">*Pin tooDashboard*</span></span> | <span data-ttu-id="5c404-155">Verificação</span><span class="sxs-lookup"><span data-stu-id="5c404-155">Check</span></span> | <span data-ttu-id="5c404-156">Recomendado toocheck essa caixa para que você pode encontrar o servidor de saudação facilmente no futuro</span><span class="sxs-lookup"><span data-stu-id="5c404-156">Recommended toocheck this box so you may find hello server easily later on</span></span> |
<span data-ttu-id="5c404-157">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5c404-157">Then, click **Create**.</span></span> <span data-ttu-id="5c404-158">Em um ou dois minutos, um novo banco de dados do Azure para o MySQL server está em execução na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="5c404-158">In a minute or two, a new Azure Database for MySQL server is running in hello cloud.</span></span> <span data-ttu-id="5c404-159">Você pode clicar em **notificações** botão no processo de implantação do hello barra de ferramentas toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="5c404-159">You can click **Notifications** button on hello toolbar toomonitor hello deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="5c404-160">Configurar o firewall</span><span class="sxs-lookup"><span data-stu-id="5c404-160">Configure firewall</span></span>
<span data-ttu-id="5c404-161">Os Banco de Dados do Azure para MySQL são protegidos por um firewall.</span><span class="sxs-lookup"><span data-stu-id="5c404-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="5c404-162">Por padrão, todas as conexões toohello server Olá bancos de dados e no servidor de saudação são rejeitados.</span><span class="sxs-lookup"><span data-stu-id="5c404-162">By default, all connections toohello server and hello databases inside hello server are rejected.</span></span> <span data-ttu-id="5c404-163">Antes de conectar tooAzure banco de dados para MySQL para Olá primeira vez, configure o endereço IP da rede pública da máquina do cliente Olá tooadd Olá firewall (ou intervalo de endereços IP).</span><span class="sxs-lookup"><span data-stu-id="5c404-163">Before connecting tooAzure Database for MySQL for hello first time, configure hello firewall tooadd hello client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="5c404-164">Clique em seu servidor recém-criado e depois clique em **Segurança de conexão**.</span><span class="sxs-lookup"><span data-stu-id="5c404-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="5c404-165">![3-1 Segurança da conexão](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="5c404-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="5c404-166">Você pode **Adicionar Meu IP** ou configurar regras de firewall aqui.</span><span class="sxs-lookup"><span data-stu-id="5c404-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="5c404-167">Lembre-se de tooclick **salvar** depois de criar regras de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c404-167">Remember tooclick **Save** after you have created hello rules.</span></span>
<span data-ttu-id="5c404-168">Agora você pode conectar o servidor de toohello usando a ferramenta de linha de comando do mysql ou MySQL Workbench GUI.</span><span class="sxs-lookup"><span data-stu-id="5c404-168">You can now connect toohello server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="5c404-169">O Banco de Dados do Azure para servidor MySQL se comunica pela porta 3306.</span><span class="sxs-lookup"><span data-stu-id="5c404-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="5c404-170">Se você estiver tentando tooconnect de dentro de uma rede corporativa, o tráfego de saída pela porta 3306 talvez não consigam pelo firewall da rede.</span><span class="sxs-lookup"><span data-stu-id="5c404-170">If you are trying tooconnect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="5c404-171">Nesse caso, você não pode se conectar tooAzure MySQL server, a menos que o departamento de TI abre a porta 3306.</span><span class="sxs-lookup"><span data-stu-id="5c404-171">If so, you cannot connect tooAzure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="5c404-172">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="5c404-172">Get connection information</span></span>
<span data-ttu-id="5c404-173">Olá Get totalmente qualificado **nome do servidor** e **nome de logon de administrador do servidor** para seu banco de dados do Azure para o MySQL server de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c404-173">Get hello fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from hello Azure portal.</span></span> <span data-ttu-id="5c404-174">Você usa Olá totalmente qualificado nome tooconnect tooyour server usando a ferramenta de linha de comando do mysql.</span><span class="sxs-lookup"><span data-stu-id="5c404-174">You use hello fully qualified server name tooconnect tooyour server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="5c404-175">Em [portal do Azure](https://portal.azure.com/), clique em **todos os recursos** do menu esquerdo Olá, nome do tipo hello e pesquisa para seu banco de dados do Azure para o MySQL server.</span><span class="sxs-lookup"><span data-stu-id="5c404-175">In [Azure portal](https://portal.azure.com/), click **All resources** from hello left-hand menu, type hello name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="5c404-176">Selecione detalhes de Olá tooview do nome de servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c404-176">Select hello server name tooview hello details.</span></span>

2. <span data-ttu-id="5c404-177">Em configurações de saudação do título, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="5c404-177">Under hello Settings heading, click **Properties**.</span></span> <span data-ttu-id="5c404-178">Anote o **NOME DO SERVIDOR** e o **NOME DE LOGON DO ADMINISTRADOR DO SERVIDOR**.</span><span class="sxs-lookup"><span data-stu-id="5c404-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="5c404-179">Você pode clicar Olá copiar botão Avançar tooeach campo toocopy toohello área de transferência.</span><span class="sxs-lookup"><span data-stu-id="5c404-179">You may click hello copy button next tooeach field toocopy toohello clipboard.</span></span>
   <span data-ttu-id="5c404-180">![4-2 Propriedades do servidor](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="5c404-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="5c404-181">Neste exemplo, o nome do servidor de saudação é *myserver4demo.mysql.database.azure.com*, e o logon de administrador do servidor de saudação é  *myadmin@myserver4demo* .</span><span class="sxs-lookup"><span data-stu-id="5c404-181">In this example, hello server name is *myserver4demo.mysql.database.azure.com*, and hello server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="5c404-182">Conecte-se o servidor toohello usando mysql</span><span class="sxs-lookup"><span data-stu-id="5c404-182">Connect toohello server using mysql</span></span>
<span data-ttu-id="5c404-183">Use [ferramenta de linha de comando do mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish tooyour uma conexão banco de dados do Azure para o MySQL server.</span><span class="sxs-lookup"><span data-stu-id="5c404-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="5c404-184">Você pode executar a ferramenta de linha de comando do mysql Olá de saudação Shell de nuvem do Azure no navegador de saudação ou de sua própria máquina usando ferramentas do mysql instaladas localmente.</span><span class="sxs-lookup"><span data-stu-id="5c404-184">You can run hello mysql command-line tool from hello Azure Cloud Shell in hello browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="5c404-185">Olá toolaunch Shell de nuvem do Azure, clique em Olá `Try It` botão em um bloco de código neste artigo, ou visite Olá portal do Azure e Olá `>_` ícone Olá superior direita da barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="5c404-185">toolaunch hello Azure Cloud Shell, click hello `Try It` button on a code block in this article, or visit hello Azure portal and click hello `>_` icon in hello top right toolbar.</span></span> 

<span data-ttu-id="5c404-186">Digite hello tooconnect de comando:</span><span class="sxs-lookup"><span data-stu-id="5c404-186">Type hello command tooconnect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="5c404-187">Criar um banco de dados vazio</span><span class="sxs-lookup"><span data-stu-id="5c404-187">Create a blank database</span></span>
<span data-ttu-id="5c404-188">Quando estiver conectado toohello server, crie um toowork de banco de dados em branco com.</span><span class="sxs-lookup"><span data-stu-id="5c404-188">Once you’re connected toohello server, create a blank database toowork with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="5c404-189">No prompt de hello, execute Olá após o banco de dados do comando tooswitch conexão toothis recém-criada:</span><span class="sxs-lookup"><span data-stu-id="5c404-189">At hello prompt, run hello following command tooswitch connection toothis newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="5c404-190">Criar tabelas no banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="5c404-190">Create tables in hello database</span></span>
<span data-ttu-id="5c404-191">Agora que você sabe como tooconnect toohello banco de dados para o banco de dados MySQL, podemos ir como toocomplete algumas tarefas básicas.</span><span class="sxs-lookup"><span data-stu-id="5c404-191">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="5c404-192">Primeiro, criamos uma tabela e a carregamos com alguns dados.</span><span class="sxs-lookup"><span data-stu-id="5c404-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="5c404-193">Vamos criar uma tabela que armazena informações de inventário.</span><span class="sxs-lookup"><span data-stu-id="5c404-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="5c404-194">Carregar dados em tabelas de saudação</span><span class="sxs-lookup"><span data-stu-id="5c404-194">Load data into hello tables</span></span>
<span data-ttu-id="5c404-195">Agora que temos uma tabela, podemos inserir alguns dados nela.</span><span class="sxs-lookup"><span data-stu-id="5c404-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="5c404-196">Na janela de prompt de comando aberta hello, execute Olá tooinsert de consulta a seguir algumas linhas de dados.</span><span class="sxs-lookup"><span data-stu-id="5c404-196">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="5c404-197">Agora você tem duas linhas de dados de exemplo na tabela de saudação criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5c404-197">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="5c404-198">Consultar e atualizar dados Olá nas tabelas de saudação</span><span class="sxs-lookup"><span data-stu-id="5c404-198">Query and update hello data in hello tables</span></span>
<span data-ttu-id="5c404-199">Execute Olá consultar tooretrieve informações a seguir da tabela de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c404-199">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="5c404-200">Você também pode atualizar dados Olá nas tabelas de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c404-200">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="5c404-201">linha de saudação obtém atualizada quando você recuperar dados.</span><span class="sxs-lookup"><span data-stu-id="5c404-201">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="5c404-202">Restaurar um ponto anterior do banco de dados tooa no tempo</span><span class="sxs-lookup"><span data-stu-id="5c404-202">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="5c404-203">Imagine que você excluiu acidentalmente uma tabela de banco de dados importantes e não é possível recuperar dados de saudação facilmente.</span><span class="sxs-lookup"><span data-stu-id="5c404-203">Imagine you have accidentally deleted an important database table, and cannot recover hello data easily.</span></span> <span data-ttu-id="5c404-204">Banco de dados do Azure para MySQL permite toorestore Olá server tooa ponto no tempo, criando uma cópia de bancos de dados Olá no novo servidor.</span><span class="sxs-lookup"><span data-stu-id="5c404-204">Azure Database for MySQL allows you toorestore hello server tooa point in time, creating a copy of hello databases into new server.</span></span> <span data-ttu-id="5c404-205">Você pode usar esse novo toorecover de servidor os dados excluídos.</span><span class="sxs-lookup"><span data-stu-id="5c404-205">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="5c404-206">Olá etapas Olá exemplo server tooa ponto de restauração da seguir antes de saudação tabela foi adicionada.</span><span class="sxs-lookup"><span data-stu-id="5c404-206">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

1. <span data-ttu-id="5c404-207">No hello portal do Azure, localize o banco de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="5c404-207">In hello Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="5c404-208">Em Olá **visão geral** , clique em **restaurar** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c404-208">On hello **Overview** page, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="5c404-209">Olá restauração de página é aberta.</span><span class="sxs-lookup"><span data-stu-id="5c404-209">hello Restore page opens.</span></span>

   ![10-1 restaurar um banco de dados](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="5c404-211">Preencha Olá **restaurar** formulário com informações de saudação necessária.</span><span class="sxs-lookup"><span data-stu-id="5c404-211">Fill out hello **Restore** form with hello required information.</span></span>
   
   ![10-2 formulário de restauração](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="5c404-213">**Ponto de restauração**: selecione um point-in-time que você deseja toorestore, dentro do período de saudação listado.</span><span class="sxs-lookup"><span data-stu-id="5c404-213">**Restore point**: Select a point-in-time that you want toorestore to, within hello timeframe listed.</span></span> <span data-ttu-id="5c404-214">Verifique se tooconvert tooUTC seu fuso horário local.</span><span class="sxs-lookup"><span data-stu-id="5c404-214">Make sure tooconvert your local timezone tooUTC.</span></span>
   - <span data-ttu-id="5c404-215">**Restaurar o servidor toonew**: forneça um novo nome de servidor que você deseja toorestore para.</span><span class="sxs-lookup"><span data-stu-id="5c404-215">**Restore toonew server**: Provide a new server name you want toorestore to.</span></span>
   - <span data-ttu-id="5c404-216">**Local**: Olá região é o mesmo que o servidor de origem hello e não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="5c404-216">**Location**: hello region is same as hello source server, and cannot be changed.</span></span>
   - <span data-ttu-id="5c404-217">**Camada de preços**: Olá preço é hello igual Olá servidor de origem e não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="5c404-217">**Pricing tier**: hello pricing tier is hello same as hello source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="5c404-218">Clique em **Okey** toorestore Olá servidor muito[tooa ponto de restauração pontual](./howto-restore-server-portal.md) antes Olá tabela foi excluída.</span><span class="sxs-lookup"><span data-stu-id="5c404-218">Click **OK** toorestore hello server too[restore tooa point in time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="5c404-219">Restaurar um servidor cria uma nova cópia do servidor de saudação, a partir de saudação ponto no tempo que você especificar.</span><span class="sxs-lookup"><span data-stu-id="5c404-219">Restoring a server creates a new copy of hello server, as of hello point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5c404-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5c404-220">Next steps</span></span>
<span data-ttu-id="5c404-221">Neste tutorial, você usar Olá toolearned portal do Azure como para:</span><span class="sxs-lookup"><span data-stu-id="5c404-221">In this tutorial, you use hello Azure portal toolearned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5c404-222">Criar um Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="5c404-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="5c404-223">Configurar o firewall do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="5c404-223">Configure hello server firewall</span></span>
> * <span data-ttu-id="5c404-224">Usar a ferramenta de linha de comando de mysql toocreate um banco de dados</span><span class="sxs-lookup"><span data-stu-id="5c404-224">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="5c404-225">Carregar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="5c404-225">Load sample data</span></span>
> * <span data-ttu-id="5c404-226">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="5c404-226">Query data</span></span>
> * <span data-ttu-id="5c404-227">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="5c404-227">Update data</span></span>
> * <span data-ttu-id="5c404-228">Restaurar dados</span><span class="sxs-lookup"><span data-stu-id="5c404-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5c404-229">Como tooconnect aplicativos tooAzure banco de dados para MySQL</span><span class="sxs-lookup"><span data-stu-id="5c404-229">How tooconnect applications tooAzure Database for MySQL</span></span>](./howto-connection-string.md)
