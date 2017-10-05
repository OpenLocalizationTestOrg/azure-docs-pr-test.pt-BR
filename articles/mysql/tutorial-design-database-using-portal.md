---
title: Projetar seu primeiro Banco de Dados do Azure para o banco de dados MySQL - Portal do Azure | Microsoft Docs
description: Este tutorial explica como criar e gerenciar o Banco de Dados do Azure para o servidor e banco de dados MySQL usando o Portal do Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: c7b76cacbdc4e483353f64cc4e50c974867bb5b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="86046-103">Projetar seu primeiro Banco de Dados do Azure para o banco de dados MySQL</span><span class="sxs-lookup"><span data-stu-id="86046-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="86046-104">O Banco de Dados do Azure para MySQL é um serviço gerenciado que permite executar, gerenciar e dimensionar bancos de dados altamente disponíveis do MySQL na nuvem.</span><span class="sxs-lookup"><span data-stu-id="86046-104">Azure Database for MySQL is a managed service that enables you to run, manage, and scale highly available MySQL databases in the cloud.</span></span> <span data-ttu-id="86046-105">Usando o Portal do Azure, você pode gerenciar facilmente seu servidor e projetar um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="86046-105">Using the Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="86046-106">Neste tutorial, você usará o Portal do Azure para aprender a:</span><span class="sxs-lookup"><span data-stu-id="86046-106">In this tutorial, you use the Azure portal to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="86046-107">Criar um Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="86046-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="86046-108">Configurar o firewall do servidor</span><span class="sxs-lookup"><span data-stu-id="86046-108">Configure the server firewall</span></span>
> * <span data-ttu-id="86046-109">Usar a ferramenta de linha de comando do MySQL para criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="86046-109">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="86046-110">Carregar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="86046-110">Load sample data</span></span>
> * <span data-ttu-id="86046-111">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="86046-111">Query data</span></span>
> * <span data-ttu-id="86046-112">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="86046-112">Update data</span></span>
> * <span data-ttu-id="86046-113">Restaurar dados</span><span class="sxs-lookup"><span data-stu-id="86046-113">Restore data</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="86046-114">Entrar no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="86046-114">Sign in to the Azure portal</span></span>
<span data-ttu-id="86046-115">Abra seu navegador da Web favorito e visite o [portal do Microsoft Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="86046-115">Open your favorite web browser, and visit the [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="86046-116">Insira suas credenciais para entrar no portal.</span><span class="sxs-lookup"><span data-stu-id="86046-116">Enter your credentials to sign in to the portal.</span></span> <span data-ttu-id="86046-117">A exibição padrão é o painel de serviço.</span><span class="sxs-lookup"><span data-stu-id="86046-117">The default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="86046-118">Criar um Banco de Dados do Azure para o servidor MySQL</span><span class="sxs-lookup"><span data-stu-id="86046-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="86046-119">Um Banco de Dados do Azure para o servidor MySQL é criado com um conjunto definido de recursos de [computação e armazenamento](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="86046-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="86046-120">O servidor é criado dentro de um [Grupo de recursos do Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="86046-120">The server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="86046-121">Navegue para **Bancos de Dados** > **Banco de Dados do Azure para MySQL**.</span><span class="sxs-lookup"><span data-stu-id="86046-121">Navigate to **Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="86046-122">Se você não encontrar o Servidor MySQL na categoria **Bancos de Dados**, clique em **Ver todos** para mostrar todos os serviços de banco de dados disponíveis.</span><span class="sxs-lookup"><span data-stu-id="86046-122">If you cannot find MySQL Server under **Databases** category, click **See all** to show all available database services.</span></span> <span data-ttu-id="86046-123">Você também pode digitar **Banco de Dados do Azure para MySQL** na caixa de pesquisa para localizar rapidamente o serviço.</span><span class="sxs-lookup"><span data-stu-id="86046-123">You can also type **Azure Database for MySQL** in the search box to quickly find the service.</span></span>
<span data-ttu-id="86046-124">![2-1 Navegue até MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="86046-124">![2-1 Navigate to MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="86046-125">Clique no bloco **Banco de Dados do Azure para MySQL** e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="86046-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="86046-126">Em nosso exemplo, preencha o formulário do Banco de Dados do Azure para MySQL com as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="86046-126">In our example, fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="86046-127">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="86046-127">**Setting**</span></span> | <span data-ttu-id="86046-128">**Valor sugerido**</span><span class="sxs-lookup"><span data-stu-id="86046-128">**Suggested value**</span></span> | <span data-ttu-id="86046-129">**Descrição do Campo**</span><span class="sxs-lookup"><span data-stu-id="86046-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="86046-130">*Nome do servidor*</span><span class="sxs-lookup"><span data-stu-id="86046-130">*Server name*</span></span> | <span data-ttu-id="86046-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="86046-131">myserver4demo</span></span>  | <span data-ttu-id="86046-132">O nome do servidor precisa ser exclusivo globalmente.</span><span class="sxs-lookup"><span data-stu-id="86046-132">Server name has to be globally unique.</span></span> |
| <span data-ttu-id="86046-133">*Assinatura*</span><span class="sxs-lookup"><span data-stu-id="86046-133">*Subscription*</span></span> | <span data-ttu-id="86046-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="86046-134">mysubscription</span></span> | <span data-ttu-id="86046-135">Selecione sua assinatura na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="86046-135">Select your subscription from the drop-down.</span></span> |
| <span data-ttu-id="86046-136">*Grupo de recursos*</span><span class="sxs-lookup"><span data-stu-id="86046-136">*Resource group*</span></span> | <span data-ttu-id="86046-137">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="86046-137">myresourcegroup</span></span> | <span data-ttu-id="86046-138">Crie um Grupo de recursos ou use um grupo existente.</span><span class="sxs-lookup"><span data-stu-id="86046-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="86046-139">*Logon de administrador do servidor*</span><span class="sxs-lookup"><span data-stu-id="86046-139">*Server admin login*</span></span> | <span data-ttu-id="86046-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="86046-140">myadmin</span></span> | <span data-ttu-id="86046-141">Nome da conta do administrador de configuração.</span><span class="sxs-lookup"><span data-stu-id="86046-141">Setup admin account name.</span></span> |
| <span data-ttu-id="86046-142">*Senha*</span><span class="sxs-lookup"><span data-stu-id="86046-142">*Password*</span></span> |  | <span data-ttu-id="86046-143">Defina uma senha de conta de administrador de alta segurança.</span><span class="sxs-lookup"><span data-stu-id="86046-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="86046-144">*Confirmar senha*</span><span class="sxs-lookup"><span data-stu-id="86046-144">*Confirm password*</span></span> |  | <span data-ttu-id="86046-145">Confirme a senha da conta do administrador.</span><span class="sxs-lookup"><span data-stu-id="86046-145">Confirm the admin account password.</span></span> |
| <span data-ttu-id="86046-146">*Localidade*</span><span class="sxs-lookup"><span data-stu-id="86046-146">*Location*</span></span> |  | <span data-ttu-id="86046-147">Selecione uma região disponível.</span><span class="sxs-lookup"><span data-stu-id="86046-147">Select an available region.</span></span> |
| <span data-ttu-id="86046-148">*Versão*</span><span class="sxs-lookup"><span data-stu-id="86046-148">*Version*</span></span> | <span data-ttu-id="86046-149">5.7</span><span class="sxs-lookup"><span data-stu-id="86046-149">5.7</span></span> | <span data-ttu-id="86046-150">Escolha a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="86046-150">Choose the latest version.</span></span> |
| <span data-ttu-id="86046-151">*Configurar o desempenho*</span><span class="sxs-lookup"><span data-stu-id="86046-151">*Configure performance*</span></span> | <span data-ttu-id="86046-152">Básico, 50 unidades de computação, 50 GB</span><span class="sxs-lookup"><span data-stu-id="86046-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="86046-153">Escolha **Tipo de preço**, **Unidades de Computação**, **Armazenamento (GB)**e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="86046-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="86046-154">*Fixar no painel*</span><span class="sxs-lookup"><span data-stu-id="86046-154">*Pin to Dashboard*</span></span> | <span data-ttu-id="86046-155">Verificação</span><span class="sxs-lookup"><span data-stu-id="86046-155">Check</span></span> | <span data-ttu-id="86046-156">Recomenda-se marcar essa caixa de seleção para poder encontrar o servidor facilmente no futuro</span><span class="sxs-lookup"><span data-stu-id="86046-156">Recommended to check this box so you may find the server easily later on</span></span> |
<span data-ttu-id="86046-157">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="86046-157">Then, click **Create**.</span></span> <span data-ttu-id="86046-158">Em um ou dois minutos, um novo Banco de Dados para servidor MySQL estará em execução na nuvem.</span><span class="sxs-lookup"><span data-stu-id="86046-158">In a minute or two, a new Azure Database for MySQL server is running in the cloud.</span></span> <span data-ttu-id="86046-159">Na barra de ferramentas, clique no botão **Notificações** para monitorar o processo de implantação.</span><span class="sxs-lookup"><span data-stu-id="86046-159">You can click **Notifications** button on the toolbar to monitor the deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="86046-160">Configurar o firewall</span><span class="sxs-lookup"><span data-stu-id="86046-160">Configure firewall</span></span>
<span data-ttu-id="86046-161">Os Banco de Dados do Azure para MySQL são protegidos por um firewall.</span><span class="sxs-lookup"><span data-stu-id="86046-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="86046-162">Por padrão, todas as conexões com o servidor e com os bancos de dados dentro do servidor são rejeitadas.</span><span class="sxs-lookup"><span data-stu-id="86046-162">By default, all connections to the server and the databases inside the server are rejected.</span></span> <span data-ttu-id="86046-163">Antes de se conectar ao Banco de Dados do Azure para MySQL pela primeira vez, configure o firewall para adicionar o endereço IP (ou o intervalo de endereços IP) da rede pública do computador cliente.</span><span class="sxs-lookup"><span data-stu-id="86046-163">Before connecting to Azure Database for MySQL for the first time, configure the firewall to add the client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="86046-164">Clique em seu servidor recém-criado e depois clique em **Segurança de conexão**.</span><span class="sxs-lookup"><span data-stu-id="86046-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="86046-165">![3-1 Segurança da conexão](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="86046-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="86046-166">Você pode **Adicionar Meu IP** ou configurar regras de firewall aqui.</span><span class="sxs-lookup"><span data-stu-id="86046-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="86046-167">Lembre-se de clicar em **Salvar** depois de criar as regras.</span><span class="sxs-lookup"><span data-stu-id="86046-167">Remember to click **Save** after you have created the rules.</span></span>
<span data-ttu-id="86046-168">Agora você pode se conectar ao servidor usando a ferramenta de linha de comando do MySQL ou a ferramenta de GUI do MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="86046-168">You can now connect to the server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="86046-169">O Banco de Dados do Azure para servidor MySQL se comunica pela porta 3306.</span><span class="sxs-lookup"><span data-stu-id="86046-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="86046-170">Se você estiver tentando conectar-se a partir de uma rede corporativa, o tráfego de saída pela porta 3306 poderá não ser permitido pelo firewall de sua rede.</span><span class="sxs-lookup"><span data-stu-id="86046-170">If you are trying to connect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="86046-171">Se isto acontecer, você não poderá se conectar ao MySQL Server do Azure, a menos que o departamento de TI abra a porta 3306.</span><span class="sxs-lookup"><span data-stu-id="86046-171">If so, you cannot connect to Azure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="86046-172">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="86046-172">Get connection information</span></span>
<span data-ttu-id="86046-173">Obtenha o **Nome do servidor** e o **Nome de logon do administrador do servidor** totalmente qualificados para o Banco de Dados do Azure para MySQL Server no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="86046-173">Get the fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from the Azure portal.</span></span> <span data-ttu-id="86046-174">Use o nome do servidor totalmente qualificado para se conectar ao servidor usando a ferramenta de linha de comando do MySQL.</span><span class="sxs-lookup"><span data-stu-id="86046-174">You use the fully qualified server name to connect to your server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="86046-175">No [portal do Azure](https://portal.azure.com/), clique em **Todos os recursos** no menu à esquerda, digite o nome e pesquise o Banco de Dados do Azure para MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="86046-175">In [Azure portal](https://portal.azure.com/), click **All resources** from the left-hand menu, type the name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="86046-176">Selecione o nome do servidor para exibir os detalhes.</span><span class="sxs-lookup"><span data-stu-id="86046-176">Select the server name to view the details.</span></span>

2. <span data-ttu-id="86046-177">No cabeçalho Configurações, clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="86046-177">Under the Settings heading, click **Properties**.</span></span> <span data-ttu-id="86046-178">Anote o **NOME DO SERVIDOR** e o **NOME DE LOGON DO ADMINISTRADOR DO SERVIDOR**.</span><span class="sxs-lookup"><span data-stu-id="86046-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="86046-179">Clique no botão Copiar ao lado de cada campo para copiar para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="86046-179">You may click the copy button next to each field to copy to the clipboard.</span></span>
   <span data-ttu-id="86046-180">![4-2 Propriedades do servidor](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="86046-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="86046-181">Neste exemplo, o nome do servidor é *myserver4demo.mysql.database.azure.com* e o logon de administrador do servidor é  *myadmin@myserver4demo* .</span><span class="sxs-lookup"><span data-stu-id="86046-181">In this example, the server name is *myserver4demo.mysql.database.azure.com*, and the server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="86046-182">Conectar-se ao servidor usando mysql</span><span class="sxs-lookup"><span data-stu-id="86046-182">Connect to the server using mysql</span></span>
<span data-ttu-id="86046-183">Use a [ferramenta de linha de comando do mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) para estabelecer uma conexão com seu Banco de Dados do Azure para servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="86046-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="86046-184">Execute a ferramenta de linha de comando do MySQL no Azure Cloud Shell no navegador ou no próprio computador usando as ferramentas do MySQL instaladas localmente.</span><span class="sxs-lookup"><span data-stu-id="86046-184">You can run the mysql command-line tool from the Azure Cloud Shell in the browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="86046-185">Para iniciar o Azure Cloud Shell, clique no botão `Try It` em um bloco de código deste artigo ou visite o portal do Azure e clique no ícone `>_` na barra de ferramentas superior direita.</span><span class="sxs-lookup"><span data-stu-id="86046-185">To launch the Azure Cloud Shell, click the `Try It` button on a code block in this article, or visit the Azure portal and click the `>_` icon in the top right toolbar.</span></span> 

<span data-ttu-id="86046-186">Digite o comando para se conectar:</span><span class="sxs-lookup"><span data-stu-id="86046-186">Type the command to connect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="86046-187">Criar um banco de dados vazio</span><span class="sxs-lookup"><span data-stu-id="86046-187">Create a blank database</span></span>
<span data-ttu-id="86046-188">Quando você estiver conectado ao servidor, crie um banco de dados em branco com o qual trabalhar.</span><span class="sxs-lookup"><span data-stu-id="86046-188">Once you’re connected to the server, create a blank database to work with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="86046-189">No prompt, execute o seguinte comando para mudar a conexão para esse banco de dados recém-criado:</span><span class="sxs-lookup"><span data-stu-id="86046-189">At the prompt, run the following command to switch connection to this newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="86046-190">Criar tabelas no banco de dados</span><span class="sxs-lookup"><span data-stu-id="86046-190">Create tables in the database</span></span>
<span data-ttu-id="86046-191">Agora que você sabe como se conectar ao Banco de Dados do Azure para banco de dados MySQL, podemos falar sobre como concluir algumas tarefas básicas.</span><span class="sxs-lookup"><span data-stu-id="86046-191">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="86046-192">Primeiro, criamos uma tabela e a carregamos com alguns dados.</span><span class="sxs-lookup"><span data-stu-id="86046-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="86046-193">Vamos criar uma tabela que armazena informações de inventário.</span><span class="sxs-lookup"><span data-stu-id="86046-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="86046-194">Carregar dados nas tabelas</span><span class="sxs-lookup"><span data-stu-id="86046-194">Load data into the tables</span></span>
<span data-ttu-id="86046-195">Agora que temos uma tabela, podemos inserir alguns dados nela.</span><span class="sxs-lookup"><span data-stu-id="86046-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="86046-196">Na janela do prompt de comando aberta, execute a consulta a seguir para inserir algumas linhas de dados.</span><span class="sxs-lookup"><span data-stu-id="86046-196">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="86046-197">Agora, você tem duas linhas de dados de exemplo na tabela criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="86046-197">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="86046-198">Consultar e atualizar os dados nas tabelas</span><span class="sxs-lookup"><span data-stu-id="86046-198">Query and update the data in the tables</span></span>
<span data-ttu-id="86046-199">Execute a seguinte consulta para recuperar as informações da tabela do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="86046-199">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="86046-200">Também é possível atualizar os dados nas tabelas.</span><span class="sxs-lookup"><span data-stu-id="86046-200">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="86046-201">A linha é atualizada à medida que você recupera os dados.</span><span class="sxs-lookup"><span data-stu-id="86046-201">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="86046-202">Restaurar um banco de dados em um ponto anterior no tempo</span><span class="sxs-lookup"><span data-stu-id="86046-202">Restore a database to a previous point in time</span></span>
<span data-ttu-id="86046-203">Imagine que você excluiu acidentalmente uma tabela de banco de dados importante e não consegue recuperar os dados com facilidade.</span><span class="sxs-lookup"><span data-stu-id="86046-203">Imagine you have accidentally deleted an important database table, and cannot recover the data easily.</span></span> <span data-ttu-id="86046-204">O Banco de Dados do Azure para MySQL permite restaurar o servidor para um ponto no tempo, criando uma cópia dos bancos de dados no novo servidor.</span><span class="sxs-lookup"><span data-stu-id="86046-204">Azure Database for MySQL allows you to restore the server to a point in time, creating a copy of the databases into new server.</span></span> <span data-ttu-id="86046-205">Use esse novo servidor para recuperar seus dados excluídos.</span><span class="sxs-lookup"><span data-stu-id="86046-205">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="86046-206">As etapas a seguir restauram o servidor de exemplo para um ponto anterior à adição da tabela.</span><span class="sxs-lookup"><span data-stu-id="86046-206">The following steps restore the sample server to a point before the table was added.</span></span>

1. <span data-ttu-id="86046-207">No portal do Azure, localize o Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="86046-207">In the Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="86046-208">Na página **Visão Geral**, clique em **Restaurar** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="86046-208">On the **Overview** page, click **Restore** on the toolbar.</span></span> <span data-ttu-id="86046-209">A página Restaurar é aberta.</span><span class="sxs-lookup"><span data-stu-id="86046-209">The Restore page opens.</span></span>

   ![10-1 restaurar um banco de dados](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="86046-211">Preencha o formulário **Restaurar** com as informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="86046-211">Fill out the **Restore** form with the required information.</span></span>
   
   ![10-2 formulário de restauração](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="86046-213">**Ponto de restauração**: selecione um ponto no tempo no qual você deseja restaurar, dentro do período listado.</span><span class="sxs-lookup"><span data-stu-id="86046-213">**Restore point**: Select a point-in-time that you want to restore to, within the timeframe listed.</span></span> <span data-ttu-id="86046-214">Lembre-se de converter o fuso horário local para UTC.</span><span class="sxs-lookup"><span data-stu-id="86046-214">Make sure to convert your local timezone to UTC.</span></span>
   - <span data-ttu-id="86046-215">**Restaurar em novo servidor**: forneça um novo nome do servidor no qual você deseja restaurar.</span><span class="sxs-lookup"><span data-stu-id="86046-215">**Restore to new server**: Provide a new server name you want to restore to.</span></span>
   - <span data-ttu-id="86046-216">**Localização**: a região é o mesma do servidor de origem e não pode ser alterada.</span><span class="sxs-lookup"><span data-stu-id="86046-216">**Location**: The region is same as the source server, and cannot be changed.</span></span>
   - <span data-ttu-id="86046-217">**Tipo de preço**: o tipo de preço é o mesmo do servidor de origem e não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="86046-217">**Pricing tier**: The pricing tier is the same as the source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="86046-218">Clique em **OK** para restaurar o servidor [em um ponto no tempo](./howto-restore-server-portal.md) anterior à exclusão da tabela.</span><span class="sxs-lookup"><span data-stu-id="86046-218">Click **OK** to restore the server to [restore to a point in time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="86046-219">A restauração de um servidor cria uma nova cópia do servidor, a partir do ponto no tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="86046-219">Restoring a server creates a new copy of the server, as of the point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="86046-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="86046-220">Next steps</span></span>
<span data-ttu-id="86046-221">Neste tutorial, você usará o Portal do Azure para aprender a:</span><span class="sxs-lookup"><span data-stu-id="86046-221">In this tutorial, you use the Azure portal to learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="86046-222">Criar um Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="86046-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="86046-223">Configurar o firewall do servidor</span><span class="sxs-lookup"><span data-stu-id="86046-223">Configure the server firewall</span></span>
> * <span data-ttu-id="86046-224">Usar a ferramenta de linha de comando do MySQL para criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="86046-224">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="86046-225">Carregar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="86046-225">Load sample data</span></span>
> * <span data-ttu-id="86046-226">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="86046-226">Query data</span></span>
> * <span data-ttu-id="86046-227">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="86046-227">Update data</span></span>
> * <span data-ttu-id="86046-228">Restaurar dados</span><span class="sxs-lookup"><span data-stu-id="86046-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="86046-229">Como conectar aplicativos ao Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="86046-229">How to connect applications to Azure Database for MySQL</span></span>](./howto-connection-string.md)
