---
title: "Configurar os parâmetros de serviço no Banco de Dados do Azure para PostgreSQL | Microsoft Docs"
description: "Este artigo descreve como configurar os parâmetros de serviço no bando de dados do Azure para PostgreSQL usando a linha de comando CLI do Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: c8a3b5a0225c2cede180d8d57681f2e1a6c6cc3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="8cdf3-103">Personalizar os parâmetros de configuração do servidor usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8cdf3-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="8cdf3-104">Você pode listar, exibir e atualizar os parâmetros de configuração de um servidor PostgreSQL do Azure usando a CLI (Interface de linha de comando) do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cdf3-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="8cdf3-105">No entanto, somente um subconjunto de configurações de mecanismo é exposto no nível do servidor e pode ser modificado.</span><span class="sxs-lookup"><span data-stu-id="8cdf3-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8cdf3-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8cdf3-106">Prerequisites</span></span>
<span data-ttu-id="8cdf3-107">Para seguir este guia de instruções, você precisa:</span><span class="sxs-lookup"><span data-stu-id="8cdf3-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="8cdf3-108">Um servidor e um banco de dados [Criar um Banco de Dados do Azure para PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="8cdf3-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="8cdf3-109">Instalar o utilitário de linha de comando [CLI do Azure 2.0](/cli/azure/install-azure-cli) ou usar o Azure Cloud Shell no navegador.</span><span class="sxs-lookup"><span data-stu-id="8cdf3-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="8cdf3-110">Listar os parâmetros de configuração de servidor para o bando de dados do Azure para servidor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="8cdf3-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="8cdf3-111">Para listar todos os parâmetros modificáveis em um servidor e seus valores, execute o comando [az postgres server configuration list](/cli/azure/postgres/server/configuration#list).</span><span class="sxs-lookup"><span data-stu-id="8cdf3-111">To list all modifiable parameters in a server and their values, run the [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="8cdf3-112">Você pode listar os parâmetros de configuração de servidor **mypgserver-20170401.postgres.database.azure.com** no grupo de recursos **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="8cdf3-112">You can list the server configuration parameters for the server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="8cdf3-113">Mostrar detalhes do parâmetro de configuração do servidor</span><span class="sxs-lookup"><span data-stu-id="8cdf3-113">Show server configuration parameter details</span></span>
<span data-ttu-id="8cdf3-114">Para mostrar os detalhes sobre um parâmetro de configuração específico para um servidor, execute o comando [az postgres server configuration show](/cli/azure/postgres/server/configuration#show).</span><span class="sxs-lookup"><span data-stu-id="8cdf3-114">To show details about a particular configuration parameter for a server, run the [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="8cdf3-115">Este exemplo mostra detalhes do **registro\_min\_mensagens** parâmetros de configuração de servidor para servidor **mypgserver-20170401.postgres.database.azure.com** no grupo de recursos **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="8cdf3-115">This example shows details of the **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="8cdf3-116">Modificar o valor do parâmetro de configuração do servidor</span><span class="sxs-lookup"><span data-stu-id="8cdf3-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="8cdf3-117">Você pode modificar o valor de determinados parâmetros de configuração e isso atualizará o valor da configuração subjacente para o mecanismo do servidor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8cdf3-117">You can also modify the value of a certain server configuration parameter, and this updates the underlying configuration value for the PostgreSQL server engine.</span></span> <span data-ttu-id="8cdf3-118">Para atualizar o valor de configuração execute o comando [az postgres server configuration set](/cli/azure/postgres/server/configuration#set).</span><span class="sxs-lookup"><span data-stu-id="8cdf3-118">To update the configuration use the [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="8cdf3-119">Para atualizar o **registro\_min\_mensagens** parâmetros de configuração de servidor para servidor **mypgserver-20170401.postgres.database.azure.com** no grupo de recursos **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="8cdf3-119">To update the **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="8cdf3-120">Se você quiser redefinir o valor de um parâmetro de configuração, basta simplesmente escolher deixar o parâmetro opcional `--value` e o serviço aplicará o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="8cdf3-120">If you want to reset the value of a configuration parameter, you simply choose to leave out the optional `--value` parameter, and the service will apply the default value.</span></span> <span data-ttu-id="8cdf3-121">No exemplo acima, ele teria a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="8cdf3-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="8cdf3-122">Isso redefinirá o **registro\_min\_mensagens** configuração para o valor padrão **AVISO**.</span><span class="sxs-lookup"><span data-stu-id="8cdf3-122">This will reset the **log\_min\_messages** configuration to the default value **WARNING**.</span></span> <span data-ttu-id="8cdf3-123">Para obter mais detalhes sobre a configuração do servidor e os valores permitidos, veja a documentação do PostgreSQL em [Configuração do Servidor](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span><span class="sxs-lookup"><span data-stu-id="8cdf3-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8cdf3-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8cdf3-124">Next steps</span></span>
- <span data-ttu-id="8cdf3-125">Para configurar e acessar os logs de servidor, confira [Logs de servidor no Banco de Dados do Azure para PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="8cdf3-125">To configure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
