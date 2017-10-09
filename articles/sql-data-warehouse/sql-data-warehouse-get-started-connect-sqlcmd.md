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
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a>Conecte-se tooSQL Data Warehouse com o sqlcmd
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * 
            [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Use [sqlcmd] [ sqlcmd] utilitário de linha de comando tooconnect tooand consultar um Azure SQL Data Warehouse.  

## <a name="1-connect"></a>1. Connect
tooget iniciado com [sqlcmd][sqlcmd], abra o prompt de comando hello e digite **sqlcmd** seguido Olá cadeia de caracteres de conexão para o banco de dados do SQL Data Warehouse. cadeia de caracteres de conexão Olá requer Olá parâmetros a seguir:

* **Servidor (-S):** servidor na forma de saudação `<`nome do servidor`>`. t
* **Banco de dados (-d):** nome do banco de dados.
* **Habilitar identificadores entre aspas (-I):** identificadores entre aspas devem ser uma instância de SQL Data Warehouse tooa tooconnect habilitado.

toouse autenticação do SQL Server, você precisa de parâmetros de nome de usuário/senha Olá tooadd:

* **Usuário (-U):** usuário na forma de saudação do servidor `<`usuário`>`
* **Senha (-P):** senha associada usuário hello.

Por exemplo, sua cadeia de caracteres de conexão pode parecer com hello a seguir:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

toouse a autenticação integrada do Active Directory do Azure, você precisa de parâmetros de Active Directory do Azure Olá tooadd:

* **Autenticação do Azure Active Directory (-G):** usar o Azure Active Directory para a autenticação

Por exemplo, sua cadeia de caracteres de conexão pode parecer com hello a seguir:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> É necessário muito[habilitar autenticação do Active Directory do Azure](sql-data-warehouse-authentication.md) tooauthenticate usando o Active Directory.
> 
> 

## <a name="2-query"></a>2. Consultar
Após a conexão, você pode executar qualquer instrução Transact-SQL com suporte na instância de saudação.  Neste exemplo, as consultas são enviadas no modo interativo.

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

Esses exemplos a seguir mostram como você pode executar as consultas em modo de lote usando a opção -Q de saudação ou direcionando o toosqlcmd SQL.

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a>Próximas etapas
Consulte [sqlcmd documentação] [ sqlcmd] para obter mais informações sobre detalhes sobre as opções de saudação disponíveis no sqlcmd.

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
