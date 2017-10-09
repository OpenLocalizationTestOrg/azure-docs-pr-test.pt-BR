---
title: aaaAuthentication tooAzure SQL Data Warehouse | Microsoft Docs
description: Azure Active Directory (AAD) e SQL Server authentication tooAzure SQL Data Warehouse.
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
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a><span data-ttu-id="31c8a-103">Autenticação tooAzure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="31c8a-103">Authentication tooAzure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="31c8a-104">Visão Geral da Segurança</span><span class="sxs-lookup"><span data-stu-id="31c8a-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="31c8a-105">Autenticação</span><span class="sxs-lookup"><span data-stu-id="31c8a-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="31c8a-106">Criptografia (Portal)</span><span class="sxs-lookup"><span data-stu-id="31c8a-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="31c8a-107">Criptografia (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="31c8a-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="31c8a-108">tooconnect tooSQL Data Warehouse, você deve passar as credenciais de segurança para fins de autenticação.</span><span class="sxs-lookup"><span data-stu-id="31c8a-108">tooconnect tooSQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="31c8a-109">Após estabelecer uma conexão, determinadas configurações de conexão são definidas como parte do estabelecimento de sua sessão de consulta.</span><span class="sxs-lookup"><span data-stu-id="31c8a-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="31c8a-110">Para obter mais informações sobre segurança e como tooenable conexões tooyour do data warehouse, consulte [proteger um banco de dados no Data Warehouse SQL][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="31c8a-110">For more information on security and how tooenable connections tooyour data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="31c8a-111">Autenticação do SQL</span><span class="sxs-lookup"><span data-stu-id="31c8a-111">SQL authentication</span></span>
<span data-ttu-id="31c8a-112">tooconnect tooSQL Data Warehouse, você deve fornecer Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="31c8a-112">tooconnect tooSQL Data Warehouse, you must provide hello following information:</span></span>

* <span data-ttu-id="31c8a-113">Nome totalmente qualificado do servidor</span><span class="sxs-lookup"><span data-stu-id="31c8a-113">Fully qualified servername</span></span>
* <span data-ttu-id="31c8a-114">Especificar a autenticação SQL</span><span class="sxs-lookup"><span data-stu-id="31c8a-114">Specify SQL authentication</span></span>
* <span data-ttu-id="31c8a-115">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="31c8a-115">Username</span></span>
* <span data-ttu-id="31c8a-116">Senha</span><span class="sxs-lookup"><span data-stu-id="31c8a-116">Password</span></span>
* <span data-ttu-id="31c8a-117">Banco de dados padrão (opcional)</span><span class="sxs-lookup"><span data-stu-id="31c8a-117">Default database (optional)</span></span>

<span data-ttu-id="31c8a-118">Por padrão, sua conexão conecta toohello *mestre* banco de dados e não o banco de dados do usuário.</span><span class="sxs-lookup"><span data-stu-id="31c8a-118">By default your connection connects toohello *master* database and not your user database.</span></span> <span data-ttu-id="31c8a-119">dados de usuário de tooyour tooconnect, você pode escolher toodo uma das duas coisas:</span><span class="sxs-lookup"><span data-stu-id="31c8a-119">tooconnect tooyour user database, you can choose toodo one of two things:</span></span>

