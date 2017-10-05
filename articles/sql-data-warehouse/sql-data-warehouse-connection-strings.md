---
title: Drivers do SQL Data Warehouse do Azure | Microsoft Docs
description: "Cadeias de conexão e drivers para SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 5c91f423-b550-4734-8094-c7f2c418ac8d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: e71ea1d23f68ed41c03bbce88b08863d2831c1bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="drivers-for-azure-sql-data-warehouse"></a><span data-ttu-id="3b8e8-103">Drivers do Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3b8e8-103">Drivers for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="3b8e8-104">Você pode se conectar ao SQL Data Warehouse com vários protocolos de aplicativo diferentes, por exemplo, [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP] e [JDBC][JDBC].</span><span class="sxs-lookup"><span data-stu-id="3b8e8-104">You can connect to SQL Data Warehouse with several different application protocols such as, [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP] and [JDBC][JDBC].</span></span> <span data-ttu-id="3b8e8-105">A seguir estão alguns exemplos de cadeias de conexão para cada protocolo.</span><span class="sxs-lookup"><span data-stu-id="3b8e8-105">Below are some examples of connections strings for each protocol.</span></span>  <span data-ttu-id="3b8e8-106">Você também pode usar o Portal do Azure para compilar sua cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="3b8e8-106">You can also use the Azure portal to build your connection string.</span></span>  <span data-ttu-id="3b8e8-107">Para compilar a cadeia de conexão usando o Portal do Azure, navegue até a folha do banco de dados, em *Conceitos Básicos*, clique em *Mostrar cadeias de conexão de banco de dados*.</span><span class="sxs-lookup"><span data-stu-id="3b8e8-107">To build your connection string using the Azure portal, navigate to your database blade, under *Essentials* click on *Show database connection strings*.</span></span>

## <a name="sample-adonet-connection-string"></a><span data-ttu-id="3b8e8-108">Exemplo de cadeia de conexão ADO.NET</span><span class="sxs-lookup"><span data-stu-id="3b8e8-108">Sample ADO.NET connection string</span></span>
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

## <a name="sample-odbc-connection-string"></a><span data-ttu-id="3b8e8-109">Exemplo de cadeia de conexão ODBC</span><span class="sxs-lookup"><span data-stu-id="3b8e8-109">Sample ODBC connection string</span></span>
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

## <a name="sample-php-connection-string"></a><span data-ttu-id="3b8e8-110">Exemplo de cadeia de conexão PHP</span><span class="sxs-lookup"><span data-stu-id="3b8e8-110">Sample PHP connection string</span></span>
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting to SQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

## <a name="sample-jdbc-connection-string"></a><span data-ttu-id="3b8e8-111">Exemplo de cadeia de conexão JDBC</span><span class="sxs-lookup"><span data-stu-id="3b8e8-111">Sample JDBC connection string</span></span>
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

> [!NOTE]
> <span data-ttu-id="3b8e8-112">Considere definir o tempo limite de conexão para 300 segundos a fim de permitir que a conexão perdure por curtos períodos de indisponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3b8e8-112">Consider setting the connection timeout to 300 seconds in order to allow the connection to survive short periods of  unavailability.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3b8e8-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3b8e8-113">Next steps</span></span>
<span data-ttu-id="3b8e8-114">Para começar a consultar o data warehouse com o Visual Studio e outros aplicativos, consulte [Consultar com o Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="3b8e8-114">To start querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!--Image references-->

<!--Azure.com references-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md

<!--MSDN references-->
[ADO.NET]: https://msdn.microsoft.com/library/e80y5yhx(v=vs.110).aspx
[ODBC]: https://msdn.microsoft.com/library/jj730314.aspx
[PHP]: https://msdn.microsoft.com/library/cc296172.aspx?f=255&MSPPError=-2147217396
[JDBC]: https://msdn.microsoft.com/library/mt484311(v=sql.110).aspx

<!--Other references-->
