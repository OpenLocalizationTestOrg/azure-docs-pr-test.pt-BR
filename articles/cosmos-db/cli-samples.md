---
title: aaaAzure exemplos de CLI para o banco de dados do Azure Cosmos | Microsoft Docs
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
ms.openlocfilehash: d6eefc3274e0b66eec4e69166bb7d4ddd58a522e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="80ce8-103">Exemplos da CLI do Azure para o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="80ce8-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="80ce8-104">Olá tabela a seguir inclui links toosample CLI do Azure scripts para o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="80ce8-104">hello following table includes links toosample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="80ce8-105">Páginas de referência para todos os comandos de CLI do Azure Cosmos banco de dados estão disponíveis em Olá [referência da CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="80ce8-105">Reference pages for all Azure Cosmos DB CLI commands are available in hello [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="80ce8-106">**Criar uma conta, banco de dados e contêineres do Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="80ce8-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="80ce8-107">Criar uma conta da API de DocumentDB, Graph ou Tabela</span><span class="sxs-lookup"><span data-stu-id="80ce8-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="80ce8-108">Cria uma conta da API de banco de dados do Azure Cosmos único, o banco de dados e o contêiner para uso com hello documentos, gráfico ou APIs de tabela.</span><span class="sxs-lookup"><span data-stu-id="80ce8-108">Creates a single Azure Cosmos DB API account, database, and container for use with hello DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="80ce8-109">Criar uma conta da API do MongoDB</span><span class="sxs-lookup"><span data-stu-id="80ce8-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="80ce8-110">Cria uma única conta, banco de dados e coleção da API de MongoDB do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="80ce8-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="80ce8-111">**Dimensionar o Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="80ce8-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="80ce8-112">Escalar a taxa de transferência de contêiner</span><span class="sxs-lookup"><span data-stu-id="80ce8-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="80ce8-113">Olá alterações provisionados througput em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="80ce8-113">Changes hello provisioned througput on a container.</span></span>|
|[<span data-ttu-id="80ce8-114">Replicar uma conta de banco de dados do Azure Cosmos DB em várias regiões e configurar as prioridades de failover</span><span class="sxs-lookup"><span data-stu-id="80ce8-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="80ce8-115">Replica globalmente os dados da conta em várias regiões com uma prioridade de failover especificada.</span><span class="sxs-lookup"><span data-stu-id="80ce8-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="80ce8-116">**Proteger o Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="80ce8-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="80ce8-117">Obter chaves da conta</span><span class="sxs-lookup"><span data-stu-id="80ce8-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="80ce8-118">Obtém as chaves de gravação mestre primário e secundário hello e chaves somente leitura primária e secundária para a conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="80ce8-118">Gets hello primary and secondary master write keys and primary and secondary read-only keys for hello account.</span></span>|
| [<span data-ttu-id="80ce8-119">Obter cadeia de conexão do MongoDB</span><span class="sxs-lookup"><span data-stu-id="80ce8-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="80ce8-120">Obtém o tooconnect de cadeia de caracteres de conexão de saudação seu aplicativo de MongoDB tooyour conta de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="80ce8-120">Gets hello connection string tooconnect your MongoDB app tooyour Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="80ce8-121">Regenerar chaves da conta</span><span class="sxs-lookup"><span data-stu-id="80ce8-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="80ce8-122">Regenera mestre hello ou chave de somente leitura para a conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="80ce8-122">Regenerates hello master or read-only key for hello account.</span></span>|
|[<span data-ttu-id="80ce8-123">Criar um firewall</span><span class="sxs-lookup"><span data-stu-id="80ce8-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="80ce8-124">Cria uma entrada IP acesso controle política toolimit toohello conta de acesso de um conjunto aprovado de máquinas e/ou serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="80ce8-124">Creates an inbound IP access control policy toolimit access toohello account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="80ce8-125">**Alta disponibilidade, recuperação de desastre, backup e restauração**</span><span class="sxs-lookup"><span data-stu-id="80ce8-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="80ce8-126">Configurar política de failover</span><span class="sxs-lookup"><span data-stu-id="80ce8-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="80ce8-127">Conjuntos de Olá prioridade de failover de cada região em que a conta de saudação é replicada.</span><span class="sxs-lookup"><span data-stu-id="80ce8-127">Sets hello failover priority of each region in which hello account is replicated.</span></span>|
|<span data-ttu-id="80ce8-128">**Conectar o Azure Cosmos DB aos recursos**</span><span class="sxs-lookup"><span data-stu-id="80ce8-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="80ce8-129">Conecte-se um aplicativo de web tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="80ce8-129">Connect a web app tooAzure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="80ce8-130">Criar e conectar um banco de dados do Azure Cosmos DB e um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="80ce8-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
