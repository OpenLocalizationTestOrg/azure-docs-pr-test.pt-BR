---
title: aaaLimitations no banco de dados do Azure para MySQL | Microsoft Docs
description: "Descreve as limitações de visualização no Banco de Dados para MySQL."
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 9c877c592bf640f62182d8761c9c51363882d706
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a><span data-ttu-id="af051-103">Limitações no Banco de Dados do Azure para MySQL (Visualização)</span><span class="sxs-lookup"><span data-stu-id="af051-103">Limitations in Azure Database for MySQL (Preview)</span></span>
<span data-ttu-id="af051-104">saudação de banco de dados do Azure para o serviço MySQL está em visualização pública.</span><span class="sxs-lookup"><span data-stu-id="af051-104">hello Azure Database for MySQL service is in public preview.</span></span> <span data-ttu-id="af051-105">Olá seções a seguir descrevem funcionais limites no serviço de banco de dados de saudação e capacidade.</span><span class="sxs-lookup"><span data-stu-id="af051-105">hello following sections describe capacity and functional limits in hello database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="af051-106">Limites máximos da camada de serviço</span><span class="sxs-lookup"><span data-stu-id="af051-106">Service Tier Maximums</span></span>
<span data-ttu-id="af051-107">O Banco de Dados do Azure para MySQL tem vários níveis de serviço que você pode escolher ao criar um servidor.</span><span class="sxs-lookup"><span data-stu-id="af051-107">Azure Database for MySQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="af051-108">Para saber mais, confira [Entenda o que está disponível em cada camada de serviço](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="af051-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="af051-109">Há um número máximo de conexões, as unidades de computação e armazenamento em cada camada de serviço durante a visualização de serviço hello, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="af051-109">There is a maximum number of connections, compute units, and storage in each service tier during hello service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="af051-110">**Conexões máximas**</span><span class="sxs-lookup"><span data-stu-id="af051-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="af051-111">50 unidades de computação básica</span><span class="sxs-lookup"><span data-stu-id="af051-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="af051-112">50 conexões</span><span class="sxs-lookup"><span data-stu-id="af051-112">50 connections</span></span>    |
| <span data-ttu-id="af051-113">100 unidades de computação básica</span><span class="sxs-lookup"><span data-stu-id="af051-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="af051-114">100 conexões</span><span class="sxs-lookup"><span data-stu-id="af051-114">100 connections</span></span>   |
| <span data-ttu-id="af051-115">100 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="af051-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="af051-116">200 conexões</span><span class="sxs-lookup"><span data-stu-id="af051-116">200 connections</span></span>   |
| <span data-ttu-id="af051-117">200 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="af051-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="af051-118">300 conexões</span><span class="sxs-lookup"><span data-stu-id="af051-118">300 connections</span></span>   |
| <span data-ttu-id="af051-119">400 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="af051-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="af051-120">400 conexões</span><span class="sxs-lookup"><span data-stu-id="af051-120">400 connections</span></span>   |
| <span data-ttu-id="af051-121">800 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="af051-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="af051-122">500 conexões</span><span class="sxs-lookup"><span data-stu-id="af051-122">500 connections</span></span>   |
| <span data-ttu-id="af051-123">**Unidades de computação máxima**</span><span class="sxs-lookup"><span data-stu-id="af051-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="af051-124">Camada de serviço Básica</span><span class="sxs-lookup"><span data-stu-id="af051-124">Basic service tier</span></span>         | <span data-ttu-id="af051-125">100 Unidades de computação</span><span class="sxs-lookup"><span data-stu-id="af051-125">100 Compute Units</span></span> |
| <span data-ttu-id="af051-126">Camada de serviço Standard</span><span class="sxs-lookup"><span data-stu-id="af051-126">Standard service tier</span></span>      | <span data-ttu-id="af051-127">800 Unidades de computação</span><span class="sxs-lookup"><span data-stu-id="af051-127">800 Compute Units</span></span> |
| <span data-ttu-id="af051-128">**Armazenamento Máximo**</span><span class="sxs-lookup"><span data-stu-id="af051-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="af051-129">Camada de serviço Básica</span><span class="sxs-lookup"><span data-stu-id="af051-129">Basic service tier</span></span>         | <span data-ttu-id="af051-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="af051-130">1 TB</span></span>              |
| <span data-ttu-id="af051-131">Camada de serviço Standard</span><span class="sxs-lookup"><span data-stu-id="af051-131">Standard service tier</span></span>      | <span data-ttu-id="af051-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="af051-132">1 TB</span></span>              |

<span data-ttu-id="af051-133">Quando muitas conexões são alcançadas, você pode receber Olá erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="af051-133">When too many connections are reached, you may receive hello following error:</span></span>
> <span data-ttu-id="af051-134">ERRO 1040 (08004): número excessivo de conexões</span><span class="sxs-lookup"><span data-stu-id="af051-134">ERROR 1040 (08004): Too many connections</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="af051-135">Limitações funcionais de visualização:</span><span class="sxs-lookup"><span data-stu-id="af051-135">Preview functional limitations:</span></span>
### <a name="scale-operations"></a><span data-ttu-id="af051-136">Operações de dimensionamento:</span><span class="sxs-lookup"><span data-stu-id="af051-136">Scale operations:</span></span>
1.  <span data-ttu-id="af051-137">Não há suporte para o dimensionamento dinâmico de servidores por meio de camadas de serviço.</span><span class="sxs-lookup"><span data-stu-id="af051-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="af051-138">Ou seja, alternando entre as camadas de serviço Básico e Standard.</span><span class="sxs-lookup"><span data-stu-id="af051-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="af051-139">Não há suporte para o aumento sob demanda dinâmico de armazenamento no servidor criado previamente.</span><span class="sxs-lookup"><span data-stu-id="af051-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="af051-140">Não há suporte para diminuir o tamanho de armazenamento do servidor.</span><span class="sxs-lookup"><span data-stu-id="af051-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="af051-141">Atualizações da versão do servidor:</span><span class="sxs-lookup"><span data-stu-id="af051-141">Server version upgrades:</span></span>
- <span data-ttu-id="af051-142">Não há suporte para a migração automatizada entre versões de mecanismo de banco de dados principal.</span><span class="sxs-lookup"><span data-stu-id="af051-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="af051-143">Gerenciamento de assinaturas:</span><span class="sxs-lookup"><span data-stu-id="af051-143">Subscription management:</span></span>
- <span data-ttu-id="af051-144">Não há suporte para mover dinamicamente servidores criados previamente entre a assinatura e o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="af051-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="af051-145">Recuperação pontual:</span><span class="sxs-lookup"><span data-stu-id="af051-145">Point-in-time-restore:</span></span>
1.  <span data-ttu-id="af051-146">Não é permitido restaurar toodifferent da camada de serviço e/ou tamanho de unidades de computação e armazenamento.</span><span class="sxs-lookup"><span data-stu-id="af051-146">Restoring toodifferent service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="af051-147">Não há suporte para restaurar um servidor eliminado.</span><span class="sxs-lookup"><span data-stu-id="af051-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af051-148">Próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="af051-148">Next Steps:</span></span>
<span data-ttu-id="af051-149">[O que está disponível em cada camada de serviço](concepts-service-tiers.md)
[Versões de Banco de Dados MySQL com suporte](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="af051-149">[What’s available in each service tier](concepts-service-tiers.md)
[Supported MySQL Database Versions](concepts-supported-versions.md)</span></span>
