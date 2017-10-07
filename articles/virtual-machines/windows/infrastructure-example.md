---
title: aaaExample passo a passo de infraestrutura do Azure | Microsoft Docs
description: "Saiba mais sobre Olá chave design e implementação diretrizes para implantar uma infraestrutura de exemplo no Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7032b586-e4e5-4954-952f-fdfc03fc1980
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd6b6e904404bea0b5be37dfce6d60039daae636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a><span data-ttu-id="5dd04-103">Passo a passo da infraestrutura do Azure de exemplo para VMs Windows</span><span class="sxs-lookup"><span data-stu-id="5dd04-103">Example Azure infrastructure walkthrough for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="5dd04-104">Este artigo explica como criar uma infraestrutura de aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="5dd04-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="5dd04-105">Nós de detalhe projetar uma infraestrutura de uma loja online simple que reúne todas as diretrizes de saudação e decisões relacionadas a convenções de nomenclatura, conjuntos de disponibilidade, redes virtuais e balanceadores de carga e realmente implantar suas máquinas virtuais (VMs).</span><span class="sxs-lookup"><span data-stu-id="5dd04-105">We detail designing an infrastructure for a simple on-line store that brings together all hello guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="5dd04-106">Carga de trabalho de exemplo</span><span class="sxs-lookup"><span data-stu-id="5dd04-106">Example workload</span></span>
<span data-ttu-id="5dd04-107">A Adventure Works Cycles deseja toobuild um aplicativo da loja online no Azure consiste em:</span><span class="sxs-lookup"><span data-stu-id="5dd04-107">Adventure Works Cycles wants toobuild an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="5dd04-108">Dois servidores IIS executando Olá cliente front-end em uma camada da web</span><span class="sxs-lookup"><span data-stu-id="5dd04-108">Two IIS servers running hello client front-end in a web tier</span></span>
* <span data-ttu-id="5dd04-109">Dois servidores IIS que processam dados e pedidos em uma camada de aplicativo</span><span class="sxs-lookup"><span data-stu-id="5dd04-109">Two IIS servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="5dd04-110">Duas instâncias do Microsoft SQL Server com grupos de disponibilidade AlwaysOn (dois SQL Servers e uma testemunha do nó principal) para armazenar dados de produtos e pedidos em uma camada de banco de dados</span><span class="sxs-lookup"><span data-stu-id="5dd04-110">Two Microsoft SQL Server instances with AlwaysOn availability groups (two SQL Servers and a majority node witness) for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="5dd04-111">Dois controladores de domínio do Active Directory para contas de clientes e fornecedores em uma camada de autenticação</span><span class="sxs-lookup"><span data-stu-id="5dd04-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="5dd04-112">Todos os servidores de saudação estão localizados em duas sub-redes:</span><span class="sxs-lookup"><span data-stu-id="5dd04-112">All hello servers are located in two subnets:</span></span>
  * <span data-ttu-id="5dd04-113">uma sub-rede front-end para servidores de web Olá</span><span class="sxs-lookup"><span data-stu-id="5dd04-113">a front-end subnet for hello web servers</span></span> 
  * <span data-ttu-id="5dd04-114">uma sub-rede de back-end para servidores de aplicativo hello, cluster SQL e os controladores de domínio</span><span class="sxs-lookup"><span data-stu-id="5dd04-114">a back-end subnet for hello application servers, SQL cluster, and domain controllers</span></span>

