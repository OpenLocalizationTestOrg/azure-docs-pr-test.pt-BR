---
title: Proteger o banco de dados SQL do Azure | Microsoft Docs
description: "Conheça técnicas e recursos para proteger o banco de dados SQL do Azure."
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 4bc09ad13ed0c9dc9257e9c75ec6f9ff3d689a0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="eb875-103">Proteger o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="eb875-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="eb875-104">O Banco de Dados SQL protege seus dados limitando o acesso ao banco de dados usando regras de firewall, mecanismos de autenticação que exigem que os usuários comprovem sua identidade e autorização para dados por meio de permissões e associações de função, bem como por meio de segurança em nível de linha e mascaramento de dados dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="eb875-104">SQL Database secures your data by limiting access to your database using firewall rules, authentication mechanisms requiring users to prove their identity, and authorization to data through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="eb875-105">Você pode melhorar a proteção do banco de dados contra usuários mal-intencionados ou acesso não autorizado com apenas algumas etapas simples.</span><span class="sxs-lookup"><span data-stu-id="eb875-105">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="eb875-106">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="eb875-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="eb875-107">Configurar regras de firewall no nível do servidor para o seu servidor no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="eb875-107">Set up server-level firewall rules for your server in the Azure portal</span></span>
> * <span data-ttu-id="eb875-108">Configurar regras de firewall no nível do banco de dados para o seu banco de dados usando SSMS</span><span class="sxs-lookup"><span data-stu-id="eb875-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="eb875-109">Conectar ao banco de dados usando uma cadeia de conexão segura</span><span class="sxs-lookup"><span data-stu-id="eb875-109">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="eb875-110">Gerenciar o acesso de usuário</span><span class="sxs-lookup"><span data-stu-id="eb875-110">Manage user access</span></span>
> * <span data-ttu-id="eb875-111">Proteger seus dados com criptografia</span><span class="sxs-lookup"><span data-stu-id="eb875-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="eb875-112">Habilitar a auditoria do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="eb875-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="eb875-113">Habilitar a detecção de ameaças do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="eb875-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="eb875-114">Se você não tiver uma assinatura do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="eb875-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb875-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="eb875-115">Prerequisites</span></span>

