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
# <a name="connect-tooazure-sql-data-warehouse"></a>Conecte-se tooAzure SQL Data Warehouse
Este artigo ajuda você a obter tooSQL conectado do Data Warehouse Olá primeira vez.

## <a name="find-your-server-name"></a>Localizar o nome do servidor
Olá tooSQL de tooconnecting primeira etapa do Data Warehouse é saber como toofind o nome do servidor.  Por exemplo, o nome do servidor de saudação no exemplo a seguir de saudação é sample.database.windows.net. nome do servidor totalmente qualificado de Olá toofind:

1. Vá toohello [portal do Azure][Azure portal].
2. Clique em **Bancos de dados SQL** 
3. Clique no banco de dados de saudação desejado tooconnect para.
4. Localize o nome completo do servidor de saudação.
   
    ![Nome completo do servidor][1]

## <a name="supported-drivers-and-connection-strings"></a>Drivers suportados e cadeias de conexão
SQL Data Warehouse do Azure dá suporte ao [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP], e [JDBC][JDBC]. Clique em uma saudação anterior a versão mais recente dos drivers toofind hello e documentação. tooautomatically gerar a cadeia de caracteres de conexão de saudação para driver de saudação que você está usando do hello Azure portal, você pode clicar em Olá **Mostrar cadeias de conexão de banco de dados** de saudação anterior de exemplo.  A seguir também há alguns exemplos da aparência de uma cadeia de conexão para cada driver.

> [!NOTE]
> Considere definir o tempo limite do hello conexão too300 segundos tooallow toosurvive sua conexão curtos períodos de indisponibilidade.
> 
> 

### <a name="adonet-connection-string-example"></a>Exemplo de cadeia de conexão do ADO.NET
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a>Exemplo de cadeia de conexão do ODBC
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a>Exemplo de cadeia de conexão do PHP
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting tooSQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a>Exemplo de cadeia de conexão do JDBC
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a>Configurações de conexão
O SQL Data Warehouse padroniza algumas configurações durante a conexão e a criação do objeto. Essas configurações não podem ser substituídas e incluem:

| Configuração de banco de dados | Valor |
|:--- |:--- |
| [ANSI_NULLS][ANSI_NULLS] |ATIVADO |
| [QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS] |ATIVADO |
| [DATEFORMAT][DATEFORMAT] |mdy |
| [DATEFIRST][DATEFIRST] |7 |

## <a name="next-steps"></a>Próximas etapas
tooconnect e consulta com o Visual Studio, consulte [consulta com o Visual Studio][Query with Visual Studio]. toolearn mais sobre opções de autenticação, consulte [tooAzure autenticação SQL Data Warehouse][Authentication tooAzure SQL Data Warehouse].

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