![Diagrama de níveis diferentes de infraestrutura de aplicativos](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="5dd04-116">Entrada proteger tráfego da web deve ser balanceamento de carga entre os servidores web hello como clientes procurar repositório online hello.</span><span class="sxs-lookup"><span data-stu-id="5dd04-116">Incoming secure web traffic must be load-balanced among hello web servers as customers browse hello on-line store.</span></span> <span data-ttu-id="5dd04-117">Ordem de processamento do tráfego na forma de saudação do HTTP solicitações da web hello servidores devem ser balanceados entre os servidores de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5dd04-117">Order processing traffic in hello form of HTTP requests from hello web servers must be balanced among hello application servers.</span></span> <span data-ttu-id="5dd04-118">Além disso, a infraestrutura de saudação deve ser criada para alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5dd04-118">Additionally, hello infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="5dd04-119">design resultante Olá deve incorporar:</span><span class="sxs-lookup"><span data-stu-id="5dd04-119">hello resulting design must incorporate:</span></span>

* <span data-ttu-id="5dd04-120">Uma assinatura e uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="5dd04-120">An Azure subscription and account</span></span>
* <span data-ttu-id="5dd04-121">Um único grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="5dd04-121">A single resource group</span></span>
* <span data-ttu-id="5dd04-122">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="5dd04-122">Azure Managed Disks</span></span>
* <span data-ttu-id="5dd04-123">Uma rede virtual com duas sub-redes</span><span class="sxs-lookup"><span data-stu-id="5dd04-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="5dd04-124">Conjuntos de disponibilidade para Olá VMs com funções semelhantes</span><span class="sxs-lookup"><span data-stu-id="5dd04-124">Availability sets for hello VMs with a similar role</span></span>
* <span data-ttu-id="5dd04-125">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="5dd04-125">Virtual machines</span></span>

<span data-ttu-id="5dd04-126">Todos os Olá acima siga estas convenções de nomenclatura:</span><span class="sxs-lookup"><span data-stu-id="5dd04-126">All hello above follow these naming conventions:</span></span>

* <span data-ttu-id="5dd04-127">A Adventure Works Cycles usa **[carga de trabalho de TI]-[localização]-[recurso do Azure]** como prefixo</span><span class="sxs-lookup"><span data-stu-id="5dd04-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="5dd04-128">Neste exemplo, "**azos**" (repositório online do Azure) é Olá nome da carga de trabalho de TI e "**usar**" (Leste dos EUA 2) é o local de saudação</span><span class="sxs-lookup"><span data-stu-id="5dd04-128">For this example, "**azos**" (Azure On-line Store) is hello IT workload name and "**use**" (East US 2) is hello location</span></span>
* <span data-ttu-id="5dd04-129">As redes virtuais usam AZOS-USE-VN**[número]**</span><span class="sxs-lookup"><span data-stu-id="5dd04-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="5dd04-130">Os conjuntos de disponibilidade usam azos-use-as-**[função]**</span><span class="sxs-lookup"><span data-stu-id="5dd04-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="5dd04-131">Os nomes de máquina virtual usam azos-use-vm-**[nomevm]**</span><span class="sxs-lookup"><span data-stu-id="5dd04-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="5dd04-132">Assinaturas e contas do Azure</span><span class="sxs-lookup"><span data-stu-id="5dd04-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="5dd04-133">A Adventure Works Cycles é usando sua assinatura do Enterprise, chamada assinatura de empresa Adventure Works, tooprovide cobrança para essa carga de trabalho de TI.</span><span class="sxs-lookup"><span data-stu-id="5dd04-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, tooprovide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="5dd04-134">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="5dd04-134">Storage</span></span>
<span data-ttu-id="5dd04-135">A Adventure Works Cycles determinou que deverá usar o Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="5dd04-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="5dd04-136">Ao criar VMs, ambas as camadas de armazenamento disponíveis para o armazenamento são usadas:</span><span class="sxs-lookup"><span data-stu-id="5dd04-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="5dd04-137">**Armazenamento padrão** para servidores de web hello, servidores de aplicativos e os controladores de domínio e seus discos de dados.</span><span class="sxs-lookup"><span data-stu-id="5dd04-137">**Standard storage** for hello web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="5dd04-138">**Armazenamento Premium** para Olá VMs do SQL Server e seus discos de dados.</span><span class="sxs-lookup"><span data-stu-id="5dd04-138">**Premium storage** for hello SQL Server VMs and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="5dd04-139">Rede virtual e sub-redes</span><span class="sxs-lookup"><span data-stu-id="5dd04-139">Virtual network and subnets</span></span>
<span data-ttu-id="5dd04-140">Porque a rede virtual Olá não precisa de rede local do contínuos de conectividade toohello Adventure ciclos de trabalho, eles decidiram em uma rede virtual somente em nuvem.</span><span class="sxs-lookup"><span data-stu-id="5dd04-140">Because hello virtual network does not need ongoing connectivity toohello Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="5dd04-141">Criaram uma rede virtual somente em nuvem com hello configurações usando o portal do Azure de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="5dd04-141">They created a cloud-only virtual network with hello following settings using hello Azure portal:</span></span>

* <span data-ttu-id="5dd04-142">Name: AZOS-USE-VN01</span><span class="sxs-lookup"><span data-stu-id="5dd04-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="5dd04-143">Local: Leste dos EUA 2</span><span class="sxs-lookup"><span data-stu-id="5dd04-143">Location: East US 2</span></span>
* <span data-ttu-id="5dd04-144">Espaço de endereço da rede virtual: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="5dd04-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="5dd04-145">Primeira sub-rede:</span><span class="sxs-lookup"><span data-stu-id="5dd04-145">First subnet:</span></span>
  * <span data-ttu-id="5dd04-146">Nome: FrontEnd</span><span class="sxs-lookup"><span data-stu-id="5dd04-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="5dd04-147">Espaço de endereço: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="5dd04-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="5dd04-148">Segunda sub-rede:</span><span class="sxs-lookup"><span data-stu-id="5dd04-148">Second subnet:</span></span>
  * <span data-ttu-id="5dd04-149">Nome: BackEnd</span><span class="sxs-lookup"><span data-stu-id="5dd04-149">Name: BackEnd</span></span>
  * <span data-ttu-id="5dd04-150">Espaço de endereço: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="5dd04-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="5dd04-151">Conjuntos de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="5dd04-151">Availability sets</span></span>
<span data-ttu-id="5dd04-152">toomaintain alta disponibilidade de todos os quatro níveis de sua loja online, a Adventure Works Cycles decidiu em quatro conjuntos de disponibilidade:</span><span class="sxs-lookup"><span data-stu-id="5dd04-152">toomaintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="5dd04-153">**use azos como web** Olá para servidores de web</span><span class="sxs-lookup"><span data-stu-id="5dd04-153">**azos-use-as-web** for hello web servers</span></span>
* <span data-ttu-id="5dd04-154">**usar azos como aplicativo** Olá para servidores de aplicativos</span><span class="sxs-lookup"><span data-stu-id="5dd04-154">**azos-use-as-app** for hello application servers</span></span>
* <span data-ttu-id="5dd04-155">**use azos como sql** para Olá SQL Servers</span><span class="sxs-lookup"><span data-stu-id="5dd04-155">**azos-use-as-sql** for hello SQL Servers</span></span>
* <span data-ttu-id="5dd04-156">**use azos como dc** Olá para controladores de domínio</span><span class="sxs-lookup"><span data-stu-id="5dd04-156">**azos-use-as-dc** for hello domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="5dd04-157">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="5dd04-157">Virtual machines</span></span>
<span data-ttu-id="5dd04-158">A Adventure Works Cycles decidido Olá nomes para suas VMs do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="5dd04-158">Adventure Works Cycles decided on hello following names for their Azure VMs:</span></span>

* <span data-ttu-id="5dd04-159">**azos-use vm web01** Olá primeiro servidor de web</span><span class="sxs-lookup"><span data-stu-id="5dd04-159">**azos-use-vm-web01** for hello first web server</span></span>
* <span data-ttu-id="5dd04-160">**azos-use vm web02** Olá segundo servidor de web</span><span class="sxs-lookup"><span data-stu-id="5dd04-160">**azos-use-vm-web02** for hello second web server</span></span>
* <span data-ttu-id="5dd04-161">**azos-use vm app01** Olá primeiro servidor de aplicativos</span><span class="sxs-lookup"><span data-stu-id="5dd04-161">**azos-use-vm-app01** for hello first application server</span></span>
* <span data-ttu-id="5dd04-162">**azos-use vm app02** Olá segundo servidor de aplicativos</span><span class="sxs-lookup"><span data-stu-id="5dd04-162">**azos-use-vm-app02** for hello second application server</span></span>
* <span data-ttu-id="5dd04-163">**azos-use vm sql01** para Olá primeiro do SQL server em cluster Olá</span><span class="sxs-lookup"><span data-stu-id="5dd04-163">**azos-use-vm-sql01** for hello first SQL Server server in hello cluster</span></span>
* <span data-ttu-id="5dd04-164">**azos-use vm sql02** para Olá segundo do SQL server em cluster Olá</span><span class="sxs-lookup"><span data-stu-id="5dd04-164">**azos-use-vm-sql02** for hello second SQL Server server in hello cluster</span></span>
* <span data-ttu-id="5dd04-165">**use azos-dc01 vm** Olá primeiro controlador de domínio</span><span class="sxs-lookup"><span data-stu-id="5dd04-165">**azos-use-vm-dc01** for hello first domain controller</span></span>
* <span data-ttu-id="5dd04-166">**azos-uso-vm-dc02** Olá segundo controlador de domínio</span><span class="sxs-lookup"><span data-stu-id="5dd04-166">**azos-use-vm-dc02** for hello second domain controller</span></span>

<span data-ttu-id="5dd04-167">Aqui está a configuração resultante hello.</span><span class="sxs-lookup"><span data-stu-id="5dd04-167">Here is hello resulting configuration.</span></span>

![Infraestrutura final do aplicativo implantada no Azure](./media/infrastructure-example/example-config.png)

<span data-ttu-id="5dd04-169">Essa configuração inclui:</span><span class="sxs-lookup"><span data-stu-id="5dd04-169">This configuration incorporates:</span></span>

* <span data-ttu-id="5dd04-170">Uma rede virtual somente em nuvem com duas sub-redes (front-end e back-end)</span><span class="sxs-lookup"><span data-stu-id="5dd04-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="5dd04-171">Azure Managed Disks com discos Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="5dd04-171">Azure Managed Disks with both Standard and Premium disks</span></span>
* <span data-ttu-id="5dd04-172">Quatro conjuntos de disponibilidade, um para cada camada de armazenamento online Olá</span><span class="sxs-lookup"><span data-stu-id="5dd04-172">Four availability sets, one for each tier of hello on-line store</span></span>
* <span data-ttu-id="5dd04-173">máquinas virtuais de saudação para as camadas de saudação quatro</span><span class="sxs-lookup"><span data-stu-id="5dd04-173">hello virtual machines for hello four tiers</span></span>
* <span data-ttu-id="5dd04-174">Um conjunto de balanceamento de carga externo para o tráfego da web baseado em HTTPS de servidores de web hello Internet toohello</span><span class="sxs-lookup"><span data-stu-id="5dd04-174">An external load balanced set for HTTPS-based web traffic from hello Internet toohello web servers</span></span>
* <span data-ttu-id="5dd04-175">Uma carga interna com balanceamento de conjunto para o tráfego da web não criptografada de servidores de aplicativos Olá web servidores toohello</span><span class="sxs-lookup"><span data-stu-id="5dd04-175">An internal load balanced set for unencrypted web traffic from hello web servers toohello application servers</span></span>
* <span data-ttu-id="5dd04-176">Um único grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="5dd04-176">A single resource group</span></span>