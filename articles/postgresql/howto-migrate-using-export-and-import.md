---
title: Migrar um banco de dados usando Importar e Exportar no Banco de Dados do Azure para PostgreSQL | Microsoft Docs
description: Descreve como extrair um banco de dados PostgreSQL para um arquivo de script e importar os dados para o banco de dados de destino desse arquivo.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5e306d516d04789e4526bfd09bf99139b83573ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="e0290-103">Migrar seu banco de dados PostgreSQL usando exportar e importar</span><span class="sxs-lookup"><span data-stu-id="e0290-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="e0290-104">Use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) para extrair um banco de dados PostgreSQL para um arquivo de script, e [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) para importar os dados para o banco de dados de destino desse arquivo.</span><span class="sxs-lookup"><span data-stu-id="e0290-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) to extract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) to import the data into the target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0290-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e0290-105">Prerequisites</span></span>
<span data-ttu-id="e0290-106">Para seguir este guia de instruções, você precisa:</span><span class="sxs-lookup"><span data-stu-id="e0290-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="e0290-107">Um [Servidor de Banco de Dados do Azure para PostgreSQL](quickstart-create-server-database-portal.md) com regras de firewall a fim de permitir o acesso e um banco de dados sob ele.</span><span class="sxs-lookup"><span data-stu-id="e0290-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules to allow access and database under it.</span></span>
- <span data-ttu-id="e0290-108">O utilitário de linha de comando [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) instalado</span><span class="sxs-lookup"><span data-stu-id="e0290-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="e0290-109">O utilitário de linha de comando [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) instalado</span><span class="sxs-lookup"><span data-stu-id="e0290-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="e0290-110">Execute estas etapas para exportar e importar o banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e0290-110">Follow these steps to export and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-the-data-to-be-loaded"></a><span data-ttu-id="e0290-111">Criar um arquivo de script usando pg_dump que contém os dados a serem carregados</span><span class="sxs-lookup"><span data-stu-id="e0290-111">Create a script file using pg_dump that contains the data to be loaded</span></span>
<span data-ttu-id="e0290-112">Para exportar seu banco de dados PostgreSQL existente localmente ou em uma VM para um arquivo de script sql, execute o seguinte comando em seu ambiente existente:</span><span class="sxs-lookup"><span data-stu-id="e0290-112">To export your existing PostgreSQL database on-premises or in a VM to a sql script file, run the following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="e0290-113">Por exemplo, se você tiver um servidor local e um banco de dados chamado **testdb** nele</span><span class="sxs-lookup"><span data-stu-id="e0290-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-the-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="e0290-114">Importar os dados no Banco de Dados do Azure de destino para PostrgeSQL</span><span class="sxs-lookup"><span data-stu-id="e0290-114">Import the data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="e0290-115">Você pode usar a linha de comando psql e o parâmetro -d, --dbname para importar os dados para o Banco de Dados do Azure para PostrgeSQL criamos e carregamos dados do arquivo sql.</span><span class="sxs-lookup"><span data-stu-id="e0290-115">You can use the psql command line and the -d, --dbname parameter to import the data into Azure Database for PostrgeSQL we created and load data from the sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="e0290-116">Este exemplo usa arquivo psql e de script chamado **testdb.sql** da etapa anterior para importar dados para o banco de dados **mypgsqldb** no servidor de destino **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="e0290-116">This example uses psql utility and a script file named **testdb.sql** from previous step to import data into the database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="e0290-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e0290-117">Next steps</span></span>
- <span data-ttu-id="e0290-118">Para migrar um banco de dados PostgreSQL usando dump e restore, veja [Migrar seu banco de dados PostgreSQL usando dump e restore](howto-migrate-using-dump-and-restore.md)</span><span class="sxs-lookup"><span data-stu-id="e0290-118">To migrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>