* <span data-ttu-id="31c8a-120">Especifique o banco de dados de padrão de saudação ao registrar seu servidor com hello Pesquisador de objetos do SQL Server no SSDT, SSMS, ou em sua cadeia de conexão do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="31c8a-120">Specify hello default database when registering your server with hello SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="31c8a-121">Por exemplo, inclua parâmetro InitialCatalog Olá uma conexão ODBC.</span><span class="sxs-lookup"><span data-stu-id="31c8a-121">For example, include hello InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="31c8a-122">Realce o banco de dados de usuário de saudação antes de criar uma sessão no SSDT.</span><span class="sxs-lookup"><span data-stu-id="31c8a-122">Highlight hello user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="31c8a-123">Olá instrução Transact-SQL **USE MyDatabase;** não tem suporte para alterar o banco de dados de saudação para uma conexão.</span><span class="sxs-lookup"><span data-stu-id="31c8a-123">hello Transact-SQL statement **USE MyDatabase;** is not supported for changing hello database for a connection.</span></span> <span data-ttu-id="31c8a-124">Para obter orientações sobre como conectar-se tooSQL Data Warehouse com o SSDT, consulte toohello [consulta com o Visual Studio] [ Query with Visual Studio] artigo.</span><span class="sxs-lookup"><span data-stu-id="31c8a-124">For guidance connecting tooSQL Data Warehouse with SSDT, refer toohello [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="31c8a-125">Autenticação do AAD (Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="31c8a-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="31c8a-126">[Active Directory do Azure] [ What is Azure Active Directory] autenticação é um mecanismo tooMicrosoft Azure SQL Data Warehouse para se conectar usando as identidades no Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="31c8a-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting tooMicrosoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="31c8a-127">Com a autenticação do Active Directory do Azure, você pode gerenciar centralmente as identidades de saudação de usuários de banco de dados e outros serviços da Microsoft em um local central.</span><span class="sxs-lookup"><span data-stu-id="31c8a-127">With Azure Active Directory authentication, you can centrally manage hello identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="31c8a-128">Central de gerenciamento de ID oferece um único local de usuários do SQL Data Warehouse toomanage e simplifica o gerenciamento de permissões.</span><span class="sxs-lookup"><span data-stu-id="31c8a-128">Central ID management provides a single place toomanage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="31c8a-129">Benefícios</span><span class="sxs-lookup"><span data-stu-id="31c8a-129">Benefits</span></span>
<span data-ttu-id="31c8a-130">Os benefícios do Azure Active Directory incluem:</span><span class="sxs-lookup"><span data-stu-id="31c8a-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="31c8a-131">Fornece uma autenticação de servidor tooSQL alternativo.</span><span class="sxs-lookup"><span data-stu-id="31c8a-131">Provides an alternative tooSQL Server authentication.</span></span>
* <span data-ttu-id="31c8a-132">Ajuda a parar a proliferação de saudação de identidades de usuário entre os servidores de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="31c8a-132">Helps stop hello proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="31c8a-133">Permite o rodízio de senhas em um único lugar</span><span class="sxs-lookup"><span data-stu-id="31c8a-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="31c8a-134">Gerencia as permissões de banco de dados usando grupos externos (AAD).</span><span class="sxs-lookup"><span data-stu-id="31c8a-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="31c8a-135">Elimina o armazenamento de senhas permitindo a autenticação integrada do Windows e outras formas de autenticação compatíveis com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="31c8a-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="31c8a-136">Usa contidos identidades de tooauthenticate de usuários de banco de dados no nível de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="31c8a-136">Uses contained database users tooauthenticate identities at hello database level.</span></span>
* <span data-ttu-id="31c8a-137">Oferece suporte à autenticação baseada em token para aplicativos que se conectam tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="31c8a-137">Supports token-based authentication for applications connecting tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="31c8a-138">Dá suporte ao Multi-Factor Authentication por meio de Autenticação Universal do Active Directory para SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="31c8a-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="31c8a-139">Para obter uma descrição de Multi-Factor Authentication, consulte [Suporte do SSMS para MFA do Azure AD com o Banco de Dados SQL e o SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="31c8a-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="31c8a-140">O Azure Active Directory ainda é relativamente novo e tem algumas limitações.</span><span class="sxs-lookup"><span data-stu-id="31c8a-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="31c8a-141">tooensure Active Directory do Azure é uma boa opção para seu ambiente, consulte [recursos do AD do Azure e limitações][Azure AD features and limitations], especificamente Olá considerações adicionais.</span><span class="sxs-lookup"><span data-stu-id="31c8a-141">tooensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically hello Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="31c8a-142">Etapas da configuração</span><span class="sxs-lookup"><span data-stu-id="31c8a-142">Configuration steps</span></span>
<span data-ttu-id="31c8a-143">Execute a autenticação do Active Directory do Azure essas etapas tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="31c8a-143">Follow these steps tooconfigure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="31c8a-144">Criar e popular um Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31c8a-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="31c8a-145">Opcional: Associar ou alterar Olá active directory que está associado a sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="31c8a-145">Optional: Associate or change hello active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="31c8a-146">Criar um administrador do Azure Active Directory para o SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="31c8a-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="31c8a-147">Configurar os computadores cliente</span><span class="sxs-lookup"><span data-stu-id="31c8a-147">Configure your client computers</span></span>
5. <span data-ttu-id="31c8a-148">Criar usuários de banco de dados independente em seu banco de dados mapeado tooAzure identidades do AD</span><span class="sxs-lookup"><span data-stu-id="31c8a-148">Create contained database users in your database mapped tooAzure AD identities</span></span>
6. <span data-ttu-id="31c8a-149">Conectar-se a data warehouse de tooyour usando identidades do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="31c8a-149">Connect tooyour data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="31c8a-150">Atualmente, os usuários do Azure Active Directory não são mostrados no Pesquisador de Objetos do SSDT.</span><span class="sxs-lookup"><span data-stu-id="31c8a-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="31c8a-151">Como alternativa, exibir os usuários Olá [database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="31c8a-151">As a workaround, view hello users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-hello-details"></a><span data-ttu-id="31c8a-152">Localizar detalhes de saudação</span><span class="sxs-lookup"><span data-stu-id="31c8a-152">Find hello details</span></span>
* <span data-ttu-id="31c8a-153">autenticação do Active Directory do Azure Olá etapas tooconfigure e uso são quase idênticas para o banco de dados do SQL Azure e o Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="31c8a-153">hello steps tooconfigure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="31c8a-154">Siga Olá detalhadas etapas no tópico Olá [tooSQL conectando banco de dados ou o SQL Data Warehouse por usando o Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="31c8a-154">Follow hello detailed steps in hello topic [Connecting tooSQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="31c8a-155">Criar funções de banco de dados personalizados e adicionar usuários toohello funções.</span><span class="sxs-lookup"><span data-stu-id="31c8a-155">Create custom database roles and add users toohello roles.</span></span> <span data-ttu-id="31c8a-156">Em seguida, conceda permissões granulares toohello funções.</span><span class="sxs-lookup"><span data-stu-id="31c8a-156">Then grant granular permissions toohello roles.</span></span> <span data-ttu-id="31c8a-157">Para obter mais informações, consulte o [Guia de introdução às Permissões do Mecanismo do Banco de Dados](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="31c8a-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31c8a-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="31c8a-158">Next steps</span></span>
<span data-ttu-id="31c8a-159">toostart consultando o data warehouse com o Visual Studio e outros aplicativos, consulte [consulta com o Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="31c8a-159">toostart querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
