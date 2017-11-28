---
title: "TooAzure banco de dados de conexão para MySQL do MySQL Workbench | Microsoft Docs"
description: "Este guia de início rápido fornece Olá etapas toouse MySQL Workbench tooconnect e consultar dados do banco de dados do Azure para MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a><span data-ttu-id="ca96b-103">Banco de dados do Azure para MySQL: Use MySQL Workbench tooconnect e consultar dados</span><span class="sxs-lookup"><span data-stu-id="ca96b-103">Azure Database for MySQL: Use MySQL Workbench tooconnect and query data</span></span>
<span data-ttu-id="ca96b-104">Este guia de início rápido demonstra como tooconnect tooan banco de dados do Azure para MySQL usando Olá aplicativo Workbench do MySQL.</span><span class="sxs-lookup"><span data-stu-id="ca96b-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using hello MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ca96b-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ca96b-105">Prerequisites</span></span>
<span data-ttu-id="ca96b-106">Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="ca96b-106">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="ca96b-107">Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ca96b-107">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="ca96b-108">Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ca96b-108">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a><span data-ttu-id="ca96b-109">Instalar o MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="ca96b-109">Install MySQL Workbench</span></span>
<span data-ttu-id="ca96b-110">Baixar e instalar o Workbench do MySQL no seu computador de [site do MySQL Olá](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="ca96b-110">Download and install MySQL Workbench on your computer from [hello MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="ca96b-111">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="ca96b-111">Get connection information</span></span>
<span data-ttu-id="ca96b-112">Obter Olá conexão informações necessárias tooconnect toohello banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="ca96b-112">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="ca96b-113">Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="ca96b-113">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="ca96b-114">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ca96b-114">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="ca96b-115">No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e pesquisa para o servidor de saudação que você criou, como **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="ca96b-115">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>

3. <span data-ttu-id="ca96b-116">Clique em nome do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca96b-116">Click hello server name.</span></span>

4. <span data-ttu-id="ca96b-117">Servidor de saudação selecione **propriedades** página.</span><span class="sxs-lookup"><span data-stu-id="ca96b-117">Select hello server's **Properties** page.</span></span> <span data-ttu-id="ca96b-118">Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="ca96b-118">Make a note of hello **Server name** and **Server admin login name**.</span></span>

 ![Nome do servidor do Banco de Dados do Azure para MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. <span data-ttu-id="ca96b-120">Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.</span><span class="sxs-lookup"><span data-stu-id="ca96b-120">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-toohello-server-using-mysql-workbench"></a><span data-ttu-id="ca96b-121">Conectar-se a servidor toohello usando o Workbench do MySQL</span><span class="sxs-lookup"><span data-stu-id="ca96b-121">Connect toohello server using MySQL Workbench</span></span> 
<span data-ttu-id="ca96b-122">tooconnect tooAzure MySQL server usando a ferramenta de saudação GUI MySQL Workbench:</span><span class="sxs-lookup"><span data-stu-id="ca96b-122">tooconnect tooAzure MySQL server using hello GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="ca96b-123">Inicie Olá aplicativo MySQL Workbench no seu computador.</span><span class="sxs-lookup"><span data-stu-id="ca96b-123">Launch hello MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="ca96b-124">Em **Conexão nova instalação** caixa de diálogo, digite Olá seguintes informações sobre Olá **parâmetros** guia:</span><span class="sxs-lookup"><span data-stu-id="ca96b-124">In **Setup New Connection** dialog box, enter hello following information on hello **Parameters** tab:</span></span>

    ![configurar nova conexão](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="ca96b-126">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="ca96b-126">**Setting**</span></span> | <span data-ttu-id="ca96b-127">**Valor sugerido**</span><span class="sxs-lookup"><span data-stu-id="ca96b-127">**Suggested value**</span></span> | <span data-ttu-id="ca96b-128">**Descrição do campo**</span><span class="sxs-lookup"><span data-stu-id="ca96b-128">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="ca96b-129">Nome da Conexão</span><span class="sxs-lookup"><span data-stu-id="ca96b-129">Connection Name</span></span> | <span data-ttu-id="ca96b-130">Conexão de demonstração</span><span class="sxs-lookup"><span data-stu-id="ca96b-130">Demo Connection</span></span> | <span data-ttu-id="ca96b-131">Especifique um rótulo para essa conexão.</span><span class="sxs-lookup"><span data-stu-id="ca96b-131">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="ca96b-132">Método de Conexão</span><span class="sxs-lookup"><span data-stu-id="ca96b-132">Connection Method</span></span> | <span data-ttu-id="ca96b-133">Padrão (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="ca96b-133">Standard (TCP/IP)</span></span> | <span data-ttu-id="ca96b-134">Padrão (TCP/IP) é suficiente.</span><span class="sxs-lookup"><span data-stu-id="ca96b-134">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="ca96b-135">Nome do host</span><span class="sxs-lookup"><span data-stu-id="ca96b-135">Hostname</span></span> | <span data-ttu-id="ca96b-136">*nome do servidor*</span><span class="sxs-lookup"><span data-stu-id="ca96b-136">*server name*</span></span> | <span data-ttu-id="ca96b-137">Especifique o valor de nome de servidor de saudação que foi usado quando você criou Olá banco de dados do Azure para MySQL anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ca96b-137">Specify hello server name value that was used when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="ca96b-138">Nosso servidor de exemplo mostrado é myserver4demo.mysql.database.azure.com. Use o nome de domínio totalmente qualificado hello (\*. mysql.database.azure.com) conforme mostrado no exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="ca96b-138">Our example server shown is myserver4demo.mysql.database.azure.com. Use hello fully qualified domain name (\*.mysql.database.azure.com) as shown in hello example.</span></span> <span data-ttu-id="ca96b-139">Siga etapas Olá Olá seção tooget Olá conexão as informações anteriores se você não lembrar o nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="ca96b-139">Follow hello steps in hello previous section tooget hello connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="ca96b-140">Porta</span><span class="sxs-lookup"><span data-stu-id="ca96b-140">Port</span></span> | <span data-ttu-id="ca96b-141">3306</span><span class="sxs-lookup"><span data-stu-id="ca96b-141">3306</span></span> | <span data-ttu-id="ca96b-142">Sempre use a porta 3306 durante a conexão tooAzure banco de dados para MySQL.</span><span class="sxs-lookup"><span data-stu-id="ca96b-142">Always use port 3306 when connecting tooAzure Database for MySQL.</span></span> |
    | <span data-ttu-id="ca96b-143">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ca96b-143">Username</span></span> |  <span data-ttu-id="ca96b-144">*nome de logon do administrador do servidor*</span><span class="sxs-lookup"><span data-stu-id="ca96b-144">*server admin login name*</span></span> | <span data-ttu-id="ca96b-145">Digite hello servidor admin logon nome de usuário fornecido quando você criou Olá banco de dados do Azure para MySQL anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ca96b-145">Type in hello server admin login username supplied when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="ca96b-146">Nosso nome de usuário de exemplo é myadmin@myserver4demo.</span><span class="sxs-lookup"><span data-stu-id="ca96b-146">Our example username is myadmin@myserver4demo.</span></span> <span data-ttu-id="ca96b-147">Siga etapas Olá Olá seção tooget Olá conexão as informações anteriores se não lembrar o nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca96b-147">Follow hello steps in hello previous section tooget hello connection information if you do not remember hello username.</span></span> <span data-ttu-id="ca96b-148">formato de saudação é  *username@servername* .</span><span class="sxs-lookup"><span data-stu-id="ca96b-148">hello format is *username@servername*.</span></span>
    | <span data-ttu-id="ca96b-149">Senha</span><span class="sxs-lookup"><span data-stu-id="ca96b-149">Password</span></span> | <span data-ttu-id="ca96b-150">sua senha</span><span class="sxs-lookup"><span data-stu-id="ca96b-150">your password</span></span> | <span data-ttu-id="ca96b-151">Clique em **repositório no cofre...**  senha de saudação do botão toosave.</span><span class="sxs-lookup"><span data-stu-id="ca96b-151">Click **Store in Vault...** button toosave hello password.</span></span> |

3.   <span data-ttu-id="ca96b-152">Clique em **Conexão de teste** tootest se todos os parâmetros estão configurados corretamente.</span><span class="sxs-lookup"><span data-stu-id="ca96b-152">Click **Test Connection** tootest if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="ca96b-153">Clique em **Okey** toosave conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca96b-153">Click **OK** toosave hello connection.</span></span> 

5.   <span data-ttu-id="ca96b-154">Na listagem de saudação do **conexão MySQL**, clique em Olá bloco correspondente tooyour servidor e aguarde Olá toobe de conexão estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ca96b-154">In hello listing of **MySQL Connections**, click hello tile corresponding tooyour server and wait for hello connection toobe established.</span></span>

6.   <span data-ttu-id="ca96b-155">Uma nova guia do SQL é aberta, com um editor em branco no qual você pode digitar suas consultas.</span><span class="sxs-lookup"><span data-stu-id="ca96b-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca96b-156">Por padrão, a segurança da conexão SSL é exigida e imposta no seu Banco de Dados do Azure para o servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="ca96b-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="ca96b-157">Normalmente, nenhuma configuração adicional com certificados SSL é necessária para MySQL Workbench tooconnect tooyour servidor.</span><span class="sxs-lookup"><span data-stu-id="ca96b-157">Typically no additional configuration with SSL certificates is required for MySQL Workbench tooconnect tooyour server.</span></span> <span data-ttu-id="ca96b-158">Para obter mais informações sobre o SSL, consulte [conectividade de configurar SSL em seu aplicativo toosecurely tooAzure banco de dados de conexão para MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="ca96b-158">For more information on SSL, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="ca96b-159">Se você precisar toodisable SSL, visite Olá portal do Azure e clique em Olá Conexão segurança página toodisable Olá impor SSL conexão botão de alternância.</span><span class="sxs-lookup"><span data-stu-id="ca96b-159">If you need toodisable SSL, visit hello Azure portal and click hello Connection security page toodisable hello Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="ca96b-160">Criar uma tabela, inserir dados, ler dados, atualizar dados, excluir dados</span><span class="sxs-lookup"><span data-stu-id="ca96b-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="ca96b-161">Copie e cole o código SQL de exemplo hello um tooillustrate de guia do SQL em branco alguns dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="ca96b-161">Copy and paste hello sample SQL code into a blank SQL tab tooillustrate some sample data.</span></span>

    <span data-ttu-id="ca96b-162">Esse código cria um banco de dados vazio chamado quickstartdb e, em seguida, cria uma tabela de exemplo chamada inventory.</span><span class="sxs-lookup"><span data-stu-id="ca96b-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="ca96b-163">Insere linhas, em seguida, lê as linhas de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca96b-163">It inserts some rows, then reads hello rows.</span></span> <span data-ttu-id="ca96b-164">Altera dados Olá com uma instrução update e leituras Olá linhas novamente.</span><span class="sxs-lookup"><span data-stu-id="ca96b-164">It changes hello data with an update statement, and reads hello rows again.</span></span> <span data-ttu-id="ca96b-165">Por fim exclui uma linha e lê as linhas de saudação novamente.</span><span class="sxs-lookup"><span data-stu-id="ca96b-165">Finally it deletes a row, and reads hello rows again.</span></span>
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    <span data-ttu-id="ca96b-166">saudação de captura de tela mostra um exemplo de hello código SQL na saída do SQL Workbench e hello depois que ele foi executado.</span><span class="sxs-lookup"><span data-stu-id="ca96b-166">hello screenshot shows an example of hello SQL code in SQL Workbench and hello output after it has been run.</span></span>
    
    ![Código SQL de exemplo do guia de SQL Workbench MySQL toorun](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="ca96b-168">exemplo de hello toorun código SQL, clique em Olá luminosidade ícone de raio na barra de ferramentas de saudação do hello **arquivo SQL** guia.</span><span class="sxs-lookup"><span data-stu-id="ca96b-168">toorun hello sample SQL Code, click hello lightening bolt icon in hello toolbar of hello **SQL File** tab.</span></span>
3. <span data-ttu-id="ca96b-169">Observe Olá três resultados com guias em Olá **grade de resultados** seção no meio de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca96b-169">Notice hello three tabbed results in hello **Result Grid** section in hello middle of hello page.</span></span> 
4. <span data-ttu-id="ca96b-170">Saudação de aviso **saída** lista final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="ca96b-170">Notice hello **Output** list at hello bottom of hello page.</span></span> <span data-ttu-id="ca96b-171">saudação status de cada comando é mostrado.</span><span class="sxs-lookup"><span data-stu-id="ca96b-171">hello status of each command is shown.</span></span> 

<span data-ttu-id="ca96b-172">Agora, se conectou tooAzure banco de dados para MySQL usando MySQL Workbench e tiver consultado dados usando linguagem SQL hello.</span><span class="sxs-lookup"><span data-stu-id="ca96b-172">Now, you have connected tooAzure Database for MySQL using MySQL Workbench, and have queried data using hello SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca96b-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ca96b-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ca96b-174">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="ca96b-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
