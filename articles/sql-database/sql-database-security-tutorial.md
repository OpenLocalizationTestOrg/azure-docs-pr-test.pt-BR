---
title: aaaSecure seu banco de dados SQL do Azure | Microsoft Docs
description: "Saiba mais sobre toosecure técnicas e recursos de seu banco de dados do SQL Azure."
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
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="6e8cd-103">Proteger o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="6e8cd-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="6e8cd-104">Banco de dados SQL protege seus dados por meio da limitação tooyour banco de dados usando regras de firewall, exigindo usuários tooprove sua identidade e autorização toodata por meio de permissões e associações de função, bem como por meio de mecanismos de autenticação segurança em nível de linha e mascaramento de dados dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-104">SQL Database secures your data by limiting access tooyour database using firewall rules, authentication mechanisms requiring users tooprove their identity, and authorization toodata through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="6e8cd-105">Você pode melhorar a proteção de saudação do banco de dados contra usuários mal-intencionados ou acesso não autorizado com apenas algumas etapas simples.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-105">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="6e8cd-106">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="6e8cd-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="6e8cd-107">Configurar regras de firewall no nível de servidor para o servidor de saudação portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6e8cd-107">Set up server-level firewall rules for your server in hello Azure portal</span></span>
> * <span data-ttu-id="6e8cd-108">Configurar regras de firewall no nível do banco de dados para o seu banco de dados usando SSMS</span><span class="sxs-lookup"><span data-stu-id="6e8cd-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="6e8cd-109">Conecte-se o banco de dados de tooyour usando uma cadeia de caracteres de conexão segura</span><span class="sxs-lookup"><span data-stu-id="6e8cd-109">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="6e8cd-110">Gerenciar o acesso de usuário</span><span class="sxs-lookup"><span data-stu-id="6e8cd-110">Manage user access</span></span>
> * <span data-ttu-id="6e8cd-111">Proteger seus dados com criptografia</span><span class="sxs-lookup"><span data-stu-id="6e8cd-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="6e8cd-112">Habilitar a auditoria do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="6e8cd-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="6e8cd-113">Habilitar a detecção de ameaças do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="6e8cd-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="6e8cd-114">Se você não tiver uma assinatura do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e8cd-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6e8cd-115">Prerequisites</span></span>

