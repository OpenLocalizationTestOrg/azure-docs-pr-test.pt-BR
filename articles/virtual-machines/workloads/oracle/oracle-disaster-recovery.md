---
title: "aaaOverview de um cenário de recuperação de desastres do Oracle em seu ambiente do Azure | Microsoft Docs"
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
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="5dcd2-103">Recuperação de desastre para um banco de dados Oracle Database 12c em um ambiente do Azure</span><span class="sxs-lookup"><span data-stu-id="5dcd2-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="5dcd2-104">Suposições</span><span class="sxs-lookup"><span data-stu-id="5dcd2-104">Assumptions</span></span>

- <span data-ttu-id="5dcd2-105">Você compreende o design dos ambientes do Oracle Data Guard e do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="5dcd2-106">Metas</span><span class="sxs-lookup"><span data-stu-id="5dcd2-106">Goals</span></span>
- <span data-ttu-id="5dcd2-107">Design topologia hello e configuração que atendem aos seus requisitos de recuperação de desastres.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-107">Design hello topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="5dcd2-108">Cenário 1: Sites primário e de recuperação de desastre no Azure</span><span class="sxs-lookup"><span data-stu-id="5dcd2-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="5dcd2-109">Um cliente tem um Oracle de banco de dados conjunto de backup no site primário hello.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-109">A customer has an Oracle database set up on hello primary site.</span></span> <span data-ttu-id="5dcd2-110">Um site de recuperação de desastre está em uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-110">A DR site is in a different region.</span></span> <span data-ttu-id="5dcd2-111">Prezado cliente usa o Oracle Data Guard para recuperação rápida entre esses sites.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-111">hello customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="5dcd2-112">site primário Olá também tem um banco de dados secundário para emissão de relatórios e outros usos.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-112">hello primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="5dcd2-113">Topologia</span><span class="sxs-lookup"><span data-stu-id="5dcd2-113">Topology</span></span>

<span data-ttu-id="5dcd2-114">Aqui está um resumo da saudação configuração do Azure:</span><span class="sxs-lookup"><span data-stu-id="5dcd2-114">Here is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="5dcd2-115">Dois sites (um site primário e um site de recuperação de desastre)</span><span class="sxs-lookup"><span data-stu-id="5dcd2-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="5dcd2-116">Duas redes virtuais</span><span class="sxs-lookup"><span data-stu-id="5dcd2-116">Two virtual networks</span></span>
- <span data-ttu-id="5dcd2-117">Dois bancos de dados Oracle com Data Guard (primário e em espera)</span><span class="sxs-lookup"><span data-stu-id="5dcd2-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="5dcd2-118">Dois bancos de dados Oracle com Golden Gate ou Data Guard (somente site primário)</span><span class="sxs-lookup"><span data-stu-id="5dcd2-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="5dcd2-119">Dois serviços de aplicativo, um primário e no site de saudação DR</span><span class="sxs-lookup"><span data-stu-id="5dcd2-119">Two application services, one primary and one on hello DR site</span></span>
- <span data-ttu-id="5dcd2-120">Um *conjunto de disponibilidade,* que é usada para o serviço de banco de dados e aplicativo no site primário Olá</span><span class="sxs-lookup"><span data-stu-id="5dcd2-120">An *availability set,* which is used for database and application service on hello primary site</span></span>
- <span data-ttu-id="5dcd2-121">Um jumpbox em cada site, o que restringe o acesso a rede privada toohello e só permite entrar por um administrador</span><span class="sxs-lookup"><span data-stu-id="5dcd2-121">One jumpbox on each site, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="5dcd2-122">Um jumpbox, um serviço de aplicativo, um banco de dados e um gateway de VPN em sub-redes separadas</span><span class="sxs-lookup"><span data-stu-id="5dcd2-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="5dcd2-123">O NSG imposto em sub-redes de aplicativo e do banco de dados</span><span class="sxs-lookup"><span data-stu-id="5dcd2-123">NSG enforced on application and database subnets</span></span>

