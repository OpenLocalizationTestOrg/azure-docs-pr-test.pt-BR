---
title: aaaConnect tooAzure SQL Data Warehouse | Microsoft Docs
description: "Como cadeia de conexão e o nome do servidor de saudação toofind do seu SQL Data Warehouse tooAzure"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: e52872ca-ae74-4e25-9c56-d49c85c8d0f0
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: f15e098026afb7c5efbbbfaf62b681e8cd7936bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-sql-data-warehouse"></a><span data-ttu-id="813cb-103">Conecte-se tooAzure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="813cb-103">Connect tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="813cb-104">Este artigo ajuda você a obter tooSQL conectado do Data Warehouse Olá primeira vez.</span><span class="sxs-lookup"><span data-stu-id="813cb-104">This article helps you get connected tooSQL Data Warehouse for hello first time.</span></span>

## <a name="find-your-server-name"></a><span data-ttu-id="813cb-105">Localizar o nome do servidor</span><span class="sxs-lookup"><span data-stu-id="813cb-105">Find your server name</span></span>
<span data-ttu-id="813cb-106">Olá tooSQL de tooconnecting primeira etapa do Data Warehouse é saber como toofind o nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="813cb-106">hello first step tooconnecting tooSQL Data Warehouse is knowing how toofind your server name.</span></span>  <span data-ttu-id="813cb-107">Por exemplo, o nome do servidor de saudação no exemplo a seguir de saudação é sample.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="813cb-107">For example, hello server name in hello following example is sample.database.windows.net.</span></span> <span data-ttu-id="813cb-108">nome do servidor totalmente qualificado de Olá toofind:</span><span class="sxs-lookup"><span data-stu-id="813cb-108">toofind hello fully qualified server name:</span></span>

