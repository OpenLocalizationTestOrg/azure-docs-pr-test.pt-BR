---
title: arquitetura de conectividade de banco de dados SQL do aaaAzure | Microsoft Docs
description: Este documento explica hello Azure SQLDB conectividade arquitetura de dentro do Azure ou de fora do Azure.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="6079f-103">Arquitetura de Conectividade do Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="6079f-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="6079f-104">Este artigo explica a arquitetura de conectividade de banco de dados do Azure SQL hello e explica como diferentes componentes de saudação funcionam toodirect instância de tooyour de tráfego do banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6079f-104">This article explains hello Azure SQL Database connectivity architecture and explains how hello different components function toodirect traffic tooyour instance of Azure SQL Database.</span></span> <span data-ttu-id="6079f-105">Esses componentes de conectividade de banco de dados do Azure SQL função toohello de tráfego de rede toodirect banco de dados do Azure com clientes se conectam de dentro do Azure e clientes se conectam de fora do Azure.</span><span class="sxs-lookup"><span data-stu-id="6079f-105">These Azure SQL Database connectivity components function toodirect network traffic toohello Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="6079f-106">Este artigo também fornece toochange de exemplos de script, como ocorre a conectividade e considerações de saudação relacionadas a configurações de conectividade do toochanging saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="6079f-106">This article also provides script samples toochange how connectivity occurs, and hello considerations related toochanging hello default connectivity settings.</span></span> <span data-ttu-id="6079f-107">Se houver alguma dúvida depois de ler este artigo, entre em contato com o Dhruv em dmalik@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="6079f-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="6079f-108">Arquitetura de conectividade</span><span class="sxs-lookup"><span data-stu-id="6079f-108">Connectivity architecture</span></span>

<span data-ttu-id="6079f-109">Olá diagrama a seguir fornece uma visão geral de saudação arquitetura de conectividade de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="6079f-109">hello following diagram provides a high-level overview of hello Azure SQL Database connectivity architecture.</span></span> 

