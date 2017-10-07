---
title: aaaLimitations no banco de dados do Azure para PostgreSQL | Microsoft Docs
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
ms.openlocfilehash: f53dd240e55e0633bc1dfb8ad25e1818fa8ae18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-postgresql"></a><span data-ttu-id="610d6-103">Limitações no Banco de Dados do Azure para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="610d6-103">Limitations in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="610d6-104">saudação de banco de dados PostgreSQL serviço está em visualização pública.</span><span class="sxs-lookup"><span data-stu-id="610d6-104">hello Azure Database for PostgreSQL service is in public preview.</span></span> <span data-ttu-id="610d6-105">Olá seções a seguir descrevem funcionais limites no serviço de banco de dados de saudação e capacidade.</span><span class="sxs-lookup"><span data-stu-id="610d6-105">hello following sections describe capacity and functional limits in hello database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="610d6-106">Limites máximos da camada de serviço</span><span class="sxs-lookup"><span data-stu-id="610d6-106">Service Tier Maximums</span></span>
<span data-ttu-id="610d6-107">O Banco de Dados do Azure para PostgreSQL tem vários níveis de serviço que você pode escolher ao criar um servidor.</span><span class="sxs-lookup"><span data-stu-id="610d6-107">Azure Database for PostgreSQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="610d6-108">Para saber mais, confira [Entenda o que está disponível em cada camada de serviço](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="610d6-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="610d6-109">Há um número máximo de conexões, as unidades de computação e armazenamento em cada camada de serviço durante a visualização de serviço hello, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="610d6-109">There is a maximum number of connections, compute units, and storage in each service tier during hello service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="610d6-110">**Conexões máximas**</span><span class="sxs-lookup"><span data-stu-id="610d6-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="610d6-111">50 unidades de computação básica</span><span class="sxs-lookup"><span data-stu-id="610d6-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="610d6-112">50 conexões</span><span class="sxs-lookup"><span data-stu-id="610d6-112">50 connections</span></span>    |
| <span data-ttu-id="610d6-113">100 unidades de computação básica</span><span class="sxs-lookup"><span data-stu-id="610d6-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="610d6-114">100 conexões</span><span class="sxs-lookup"><span data-stu-id="610d6-114">100 connections</span></span>   |
| <span data-ttu-id="610d6-115">100 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="610d6-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="610d6-116">200 conexões</span><span class="sxs-lookup"><span data-stu-id="610d6-116">200 connections</span></span>   |
| <span data-ttu-id="610d6-117">200 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="610d6-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="610d6-118">300 conexões</span><span class="sxs-lookup"><span data-stu-id="610d6-118">300 connections</span></span>   |
| <span data-ttu-id="610d6-119">400 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="610d6-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="610d6-120">400 conexões</span><span class="sxs-lookup"><span data-stu-id="610d6-120">400 connections</span></span>   |
| <span data-ttu-id="610d6-121">800 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="610d6-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="610d6-122">500 conexões</span><span class="sxs-lookup"><span data-stu-id="610d6-122">500 connections</span></span>   |
| <span data-ttu-id="610d6-123">**Unidades de computação máxima**</span><span class="sxs-lookup"><span data-stu-id="610d6-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="610d6-124">Camada de serviço Básica</span><span class="sxs-lookup"><span data-stu-id="610d6-124">Basic service tier</span></span>         | <span data-ttu-id="610d6-125">100 Unidades de computação</span><span class="sxs-lookup"><span data-stu-id="610d6-125">100 Compute Units</span></span> |
| <span data-ttu-id="610d6-126">Camada de serviço Standard</span><span class="sxs-lookup"><span data-stu-id="610d6-126">Standard service tier</span></span>      | <span data-ttu-id="610d6-127">800 Unidades de computação</span><span class="sxs-lookup"><span data-stu-id="610d6-127">800 Compute Units</span></span> |
| <span data-ttu-id="610d6-128">**Armazenamento Máximo**</span><span class="sxs-lookup"><span data-stu-id="610d6-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="610d6-129">Camada de serviço Básica</span><span class="sxs-lookup"><span data-stu-id="610d6-129">Basic service tier</span></span>         | <span data-ttu-id="610d6-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="610d6-130">1 TB</span></span>              |
| <span data-ttu-id="610d6-131">Camada de serviço Standard</span><span class="sxs-lookup"><span data-stu-id="610d6-131">Standard service tier</span></span>      | <span data-ttu-id="610d6-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="610d6-132">1 TB</span></span>              |

<span data-ttu-id="610d6-133">Quando muitas conexões são alcançadas, você pode receber Olá erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="610d6-133">When too many connections are reached, you may receive hello following error:</span></span>
> <span data-ttu-id="610d6-134">FATAL: já existem muitos clientes</span><span class="sxs-lookup"><span data-stu-id="610d6-134">FATAL:  sorry, too many clients already</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="610d6-135">Limitações funcionais da versão prévia</span><span class="sxs-lookup"><span data-stu-id="610d6-135">Preview functional limitations</span></span>
### <a name="scale-operations"></a><span data-ttu-id="610d6-136">Operações de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="610d6-136">Scale operations</span></span>
1.  <span data-ttu-id="610d6-137">Não há suporte para o dimensionamento dinâmico de servidores por meio de camadas de serviço.</span><span class="sxs-lookup"><span data-stu-id="610d6-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="610d6-138">Ou seja, alternando entre as camadas de serviço Básico e Standard.</span><span class="sxs-lookup"><span data-stu-id="610d6-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="610d6-139">Não há suporte para o aumento sob demanda dinâmico de armazenamento no servidor criado previamente.</span><span class="sxs-lookup"><span data-stu-id="610d6-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="610d6-140">Não há suporte para diminuir o tamanho de armazenamento do servidor.</span><span class="sxs-lookup"><span data-stu-id="610d6-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="610d6-141">Upgrade da versão do servidor</span><span class="sxs-lookup"><span data-stu-id="610d6-141">Server version upgrades</span></span>
- <span data-ttu-id="610d6-142">Não há suporte para a migração automatizada entre versões de mecanismo de banco de dados principal.</span><span class="sxs-lookup"><span data-stu-id="610d6-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="610d6-143">Gerenciamento de assinaturas</span><span class="sxs-lookup"><span data-stu-id="610d6-143">Subscription management</span></span>
- <span data-ttu-id="610d6-144">Não há suporte para mover dinamicamente servidores criados previamente entre a assinatura e o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="610d6-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="610d6-145">Restauração pontual</span><span class="sxs-lookup"><span data-stu-id="610d6-145">Point-in-time-restore</span></span>
1.  <span data-ttu-id="610d6-146">Não é permitido restaurar toodifferent da camada de serviço e/ou tamanho de unidades de computação e armazenamento.</span><span class="sxs-lookup"><span data-stu-id="610d6-146">Restoring toodifferent service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="610d6-147">Não há suporte para restaurar um servidor eliminado.</span><span class="sxs-lookup"><span data-stu-id="610d6-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="610d6-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="610d6-148">Next steps</span></span>
- <span data-ttu-id="610d6-149">Entenda [O que está disponível em cada tipo de preço](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="610d6-149">Understand [What’s available in each pricing tier](concepts-service-tiers.md)</span></span>
- <span data-ttu-id="610d6-150">Entenda as [Versões de banco de dados PostgreSQL com suporte](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="610d6-150">Understand [Supported PostgreSQL Database Versions](concepts-supported-versions.md)</span></span>
- <span data-ttu-id="610d6-151">Revisão [como tooBack backup e restauração de um servidor no banco de dados do Azure para usar PostgreSQL Olá portal do Azure](howto-restore-server-portal.md)</span><span class="sxs-lookup"><span data-stu-id="610d6-151">Review [How tooBack up and Restore a server in Azure Database for PostgreSQL using hello Azure portal](howto-restore-server-portal.md)</span></span>
