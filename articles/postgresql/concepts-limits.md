---
title: "Limitações no Banco de Dados do Azure para PostgreSQL | Microsoft Docs"
description: "Descreve as limitações no Banco de Dados do Azure para PostgreSQL."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: article
ms.date: 06/01/2017
ms.openlocfilehash: 38988fc5c0dc05331ea078534cd1a05e9eca2493
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="limitations-in-azure-database-for-postgresql"></a><span data-ttu-id="3cc53-103">Limitações no Banco de Dados do Azure para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="3cc53-103">Limitations in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="3cc53-104">O Banco de Dados do Azure para o serviço PostgreSQL está em visualização pública.</span><span class="sxs-lookup"><span data-stu-id="3cc53-104">The Azure Database for PostgreSQL service is in public preview.</span></span> <span data-ttu-id="3cc53-105">As seções a seguir descrevem a capacidade e os limites funcionais no serviço de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="3cc53-105">The following sections describe capacity and functional limits in the database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="3cc53-106">Limites máximos da camada de serviço</span><span class="sxs-lookup"><span data-stu-id="3cc53-106">Service Tier Maximums</span></span>
<span data-ttu-id="3cc53-107">O Banco de Dados do Azure para PostgreSQL tem vários níveis de serviço que você pode escolher ao criar um servidor.</span><span class="sxs-lookup"><span data-stu-id="3cc53-107">Azure Database for PostgreSQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="3cc53-108">Para saber mais, confira [Entenda o que está disponível em cada camada de serviço](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="3cc53-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="3cc53-109">Há um número máximo de conexões, unidades de computação e armazenamento em cada camada de serviço durante a visualização do serviço, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3cc53-109">There is a maximum number of connections, compute units, and storage in each service tier during the service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="3cc53-110">**Conexões máximas**</span><span class="sxs-lookup"><span data-stu-id="3cc53-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="3cc53-111">50 unidades de computação básica</span><span class="sxs-lookup"><span data-stu-id="3cc53-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="3cc53-112">50 conexões</span><span class="sxs-lookup"><span data-stu-id="3cc53-112">50 connections</span></span>    |
| <span data-ttu-id="3cc53-113">100 unidades de computação básica</span><span class="sxs-lookup"><span data-stu-id="3cc53-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="3cc53-114">100 conexões</span><span class="sxs-lookup"><span data-stu-id="3cc53-114">100 connections</span></span>   |
| <span data-ttu-id="3cc53-115">100 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="3cc53-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="3cc53-116">200 conexões</span><span class="sxs-lookup"><span data-stu-id="3cc53-116">200 connections</span></span>   |
| <span data-ttu-id="3cc53-117">200 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="3cc53-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="3cc53-118">300 conexões</span><span class="sxs-lookup"><span data-stu-id="3cc53-118">300 connections</span></span>   |
| <span data-ttu-id="3cc53-119">400 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="3cc53-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="3cc53-120">400 conexões</span><span class="sxs-lookup"><span data-stu-id="3cc53-120">400 connections</span></span>   |
| <span data-ttu-id="3cc53-121">800 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="3cc53-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="3cc53-122">500 conexões</span><span class="sxs-lookup"><span data-stu-id="3cc53-122">500 connections</span></span>   |
| <span data-ttu-id="3cc53-123">**Unidades de computação máxima**</span><span class="sxs-lookup"><span data-stu-id="3cc53-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="3cc53-124">Camada de serviço Básica</span><span class="sxs-lookup"><span data-stu-id="3cc53-124">Basic service tier</span></span>         | <span data-ttu-id="3cc53-125">100 Unidades de computação</span><span class="sxs-lookup"><span data-stu-id="3cc53-125">100 Compute Units</span></span> |
| <span data-ttu-id="3cc53-126">Camada de serviço Standard</span><span class="sxs-lookup"><span data-stu-id="3cc53-126">Standard service tier</span></span>      | <span data-ttu-id="3cc53-127">800 Unidades de computação</span><span class="sxs-lookup"><span data-stu-id="3cc53-127">800 Compute Units</span></span> |
| <span data-ttu-id="3cc53-128">**Armazenamento Máximo**</span><span class="sxs-lookup"><span data-stu-id="3cc53-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="3cc53-129">Camada de serviço Básica</span><span class="sxs-lookup"><span data-stu-id="3cc53-129">Basic service tier</span></span>         | <span data-ttu-id="3cc53-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="3cc53-130">1 TB</span></span>              |
| <span data-ttu-id="3cc53-131">Camada de serviço Standard</span><span class="sxs-lookup"><span data-stu-id="3cc53-131">Standard service tier</span></span>      | <span data-ttu-id="3cc53-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="3cc53-132">1 TB</span></span>              |

<span data-ttu-id="3cc53-133">Quando um número excessivo de conexões for atingido, você receberá o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="3cc53-133">When too many connections are reached, you may receive the following error:</span></span>
> <span data-ttu-id="3cc53-134">FATAL: já existem muitos clientes</span><span class="sxs-lookup"><span data-stu-id="3cc53-134">FATAL:  sorry, too many clients already</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="3cc53-135">Limitações funcionais da versão prévia</span><span class="sxs-lookup"><span data-stu-id="3cc53-135">Preview functional limitations</span></span>
### <a name="scale-operations"></a><span data-ttu-id="3cc53-136">Operações de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="3cc53-136">Scale operations</span></span>
1.  <span data-ttu-id="3cc53-137">Não há suporte para o dimensionamento dinâmico de servidores por meio de camadas de serviço.</span><span class="sxs-lookup"><span data-stu-id="3cc53-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="3cc53-138">Ou seja, alternando entre as camadas de serviço Básico e Standard.</span><span class="sxs-lookup"><span data-stu-id="3cc53-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="3cc53-139">Não há suporte para o aumento sob demanda dinâmico de armazenamento no servidor criado previamente.</span><span class="sxs-lookup"><span data-stu-id="3cc53-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="3cc53-140">Não há suporte para diminuir o tamanho de armazenamento do servidor.</span><span class="sxs-lookup"><span data-stu-id="3cc53-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="3cc53-141">Upgrade da versão do servidor</span><span class="sxs-lookup"><span data-stu-id="3cc53-141">Server version upgrades</span></span>
- <span data-ttu-id="3cc53-142">Não há suporte para a migração automatizada entre versões de mecanismo de banco de dados principal.</span><span class="sxs-lookup"><span data-stu-id="3cc53-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="3cc53-143">Gerenciamento de assinaturas</span><span class="sxs-lookup"><span data-stu-id="3cc53-143">Subscription management</span></span>
- <span data-ttu-id="3cc53-144">Não há suporte para mover dinamicamente servidores criados previamente entre a assinatura e o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3cc53-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="3cc53-145">Restauração pontual</span><span class="sxs-lookup"><span data-stu-id="3cc53-145">Point-in-time-restore</span></span>
1.  <span data-ttu-id="3cc53-146">Não é permitido restaurar para a camada de serviço diferente e/ou Unidades de computação e Tamanho do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3cc53-146">Restoring to different service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="3cc53-147">Não há suporte para restaurar um servidor eliminado.</span><span class="sxs-lookup"><span data-stu-id="3cc53-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cc53-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3cc53-148">Next steps</span></span>
- <span data-ttu-id="3cc53-149">Entenda [O que está disponível em cada tipo de preço](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="3cc53-149">Understand [What’s available in each pricing tier](concepts-service-tiers.md)</span></span>
- <span data-ttu-id="3cc53-150">Entenda as [Versões de banco de dados PostgreSQL com suporte](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="3cc53-150">Understand [Supported PostgreSQL Database Versions](concepts-supported-versions.md)</span></span>
- <span data-ttu-id="3cc53-151">Veja [Como fazer backup e restaurar um servidor no Banco de Dados do Azure para PostgreSQL usando o Portal do Azure](howto-restore-server-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3cc53-151">Review [How To Back up and Restore a server in Azure Database for PostgreSQL using the Azure portal](howto-restore-server-portal.md)</span></span>
