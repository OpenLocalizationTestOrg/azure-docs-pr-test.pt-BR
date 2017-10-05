---
title: Exemplos do Azure PowerShell para o BD Cosmos do Azure | Microsoft Docs
description: "Exemplos do Azure PowerShell – scripts para ajudá-lo a criar contas do BD Cosmos do Azure."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 7698e03c0dc8d1c6d1e926f45e903a909bfd0c93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples-for-azure-cosmos-db"></a><span data-ttu-id="d8b82-103">Exemplos do Azure PowerShell para o BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="d8b82-103">Azure PowerShell samples for Azure Cosmos DB</span></span>

<span data-ttu-id="d8b82-104">A tabela a seguir inclui links para scripts de exemplo do Azure PowerShell para o BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8b82-104">The following table includes links to sample Azure PowerShell scripts for Azure Cosmos DB.</span></span>

| |  |
|---|---|
|<span data-ttu-id="d8b82-105">**Criar uma conta do BD Cosmos do Azure**</span><span class="sxs-lookup"><span data-stu-id="d8b82-105">**Create an Azure Cosmos DB account**</span></span>||
|[<span data-ttu-id="d8b82-106">Criar uma conta da API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d8b82-106">Create a DocumentDB API account</span></span>](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="d8b82-107">Cria uma única conta do BD Cosmos do Azure para ser usada com a API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d8b82-107">Creates a single Azure Cosmos DB account to use with the DocumentDB API.</span></span> |
|<span data-ttu-id="d8b82-108">**Dimensionar o BD Cosmos do Azure**</span><span class="sxs-lookup"><span data-stu-id="d8b82-108">**Scale Azure Cosmos DB**</span></span>||
|[<span data-ttu-id="d8b82-109">Replicar uma conta do BD Cosmos do Azure em várias regiões e configurar as prioridades de failover</span><span class="sxs-lookup"><span data-stu-id="d8b82-109">Replicate Azure Cosmos DB account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="d8b82-110">Replica globalmente os dados da conta em várias regiões com uma prioridade de failover especificada.</span><span class="sxs-lookup"><span data-stu-id="d8b82-110">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="d8b82-111">**Proteger o Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="d8b82-111">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="d8b82-112">Obter chaves da conta</span><span class="sxs-lookup"><span data-stu-id="d8b82-112">Get account keys</span></span>](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="d8b82-113">Obtém a chaves de gravação mestre primária e secundária e as chaves somente leitura primária e secundária da conta.</span><span class="sxs-lookup"><span data-stu-id="d8b82-113">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="d8b82-114">Obter cadeia de conexão do MongoDB</span><span class="sxs-lookup"><span data-stu-id="d8b82-114">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="d8b82-115">Obtém a cadeia de conexão para conectar seu aplicativo MongoDB à sua conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d8b82-115">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="d8b82-116">Regenerar chaves da conta</span><span class="sxs-lookup"><span data-stu-id="d8b82-116">Regenerate account keys</span></span>](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="d8b82-117">Regenera a chave mestre ou somente leitura da conta.</span><span class="sxs-lookup"><span data-stu-id="d8b82-117">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="d8b82-118">Criar um firewall</span><span class="sxs-lookup"><span data-stu-id="d8b82-118">Create a firewall</span></span>](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="d8b82-119">Cria uma política de controle de acesso IP de entrada para limitar o acesso à conta por um conjunto aprovado de máquinas e/ou serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="d8b82-119">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="d8b82-120">**Alta disponibilidade, recuperação de desastre, backup e restauração**</span><span class="sxs-lookup"><span data-stu-id="d8b82-120">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="d8b82-121">Configurar política de failover</span><span class="sxs-lookup"><span data-stu-id="d8b82-121">Configure failover policy</span></span>](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="d8b82-122">Define a prioridade de failover para cada região em que a conta é replicada.</span><span class="sxs-lookup"><span data-stu-id="d8b82-122">Sets the failover priority of each region in which the account is replicated.</span></span>|
|||