<span data-ttu-id="6e8cd-116">toocomplete este tutorial, verifique se você tem Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6e8cd-116">toocomplete this tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="6e8cd-117">A versão mais recente instalada saudação do [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="6e8cd-117">Installed hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="6e8cd-118">O Microsoft Excel instalado</span><span class="sxs-lookup"><span data-stu-id="6e8cd-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="6e8cd-119">Criado um servidor do SQL Azure e o banco de dados - consulte [criar um banco de dados do SQL Azure no portal do Azure de saudação](sql-database-get-started-portal.md), [criar um único banco de dados SQL do Azure usando Olá CLI do Azure](sql-database-get-started-cli.md), e [criar um único SQL Azure banco de dados usando o PowerShell](sql-database-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6e8cd-119">Created an Azure SQL server and database - See [Create an Azure SQL database in hello Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using hello Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="6e8cd-120">Faça logon no toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6e8cd-120">Log in toohello Azure portal</span></span>

<span data-ttu-id="6e8cd-121">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6e8cd-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="6e8cd-122">Criar uma regra de firewall de nível de servidor no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6e8cd-122">Create a server-level firewall rule in hello Azure portal</span></span>

<span data-ttu-id="6e8cd-123">Os banco de dados SQL são protegidos por um firewall no Azure.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="6e8cd-124">Por padrão, todas as conexões toohello server Olá bancos de dados e no servidor de saudação são rejeitados com exceção de conexões de outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-124">By default, all connections toohello server and hello databases inside hello server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="6e8cd-125">Para saber mais, confira [Regras de firewall no nível do servidor e no nível do banco de dados do Banco de Dados SQL do Azure](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6e8cd-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="6e8cd-126">configuração mais segura de saudação é tooset 'Permitir acesso serviços tooAzure' tooOFF.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-126">hello most secure configuration is tooset 'Allow access tooAzure services' tooOFF.</span></span> <span data-ttu-id="6e8cd-127">Se você precisar tooconnect toohello banco de dados de um serviço de nuvem ou VM do Azure, você deve criar um [IP reservado](../virtual-network/virtual-networks-reserved-public-ip.md) e permitir acesso somente de saudação reservado IP endereço através do firewall do hello.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-127">If you need tooconnect toohello database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only hello reserved IP address access through hello firewall.</span></span> 

<span data-ttu-id="6e8cd-128">Siga estas etapas toocreate um [regra de firewall de nível de servidor de banco de dados SQL](sql-database-firewall-configure.md) suas conexões de servidor tooallow de um endereço IP específico.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-128">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server tooallow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="6e8cd-129">Se você tiver criado um banco de dados de exemplo no Azure usando um dos tutoriais anteriores hello ou guias de início rápido e são executar este tutorial em um computador com hello mesmo endereço IP que ele tinha quando você analisou os tutoriais, você pode ignorar esta etapa, você terá já criou uma regra de firewall de nível de servidor.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-129">If you have created a sample database in Azure using one of hello previous tutorials or quickstarts and are performing this tutorial on a computer with hello same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="6e8cd-130">Clique em **bancos de dados SQL** de saudação esquerdo menu e clique em Olá banco de dados você gostaria que regra de firewall de saudação tooconfigure para em Olá **bancos de dados SQL** página.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-130">Click **SQL databases** from hello left-hand menu and click hello database you would like tooconfigure hello firewall rule for on hello **SQL databases** page.</span></span> <span data-ttu-id="6e8cd-131">Olá, página de visão geral para o banco de dados abre, mostrando a você Olá totalmente qualificado nome do servidor (como **mynewserver 20170313.database.windows.net**) e fornece opções de configuração adicional.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-131">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![regra de firewall do servidor](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="6e8cd-133">Clique em **definir o firewall do servidor** na barra de ferramentas Olá conforme mostrado na imagem anterior hello.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-133">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="6e8cd-134">Olá **configurações de Firewall** página para o servidor de banco de dados SQL Olá é aberta.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-134">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

3. <span data-ttu-id="6e8cd-135">Clique em **Adicionar IP do cliente** Olá barra de ferramentas tooadd Olá endereço IP público do portal de toohello conectado Olá computador com ou inserir a regra de firewall Olá manualmente e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-135">Click **Add client IP** on hello toolbar tooadd hello public IP address of hello computer connected toohello portal with or enter hello firewall rule manually and then click **Save**.</span></span>

      ![definir regra de firewall do servidor](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="6e8cd-137">Clique em **Okey** e, em seguida, clique em Olá **X** tooclose Olá **configurações de Firewall** página.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-137">Click **OK** and then click hello **X** tooclose hello **Firewall settings** page.</span></span>

<span data-ttu-id="6e8cd-138">Agora você pode conectar o banco de dados tooany no servidor de saudação com hello especificado um intervalo de endereços IP ou endereço IP.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-138">You can now connect tooany database in hello server with hello specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="6e8cd-139">O Banco de Dados SQL se comunica pela porta 1433.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="6e8cd-140">Se você estiver tentando tooconnect de dentro de uma rede corporativa, o tráfego de saída pela porta 1433 talvez não consigam pelo firewall da rede.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-140">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="6e8cd-141">Nesse caso, não será tooconnect capaz de servidor de banco de dados SQL de tooyour, a menos que o departamento de TI abre a porta 1433.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-141">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="6e8cd-142">Criar uma regra de firewall no nível do banco de dados usando SSMS</span><span class="sxs-lookup"><span data-stu-id="6e8cd-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="6e8cd-143">Regras de firewall de nível de banco de dados permitem que você toocreate as configurações de firewall diferentes para bancos de dados diferentes em Olá mesmo firewall de servidor e toocreate lógico as regras de portátil - que significa que sigam o banco de dados de saudação durante um [failover ](sql-database-geo-replication-overview.md) em vez de serem armazenados no SQL server de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-143">Database-level firewall rules enable you toocreate different firewall settings for different databases within hello same logical server and toocreate firewall rules that are portable - meaning that they follow hello database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on hello SQL server.</span></span> <span data-ttu-id="6e8cd-144">Regras de firewall de nível de banco de dados só podem ser configurado usando instruções Transact-SQL e somente depois que você configurou a primeira regra de firewall de nível de servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured hello first server-level firewall rule.</span></span> <span data-ttu-id="6e8cd-145">Para saber mais, confira [Regras de firewall no nível do servidor e no nível do banco de dados do Banco de Dados SQL do Azure](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6e8cd-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="6e8cd-146">Segue essas etapas toocreate uma regra de firewall de banco de dados específico.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-146">Follows these steps toocreate a database-specific firewall rule.</span></span>

1. <span data-ttu-id="6e8cd-147">Conecte-se o banco de dados tooyour, por exemplo, usando [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="6e8cd-147">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="6e8cd-148">No Pesquisador de objetos, clique com botão direito no banco de dados de saudação desejado tooadd regra para de um firewall e clique em **nova consulta**.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-148">In Object Explorer, right-click on hello database you want tooadd a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="6e8cd-149">Uma janela de consulta em branco é aberto que é conectado tooyour banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-149">A blank query window opens that is connected tooyour database.</span></span>

3. <span data-ttu-id="6e8cd-150">Na janela de consulta Olá, modifique Olá IP endereço tooyour endereço IP público e, em seguida, execute Olá consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="6e8cd-150">In hello query window, modify hello IP address tooyour public IP address and then execute hello following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="6e8cd-151">Na barra de ferramentas hello, clique em **Execute** toocreate regra de firewall de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-151">On hello toolbar, click **Execute** toocreate hello firewall rule.</span></span>

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a><span data-ttu-id="6e8cd-152">Exibir como tooconnect tooyour um aplicativo de banco de dados usando uma cadeia de caracteres de conexão segura</span><span class="sxs-lookup"><span data-stu-id="6e8cd-152">View how tooconnect an application tooyour database using a secure connection string</span></span>

<span data-ttu-id="6e8cd-153">tooensure uma conexão segura e criptografada entre um aplicativo cliente e o banco de dados SQL, a cadeia de caracteres de conexão Olá tem toobe configurado para:</span><span class="sxs-lookup"><span data-stu-id="6e8cd-153">tooensure a secure, encrypted connection between a client application and SQL Database, hello connection string has toobe configured to:</span></span>

- <span data-ttu-id="6e8cd-154">Solicitar uma conexão criptografada, e</span><span class="sxs-lookup"><span data-stu-id="6e8cd-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="6e8cd-155">certificado do servidor da saudação toonot confiável.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-155">toonot trust hello server certificate.</span></span> 

<span data-ttu-id="6e8cd-156">Isso estabelece uma conexão usando a segurança de camada de transporte (TLS) e reduz o risco de saudação de ataques man-in-the-middle.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-156">This establishes a connection using Transport Layer Security (TLS) and reduces hello risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="6e8cd-157">Você pode obter cadeias de caracteres de conexão configurada corretamente para seu banco de dados SQL para o cliente com suporte drivers de saudação portal do Azure conforme mostrado para ADO.net nesta captura de tela.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from hello Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="6e8cd-158">Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-158">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span>

2. <span data-ttu-id="6e8cd-159">Em Olá **visão geral** para seu banco de dados, clique em **Mostrar cadeias de conexão de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-159">On hello **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="6e8cd-160">Saudação de revisão completa **ADO.NET** cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-160">Review hello complete **ADO.NET** connection string.</span></span>

    ![Cadeia de conexão do ADO.NET](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="6e8cd-162">Criar usuários de banco de dados</span><span class="sxs-lookup"><span data-stu-id="6e8cd-162">Creating database users</span></span>

<span data-ttu-id="6e8cd-163">Antes de criar os usuários, primeiro você deve escolher um dos dois tipos de autenticação com suporte no Banco de Dados SQL do Azure:</span><span class="sxs-lookup"><span data-stu-id="6e8cd-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="6e8cd-164">**Autenticação do SQL**, que usa o nome de usuário e senha para logons e usuários que são válidos somente no contexto de um banco de dados específico dentro de um servidor lógico de hello.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in hello context of a specific database within a logical server.</span></span> 

<span data-ttu-id="6e8cd-165">**Autenticação do Azure Active Directory**, que usa identidades gerenciadas pelo Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="6e8cd-166">Se você quiser toouse [Active Directory do Azure](./sql-database-aad-authentication.md) tooauthenticate no banco de dados SQL, um Azure Active Directory preenchida deve existir antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-166">If you want toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="6e8cd-167">Siga estas etapas toocreate um usuário usando a autenticação do SQL:</span><span class="sxs-lookup"><span data-stu-id="6e8cd-167">Follow these steps toocreate a user using SQL Authentication:</span></span>

1. <span data-ttu-id="6e8cd-168">Conecte-se o banco de dados tooyour, por exemplo, usando [SQL Server Management Studio](./sql-database-connect-query-ssms.md) usando suas credenciais de administrador do servidor.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-168">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="6e8cd-169">No Pesquisador de objetos, clique com botão direito no banco de dados de saudação desejado tooadd um novo usuário em e clique em **nova consulta**.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-169">In Object Explorer, right-click on hello database you want tooadd a new user on and click **New Query**.</span></span> <span data-ttu-id="6e8cd-170">Uma janela de consulta em branco é aberto que é conectado toohello banco de dados selecionado.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-170">A blank query window opens that is connected toohello selected database.</span></span>

3. <span data-ttu-id="6e8cd-171">Na janela de consulta hello, digite Olá consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="6e8cd-171">In hello query window, enter hello following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="6e8cd-172">Na barra de ferramentas hello, clique em **Execute** toocreate usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-172">On hello toolbar, click **Execute** toocreate hello user.</span></span>

5. <span data-ttu-id="6e8cd-173">Por padrão, o usuário de Olá pode se conectar a banco de dados toohello, mas não tem permissões tooread ou gravar dados.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-173">By default, hello user can connect toohello database, but has no permissions tooread or write data.</span></span> <span data-ttu-id="6e8cd-174">toogrant toohello essas permissões usuário recém-criado, execute Olá dois comandos em uma nova janela de consulta a seguir</span><span class="sxs-lookup"><span data-stu-id="6e8cd-174">toogrant these permissions toohello newly created user, execute hello following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="6e8cd-175">É melhor toocreate prática essas contas não-administrador no hello tooyour de tooconnect de nível de banco de dados do banco de dados, a menos que você precisa tooexecute tarefas do administrador como a criação de novos usuários.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-175">It is best practice toocreate these non-administrator accounts at hello database level tooconnect tooyour database unless you need tooexecute administrator tasks like creating new users.</span></span> <span data-ttu-id="6e8cd-176">Analise Olá [tutorial do Active Directory do Azure](./sql-database-aad-authentication-configure.md) sobre como tooauthenticate usando o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-176">Please review hello [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how tooauthenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="6e8cd-177">Proteger seus dados com criptografia</span><span class="sxs-lookup"><span data-stu-id="6e8cd-177">Protect your data with encryption</span></span>

<span data-ttu-id="6e8cd-178">Criptografia de dados transparente de banco de dados SQL do Azure (TDE) criptografa automaticamente os dados em repouso, sem a necessidade de quaisquer alterações toohello aplicativo acessando Olá banco de dados criptografado.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes toohello application accessing hello encrypted database.</span></span> <span data-ttu-id="6e8cd-179">Para bancos de dados recém-criados, a TDE estará ativada por padrão.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="6e8cd-180">tooenable TDE para seu banco de dados ou tooverify TDE está ativada, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="6e8cd-180">tooenable TDE for your database or tooverify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="6e8cd-181">Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-181">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="6e8cd-182">Clique em **criptografia transparente de dados** tooopen página de configuração de saudação para TDE.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-182">Click on **Transparent data encryption** tooopen hello configuration page for TDE.</span></span>

    ![Transparent Data Encryption](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="6e8cd-184">Se necessário, defina **criptografia de dados** tooON e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-184">If necessary, set **Data encryption** tooON and click **Save**.</span></span>

<span data-ttu-id="6e8cd-185">Inicia o processo de criptografia Olá no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-185">hello encryption process starts in hello background.</span></span> <span data-ttu-id="6e8cd-186">Você pode monitorar o progresso de saudação pelo banco de dados usando conexão tooSQL [SQL Server Management Studio](./sql-database-connect-query-ssms.md) consultando a coluna encryption_state Olá Olá `sys.dm_database_encryption_keys` exibição.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-186">You can monitor hello progress by connecting tooSQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying hello encryption_state column of hello `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="6e8cd-187">Habilitar a auditoria do Banco de Dados SQL, se for necessário</span><span class="sxs-lookup"><span data-stu-id="6e8cd-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="6e8cd-188">Auditoria de banco de dados SQL Azure rastreia eventos de banco de dados e grava o log de auditoria tooan em sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-188">Azure SQL Database Auditing tracks database events and writes them tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="6e8cd-189">A auditoria pode ajudar você a manter uma conformidade regulatória, a entender a atividade do banco de dados e a obter informações sobre discrepâncias e anomalias que poderiam indicar potenciais violações de segurança.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="6e8cd-190">Siga essas etapas toocreate uma política de auditoria padrão do banco de dados SQL:</span><span class="sxs-lookup"><span data-stu-id="6e8cd-190">Follow these steps toocreate a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="6e8cd-191">Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-191">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="6e8cd-192">Na folha de configurações hello, selecione **auditoria e detecção de ameaças**.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-192">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="6e8cd-193">Observe que a auditoria de nível de servidor é diabled e que haja um **exibir configurações de servidor** link que permite que você tooview ou modificar configurações de auditoria de servidor de saudação neste contexto.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you tooview or modify hello server auditing settings from this context.</span></span>

    ![Folha Auditoria](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="6e8cd-195">Se você preferir tooenable uma auditoria tipo (ou local?) diferente da saudação especificada no nível do servidor de saudação, ativar **ON** auditoria e escolha Olá **Blob** tipo de auditoria.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-195">If you prefer tooenable an Audit type (or location?) different from hello one specified at hello server level, turn **ON** Auditing, and choose hello **Blob** Auditing Type.</span></span> <span data-ttu-id="6e8cd-196">Se o servidor Blob auditoria estiver habilitada, auditoria de banco de dados configurado Olá existirá lado a lado com a auditoria de Blob do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-196">If server Blob auditing is enabled, hello database configured audit will exist side by side with hello server Blob audit.</span></span>

    ![Ativar a auditoria](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="6e8cd-198">Selecione **detalhes armazenamento** tooopen Olá folha de armazenamento de Logs de auditoria.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-198">Select **Storage Details** tooopen hello Audit Logs Storage Blade.</span></span> <span data-ttu-id="6e8cd-199">Conta de armazenamento do Azure hello selecione onde os logs serão salvas e período de retenção hello, após o qual Olá logs antigos serão excluídos, clique em **Okey** na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-199">Select hello Azure storage account where logs will be saved, and hello retention period, after which hello old logs will be deleted, then click **OK** at hello bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="6e8cd-200">Use Olá a mesma conta de armazenamento para todos os Olá de tooget auditados bancos de dados máximo Olá auditoria modelos de relatórios.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-200">Use hello same storage account for all audited databases tooget hello most out of hello auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="6e8cd-201">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e8cd-202">Se você quiser toocustomize eventos de saudação auditado, você pode fazer isso por meio do PowerShell ou REST API - consulte Olá [automação (PowerShell / API REST)](sql-database-auditing.md#subheading-7) seção para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-202">If you want toocustomize hello audited events, you can do this via PowerShell or REST API - see hello [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="6e8cd-203">Habilitar a detecção de ameaças do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="6e8cd-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="6e8cd-204">A detecção de ameaças fornece uma nova camada de segurança, que permite que os clientes toodetect e responde a ameaças de toopotential conforme elas ocorrem, fornecendo alertas de segurança em atividades anormais.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-204">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="6e8cd-205">Os usuários podem explorar eventos suspeitos hello, usando a auditoria de banco de dados do SQL toodetermine se eles são provenientes de um tooaccess tentativa, violação ou exploram dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-205">Users can explore hello suspicious events using SQL Database Auditing toodetermine if they result from an attempt tooaccess, breach or exploit data in hello database.</span></span> <span data-ttu-id="6e8cd-206">A detecção de ameaças torna simples tooaddress potenciais ameaças toohello banco de dados sem a necessidade de saudação toobe um especialista em segurança ou gerenciar os sistemas de monitoramento de segurança avançada.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-206">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="6e8cd-207">Por exemplo, a Detecção de Ameaças detecta determinadas atividades anormais do banco de dados que indicam possíveis tentativas de injeção de SQL.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="6e8cd-208">Injeção de SQL é um dos Olá Web aplicativo problemas de segurança comuns em Olá Internet, os aplicativos usados tooattack controladas por dados.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-208">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="6e8cd-209">Os invasores tirar proveito de aplicativo vulnerabilidades tooinject de instruções SQL mal-intencionadas nos campos de entrada do aplicativo, para serem violados ou modificar dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-209">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

1. <span data-ttu-id="6e8cd-210">Navegue toohello folha de configuração de saudação deseja toomonitor do banco de dados do SQL.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-210">Navigate toohello configuration blade of hello SQL database you want toomonitor.</span></span> <span data-ttu-id="6e8cd-211">Na folha de configurações hello, selecione **auditoria e detecção de ameaças**.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-211">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![Painel de navegação](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="6e8cd-213">Em Olá **auditoria e detecção de ameaças** configuração folha ativar **ON** auditoria, que exibirá as configurações de detecção de ameaças hello.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-213">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello threat detection settings.</span></span>

3. <span data-ttu-id="6e8cd-214">**ATIVE** a detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="6e8cd-215">Configure Olá lista de endereços de email que receberão alertas de segurança após a detecção de atividades anormais de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-215">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="6e8cd-216">Clique em **salvar** em Olá **detecção de auditoria e ameaças** toosave folha Olá nova ou atualizada política de detecção de ameaças e auditoria.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-216">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection policy.</span></span>

    ![Painel de navegação](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="6e8cd-218">Se forem detectadas atividades anormais de banco de dados, você receberá uma notificação por email na detecção das atividades anormais do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="6e8cd-219">email Olá fornecerá informações sobre eventos de segurança suspeitos Olá incluindo natureza Olá de atividades anormais Olá, nome do banco de dados, a hora de evento de nome e hello do servidor.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-219">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="6e8cd-220">Além disso, ele fornecerá informações sobre possíveis causas e recomendado tooinvestigate ações e reduzir Olá potenciais ameaças toohello banco de dados de.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-220">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span> <span data-ttu-id="6e8cd-221">exame de etapas Avançar Olá você através do qual toodo você deve receber um email:</span><span class="sxs-lookup"><span data-stu-id="6e8cd-221">hello next steps walk you through what toodo should you receive such an email:</span></span>

    ![Email de detecção de ameaças](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="6e8cd-223">No email de saudação, clique em Olá **o Log de auditoria do SQL Azure** link, o que iniciará Olá portal do Azure e exibir registros de auditoria relevantes Olá em torno de tempo de saudação do evento suspeitas Olá.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-223">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure portal and show hello relevant auditing records around hello time of hello suspicious event.</span></span>

    ![Registros de auditoria](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="6e8cd-225">Clique em tooview de registros de auditoria hello mais detalhes sobre atividades de banco de dados suspeito hello, como a instrução SQL, IP de cliente e o motivo da falha.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-225">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![Detalhes do registro](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="6e8cd-227">Na folha de registros de auditoria de saudação, clique em **abrir no Excel** tooopen previamente configurada do excel tooimport de modelo e executar uma análise mais profunda do log de auditoria Olá em torno de tempo de saudação do evento suspeitas hello.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-227">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6e8cd-228">No Excel 2010 ou posterior, o Power Query e Olá **combinação rápida** configuração é necessária.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-228">In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required.</span></span>

    ![Abrir registros no Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="6e8cd-230">Olá tooconfigure **combinação rápida** configuração - no hello **POWER QUERY** guia de faixa de opções, selecione **opções** toodisplay caixa de diálogo de opções de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-230">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="6e8cd-231">Selecione a seção de privacidade hello e escolha Olá segunda opção - 'Ignorar Olá níveis de privacidade e potencialmente melhorar o desempenho':</span><span class="sxs-lookup"><span data-stu-id="6e8cd-231">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>

    ![Combinação Rápida do Excel](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="6e8cd-233">logs de auditoria do SQL tooload, verifique se Olá parâmetros na guia Configurações de saudação estão definidos corretamente e, em seguida, selecione a faixa de opções de 'Dados' hello e clique o botão 'Atualizar tudo' hello.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-233">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>

    ![Parâmetros do Excel](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="6e8cd-235">resultados de saudação aparecem na Olá **os Logs de auditoria do SQL** folha que permite que você toorun uma análise mais profunda de atividades anormais de saudação que foram detectadas e reduzir o impacto de saudação do evento de segurança de saudação em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-235">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6e8cd-236">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6e8cd-236">Next steps</span></span>
<span data-ttu-id="6e8cd-237">Você pode melhorar a proteção de saudação do banco de dados contra usuários mal-intencionados ou acesso não autorizado com apenas algumas etapas simples.</span><span class="sxs-lookup"><span data-stu-id="6e8cd-237">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="6e8cd-238">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="6e8cd-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="6e8cd-239">Configurar regras de firewall para seu servidor e/ou banco de dados</span><span class="sxs-lookup"><span data-stu-id="6e8cd-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="6e8cd-240">Conecte-se o banco de dados de tooyour usando uma cadeia de caracteres de conexão segura</span><span class="sxs-lookup"><span data-stu-id="6e8cd-240">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="6e8cd-241">Gerenciar o acesso de usuário</span><span class="sxs-lookup"><span data-stu-id="6e8cd-241">Manage user access</span></span>
> * <span data-ttu-id="6e8cd-242">Proteger seus dados com criptografia</span><span class="sxs-lookup"><span data-stu-id="6e8cd-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="6e8cd-243">Habilitar a auditoria do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="6e8cd-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="6e8cd-244">Habilitar a detecção de ameaças do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="6e8cd-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="6e8cd-245">Melhore o desempenho do banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="6e8cd-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

