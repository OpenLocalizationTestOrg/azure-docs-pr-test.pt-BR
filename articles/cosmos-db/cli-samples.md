---
title: Exemplos da CLI do Azure para o Azure Cosmos DB | Microsoft Docs
description: "Exemplos da CLI do Azure - Criar e gerenciar contas, , bancos de dados, contêineres, regiões e firewalls do Azure Cosmos DB."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 06/07/2017
ms.author: mimig
ms.openlocfilehash: 709d2ccce0f4b9827a8076f683c7e0f74cbdd4ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="07c2e-103">Exemplos da CLI do Azure para o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="07c2e-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="07c2e-104">A tabela a seguir inclui links para exemplos de scripts de CLI do Azure para o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="07c2e-104">The following table includes links to sample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="07c2e-105">Páginas de referência para todos os comandos de CLI do Azure Cosmos DB estão disponíveis na [referência da CLI 2.0 do Azure](https://docs.microsoft.com/cli/azure/cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="07c2e-105">Reference pages for all Azure Cosmos DB CLI commands are available in the [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="07c2e-106">**Criar uma conta, banco de dados e contêineres do Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="07c2e-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="07c2e-107">Criar uma conta da API de DocumentDB, Graph ou Tabela</span><span class="sxs-lookup"><span data-stu-id="07c2e-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="07c2e-108">Criar uma única conta, banco de dados e contêiner da API do Azure Cosmos DB para usar com APIs do DocumentDB, Graph ou Tabela.</span><span class="sxs-lookup"><span data-stu-id="07c2e-108">Creates a single Azure Cosmos DB API account, database, and container for use with the DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="07c2e-109">Criar uma conta da API do MongoDB</span><span class="sxs-lookup"><span data-stu-id="07c2e-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="07c2e-110">Cria uma única conta, banco de dados e coleção da API de MongoDB do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="07c2e-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="07c2e-111">**Dimensionar o Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="07c2e-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="07c2e-112">Escalar a taxa de transferência de contêiner</span><span class="sxs-lookup"><span data-stu-id="07c2e-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="07c2e-113">Altera a taxa de transferência provisionada em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="07c2e-113">Changes the provisioned througput on a container.</span></span>|
|[<span data-ttu-id="07c2e-114">Replicar uma conta de banco de dados do Azure Cosmos DB em várias regiões e configurar as prioridades de failover</span><span class="sxs-lookup"><span data-stu-id="07c2e-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="07c2e-115">Replica globalmente os dados da conta em várias regiões com uma prioridade de failover especificada.</span><span class="sxs-lookup"><span data-stu-id="07c2e-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="07c2e-116">**Proteger o Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="07c2e-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="07c2e-117">Obter chaves da conta</span><span class="sxs-lookup"><span data-stu-id="07c2e-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="07c2e-118">Obtém a chaves de gravação mestre primária e secundária e as chaves somente leitura primária e secundária da conta.</span><span class="sxs-lookup"><span data-stu-id="07c2e-118">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="07c2e-119">Obter cadeia de conexão do MongoDB</span><span class="sxs-lookup"><span data-stu-id="07c2e-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="07c2e-120">Obtém a cadeia de conexão para conectar seu aplicativo MongoDB à sua conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="07c2e-120">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="07c2e-121">Regenerar chaves da conta</span><span class="sxs-lookup"><span data-stu-id="07c2e-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="07c2e-122">Regenera a chave mestre ou somente leitura da conta.</span><span class="sxs-lookup"><span data-stu-id="07c2e-122">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="07c2e-123">Criar um firewall</span><span class="sxs-lookup"><span data-stu-id="07c2e-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="07c2e-124">Cria uma política de controle de acesso IP de entrada para limitar o acesso à conta por um conjunto aprovado de máquinas e/ou serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="07c2e-124">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="07c2e-125">**Alta disponibilidade, recuperação de desastre, backup e restauração**</span><span class="sxs-lookup"><span data-stu-id="07c2e-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="07c2e-126">Configurar política de failover</span><span class="sxs-lookup"><span data-stu-id="07c2e-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="07c2e-127">Define a prioridade de failover para cada região em que a conta é replicada.</span><span class="sxs-lookup"><span data-stu-id="07c2e-127">Sets the failover priority of each region in which the account is replicated.</span></span>|
|<span data-ttu-id="07c2e-128">**Conectar o Azure Cosmos DB aos recursos**</span><span class="sxs-lookup"><span data-stu-id="07c2e-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="07c2e-129">Conectar um aplicativo Web ao Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="07c2e-129">Connect a web app to Azure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="07c2e-130">Criar e conectar um banco de dados do Azure Cosmos DB e um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="07c2e-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
