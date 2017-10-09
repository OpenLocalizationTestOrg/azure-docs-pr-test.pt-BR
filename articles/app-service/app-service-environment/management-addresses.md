---
title: "endereços de gerenciamento do ambiente de serviço de aplicativo aaaAzure"
description: "Listas de endereços de gerenciamento de saudação usado toocommand um ambiente de serviço de aplicativo"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a7738a24-89ef-43d3-bff1-77f43d5a3952
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: b34b6266dc3a35915421b14bf34eddc07c2825c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-management-addresses"></a><span data-ttu-id="e3d26-103">Endereços de gerenciamento de Ambiente de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="e3d26-103">App Service Environment management addresses</span></span>

<span data-ttu-id="e3d26-104">Olá Environment(ASE) do serviço de aplicativo é uma implantação de saudação do serviço de aplicativo do Azure em uma sub-rede em sua rede Virtual do Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="e3d26-104">hello App Service Environment(ASE) is a deployment of hello Azure App Service into a subnet in your Azure Virtual Network (VNet).</span></span>  <span data-ttu-id="e3d26-105">Olá ASE deve ser acessível de saudação do serviço de aplicativo do Azure para que ele possa ser gerenciado.</span><span class="sxs-lookup"><span data-stu-id="e3d26-105">hello ASE must be accessible from hello Azure App Service so that it can be managed.</span></span>  <span data-ttu-id="e3d26-106">Esse tráfego de gerenciamento ASE atravessa a rede de controlado pelo usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3d26-106">This ASE management traffic traverses hello user controlled network.</span></span>  <span data-ttu-id="e3d26-107">Ela é proveniente do serviço de aplicativo do Azure gerenciamento servidores toohello VIP público associado ASE hello.</span><span class="sxs-lookup"><span data-stu-id="e3d26-107">It comes from Azure App Service management servers toohello public VIP that is associated with hello ASE.</span></span>  <span data-ttu-id="e3d26-108">Para obter detalhes sobre Olá ASE rede dependências ler [Olá ambiente de serviço de aplicativo e considerações de rede][networking].</span><span class="sxs-lookup"><span data-stu-id="e3d26-108">For details on hello ASE networking dependencies read [Networking considerations and hello App Service Environment][networking].</span></span>  <span data-ttu-id="e3d26-109">Para obter informações gerais sobre ASE hello, você pode iniciar com [Introdução toohello ambiente de serviço de aplicativo][intro].</span><span class="sxs-lookup"><span data-stu-id="e3d26-109">For general information on hello ASE you can start with [Introduction toohello App Service Environment][intro].</span></span>

<span data-ttu-id="e3d26-110">Este documento lista Olá IPs de origem toohello de tráfego de gerenciamento ASE.</span><span class="sxs-lookup"><span data-stu-id="e3d26-110">This document lists hello source IPs for management traffic toohello ASE.</span></span> <span data-ttu-id="e3d26-111">Você pode usar toolock de grupos de segurança de rede de toocreate esses endereços para baixo tráfego de entrada ou usá-los em tabelas de rotas, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="e3d26-111">You can use these addresses toocreate Network Security Groups toolock down incoming traffic or use them in Route Tables as needed.</span></span>  <span data-ttu-id="e3d26-112">toouse essas informações precisam toouse:</span><span class="sxs-lookup"><span data-stu-id="e3d26-112">toouse this information you need toouse:</span></span>

* <span data-ttu-id="e3d26-113">endereços IP Hello listados para todas as regiões</span><span class="sxs-lookup"><span data-stu-id="e3d26-113">hello IP addresses that are listed for All regions</span></span>
* <span data-ttu-id="e3d26-114">os endereços de IP de saudação correspondência toohello região que sua ASE é implantado em.</span><span class="sxs-lookup"><span data-stu-id="e3d26-114">hello IP addresses that match toohello region that your ASE is deployed into.</span></span>

<span data-ttu-id="e3d26-115">o tráfego de gerenciamento entrada Hello proveniente esses endereços IP tooports 454 e 455.</span><span class="sxs-lookup"><span data-stu-id="e3d26-115">hello incoming management traffic comes in from these IP addresses tooports 454 and 455.</span></span>

