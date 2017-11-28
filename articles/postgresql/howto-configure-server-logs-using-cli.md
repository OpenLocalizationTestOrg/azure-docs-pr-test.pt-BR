---
title: Configurar e acessar os logs do servidor para PostgreSQL usando a CLI do Azure | Microsoft Docs
description: "Este artigo descreve como configurar e acessar os registros de serviço no bando de dados do Azure para PostgreSQL usando a linha de comando CLI do Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 26f8e12c493904f722cad5191ee053feff20f7fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="b72dd-103">Configurar e acessar logs de servidor usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b72dd-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="b72dd-104">Você pode listar e baixar logs de erro do servidor PostgreSQL do Azure usando a interface de linha de comando (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="b72dd-104">You can download the PostgreSQL server error logs using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="b72dd-105">No entanto, não há suporte para acesso aos logs de transação.</span><span class="sxs-lookup"><span data-stu-id="b72dd-105">However, access to transaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b72dd-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b72dd-106">Prerequisites</span></span>
<span data-ttu-id="b72dd-107">Para seguir este guia de instruções, você precisa:</span><span class="sxs-lookup"><span data-stu-id="b72dd-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="b72dd-108">Um [servidor de Banco de Dados do Azure para PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="b72dd-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="b72dd-109">Instalar o utilitário de linha de comando [CLI do Azure 2.0](/cli/azure/install-azure-cli) ou usar o Azure Cloud Shell no navegador.</span><span class="sxs-lookup"><span data-stu-id="b72dd-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="b72dd-110">Configurar o registro em log para o Banco de Dados do Azure para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="b72dd-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="b72dd-111">Você pode configurar o servidor para acessar os logs de erro e os logs de consulta.</span><span class="sxs-lookup"><span data-stu-id="b72dd-111">You can configure the server to access query logs and error logs.</span></span> <span data-ttu-id="b72dd-112">Os logs de erros podem conter informações de pontos de verificação, conexão e vácuo automático.</span><span class="sxs-lookup"><span data-stu-id="b72dd-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="b72dd-113">Ativar o registro em log</span><span class="sxs-lookup"><span data-stu-id="b72dd-113">Turn on logging</span></span>
2. <span data-ttu-id="b72dd-114">Atualizar log\_statement e log\_min\_duration\_statement para habilitar o registro em log de consulta</span><span class="sxs-lookup"><span data-stu-id="b72dd-114">Update log\_statement and log\_min\_duration\_statement to enable query logging</span></span>
3. <span data-ttu-id="b72dd-115">Atualizar o período de retenção</span><span class="sxs-lookup"><span data-stu-id="b72dd-115">Update retention period</span></span>

<span data-ttu-id="b72dd-116">Para mais informações, confira [personalizando os parâmetros de configuração do servidor](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b72dd-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="b72dd-117">Liste os registros para servidor de Banco de Dados do Azure para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="b72dd-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="b72dd-118">Para listar os arquivos de log disponíveis para o servidor, execute o comando [az postgres server-logs list](/cli/azure/postgres/server-logs#list).</span><span class="sxs-lookup"><span data-stu-id="b72dd-118">To list the available log files for your server, run the [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="b72dd-119">Você pode listar os arquivos de log para o servidor **mypgserver-20170401.postgres.database.azure.com** no grupo de recursos **myresourcegroup**, e direcioná-los para um arquivo de texto chamado **log\_files\_list.txt.**</span><span class="sxs-lookup"><span data-stu-id="b72dd-119">You can list the log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it to a text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-the-server"></a><span data-ttu-id="b72dd-120">Baixa logs localmente do servidor</span><span class="sxs-lookup"><span data-stu-id="b72dd-120">Download logs locally from the server</span></span>
<span data-ttu-id="b72dd-121">O comando [az postgres server-logs download](/cli/azure/postgres/server-logs#download) permite que você baixe arquivos de log individuais para o seu servidor.</span><span class="sxs-lookup"><span data-stu-id="b72dd-121">The [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you to download individual log files for your server.</span></span> 

<span data-ttu-id="b72dd-122">Este exemplo baixa o arquivo de log específico para o servidor **mypgserver-20170401.postgres.database.azure.com** no Grupo de Recursos **myresourcegroup** para seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="b72dd-122">This example downloads the specific log file for the server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** to your local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="b72dd-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b72dd-123">Next steps</span></span>
- <span data-ttu-id="b72dd-124">Para saber mais sobre os logs de servidor, confira [Logs de servidor no Banco de Dados do Azure para PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="b72dd-124">To learn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="b72dd-125">Para saber mais sobre os parâmetros de servidor, veja [Personalizar os parâmetros de configuração de servidor usando a CLI do Azure](howto-configure-server-parameters-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="b72dd-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