![Captura de tela da página de topologia Olá DR](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="5dcd2-125">Cenário 2: Site primário local e site de recuperação de desastre no Azure</span><span class="sxs-lookup"><span data-stu-id="5dcd2-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="5dcd2-126">Um cliente tem uma configuração de banco de dados Oracle local (site primário).</span><span class="sxs-lookup"><span data-stu-id="5dcd2-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="5dcd2-127">Um site de recuperação de desastre reside no Azure.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-127">A DR site is on Azure.</span></span> <span data-ttu-id="5dcd2-128">O Oracle Data Guard é usado para recuperação rápida entre esses sites.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="5dcd2-129">site primário Olá também tem um banco de dados secundário para emissão de relatórios e outros usos.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-129">hello primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="5dcd2-130">Há duas abordagens para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a><span data-ttu-id="5dcd2-131">Abordagem 1: A conexão direta entre local e o Azure, a necessidade de abrir as portas TCP no firewall Olá</span><span class="sxs-lookup"><span data-stu-id="5dcd2-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on hello firewall</span></span> 

<span data-ttu-id="5dcd2-132">Não é recomendável conexões diretas porque eles expõem Olá toohello de portas TCP fora do mundo.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-132">We don't recommend direct connections because they expose hello TCP ports toohello outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="5dcd2-133">Topologia</span><span class="sxs-lookup"><span data-stu-id="5dcd2-133">Topology</span></span>

<span data-ttu-id="5dcd2-134">A seguir está um resumo de hello a instalação do Azure:</span><span class="sxs-lookup"><span data-stu-id="5dcd2-134">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="5dcd2-135">Um site de recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="5dcd2-135">One DR site</span></span> 
- <span data-ttu-id="5dcd2-136">Uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="5dcd2-136">One virtual network</span></span>
- <span data-ttu-id="5dcd2-137">Um banco de dados Oracle com Data Guard (ativo)</span><span class="sxs-lookup"><span data-stu-id="5dcd2-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="5dcd2-138">Serviço de um aplicativo no site de saudação DR</span><span class="sxs-lookup"><span data-stu-id="5dcd2-138">One application service on hello DR site</span></span>
- <span data-ttu-id="5dcd2-139">Um jumpbox, que restringe o acesso a rede privada toohello e só permite entrar por um administrador</span><span class="sxs-lookup"><span data-stu-id="5dcd2-139">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="5dcd2-140">Um jumpbox, um serviço de aplicativo, um banco de dados e um gateway de VPN em sub-redes separadas</span><span class="sxs-lookup"><span data-stu-id="5dcd2-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="5dcd2-141">O NSG imposto em sub-redes de aplicativo e do banco de dados</span><span class="sxs-lookup"><span data-stu-id="5dcd2-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="5dcd2-142">A porta TCP 1521 (ou uma porta definidos pelo usuário) de entrada de um tooallow de regra de política/NSG</span><span class="sxs-lookup"><span data-stu-id="5dcd2-142">An NSG policy/rule tooallow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="5dcd2-143">Uma NSG/regra de política toorestrict somente Olá IP endereço/endereços locais (banco de dados ou aplicativo) tooaccess Olá rede virtual</span><span class="sxs-lookup"><span data-stu-id="5dcd2-143">An NSG policy/rule toorestrict only hello IP address/addresses on-premises (DB or application) tooaccess hello virtual network</span></span>

![Captura de tela da página de topologia Olá DR](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="5dcd2-145">Método 2: VPN Site a site</span><span class="sxs-lookup"><span data-stu-id="5dcd2-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="5dcd2-146">A VPN site a site é uma abordagem melhor.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="5dcd2-147">Para saber mais sobre como configurar uma VPN, veja [Criar uma rede virtual com uma conexão VPN Site a Site usando a CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="5dcd2-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="5dcd2-148">Topologia</span><span class="sxs-lookup"><span data-stu-id="5dcd2-148">Topology</span></span>

<span data-ttu-id="5dcd2-149">A seguir está um resumo de hello a instalação do Azure:</span><span class="sxs-lookup"><span data-stu-id="5dcd2-149">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="5dcd2-150">Um site de recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="5dcd2-150">One DR site</span></span> 
- <span data-ttu-id="5dcd2-151">Uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="5dcd2-151">One virtual network</span></span> 
- <span data-ttu-id="5dcd2-152">Um banco de dados Oracle com Data Guard (ativo)</span><span class="sxs-lookup"><span data-stu-id="5dcd2-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="5dcd2-153">Serviço de um aplicativo no site de saudação DR</span><span class="sxs-lookup"><span data-stu-id="5dcd2-153">One application service on hello DR site</span></span>
- <span data-ttu-id="5dcd2-154">Um jumpbox, que restringe o acesso a rede privada toohello e só permite entrar por um administrador</span><span class="sxs-lookup"><span data-stu-id="5dcd2-154">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="5dcd2-155">Um jumpbox, um serviço de aplicativo, um banco de dados e um gateway de VPN ficam em sub-redes separadas</span><span class="sxs-lookup"><span data-stu-id="5dcd2-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="5dcd2-156">O NSG imposto em sub-redes de aplicativo e do banco de dados</span><span class="sxs-lookup"><span data-stu-id="5dcd2-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="5dcd2-157">Conexão VPN site a site entre sites locais e o Azure</span><span class="sxs-lookup"><span data-stu-id="5dcd2-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![Captura de tela da página de topologia Olá DR](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="5dcd2-159">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="5dcd2-159">Additional reading</span></span>

- [<span data-ttu-id="5dcd2-160">Projetar e implementar um banco de dados Oracle no Azure</span><span class="sxs-lookup"><span data-stu-id="5dcd2-160">Design and implement an Oracle database on Azure</span></span>](oracle-design.md)
- [<span data-ttu-id="5dcd2-161">Configurar o Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="5dcd2-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="5dcd2-162">Configurar o Oracle Golden Gate</span><span class="sxs-lookup"><span data-stu-id="5dcd2-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="5dcd2-163">Backup e recuperação do Oracle</span><span class="sxs-lookup"><span data-stu-id="5dcd2-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="5dcd2-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5dcd2-164">Next steps</span></span>

- [<span data-ttu-id="5dcd2-165">Tutorial: criar VMs altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="5dcd2-165">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="5dcd2-166">Explorar exemplos da CLI do Azure de implantação de VM</span><span class="sxs-lookup"><span data-stu-id="5dcd2-166">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
