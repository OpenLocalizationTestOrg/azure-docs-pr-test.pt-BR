---
title: Hospedagem de zonas de pesquisa de DNS reverso no Azure DNS | Microsoft Docs
description: Aprenda a usar o DNS do Azure para hospedar as zonas de pesquisa inversas de DNS para seus intervalos de IP
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 3e10b25d2f9b91c96af2958fef6dc6a4fdbff301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="43cba-103">Hospedagem de zonas de pesquisa de DNS reverso no Azure DNS</span><span class="sxs-lookup"><span data-stu-id="43cba-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="43cba-104">Este artigo explica como hospedar as zonas de pesquisa inversas do DNS para seus intervalos de IP atribuídos no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="43cba-104">This article explains how to host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="43cba-105">Os intervalos de IP representados pela zona de pesquisa inversa devem ser atribuídos à sua organização, normalmente por seu ISP.</span><span class="sxs-lookup"><span data-stu-id="43cba-105">The IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="43cba-106">Para configurar o DNS reverso para o endereço IP de propriedade do Azure atribuído ao serviço do Azure, veja [Configurar a pesquisa inversa para os endereços IP alocados em seu serviço do Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="43cba-106">To configure reverse DNS for Azure-owned IP address assigned to your Azure service, see [configure the reverse lookup for the IP addresses allocated to your Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="43cba-107">Antes de ler este artigo, você deve estar familiarizado com essa [Visão geral de DNS reverso e suporte no Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="43cba-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="43cba-108">Este artigo explica as etapas para criar sua primeira zona DNS de pesquisa inversa e registro DNS usando o Portal do Azure, Azure PowerShell, CLI 1.0 do Azure ou CLI 2.0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="43cba-108">This article walks you through the steps to create your first reverse lookup DNS zone and record using the Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="43cba-109">Criar uma zona DNS de pesquisa inversa</span><span class="sxs-lookup"><span data-stu-id="43cba-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="43cba-110">Entre no [Portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="43cba-110">Sign in to the [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="43cba-111">No menu Hub, clique em **Novo** > **Rede** > e, em seguida, clique em **Zona DNS** para abrir a folha **Criar zona DNS**.</span><span class="sxs-lookup"><span data-stu-id="43cba-111">On the Hub menu, click and click **New** > **Networking** > and then click **DNS zone** to open the **Create DNS zone** blade.</span></span>

   ![Zona DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="43cba-113">Na folha **Criar zona DNS**, dê um nome para sua zona DNS.</span><span class="sxs-lookup"><span data-stu-id="43cba-113">On the **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="43cba-114">O nome da zona é elaborado diferente para prefixos de IPv4 e IPv6.</span><span class="sxs-lookup"><span data-stu-id="43cba-114">The name of the zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="43cba-115">Use as instruções para [IPV4](#ipv4) ou [IPv6](#ipv6) para nomear sua zona.</span><span class="sxs-lookup"><span data-stu-id="43cba-115">Use either the instructions for [IPV4](#ipv4) or [IPv6](#ipv6) to name your zone.</span></span> <span data-ttu-id="43cba-116">Ao concluir, clique em **Criar** para criar a zona.</span><span class="sxs-lookup"><span data-stu-id="43cba-116">When complete click **Create** to create the zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="43cba-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="43cba-117">IPv4</span></span>

<span data-ttu-id="43cba-118">O nome de uma zona de pesquisa inversa de IPv4 baseia-se no intervalo de IP que ela representa.</span><span class="sxs-lookup"><span data-stu-id="43cba-118">The name of an IPv4 reverse lookup zone is based on the IP range it represents.</span></span> <span data-ttu-id="43cba-119">Deve estar no seguinte formato: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="43cba-119">It should be in the following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="43cba-120">Para obter exemplos, veja [Visão geral de DNS reverso e suporte no Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="43cba-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="43cba-121">Ao criar zonas de pesquisa de DNS reverso sem classe no DNS do Azure, você deverá usar um hífen (`-`) em vez de barra invertida ('/') no nome da zona.</span><span class="sxs-lookup"><span data-stu-id="43cba-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in the zone name.</span></span>
>
> <span data-ttu-id="43cba-122">Por exemplo, para o intervalo de IP 192.0.2.128/26, você deve usar `128-26.2.0.192.in-addr.arpa` como o nome da zona em vez de `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="43cba-122">For example, for the IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as the zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="43cba-123">Isso ocorre porque, embora ambos tenham suporte dos padrões de DNS, os nomes de zona DNS que contêm a barra invertida (`/`) não têm suporte no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="43cba-123">This is because, while both are supported by the DNS standards, DNS zone names containing the forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="43cba-124">O exemplo a seguir mostra como criar uma zona DNS reversa 'Classe C' chamada `2.0.192.in-addr.arpa` no DNS do Azure por meio do Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="43cba-124">The following example shows how to create a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via the Azure portal:</span></span>

 ![criar zona DNS](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="43cba-126">O 'Local de grupo de recursos' define o local do grupo de recursos e não tem impacto sobre o local da zona DNS.</span><span class="sxs-lookup"><span data-stu-id="43cba-126">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="43cba-127">O local da zona DNS sempre é 'global' e não é exibido.</span><span class="sxs-lookup"><span data-stu-id="43cba-127">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="43cba-128">Os exemplos a seguir mostram como concluir essa tarefa com o Azure PowerShell e a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="43cba-128">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="43cba-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="43cba-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="43cba-130">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="43cba-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="43cba-131">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="43cba-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="43cba-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="43cba-132">IPv6</span></span>

<span data-ttu-id="43cba-133">O nome de uma zona de pesquisa inversa de IPv6 deve estar no seguinte formato: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="43cba-133">The name of an IPv6 reverse lookup zone should be in the following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="43cba-134">Para obter exemplos, veja [Visão geral de DNS reverso e suporte no Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="43cba-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="43cba-135">O exemplo a seguir mostra como criar uma zona de pesquisa inversa de DNS de IPv6 chamada `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` no DNS do Azure por meio do Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="43cba-135">The following example shows how to create an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via the Azure portal:</span></span>

 ![criar zona DNS](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="43cba-137">O 'Local de grupo de recursos' define o local do grupo de recursos e não tem impacto sobre o local da zona DNS.</span><span class="sxs-lookup"><span data-stu-id="43cba-137">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="43cba-138">O local da zona DNS sempre é 'global' e não é exibido.</span><span class="sxs-lookup"><span data-stu-id="43cba-138">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="43cba-139">Os exemplos a seguir mostram como concluir essa tarefa com o Azure PowerShell e a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="43cba-139">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="43cba-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="43cba-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="43cba-141">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="43cba-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="43cba-142">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="43cba-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="43cba-143">Delegar uma zona de pesquisa inversa de DNS</span><span class="sxs-lookup"><span data-stu-id="43cba-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="43cba-144">Depois de criar a zona de pesquisa inversa de DNS, você deverá garantir que a zona seja delegada a partir da zona pai.</span><span class="sxs-lookup"><span data-stu-id="43cba-144">Having created your reverse DNS lookup zone, you must ensure that the zone is delegated from the parent zone.</span></span> <span data-ttu-id="43cba-145">A delegação de DNS permite que o processo de resolução de nome DNS localize os servidores de nomes que hospedam a zona de pesquisa inversa de DNS.</span><span class="sxs-lookup"><span data-stu-id="43cba-145">DNS delegation enables the DNS name resolution process to find the name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="43cba-146">Isso permite que os servidores de nomes respondam a consultas inversas de DNS para os endereços IP em seu intervalo de endereços.</span><span class="sxs-lookup"><span data-stu-id="43cba-146">This enables those name servers to answer DNS reverse queries for the IP addresses in your address range.</span></span>

<span data-ttu-id="43cba-147">Para zonas de pesquisa direta, o processo de delegação de uma zona DNS está descrito em [Delegar seu domínio ao DNS do Azure](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="43cba-147">For forward lookup zones, the process of delegating a DNS zone is described in [Delegate your domain to Azure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="43cba-148">A delegação de zonas de pesquisa inversa funciona da mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="43cba-148">Delegation for reverse lookup zones works the same way.</span></span> <span data-ttu-id="43cba-149">A única diferença é que você precisa configurar os servidores de nome com o provedor que forneceu o intervalo de IP, em vez de seu registrador de nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="43cba-149">The only difference is that you need to configure the name servers with the ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="43cba-150">Criar um registro PTR DNS</span><span class="sxs-lookup"><span data-stu-id="43cba-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="43cba-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="43cba-151">IPv4</span></span>

<span data-ttu-id="43cba-152">O exemplo a seguir explica o processo de criação de um registro PTR em uma zona DNS reverso no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="43cba-152">The following example walks you through the process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="43cba-153">Para outros tipos de registro e para modificar os registros existentes, confira [Gerenciar registros DNS e conjuntos de registros usando o Portal do Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="43cba-153">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="43cba-154">Na parte superior da folha **zona DNS**, selecione **+Conjunto de registros** para abrir a folha **Adicionar conjunto de registros**.</span><span class="sxs-lookup"><span data-stu-id="43cba-154">At the top of the **DNS zone** blade, select **+ Record set** to open the **Add record set** blade.</span></span>

 ![Zona DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="43cba-156">Na folha **Adicionar conjunto de registros**.</span><span class="sxs-lookup"><span data-stu-id="43cba-156">On the **Add record set** blade.</span></span> 
1. <span data-ttu-id="43cba-157">Selecione **PTR** do menu de registro "**Tipo**".</span><span class="sxs-lookup"><span data-stu-id="43cba-157">Select **PTR** from the record "**Type**" menu.</span></span>  
1. <span data-ttu-id="43cba-158">O nome do registro definido para um registro PTR precisa ser o restante do endereço IPv4 na ordem inversa.</span><span class="sxs-lookup"><span data-stu-id="43cba-158">The name of the record set for a PTR record needs to be the rest of the IPv4 address in reverse order.</span></span> <span data-ttu-id="43cba-159">Neste exemplo, os três primeiros octetos já estão preenchidos como parte do nome da zona (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="43cba-159">In this example, the first three octets are already populated as part of the zone name (.2.0.192).</span></span> <span data-ttu-id="43cba-160">Portanto, apenas o último octeto é fornecido no campo de nome.</span><span class="sxs-lookup"><span data-stu-id="43cba-160">Therefore, only the last octet is supplied in the name field.</span></span> <span data-ttu-id="43cba-161">Por exemplo, você poderia nomear seu conjunto de registros "**15**" para um recurso cujo endereço IP é 192.0.2.15.</span><span class="sxs-lookup"><span data-stu-id="43cba-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="43cba-162">No campo "**Nome de Domínio**", insira o nome de domínio totalmente qualificado (FQDN) do recurso usando o IP.</span><span class="sxs-lookup"><span data-stu-id="43cba-162">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
1. <span data-ttu-id="43cba-163">Selecione **OK** na parte inferior da folha para criar o registro DNS.</span><span class="sxs-lookup"><span data-stu-id="43cba-163">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

 ![adicionar conjunto de registros](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="43cba-165">Os exemplos a seguir mostram como concluir essa tarefa com o PowerShell e a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="43cba-165">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="43cba-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="43cba-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="43cba-167">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="43cba-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="43cba-168">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="43cba-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="43cba-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="43cba-169">IPv6</span></span>

<span data-ttu-id="43cba-170">O exemplo a seguir explica o processo de criação de um novo registro 'PTR'.</span><span class="sxs-lookup"><span data-stu-id="43cba-170">The following example walks you through the process of creating new 'PTR' record.</span></span> <span data-ttu-id="43cba-171">Para outros tipos de registro e para modificar os registros existentes, confira [Gerenciar registros DNS e conjuntos de registros usando o Portal do Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="43cba-171">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="43cba-172">Na parte superior da folha **zona DNS**, selecione **+Conjunto de registros** para abrir a folha **Adicionar conjunto de registros**.</span><span class="sxs-lookup"><span data-stu-id="43cba-172">At the top of the **DNS zone blade**, select **+ Record set** to open the **Add record set** blade.</span></span>

  ![folha de zona DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="43cba-174">Na folha **Adicionar conjunto de registros**.</span><span class="sxs-lookup"><span data-stu-id="43cba-174">On the **Add record set** blade.</span></span> 
3. <span data-ttu-id="43cba-175">Selecione **PTR** do menu de registro "**Tipo**".</span><span class="sxs-lookup"><span data-stu-id="43cba-175">Select **PTR** from the record "**Type**" menu.</span></span>  
4. <span data-ttu-id="43cba-176">O nome do registro definido para um registro PTR precisa ser o restante do endereço IPv6 na ordem inversa.</span><span class="sxs-lookup"><span data-stu-id="43cba-176">The name of the record set for a PTR record needs to be the rest of the IPv6 address in reverse order.</span></span> <span data-ttu-id="43cba-177">Ele não deve incluir compactação.</span><span class="sxs-lookup"><span data-stu-id="43cba-177">It must not include any zero compression.</span></span> <span data-ttu-id="43cba-178">Neste exemplo, os primeiros 64 bits do IPv6 já estão preenchidos como parte do nome da zona (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="43cba-178">In this example, the first 64 bits of the IPv6 are already populated as part of the zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="43cba-179">Portanto, apenas os últimos 64 bits são fornecidos no campo de nome.</span><span class="sxs-lookup"><span data-stu-id="43cba-179">Therefore, only the last 64 bits are supplied in the name field.</span></span> <span data-ttu-id="43cba-180">Os últimos 64 bits do endereço IP são inseridos na ordem inversa, usando um período como o delimitador entre cada número hexadecimal.</span><span class="sxs-lookup"><span data-stu-id="43cba-180">The last 64 bits of the IP address are entered in reverse order, using a period as the delimiter between each hexadecimal number.</span></span> <span data-ttu-id="43cba-181">Por exemplo, você poderia nomear seu conjunto de registros "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" para um recurso cujo endereço IP é 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span><span class="sxs-lookup"><span data-stu-id="43cba-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="43cba-182">No campo "**Nome de Domínio**", insira o nome de domínio totalmente qualificado (FQDN) do recurso usando o IP.</span><span class="sxs-lookup"><span data-stu-id="43cba-182">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
6. <span data-ttu-id="43cba-183">Selecione **OK** na parte inferior da folha para criar o registro DNS.</span><span class="sxs-lookup"><span data-stu-id="43cba-183">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

![adicionar conjunto de registros](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="43cba-185">Os exemplos a seguir mostram como concluir essa tarefa com o PowerShell e a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="43cba-185">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="43cba-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="43cba-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="43cba-187">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="43cba-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="43cba-188">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="43cba-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="43cba-189">Exibir registros</span><span class="sxs-lookup"><span data-stu-id="43cba-189">View Records</span></span>

<span data-ttu-id="43cba-190">Para exibir os registros que você criou, navegue até sua zona DNS no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="43cba-190">To view the records you created, navigate to your DNS zone in the Azure portal.</span></span> <span data-ttu-id="43cba-191">Na parte inferior da folha **Zona DNS**, é possível ver os registros da zona DNS.</span><span class="sxs-lookup"><span data-stu-id="43cba-191">In the lower part of the **DNS zone** blade, you can see the records for the DNS zone.</span></span> <span data-ttu-id="43cba-192">Você deve ver os registros NS e SOA padrão, que são criados em cada zona, além de quaisquer registros novos que você criou.</span><span class="sxs-lookup"><span data-stu-id="43cba-192">You should see the default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="43cba-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="43cba-193">IPv4</span></span>

<span data-ttu-id="43cba-194">Folha de zona DNS, mostrando os registros PTR de IPv4:</span><span class="sxs-lookup"><span data-stu-id="43cba-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![folha de zona DNS](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="43cba-196">Os exemplos a seguir mostram como exibir os registros PTR usando o PowerShell ou a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="43cba-196">The following examples show how to view the PTR records using PowerShell or the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="43cba-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="43cba-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="43cba-198">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="43cba-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="43cba-199">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="43cba-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="43cba-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="43cba-200">IPv6</span></span>

<span data-ttu-id="43cba-201">Folha de zona DNS, mostrando os registros PTR de IPv6:</span><span class="sxs-lookup"><span data-stu-id="43cba-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![folha de zona DNS](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="43cba-203">Os exemplos a seguir mostram como exibir os registros usando o PowerShell ou a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="43cba-203">The following are examples on how to view the records with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="43cba-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="43cba-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="43cba-205">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="43cba-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="43cba-206">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="43cba-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="43cba-207">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="43cba-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="43cba-208">Posso hospedar zonas de pesquisa inversa de DNS para meus blocos IP atribuídos pelo ISP no DNS do Azure?</span><span class="sxs-lookup"><span data-stu-id="43cba-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="43cba-209">Sim.</span><span class="sxs-lookup"><span data-stu-id="43cba-209">Yes.</span></span> <span data-ttu-id="43cba-210">A hospedagem das zonas de pesquisa inversa (ARPA) para seus próprios intervalos de IP no DNS do Azure tem suporte total.</span><span class="sxs-lookup"><span data-stu-id="43cba-210">Hosting the reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="43cba-211">Crie a zona de pesquisa inversa no DNS do Azure conforme explicado neste artigo e trabalhe com seu provedor de serviços de Internet para [delegar a zona](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="43cba-211">Create the reverse lookup zone in Azure DNS as explained in this article, then work with your ISP to [delegate the zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="43cba-212">Em seguida, você pode gerenciar os registros PTR para cada pesquisa inversa da mesma forma que outros tipos de registro.</span><span class="sxs-lookup"><span data-stu-id="43cba-212">You can then manage the PTR records for each reverse lookup in the same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="43cba-213">Quanto custa hospedar minha zona de pesquisa inverso de DNS?</span><span class="sxs-lookup"><span data-stu-id="43cba-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="43cba-214">A hospedagem da zona de pesquisa inversa de DNS para o bloco IP atribuído pelo ISP no DNS do Azure é cobrado usando [taxas padrão do DNS do Azure](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="43cba-214">Hosting the reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="43cba-215">Posso hospedar zonas de pesquisa inversa de DNS para endereços IPv4 e IPv6 no DNS do Azure?</span><span class="sxs-lookup"><span data-stu-id="43cba-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="43cba-216">Sim.</span><span class="sxs-lookup"><span data-stu-id="43cba-216">Yes.</span></span> <span data-ttu-id="43cba-217">Este artigo explica como criar zonas de pesquisa inversa de DNS de IPv4 e IPv6 no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="43cba-217">This article explains how to create both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="43cba-218">Posso importar uma zona de pesquisa inversa de DNS existente?</span><span class="sxs-lookup"><span data-stu-id="43cba-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="43cba-219">Sim.</span><span class="sxs-lookup"><span data-stu-id="43cba-219">Yes.</span></span> <span data-ttu-id="43cba-220">Você pode usar a CLI do Azure para importar as zonas DNS existentes para o DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="43cba-220">You can use the Azure CLI to import existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="43cba-221">Isso funciona para zonas de pesquisa direta e zonas de pesquisa inversa.</span><span class="sxs-lookup"><span data-stu-id="43cba-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="43cba-222">Para saber mais, veja [Importar e exportar um arquivo de zona DNS usando a CLI do Azure](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="43cba-222">For more information, see [Import and export a DNS zone file using the Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="43cba-223">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="43cba-223">Next steps</span></span>

<span data-ttu-id="43cba-224">Para saber mais sobre DNS reverso, confira [Pesquisa de DNS reverso na Wikipédia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="43cba-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="43cba-225">Saiba como [gerenciar registros DNS reversos para seus serviços do Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="43cba-225">Learn how to [manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
