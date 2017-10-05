---
title: Como fazer backup e restaurar um servidor no Banco de Dados do Azure para PostgreSQL | Microsoft Docs
description: Saiba como fazer backup e restaurar um servidor no Banco de Dados do Azure para PostgreSQL usando a CLI do Azure.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 871887e67d686a965a0648d2c6f0c72b3008db05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-back-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-the-azure-cli"></a><span data-ttu-id="c6c53-103">Como fazer backup e restaurar um servidor no Banco de Dados do Azure para PostgreSQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c6c53-103">How to back up and restore a server in Azure Database for PostgreSQL by using the Azure CLI</span></span>

<span data-ttu-id="c6c53-104">Use o Banco de Dados do Azure para PostgreSQL para restaurar um banco de dados do servidor para uma data anterior que abranja de sete a 35 dias.</span><span class="sxs-lookup"><span data-stu-id="c6c53-104">Use Azure Database for PostgreSQL to restore a server database to an earlier date that spans from 7 to 35 days.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6c53-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c6c53-105">Prerequisites</span></span>
<span data-ttu-id="c6c53-106">Para concluir este guia de instruções, você precisa:</span><span class="sxs-lookup"><span data-stu-id="c6c53-106">To complete this how-to guide, you need:</span></span>
- <span data-ttu-id="c6c53-107">Um [Banco de Dados do Azure para servidor e banco de dados PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="c6c53-107">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> <span data-ttu-id="c6c53-108">Se você instalar e usar a CLI do Azure localmente, este guia de instruções exige que você use a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c6c53-108">If you install and use the Azure CLI locally, this how-to guide requires that you use Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c6c53-109">Para confirmar a versão, no prompt de comando da CLI do Azure, digite `az --version`.</span><span class="sxs-lookup"><span data-stu-id="c6c53-109">To confirm the version, at the Azure CLI command prompt, enter `az --version`.</span></span> <span data-ttu-id="c6c53-110">Para instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c6c53-110">To install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="back-up-happens-automatically"></a><span data-ttu-id="c6c53-111">O backup ocorre automaticamente</span><span class="sxs-lookup"><span data-stu-id="c6c53-111">Back up happens automatically</span></span>
<span data-ttu-id="c6c53-112">Ao usar o Banco de Dados do Azure para PostgreSQL, o serviço de banco de dados faz automaticamente um backup do serviço a cada cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="c6c53-112">When you use Azure Database for PostgreSQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="c6c53-113">Para a Camada Básica, os backups estão disponíveis por sete dias.</span><span class="sxs-lookup"><span data-stu-id="c6c53-113">For Basic Tier, the backups are available for 7 days.</span></span> <span data-ttu-id="c6c53-114">Para a Camada Padrão, os backups estão disponíveis por 35 dias.</span><span class="sxs-lookup"><span data-stu-id="c6c53-114">For Standard Tier, the backups are available for 35 days.</span></span> <span data-ttu-id="c6c53-115">Para saber mais, confira [Tipos de preço do Banco de Dados do Azure para PostgreSQL](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="c6c53-115">For more information, see [Azure Database for PostgreSQL pricing tiers](concepts-service-tiers.md).</span></span>

<span data-ttu-id="c6c53-116">Com esse recurso de backup automático, você pode restaurar o servidor e seus bancos de dados para uma data em momento anterior.</span><span class="sxs-lookup"><span data-stu-id="c6c53-116">With this automatic backup feature, you can restore the server and its databases to an earlier date, or point in time.</span></span>

## <a name="restore-a-database-to-a-previous-point-in-time-by-using-the-azure-cli"></a><span data-ttu-id="c6c53-117">Restaurar um banco de dados para um momento anterior usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c6c53-117">Restore a database to a previous point in time by using the Azure CLI</span></span>
<span data-ttu-id="c6c53-118">Use o Banco de Dados do Azure para PostgreSQL para restaurar o servidor para um momento anterior.</span><span class="sxs-lookup"><span data-stu-id="c6c53-118">Use Azure Database for PostgreSQL to restore the server to a previous point in time.</span></span> <span data-ttu-id="c6c53-119">Os dados restaurados são copiados para um novo servidor e o servidor existente é deixado como está.</span><span class="sxs-lookup"><span data-stu-id="c6c53-119">The restored data is copied to a new server, and the existing server is left as is.</span></span> <span data-ttu-id="c6c53-120">Por exemplo, se uma tabela tiver sido descartada acidentalmente ao meio-dia de hoje, você poderá restaurá-la para um horário um pouco antes do meio-dia.</span><span class="sxs-lookup"><span data-stu-id="c6c53-120">For example, if a table is accidentally dropped at noon today, you can restore to the time just before noon.</span></span> <span data-ttu-id="c6c53-121">Depois, você pode recuperar a tabela e os dados ausentes da cópia restaurada do servidor.</span><span class="sxs-lookup"><span data-stu-id="c6c53-121">Then, you can retrieve the missing table and data from the restored copy of the server.</span></span> 

<span data-ttu-id="c6c53-122">Para restaurar o servidor, use o comando [az postgres server restore](/cli/azure/postgres/server#restore) da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6c53-122">To restore the server, use the Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) command.</span></span>

### <a name="run-the-restore-command"></a><span data-ttu-id="c6c53-123">Executar o comando restore</span><span class="sxs-lookup"><span data-stu-id="c6c53-123">Run the restore command</span></span>

<span data-ttu-id="c6c53-124">Para restaurar o servidor, no prompt de comando da CLI do Azure, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c6c53-124">To restore the server, at the Azure CLI command prompt, enter the following command:</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="c6c53-125">O comando `az postgres server restore` exige os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="c6c53-125">The `az postgres server restore` command requires the following parameters:</span></span>
| <span data-ttu-id="c6c53-126">Configuração</span><span class="sxs-lookup"><span data-stu-id="c6c53-126">Setting</span></span> | <span data-ttu-id="c6c53-127">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="c6c53-127">Suggested value</span></span> | <span data-ttu-id="c6c53-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="c6c53-128">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="c6c53-129">resource-group</span><span class="sxs-lookup"><span data-stu-id="c6c53-129">resource-group</span></span> |  <span data-ttu-id="c6c53-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c6c53-130">myResourceGroup</span></span> |  <span data-ttu-id="c6c53-131">O grupo de recursos em que o servidor de origem existe.</span><span class="sxs-lookup"><span data-stu-id="c6c53-131">The resource group where the source server exists.</span></span>  |
| <span data-ttu-id="c6c53-132">name</span><span class="sxs-lookup"><span data-stu-id="c6c53-132">name</span></span> | <span data-ttu-id="c6c53-133">restaurado mypgserver</span><span class="sxs-lookup"><span data-stu-id="c6c53-133">mypgserver-restored</span></span> | <span data-ttu-id="c6c53-134">O nome do novo servidor que é criado pelo comando de restauração.</span><span class="sxs-lookup"><span data-stu-id="c6c53-134">The name of the new server that is created by the restore command.</span></span> |
| <span data-ttu-id="c6c53-135">Restauração-point-in-time</span><span class="sxs-lookup"><span data-stu-id="c6c53-135">restore-point-in-time</span></span> | <span data-ttu-id="c6c53-136">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="c6c53-136">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="c6c53-137">Selecione um ponto no tempo para o qual restaurar.</span><span class="sxs-lookup"><span data-stu-id="c6c53-137">Select a point in time to restore to.</span></span> <span data-ttu-id="c6c53-138">Essa data e hora devem estar dentro do período de retenção de backup do servidor de origem.</span><span class="sxs-lookup"><span data-stu-id="c6c53-138">This date and time must be within the source server's back up retention period.</span></span> <span data-ttu-id="c6c53-139">Use o formato ISO8601 de data e hora.</span><span class="sxs-lookup"><span data-stu-id="c6c53-139">Use the ISO8601 date and time format.</span></span> <span data-ttu-id="c6c53-140">Por exemplo, você pode usar seu fuso horário local, como `2017-04-13T05:59:00-08:00`.</span><span class="sxs-lookup"><span data-stu-id="c6c53-140">For example, you can use your own local time zone, such as `2017-04-13T05:59:00-08:00`.</span></span> <span data-ttu-id="c6c53-141">Você também pode usar o formato UTC Zulu, por exemplo, `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="c6c53-141">You can also use the UTC Zulu format, for example, `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="c6c53-142">source-server</span><span class="sxs-lookup"><span data-stu-id="c6c53-142">source-server</span></span> | <span data-ttu-id="c6c53-143">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="c6c53-143">mypgserver-20170401</span></span> | <span data-ttu-id="c6c53-144">O nome ou ID para restaurar a partir do servidor de origem.</span><span class="sxs-lookup"><span data-stu-id="c6c53-144">The name or ID of the source server to restore from.</span></span> |

<span data-ttu-id="c6c53-145">Quando você restaura um servidor para um ponto anterior no tempo, é criado um novo servidor.</span><span class="sxs-lookup"><span data-stu-id="c6c53-145">When you restore a server to an earlier point in time, a new server is created.</span></span> <span data-ttu-id="c6c53-146">O servidor original e seus bancos de dados do ponto no tempo especificado são copiados para o novo servidor.</span><span class="sxs-lookup"><span data-stu-id="c6c53-146">The original server and its databases from the specified point in time are copied to the new server.</span></span>

<span data-ttu-id="c6c53-147">Os valores de local e tipo de preço para o servidor restaurado permanecem iguais aos do servidor de origem.</span><span class="sxs-lookup"><span data-stu-id="c6c53-147">The location and pricing tier values for the restored server remain the same as the original server.</span></span> 

<span data-ttu-id="c6c53-148">O comando `az postgres server restore` é síncrono.</span><span class="sxs-lookup"><span data-stu-id="c6c53-148">The `az postgres server restore` command is synchronous.</span></span> <span data-ttu-id="c6c53-149">Depois que o servidor é restaurado, você pode usá-lo novamente para repetir o processo para outro ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="c6c53-149">After the server is restored, you can use it again to repeat the process for a different point in time.</span></span> 

<span data-ttu-id="c6c53-150">Depois que o processo de restauração é concluído, localize o novo servidor e verifique se os dados são restaurados como esperado.</span><span class="sxs-lookup"><span data-stu-id="c6c53-150">After the restore process finishes, locate the new server and verify that the data is restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6c53-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6c53-151">Next steps</span></span>
[<span data-ttu-id="c6c53-152">Bibliotecas de conexão para o Banco de Dados do Azure para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="c6c53-152">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
