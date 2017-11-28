---
title: Conectar-se ao sqlcmd do SQL Data Warehouse do Azure | Microsoft Docs
description: "Use o utilitário de linha de comando [sqlcmd][sqlcmd] para conectar-se ao SQL Data Warehouse do Azure e fazer uma consulta."
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
ms.openlocfilehash: 5a3fe1046c3417070ba8ff5bd18a0485e2152eff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="16afd-103">Conecte-se ao SQL Data Warehouse com sqlcmd</span><span class="sxs-lookup"><span data-stu-id="16afd-103">Connect to SQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="16afd-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="16afd-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * <span data-ttu-id="16afd-105">
            [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="16afd-105">[Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span></span>
> * [<span data-ttu-id="16afd-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16afd-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="16afd-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="16afd-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="16afd-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="16afd-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="16afd-109">Use o utilitário de linha de comando [sqlcmd][sqlcmd] para conectar-se ao SQL Data Warehouse do Azure e fazer uma consulta.</span><span class="sxs-lookup"><span data-stu-id="16afd-109">Use [sqlcmd][sqlcmd] command-line utility to connect to and query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="16afd-110">1. Connect</span><span class="sxs-lookup"><span data-stu-id="16afd-110">1. Connect</span></span>
<span data-ttu-id="16afd-111">Para começar com o [sqlcmd][sqlcmd], abra o prompt de comando e digite **sqlcmd** seguido da cadeia de conexão do banco de dados SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="16afd-111">To get started with [sqlcmd][sqlcmd], open the command prompt and enter **sqlcmd** followed by the connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="16afd-112">A cadeia de conexão precisará dos seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="16afd-112">The connection string requires the following parameters:</span></span>

* <span data-ttu-id="16afd-113">**Servidor (-S):** Servidor no formato `<`Nome do Servidor`>`.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="16afd-113">**Server (-S):** Server in the form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="16afd-114">**Banco de dados (-d):** nome do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="16afd-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="16afd-115">**Habilitar Identificadores com Cotas (-I):** os identificadores com cotas devem ser habilitados para conectarem uma instância do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="16afd-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled to connect to a SQL Data Warehouse instance.</span></span>

<span data-ttu-id="16afd-116">Para usar a Autenticação do SQL Server, você precisa adicionar os parâmetros do nome de usuário/senha:</span><span class="sxs-lookup"><span data-stu-id="16afd-116">To use SQL Server Authentication, you need to add the username/password parameters:</span></span>

* <span data-ttu-id="16afd-117">**Usuário (-U):** usuário do servidor no formato `<`Usuário`>`</span><span class="sxs-lookup"><span data-stu-id="16afd-117">**User (-U):** Server user in the form `<`User`>`</span></span>
* <span data-ttu-id="16afd-118">**Senha (-P):** senha associada ao usuário.</span><span class="sxs-lookup"><span data-stu-id="16afd-118">**Password (-P):** Password associated with the user.</span></span>

<span data-ttu-id="16afd-119">Por exemplo, a cadeia de conexão pode parecer com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="16afd-119">For example, your connection string might look like the following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="16afd-120">Para usar a autenticação Integrada do Azure Active Directory, você precisa adicionar os parâmetros do Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="16afd-120">To use Azure Active Directory Integrated authentication, you need to add the Azure Active Directory parameters:</span></span>

* <span data-ttu-id="16afd-121">**Autenticação do Azure Active Directory (-G):** usar o Azure Active Directory para a autenticação</span><span class="sxs-lookup"><span data-stu-id="16afd-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="16afd-122">Por exemplo, a cadeia de conexão pode parecer com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="16afd-122">For example, your connection string might look like the following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="16afd-123">Você precisa [habilitar a Autenticação do Azure Active Directory](sql-data-warehouse-authentication.md) para autenticar usando o Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16afd-123">You need to [enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) to authenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="16afd-124">2. Consultar</span><span class="sxs-lookup"><span data-stu-id="16afd-124">2. Query</span></span>
<span data-ttu-id="16afd-125">Após a conexão, você pode executar quaisquer instruções Transact-SQL compatíveis com a instância.</span><span class="sxs-lookup"><span data-stu-id="16afd-125">After connection, you can issue any supported Transact-SQL statements against the instance.</span></span>  <span data-ttu-id="16afd-126">Neste exemplo, as consultas são enviadas no modo interativo.</span><span class="sxs-lookup"><span data-stu-id="16afd-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="16afd-127">Os próximos exemplos mostram como você pode executar as consultas no modo de lote usando a opção -Q ou direcionando o SQL para sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="16afd-127">These next examples show how you can run your queries in batch mode using the -Q option or piping your SQL to sqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="16afd-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="16afd-128">Next steps</span></span>
<span data-ttu-id="16afd-129">Confira a [documentação do sqlcmd][sqlcmd] para obter mais detalhes sobre as opções disponíveis no sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="16afd-129">See [sqlcmd documentation][sqlcmd] for more about details about the options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
