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
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="fef9e-103">Migrar seu banco de dados PostgreSQL usando exportar e importar</span><span class="sxs-lookup"><span data-stu-id="fef9e-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="fef9e-104">Você pode usar [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract um banco de dados PostgreSQL em um arquivo de script e [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport dados de saudação no banco de dados de destino de saudação do arquivo.</span><span class="sxs-lookup"><span data-stu-id="fef9e-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport hello data into hello target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fef9e-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fef9e-105">Prerequisites</span></span>
<span data-ttu-id="fef9e-106">toostep por este tooguide como, você precisa:</span><span class="sxs-lookup"><span data-stu-id="fef9e-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="fef9e-107">Um [banco de dados do Azure para o servidor PostgreSQL](quickstart-create-server-database-portal.md) com acesso de tooallow de regras de firewall e de banco de dados sob ele.</span><span class="sxs-lookup"><span data-stu-id="fef9e-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="fef9e-108">O utilitário de linha de comando [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) instalado</span><span class="sxs-lookup"><span data-stu-id="fef9e-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="fef9e-109">O utilitário de linha de comando [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) instalado</span><span class="sxs-lookup"><span data-stu-id="fef9e-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="fef9e-110">Siga estas etapas tooexport e importar o banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fef9e-110">Follow these steps tooexport and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="fef9e-111">Criar um arquivo de script usando pg_dump que contém a saudação dados toobe carregado</span><span class="sxs-lookup"><span data-stu-id="fef9e-111">Create a script file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="fef9e-112">tooexport seu PostgreSQL existente no local do banco de dados ou em um arquivo de script do VM tooa sql, execute Olá comando no seu ambiente a seguir:</span><span class="sxs-lookup"><span data-stu-id="fef9e-112">tooexport your existing PostgreSQL database on-premises or in a VM tooa sql script file, run hello following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="fef9e-113">Por exemplo, se você tiver um servidor local e um banco de dados chamado **testdb** nele</span><span class="sxs-lookup"><span data-stu-id="fef9e-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="fef9e-114">Importar dados de saudação no banco de dados de destino para PostrgeSQL</span><span class="sxs-lookup"><span data-stu-id="fef9e-114">Import hello data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="fef9e-115">Você pode usar a linha de comando psql hello e Olá -d, dados de saudação do – dbname parâmetro tooimport no banco de dados do Azure para PostrgeSQL é criado e carregar dados do arquivo de saudação do sql.</span><span class="sxs-lookup"><span data-stu-id="fef9e-115">You can use hello psql command line and hello -d, --dbname parameter tooimport hello data into Azure Database for PostrgeSQL we created and load data from hello sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="fef9e-116">Este exemplo usa o utilitário psql e um arquivo de script chamado **testdb.sql** de dados de tooimport etapa anterior no banco de dados de saudação **mypgsqldb** no servidor de destino  **mypgserver 20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="fef9e-116">This example uses psql utility and a script file named **testdb.sql** from previous step tooimport data into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="fef9e-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fef9e-117">Next steps</span></span>
- <span data-ttu-id="fef9e-118">toomigrate um banco de dados PostgreSQL usando dump e restore, consulte [migrar seu banco de dados PostgreSQL usando dump e restore](howto-migrate-using-dump-and-restore.md)</span><span class="sxs-lookup"><span data-stu-id="fef9e-118">toomigrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>
