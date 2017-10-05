---
title: "Visão geral de um cenário de recuperação de desastre do Oracle no ambiente do Azure | Microsoft Docs"
description: "Um cenário de recuperação de desastre do banco de dados Oracle Database 12c no ambiente do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: f17ebb2b74cd7ad872f88483ed7cdb4f239ee069
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="fec97-103">Recuperação de desastre para um banco de dados Oracle Database 12c em um ambiente do Azure</span><span class="sxs-lookup"><span data-stu-id="fec97-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="fec97-104">Suposições</span><span class="sxs-lookup"><span data-stu-id="fec97-104">Assumptions</span></span>

- <span data-ttu-id="fec97-105">Você compreende o design dos ambientes do Oracle Data Guard e do Azure.</span><span class="sxs-lookup"><span data-stu-id="fec97-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="fec97-106">Metas</span><span class="sxs-lookup"><span data-stu-id="fec97-106">Goals</span></span>
- <span data-ttu-id="fec97-107">Projetar a topologia e a configuração para atender aos seus requisitos de recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="fec97-107">Design the topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="fec97-108">Cenário 1: Sites primário e de recuperação de desastre no Azure</span><span class="sxs-lookup"><span data-stu-id="fec97-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="fec97-109">Um cliente tem uma configuração de banco de dados Oracle no site primário.</span><span class="sxs-lookup"><span data-stu-id="fec97-109">A customer has an Oracle database set up on the primary site.</span></span> <span data-ttu-id="fec97-110">Um site de recuperação de desastre está em uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="fec97-110">A DR site is in a different region.</span></span> <span data-ttu-id="fec97-111">O cliente usa o Oracle Data Guard para recuperação rápida entre esses sites.</span><span class="sxs-lookup"><span data-stu-id="fec97-111">The customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="fec97-112">O site primário também tem um banco de dados secundário para relatórios e outros usos.</span><span class="sxs-lookup"><span data-stu-id="fec97-112">The primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="fec97-113">Topologia</span><span class="sxs-lookup"><span data-stu-id="fec97-113">Topology</span></span>

<span data-ttu-id="fec97-114">Veja aqui um resumo da configuração do Azure:</span><span class="sxs-lookup"><span data-stu-id="fec97-114">Here is a summary of the Azure setup:</span></span>

- <span data-ttu-id="fec97-115">Dois sites (um site primário e um site de recuperação de desastre)</span><span class="sxs-lookup"><span data-stu-id="fec97-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="fec97-116">Duas redes virtuais</span><span class="sxs-lookup"><span data-stu-id="fec97-116">Two virtual networks</span></span>
- <span data-ttu-id="fec97-117">Dois bancos de dados Oracle com Data Guard (primário e em espera)</span><span class="sxs-lookup"><span data-stu-id="fec97-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="fec97-118">Dois bancos de dados Oracle com Golden Gate ou Data Guard (somente site primário)</span><span class="sxs-lookup"><span data-stu-id="fec97-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="fec97-119">Dois serviços de aplicativos, um principal e um site de recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="fec97-119">Two application services, one primary and one on the DR site</span></span>
- <span data-ttu-id="fec97-120">Um *conjunto de disponibilidade* usado para o banco de dados e para o serviço de aplicativo no site primário</span><span class="sxs-lookup"><span data-stu-id="fec97-120">An *availability set,* which is used for database and application service on the primary site</span></span>
- <span data-ttu-id="fec97-121">Um jumpbox em cada site, que restringe o acesso à rede privada, permitindo que somente o administrador se conecte</span><span class="sxs-lookup"><span data-stu-id="fec97-121">One jumpbox on each site, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="fec97-122">Um jumpbox, um serviço de aplicativo, um banco de dados e um gateway de VPN em sub-redes separadas</span><span class="sxs-lookup"><span data-stu-id="fec97-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="fec97-123">O NSG imposto em sub-redes de aplicativo e do banco de dados</span><span class="sxs-lookup"><span data-stu-id="fec97-123">NSG enforced on application and database subnets</span></span>

