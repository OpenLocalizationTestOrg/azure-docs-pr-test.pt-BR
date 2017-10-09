---
title: "parâmetros de serviço Olá aaaConfigure no banco de dados do Azure para PostgreSQL | Microsoft Docs"
description: "Este artigo descreve como parâmetros de serviço de saudação tooconfigure no banco de dados do Azure para usar PostgreSQL Olá a linha de comando CLI do Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="1f418-103">Personalizar os parâmetros de configuração do servidor usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1f418-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="1f418-104">Você pode listar, mostrar e atualizar os parâmetros de configuração para um servidor do Azure PostgreSQL usando Olá Interface de linha de comando (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="1f418-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="1f418-105">No entanto, somente um subconjunto de configurações de mecanismo é exposto no nível do servidor e pode ser modificado.</span><span class="sxs-lookup"><span data-stu-id="1f418-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1f418-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1f418-106">Prerequisites</span></span>
<span data-ttu-id="1f418-107">toostep por este tooguide como, você precisa:</span><span class="sxs-lookup"><span data-stu-id="1f418-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="1f418-108">Um servidor e um banco de dados [Criar um Banco de Dados do Azure para PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="1f418-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="1f418-109">Instalar [2.0 do CLI do Azure](/cli/azure/install-azure-cli) linha de comando utilitário ou use Olá Shell de nuvem do Azure no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f418-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="1f418-110">Listar os parâmetros de configuração de servidor para o bando de dados do Azure para servidor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1f418-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="1f418-111">execução de todos os parâmetros modificáveis em um servidor e seus valores, toolist Olá [lista de configuração de servidor az postgres](/cli/azure/postgres/server/configuration#list) comando.</span><span class="sxs-lookup"><span data-stu-id="1f418-111">toolist all modifiable parameters in a server and their values, run hello [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="1f418-112">Você pode listar os parâmetros de configuração de servidor Olá para o servidor de saudação **mypgserver 20170401.postgres.database.azure.com** no grupo de recursos **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="1f418-112">You can list hello server configuration parameters for hello server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="1f418-113">Mostrar detalhes do parâmetro de configuração do servidor</span><span class="sxs-lookup"><span data-stu-id="1f418-113">Show server configuration parameter details</span></span>
<span data-ttu-id="1f418-114">tooshow detalhes sobre um parâmetro de configuração específico para um servidor, execute Olá [Mostrar de configuração de servidor az postgres](/cli/azure/postgres/server/configuration#show) comando.</span><span class="sxs-lookup"><span data-stu-id="1f418-114">tooshow details about a particular configuration parameter for a server, run hello [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="1f418-115">Este exemplo mostra detalhes de saudação **log\_min\_mensagens** parâmetro de configuração de servidor para servidor **mypgserver 20170401.postgres.database.azure.com** em grupo de recursos **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="1f418-115">This example shows details of hello **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="1f418-116">Modificar o valor do parâmetro de configuração do servidor</span><span class="sxs-lookup"><span data-stu-id="1f418-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="1f418-117">Você também pode modificar o valor de saudação de um determinado parâmetro de configuração do servidor, e isso atualiza o valor de configuração subjacentes Olá para o mecanismo do hello PostgreSQL server.</span><span class="sxs-lookup"><span data-stu-id="1f418-117">You can also modify hello value of a certain server configuration parameter, and this updates hello underlying configuration value for hello PostgreSQL server engine.</span></span> <span data-ttu-id="1f418-118">saudação de uso de configuração de Olá tooupdate [conjunto de configurações de servidor az postgres](/cli/azure/postgres/server/configuration#set) comando.</span><span class="sxs-lookup"><span data-stu-id="1f418-118">tooupdate hello configuration use hello [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="1f418-119">Olá tooupdate **log\_min\_mensagens** parâmetro de configuração do servidor do servidor **mypgserver 20170401.postgres.database.azure.com** dogrupoderecursos**myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="1f418-119">tooupdate hello **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="1f418-120">Se você desejar tooreset Olá valor de um parâmetro de configuração, você simplesmente escolher tooleave out Olá opcional `--value` parâmetro e serviço Olá aplicará o valor padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f418-120">If you want tooreset hello value of a configuration parameter, you simply choose tooleave out hello optional `--value` parameter, and hello service will apply hello default value.</span></span> <span data-ttu-id="1f418-121">No exemplo acima, ele teria a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="1f418-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="1f418-122">Isso irá redefinir Olá **log\_min\_mensagens** valor padrão da configuração toohello **aviso**.</span><span class="sxs-lookup"><span data-stu-id="1f418-122">This will reset hello **log\_min\_messages** configuration toohello default value **WARNING**.</span></span> <span data-ttu-id="1f418-123">Para obter mais detalhes sobre a configuração do servidor e os valores permitidos, veja a documentação do PostgreSQL em [Configuração do Servidor](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span><span class="sxs-lookup"><span data-stu-id="1f418-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f418-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1f418-124">Next steps</span></span>
- <span data-ttu-id="1f418-125">logs do servidor tooconfigure e acesso, consulte [Logs do servidor no banco de dados do Azure para PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="1f418-125">tooconfigure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
