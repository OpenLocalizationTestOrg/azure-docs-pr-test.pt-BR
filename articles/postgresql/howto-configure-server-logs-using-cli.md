---
title: logs do servidor aaaConfigure e acesso para PostgreSQL usando a CLI do Azure | Microsoft Docs
description: "Este artigo descreve como tooconfigure e acesso Olá logs do servidor no banco de dados do Azure para PostgreSQL usando a linha de comando CLI do Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="25cd4-103">Configurar e acessar logs de servidor usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="25cd4-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="25cd4-104">Você pode baixar os logs de erros do hello PostgreSQL server usando Olá Interface de linha de comando (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="25cd4-104">You can download hello PostgreSQL server error logs using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="25cd4-105">No entanto, não há suporte para acesso tootransaction logs.</span><span class="sxs-lookup"><span data-stu-id="25cd4-105">However, access tootransaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="25cd4-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="25cd4-106">Prerequisites</span></span>
<span data-ttu-id="25cd4-107">toostep por este tooguide como, você precisa:</span><span class="sxs-lookup"><span data-stu-id="25cd4-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="25cd4-108">Um [servidor de Banco de Dados do Azure para PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="25cd4-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="25cd4-109">Instalar [2.0 do CLI do Azure](/cli/azure/install-azure-cli) de linha de comando utilitário ou use Olá Shell de nuvem do Azure no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="25cd4-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="25cd4-110">Configurar o registro em log para o Banco de Dados do Azure para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="25cd4-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="25cd4-111">Você pode configurar logs de consulta Olá servidor tooaccess e logs de erros.</span><span class="sxs-lookup"><span data-stu-id="25cd4-111">You can configure hello server tooaccess query logs and error logs.</span></span> <span data-ttu-id="25cd4-112">Os logs de erros podem conter informações de pontos de verificação, conexão e vácuo automático.</span><span class="sxs-lookup"><span data-stu-id="25cd4-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="25cd4-113">Ativar o registro em log</span><span class="sxs-lookup"><span data-stu-id="25cd4-113">Turn on logging</span></span>
2. <span data-ttu-id="25cd4-114">Log de atualização\_instrução e log\_min\_duração\_log de consulta de tooenable de instrução</span><span class="sxs-lookup"><span data-stu-id="25cd4-114">Update log\_statement and log\_min\_duration\_statement tooenable query logging</span></span>
3. <span data-ttu-id="25cd4-115">Atualizar o período de retenção</span><span class="sxs-lookup"><span data-stu-id="25cd4-115">Update retention period</span></span>

<span data-ttu-id="25cd4-116">Para mais informações, confira [personalizando os parâmetros de configuração do servidor](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="25cd4-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="25cd4-117">Liste os registros para servidor de Banco de Dados do Azure para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="25cd4-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="25cd4-118">arquivos de log disponíveis toolist Olá para o servidor, execute Olá [lista de logs do servidor postgres az](/cli/azure/postgres/server-logs#list) comando.</span><span class="sxs-lookup"><span data-stu-id="25cd4-118">toolist hello available log files for your server, run hello [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="25cd4-119">Você pode listar os arquivos de log Olá para o servidor **mypgserver 20170401.postgres.database.azure.com** no grupo de recursos **myresourcegroup**e direcioná-lo tooa texto arquivo chamado **log\_arquivos\_txt.**</span><span class="sxs-lookup"><span data-stu-id="25cd4-119">You can list hello log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it tooa text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a><span data-ttu-id="25cd4-120">Baixar os logs do servidor de saudação localmente</span><span class="sxs-lookup"><span data-stu-id="25cd4-120">Download logs locally from hello server</span></span>
<span data-ttu-id="25cd4-121">Olá [baixar logs de servidor az postgres](/cli/azure/postgres/server-logs#download) comando permite que os arquivos de log individuais toodownload para o servidor.</span><span class="sxs-lookup"><span data-stu-id="25cd4-121">hello [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you toodownload individual log files for your server.</span></span> 

<span data-ttu-id="25cd4-122">Este exemplo hello de downloads de arquivo de log específico para o servidor de saudação **mypgserver 20170401.postgres.database.azure.com** no grupo de recursos **myresourcegroup** tooyour ambiente de local.</span><span class="sxs-lookup"><span data-stu-id="25cd4-122">This example downloads hello specific log file for hello server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** tooyour local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="25cd4-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="25cd4-123">Next steps</span></span>
- <span data-ttu-id="25cd4-124">toolearn mais sobre os logs do servidor, consulte [Logs do servidor no banco de dados do Azure para PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="25cd4-124">toolearn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="25cd4-125">Para saber mais sobre os parâmetros de servidor, veja [Personalizar os parâmetros de configuração de servidor usando a CLI do Azure](howto-configure-server-parameters-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="25cd4-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
