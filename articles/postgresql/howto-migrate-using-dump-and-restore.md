---
title: "aaaHow tooDump e restauração no banco de dados do Azure para PostgreSQL | Microsoft Docs"
description: "Descreve como tooextract um PostgreSQL banco de dados em um arquivo de despejo de memória e de dados PostgreSQL Olá restauração de um arquivo criado pelo pg_dump no banco de dados do Azure para PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 9ad28e9dec3927b0f80b5e6bab6423cc944f5156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a>Migrar seu banco de dados PostgreSQL usando despejar e restaurar
Você pode usar [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract um banco de dados PostgreSQL em um arquivo de despejo de memória e [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore de dados PostgreSQL Olá de um arquivo criado pelo pg_dump.

## <a name="prerequisites"></a>Pré-requisitos
toostep por este tooguide como, você precisa:
- Um [banco de dados do Azure para o servidor PostgreSQL](quickstart-create-server-database-portal.md) com acesso de tooallow de regras de firewall e de banco de dados sob ele.
- Utilitários de linha de comando [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) e [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) instalados

Siga estas etapas toodump e restaurar seu banco de dados PostgreSQL:

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Criar um arquivo de despejo de memória usando pg_dump que contém a saudação dados toobe carregado
tooback a um existente PostgreSQL local do banco de dados ou em uma VM, execute Olá comando a seguir:
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
Por exemplo, se você tiver um servidor local e um banco de dados chamado **testdb** nele
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a>Restaurar dados de saudação no banco de dados de destino, Olá para PostrgeSQL usando pg_restore
Depois que você criou o banco de dados de destino hello, você pode usar o comando de pg_restore hello e Olá -d, dados de saudação do – dbname parâmetro toorestore no banco de dados de destino de saudação do arquivo de despejo de saudação.
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
Neste exemplo, restaurar dados de saudação do arquivo de despejo Olá **testdb.dump** no banco de dados de saudação **mypgsqldb** no servidor de destino **mypgserver-20170401.postgres.database.azure.com**.
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a>Próximas etapas
- toomigrate um banco de dados PostgreSQL usando exportação e importação, consulte [migrar seu banco de dados PostgreSQL exportar e importar](howto-migrate-using-export-and-import.md)
