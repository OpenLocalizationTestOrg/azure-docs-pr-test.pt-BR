---
title: Conectar-se ao Azure Data Lake Store por Redes Virtuais | Microsoft Docs
description: Conectar-se ao Azure Data Lake Store pelas Redes Virtuais do Azure
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ff7d28d7b53e872b804788647b1e672fafcf6995
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a><span data-ttu-id="4c95a-103">Acessar o Azure Data Lake Store por VMs em uma Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="4c95a-103">Access Azure Data Lake Store from VMs within an Azure VNET</span></span>
<span data-ttu-id="4c95a-104">O Azure Data Lake Store é um serviço de PaaS executado em endereços de IP de Internet públicos.</span><span class="sxs-lookup"><span data-stu-id="4c95a-104">Azure Data Lake Store is a PaaS service that runs on public Internet IP addresses.</span></span> <span data-ttu-id="4c95a-105">Em geral, qualquer servidor que pode se conectar à Internet pública também pode se conectar a pontos de extremidade do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4c95a-105">Any server that can connect to the public Internet can typically connect to Azure Data Lake Store endpoints as well.</span></span> <span data-ttu-id="4c95a-106">Por padrão, todas as VMs que estão em Redes Virtuais do Azure podem acessar a Internet e, portanto, podem acessar o Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4c95a-106">By default, all VMs that are in Azure VNETs can access the Internet and hence can access Azure Data Lake Store.</span></span> <span data-ttu-id="4c95a-107">No entanto, é possível configurar VMs em uma Rede Virtual para que ela não tenha acesso à Internet.</span><span class="sxs-lookup"><span data-stu-id="4c95a-107">However, it is possible to configure VMs in a VNET to not have access to the Internet.</span></span> <span data-ttu-id="4c95a-108">Para essas VMs, o acesso ao Azure Data Lake Store também é restrito.</span><span class="sxs-lookup"><span data-stu-id="4c95a-108">For such VMs, access to Azure Data Lake Store is restricted as well.</span></span> <span data-ttu-id="4c95a-109">O bloqueio do acesso à Internet pública para VMs em Redes Virtuais do Azure pode ser feito usando uma das abordagens a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c95a-109">Blocking public Internet access for VMs in Azure VNETs can be done using any of the following approach.</span></span>

* <span data-ttu-id="4c95a-110">Configurando NSGs (Grupos de Segurança de Rede)</span><span class="sxs-lookup"><span data-stu-id="4c95a-110">By configuring Network Security Groups (NSG)</span></span>
* <span data-ttu-id="4c95a-111">Configurando UDRs (Rotas Definidas pelo Usuário)</span><span class="sxs-lookup"><span data-stu-id="4c95a-111">By configuring User Defined Routes (UDR)</span></span>
* <span data-ttu-id="4c95a-112">Trocando rotas pelo protocolo BGP (protocolo de roteamento dinâmico padrão do setor) quando o ExpressRoute é usado e que bloqueia o acesso à Internet</span><span class="sxs-lookup"><span data-stu-id="4c95a-112">By exchanging routes via BGP (industry standard dynamic routing protocol) when ExpressRoute is used that block access to the Internet</span></span>

<span data-ttu-id="4c95a-113">Neste artigo, você saberá como habilitar o acesso ao Azure Data Lake Store em VMs do Azure que foram restritas para acessar os recursos, usando um dos três métodos listados acima.</span><span class="sxs-lookup"><span data-stu-id="4c95a-113">In this article, you will learn how to enable access to the Azure Data Lake Store from Azure VMs which have been restricted to access resources using one of the three methods listed above.</span></span>

## <a name="enabling-connectivity-to-azure-data-lake-store-from-vms-with-restricted-connectivity"></a><span data-ttu-id="4c95a-114">Habilitando a conectividade com o Azure Data Lake Store em VMs com conectividade restrita</span><span class="sxs-lookup"><span data-stu-id="4c95a-114">Enabling connectivity to Azure Data Lake Store from VMs with restricted connectivity</span></span>
<span data-ttu-id="4c95a-115">Para acessar o Azure Data Lake Store nessas VMs, você deve configurá-las para acessar o endereço IP em que a conta do Azure Data Lake Store está disponível.</span><span class="sxs-lookup"><span data-stu-id="4c95a-115">To access Azure Data Lake Store from such VMs, you must configure them to access the IP address where the Azure Data Lake Store account is available.</span></span> <span data-ttu-id="4c95a-116">Identifique os endereços IP das contas do Data Lake Store resolvendo os nomes DNS das contas (`<account>.azuredatalakestore.net`).</span><span class="sxs-lookup"><span data-stu-id="4c95a-116">You can identify the IP addresses for your Data Lake Store accounts by resolving the DNS names of your accounts (`<account>.azuredatalakestore.net`).</span></span> <span data-ttu-id="4c95a-117">Para isso, use ferramentas como **nslookup**.</span><span class="sxs-lookup"><span data-stu-id="4c95a-117">For this you can use tools such as **nslookup**.</span></span> <span data-ttu-id="4c95a-118">Abra um prompt de comando no computador e execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c95a-118">Open a command prompt on your computer and run the following command.</span></span>

    nslookup mydatastore.azuredatalakestore.net

