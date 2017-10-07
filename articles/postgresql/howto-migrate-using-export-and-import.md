---
title: "aaaMigrate usando um banco de dados de importação e exportação no banco de dados do Azure para PostgreSQL | Microsoft Docs"
description: "Descreve como extrair um banco de dados PostgreSQL em um arquivo de script e importar dados de saudação para o banco de dados de destino de saudação do arquivo."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5ca4650782b02e1067c5a8a3710f2dfbc8c76063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a>Migrar seu banco de dados PostgreSQL usando exportar e importar
Você pode usar [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract um banco de dados PostgreSQL em um arquivo de script e [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport dados de saudação no banco de dados de destino de saudação do arquivo.

## <a name="prerequisites"></a>Pré-requisitos
toostep por este tooguide como, você precisa:
- Um [banco de dados do Azure para o servidor PostgreSQL](quickstart-create-server-database-portal.md) com acesso de tooallow de regras de firewall e de banco de dados sob ele.
- O utilitário de linha de comando [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) instalado
- O utilitário de linha de comando [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) instalado

Siga estas etapas tooexport e importar o banco de dados PostgreSQL.

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Criar um arquivo de script usando pg_dump que contém a saudação dados toobe carregado
tooexport seu PostgreSQL existente no local do banco de dados ou em um arquivo de script do VM tooa sql, execute Olá comando no seu ambiente a seguir:
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
Por exemplo, se você tiver um servidor local e um banco de dados chamado **testdb** nele
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a>Importar dados de saudação no banco de dados de destino para PostrgeSQL
Você pode usar a linha de comando psql hello e Olá -d, dados de saudação do – dbname parâmetro tooimport no banco de dados do Azure para PostrgeSQL é criado e carregar dados do arquivo de saudação do sql.
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
Este exemplo usa o utilitário psql e um arquivo de script chamado **testdb.sql** de dados de tooimport etapa anterior no banco de dados de saudação **mypgsqldb** no servidor de destino  **mypgserver 20170401.postgres.database.azure.com**.
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a>Próximas etapas
- toomigrate um banco de dados PostgreSQL usando dump e restore, consulte [migrar seu banco de dados PostgreSQL usando dump e restore](howto-migrate-using-dump-and-restore.md)
