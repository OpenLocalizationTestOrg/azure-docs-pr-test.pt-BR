---
title: Conectar-se ao SQL Data Warehouse do Azure | Microsoft Docs
description: "Como localizar o servidor de nome e a cadeia de conexão para o Azure SQL Data Warehouse"
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
ms.openlocfilehash: 72c2b404e66611da421eca0dc30aa71e18c6d120
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-azure-sql-data-warehouse"></a><span data-ttu-id="ef616-103">Conectar-se ao SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="ef616-103">Connect to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="ef616-104">Este artigo ajuda você a conectar o SQL Data Warehouse pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="ef616-104">This article helps you get connected to SQL Data Warehouse for the first time.</span></span>

## <a name="find-your-server-name"></a><span data-ttu-id="ef616-105">Localizar o nome do servidor</span><span class="sxs-lookup"><span data-stu-id="ef616-105">Find your server name</span></span>
<span data-ttu-id="ef616-106">A primeira etapa para conectar o SQL Data Warehouse é saber como localizar o nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="ef616-106">The first step to connecting to SQL Data Warehouse is knowing how to find your server name.</span></span>  <span data-ttu-id="ef616-107">Por exemplo, o nome do servidor no exemplo a seguir é sample.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="ef616-107">For example, the server name in the following example is sample.database.windows.net.</span></span> <span data-ttu-id="ef616-108">Para localizar o nome de servidor totalmente qualificado:</span><span class="sxs-lookup"><span data-stu-id="ef616-108">To find the fully qualified server name:</span></span>

