---
title: Como tooback backup e restaurar um servidor no banco de dados do Azure para PostgreSQL | Microsoft Docs
description: "Saiba como tooback backup e restauração de um servidor de banco de dados do Azure para PostgreSQL usando Olá CLI do Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a><span data-ttu-id="e183b-103">Como tooback backup e restauração de um servidor de banco de dados do Azure para PostgreSQL usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e183b-103">How tooback up and restore a server in Azure Database for PostgreSQL by using hello Azure CLI</span></span>

<span data-ttu-id="e183b-104">Use banco de dados PostgreSQL toorestore um tooan de banco de dados do servidor data anterior que abrange de 7 dias too35.</span><span class="sxs-lookup"><span data-stu-id="e183b-104">Use Azure Database for PostgreSQL toorestore a server database tooan earlier date that spans from 7 too35 days.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e183b-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e183b-105">Prerequisites</span></span>
<span data-ttu-id="e183b-106">toocomplete tooguide esse como, você precisa:</span><span class="sxs-lookup"><span data-stu-id="e183b-106">toocomplete this how-tooguide, you need:</span></span>
- <span data-ttu-id="e183b-107">Um [Banco de Dados do Azure para servidor e banco de dados PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="e183b-107">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> <span data-ttu-id="e183b-108">Se você instala e usa o hello CLI do Azure localmente, esse tooguide como requer que você use a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e183b-108">If you install and use hello Azure CLI locally, this how-tooguide requires that you use Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e183b-109">versão de hello tooconfirm, no prompt de comando CLI do Azure hello, digite `az --version`.</span><span class="sxs-lookup"><span data-stu-id="e183b-109">tooconfirm hello version, at hello Azure CLI command prompt, enter `az --version`.</span></span> <span data-ttu-id="e183b-110">tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e183b-110">tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="back-up-happens-automatically"></a><span data-ttu-id="e183b-111">O backup ocorre automaticamente</span><span class="sxs-lookup"><span data-stu-id="e183b-111">Back up happens automatically</span></span>
<span data-ttu-id="e183b-112">Quando você usa o banco de dados do Azure para PostgreSQL, o serviço de banco de dados de saudação torna automaticamente um backup do serviço de saudação a cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="e183b-112">When you use Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="e183b-113">Para a camada básica, os backups de saudação estão disponíveis para 7 dias.</span><span class="sxs-lookup"><span data-stu-id="e183b-113">For Basic Tier, hello backups are available for 7 days.</span></span> <span data-ttu-id="e183b-114">Para a camada padrão, os backups de saudação estão disponíveis para 35 dias.</span><span class="sxs-lookup"><span data-stu-id="e183b-114">For Standard Tier, hello backups are available for 35 days.</span></span> <span data-ttu-id="e183b-115">Para saber mais, confira [Tipos de preço do Banco de Dados do Azure para PostgreSQL](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="e183b-115">For more information, see [Azure Database for PostgreSQL pricing tiers](concepts-service-tiers.md).</span></span>

<span data-ttu-id="e183b-116">Com esse recurso de backup automático, você pode restaurar o servidor de saudação e tooan seus bancos de dados data anterior ou ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="e183b-116">With this automatic backup feature, you can restore hello server and its databases tooan earlier date, or point in time.</span></span>

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a><span data-ttu-id="e183b-117">Restaurar um ponto anterior do banco de dados tooa no tempo usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e183b-117">Restore a database tooa previous point in time by using hello Azure CLI</span></span>
<span data-ttu-id="e183b-118">Usar banco de dados do Azure para PostgreSQL toorestore Olá server tooa ponto anterior no tempo.</span><span class="sxs-lookup"><span data-stu-id="e183b-118">Use Azure Database for PostgreSQL toorestore hello server tooa previous point in time.</span></span> <span data-ttu-id="e183b-119">dados saudação restaurado são copiado tooa novo servidor e servidor de saudação existente será deixado como está.</span><span class="sxs-lookup"><span data-stu-id="e183b-119">hello restored data is copied tooa new server, and hello existing server is left as is.</span></span> <span data-ttu-id="e183b-120">Por exemplo, se uma tabela for descartada acidentalmente ao meio-dia hoje, você pode restaurar toohello tempo antes de meio-dia.</span><span class="sxs-lookup"><span data-stu-id="e183b-120">For example, if a table is accidentally dropped at noon today, you can restore toohello time just before noon.</span></span> <span data-ttu-id="e183b-121">Em seguida, você pode recuperar Olá ausente da tabela e dados de cópia de saudação restaurada do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="e183b-121">Then, you can retrieve hello missing table and data from hello restored copy of hello server.</span></span> 

<span data-ttu-id="e183b-122">servidor de saudação toorestore, use Olá CLI do Azure [restauração do servidor postgres az](/cli/azure/postgres/server#restore) comando.</span><span class="sxs-lookup"><span data-stu-id="e183b-122">toorestore hello server, use hello Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) command.</span></span>

### <a name="run-hello-restore-command"></a><span data-ttu-id="e183b-123">Execute o comando restore Olá</span><span class="sxs-lookup"><span data-stu-id="e183b-123">Run hello restore command</span></span>

<span data-ttu-id="e183b-124">servidor de saudação toorestore, no prompt de comando CLI do Azure hello, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e183b-124">toorestore hello server, at hello Azure CLI command prompt, enter hello following command:</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="e183b-125">Olá `az postgres server restore` comando requer Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="e183b-125">hello `az postgres server restore` command requires hello following parameters:</span></span>
| <span data-ttu-id="e183b-126">Configuração</span><span class="sxs-lookup"><span data-stu-id="e183b-126">Setting</span></span> | <span data-ttu-id="e183b-127">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="e183b-127">Suggested value</span></span> | <span data-ttu-id="e183b-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="e183b-128">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="e183b-129">resource-group</span><span class="sxs-lookup"><span data-stu-id="e183b-129">resource-group</span></span> |  <span data-ttu-id="e183b-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e183b-130">myResourceGroup</span></span> |  <span data-ttu-id="e183b-131">O grupo de recursos onde o servidor de origem de saudação existe.</span><span class="sxs-lookup"><span data-stu-id="e183b-131">The resource group where hello source server exists.</span></span>  |
| <span data-ttu-id="e183b-132">name</span><span class="sxs-lookup"><span data-stu-id="e183b-132">name</span></span> | <span data-ttu-id="e183b-133">restaurado mypgserver</span><span class="sxs-lookup"><span data-stu-id="e183b-133">mypgserver-restored</span></span> | <span data-ttu-id="e183b-134">nome de Olá do novo servidor de saudação é criado pelo comando de restauração de saudação.</span><span class="sxs-lookup"><span data-stu-id="e183b-134">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="e183b-135">Restauração-point-in-time</span><span class="sxs-lookup"><span data-stu-id="e183b-135">restore-point-in-time</span></span> | <span data-ttu-id="e183b-136">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="e183b-136">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="e183b-137">Selecione um ponto no tempo toorestore para.</span><span class="sxs-lookup"><span data-stu-id="e183b-137">Select a point in time toorestore to.</span></span> <span data-ttu-id="e183b-138">A data e a hora devem estar dentro de saudação do servidor de origem período de retenção de backup.</span><span class="sxs-lookup"><span data-stu-id="e183b-138">This date and time must be within hello source server's back up retention period.</span></span> <span data-ttu-id="e183b-139">Use o formato de data e hora Olá ISO8601.</span><span class="sxs-lookup"><span data-stu-id="e183b-139">Use hello ISO8601 date and time format.</span></span> <span data-ttu-id="e183b-140">Por exemplo, você pode usar seu fuso horário local, como `2017-04-13T05:59:00-08:00`.</span><span class="sxs-lookup"><span data-stu-id="e183b-140">For example, you can use your own local time zone, such as `2017-04-13T05:59:00-08:00`.</span></span> <span data-ttu-id="e183b-141">Você também pode usar o hello formato UTC Zulu, por exemplo, `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="e183b-141">You can also use hello UTC Zulu format, for example, `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="e183b-142">source-server</span><span class="sxs-lookup"><span data-stu-id="e183b-142">source-server</span></span> | <span data-ttu-id="e183b-143">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="e183b-143">mypgserver-20170401</span></span> | <span data-ttu-id="e183b-144">nome de saudação ou ID do hello toorestore de servidor de origem do.</span><span class="sxs-lookup"><span data-stu-id="e183b-144">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="e183b-145">Quando você restaurar um servidor tooan ponto anterior no tempo, um novo servidor é criado.</span><span class="sxs-lookup"><span data-stu-id="e183b-145">When you restore a server tooan earlier point in time, a new server is created.</span></span> <span data-ttu-id="e183b-146">servidor de saudação original e seus bancos de dados de saudação especificado ponto no tempo são copiados toohello novo servidor.</span><span class="sxs-lookup"><span data-stu-id="e183b-146">hello original server and its databases from hello specified point in time are copied toohello new server.</span></span>

<span data-ttu-id="e183b-147">Olá local e preços de valores de nível para o servidor de saudação restaurado permanecer Olá mesmo o como servidor de saudação original.</span><span class="sxs-lookup"><span data-stu-id="e183b-147">hello location and pricing tier values for hello restored server remain hello same as hello original server.</span></span> 

<span data-ttu-id="e183b-148">Olá `az postgres server restore` comando é síncrono.</span><span class="sxs-lookup"><span data-stu-id="e183b-148">hello `az postgres server restore` command is synchronous.</span></span> <span data-ttu-id="e183b-149">Depois que o servidor de saudação é restaurado, você pode usá-la novamente toorepeat Olá processo para outro ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="e183b-149">After hello server is restored, you can use it again toorepeat hello process for a different point in time.</span></span> 

<span data-ttu-id="e183b-150">Depois de saudação conclusão do processo de restauração, localize o novo servidor de saudação e verificar se os dados de saudação são restaurados conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="e183b-150">After hello restore process finishes, locate hello new server and verify that hello data is restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e183b-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e183b-151">Next steps</span></span>
[<span data-ttu-id="e183b-152">Bibliotecas de conexão para o Banco de Dados do Azure para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="e183b-152">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