![visão geral da arquitetura](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="6079f-111">Olá etapas a seguir descrevem como uma conexão é estabelecida tooan banco de dados de SQL do Azure através de hello Azure SQL Database software balanceador de carga (SLB) e o gateway de banco de dados SQL do hello.</span><span class="sxs-lookup"><span data-stu-id="6079f-111">hello following steps describe how a connection is established tooan Azure SQL database through hello Azure SQL Database software load-balancer (SLB) and hello Azure SQL Database gateway.</span></span>

- <span data-ttu-id="6079f-112">Clientes no Azure ou fora do Azure se conectar toohello SLB, que tem um endereço IP público e escuta na porta 1433.</span><span class="sxs-lookup"><span data-stu-id="6079f-112">Clients within Azure or outside of Azure connect toohello SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="6079f-113">Olá SLB direciona o gateway de banco de dados SQL do tráfego toohello.</span><span class="sxs-lookup"><span data-stu-id="6079f-113">hello SLB directs traffic toohello Azure SQL Database gateway.</span></span>
- <span data-ttu-id="6079f-114">gateway Olá redireciona Olá tráfego toohello proxy corretas middleware.</span><span class="sxs-lookup"><span data-stu-id="6079f-114">hello gateway redirects hello traffic toohello correct proxy middleware.</span></span>
- <span data-ttu-id="6079f-115">Olá proxy middleware redireciona Olá tráfego toohello SQL Azure banco de dados apropriado.</span><span class="sxs-lookup"><span data-stu-id="6079f-115">hello proxy middleware redirects hello traffic toohello appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6079f-116">Cada um desses componentes tem distribuído negação de proteção de serviço (DDoS) interna em rede hello e camada de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6079f-116">Each of these components has distributed denial of service (DDoS) protection built-in at hello network and hello app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="6079f-117">Conectividade de dentro do Azure</span><span class="sxs-lookup"><span data-stu-id="6079f-117">Connectivity from within Azure</span></span>

<span data-ttu-id="6079f-118">Se você estiver se conectando de dentro do Azure, as conexões têm uma política de conexão de **Redirecionamento** por padrão.</span><span class="sxs-lookup"><span data-stu-id="6079f-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="6079f-119">Uma política de **redirecionar** significa que conexões após a sessão TCP Olá estabelecida toohello banco de dados do SQL Azure, sessão de saudação do cliente é então redirecionado toohello proxy middleware com IP virtual de destino do toohello uma alteração de que de hello Azure SQL Database gateway toothat de saudação proxy middleware.</span><span class="sxs-lookup"><span data-stu-id="6079f-119">A policy of **Redirect** means that connections after hello TCP session is established toohello Azure SQL database, hello client session is then redirected toohello proxy middleware with a change toohello destination virtual IP from that of hello Azure SQL Database gateway toothat of hello proxy middleware.</span></span> <span data-ttu-id="6079f-120">Depois disso, todos os pacotes subsequentes fluam diretamente por meio do middleware de proxy hello, ignorando o gateway de banco de dados do Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="6079f-120">Thereafter, all subsequent packets flow directly via hello proxy middleware, bypassing hello Azure SQL Database gateway.</span></span> <span data-ttu-id="6079f-121">Olá diagrama a seguir ilustra esse fluxo de tráfego.</span><span class="sxs-lookup"><span data-stu-id="6079f-121">hello following diagram illustrates this traffic flow.</span></span>

![visão geral da arquitetura](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="6079f-123">Conectividade de fora do Azure</span><span class="sxs-lookup"><span data-stu-id="6079f-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="6079f-124">Se você estiver se conectando de fora do Azure, as conexões têm uma política de conexão de **Proxy** por padrão.</span><span class="sxs-lookup"><span data-stu-id="6079f-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="6079f-125">Uma política de **Proxy** significa que a sessão TCP de saudação é estabelecido por meio do gateway de banco de dados do Azure SQL hello e todos os pacotes subsequentes fluam através de Olá gateway.</span><span class="sxs-lookup"><span data-stu-id="6079f-125">A policy of **Proxy** means that hello TCP session is established via hello Azure SQL Database gateway and all subsequent packets flow via hello gateway.</span></span> <span data-ttu-id="6079f-126">Olá diagrama a seguir ilustra esse fluxo de tráfego.</span><span class="sxs-lookup"><span data-stu-id="6079f-126">hello following diagram illustrates this traffic flow.</span></span>

![visão geral da arquitetura](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="6079f-128">Endereços IP de gateway do Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="6079f-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="6079f-129">tooconnect tooan SQL Azure banco de dados de recursos locais, você precisa de tooallow rede de saída tráfego toohello banco de dados de SQL Azure gateway para sua região do Azure.</span><span class="sxs-lookup"><span data-stu-id="6079f-129">tooconnect tooan Azure SQL database from on-premises resources, you need tooallow outbound network traffic toohello Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="6079f-130">As conexões vão somente por meio do gateway de saudação ao conectar-se no modo de Proxy, que é o padrão de saudação ao conectar-se de recursos locais.</span><span class="sxs-lookup"><span data-stu-id="6079f-130">Your connections only go via hello gateway when connecting in Proxy mode, which is hello default when connecting from on-premises resources.</span></span>

<span data-ttu-id="6079f-131">Olá a tabela a seguir lista Olá IPs primários e secundários do gateway de banco de dados do Azure SQL Olá para todas as regiões de dados.</span><span class="sxs-lookup"><span data-stu-id="6079f-131">hello following table lists hello primary and secondary IPs of hello Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="6079f-132">Para algumas regiões, há dois endereços IP.</span><span class="sxs-lookup"><span data-stu-id="6079f-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="6079f-133">Essas regiões, endereço IP primário Olá é Olá atual endereço IP do gateway de saudação e Olá segundo endereço IP é um endereço IP de failover.</span><span class="sxs-lookup"><span data-stu-id="6079f-133">In these regions, hello primary IP address is hello current IP address of hello gateway and hello second IP address is a failover IP address.</span></span> <span data-ttu-id="6079f-134">endereço de failover de saudação é Olá endereço toowhich podemos pode mover seu servidor tookeep Olá disponibilidade do serviço alta.</span><span class="sxs-lookup"><span data-stu-id="6079f-134">hello failover address is hello address toowhich we might move your server tookeep hello service availability high.</span></span> <span data-ttu-id="6079f-135">Para essas regiões, é recomendável permitir saída tooboth endereços IP hello.</span><span class="sxs-lookup"><span data-stu-id="6079f-135">For these regions, we recommend that you allow outbound tooboth hello IP addresses.</span></span> <span data-ttu-id="6079f-136">endereço IP da segunda Olá pertence pela Microsoft e não escutará todos os serviços até que ele seja ativado por conexões de tooaccept do banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="6079f-136">hello second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database tooaccept connections.</span></span>

| <span data-ttu-id="6079f-137">Nome da Região</span><span class="sxs-lookup"><span data-stu-id="6079f-137">Region Name</span></span> | <span data-ttu-id="6079f-138">Endereço IP primário</span><span class="sxs-lookup"><span data-stu-id="6079f-138">Primary IP address</span></span> | <span data-ttu-id="6079f-139">Endereço IP secundário</span><span class="sxs-lookup"><span data-stu-id="6079f-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="6079f-140">Leste da Austrália</span><span class="sxs-lookup"><span data-stu-id="6079f-140">Australia East</span></span> | <span data-ttu-id="6079f-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="6079f-141">191.238.66.109</span></span> | <span data-ttu-id="6079f-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="6079f-142">13.75.149.87</span></span> |
| <span data-ttu-id="6079f-143">Sudeste da Austrália</span><span class="sxs-lookup"><span data-stu-id="6079f-143">Australia South East</span></span> | <span data-ttu-id="6079f-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="6079f-144">191.239.192.109</span></span> | <span data-ttu-id="6079f-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="6079f-145">13.73.109.251</span></span> |
| <span data-ttu-id="6079f-146">Sul do Brasil</span><span class="sxs-lookup"><span data-stu-id="6079f-146">Brazil South</span></span> | <span data-ttu-id="6079f-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="6079f-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="6079f-148">Canadá Central</span><span class="sxs-lookup"><span data-stu-id="6079f-148">Canada Central</span></span> | <span data-ttu-id="6079f-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="6079f-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="6079f-150">Leste do Canadá</span><span class="sxs-lookup"><span data-stu-id="6079f-150">Canada East</span></span> | <span data-ttu-id="6079f-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="6079f-151">40.86.226.166</span></span> | |
| <span data-ttu-id="6079f-152">Centro dos EUA</span><span class="sxs-lookup"><span data-stu-id="6079f-152">Central US</span></span> | <span data-ttu-id="6079f-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="6079f-153">23.99.160.139</span></span> | <span data-ttu-id="6079f-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="6079f-154">13.67.215.62</span></span> |
| <span data-ttu-id="6079f-155">Ásia Oriental</span><span class="sxs-lookup"><span data-stu-id="6079f-155">East Asia</span></span> | <span data-ttu-id="6079f-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="6079f-156">191.234.2.139</span></span> | <span data-ttu-id="6079f-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="6079f-157">52.175.33.150</span></span> |
| <span data-ttu-id="6079f-158">Leste dos EUA 1</span><span class="sxs-lookup"><span data-stu-id="6079f-158">East US 1</span></span> | <span data-ttu-id="6079f-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="6079f-159">191.238.6.43</span></span> | <span data-ttu-id="6079f-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="6079f-160">40.121.158.30</span></span> |
| <span data-ttu-id="6079f-161">Leste dos EUA 2</span><span class="sxs-lookup"><span data-stu-id="6079f-161">East US 2</span></span> | <span data-ttu-id="6079f-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="6079f-162">191.239.224.107</span></span> | <span data-ttu-id="6079f-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="6079f-163">40.79.84.180</span></span> |
| <span data-ttu-id="6079f-164">Centro da Índia</span><span class="sxs-lookup"><span data-stu-id="6079f-164">India Central</span></span> | <span data-ttu-id="6079f-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="6079f-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="6079f-166">Sul da Índia</span><span class="sxs-lookup"><span data-stu-id="6079f-166">India South</span></span> | <span data-ttu-id="6079f-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="6079f-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="6079f-168">Oeste da Índia</span><span class="sxs-lookup"><span data-stu-id="6079f-168">India West</span></span> | <span data-ttu-id="6079f-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="6079f-169">104.211.160.80</span></span> | |
| <span data-ttu-id="6079f-170">Leste do Japão</span><span class="sxs-lookup"><span data-stu-id="6079f-170">Japan East</span></span> | <span data-ttu-id="6079f-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="6079f-171">191.237.240.43</span></span> | <span data-ttu-id="6079f-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="6079f-172">13.78.61.196</span></span> |
| <span data-ttu-id="6079f-173">Oeste do Japão</span><span class="sxs-lookup"><span data-stu-id="6079f-173">Japan West</span></span> | <span data-ttu-id="6079f-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="6079f-174">191.238.68.11</span></span> | <span data-ttu-id="6079f-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="6079f-175">104.214.148.156</span></span> |
| <span data-ttu-id="6079f-176">Coreia Central</span><span class="sxs-lookup"><span data-stu-id="6079f-176">Korea Central</span></span> | <span data-ttu-id="6079f-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="6079f-177">52.231.32.42</span></span> | |
| <span data-ttu-id="6079f-178">Sul da Coreia</span><span class="sxs-lookup"><span data-stu-id="6079f-178">Korea South</span></span> | <span data-ttu-id="6079f-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="6079f-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="6079f-180">Centro-Norte dos EUA</span><span class="sxs-lookup"><span data-stu-id="6079f-180">North Central US</span></span> | <span data-ttu-id="6079f-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="6079f-181">23.98.55.75</span></span> | <span data-ttu-id="6079f-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="6079f-182">23.96.178.199</span></span> |
| <span data-ttu-id="6079f-183">Norte da Europa</span><span class="sxs-lookup"><span data-stu-id="6079f-183">North Europe</span></span> | <span data-ttu-id="6079f-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="6079f-184">191.235.193.75</span></span> | <span data-ttu-id="6079f-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="6079f-185">40.113.93.91</span></span> |
| <span data-ttu-id="6079f-186">Centro-Sul dos Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="6079f-186">South Central US</span></span> | <span data-ttu-id="6079f-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="6079f-187">23.98.162.75</span></span> | <span data-ttu-id="6079f-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="6079f-188">13.66.62.124</span></span> |
| <span data-ttu-id="6079f-189">Sudeste da Ásia</span><span class="sxs-lookup"><span data-stu-id="6079f-189">South East Asia</span></span> | <span data-ttu-id="6079f-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="6079f-190">23.100.117.95</span></span> | <span data-ttu-id="6079f-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="6079f-191">104.43.15.0</span></span> |
| <span data-ttu-id="6079f-192">Norte do Reino Unido</span><span class="sxs-lookup"><span data-stu-id="6079f-192">UK North</span></span> | <span data-ttu-id="6079f-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="6079f-193">13.87.97.210</span></span> | |
| <span data-ttu-id="6079f-194">Sul do Reino Unido 1</span><span class="sxs-lookup"><span data-stu-id="6079f-194">UK South 1</span></span> | <span data-ttu-id="6079f-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="6079f-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="6079f-196">Sul do Reino Unido 2</span><span class="sxs-lookup"><span data-stu-id="6079f-196">UK South 2</span></span> | <span data-ttu-id="6079f-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="6079f-197">13.87.34.7</span></span> | |
| <span data-ttu-id="6079f-198">Oeste do Reino Unido</span><span class="sxs-lookup"><span data-stu-id="6079f-198">UK West</span></span> | <span data-ttu-id="6079f-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="6079f-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="6079f-200">Centro-Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="6079f-200">West Central US</span></span> | <span data-ttu-id="6079f-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="6079f-201">13.78.145.25</span></span> | |
| <span data-ttu-id="6079f-202">Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="6079f-202">West Europe</span></span> | <span data-ttu-id="6079f-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="6079f-203">191.237.232.75</span></span> | <span data-ttu-id="6079f-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="6079f-204">40.68.37.158</span></span> |
| <span data-ttu-id="6079f-205">Oeste dos EUA 1</span><span class="sxs-lookup"><span data-stu-id="6079f-205">West US 1</span></span> | <span data-ttu-id="6079f-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="6079f-206">23.99.34.75</span></span> | <span data-ttu-id="6079f-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="6079f-207">104.42.238.205</span></span> |
| <span data-ttu-id="6079f-208">Oeste dos EUA 2</span><span class="sxs-lookup"><span data-stu-id="6079f-208">West US 2</span></span> | <span data-ttu-id="6079f-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="6079f-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="6079f-210">Alterar a política de conexão do Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="6079f-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="6079f-211">Olá toochange diretiva de conexão de banco de dados SQL para um servidor de banco de dados SQL, use Olá [API REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="6079f-211">toochange hello Azure SQL Database connection policy for an Azure SQL Database server, use hello [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="6079f-212">Se a diretiva de conexão está definida muito**Proxy**, todo o fluxo de pacotes por meio do gateway de banco de dados SQL de saudação de rede.</span><span class="sxs-lookup"><span data-stu-id="6079f-212">If your connection policy is set too**Proxy**, all network packets flow via hello Azure SQL Database gateway.</span></span> <span data-ttu-id="6079f-213">Para essa configuração, você precisa tooallow tooonly saída hello Azure SQL Database gateway IP.</span><span class="sxs-lookup"><span data-stu-id="6079f-213">For this setting, you need tooallow outbound tooonly hello Azure SQL Database gateway IP.</span></span> <span data-ttu-id="6079f-214">Usar uma configuração de **Proxy** resulta em uma latência maior do que aquela da configuração de **Redirecionamento**.</span><span class="sxs-lookup"><span data-stu-id="6079f-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="6079f-215">Se a diretiva de conexão está definindo **redirecionar**, todos os pacotes de rede diretamente fluem toohello middleware proxy.</span><span class="sxs-lookup"><span data-stu-id="6079f-215">If your connection policy is setting **Redirect**, all network packets flow directly toohello middleware proxy.</span></span> <span data-ttu-id="6079f-216">Para essa configuração, você precisa tooallow saída toomultiple IPs.</span><span class="sxs-lookup"><span data-stu-id="6079f-216">For this setting, you need tooallow outbound toomultiple IPs.</span></span> 

## <a name="script-toochange-connection-settings"></a><span data-ttu-id="6079f-217">Configurações de conexão do script toochange</span><span class="sxs-lookup"><span data-stu-id="6079f-217">Script toochange connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6079f-218">Este script requer Olá [módulo Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="6079f-218">This script requires hello [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="6079f-219">saudação de script do PowerShell a seguir mostra como toochange Olá diretiva de conexão.</span><span class="sxs-lookup"><span data-stu-id="6079f-219">hello following PowerShell script shows how toochange hello connection policy.</span></span>

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="6079f-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6079f-220">Next steps</span></span>

- <span data-ttu-id="6079f-221">Para obter informações sobre como toochange Olá diretiva de conexão de banco de dados SQL para um servidor de banco de dados SQL, consulte [criar ou atualizar política de Conexão de servidor usando Olá REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="6079f-221">For information on how toochange hello Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using hello REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="6079f-222">Para obter mais informações sobre o comportamento de conexão do Banco de Dados SQL do Azure para clientes que usam ADO.NET 4.5 ou uma versão mais recente, consulte [Portas depois da 1433 para ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="6079f-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="6079f-223">Para obter informações sobre a visão geral do desenvolvimento de aplicativos em geral, consulte [Visão Geral do Desenvolvimento de Aplicativos do Banco de Dados SQL](sql-database-develop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6079f-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
