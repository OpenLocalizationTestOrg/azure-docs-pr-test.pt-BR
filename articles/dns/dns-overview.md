---
title: aaaOverview do DNS do Azure | Microsoft Docs
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
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="63c15-104">Visão geral do DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="63c15-104">Azure DNS overview</span></span>

<span data-ttu-id="63c15-105">Olá, sistema de nomes de domínio ou DNS, é responsável pela conversão (ou seja, resolver) um site ou serviço name tooits endereço IP.</span><span class="sxs-lookup"><span data-stu-id="63c15-105">hello Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name tooits IP address.</span></span> <span data-ttu-id="63c15-106">O DNS do Azure é um serviço de hospedagem para domínios DNS, fornecendo resolução de nomes usando a infraestrutura do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="63c15-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="63c15-107">Ao hospedar seus domínios no Azure, você pode gerenciar seu DNS registros usando Olá mesmo credenciais, APIs, ferramentas e cobrança como outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="63c15-107">By hosting your domains in Azure, you can manage your DNS records using hello same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![Visão geral de DNS](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="63c15-109">Recursos</span><span class="sxs-lookup"><span data-stu-id="63c15-109">Features</span></span>

* <span data-ttu-id="63c15-110">**Confiabilidade e desempenho** - domínios DNS no DNS do Azure são hospedados na rede global do Azure de servidores de nomes DNS.</span><span class="sxs-lookup"><span data-stu-id="63c15-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="63c15-111">Usamos a difusão de rede para que cada consulta DNS for atendida, o servidor DNS mais próximo disponível para o hello.</span><span class="sxs-lookup"><span data-stu-id="63c15-111">We use Anycast networking so that each DNS query is answered by hello closest available DNS server.</span></span> <span data-ttu-id="63c15-112">Isso fornece desempenho rápido e alta disponibilidade para seu domínio.</span><span class="sxs-lookup"><span data-stu-id="63c15-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="63c15-113">**Integração perfeita** -serviço de DNS do Azure Olá pode ser usado toomanage registros de DNS para os serviços do Azure e pode ser usado tooprovide DNS para os recursos externos, bem.</span><span class="sxs-lookup"><span data-stu-id="63c15-113">**Seamless integration** - hello Azure DNS service can be used toomanage DNS records for your Azure services and can be used tooprovide DNS for your external resources as well.</span></span> <span data-ttu-id="63c15-114">DNS do Azure é integrado no hello portal do Azure e usa Olá as mesmas credenciais, cobrança e contrato de suporte como os outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="63c15-114">Azure DNS is integrated in hello Azure portal and uses hello same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="63c15-115">**Segurança** -Olá serviço DNS do Azure baseia-se no Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="63c15-115">**Security** - hello Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="63c15-116">Sendo assim, ele aproveita recursos do Resource Manager, como o controle de acesso baseado em função, os logs de auditoria e o bloqueio de recursos.</span><span class="sxs-lookup"><span data-stu-id="63c15-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="63c15-117">Seus domínios e registros podem ser gerenciados por meio de saudação portal do Azure, cmdlets do PowerShell do Azure, em Olá CLI do Azure de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="63c15-117">Your domains and records can be managed via hello Azure portal, Azure PowerShell cmdlets, and hello cross-platform Azure CLI.</span></span> <span data-ttu-id="63c15-118">Aplicativos que exigem o gerenciamento automático de DNS podem integrar saudação do serviço por meio de saudação API REST e SDKs.</span><span class="sxs-lookup"><span data-stu-id="63c15-118">Applications requiring automatic DNS management can integrate with hello service via hello REST API and SDKs.</span></span>

<span data-ttu-id="63c15-119">O DNS do Azure não dá suporte a compra de nomes de domínio.</span><span class="sxs-lookup"><span data-stu-id="63c15-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="63c15-120">Se você quiser toopurchase domínios, é necessário toouse um registrador de nomes de domínio de terceiro.</span><span class="sxs-lookup"><span data-stu-id="63c15-120">If you want toopurchase domains, you need toouse a third-party domain name registrar.</span></span> <span data-ttu-id="63c15-121">registrador Olá normalmente cobra uma pequena taxa anual.</span><span class="sxs-lookup"><span data-stu-id="63c15-121">hello registrar typically charges a small annual fee.</span></span> <span data-ttu-id="63c15-122">domínios Olá, em seguida, podem ser hospedados no Azure DNS para o gerenciamento de registros de DNS.</span><span class="sxs-lookup"><span data-stu-id="63c15-122">hello domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="63c15-123">Consulte [delegar tooAzure um domínio DNS](dns-domain-delegation.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="63c15-123">See [Delegate a Domain tooAzure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="63c15-124">Preços</span><span class="sxs-lookup"><span data-stu-id="63c15-124">Pricing</span></span>

<span data-ttu-id="63c15-125">Cobrança do DNS é com base no número de saudação de zonas DNS hospedadas no Azure e pelo número de saudação de consultas DNS.</span><span class="sxs-lookup"><span data-stu-id="63c15-125">DNS billing is based on hello number of DNS zones hosted in Azure and by hello number of DNS queries.</span></span> <span data-ttu-id="63c15-126">toolearn mais sobre preços visite [de preços do Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="63c15-126">toolearn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="63c15-127">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="63c15-127">FAQ</span></span>

<span data-ttu-id="63c15-128">Para perguntas frequentes sobre o DNS do Azure, consulte Olá [perguntas Frequentes do Azure DNS](dns-faq.md).</span><span class="sxs-lookup"><span data-stu-id="63c15-128">For frequently asked questions about Azure DNS, see hello [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="63c15-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="63c15-129">Next steps</span></span>

<span data-ttu-id="63c15-130">Saiba mais sobre as zonas e registros DNS visitando: [Visão geral de zonas e registros DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="63c15-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="63c15-131">Saiba como muito[criar uma zona DNS](./dns-getstarted-create-dnszone-portal.md) no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="63c15-131">Learn how too[create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="63c15-132">Saiba mais sobre alguns dos Olá outra chave [recursos de rede](../networking/networking-overview.md) do Azure.</span><span class="sxs-lookup"><span data-stu-id="63c15-132">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