1. <span data-ttu-id="ef616-109">Acesse o [Portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="ef616-109">Go to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="ef616-110">Clique em **Bancos de dados SQL**</span><span class="sxs-lookup"><span data-stu-id="ef616-110">Click on **SQL databases**</span></span> 
3. <span data-ttu-id="ef616-111">Clique no banco de dados que você deseja conectar.</span><span class="sxs-lookup"><span data-stu-id="ef616-111">Click on the database you want to connect to.</span></span>
4. <span data-ttu-id="ef616-112">Localize o nome completo do servidor.</span><span class="sxs-lookup"><span data-stu-id="ef616-112">Locate the full server name.</span></span>
   
    ![Nome completo do servidor][1]

## <a name="supported-drivers-and-connection-strings"></a><span data-ttu-id="ef616-114">Drivers suportados e cadeias de conexão</span><span class="sxs-lookup"><span data-stu-id="ef616-114">Supported drivers and connection strings</span></span>
<span data-ttu-id="ef616-115">SQL Data Warehouse do Azure dá suporte ao [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP], e [JDBC][JDBC].</span><span class="sxs-lookup"><span data-stu-id="ef616-115">Azure SQL Data Warehouse supports [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP], and [JDBC][JDBC].</span></span> <span data-ttu-id="ef616-116">Clique em um dos drivers anteriores para localizar a versão mais recente e a documentação.</span><span class="sxs-lookup"><span data-stu-id="ef616-116">Click on one of the preceding drivers to find the latest version and documentation.</span></span> <span data-ttu-id="ef616-117">Para gerar automaticamente a cadeia de conexão para o driver que você está usando no portal do Azure, você pode clicar em **Mostrar cadeias de conexão do banco de dados** no exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="ef616-117">To automatically generate the connection string for the driver that you are using from the Azure portal, you can click on the **Show database connection strings** from the preceding example.</span></span>  <span data-ttu-id="ef616-118">A seguir também há alguns exemplos da aparência de uma cadeia de conexão para cada driver.</span><span class="sxs-lookup"><span data-stu-id="ef616-118">Following are also some examples of what a connection string looks like for each driver.</span></span>

> [!NOTE]
> <span data-ttu-id="ef616-119">Considere definir o tempo limite de conexão para 300 segundos a fim de permitir que a conexão perdure em curtos períodos de indisponibilidade.</span><span class="sxs-lookup"><span data-stu-id="ef616-119">Consider setting the connection timeout to 300 seconds to allow your connection to survive short periods of unavailability.</span></span>
> 
> 

### <a name="adonet-connection-string-example"></a><span data-ttu-id="ef616-120">Exemplo de cadeia de conexão do ADO.NET</span><span class="sxs-lookup"><span data-stu-id="ef616-120">ADO.NET connection string example</span></span>
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a><span data-ttu-id="ef616-121">Exemplo de cadeia de conexão do ODBC</span><span class="sxs-lookup"><span data-stu-id="ef616-121">ODBC connection string example</span></span>
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a><span data-ttu-id="ef616-122">Exemplo de cadeia de conexão do PHP</span><span class="sxs-lookup"><span data-stu-id="ef616-122">PHP connection string example</span></span>
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting to SQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a><span data-ttu-id="ef616-123">Exemplo de cadeia de conexão do JDBC</span><span class="sxs-lookup"><span data-stu-id="ef616-123">JDBC connection string example</span></span>
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a><span data-ttu-id="ef616-124">Configurações de conexão</span><span class="sxs-lookup"><span data-stu-id="ef616-124">Connection settings</span></span>
<span data-ttu-id="ef616-125">O SQL Data Warehouse padroniza algumas configurações durante a conexão e a criação do objeto.</span><span class="sxs-lookup"><span data-stu-id="ef616-125">SQL Data Warehouse standardizes some settings during connection and object creation.</span></span> <span data-ttu-id="ef616-126">Essas configurações não podem ser substituídas e incluem:</span><span class="sxs-lookup"><span data-stu-id="ef616-126">These settings cannot be overridden and include:</span></span>

| <span data-ttu-id="ef616-127">Configuração de banco de dados</span><span class="sxs-lookup"><span data-stu-id="ef616-127">Database Setting</span></span> | <span data-ttu-id="ef616-128">Valor</span><span class="sxs-lookup"><span data-stu-id="ef616-128">Value</span></span> |
|:--- |:--- |
| <span data-ttu-id="ef616-129">[ANSI_NULLS][ANSI_NULLS]</span><span class="sxs-lookup"><span data-stu-id="ef616-129">[ANSI_NULLS][ANSI_NULLS]</span></span> |<span data-ttu-id="ef616-130">ATIVADO</span><span class="sxs-lookup"><span data-stu-id="ef616-130">ON</span></span> |
| <span data-ttu-id="ef616-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span><span class="sxs-lookup"><span data-stu-id="ef616-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span></span> |<span data-ttu-id="ef616-132">ATIVADO</span><span class="sxs-lookup"><span data-stu-id="ef616-132">ON</span></span> |
| <span data-ttu-id="ef616-133">[DATEFORMAT][DATEFORMAT]</span><span class="sxs-lookup"><span data-stu-id="ef616-133">[DATEFORMAT][DATEFORMAT]</span></span> |<span data-ttu-id="ef616-134">mdy</span><span class="sxs-lookup"><span data-stu-id="ef616-134">mdy</span></span> |
| <span data-ttu-id="ef616-135">[DATEFIRST][DATEFIRST]</span><span class="sxs-lookup"><span data-stu-id="ef616-135">[DATEFIRST][DATEFIRST]</span></span> |<span data-ttu-id="ef616-136">7</span><span class="sxs-lookup"><span data-stu-id="ef616-136">7</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ef616-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ef616-137">Next steps</span></span>
<span data-ttu-id="ef616-138">Para se conectar e consultar com o Visual Studio, confira [Consultar com o Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="ef616-138">To connect and query with Visual Studio, see [Query with Visual Studio][Query with Visual Studio].</span></span> <span data-ttu-id="ef616-139">Para saber mais sobre as opções de autenticação, confira [Autenticação no SQL Data Warehouse do Azure][Authentication to Azure SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="ef616-139">To learn more about authentication options, see [Authentication to Azure SQL Data Warehouse][Authentication to Azure SQL Data Warehouse].</span></span>

<!--Articles-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[Authentication to Azure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md

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


