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
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a><span data-ttu-id="7364b-103">Migrar seu banco de dados PostgreSQL usando despejar e restaurar</span><span class="sxs-lookup"><span data-stu-id="7364b-103">Migrate your PostgreSQL database using dump and restore</span></span>
<span data-ttu-id="7364b-104">Você pode usar [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract um banco de dados PostgreSQL em um arquivo de despejo de memória e [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore de dados PostgreSQL Olá de um arquivo criado pelo pg_dump.</span><span class="sxs-lookup"><span data-stu-id="7364b-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a dump file and [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore hello PostgreSQL database from an archive file created by pg_dump.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7364b-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7364b-105">Prerequisites</span></span>
<span data-ttu-id="7364b-106">toostep por este tooguide como, você precisa:</span><span class="sxs-lookup"><span data-stu-id="7364b-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="7364b-107">Um [banco de dados do Azure para o servidor PostgreSQL](quickstart-create-server-database-portal.md) com acesso de tooallow de regras de firewall e de banco de dados sob ele.</span><span class="sxs-lookup"><span data-stu-id="7364b-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="7364b-108">Utilitários de linha de comando [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) e [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) instalados</span><span class="sxs-lookup"><span data-stu-id="7364b-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) and [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) command-line utilities installed</span></span>

<span data-ttu-id="7364b-109">Siga estas etapas toodump e restaurar seu banco de dados PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="7364b-109">Follow these steps toodump and restore your PostgreSQL database:</span></span>

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="7364b-110">Criar um arquivo de despejo de memória usando pg_dump que contém a saudação dados toobe carregado</span><span class="sxs-lookup"><span data-stu-id="7364b-110">Create a dump file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="7364b-111">tooback a um existente PostgreSQL local do banco de dados ou em uma VM, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7364b-111">tooback up an existing PostgreSQL database on-premises or in a VM, run hello following command:</span></span>
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
<span data-ttu-id="7364b-112">Por exemplo, se você tiver um servidor local e um banco de dados chamado **testdb** nele</span><span class="sxs-lookup"><span data-stu-id="7364b-112">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a><span data-ttu-id="7364b-113">Restaurar dados de saudação no banco de dados de destino, Olá para PostrgeSQL usando pg_restore</span><span class="sxs-lookup"><span data-stu-id="7364b-113">Restore hello data into hello target Azure Database for PostrgeSQL using pg_restore</span></span>
<span data-ttu-id="7364b-114">Depois que você criou o banco de dados de destino hello, você pode usar o comando de pg_restore hello e Olá -d, dados de saudação do – dbname parâmetro toorestore no banco de dados de destino de saudação do arquivo de despejo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7364b-114">Once you have created hello target database, you can use hello pg_restore command and hello -d, --dbname parameter toorestore hello data into hello target database from hello dump file.</span></span>
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
<span data-ttu-id="7364b-115">Neste exemplo, restaurar dados de saudação do arquivo de despejo Olá **testdb.dump** no banco de dados de saudação **mypgsqldb** no servidor de destino **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="7364b-115">In this example, restore hello data from hello dump file **testdb.dump** into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a><span data-ttu-id="7364b-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7364b-116">Next steps</span></span>
- <span data-ttu-id="7364b-117">toomigrate um banco de dados PostgreSQL usando exportação e importação, consulte [migrar seu banco de dados PostgreSQL exportar e importar](howto-migrate-using-export-and-import.md)</span><span class="sxs-lookup"><span data-stu-id="7364b-117">toomigrate a PostgreSQL database using export and import, see [Migrate your PostgreSQL database using export and import](howto-migrate-using-export-and-import.md)</span></span>