<span data-ttu-id="4c95a-119">A saída é semelhante ao mostrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c95a-119">The output resembles the following.</span></span> <span data-ttu-id="4c95a-120">O valor na propriedade **Address** é o endereço IP associado à sua conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4c95a-120">The value against **Address** property is the IP address associated with your Data Lake Store account.</span></span>

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a><span data-ttu-id="4c95a-121">Habilitando a conectividade em VMs restritas usando o NSG</span><span class="sxs-lookup"><span data-stu-id="4c95a-121">Enabling connectivity from VMs restricted by using NSG</span></span>
<span data-ttu-id="4c95a-122">Quando uma regra do NSG é usada para bloquear o acesso à Internet, é possível criar outro NSG que permite o acesso ao Endereço IP do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4c95a-122">When a NSG rule is used to block access to the Internet, then you can create another NSG that allows access to the Data Lake Store IP Address.</span></span> <span data-ttu-id="4c95a-123">Mais informações sobre as regras do NSG estão disponíveis em [O que é um Grupo de Segurança de Rede?](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="4c95a-123">More information on NSG rules is available at [What is a Network Security Group?](../virtual-network/virtual-networks-nsg.md).</span></span> <span data-ttu-id="4c95a-124">Para obter instruções sobre como criar NSGs, consulte [Como gerenciar NSGs usando o portal do Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="4c95a-124">For instructions on how to create NSGs see [How to manage NSGs using the Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a><span data-ttu-id="4c95a-125">Habilitando a conectividade em VMs restritas usando a UDR ou o ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4c95a-125">Enabling connectivity from VMs restricted by using UDR or ExpressRoute</span></span>
<span data-ttu-id="4c95a-126">Quando rotas, sejam UDRs ou rotas trocadas pelo protocolo BGP, são usadas para bloquear o acesso à Internet, uma rota especial precisa ser configurada para que as VMs nessas sub-redes possam acessar os pontos de extremidade do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4c95a-126">When routes, either UDRs or BGP-exchanged routes, are used to block access to the Internet, a special route needs to be configured so that VMs in such subnets can access Data Lake Store endpoints.</span></span> <span data-ttu-id="4c95a-127">Para obter mais informações, consulte [O que são Rotas Definidas pelo Usuário?](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c95a-127">For more information, see [What are User Defined Routes?](../virtual-network/virtual-networks-udr-overview.md).</span></span> <span data-ttu-id="4c95a-128">Para obter instruções sobre como criar UDRs, consulte [Criar UDRs no Gerenciador de Recursos](../virtual-network/virtual-network-create-udr-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4c95a-128">For instructions on creating UDRs, see [Create UDRs in Resource Manager](../virtual-network/virtual-network-create-udr-arm-ps.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a><span data-ttu-id="4c95a-129">Habilitando a conectividade em VMs restritas usando o ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4c95a-129">Enabling connectivity from VMs restricted by using ExpressRoute</span></span>
<span data-ttu-id="4c95a-130">Quando um circuito do ExpressRoute está configurado, os servidores locais podem acessar o Data Lake Store por meio do emparelhamento público.</span><span class="sxs-lookup"><span data-stu-id="4c95a-130">When an ExpressRoute circuit is configured, the on-premises servers can access Data Lake Store through public peering.</span></span> <span data-ttu-id="4c95a-131">Mais detalhes sobre como configurar o emparelhamento público no ExpressRoute está disponível em [Perguntas frequentes sobre o ExpressRoute](../expressroute/expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="4c95a-131">More details on configuring ExpressRoute for public peering is available at [ExpressRoute FAQs](../expressroute/expressroute-faqs.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4c95a-132">Confira também</span><span class="sxs-lookup"><span data-stu-id="4c95a-132">See also</span></span>
* [<span data-ttu-id="4c95a-133">Visão geral do Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="4c95a-133">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="4c95a-134">Protegendo os dados armazenados no Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4c95a-134">Securing data stored in Azure Data Lake Store</span></span>](data-lake-store-security-overview.md)

