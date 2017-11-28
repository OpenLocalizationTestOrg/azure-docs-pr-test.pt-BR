---
title: "Visão geral do DNS do Azure | Microsoft Docs"
description: "Visão geral do Serviço de hospedagem de DNS no Microsoft Azure. Hospede seu domínio no Microsoft Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: 3705457e4c90f8869496f7f5177531bd128d1057
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="8731e-104">Visão geral do DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="8731e-104">Azure DNS overview</span></span>

<span data-ttu-id="8731e-105">O sistema de nomes de domínio, ou DNS, é responsável por converter (ou seja, resolver) um nome do site ou serviço para seu endereço IP.</span><span class="sxs-lookup"><span data-stu-id="8731e-105">The Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name to its IP address.</span></span> <span data-ttu-id="8731e-106">O DNS do Azure é um serviço de hospedagem para domínios DNS, fornecendo resolução de nomes usando a infraestrutura do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8731e-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="8731e-107">Ao hospedar seus domínios no Azure, você pode gerenciar seus registros DNS usando as mesmas credenciais, APIs, ferramentas e cobrança que seus outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="8731e-107">By hosting your domains in Azure, you can manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![Visão geral de DNS](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="8731e-109">Recursos</span><span class="sxs-lookup"><span data-stu-id="8731e-109">Features</span></span>

* <span data-ttu-id="8731e-110">**Confiabilidade e desempenho** - domínios DNS no DNS do Azure são hospedados na rede global do Azure de servidores de nomes DNS.</span><span class="sxs-lookup"><span data-stu-id="8731e-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="8731e-111">Podemos usar a rede Anycast, para que cada consulta DNS seja atendida pelo servidor DNS mais próximo disponível.</span><span class="sxs-lookup"><span data-stu-id="8731e-111">We use Anycast networking so that each DNS query is answered by the closest available DNS server.</span></span> <span data-ttu-id="8731e-112">Isso fornece desempenho rápido e alta disponibilidade para seu domínio.</span><span class="sxs-lookup"><span data-stu-id="8731e-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="8731e-113">**Integração perfeita** - o serviço de DNS do Azure pode ser usado para gerenciar os registros DNS para os serviços do Azure e também pode ser usado para fornecer o DNS para os recursos externos.</span><span class="sxs-lookup"><span data-stu-id="8731e-113">**Seamless integration** - The Azure DNS service can be used to manage DNS records for your Azure services and can be used to provide DNS for your external resources as well.</span></span> <span data-ttu-id="8731e-114">O DNS do Azure é integrado no portal do Azure e usa as mesmas credenciais, cobrança e contrato de suporte que outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="8731e-114">Azure DNS is integrated in the Azure portal and uses the same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="8731e-115">**Segurança** - o serviço de DNS do Azure baseia-se no Azure Resource Manager, Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8731e-115">**Security** - The Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="8731e-116">Sendo assim, ele aproveita recursos do Resource Manager, como o controle de acesso baseado em função, os logs de auditoria e o bloqueio de recursos.</span><span class="sxs-lookup"><span data-stu-id="8731e-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="8731e-117">Seus domínios e registros podem ser gerenciados por meio do portal do Azure, cmdlets do Azure PowerShell e a CLI do Azure de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="8731e-117">Your domains and records can be managed via the Azure portal, Azure PowerShell cmdlets, and the cross-platform Azure CLI.</span></span> <span data-ttu-id="8731e-118">Aplicativos que requerem gerenciamento automático de DNS podem se integrar com o serviço por meio da API REST e dos SDKs.</span><span class="sxs-lookup"><span data-stu-id="8731e-118">Applications requiring automatic DNS management can integrate with the service via the REST API and SDKs.</span></span>

<span data-ttu-id="8731e-119">O DNS do Azure não dá suporte a compra de nomes de domínio.</span><span class="sxs-lookup"><span data-stu-id="8731e-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="8731e-120">Se você deseja adquirir domínios, será necessário usar um registrador de nomes de domínio de terceiros.</span><span class="sxs-lookup"><span data-stu-id="8731e-120">If you want to purchase domains, you need to use a third-party domain name registrar.</span></span> <span data-ttu-id="8731e-121">O registrador normalmente cobra uma pequena taxa anual.</span><span class="sxs-lookup"><span data-stu-id="8731e-121">The registrar typically charges a small annual fee.</span></span> <span data-ttu-id="8731e-122">Os domínios, em seguida, podem ser hospedados no DNS do Azure para gerenciamento de registros DNS.</span><span class="sxs-lookup"><span data-stu-id="8731e-122">The domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="8731e-123">Consulte [Delegar um domínio ao DNS do Azure](dns-domain-delegation.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="8731e-123">See [Delegate a Domain to Azure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="8731e-124">Preços</span><span class="sxs-lookup"><span data-stu-id="8731e-124">Pricing</span></span>

<span data-ttu-id="8731e-125">O preço do Azure é baseado no número de zonas DNS hospedadas no Azure e o número de consultas DNS.</span><span class="sxs-lookup"><span data-stu-id="8731e-125">DNS billing is based on the number of DNS zones hosted in Azure and by the number of DNS queries.</span></span> <span data-ttu-id="8731e-126">Para saber mais sobre os preços, visite [Preços de DNS do Azure](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="8731e-126">To learn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="8731e-127">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="8731e-127">FAQ</span></span>

<span data-ttu-id="8731e-128">Para ver as perguntas frequentes sobre o DNS do Azure, veja o [Perguntas frequentes do DNS do Azure](dns-faq.md).</span><span class="sxs-lookup"><span data-stu-id="8731e-128">For frequently asked questions about Azure DNS, see the [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8731e-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8731e-129">Next steps</span></span>

<span data-ttu-id="8731e-130">Saiba mais sobre as zonas e registros DNS visitando: [Visão geral de zonas e registros DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="8731e-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="8731e-131">Saiba como [criar uma zona DNS](./dns-getstarted-create-dnszone-portal.md) no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="8731e-131">Learn how to [create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="8731e-132">Saiba mais sobre alguns dos outros principais [recursos de rede](../networking/networking-overview.md) do Azure.</span><span class="sxs-lookup"><span data-stu-id="8731e-132">Learn about some of the other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