![Captura de tela da página de topologia de recuperação de desastre](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="fec97-125">Cenário 2: Site primário local e site de recuperação de desastre no Azure</span><span class="sxs-lookup"><span data-stu-id="fec97-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="fec97-126">Um cliente tem uma configuração de banco de dados Oracle local (site primário).</span><span class="sxs-lookup"><span data-stu-id="fec97-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="fec97-127">Um site de recuperação de desastre reside no Azure.</span><span class="sxs-lookup"><span data-stu-id="fec97-127">A DR site is on Azure.</span></span> <span data-ttu-id="fec97-128">O Oracle Data Guard é usado para recuperação rápida entre esses sites.</span><span class="sxs-lookup"><span data-stu-id="fec97-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="fec97-129">O site primário também tem um banco de dados secundário para relatórios e outros usos.</span><span class="sxs-lookup"><span data-stu-id="fec97-129">The primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="fec97-130">Há duas abordagens para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="fec97-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-the-firewall"></a><span data-ttu-id="fec97-131">Abordagem 1: Conexões diretas entre o local e o Azure, é necessário abrir as portas TCP no firewall</span><span class="sxs-lookup"><span data-stu-id="fec97-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on the firewall</span></span> 

<span data-ttu-id="fec97-132">Nós não recomendamos conexões diretas, pois expõem as portas TCP para o mundo exterior.</span><span class="sxs-lookup"><span data-stu-id="fec97-132">We don't recommend direct connections because they expose the TCP ports to the outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="fec97-133">Topologia</span><span class="sxs-lookup"><span data-stu-id="fec97-133">Topology</span></span>

<span data-ttu-id="fec97-134">Veja aqui um resumo da configuração do Azure:</span><span class="sxs-lookup"><span data-stu-id="fec97-134">Following is a summary of the Azure setup:</span></span>

- <span data-ttu-id="fec97-135">Um site de recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="fec97-135">One DR site</span></span> 
- <span data-ttu-id="fec97-136">Uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="fec97-136">One virtual network</span></span>
- <span data-ttu-id="fec97-137">Um banco de dados Oracle com Data Guard (ativo)</span><span class="sxs-lookup"><span data-stu-id="fec97-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="fec97-138">Um serviço de aplicativo no site de recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="fec97-138">One application service on the DR site</span></span>
- <span data-ttu-id="fec97-139">Um Jumpbox, que restringe o acesso à rede privada, permitindo que somente o administrador se conecte</span><span class="sxs-lookup"><span data-stu-id="fec97-139">One jumpbox, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="fec97-140">Um jumpbox, um serviço de aplicativo, um banco de dados e um gateway de VPN em sub-redes separadas</span><span class="sxs-lookup"><span data-stu-id="fec97-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="fec97-141">O NSG imposto em sub-redes de aplicativo e do banco de dados</span><span class="sxs-lookup"><span data-stu-id="fec97-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="fec97-142">Uma política/regra de NSG para permitir entrada na porta TCP 1521 (ou uma porta definida pelo usuário)</span><span class="sxs-lookup"><span data-stu-id="fec97-142">An NSG policy/rule to allow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="fec97-143">Adicione a política/regra de NSG para restringir somente endereços IP/locais (BD ou aplicativo) para acessarem a rede virtual</span><span class="sxs-lookup"><span data-stu-id="fec97-143">An NSG policy/rule to restrict only the IP address/addresses on-premises (DB or application) to access the virtual network</span></span>

![Captura de tela da página de topologia de recuperação de desastre](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="fec97-145">Método 2: VPN Site a site</span><span class="sxs-lookup"><span data-stu-id="fec97-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="fec97-146">A VPN site a site é uma abordagem melhor.</span><span class="sxs-lookup"><span data-stu-id="fec97-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="fec97-147">Para saber mais sobre como configurar uma VPN, veja [Criar uma rede virtual com uma conexão VPN Site a Site usando a CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="fec97-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="fec97-148">Topologia</span><span class="sxs-lookup"><span data-stu-id="fec97-148">Topology</span></span>

<span data-ttu-id="fec97-149">Veja aqui um resumo da configuração do Azure:</span><span class="sxs-lookup"><span data-stu-id="fec97-149">Following is a summary of the Azure setup:</span></span>

- <span data-ttu-id="fec97-150">Um site de recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="fec97-150">One DR site</span></span> 
- <span data-ttu-id="fec97-151">Uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="fec97-151">One virtual network</span></span> 
- <span data-ttu-id="fec97-152">Um banco de dados Oracle com Data Guard (ativo)</span><span class="sxs-lookup"><span data-stu-id="fec97-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="fec97-153">Um serviço de aplicativo no site de recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="fec97-153">One application service on the DR site</span></span>
- <span data-ttu-id="fec97-154">Um Jumpbox, que restringe o acesso à rede privada, permitindo que somente o administrador se conecte</span><span class="sxs-lookup"><span data-stu-id="fec97-154">One jumpbox, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="fec97-155">Um jumpbox, um serviço de aplicativo, um banco de dados e um gateway de VPN ficam em sub-redes separadas</span><span class="sxs-lookup"><span data-stu-id="fec97-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="fec97-156">O NSG imposto em sub-redes de aplicativo e do banco de dados</span><span class="sxs-lookup"><span data-stu-id="fec97-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="fec97-157">Conexão VPN site a site entre sites locais e o Azure</span><span class="sxs-lookup"><span data-stu-id="fec97-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![Captura de tela da página de topologia de recuperação de desastre](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="fec97-159">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="fec97-159">Additional reading</span></span>

- [<span data-ttu-id="fec97-160">Projetar e implementar um banco de dados Oracle no Azure</span><span class="sxs-lookup"><span data-stu-id="fec97-160">Design and implement an Oracle database on Azure</span></span>](oracle-design.md)
- [<span data-ttu-id="fec97-161">Configurar o Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="fec97-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="fec97-162">Configurar o Oracle Golden Gate</span><span class="sxs-lookup"><span data-stu-id="fec97-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="fec97-163">Backup e recuperação do Oracle</span><span class="sxs-lookup"><span data-stu-id="fec97-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="fec97-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fec97-164">Next steps</span></span>

- [<span data-ttu-id="fec97-165">Tutorial: criar VMs altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="fec97-165">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="fec97-166">Explorar exemplos da CLI do Azure de implantação de VM</span><span class="sxs-lookup"><span data-stu-id="fec97-166">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
