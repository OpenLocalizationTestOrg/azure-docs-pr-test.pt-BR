---
title: Conectar-se ao Banco de Dados do Azure para MySQL do MySQL Workbench | Microsoft Docs
description: "Este guia de início rápido fornece as etapas para usar o MySQL Workbench para se conectar e consultar dados do Banco de Dados do Azure para MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: 20a1f31ce42abb924504c4008f85420fc49aec89
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-to-connect-and-query-data"></a><span data-ttu-id="0a298-103">Banco de Dados do Azure para MySQL: usar o MySQL Workbench para se conectar e consultar dados</span><span class="sxs-lookup"><span data-stu-id="0a298-103">Azure Database for MySQL: Use MySQL Workbench to connect and query data</span></span>
<span data-ttu-id="0a298-104">Este guia de início rápido demonstra como se conectar a um Banco de Dados do Azure para MySQL usando o aplicativo MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="0a298-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using the MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0a298-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0a298-105">Prerequisites</span></span>
<span data-ttu-id="0a298-106">Este guia de início rápido usa os recursos criados em um destes guias como ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="0a298-106">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="0a298-107">Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0a298-107">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="0a298-108">Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0a298-108">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a><span data-ttu-id="0a298-109">Instalar o MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="0a298-109">Install MySQL Workbench</span></span>
<span data-ttu-id="0a298-110">Baixe e instale o MySQL Workbench em seu computador e do [site do MySQL](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="0a298-110">Download and install MySQL Workbench on your computer from [the MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="0a298-111">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="0a298-111">Get connection information</span></span>
<span data-ttu-id="0a298-112">Obtenha as informações de conexão necessárias para se conectar ao Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="0a298-112">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="0a298-113">Você precisa das credenciais de logon e do nome do servidor totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="0a298-113">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="0a298-114">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0a298-114">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="0a298-115">No menu à esquerda no Portal do Azure, clique em **Todos os recursos** e pesquise pelo servidor que você criou, como **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="0a298-115">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>

3. <span data-ttu-id="0a298-116">Clique no nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="0a298-116">Click the server name.</span></span>

4. <span data-ttu-id="0a298-117">Selecione a página **Propriedades** do servidor.</span><span class="sxs-lookup"><span data-stu-id="0a298-117">Select the server's **Properties** page.</span></span> <span data-ttu-id="0a298-118">Anote o **Nome do servidor** e o **Nome de logon de administrador do servidor**.</span><span class="sxs-lookup"><span data-stu-id="0a298-118">Make a note of the **Server name** and **Server admin login name**.</span></span>

 ![Nome do servidor do Banco de Dados do Azure para MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. <span data-ttu-id="0a298-120">Se você se esquecer das informações de logon do servidor, navegue até a página **Visão Geral** para exibir o nome de logon do Administrador do servidor e, se necessário, redefinir a senha.</span><span class="sxs-lookup"><span data-stu-id="0a298-120">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-to-the-server-using-mysql-workbench"></a><span data-ttu-id="0a298-121">Conectar-se ao servidor usando MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="0a298-121">Connect to the server using MySQL Workbench</span></span> 
<span data-ttu-id="0a298-122">Para se conectar ao servidor MySQL do Azure usando a ferramenta de GUI MySQL Workbench:</span><span class="sxs-lookup"><span data-stu-id="0a298-122">To connect to Azure MySQL server using the GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="0a298-123">Inicie o aplicativo MySQL Workbench em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0a298-123">Launch the MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="0a298-124">Na caixa de diálogo **Configurar Nova Conexão**, insira as seguintes informações na guia **Parâmetros**:</span><span class="sxs-lookup"><span data-stu-id="0a298-124">In **Setup New Connection** dialog box, enter the following information on the **Parameters** tab:</span></span>

    ![configurar nova conexão](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="0a298-126">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="0a298-126">**Setting**</span></span> | <span data-ttu-id="0a298-127">**Valor sugerido**</span><span class="sxs-lookup"><span data-stu-id="0a298-127">**Suggested value**</span></span> | <span data-ttu-id="0a298-128">**Descrição do campo**</span><span class="sxs-lookup"><span data-stu-id="0a298-128">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="0a298-129">Nome da Conexão</span><span class="sxs-lookup"><span data-stu-id="0a298-129">Connection Name</span></span> | <span data-ttu-id="0a298-130">Conexão de demonstração</span><span class="sxs-lookup"><span data-stu-id="0a298-130">Demo Connection</span></span> | <span data-ttu-id="0a298-131">Especifique um rótulo para essa conexão.</span><span class="sxs-lookup"><span data-stu-id="0a298-131">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="0a298-132">Método de Conexão</span><span class="sxs-lookup"><span data-stu-id="0a298-132">Connection Method</span></span> | <span data-ttu-id="0a298-133">Padrão (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="0a298-133">Standard (TCP/IP)</span></span> | <span data-ttu-id="0a298-134">Padrão (TCP/IP) é suficiente.</span><span class="sxs-lookup"><span data-stu-id="0a298-134">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="0a298-135">Nome do host</span><span class="sxs-lookup"><span data-stu-id="0a298-135">Hostname</span></span> | <span data-ttu-id="0a298-136">*nome do servidor*</span><span class="sxs-lookup"><span data-stu-id="0a298-136">*server name*</span></span> | <span data-ttu-id="0a298-137">Especifique o valor do nome do servidor que foi usado quando você criou o Banco de Dados do Azure para MySQL anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0a298-137">Specify the server name value that was used when you created the Azure Database for MySQL earlier.</span></span> <span data-ttu-id="0a298-138">Nosso servidor de exemplo mostrado é myserver4demo.mysql.database.azure.com. Use o nome de domínio totalmente qualificado (\*.mysql.database.azure.com) conforme mostrado no exemplo.</span><span class="sxs-lookup"><span data-stu-id="0a298-138">Our example server shown is myserver4demo.mysql.database.azure.com. Use the fully qualified domain name (\*.mysql.database.azure.com) as shown in the example.</span></span> <span data-ttu-id="0a298-139">Siga as etapas na seção anterior para obter as informações da conexão, caso não se lembre do seu nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="0a298-139">Follow the steps in the previous section to get the connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="0a298-140">Porta</span><span class="sxs-lookup"><span data-stu-id="0a298-140">Port</span></span> | <span data-ttu-id="0a298-141">3306</span><span class="sxs-lookup"><span data-stu-id="0a298-141">3306</span></span> | <span data-ttu-id="0a298-142">Sempre use a porta 3306 ao conectar o Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="0a298-142">Always use port 3306 when connecting to Azure Database for MySQL.</span></span> |
    | <span data-ttu-id="0a298-143">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="0a298-143">Username</span></span> |  <span data-ttu-id="0a298-144">*nome de logon do administrador do servidor*</span><span class="sxs-lookup"><span data-stu-id="0a298-144">*server admin login name*</span></span> | <span data-ttu-id="0a298-145">Digite o nome de usuário de logon do administrador do servidor fornecido na criação do Banco de Dados do Azure para MySQL anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0a298-145">Type in the server admin login username supplied when you created the Azure Database for MySQL earlier.</span></span> <span data-ttu-id="0a298-146">Nosso nome de usuário de exemplo é myadmin@myserver4demo.</span><span class="sxs-lookup"><span data-stu-id="0a298-146">Our example username is myadmin@myserver4demo.</span></span> <span data-ttu-id="0a298-147">Siga as etapas na seção anterior para obter as informações da conexão, caso não se lembre do nome do usuário.</span><span class="sxs-lookup"><span data-stu-id="0a298-147">Follow the steps in the previous section to get the connection information if you do not remember the username.</span></span> <span data-ttu-id="0a298-148">O formato é *username@servername*.</span><span class="sxs-lookup"><span data-stu-id="0a298-148">The format is *username@servername*.</span></span>
    | <span data-ttu-id="0a298-149">Senha</span><span class="sxs-lookup"><span data-stu-id="0a298-149">Password</span></span> | <span data-ttu-id="0a298-150">sua senha</span><span class="sxs-lookup"><span data-stu-id="0a298-150">your password</span></span> | <span data-ttu-id="0a298-151">Clique no botão **Armazenar no cofre...** para salvar a senha.</span><span class="sxs-lookup"><span data-stu-id="0a298-151">Click **Store in Vault...** button to save the password.</span></span> |

3.   <span data-ttu-id="0a298-152">Clique em **Testar Conexão** para testar se todos os parâmetros estiverem configurados corretamente.</span><span class="sxs-lookup"><span data-stu-id="0a298-152">Click **Test Connection** to test if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="0a298-153">Clique em **OK** para salvar a conexão.</span><span class="sxs-lookup"><span data-stu-id="0a298-153">Click **OK** to save the connection.</span></span> 

5.   <span data-ttu-id="0a298-154">Na lista de **Conexões MySQL**, clique no bloco correspondente ao seu servidor e aguarde até que a conexão seja estabelecida.</span><span class="sxs-lookup"><span data-stu-id="0a298-154">In the listing of **MySQL Connections**, click the tile corresponding to your server and wait for the connection to be established.</span></span>

6.   <span data-ttu-id="0a298-155">Uma nova guia do SQL é aberta, com um editor em branco no qual você pode digitar suas consultas.</span><span class="sxs-lookup"><span data-stu-id="0a298-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0a298-156">Por padrão, a segurança da conexão SSL é exigida e imposta no seu Banco de Dados do Azure para o servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="0a298-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="0a298-157">Normalmente, nenhuma configuração adicional com certificados SSL é necessária para que o MySQL Workbench se conecte ao servidor.</span><span class="sxs-lookup"><span data-stu-id="0a298-157">Typically no additional configuration with SSL certificates is required for MySQL Workbench to connect to your server.</span></span> <span data-ttu-id="0a298-158">Para saber mais sobre SSL, confira [Configurar a conectividade SSL em seu aplicativo para se conectar com segurança ao Banco de Dados do Azure para MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="0a298-158">For more information on SSL, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="0a298-159">Se precisar desabilitar o SSL, visite o portal do Azure e clique na página Segurança de conexão para desabilitar o botão de alternância Impor conexão SSL.</span><span class="sxs-lookup"><span data-stu-id="0a298-159">If you need to disable SSL, visit the Azure portal and click the Connection security page to disable the Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="0a298-160">Criar uma tabela, inserir dados, ler dados, atualizar dados, excluir dados</span><span class="sxs-lookup"><span data-stu-id="0a298-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="0a298-161">Copie e cole o código de exemplo do SQL em uma guia SQL em branco para ilustrar alguns dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="0a298-161">Copy and paste the sample SQL code into a blank SQL tab to illustrate some sample data.</span></span>

    <span data-ttu-id="0a298-162">Esse código cria um banco de dados vazio chamado quickstartdb e, em seguida, cria uma tabela de exemplo chamada inventory.</span><span class="sxs-lookup"><span data-stu-id="0a298-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="0a298-163">Ele insere algumas linhas e, em seguida, lê as linhas.</span><span class="sxs-lookup"><span data-stu-id="0a298-163">It inserts some rows, then reads the rows.</span></span> <span data-ttu-id="0a298-164">Ele altera os dados com uma instrução de atualização e lê as linhas novamente.</span><span class="sxs-lookup"><span data-stu-id="0a298-164">It changes the data with an update statement, and reads the rows again.</span></span> <span data-ttu-id="0a298-165">Por fim, exclui uma linha e lê as linhas novamente.</span><span class="sxs-lookup"><span data-stu-id="0a298-165">Finally it deletes a row, and reads the rows again.</span></span>
    
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

    <span data-ttu-id="0a298-166">A captura de tela mostra um exemplo do código SQL no SQL Workbench e a saída após sua execução.</span><span class="sxs-lookup"><span data-stu-id="0a298-166">The screenshot shows an example of the SQL code in SQL Workbench and the output after it has been run.</span></span>
    
    ![Guia de SQL do MySQL Workbench para executar código SQL de exemplo](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="0a298-168">Para executar o código SQL de exemplo, clique no ícone de raio na barra de ferramentas da guia **Arquivo SQL**.</span><span class="sxs-lookup"><span data-stu-id="0a298-168">To run the sample SQL Code, click the lightening bolt icon in the toolbar of the **SQL File** tab.</span></span>
3. <span data-ttu-id="0a298-169">Observe os resultados em três guias na seção **Grade de Resultados** no meio da página.</span><span class="sxs-lookup"><span data-stu-id="0a298-169">Notice the three tabbed results in the **Result Grid** section in the middle of the page.</span></span> 
4. <span data-ttu-id="0a298-170">Observe a lista de **Saída** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="0a298-170">Notice the **Output** list at the bottom of the page.</span></span> <span data-ttu-id="0a298-171">O status de cada comando é mostrado.</span><span class="sxs-lookup"><span data-stu-id="0a298-171">The status of each command is shown.</span></span> 

<span data-ttu-id="0a298-172">Agora, você se conectou ao Banco de Dados do Azure para MySQL usando o MySQL Workbench e consultou dados usando a linguagem SQL.</span><span class="sxs-lookup"><span data-stu-id="0a298-172">Now, you have connected to Azure Database for MySQL using MySQL Workbench, and have queried data using the SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a298-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0a298-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0a298-174">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="0a298-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
