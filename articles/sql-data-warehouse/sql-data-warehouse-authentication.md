---
title: "Autenticação no Azure SQL Data Warehouse | Microsoft Docs"
description: "Autenticação do AAD (Azure Active Directory) e SQL Server no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 92f48027051bc4aff4d6b8d66fdd6de81bba3657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="authentication-to-azure-sql-data-warehouse"></a><span data-ttu-id="2ca37-103">Autenticação no Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2ca37-103">Authentication to Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ca37-104">Visão Geral da Segurança</span><span class="sxs-lookup"><span data-stu-id="2ca37-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="2ca37-105">Autenticação</span><span class="sxs-lookup"><span data-stu-id="2ca37-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="2ca37-106">Criptografia (Portal)</span><span class="sxs-lookup"><span data-stu-id="2ca37-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="2ca37-107">Criptografia (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="2ca37-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="2ca37-108">Para se conectar ao SQL Data Warehouse, você precisa inserir credenciais de segurança para fins de autenticação.</span><span class="sxs-lookup"><span data-stu-id="2ca37-108">To connect to SQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="2ca37-109">Após estabelecer uma conexão, determinadas configurações de conexão são definidas como parte do estabelecimento de sua sessão de consulta.</span><span class="sxs-lookup"><span data-stu-id="2ca37-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="2ca37-110">Para obter mais informações sobre segurança e como habilitar conexões ao data warehouse, consulte [Proteger um banco de dados no SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="2ca37-110">For more information on security and how to enable connections to your data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="2ca37-111">Autenticação do SQL</span><span class="sxs-lookup"><span data-stu-id="2ca37-111">SQL authentication</span></span>
<span data-ttu-id="2ca37-112">Para se conectar ao SQL Data Warehouse, deve fornecer as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="2ca37-112">To connect to SQL Data Warehouse, you must provide the following information:</span></span>

* <span data-ttu-id="2ca37-113">Nome totalmente qualificado do servidor</span><span class="sxs-lookup"><span data-stu-id="2ca37-113">Fully qualified servername</span></span>
* <span data-ttu-id="2ca37-114">Especificar a autenticação SQL</span><span class="sxs-lookup"><span data-stu-id="2ca37-114">Specify SQL authentication</span></span>
* <span data-ttu-id="2ca37-115">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="2ca37-115">Username</span></span>
* <span data-ttu-id="2ca37-116">Senha</span><span class="sxs-lookup"><span data-stu-id="2ca37-116">Password</span></span>
* <span data-ttu-id="2ca37-117">Banco de dados padrão (opcional)</span><span class="sxs-lookup"><span data-stu-id="2ca37-117">Default database (optional)</span></span>

<span data-ttu-id="2ca37-118">Por padrão, a conexão se conecta ao banco de dados *mestre* e não ao banco de dados do usuário.</span><span class="sxs-lookup"><span data-stu-id="2ca37-118">By default your connection connects to the *master* database and not your user database.</span></span> <span data-ttu-id="2ca37-119">Para se conectar ao banco de dados do usuário, você pode optar por fazer uma de duas opções:</span><span class="sxs-lookup"><span data-stu-id="2ca37-119">To connect to your user database, you can choose to do one of two things:</span></span>

* <span data-ttu-id="2ca37-120">Especifique o banco de dados padrão ao registrar o servidor com o SQL Server Object Explorer no SSDT, SSMS ou em sua cadeia de conexão do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ca37-120">Specify the default database when registering your server with the SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="2ca37-121">Por exemplo, inclua o parâmetro InitialCatalog em uma conexão ODBC.</span><span class="sxs-lookup"><span data-stu-id="2ca37-121">For example, include the InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="2ca37-122">Destaque o banco de dados do usuário antes de criar uma sessão no SSDT.</span><span class="sxs-lookup"><span data-stu-id="2ca37-122">Highlight the user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="2ca37-123">A instrução Transact-SQL **USE MyDatabase;** não tem suporte para alterar o banco de dados para uma conexão.</span><span class="sxs-lookup"><span data-stu-id="2ca37-123">The Transact-SQL statement **USE MyDatabase;** is not supported for changing the database for a connection.</span></span> <span data-ttu-id="2ca37-124">Para obter as diretrizes de conexão ao SQL Data Warehouse com o SSDT, consulte o artigo [Consultar com o Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="2ca37-124">For guidance connecting to SQL Data Warehouse with SSDT, refer to the [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="2ca37-125">Autenticação do AAD (Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="2ca37-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="2ca37-126">A autenticação do [Azure Active Directory][What is Azure Active Directory] é um mecanismo de conexão ao SQL Data Warehouse do Microsoft Azure usando identidades no Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="2ca37-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting to Microsoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="2ca37-127">Com a autenticação do Azure Active Directory, você pode gerenciar centralmente as identidades de usuários do banco de dados e outros serviços da Microsoft em uma única localização central.</span><span class="sxs-lookup"><span data-stu-id="2ca37-127">With Azure Active Directory authentication, you can centrally manage the identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="2ca37-128">O gerenciamento central de ID fornece um único local para gerenciar usuários do SQL Data Warehouse e simplifica o gerenciamento de permissões.</span><span class="sxs-lookup"><span data-stu-id="2ca37-128">Central ID management provides a single place to manage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="2ca37-129">Benefícios</span><span class="sxs-lookup"><span data-stu-id="2ca37-129">Benefits</span></span>
<span data-ttu-id="2ca37-130">Os benefícios do Azure Active Directory incluem:</span><span class="sxs-lookup"><span data-stu-id="2ca37-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="2ca37-131">Fornece uma alternativa à autenticação do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2ca37-131">Provides an alternative to SQL Server authentication.</span></span>
* <span data-ttu-id="2ca37-132">Ajuda a interromper a proliferação de identidades de usuário entre os servidores de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2ca37-132">Helps stop the proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="2ca37-133">Permite o rodízio de senhas em um único lugar</span><span class="sxs-lookup"><span data-stu-id="2ca37-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="2ca37-134">Gerencia as permissões de banco de dados usando grupos externos (AAD).</span><span class="sxs-lookup"><span data-stu-id="2ca37-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="2ca37-135">Elimina o armazenamento de senhas permitindo a autenticação integrada do Windows e outras formas de autenticação compatíveis com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ca37-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="2ca37-136">Usa usuários de banco de dados independente para autenticar identidades no nível de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2ca37-136">Uses contained database users to authenticate identities at the database level.</span></span>
* <span data-ttu-id="2ca37-137">Dá suporte à autenticação baseada em token para aplicativos que se conectam ao SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2ca37-137">Supports token-based authentication for applications connecting to SQL Data Warehouse.</span></span>
* <span data-ttu-id="2ca37-138">Dá suporte ao Multi-Factor Authentication por meio de Autenticação Universal do Active Directory para SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="2ca37-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="2ca37-139">Para obter uma descrição de Multi-Factor Authentication, consulte [Suporte do SSMS para MFA do Azure AD com o Banco de Dados SQL e o SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2ca37-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2ca37-140">O Azure Active Directory ainda é relativamente novo e tem algumas limitações.</span><span class="sxs-lookup"><span data-stu-id="2ca37-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="2ca37-141">Para garantir que o Azure Active Directory é uma boa opção para seu ambiente, consulte [Limitações e recursos do Azure AD][Azure AD features and limitations], especificamente, as Considerações adicionais.</span><span class="sxs-lookup"><span data-stu-id="2ca37-141">To ensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically the Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="2ca37-142">Etapas da configuração</span><span class="sxs-lookup"><span data-stu-id="2ca37-142">Configuration steps</span></span>
<span data-ttu-id="2ca37-143">Siga estas etapas para configurar a autenticação do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ca37-143">Follow these steps to configure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="2ca37-144">Criar e popular um Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ca37-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="2ca37-145">Opcional: associar ou alterar o Active Directory que está associado atualmente à sua Assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="2ca37-145">Optional: Associate or change the active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="2ca37-146">Criar um administrador do Azure Active Directory para o SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="2ca37-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="2ca37-147">Configurar os computadores cliente</span><span class="sxs-lookup"><span data-stu-id="2ca37-147">Configure your client computers</span></span>
5. <span data-ttu-id="2ca37-148">Criar usuários de banco de dados independente em seu banco de dados, mapeados para identidades do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2ca37-148">Create contained database users in your database mapped to Azure AD identities</span></span>
6. <span data-ttu-id="2ca37-149">Conectar-se ao data warehouse usando identidades do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ca37-149">Connect to your data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="2ca37-150">Atualmente, os usuários do Azure Active Directory não são mostrados no Pesquisador de Objetos do SSDT.</span><span class="sxs-lookup"><span data-stu-id="2ca37-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="2ca37-151">Como alternativa, exiba os usuários em [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ca37-151">As a workaround, view the users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-the-details"></a><span data-ttu-id="2ca37-152">Localização dos detalhes</span><span class="sxs-lookup"><span data-stu-id="2ca37-152">Find the details</span></span>
* <span data-ttu-id="2ca37-153">As etapas para configurar e usar a autenticação do Azure Active Directory são quase idênticas para o Banco de Dados SQL do Azure e o SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="2ca37-153">The steps to configure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="2ca37-154">Siga as etapas detalhadas no tópico [Conexão ao Banco de Dados SQL ou ao SQL Data Warehouse usando a autenticação do Azure Active Directory](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2ca37-154">Follow the detailed steps in the topic [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="2ca37-155">Crie funções de banco de dados personalizadas e adicione usuários às funções.</span><span class="sxs-lookup"><span data-stu-id="2ca37-155">Create custom database roles and add users to the roles.</span></span> <span data-ttu-id="2ca37-156">Em seguida, conceda permissões granulares para as funções.</span><span class="sxs-lookup"><span data-stu-id="2ca37-156">Then grant granular permissions to the roles.</span></span> <span data-ttu-id="2ca37-157">Para obter mais informações, consulte o [Guia de introdução às Permissões do Mecanismo do Banco de Dados](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ca37-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ca37-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2ca37-158">Next steps</span></span>
<span data-ttu-id="2ca37-159">Para começar a consultar o data warehouse com o Visual Studio e outros aplicativos, consulte [Consultar com o Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="2ca37-159">To start querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