| <span data-ttu-id="e3d26-116">Região</span><span class="sxs-lookup"><span data-stu-id="e3d26-116">Region</span></span> | <span data-ttu-id="e3d26-117">Endereços</span><span class="sxs-lookup"><span data-stu-id="e3d26-117">Addresses</span></span> |
|--------|-----------|
| <span data-ttu-id="e3d26-118">Todas as regiões</span><span class="sxs-lookup"><span data-stu-id="e3d26-118">All regions</span></span> | <span data-ttu-id="e3d26-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span><span class="sxs-lookup"><span data-stu-id="e3d26-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span></span> |
| <span data-ttu-id="e3d26-120">Centro-Sul dos EUA e Centro-Norte dos EUA</span><span class="sxs-lookup"><span data-stu-id="e3d26-120">South Central US & North Central US</span></span> | <span data-ttu-id="e3d26-121">23.102.188.65, 191.236.154.88</span><span class="sxs-lookup"><span data-stu-id="e3d26-121">23.102.188.65, 191.236.154.88</span></span> |
| <span data-ttu-id="e3d26-122">Sudeste da Austrália e Leste da Austrália</span><span class="sxs-lookup"><span data-stu-id="e3d26-122">Australia Southeast & Australia East</span></span> | <span data-ttu-id="e3d26-123">23.101.234.41, 104.210.90.65</span><span class="sxs-lookup"><span data-stu-id="e3d26-123">23.101.234.41, 104.210.90.65</span></span> |
| <span data-ttu-id="e3d26-124">Oeste dos EUA e Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="e3d26-124">US West & US East</span></span> | <span data-ttu-id="e3d26-125">104.45.227.37, 191.236.60.72</span><span class="sxs-lookup"><span data-stu-id="e3d26-125">104.45.227.37, 191.236.60.72</span></span> |
| <span data-ttu-id="e3d26-126">Europa Ocidental e Europa Setentrional</span><span class="sxs-lookup"><span data-stu-id="e3d26-126">West Europe & North Europe</span></span> | <span data-ttu-id="e3d26-127">191.233.94.45, 191.237.222.191</span><span class="sxs-lookup"><span data-stu-id="e3d26-127">191.233.94.45, 191.237.222.191</span></span> |
| <span data-ttu-id="e3d26-128">Centro-Oeste dos EUA e Oeste dos EUA 2</span><span class="sxs-lookup"><span data-stu-id="e3d26-128">West Central US & West US 2</span></span> | <span data-ttu-id="e3d26-129">13.78.148.75, 13.66.225.188</span><span class="sxs-lookup"><span data-stu-id="e3d26-129">13.78.148.75, 13.66.225.188</span></span> |
| <span data-ttu-id="e3d26-130">EUA Central e Leste dos EUA 2</span><span class="sxs-lookup"><span data-stu-id="e3d26-130">Central US & East US 2</span></span> | <span data-ttu-id="e3d26-131">104.43.165.73, 104.46.108.135</span><span class="sxs-lookup"><span data-stu-id="e3d26-131">104.43.165.73, 104.46.108.135</span></span> |
| <span data-ttu-id="e3d26-132">Ásia Oriental e Sudeste Asiático</span><span class="sxs-lookup"><span data-stu-id="e3d26-132">East Asia & Southeast Asia</span></span> | <span data-ttu-id="e3d26-133">23.99.115.5, 104.215.158.33</span><span class="sxs-lookup"><span data-stu-id="e3d26-133">23.99.115.5, 104.215.158.33</span></span> |
| <span data-ttu-id="e3d26-134">Leste do Japão e Oeste do Japão</span><span class="sxs-lookup"><span data-stu-id="e3d26-134">Japan East & Japan West</span></span> | <span data-ttu-id="e3d26-135">104.41.185.116, 191.239.104.48</span><span class="sxs-lookup"><span data-stu-id="e3d26-135">104.41.185.116, 191.239.104.48</span></span> |
| <span data-ttu-id="e3d26-136">Centro do Canadá e Leste do Canadá</span><span class="sxs-lookup"><span data-stu-id="e3d26-136">Canada Central & Canada East</span></span> | <span data-ttu-id="e3d26-137">40.85.230.101, 40.86.229.100</span><span class="sxs-lookup"><span data-stu-id="e3d26-137">40.85.230.101, 40.86.229.100</span></span> |
| <span data-ttu-id="e3d26-138">Oeste do Reino Unido e Sul do Reino Unido</span><span class="sxs-lookup"><span data-stu-id="e3d26-138">UK West & UK South</span></span> | <span data-ttu-id="e3d26-139">51.141.8.34, 51.140.185.75</span><span class="sxs-lookup"><span data-stu-id="e3d26-139">51.141.8.34, 51.140.185.75</span></span> |
| <span data-ttu-id="e3d26-140">Sul da Coreia e Centro da Coreia</span><span class="sxs-lookup"><span data-stu-id="e3d26-140">Korea South & Korea Central</span></span> | <span data-ttu-id="e3d26-141">52.231.200.177, 52.231.32.117</span><span class="sxs-lookup"><span data-stu-id="e3d26-141">52.231.200.177, 52.231.32.117</span></span> |
| <span data-ttu-id="e3d26-142">Sul do Brasil e Centro-Sul dos EUA</span><span class="sxs-lookup"><span data-stu-id="e3d26-142">Brazil South & South Central US</span></span>| <span data-ttu-id="e3d26-143">104.41.46.178, 23.102.188.65</span><span class="sxs-lookup"><span data-stu-id="e3d26-143">104.41.46.178, 23.102.188.65</span></span> |
| <span data-ttu-id="e3d26-144">Índia Central e Sul da Índia</span><span class="sxs-lookup"><span data-stu-id="e3d26-144">Central India & South India</span></span> | <span data-ttu-id="e3d26-145">104.211.98.24, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="e3d26-145">104.211.98.24, 104.211.225.66</span></span> |
| <span data-ttu-id="e3d26-146">Índia Ocidental e Sul da Índia</span><span class="sxs-lookup"><span data-stu-id="e3d26-146">West India & South India</span></span> | <span data-ttu-id="e3d26-147">104.211.160.229, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="e3d26-147">104.211.160.229, 104.211.225.66</span></span> |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
