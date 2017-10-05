---
title: "Limitações no Banco de Dados do Azure para MySQL | Microsoft Docs"
description: "Descreve as limitações de visualização no Banco de Dados para MySQL."
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c61d70897b66c2ffee819ac98c38ab75000db907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a><span data-ttu-id="f6bc6-103">Limitações no Banco de Dados do Azure para MySQL (Visualização)</span><span class="sxs-lookup"><span data-stu-id="f6bc6-103">Limitations in Azure Database for MySQL (Preview)</span></span>
<span data-ttu-id="f6bc6-104">O Banco de Dados do Azure para o serviço do MySQL está em visualização pública.</span><span class="sxs-lookup"><span data-stu-id="f6bc6-104">The Azure Database for MySQL service is in public preview.</span></span> <span data-ttu-id="f6bc6-105">As seções a seguir descrevem a capacidade e os limites funcionais no serviço de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f6bc6-105">The following sections describe capacity and functional limits in the database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="f6bc6-106">Limites máximos da camada de serviço</span><span class="sxs-lookup"><span data-stu-id="f6bc6-106">Service Tier Maximums</span></span>
<span data-ttu-id="f6bc6-107">O Banco de Dados do Azure para MySQL tem vários níveis de serviço que você pode escolher ao criar um servidor.</span><span class="sxs-lookup"><span data-stu-id="f6bc6-107">Azure Database for MySQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="f6bc6-108">Para saber mais, confira [Entenda o que está disponível em cada camada de serviço](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="f6bc6-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="f6bc6-109">Há um número máximo de conexões, unidades de computação e armazenamento em cada camada de serviço durante a visualização do serviço, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f6bc6-109">There is a maximum number of connections, compute units, and storage in each service tier during the service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="f6bc6-110">**Conexões máximas**</span><span class="sxs-lookup"><span data-stu-id="f6bc6-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="f6bc6-111">50 unidades de computação básica</span><span class="sxs-lookup"><span data-stu-id="f6bc6-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="f6bc6-112">50 conexões</span><span class="sxs-lookup"><span data-stu-id="f6bc6-112">50 connections</span></span>    |
| <span data-ttu-id="f6bc6-113">100 unidades de computação básica</span><span class="sxs-lookup"><span data-stu-id="f6bc6-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="f6bc6-114">100 conexões</span><span class="sxs-lookup"><span data-stu-id="f6bc6-114">100 connections</span></span>   |
| <span data-ttu-id="f6bc6-115">100 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="f6bc6-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="f6bc6-116">200 conexões</span><span class="sxs-lookup"><span data-stu-id="f6bc6-116">200 connections</span></span>   |
| <span data-ttu-id="f6bc6-117">200 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="f6bc6-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="f6bc6-118">300 conexões</span><span class="sxs-lookup"><span data-stu-id="f6bc6-118">300 connections</span></span>   |
| <span data-ttu-id="f6bc6-119">400 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="f6bc6-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="f6bc6-120">400 conexões</span><span class="sxs-lookup"><span data-stu-id="f6bc6-120">400 connections</span></span>   |
| <span data-ttu-id="f6bc6-121">800 unidades de computação standard</span><span class="sxs-lookup"><span data-stu-id="f6bc6-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="f6bc6-122">500 conexões</span><span class="sxs-lookup"><span data-stu-id="f6bc6-122">500 connections</span></span>   |
| <span data-ttu-id="f6bc6-123">**Unidades de computação máxima**</span><span class="sxs-lookup"><span data-stu-id="f6bc6-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="f6bc6-124">Camada de serviço Básica</span><span class="sxs-lookup"><span data-stu-id="f6bc6-124">Basic service tier</span></span>         | <span data-ttu-id="f6bc6-125">100 Unidades de computação</span><span class="sxs-lookup"><span data-stu-id="f6bc6-125">100 Compute Units</span></span> |
| <span data-ttu-id="f6bc6-126">Camada de serviço Standard</span><span class="sxs-lookup"><span data-stu-id="f6bc6-126">Standard service tier</span></span>      | <span data-ttu-id="f6bc6-127">800 Unidades de computação</span><span class="sxs-lookup"><span data-stu-id="f6bc6-127">800 Compute Units</span></span> |
| <span data-ttu-id="f6bc6-128">**Armazenamento Máximo**</span><span class="sxs-lookup"><span data-stu-id="f6bc6-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="f6bc6-129">Camada de serviço Básica</span><span class="sxs-lookup"><span data-stu-id="f6bc6-129">Basic service tier</span></span>         | <span data-ttu-id="f6bc6-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="f6bc6-130">1 TB</span></span>              |
| <span data-ttu-id="f6bc6-131">Camada de serviço Standard</span><span class="sxs-lookup"><span data-stu-id="f6bc6-131">Standard service tier</span></span>      | <span data-ttu-id="f6bc6-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="f6bc6-132">1 TB</span></span>              |

<span data-ttu-id="f6bc6-133">Quando um número excessivo de conexões for atingido, você receberá o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="f6bc6-133">When too many connections are reached, you may receive the following error:</span></span>
> <span data-ttu-id="f6bc6-134">ERRO 1040 (08004): número excessivo de conexões</span><span class="sxs-lookup"><span data-stu-id="f6bc6-134">ERROR 1040 (08004): Too many connections</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="f6bc6-135">Limitações funcionais de visualização:</span><span class="sxs-lookup"><span data-stu-id="f6bc6-135">Preview functional limitations:</span></span>
### <a name="scale-operations"></a><span data-ttu-id="f6bc6-136">Operações de dimensionamento:</span><span class="sxs-lookup"><span data-stu-id="f6bc6-136">Scale operations:</span></span>
1.  <span data-ttu-id="f6bc6-137">Não há suporte para o dimensionamento dinâmico de servidores por meio de camadas de serviço.</span><span class="sxs-lookup"><span data-stu-id="f6bc6-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="f6bc6-138">Ou seja, alternando entre as camadas de serviço Básico e Standard.</span><span class="sxs-lookup"><span data-stu-id="f6bc6-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="f6bc6-139">Não há suporte para o aumento sob demanda dinâmico de armazenamento no servidor criado previamente.</span><span class="sxs-lookup"><span data-stu-id="f6bc6-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="f6bc6-140">Não há suporte para diminuir o tamanho de armazenamento do servidor.</span><span class="sxs-lookup"><span data-stu-id="f6bc6-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="f6bc6-141">Atualizações da versão do servidor:</span><span class="sxs-lookup"><span data-stu-id="f6bc6-141">Server version upgrades:</span></span>
- <span data-ttu-id="f6bc6-142">Não há suporte para a migração automatizada entre versões de mecanismo de banco de dados principal.</span><span class="sxs-lookup"><span data-stu-id="f6bc6-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="f6bc6-143">Gerenciamento de assinaturas:</span><span class="sxs-lookup"><span data-stu-id="f6bc6-143">Subscription management:</span></span>
- <span data-ttu-id="f6bc6-144">Não há suporte para mover dinamicamente servidores criados previamente entre a assinatura e o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f6bc6-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="f6bc6-145">Recuperação pontual:</span><span class="sxs-lookup"><span data-stu-id="f6bc6-145">Point-in-time-restore:</span></span>
1.  <span data-ttu-id="f6bc6-146">Não é permitido restaurar para a camada de serviço diferente e/ou Unidades de computação e Tamanho do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f6bc6-146">Restoring to different service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="f6bc6-147">Não há suporte para restaurar um servidor eliminado.</span><span class="sxs-lookup"><span data-stu-id="f6bc6-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6bc6-148">Próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="f6bc6-148">Next Steps:</span></span>
<span data-ttu-id="f6bc6-149">[O que está disponível em cada camada de serviço](concepts-service-tiers.md)
[Versões de Banco de Dados MySQL com suporte](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="f6bc6-149">[What’s available in each service tier](concepts-service-tiers.md)
[Supported MySQL Database Versions](concepts-supported-versions.md)</span></span>
