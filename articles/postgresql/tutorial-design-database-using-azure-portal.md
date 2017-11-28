---
title: Projetar seu primeiro Banco de Dados do Azure para PostgreSQL usando o portal do Azure | Microsoft Docs
description: "Este tutorial mostra como tooDesign do Azure primeiro banco de dados para PostgreSQL usando Olá portal do Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: tutorial, mvc
ms.topic: tutorial
ms.date: 05/10/2017
ms.openlocfilehash: fde7e9d1ae2bad4291d18bebd3356f4f8a2ac86a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-hello-azure-portal"></a><span data-ttu-id="789f4-103">Criar seu primeiro banco de dados do Azure para PostgreSQL usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="789f4-103">Design your first Azure Database for PostgreSQL using hello Azure portal</span></span>

<span data-ttu-id="789f4-104">Banco de dados do Azure para PostgreSQL é um serviço gerenciado que permite que você toorun, gerenciar e dimensionar os bancos de dados PostgreSQL altamente disponíveis na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="789f4-104">Azure Database for PostgreSQL is a managed service that enables you toorun, manage, and scale highly available PostgreSQL databases in hello cloud.</span></span> <span data-ttu-id="789f4-105">Usando Olá portal do Azure, você pode facilmente gerenciar seu servidor e criar um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="789f4-105">Using hello Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="789f4-106">Neste tutorial, você usar Olá toolearn portal do Azure como para:</span><span class="sxs-lookup"><span data-stu-id="789f4-106">In this tutorial, you use hello Azure portal toolearn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="789f4-107">Criar um Banco de Dados do Azure para o PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="789f4-107">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="789f4-108">Configurar o firewall do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="789f4-108">Configure hello server firewall</span></span>
> * <span data-ttu-id="789f4-109">Use [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate utilitário um banco de dados</span><span class="sxs-lookup"><span data-stu-id="789f4-109">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="789f4-110">Carregar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="789f4-110">Load sample data</span></span>
> * <span data-ttu-id="789f4-111">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="789f4-111">Query data</span></span>
> * <span data-ttu-id="789f4-112">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="789f4-112">Update data</span></span>
> * <span data-ttu-id="789f4-113">Restaurar dados</span><span class="sxs-lookup"><span data-stu-id="789f4-113">Restore data</span></span>

## <a name="prerequisites"></a><span data-ttu-id="789f4-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="789f4-114">Prerequisites</span></span>
<span data-ttu-id="789f4-115">Se você não tiver uma assinatura do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="789f4-115">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="789f4-116">Faça logon no toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="789f4-116">Log in toohello Azure portal</span></span>
<span data-ttu-id="789f4-117">Faça logon no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="789f4-117">Log in toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-postgresql"></a><span data-ttu-id="789f4-118">Criar um Banco de Dados do Azure para o PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="789f4-118">Create an Azure Database for PostgreSQL</span></span>

<span data-ttu-id="789f4-119">Um Banco de Dados do Azure para PostgreSQL é criado com um conjunto definido de [recursos de computação e armazenamento](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="789f4-119">An Azure Database for PostgreSQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="789f4-120">Olá servidor será criado dentro de um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="789f4-120">hello server is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="789f4-121">Siga essas toocreate etapas um banco de dados do Azure para o servidor PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="789f4-121">Follow these steps toocreate an Azure Database for PostgreSQL server:</span></span>
1.  <span data-ttu-id="789f4-122">Clique em Olá **+ novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="789f4-122">Click hello **+ New**  button found on hello upper left-hand corner of hello Azure portal.</span></span>
2.  <span data-ttu-id="789f4-123">Selecione **bancos de dados** de saudação **novo** página e selecione **banco de dados do Azure para PostgreSQL** de saudação **bancos de dados** página.</span><span class="sxs-lookup"><span data-stu-id="789f4-123">Select **Databases** from hello **New** page, and select **Azure Database for PostgreSQL** from hello **Databases** page.</span></span>
 <span data-ttu-id="789f4-124">![Banco de dados do Azure para PostgreSQL - criar o banco de dados de saudação](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span><span class="sxs-lookup"><span data-stu-id="789f4-124">![Azure Database for PostgreSQL - Create hello database](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span></span>

3.  <span data-ttu-id="789f4-125">Preencha novo formulário de detalhes de servidor Olá com hello seguintes informações, conforme mostrado na saudação anterior imagem:</span><span class="sxs-lookup"><span data-stu-id="789f4-125">Fill out hello new server details form with hello following information, as shown on hello preceding image:</span></span>
    - <span data-ttu-id="789f4-126">Nome do servidor: **mypgserver 20170401** (o nome de um servidor mapeia o nome tooDNS e, portanto, é necessário toobe globalmente exclusivo)</span><span class="sxs-lookup"><span data-stu-id="789f4-126">Server name: **mypgserver-20170401** (name of a server maps tooDNS name and is thus required toobe globally unique)</span></span> 
    - <span data-ttu-id="789f4-127">Assinatura: Se você tiver várias assinaturas, escolha assinatura de saudação apropriado no qual o recurso de saudação existe ou é cobrado por.</span><span class="sxs-lookup"><span data-stu-id="789f4-127">Subscription: If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span>
    - <span data-ttu-id="789f4-128">Grupo de recursos: **myresourcegroup**</span><span class="sxs-lookup"><span data-stu-id="789f4-128">Resource group: **myresourcegroup**</span></span>
    - <span data-ttu-id="789f4-129">Logon e senha de administrador do servidor à sua escolha</span><span class="sxs-lookup"><span data-stu-id="789f4-129">Server admin login and password of your choice</span></span>
    - <span data-ttu-id="789f4-130">Local</span><span class="sxs-lookup"><span data-stu-id="789f4-130">Location</span></span>
    - <span data-ttu-id="789f4-131">Versão do PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="789f4-131">PostgreSQL Version</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="789f4-132">Olá administrador logon e senha que você especificar aqui são toolog necessária no servidor de toohello e seus bancos de dados mais tarde nesse início rápido.</span><span class="sxs-lookup"><span data-stu-id="789f4-132">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="789f4-133">Lembre-se ou registre essas informações para o uso posterior.</span><span class="sxs-lookup"><span data-stu-id="789f4-133">Remember or record this information for later use.</span></span>

4.  <span data-ttu-id="789f4-134">Clique em **preço** toospecify Olá desempenho e da camada de nível de serviço para o novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="789f4-134">Click **Pricing tier** toospecify hello service tier and performance level for your new database.</span></span> <span data-ttu-id="789f4-135">Para esse início rápido, selecione a camada **Básica**, **50 Unidades de Computação** e **50 GB** de armazenamento incluído.</span><span class="sxs-lookup"><span data-stu-id="789f4-135">For this quick start, select **Basic** Tier, **50 Compute Units** and **50 GB** of included storage.</span></span>
 <span data-ttu-id="789f4-136">![Banco de dados do Azure para PostgreSQL - camada de serviço pick Olá](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span><span class="sxs-lookup"><span data-stu-id="789f4-136">![Azure Database for PostgreSQL - pick hello service tier](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span></span>
5.  <span data-ttu-id="789f4-137">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="789f4-137">Click **Ok**.</span></span>
6.  <span data-ttu-id="789f4-138">Clique em **criar** tooprovision servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="789f4-138">Click **Create** tooprovision hello server.</span></span> <span data-ttu-id="789f4-139">O provisionamento demora alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="789f4-139">Provisioning takes a few minutes.</span></span>

  > [!TIP]
  > <span data-ttu-id="789f4-140">Verificar Olá **toodashboard Pin** opção tooallow facilidade no rastreamento de suas implantações.</span><span class="sxs-lookup"><span data-stu-id="789f4-140">Check hello **Pin toodashboard** option tooallow easy tracking of your deployments.</span></span>

7.  <span data-ttu-id="789f4-141">Na barra de ferramentas hello, clique em **notificações** toomonitor processo de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="789f4-141">On hello toolbar, click **Notifications** toomonitor hello deployment process.</span></span>
 <span data-ttu-id="789f4-142">![Banco de Dados do Azure para PostgreSQL – Ver notificações](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span><span class="sxs-lookup"><span data-stu-id="789f4-142">![Azure Database for PostgreSQL - See notifications](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span></span>
   
  <span data-ttu-id="789f4-143">Por padrão, o banco de dados **postgres** é criado em seu servidor.</span><span class="sxs-lookup"><span data-stu-id="789f4-143">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="789f4-144">Olá [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) banco de dados é um banco de dados padrão devem ser usados pelos usuários, utilitários e aplicativos de terceiros.</span><span class="sxs-lookup"><span data-stu-id="789f4-144">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 

## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="789f4-145">Configurar uma regra de firewall no nível de servidor</span><span class="sxs-lookup"><span data-stu-id="789f4-145">Configure a server-level firewall rule</span></span>

<span data-ttu-id="789f4-146">saudação de banco de dados PostgreSQL serviço cria um firewall no nível de servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="789f4-146">hello Azure Database for PostgreSQL service creates a firewall at hello server-level.</span></span> <span data-ttu-id="789f4-147">Esse firewall impede que aplicativos externos e ferramentas conectando toohello server e bancos de dados no servidor de saudação, a menos que uma regra de firewall será criada tooopen firewall de saudação para endereços IP específicos.</span><span class="sxs-lookup"><span data-stu-id="789f4-147">This firewall prevents external applications and tools from connecting toohello server and any databases on hello server unless a firewall rule is created tooopen hello firewall for specific IP addresses.</span></span> 

1.  <span data-ttu-id="789f4-148">Após a conclusão da implantação hello, clique em **todos os recursos** do menu esquerdo hello e digite o nome de saudação **mypgserver 20170401** toosearch para seu servidor recém-criado.</span><span class="sxs-lookup"><span data-stu-id="789f4-148">After hello deployment completes, click **All Resources** from hello left-hand menu and type in hello name **mypgserver-20170401** toosearch for your newly created server.</span></span> <span data-ttu-id="789f4-149">Clique em nome do servidor de saudação listado no resultado da pesquisa hello.</span><span class="sxs-lookup"><span data-stu-id="789f4-149">Click hello server name listed in hello search result.</span></span> <span data-ttu-id="789f4-150">Olá **visão geral** página para o servidor é aberta e oferece opções de configuração adicional.</span><span class="sxs-lookup"><span data-stu-id="789f4-150">hello **Overview** page for your server opens and provides options for further configuration.</span></span>
 
 ![<span data-ttu-id="789f4-151">Banco de Dados do Azure para PostgreSQL – Pesquisar o servidor</span><span class="sxs-lookup"><span data-stu-id="789f4-151">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

2.  <span data-ttu-id="789f4-152">Na folha do servidor de saudação, selecione **segurança de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="789f4-152">In hello server blade, select **Connection Security**.</span></span> 
3.  <span data-ttu-id="789f4-153">Clique na caixa de texto de saudação em **nome da regra,** e adicione um novo firewall regra toowhitelist Olá intervalo IP para conectividade.</span><span class="sxs-lookup"><span data-stu-id="789f4-153">Click in hello text box under **Rule Name,** and add a new firewall rule toowhitelist hello IP range for connectivity.</span></span> <span data-ttu-id="789f4-154">Para este tutorial, vamos permitir todos os IPs digitando **Nome da regra = PermitirTodosIps**, **IP inicial = 0.0.0.0** e **IP final = 255.255.255.255** e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="789f4-154">For this tutorial, let's allow all IPs by typing in **Rule Name = AllowAllIps**, **Start IP = 0.0.0.0** and **End IP = 255.255.255.255** and then click **Save**.</span></span> <span data-ttu-id="789f4-155">Você pode definir uma regra de firewall que abrange um tooconnect IP intervalo toobe capaz de sua rede.</span><span class="sxs-lookup"><span data-stu-id="789f4-155">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span>
 
 ![Banco de Dados do Azure para PostgreSQL – Criar regra de firewall](./media/tutorial-design-database-using-azure-portal/5-firewall-2.png)

4.  <span data-ttu-id="789f4-157">Clique em **salvar** e, em seguida, clique em Olá **X** tooclose Olá **conexões segurança** página.</span><span class="sxs-lookup"><span data-stu-id="789f4-157">Click **Save** and then click hello **X** tooclose hello **Connections Security** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="789f4-158">O servidor PostgreSQL do Azure se comunica pela porta 5432.</span><span class="sxs-lookup"><span data-stu-id="789f4-158">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="789f4-159">Se você estiver tentando tooconnect de dentro de uma rede corporativa, o tráfego de saída pela porta 5432 talvez não consigam pelo firewall da rede.</span><span class="sxs-lookup"><span data-stu-id="789f4-159">If you are trying tooconnect from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="789f4-160">Nesse caso, não será tooconnect capaz de servidor de banco de dados SQL de tooyour, a menos que o departamento de TI abre a porta 5432.</span><span class="sxs-lookup"><span data-stu-id="789f4-160">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 5432.</span></span>
  >


## <a name="get-hello-connection-information"></a><span data-ttu-id="789f4-161">Obter informações de conexão Olá</span><span class="sxs-lookup"><span data-stu-id="789f4-161">Get hello connection information</span></span>

<span data-ttu-id="789f4-162">Quando criamos nosso banco de dados do Azure para o servidor PostgreSQL, Olá padrão **postgres** banco de dados também é criado.</span><span class="sxs-lookup"><span data-stu-id="789f4-162">When we created our Azure Database for PostgreSQL server, hello default **postgres** database also gets created.</span></span> <span data-ttu-id="789f4-163">servidor de banco de dados de tooyour tooconnect, é necessário tooprovide credenciais de acesso e informações do host.</span><span class="sxs-lookup"><span data-stu-id="789f4-163">tooconnect tooyour database server, you need tooprovide host information and access credentials.</span></span>

1. <span data-ttu-id="789f4-164">No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e procure o servidor de saudação que você acabou de criar **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="789f4-164">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you just created **mypgserver-20170401**.</span></span>

  ![<span data-ttu-id="789f4-165">Banco de Dados do Azure para PostgreSQL – Pesquisar o servidor</span><span class="sxs-lookup"><span data-stu-id="789f4-165">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

3. <span data-ttu-id="789f4-166">Clique em nome do servidor de saudação **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="789f4-166">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="789f4-167">Servidor de saudação selecione **visão geral** página.</span><span class="sxs-lookup"><span data-stu-id="789f4-167">Select hello server's **Overview** page.</span></span> <span data-ttu-id="789f4-168">Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="789f4-168">Make a note of hello **Server name** and **Server admin login name**.</span></span>

 ![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/tutorial-design-database-using-azure-portal/6-server-name.png)


## <a name="connect-toopostgresql-database-using-psql-in-cloud-shell"></a><span data-ttu-id="789f4-170">Conecte-se o banco de dados de tooPostgreSQL usando psql no Shell de nuvem</span><span class="sxs-lookup"><span data-stu-id="789f4-170">Connect tooPostgreSQL database using psql in Cloud Shell</span></span>

<span data-ttu-id="789f4-171">Agora vamos usar Olá psql utilitário de linha de comando tooconnect toohello banco de dados para o servidor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="789f4-171">Let's now use hello psql command-line utility tooconnect toohello Azure Database for PostgreSQL server.</span></span> 
1. <span data-ttu-id="789f4-172">Inicie Olá Shell de nuvem do Azure através do ícone de terminal no painel de navegação superior Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="789f4-172">Launch hello Azure Cloud Shell via hello terminal icon on hello top navigation pane.</span></span>

   ![Banco de Dados do Azure para PostgreSQL – Ícone do terminal do Azure Cloud Shell](./media/tutorial-design-database-using-azure-portal/7-cloud-shell.png)

2. <span data-ttu-id="789f4-174">Olá Shell de nuvem do Azure é aberto no navegador, permitindo que você tootype bash comandos.</span><span class="sxs-lookup"><span data-stu-id="789f4-174">hello Azure Cloud Shell opens in your browser, enabling you tootype bash commands.</span></span>

   ![Banco de Dados do Azure para PostgreSQL – Prompt de bash do Azure Shell](./media/tutorial-design-database-using-azure-portal/8-bash.png)

3. <span data-ttu-id="789f4-176">No prompt de Shell de nuvem hello, conecte-se tooyour banco de dados para o servidor PostgreSQL usando Olá psql comandos.</span><span class="sxs-lookup"><span data-stu-id="789f4-176">At hello Cloud Shell prompt, connect tooyour Azure Database for PostgreSQL server using hello psql commands.</span></span> <span data-ttu-id="789f4-177">Olá, formato a seguir é usado tooconnect tooan banco de dados para o servidor PostgreSQL com hello [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilitário:</span><span class="sxs-lookup"><span data-stu-id="789f4-177">hello following format is used tooconnect tooan Azure Database for PostgreSQL server with hello [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility:</span></span>
   ```bash
   psql --host=<myserver> --port=<port> --username=<server admin login> --dbname=<database name>
   ```

   <span data-ttu-id="789f4-178">Por exemplo, Olá comando a seguir conecta o banco de dados padrão toohello chamado **postgres** no seu servidor PostgreSQL **mypgserver 20170401.postgres.database.azure.com** usando as credenciais de acesso.</span><span class="sxs-lookup"><span data-stu-id="789f4-178">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="789f4-179">Insira a senha de administrador do servidor quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="789f4-179">Enter your server admin password when prompted.</span></span>

   ```bash
   psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
   ```

## <a name="create-a-new-database"></a><span data-ttu-id="789f4-180">Criar um novo banco de dados</span><span class="sxs-lookup"><span data-stu-id="789f4-180">Create a New Database</span></span>
<span data-ttu-id="789f4-181">Quando estiver conectado toohello server, crie um banco de dados em branco no prompt de saudação.</span><span class="sxs-lookup"><span data-stu-id="789f4-181">Once you're connected toohello server, create a blank database at hello prompt.</span></span>
```bash
CREATE DATABASE mypgsqldb;
```

<span data-ttu-id="789f4-182">No prompt de hello, execute Olá após o banco de dados do comando tooswitch conexão toohello recém-criado **mypgsqldb**.</span><span class="sxs-lookup"><span data-stu-id="789f4-182">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**.</span></span>
```bash
\c mypgsqldb
```
## <a name="create-tables-in-hello-database"></a><span data-ttu-id="789f4-183">Criar tabelas no banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="789f4-183">Create tables in hello database</span></span>
<span data-ttu-id="789f4-184">Agora que você sabe como tooconnect toohello banco de dados do Azure para PostgreSQL, podemos ir como toocomplete algumas tarefas básicas.</span><span class="sxs-lookup"><span data-stu-id="789f4-184">Now that you know how tooconnect toohello Azure Database for PostgreSQL, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="789f4-185">Primeiro, criamos uma tabela e a carregamos com alguns dados.</span><span class="sxs-lookup"><span data-stu-id="789f4-185">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="789f4-186">Vamos criar uma tabela que rastreia informações de inventário.</span><span class="sxs-lookup"><span data-stu-id="789f4-186">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="789f4-187">Você pode ver Olá recém-criado tabela na lista de saudação do tabvles agora digitando:</span><span class="sxs-lookup"><span data-stu-id="789f4-187">You can see hello newly created table in hello list of tabvles now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="789f4-188">Carregar dados em tabelas de saudação</span><span class="sxs-lookup"><span data-stu-id="789f4-188">Load data into hello tables</span></span>
<span data-ttu-id="789f4-189">Agora que temos uma tabela, podemos inserir alguns dados nela.</span><span class="sxs-lookup"><span data-stu-id="789f4-189">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="789f4-190">Na janela de prompt de comando aberta hello, executar Olá tooinsert de consulta a seguir algumas linhas de dados</span><span class="sxs-lookup"><span data-stu-id="789f4-190">At hello open command prompt window, run hello following query tooinsert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="789f4-191">Você tem agora duas linhas de dados de exemplo na tabela de saudação criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="789f4-191">You have now two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="789f4-192">Consultar e atualizar dados Olá nas tabelas de saudação</span><span class="sxs-lookup"><span data-stu-id="789f4-192">Query and update hello data in hello tables</span></span>
<span data-ttu-id="789f4-193">Execute Olá consultar tooretrieve informações a seguir da tabela de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="789f4-193">Execute hello following query tooretrieve information from hello database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="789f4-194">Você também pode atualizar dados Olá nas tabelas de saudação</span><span class="sxs-lookup"><span data-stu-id="789f4-194">You can also update hello data in hello tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="789f4-195">linha de saudação obtém atualizada quando você recuperar dados.</span><span class="sxs-lookup"><span data-stu-id="789f4-195">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-data-tooa-previous-point-in-time"></a><span data-ttu-id="789f4-196">Restaurar ponto de tooa de dados anterior no tempo</span><span class="sxs-lookup"><span data-stu-id="789f4-196">Restore data tooa previous point in time</span></span>
<span data-ttu-id="789f4-197">Imagine que você excluiu acidentalmente essa tabela.</span><span class="sxs-lookup"><span data-stu-id="789f4-197">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="789f4-198">Essa situação é algo do qual você não pode se recuperar facilmente.</span><span class="sxs-lookup"><span data-stu-id="789f4-198">This situation is something you cannot easily recover from.</span></span> <span data-ttu-id="789f4-199">Banco de dados do Azure para PostgreSQL permite voltar tooany de toogo point-in-time (em Olá última too7 dias (Basic) e 35 dias (padrão)) e restaurar esse point-in-time tooa novo servidor.</span><span class="sxs-lookup"><span data-stu-id="789f4-199">Azure Database for PostgreSQL allows you toogo back tooany point-in-time (in hello last up too7 days (Basic) and 35 days (Standard)) and restore this point-in-time tooa new server.</span></span> <span data-ttu-id="789f4-200">Você pode usar esse novo toorecover de servidor os dados excluídos.</span><span class="sxs-lookup"><span data-stu-id="789f4-200">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="789f4-201">Olá etapas Olá exemplo server tooa ponto de restauração da seguir antes de saudação tabela foi adicionada.</span><span class="sxs-lookup"><span data-stu-id="789f4-201">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

1.  <span data-ttu-id="789f4-202">No banco de dados do Azure Olá PostgreSQL página para o servidor, clique em **restaurar** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="789f4-202">On hello Azure Database for PostgreSQL page for your server, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="789f4-203">Olá **restaurar** página será aberta.</span><span class="sxs-lookup"><span data-stu-id="789f4-203">hello **Restore** page opens.</span></span>
  <span data-ttu-id="789f4-204">![Portal do Azure - Opções do formulário de restauração](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span><span class="sxs-lookup"><span data-stu-id="789f4-204">![Azure portal - Restore form options](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span></span>
2.  <span data-ttu-id="789f4-205">Preencha Olá **restaurar** formulário com informações de saudação necessários:</span><span class="sxs-lookup"><span data-stu-id="789f4-205">Fill out hello **Restore** form with hello required information:</span></span>

  ![Portal do Azure - Opções do formulário de restauração](./media/tutorial-design-database-using-azure-portal/10-azure-portal-restore.png)
  - <span data-ttu-id="789f4-207">**Ponto de restauração**: selecione um point-in-time que ocorre antes que o servidor de saudação foi alterado</span><span class="sxs-lookup"><span data-stu-id="789f4-207">**Restore point**: Select a point-in-time that occurs before hello server was changed</span></span>
  - <span data-ttu-id="789f4-208">**Servidor de destino**: forneça um novo nome de servidor que você deseja toorestore para</span><span class="sxs-lookup"><span data-stu-id="789f4-208">**Target server**: Provide a new server name you want toorestore to</span></span>
  - <span data-ttu-id="789f4-209">**Local**: não é possível selecionar região hello, por padrão, ele é igual ao servidor de origem Olá</span><span class="sxs-lookup"><span data-stu-id="789f4-209">**Location**: You cannot select hello region, by default it is same as hello source server</span></span>
  - <span data-ttu-id="789f4-210">**Tipo de preço**: não é possível alterar esse valor ao restaurar um servidor.</span><span class="sxs-lookup"><span data-stu-id="789f4-210">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="789f4-211">É igual ao servidor de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="789f4-211">It is same as hello source server.</span></span> 
3.  <span data-ttu-id="789f4-212">Clique em **Okey** toorestore Olá servidor muito[restauração point-in-time tooa](./howto-restore-server-portal.md) antes de tabelas de saudação foi excluído.</span><span class="sxs-lookup"><span data-stu-id="789f4-212">Click **OK** toorestore hello server too[restore tooa point-in-time](./howto-restore-server-portal.md) before hello tables was deleted.</span></span> <span data-ttu-id="789f4-213">Restaurar o servidor tooa outro ponto no tempo cria um duplicado novo servidor como servidor de saudação original como de saudação ponto no tempo especificado, desde que está dentro do período de retenção de saudação de seu [camada de serviço](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="789f4-213">Restoring a server tooa different point in time creates a duplicate new server as hello original server as of hello point in time you specify, provided that it is within hello retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="789f4-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="789f4-214">Next Steps</span></span>
<span data-ttu-id="789f4-215">Neste tutorial, você aprendeu como toouse Olá portal do Azure e outros utilitários para:</span><span class="sxs-lookup"><span data-stu-id="789f4-215">In this tutorial, you learned how toouse hello Azure portal and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="789f4-216">Criar um Banco de Dados do Azure para o PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="789f4-216">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="789f4-217">Configurar o firewall do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="789f4-217">Configure hello server firewall</span></span>
> * <span data-ttu-id="789f4-218">Use [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate utilitário um banco de dados</span><span class="sxs-lookup"><span data-stu-id="789f4-218">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="789f4-219">Carregar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="789f4-219">Load sample data</span></span>
> * <span data-ttu-id="789f4-220">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="789f4-220">Query data</span></span>
> * <span data-ttu-id="789f4-221">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="789f4-221">Update data</span></span>
> * <span data-ttu-id="789f4-222">Restaurar dados</span><span class="sxs-lookup"><span data-stu-id="789f4-222">Restore data</span></span>

<span data-ttu-id="789f4-223">Em seguida, Aprenda como tarefas semelhantes do toouse CLI do Azure toodo, examine este tutorial: [criar seu primeiro banco de dados do Azure para PostgreSQL usando a CLI do Azure](tutorial-design-database-using-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="789f4-223">Next, learn how toouse Azure CLI toodo similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using Azure CLI](tutorial-design-database-using-azure-cli.md)</span></span>