1. <span data-ttu-id="813cb-109">Vá toohello [portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="813cb-109">Go toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="813cb-110">Clique em **Bancos de dados SQL**</span><span class="sxs-lookup"><span data-stu-id="813cb-110">Click on **SQL databases**</span></span> 
3. <span data-ttu-id="813cb-111">Clique no banco de dados de saudação desejado tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="813cb-111">Click on hello database you want tooconnect to.</span></span>
4. <span data-ttu-id="813cb-112">Localize o nome completo do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="813cb-112">Locate hello full server name.</span></span>
   
    ![Nome completo do servidor][1]

## <a name="supported-drivers-and-connection-strings"></a><span data-ttu-id="813cb-114">Drivers suportados e cadeias de conexão</span><span class="sxs-lookup"><span data-stu-id="813cb-114">Supported drivers and connection strings</span></span>
<span data-ttu-id="813cb-115">SQL Data Warehouse do Azure dá suporte ao [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP], e [JDBC][JDBC].</span><span class="sxs-lookup"><span data-stu-id="813cb-115">Azure SQL Data Warehouse supports [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP], and [JDBC][JDBC].</span></span> <span data-ttu-id="813cb-116">Clique em uma saudação anterior a versão mais recente dos drivers toofind hello e documentação.</span><span class="sxs-lookup"><span data-stu-id="813cb-116">Click on one of hello preceding drivers toofind hello latest version and documentation.</span></span> <span data-ttu-id="813cb-117">tooautomatically gerar a cadeia de caracteres de conexão de saudação para driver de saudação que você está usando do hello Azure portal, você pode clicar em Olá **Mostrar cadeias de conexão de banco de dados** de saudação anterior de exemplo.</span><span class="sxs-lookup"><span data-stu-id="813cb-117">tooautomatically generate hello connection string for hello driver that you are using from hello Azure portal, you can click on hello **Show database connection strings** from hello preceding example.</span></span>  <span data-ttu-id="813cb-118">A seguir também há alguns exemplos da aparência de uma cadeia de conexão para cada driver.</span><span class="sxs-lookup"><span data-stu-id="813cb-118">Following are also some examples of what a connection string looks like for each driver.</span></span>

> [!NOTE]
> <span data-ttu-id="813cb-119">Considere definir o tempo limite do hello conexão too300 segundos tooallow toosurvive sua conexão curtos períodos de indisponibilidade.</span><span class="sxs-lookup"><span data-stu-id="813cb-119">Consider setting hello connection timeout too300 seconds tooallow your connection toosurvive short periods of unavailability.</span></span>
> 
> 

### <a name="adonet-connection-string-example"></a><span data-ttu-id="813cb-120">Exemplo de cadeia de conexão do ADO.NET</span><span class="sxs-lookup"><span data-stu-id="813cb-120">ADO.NET connection string example</span></span>
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a><span data-ttu-id="813cb-121">Exemplo de cadeia de conexão do ODBC</span><span class="sxs-lookup"><span data-stu-id="813cb-121">ODBC connection string example</span></span>
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a><span data-ttu-id="813cb-122">Exemplo de cadeia de conexão do PHP</span><span class="sxs-lookup"><span data-stu-id="813cb-122">PHP connection string example</span></span>
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting tooSQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a><span data-ttu-id="813cb-123">Exemplo de cadeia de conexão do JDBC</span><span class="sxs-lookup"><span data-stu-id="813cb-123">JDBC connection string example</span></span>
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a><span data-ttu-id="813cb-124">Configurações de conexão</span><span class="sxs-lookup"><span data-stu-id="813cb-124">Connection settings</span></span>
<span data-ttu-id="813cb-125">O SQL Data Warehouse padroniza algumas configurações durante a conexão e a criação do objeto.</span><span class="sxs-lookup"><span data-stu-id="813cb-125">SQL Data Warehouse standardizes some settings during connection and object creation.</span></span> <span data-ttu-id="813cb-126">Essas configurações não podem ser substituídas e incluem:</span><span class="sxs-lookup"><span data-stu-id="813cb-126">These settings cannot be overridden and include:</span></span>

| <span data-ttu-id="813cb-127">Configuração de banco de dados</span><span class="sxs-lookup"><span data-stu-id="813cb-127">Database Setting</span></span> | <span data-ttu-id="813cb-128">Valor</span><span class="sxs-lookup"><span data-stu-id="813cb-128">Value</span></span> |
|:--- |:--- |
| <span data-ttu-id="813cb-129">[ANSI_NULLS][ANSI_NULLS]</span><span class="sxs-lookup"><span data-stu-id="813cb-129">[ANSI_NULLS][ANSI_NULLS]</span></span> |<span data-ttu-id="813cb-130">ATIVADO</span><span class="sxs-lookup"><span data-stu-id="813cb-130">ON</span></span> |
| <span data-ttu-id="813cb-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span><span class="sxs-lookup"><span data-stu-id="813cb-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span></span> |<span data-ttu-id="813cb-132">ATIVADO</span><span class="sxs-lookup"><span data-stu-id="813cb-132">ON</span></span> |
| <span data-ttu-id="813cb-133">[DATEFORMAT][DATEFORMAT]</span><span class="sxs-lookup"><span data-stu-id="813cb-133">[DATEFORMAT][DATEFORMAT]</span></span> |<span data-ttu-id="813cb-134">mdy</span><span class="sxs-lookup"><span data-stu-id="813cb-134">mdy</span></span> |
| <span data-ttu-id="813cb-135">[DATEFIRST][DATEFIRST]</span><span class="sxs-lookup"><span data-stu-id="813cb-135">[DATEFIRST][DATEFIRST]</span></span> |<span data-ttu-id="813cb-136">7</span><span class="sxs-lookup"><span data-stu-id="813cb-136">7</span></span> |

## <a name="next-steps"></a><span data-ttu-id="813cb-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="813cb-137">Next steps</span></span>
<span data-ttu-id="813cb-138">tooconnect e consulta com o Visual Studio, consulte [consulta com o Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="813cb-138">tooconnect and query with Visual Studio, see [Query with Visual Studio][Query with Visual Studio].</span></span> <span data-ttu-id="813cb-139">toolearn mais sobre opções de autenticação, consulte [tooAzure autenticação SQL Data Warehouse][Authentication tooAzure SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="813cb-139">toolearn more about authentication options, see [Authentication tooAzure SQL Data Warehouse][Authentication tooAzure SQL Data Warehouse].</span></span>

<!--Articles-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[ADO.NET]: https://msdn.microsoft.com/library/e80y5yhx(v=vs.110).aspx
[ODBC]: https://msdn.microsoft.com/library/jj730314.aspx
[PHP]: https://msdn.microsoft.com/library/cc296172.aspx?f=255&MSPPError=-2147217396
[JDBC]: https://msdn.microsoft.com/library/mt484311(v=sql.110).aspx
[ANSI_NULLS]: https://msdn.microsoft.com/library/ms188048.aspx
[QUOTED_IDENTIFIERS]: https://msdn.microsoft.com/library/ms174393.aspx
[DATEFORMAT]: https://msdn.microsoft.com/library/ms189491.aspx
[DATEFIRST]: https://msdn.microsoft.com/library/ms181598.aspx

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->
[1]: media/sql-data-warehouse-connect-overview/get-server-name.png