<span data-ttu-id="eb875-116">Para concluir este tutorial, você precisa do seguinte:</span><span class="sxs-lookup"><span data-stu-id="eb875-116">To complete this tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="eb875-117">A versão mais recente instalada do [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="eb875-117">Installed the newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="eb875-118">O Microsoft Excel instalado</span><span class="sxs-lookup"><span data-stu-id="eb875-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="eb875-119">Um servidor e banco de dados SQL do Azure - confira [Criar um banco de dados SQL do Azure no Portal do Azure](sql-database-get-started-portal.md), [Criar um único banco de dados SQL do Azure usando a CLI do Azure](sql-database-get-started-cli.md) e [Criar um único banco de dados SQL do Azure usando o PowerShell](sql-database-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="eb875-119">Created an Azure SQL server and database - See [Create an Azure SQL database in the Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using the Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="eb875-120">Faça logon no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="eb875-120">Log in to the Azure portal</span></span>

<span data-ttu-id="eb875-121">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="eb875-121">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="eb875-122">Criar uma regra de firewall de nível de servidor no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="eb875-122">Create a server-level firewall rule in the Azure portal</span></span>

<span data-ttu-id="eb875-123">Os banco de dados SQL são protegidos por um firewall no Azure.</span><span class="sxs-lookup"><span data-stu-id="eb875-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="eb875-124">Por padrão, todas as conexões com o servidor e os bancos de dados dentro do servidor são rejeitadas, exceto as conexões de outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb875-124">By default, all connections to the server and the databases inside the server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="eb875-125">Para saber mais, confira [Regras de firewall no nível do servidor e no nível do banco de dados do Banco de Dados SQL do Azure](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="eb875-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="eb875-126">A configuração mais segura é definir ‘Permitir acesso aos serviços do Azure’ como DESATIVADO.</span><span class="sxs-lookup"><span data-stu-id="eb875-126">The most secure configuration is to set 'Allow access to Azure services' to OFF.</span></span> <span data-ttu-id="eb875-127">Se você precisar se conectar ao banco de dados em uma VM do Azure ou um serviço de nuvem, deverá criar um [IP Reservado](../virtual-network/virtual-networks-reserved-public-ip.md) e permitir somente o acesso ao endereço IP reservado por meio do firewall.</span><span class="sxs-lookup"><span data-stu-id="eb875-127">If you need to connect to the database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only the reserved IP address access through the firewall.</span></span> 

<span data-ttu-id="eb875-128">Siga estas etapas para criar uma [regra de firewall no nível do servidor de Banco de Dados SQL](sql-database-firewall-configure.md) para que o servidor permita conexões de um endereço IP específico.</span><span class="sxs-lookup"><span data-stu-id="eb875-128">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server to allow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="eb875-129">Se você criou um exemplo de banco de dados no Azure usando um dos tutoriais ou guias de início rápido anteriores e estiver executando este tutorial em um computador com o mesmo endereço IP usado nos tutoriais, ignore esta etapa, pois você já criou uma regra de firewall no nível do servidor.</span><span class="sxs-lookup"><span data-stu-id="eb875-129">If you have created a sample database in Azure using one of the previous tutorials or quickstarts and are performing this tutorial on a computer with the same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="eb875-130">Clique em **Bancos de dados SQL** no menu esquerdo e clique no banco de dados para o qual você gostaria de configurar a regra de firewall na página **Bancos de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="eb875-130">Click **SQL databases** from the left-hand menu and click the database you would like to configure the firewall rule for on the **SQL databases** page.</span></span> <span data-ttu-id="eb875-131">A página de visão geral de seu banco de dados é aberta, mostrando o nome totalmente qualificado do servidor (como **mynewserver-20170313.database.windows.net**) e fornece opções para configurações adicionais.</span><span class="sxs-lookup"><span data-stu-id="eb875-131">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![regra de firewall do servidor](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="eb875-133">Clique em **Definir o firewall do servidor** na barra de ferramentas, conforme mostrado na imagem anterior.</span><span class="sxs-lookup"><span data-stu-id="eb875-133">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="eb875-134">A página **Configurações do firewall** do servidor de Banco de Dados SQL é aberta.</span><span class="sxs-lookup"><span data-stu-id="eb875-134">The **Firewall settings** page for the SQL Database server opens.</span></span> 

3. <span data-ttu-id="eb875-135">Clique em **Adicionar IP do cliente** na barra de ferramentas para adicionar o endereço IP público do computador conectado ao portal ou inserir a regra de firewall manualmente e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="eb875-135">Click **Add client IP** on the toolbar to add the public IP address of the computer connected to the portal with or enter the firewall rule manually and then click **Save**.</span></span>

      ![definir regra de firewall do servidor](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="eb875-137">Clique em **OK** e clique no **X** para fechar a página **Configurações do firewall**.</span><span class="sxs-lookup"><span data-stu-id="eb875-137">Click **OK** and then click the **X** to close the **Firewall settings** page.</span></span>

<span data-ttu-id="eb875-138">Agora você pode se conectar a qualquer banco de dados do servidor com o endereço IP ou o intervalo de endereços IP especificado.</span><span class="sxs-lookup"><span data-stu-id="eb875-138">You can now connect to any database in the server with the specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="eb875-139">O Banco de Dados SQL se comunica pela porta 1433.</span><span class="sxs-lookup"><span data-stu-id="eb875-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="eb875-140">Se você estiver tentando conectar-se a partir de uma rede corporativa, o tráfego de saída pela porta 1433 poderá não ser permitido pelo firewall de sua rede.</span><span class="sxs-lookup"><span data-stu-id="eb875-140">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="eb875-141">Se isto acontecer, você não conseguirá conectar seu servidor do Banco de Dados SQL do Azure, a menos que o departamento de TI abra a porta 1433.</span><span class="sxs-lookup"><span data-stu-id="eb875-141">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="eb875-142">Criar uma regra de firewall no nível do banco de dados usando SSMS</span><span class="sxs-lookup"><span data-stu-id="eb875-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="eb875-143">As regras de firewall no nível do banco de dados permitem a criação de configurações de firewall diferentes para bancos de dados diferentes dentro do mesmo servidor lógico, e a criação de regras de firewall portáteis, ou seja, elas seguem o banco de dados durante um [failover](sql-database-geo-replication-overview.md) em vez de serem armazenadas no SQL server.</span><span class="sxs-lookup"><span data-stu-id="eb875-143">Database-level firewall rules enable you to create different firewall settings for different databases within the same logical server and to create firewall rules that are portable - meaning that they follow the database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on the SQL server.</span></span> <span data-ttu-id="eb875-144">As regras de firewall no nível do banco de dados só podem ser configuradas usando instruções Transact-SQL e somente depois de ter configurado a primeira regra de firewall no nível do servidor.</span><span class="sxs-lookup"><span data-stu-id="eb875-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured the first server-level firewall rule.</span></span> <span data-ttu-id="eb875-145">Para saber mais, confira [Regras de firewall no nível do servidor e no nível do banco de dados do Banco de Dados SQL do Azure](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="eb875-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="eb875-146">Siga estas etapas para criar uma regra de firewall específica ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="eb875-146">Follows these steps to create a database-specific firewall rule.</span></span>

1. <span data-ttu-id="eb875-147">Conecte ao banco de dados, por exemplo, usando o [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="eb875-147">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="eb875-148">No Pesquisador de Objetos, clique com o botão direito do mouse no banco de dados ao qual você deseja adicionar uma regra de firewall e clique em **Nova Consulta**.</span><span class="sxs-lookup"><span data-stu-id="eb875-148">In Object Explorer, right-click on the database you want to add a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="eb875-149">Uma janela de consulta em branco conectada ao seu banco de dados é aberta.</span><span class="sxs-lookup"><span data-stu-id="eb875-149">A blank query window opens that is connected to your database.</span></span>

3. <span data-ttu-id="eb875-150">Na janela de consulta, modifique o endereço IP para seu endereço IP público e, depois, execute a seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="eb875-150">In the query window, modify the IP address to your public IP address and then execute the following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="eb875-151">Na barra de ferramentas, clique em **Executar** para criar a regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="eb875-151">On the toolbar, click **Execute** to create the firewall rule.</span></span>

## <a name="view-how-to-connect-an-application-to-your-database-using-a-secure-connection-string"></a><span data-ttu-id="eb875-152">Veja como conectar um aplicativo ao seu banco de dados usando uma cadeia de conexão segura</span><span class="sxs-lookup"><span data-stu-id="eb875-152">View how to connect an application to your database using a secure connection string</span></span>

<span data-ttu-id="eb875-153">Para garantir uma conexão segura e criptografada entre um aplicativo cliente e o banco de dados SQL, a cadeia de conexão deve ser configurada para:</span><span class="sxs-lookup"><span data-stu-id="eb875-153">To ensure a secure, encrypted connection between a client application and SQL Database, the connection string has to be configured to:</span></span>

- <span data-ttu-id="eb875-154">Solicitar uma conexão criptografada, e</span><span class="sxs-lookup"><span data-stu-id="eb875-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="eb875-155">Não confiar no certificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="eb875-155">To not trust the server certificate.</span></span> 

<span data-ttu-id="eb875-156">Isso estabelece uma conexão usando o protocolo TLS e reduz o risco de ataques man-in-the-middle.</span><span class="sxs-lookup"><span data-stu-id="eb875-156">This establishes a connection using Transport Layer Security (TLS) and reduces the risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="eb875-157">Você pode obter cadeias de conexão configuradas corretamente para seu Banco de Dados SQL para os drivers cliente com suporte no portal do Azure, conforme mostrado para o ADO.net nesta captura de tela.</span><span class="sxs-lookup"><span data-stu-id="eb875-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from the Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="eb875-158">Selecione **Bancos de dados SQL** no menu à esquerda e clique em seu banco de dados na página **Bancos de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="eb875-158">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span>

2. <span data-ttu-id="eb875-159">Na página **Visão Geral** do banco de dados, clique em **Mostrar cadeias de conexão de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="eb875-159">On the **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="eb875-160">Examine a cadeia de conexão completa do **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="eb875-160">Review the complete **ADO.NET** connection string.</span></span>

    ![Cadeia de conexão do ADO.NET](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="eb875-162">Criar usuários de banco de dados</span><span class="sxs-lookup"><span data-stu-id="eb875-162">Creating database users</span></span>

<span data-ttu-id="eb875-163">Antes de criar os usuários, primeiro você deve escolher um dos dois tipos de autenticação com suporte no Banco de Dados SQL do Azure:</span><span class="sxs-lookup"><span data-stu-id="eb875-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="eb875-164">**Autenticação do SQL**, que usa o nome de usuário e a senha para logons e usuários que são válidos somente no contexto de um banco de dados específico em um servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="eb875-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in the context of a specific database within a logical server.</span></span> 

<span data-ttu-id="eb875-165">**Autenticação do Azure Active Directory**, que usa identidades gerenciadas pelo Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eb875-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="eb875-166">Se você desejar usar o [Azure Active Directory](./sql-database-aad-authentication.md) para realizar a autenticação no Banco de Dados SQL, deverá haver um Azure Active Directory populado antes que você possa continuar.</span><span class="sxs-lookup"><span data-stu-id="eb875-166">If you want to use [Azure Active Directory](./sql-database-aad-authentication.md) to authenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="eb875-167">Siga estas etapas para criar um usuário usando a Autenticação do SQL:</span><span class="sxs-lookup"><span data-stu-id="eb875-167">Follow these steps to create a user using SQL Authentication:</span></span>

1. <span data-ttu-id="eb875-168">Conecte-se ao banco de dados, por exemplo, usando o [SQL Server Management Studio](./sql-database-connect-query-ssms.md) com suas credenciais de administrador do servidor.</span><span class="sxs-lookup"><span data-stu-id="eb875-168">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="eb875-169">No Pesquisador de Objetos, clique com o botão direito do mouse no banco de dados ao qual você deseja adicionar um novo usuário e clique em **Nova Consulta**.</span><span class="sxs-lookup"><span data-stu-id="eb875-169">In Object Explorer, right-click on the database you want to add a new user on and click **New Query**.</span></span> <span data-ttu-id="eb875-170">Uma janela de consulta em branco conectada ao banco de dados selecionado é aberta.</span><span class="sxs-lookup"><span data-stu-id="eb875-170">A blank query window opens that is connected to the selected database.</span></span>

3. <span data-ttu-id="eb875-171">Na janela de consulta, insira a seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="eb875-171">In the query window, enter the following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="eb875-172">Na barra de ferramentas, clique em **Executar** para criar o usuário.</span><span class="sxs-lookup"><span data-stu-id="eb875-172">On the toolbar, click **Execute** to create the user.</span></span>

5. <span data-ttu-id="eb875-173">Por padrão, o usuário pode se conectar ao banco de dados, mas não tem permissões para ler nem gravar dados.</span><span class="sxs-lookup"><span data-stu-id="eb875-173">By default, the user can connect to the database, but has no permissions to read or write data.</span></span> <span data-ttu-id="eb875-174">Para conceder essas permissões ao usuário recém-criado, execute os dois comandos a seguir em uma nova janela de consulta</span><span class="sxs-lookup"><span data-stu-id="eb875-174">To grant these permissions to the newly created user, execute the following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="eb875-175">É uma melhor prática criar essas contas não administrador no nível do banco de dados para se conectar ao banco de dados, a menos que você precise executar tarefas de administrador como criar novos usuários.</span><span class="sxs-lookup"><span data-stu-id="eb875-175">It is best practice to create these non-administrator accounts at the database level to connect to your database unless you need to execute administrator tasks like creating new users.</span></span> <span data-ttu-id="eb875-176">Consulte o [tutorial do Azure Active Directory](./sql-database-aad-authentication-configure.md) para saber como realizar a autenticação usando o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eb875-176">Please review the [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how to authenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="eb875-177">Proteger seus dados com criptografia</span><span class="sxs-lookup"><span data-stu-id="eb875-177">Protect your data with encryption</span></span>

<span data-ttu-id="eb875-178">A TDE (Transparent Data Encryption) do Banco de Dados SQL do Azure criptografa seus dados em repouso automaticamente, sem a necessidade de alterações no aplicativo que acessa o banco de dados criptografado.</span><span class="sxs-lookup"><span data-stu-id="eb875-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes to the application accessing the encrypted database.</span></span> <span data-ttu-id="eb875-179">Para bancos de dados recém-criados, a TDE estará ativada por padrão.</span><span class="sxs-lookup"><span data-stu-id="eb875-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="eb875-180">Para habilitar a TDE para seu banco de dados ou verificar se a TDE está ativada, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="eb875-180">To enable TDE for your database or to verify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="eb875-181">Selecione **Bancos de dados SQL** no menu à esquerda e clique em seu banco de dados na página **Bancos de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="eb875-181">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="eb875-182">Clique em **Transparent Data Encryption** para abrir a página de configuração da TDE.</span><span class="sxs-lookup"><span data-stu-id="eb875-182">Click on **Transparent data encryption** to open the configuration page for TDE.</span></span>

    ![Transparent Data Encryption](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="eb875-184">Se for necessário, defina **Criptografia de dados** como ATIVADO e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="eb875-184">If necessary, set **Data encryption** to ON and click **Save**.</span></span>

<span data-ttu-id="eb875-185">O processo de criptografia é iniciado em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="eb875-185">The encryption process starts in the background.</span></span> <span data-ttu-id="eb875-186">Você pode monitorar o progresso ao se conectar ao banco de dados SQL usando o [SQL Server Management Studio](./sql-database-connect-query-ssms.md) ao consultar a coluna encryption_state da exibição `sys.dm_database_encryption_keys`.</span><span class="sxs-lookup"><span data-stu-id="eb875-186">You can monitor the progress by connecting to SQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying the encryption_state column of the `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="eb875-187">Habilitar a auditoria do Banco de Dados SQL, se for necessário</span><span class="sxs-lookup"><span data-stu-id="eb875-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="eb875-188">A Auditoria do Azure SQL Database rastreia eventos do banco de dados e os grava em um log de auditoria em sua conta do Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="eb875-188">Azure SQL Database Auditing tracks database events and writes them to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="eb875-189">A auditoria pode ajudar você a manter uma conformidade regulatória, a entender a atividade do banco de dados e a obter informações sobre discrepâncias e anomalias que poderiam indicar potenciais violações de segurança.</span><span class="sxs-lookup"><span data-stu-id="eb875-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="eb875-190">Siga estas etapas para criar uma política de auditoria padrão para o banco de dados SQL:</span><span class="sxs-lookup"><span data-stu-id="eb875-190">Follow these steps to create a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="eb875-191">Selecione **Bancos de dados SQL** no menu à esquerda e clique em seu banco de dados na página **Bancos de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="eb875-191">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="eb875-192">Na folha Configurações, selecione **Auditoria e Detecção de Ameaças**.</span><span class="sxs-lookup"><span data-stu-id="eb875-192">In the Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="eb875-193">Observe que a auditoria no nível do servidor está desabilitada e que há um link **Exibir configurações do servidor**, o qual permite a exibição ou modificação das configurações de auditoria do servidor neste contexto.</span><span class="sxs-lookup"><span data-stu-id="eb875-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you to view or modify the server auditing settings from this context.</span></span>

    ![Folha Auditoria](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="eb875-195">Se você preferir habilitar um tipo (ou local?) de Auditoria diferente do especificado no nível do servidor, **ATIVE** a opção Auditoria e escolha o Tipo de Auditoria **Blob**.</span><span class="sxs-lookup"><span data-stu-id="eb875-195">If you prefer to enable an Audit type (or location?) different from the one specified at the server level, turn **ON** Auditing, and choose the **Blob** Auditing Type.</span></span> <span data-ttu-id="eb875-196">Se a auditoria de blob do servidor estiver habilitada, a auditoria de banco de dados configurada existirá lado a lado com a auditoria de blob do servidor.</span><span class="sxs-lookup"><span data-stu-id="eb875-196">If server Blob auditing is enabled, the database configured audit will exist side by side with the server Blob audit.</span></span>

    ![Ativar a auditoria](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="eb875-198">Selecione **Detalhes de Armazenamento** para abrir a Folha de Armazenamento de Logs de Auditoria.</span><span class="sxs-lookup"><span data-stu-id="eb875-198">Select **Storage Details** to open the Audit Logs Storage Blade.</span></span> <span data-ttu-id="eb875-199">Selecione a conta do Azure Storage em que os logs serão salvos e o período de retenção, após o qual os logs antigos serão excluídos, e clique em **OK** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="eb875-199">Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted, then click **OK** at the bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="eb875-200">Use a mesma conta de armazenamento para todos os bancos de dados auditados para aproveitar ao máximo os modelos de relatórios de auditoria.</span><span class="sxs-lookup"><span data-stu-id="eb875-200">Use the same storage account for all audited databases to get the most out of the auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="eb875-201">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="eb875-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eb875-202">Se desejar personalizar os eventos auditados, você pode fazer isso por meio do PowerShell ou API REST. Consulte a seção [Automação (PowerShell/API REST)](sql-database-auditing.md#subheading-7) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="eb875-202">If you want to customize the audited events, you can do this via PowerShell or REST API - see the [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="eb875-203">Habilitar a detecção de ameaças do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="eb875-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="eb875-204">A Detecção de Ameaças fornece uma nova camada de segurança, que permite que os clientes detectem e respondam às ameaças potenciais conforme elas ocorrem, fornecendo alertas de segurança nas atividades anormais.</span><span class="sxs-lookup"><span data-stu-id="eb875-204">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="eb875-205">Os usuários podem explorar os eventos suspeitos usando a Auditoria do Banco de Dados SQL para determinar se eles resultam de uma tentativa de acesso, violação ou exploração dos dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="eb875-205">Users can explore the suspicious events using SQL Database Auditing to determine if they result from an attempt to access, breach or exploit data in the database.</span></span> <span data-ttu-id="eb875-206">A Detecção de Ameaças torna simples tratar as possíveis ameaças no banco de dados sem a necessidade de ser um especialista em segurança ou gerenciar os sistemas de monitoramento de segurança avançados.</span><span class="sxs-lookup"><span data-stu-id="eb875-206">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="eb875-207">Por exemplo, a Detecção de Ameaças detecta determinadas atividades anormais do banco de dados que indicam possíveis tentativas de injeção de SQL.</span><span class="sxs-lookup"><span data-stu-id="eb875-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="eb875-208">A injeção de SQL é um dos problemas comuns de segurança do aplicativo da Web na Internet, usada para atacar os aplicativos controlados por dados.</span><span class="sxs-lookup"><span data-stu-id="eb875-208">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="eb875-209">Os invasores aproveitam as vulnerabilidades do aplicativo para inserir instruções SQL mal-intencionadas nos campos de entrada do aplicativo, para violar ou modificar os dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="eb875-209">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

1. <span data-ttu-id="eb875-210">Navegue para a folha de configuração do banco de dados SQL que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="eb875-210">Navigate to the configuration blade of the SQL database you want to monitor.</span></span> <span data-ttu-id="eb875-211">Na folha Configurações, selecione **Auditoria e Detecção de Ameaças**.</span><span class="sxs-lookup"><span data-stu-id="eb875-211">In the Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![Painel de navegação](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="eb875-213">Na folha de configuração **Auditoria e Detecção de Ameaças**, **ATIVE** a auditoria, o que exibirá as configurações de detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="eb875-213">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the threat detection settings.</span></span>

3. <span data-ttu-id="eb875-214">**ATIVE** a detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="eb875-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="eb875-215">Configure a lista de emails que receberão os alertas de segurança após a detecção das atividades anormais do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="eb875-215">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="eb875-216">Clique em **Salvar** na folha **Auditoria e detecção de ameaças** para salvar a auditoria nova ou atualizada e a política de detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="eb875-216">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection policy.</span></span>

    ![Painel de navegação](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="eb875-218">Se forem detectadas atividades anormais de banco de dados, você receberá uma notificação por email na detecção das atividades anormais do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="eb875-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="eb875-219">O email fornecerá informações sobre o evento de segurança suspeito, incluindo a natureza das atividades anormais, nome do banco de dados, nome do servidor e a hora do evento.</span><span class="sxs-lookup"><span data-stu-id="eb875-219">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="eb875-220">Além disso, ele fornecerá informações sobre as possíveis causas e ações recomendadas para investigar e atenuar a ameaça em potencial no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="eb875-220">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span> <span data-ttu-id="eb875-221">As próximas etapas explicam o que deverá ser feito caso você receba um email desse tipo:</span><span class="sxs-lookup"><span data-stu-id="eb875-221">The next steps walk you through what to do should you receive such an email:</span></span>

    ![Email de detecção de ameaças](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="eb875-223">No email, clique no link **Log de Auditoria do SQL do Azure**, que iniciará o portal do Azure e mostrará os registros de auditoria relevantes do período do evento suspeito.</span><span class="sxs-lookup"><span data-stu-id="eb875-223">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure portal and show the relevant auditing records around the time of the suspicious event.</span></span>

    ![Registros de auditoria](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="eb875-225">Clique nos registros de auditoria para exibir mais detalhes sobre as atividades suspeitas do banco de dados, como a instrução SQL, motivo da falha e IP do cliente.</span><span class="sxs-lookup"><span data-stu-id="eb875-225">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![Detalhes do registro](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="eb875-227">Na folha Registros de Auditoria, clique em **Abrir no Excel** para abrir um modelo pré-configurado do Excel para importar e executar uma análise mais profunda do log de auditoria na época do evento suspeito.</span><span class="sxs-lookup"><span data-stu-id="eb875-227">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eb875-228">No Excel 2010 ou posterior, o Power Query e a configuração **Combinação Rápida** são necessários.</span><span class="sxs-lookup"><span data-stu-id="eb875-228">In Excel 2010 or later, Power Query and the **Fast Combine** setting is required.</span></span>

    ![Abrir registros no Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="eb875-230">Para definir a configuração **Combinação Rápida**: na guia de faixa de opções **POWER QUERY**, selecione **Opções** para exibir a caixa de diálogo Opções.</span><span class="sxs-lookup"><span data-stu-id="eb875-230">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="eb875-231">Selecione a seção Privacidade e escolha a segunda opção - 'Ignorar os Níveis de Privacidade e melhorar potencialmente o desempenho':</span><span class="sxs-lookup"><span data-stu-id="eb875-231">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>

    ![Combinação Rápida do Excel](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="eb875-233">Para carregar os logs de auditoria do SQL, verifique se os parâmetros na guia de configurações estão definidos corretamente e, em seguida, selecione a faixa de opções 'Dados' e clique no botão 'Atualizar Tudo'.</span><span class="sxs-lookup"><span data-stu-id="eb875-233">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>

    ![Parâmetros do Excel](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="eb875-235">Os resultados aparecem na folha **Logs de Auditoria do SQL** , que permite executar uma análise mais profunda das atividades anormais detectadas e minimizar o impacto do evento de segurança em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eb875-235">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="eb875-236">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eb875-236">Next steps</span></span>
<span data-ttu-id="eb875-237">Você pode melhorar a proteção do banco de dados contra usuários mal-intencionados ou acesso não autorizado com apenas algumas etapas simples.</span><span class="sxs-lookup"><span data-stu-id="eb875-237">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="eb875-238">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="eb875-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="eb875-239">Configurar regras de firewall para seu servidor e/ou banco de dados</span><span class="sxs-lookup"><span data-stu-id="eb875-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="eb875-240">Conectar ao banco de dados usando uma cadeia de conexão segura</span><span class="sxs-lookup"><span data-stu-id="eb875-240">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="eb875-241">Gerenciar o acesso de usuário</span><span class="sxs-lookup"><span data-stu-id="eb875-241">Manage user access</span></span>
> * <span data-ttu-id="eb875-242">Proteger seus dados com criptografia</span><span class="sxs-lookup"><span data-stu-id="eb875-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="eb875-243">Habilitar a auditoria do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="eb875-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="eb875-244">Habilitar a detecção de ameaças do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="eb875-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="eb875-245">Melhore o desempenho do banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="eb875-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

