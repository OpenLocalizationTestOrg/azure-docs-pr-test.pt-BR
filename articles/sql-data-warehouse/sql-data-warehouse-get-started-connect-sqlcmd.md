---
title: aaaConnect tooAzure SQL Data Warehouse sqlcmd | Microsoft Docs
description: "Use [sqlcmd] [sqlcmd] Utilitário de linha de comando tooconnect tooand consulta um Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 6e2b69e5-4806-4e91-9ea1-e2b63bf28c46
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 0334df7b969da1966ba29c97f835a2dc9e383e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="bd90b-103">Conecte-se tooSQL Data Warehouse com o sqlcmd</span><span class="sxs-lookup"><span data-stu-id="bd90b-103">Connect tooSQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd90b-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="bd90b-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * <span data-ttu-id="bd90b-105">
            [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="bd90b-105">[Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span></span>
> * [<span data-ttu-id="bd90b-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bd90b-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="bd90b-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="bd90b-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="bd90b-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="bd90b-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="bd90b-109">Use [sqlcmd] [ sqlcmd] utilitário de linha de comando tooconnect tooand consultar um Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bd90b-109">Use [sqlcmd][sqlcmd] command-line utility tooconnect tooand query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="bd90b-110">1. Connect</span><span class="sxs-lookup"><span data-stu-id="bd90b-110">1. Connect</span></span>
<span data-ttu-id="bd90b-111">tooget iniciado com [sqlcmd][sqlcmd], abra o prompt de comando hello e digite **sqlcmd** seguido Olá cadeia de caracteres de conexão para o banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bd90b-111">tooget started with [sqlcmd][sqlcmd], open hello command prompt and enter **sqlcmd** followed by hello connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="bd90b-112">cadeia de caracteres de conexão Olá requer Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd90b-112">hello connection string requires hello following parameters:</span></span>

* <span data-ttu-id="bd90b-113">**Servidor (-S):** servidor na forma de saudação `<`nome do servidor`>`. t</span><span class="sxs-lookup"><span data-stu-id="bd90b-113">**Server (-S):** Server in hello form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="bd90b-114">**Banco de dados (-d):** nome do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="bd90b-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="bd90b-115">**Habilitar identificadores entre aspas (-I):** identificadores entre aspas devem ser uma instância de SQL Data Warehouse tooa tooconnect habilitado.</span><span class="sxs-lookup"><span data-stu-id="bd90b-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled tooconnect tooa SQL Data Warehouse instance.</span></span>

<span data-ttu-id="bd90b-116">toouse autenticação do SQL Server, você precisa de parâmetros de nome de usuário/senha Olá tooadd:</span><span class="sxs-lookup"><span data-stu-id="bd90b-116">toouse SQL Server Authentication, you need tooadd hello username/password parameters:</span></span>

* <span data-ttu-id="bd90b-117">**Usuário (-U):** usuário na forma de saudação do servidor `<`usuário`>`</span><span class="sxs-lookup"><span data-stu-id="bd90b-117">**User (-U):** Server user in hello form `<`User`>`</span></span>
* <span data-ttu-id="bd90b-118">**Senha (-P):** senha associada usuário hello.</span><span class="sxs-lookup"><span data-stu-id="bd90b-118">**Password (-P):** Password associated with hello user.</span></span>

<span data-ttu-id="bd90b-119">Por exemplo, sua cadeia de caracteres de conexão pode parecer com hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd90b-119">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="bd90b-120">toouse a autenticação integrada do Active Directory do Azure, você precisa de parâmetros de Active Directory do Azure Olá tooadd:</span><span class="sxs-lookup"><span data-stu-id="bd90b-120">toouse Azure Active Directory Integrated authentication, you need tooadd hello Azure Active Directory parameters:</span></span>

* <span data-ttu-id="bd90b-121">**Autenticação do Azure Active Directory (-G):** usar o Azure Active Directory para a autenticação</span><span class="sxs-lookup"><span data-stu-id="bd90b-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="bd90b-122">Por exemplo, sua cadeia de caracteres de conexão pode parecer com hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd90b-122">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="bd90b-123">É necessário muito[habilitar autenticação do Active Directory do Azure](sql-data-warehouse-authentication.md) tooauthenticate usando o Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bd90b-123">You need too[enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) tooauthenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="bd90b-124">2. Consultar</span><span class="sxs-lookup"><span data-stu-id="bd90b-124">2. Query</span></span>
<span data-ttu-id="bd90b-125">Após a conexão, você pode executar qualquer instrução Transact-SQL com suporte na instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd90b-125">After connection, you can issue any supported Transact-SQL statements against hello instance.</span></span>  <span data-ttu-id="bd90b-126">Neste exemplo, as consultas são enviadas no modo interativo.</span><span class="sxs-lookup"><span data-stu-id="bd90b-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="bd90b-127">Esses exemplos a seguir mostram como você pode executar as consultas em modo de lote usando a opção -Q de saudação ou direcionando o toosqlcmd SQL.</span><span class="sxs-lookup"><span data-stu-id="bd90b-127">These next examples show how you can run your queries in batch mode using hello -Q option or piping your SQL toosqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="bd90b-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bd90b-128">Next steps</span></span>
<span data-ttu-id="bd90b-129">Consulte [sqlcmd documentação] [ sqlcmd] para obter mais informações sobre detalhes sobre as opções de saudação disponíveis no sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="bd90b-129">See [sqlcmd documentation][sqlcmd] for more about details about hello options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
