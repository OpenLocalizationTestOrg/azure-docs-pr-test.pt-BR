---
title: aaaHosting inverter as zonas de pesquisa DNS no DNS do Azure | Microsoft Docs
description: "Saiba como saudação do toouse DNS do Azure toohost inverter as zonas de pesquisa DNS para seus intervalos de IP"
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
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="72ee8-103">Hospedagem de zonas de pesquisa de DNS reverso no Azure DNS</span><span class="sxs-lookup"><span data-stu-id="72ee8-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="72ee8-104">Este artigo explica como toohost Olá inverter as zonas de pesquisa DNS para seus intervalos IP atribuídos no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="72ee8-104">This article explains how toohost hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="72ee8-105">os intervalos IP Hello representados por zona de pesquisa inversa Olá devem ser atribuídos tooyour organização, normalmente por seu ISP.</span><span class="sxs-lookup"><span data-stu-id="72ee8-105">hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="72ee8-106">tooconfigure inversa de DNS para a propriedade Azure IP endereço atribuído tooyour serviço do Azure, consulte [Configurar pesquisa inversa Olá para endereços IP de saudação alocados tooyour serviço do Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="72ee8-106">tooconfigure reverse DNS for Azure-owned IP address assigned tooyour Azure service, see [configure hello reverse lookup for hello IP addresses allocated tooyour Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="72ee8-107">Antes de ler este artigo, você deve estar familiarizado com essa [Visão geral de DNS reverso e suporte no Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="72ee8-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="72ee8-108">Este artigo orienta Olá etapas toocreate sua primeira zona pesquisa inversa de DNS e o registro usando Olá portal do Azure, o PowerShell do Azure, Azure CLI 1.0 ou 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="72ee8-108">This article walks you through hello steps toocreate your first reverse lookup DNS zone and record using hello Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="72ee8-109">Criar uma zona DNS de pesquisa inversa</span><span class="sxs-lookup"><span data-stu-id="72ee8-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="72ee8-110">Entrar toohello [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="72ee8-110">Sign in toohello [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="72ee8-111">No menu de Hub hello, clique em e clique em **novo** > **rede** > e, em seguida, clique em **zona DNS** tooopen Olá **zona DNS criar**folha.</span><span class="sxs-lookup"><span data-stu-id="72ee8-111">On hello Hub menu, click and click **New** > **Networking** > and then click **DNS zone** tooopen hello **Create DNS zone** blade.</span></span>

   ![Zona DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="72ee8-113">Em Olá **zona DNS criar** folha, nomeie a zona DNS.</span><span class="sxs-lookup"><span data-stu-id="72ee8-113">On hello **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="72ee8-114">nome de saudação da zona de saudação é criado diferente para os prefixos de IPv4 e IPv6.</span><span class="sxs-lookup"><span data-stu-id="72ee8-114">hello name of hello zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="72ee8-115">Use qualquer instruções Olá para [IPV4](#ipv4) ou [IPv6](#ipv6) tooname a zona.</span><span class="sxs-lookup"><span data-stu-id="72ee8-115">Use either hello instructions for [IPV4](#ipv4) or [IPv6](#ipv6) tooname your zone.</span></span> <span data-ttu-id="72ee8-116">Quando concluir clique **criar** toocreate zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="72ee8-116">When complete click **Create** toocreate hello zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="72ee8-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="72ee8-117">IPv4</span></span>

<span data-ttu-id="72ee8-118">nome de saudação de uma zona de pesquisa inversa IPv4 é baseado no intervalo IP hello representa.</span><span class="sxs-lookup"><span data-stu-id="72ee8-118">hello name of an IPv4 reverse lookup zone is based on hello IP range it represents.</span></span> <span data-ttu-id="72ee8-119">Ele deve estar no hello formato a seguir: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="72ee8-119">It should be in hello following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="72ee8-120">Para obter exemplos, veja [Visão geral de DNS reverso e suporte no Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="72ee8-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="72ee8-121">Ao criar classless zonas de pesquisa DNS inversas no DNS do Azure, você deve usar um hífen (`-`) em vez de uma barra invertida ('/ ') no nome da zona hello.</span><span class="sxs-lookup"><span data-stu-id="72ee8-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in hello zone name.</span></span>
>
> <span data-ttu-id="72ee8-122">Por exemplo, para Olá IP intervalo 192.0.2.128/26, você deve usar `128-26.2.0.192.in-addr.arpa` como nome da zona Olá em vez de `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="72ee8-122">For example, for hello IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as hello zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="72ee8-123">Isso ocorre porque, enquanto ambos têm suporte pelos padrões de DNS hello, nomes que contenham barra Olá da zona DNS (`/`) não há suporte para caracteres no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="72ee8-123">This is because, while both are supported by hello DNS standards, DNS zone names containing hello forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="72ee8-124">Olá exemplo a seguir mostra como toocreate uma 'classe C' Reverter zona DNS denominada `2.0.192.in-addr.arpa` no DNS do Azure por meio de saudação portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="72ee8-124">hello following example shows how toocreate a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![criar zona DNS](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="72ee8-126">Olá 'Local do grupo de recursos' define o local Olá Olá para grupo de recursos e não tem nenhum impacto na zona DNS de saudação.</span><span class="sxs-lookup"><span data-stu-id="72ee8-126">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="72ee8-127">local da zona DNS Olá é sempre 'global' e não será exibida.</span><span class="sxs-lookup"><span data-stu-id="72ee8-127">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="72ee8-128">Olá exemplos a seguir mostram como toocomplete essa tarefa com o PowerShell do Azure e hello CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="72ee8-128">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="72ee8-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72ee8-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="72ee8-130">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="72ee8-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="72ee8-131">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="72ee8-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="72ee8-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="72ee8-132">IPv6</span></span>

<span data-ttu-id="72ee8-133">nome de saudação de uma zona de pesquisa inversa IPv6 deve estar no hello formulário a seguir: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="72ee8-133">hello name of an IPv6 reverse lookup zone should be in hello following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="72ee8-134">Para obter exemplos, veja [Visão geral de DNS reverso e suporte no Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="72ee8-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="72ee8-135">Olá exemplo a seguir mostra como toocreate uma zona de pesquisa inversa DNS IPv6 nomeados `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` no DNS do Azure por meio de saudação portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="72ee8-135">hello following example shows how toocreate an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![criar zona DNS](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="72ee8-137">Olá 'Local do grupo de recursos' define o local Olá Olá para grupo de recursos e não tem nenhum impacto na zona DNS de saudação.</span><span class="sxs-lookup"><span data-stu-id="72ee8-137">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="72ee8-138">local da zona DNS Olá é sempre 'global' e não será exibida.</span><span class="sxs-lookup"><span data-stu-id="72ee8-138">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="72ee8-139">Olá exemplos a seguir mostram como toocomplete essa tarefa com o PowerShell do Azure e hello CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="72ee8-139">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="72ee8-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72ee8-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="72ee8-141">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="72ee8-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="72ee8-142">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="72ee8-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="72ee8-143">Delegar uma zona de pesquisa inversa de DNS</span><span class="sxs-lookup"><span data-stu-id="72ee8-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="72ee8-144">Tendo criado a zona de pesquisa inversa do DNS, você deve garantir que zona Olá é delegada da zona pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="72ee8-144">Having created your reverse DNS lookup zone, you must ensure that hello zone is delegated from hello parent zone.</span></span> <span data-ttu-id="72ee8-145">Delegação de DNS permite Olá resolução processo toofind Olá nome servidores de nome DNS hospeda a zona de pesquisa inversa do DNS.</span><span class="sxs-lookup"><span data-stu-id="72ee8-145">DNS delegation enables hello DNS name resolution process toofind hello name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="72ee8-146">Isso permite que esses servidores tooanswer DNS inversas consultas de nomes para endereços IP de saudação em seu intervalo de endereços.</span><span class="sxs-lookup"><span data-stu-id="72ee8-146">This enables those name servers tooanswer DNS reverse queries for hello IP addresses in your address range.</span></span>

<span data-ttu-id="72ee8-147">Zonas de pesquisa direta, o processo de saudação de delegação de zona DNS é descrito em [delegar tooAzure seu domínio DNS](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="72ee8-147">For forward lookup zones, hello process of delegating a DNS zone is described in [Delegate your domain tooAzure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="72ee8-148">A delegação para zonas de pesquisa inversa funciona Olá mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="72ee8-148">Delegation for reverse lookup zones works hello same way.</span></span> <span data-ttu-id="72ee8-149">Olá única diferença é que você precisa de servidores de nome de saudação tooconfigure com hello ISP que forneceu o intervalo de IP, em vez de seu registrador de nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="72ee8-149">hello only difference is that you need tooconfigure hello name servers with hello ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="72ee8-150">Criar um registro PTR DNS</span><span class="sxs-lookup"><span data-stu-id="72ee8-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="72ee8-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="72ee8-151">IPv4</span></span>

<span data-ttu-id="72ee8-152">Olá exemplo a seguir orienta Olá processo de criação de um registro PTR em uma zona DNS inversa no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="72ee8-152">hello following example walks you through hello process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="72ee8-153">Para outros tipos de registro e toomodify os registros existentes, consulte [registros DNS de gerenciar e conjuntos de registros usando Olá portal do Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="72ee8-153">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="72ee8-154">Na parte superior de saudação do hello **zona DNS** folha, selecione **+ registrar conjunto** tooopen Olá **Adicionar conjunto de registros** folha.</span><span class="sxs-lookup"><span data-stu-id="72ee8-154">At hello top of hello **DNS zone** blade, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

 ![Zona DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="72ee8-156">Em Olá **Adicionar conjunto de registros** folha.</span><span class="sxs-lookup"><span data-stu-id="72ee8-156">On hello **Add record set** blade.</span></span> 
1. <span data-ttu-id="72ee8-157">Selecione **PTR** do registro hello "**tipo**" menu.</span><span class="sxs-lookup"><span data-stu-id="72ee8-157">Select **PTR** from hello record "**Type**" menu.</span></span>  
1. <span data-ttu-id="72ee8-158">Olá nome do conjunto de registros de saudação para um registro PTR precisa toobe restante Olá Olá endereço IPv4 na ordem inversa.</span><span class="sxs-lookup"><span data-stu-id="72ee8-158">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv4 address in reverse order.</span></span> <span data-ttu-id="72ee8-159">Neste exemplo, hello três primeiros octetos já foram preenchidos como parte do nome da zona hello (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="72ee8-159">In this example, hello first three octets are already populated as part of hello zone name (.2.0.192).</span></span> <span data-ttu-id="72ee8-160">Portanto, apenas Olá último octeto é fornecido no campo de nome de saudação.</span><span class="sxs-lookup"><span data-stu-id="72ee8-160">Therefore, only hello last octet is supplied in hello name field.</span></span> <span data-ttu-id="72ee8-161">Por exemplo, você poderia nomear seu conjunto de registros "**15**" para um recurso cujo endereço IP é 192.0.2.15.</span><span class="sxs-lookup"><span data-stu-id="72ee8-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="72ee8-162">Em hello "**nome de domínio**", digite o nome de domínio totalmente qualificado (FQDN) saudação do recurso hello usando IP hello.</span><span class="sxs-lookup"><span data-stu-id="72ee8-162">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
1. <span data-ttu-id="72ee8-163">Selecione **Okey** na parte inferior da saudação de registro DNS Olá folha toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="72ee8-163">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

 ![adicionar conjunto de registros](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="72ee8-165">Olá, a seguir estão exemplos sobre como toocomplete essa tarefa com o PowerShell e hello AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="72ee8-165">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="72ee8-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72ee8-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="72ee8-167">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="72ee8-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="72ee8-168">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="72ee8-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="72ee8-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="72ee8-169">IPv6</span></span>

<span data-ttu-id="72ee8-170">Olá exemplo a seguir orienta você pelo processo de saudação de criar um novo registro de 'PTR'.</span><span class="sxs-lookup"><span data-stu-id="72ee8-170">hello following example walks you through hello process of creating new 'PTR' record.</span></span> <span data-ttu-id="72ee8-171">Para outros tipos de registro e toomodify os registros existentes, consulte [registros DNS de gerenciar e conjuntos de registros usando Olá portal do Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="72ee8-171">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="72ee8-172">Na parte superior de saudação do hello **folha de zona DNS**, selecione **+ registrar conjunto** tooopen Olá **Adicionar conjunto de registros** folha.</span><span class="sxs-lookup"><span data-stu-id="72ee8-172">At hello top of hello **DNS zone blade**, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

  ![folha de zona DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="72ee8-174">Em Olá **Adicionar conjunto de registros** folha.</span><span class="sxs-lookup"><span data-stu-id="72ee8-174">On hello **Add record set** blade.</span></span> 
3. <span data-ttu-id="72ee8-175">Selecione **PTR** do registro hello "**tipo**" menu.</span><span class="sxs-lookup"><span data-stu-id="72ee8-175">Select **PTR** from hello record "**Type**" menu.</span></span>  
4. <span data-ttu-id="72ee8-176">Olá nome do conjunto de registros de saudação para um registro PTR precisa toobe restante Olá Olá endereço IPv6 na ordem inversa.</span><span class="sxs-lookup"><span data-stu-id="72ee8-176">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv6 address in reverse order.</span></span> <span data-ttu-id="72ee8-177">Ele não deve incluir compactação.</span><span class="sxs-lookup"><span data-stu-id="72ee8-177">It must not include any zero compression.</span></span> <span data-ttu-id="72ee8-178">Neste exemplo, Olá primeiros 64 bits do hello IPv6 já foram preenchidos como parte do nome da zona hello (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="72ee8-178">In this example, hello first 64 bits of hello IPv6 are already populated as part of hello zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="72ee8-179">Portanto, Olá últimos 64 bits são fornecidos no campo de nome de saudação.</span><span class="sxs-lookup"><span data-stu-id="72ee8-179">Therefore, only hello last 64 bits are supplied in hello name field.</span></span> <span data-ttu-id="72ee8-180">Olá últimos 64 bits do endereço IP de saudação são inseridos na ordem inversa, usando um período como o delimitador de saudação entre cada número hexadecimal.</span><span class="sxs-lookup"><span data-stu-id="72ee8-180">hello last 64 bits of hello IP address are entered in reverse order, using a period as hello delimiter between each hexadecimal number.</span></span> <span data-ttu-id="72ee8-181">Por exemplo, você poderia nomear seu conjunto de registros "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" para um recurso cujo endereço IP é 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span><span class="sxs-lookup"><span data-stu-id="72ee8-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="72ee8-182">Em hello "**nome de domínio**", digite o nome de domínio totalmente qualificado (FQDN) saudação do recurso hello usando IP hello.</span><span class="sxs-lookup"><span data-stu-id="72ee8-182">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
6. <span data-ttu-id="72ee8-183">Selecione **Okey** na parte inferior da saudação de registro DNS Olá folha toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="72ee8-183">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

![adicionar conjunto de registros](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="72ee8-185">Olá, a seguir estão exemplos sobre como toocomplete essa tarefa com o PowerShell e hello AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="72ee8-185">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="72ee8-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72ee8-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="72ee8-187">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="72ee8-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="72ee8-188">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="72ee8-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="72ee8-189">Exibir registros</span><span class="sxs-lookup"><span data-stu-id="72ee8-189">View Records</span></span>

<span data-ttu-id="72ee8-190">registros de saudação tooview você criou, navegue tooyour zona DNS no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="72ee8-190">tooview hello records you created, navigate tooyour DNS zone in hello Azure portal.</span></span> <span data-ttu-id="72ee8-191">Em Olá diminuir parte da saudação **zona DNS** folha, você pode ver registros Olá para a zona DNS de saudação.</span><span class="sxs-lookup"><span data-stu-id="72ee8-191">In hello lower part of hello **DNS zone** blade, you can see hello records for hello DNS zone.</span></span> <span data-ttu-id="72ee8-192">Você deve ver o saudação padrão registros NS e SOA, que são criados em cada região, além de quaisquer novos registros que você criou.</span><span class="sxs-lookup"><span data-stu-id="72ee8-192">You should see hello default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="72ee8-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="72ee8-193">IPv4</span></span>

<span data-ttu-id="72ee8-194">Folha de zona DNS, mostrando os registros PTR de IPv4:</span><span class="sxs-lookup"><span data-stu-id="72ee8-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![folha de zona DNS](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="72ee8-196">Olá exemplos a seguir mostram como tooview Olá PTR registros usando o PowerShell ou Olá CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="72ee8-196">hello following examples show how tooview hello PTR records using PowerShell or hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="72ee8-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72ee8-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="72ee8-198">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="72ee8-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="72ee8-199">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="72ee8-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="72ee8-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="72ee8-200">IPv6</span></span>

<span data-ttu-id="72ee8-201">Folha de zona DNS, mostrando os registros PTR de IPv6:</span><span class="sxs-lookup"><span data-stu-id="72ee8-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![folha de zona DNS](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="72ee8-203">Olá seguem exemplos de como Olá tooview registros com o PowerShell e Olá AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="72ee8-203">hello following are examples on how tooview hello records with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="72ee8-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72ee8-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="72ee8-205">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="72ee8-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="72ee8-206">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="72ee8-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="72ee8-207">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="72ee8-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="72ee8-208">Posso hospedar zonas de pesquisa inversa de DNS para meus blocos IP atribuídos pelo ISP no DNS do Azure?</span><span class="sxs-lookup"><span data-stu-id="72ee8-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="72ee8-209">Sim.</span><span class="sxs-lookup"><span data-stu-id="72ee8-209">Yes.</span></span> <span data-ttu-id="72ee8-210">Hospedagem de zonas de pesquisa inversa (ARPA) Olá para seus próprios intervalos de IP no DNS do Azure tem suporte total.</span><span class="sxs-lookup"><span data-stu-id="72ee8-210">Hosting hello reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="72ee8-211">Criar uma zona de pesquisa inversa de Olá em DNS do Azure como explicado neste artigo, e trabalhar com seu ISP muito[delegado Olá zona](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="72ee8-211">Create hello reverse lookup zone in Azure DNS as explained in this article, then work with your ISP too[delegate hello zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="72ee8-212">Você pode gerenciar os registros PTR Olá para cada pesquisa inversa no hello mesma maneira que outros tipos de registro.</span><span class="sxs-lookup"><span data-stu-id="72ee8-212">You can then manage hello PTR records for each reverse lookup in hello same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="72ee8-213">Quanto custa hospedar minha zona de pesquisa inverso de DNS?</span><span class="sxs-lookup"><span data-stu-id="72ee8-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="72ee8-214">Zona de pesquisa DNS inversa Olá de hospedagem para o bloco IP atribuído pelo ISP no DNS do Azure é cobrado nos [taxas de DNS do Azure padrão](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="72ee8-214">Hosting hello reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="72ee8-215">Posso hospedar zonas de pesquisa inversa de DNS para endereços IPv4 e IPv6 no DNS do Azure?</span><span class="sxs-lookup"><span data-stu-id="72ee8-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="72ee8-216">Sim.</span><span class="sxs-lookup"><span data-stu-id="72ee8-216">Yes.</span></span> <span data-ttu-id="72ee8-217">Este artigo explica como toocreate IPv4 e IPv6 inverter as zonas de pesquisa DNS no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="72ee8-217">This article explains how toocreate both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="72ee8-218">Posso importar uma zona de pesquisa inversa de DNS existente?</span><span class="sxs-lookup"><span data-stu-id="72ee8-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="72ee8-219">Sim.</span><span class="sxs-lookup"><span data-stu-id="72ee8-219">Yes.</span></span> <span data-ttu-id="72ee8-220">Você pode usar o hello CLI do Azure tooimport existentes zonas do DNS no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="72ee8-220">You can use hello Azure CLI tooimport existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="72ee8-221">Isso funciona para zonas de pesquisa direta e zonas de pesquisa inversa.</span><span class="sxs-lookup"><span data-stu-id="72ee8-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="72ee8-222">Para obter mais informações, consulte [Olá importar e exportar um arquivo de zona DNS usando a CLI do Azure](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="72ee8-222">For more information, see [Import and export a DNS zone file using hello Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="72ee8-223">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="72ee8-223">Next steps</span></span>

<span data-ttu-id="72ee8-224">Para saber mais sobre DNS reverso, confira [Pesquisa de DNS reverso na Wikipédia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="72ee8-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="72ee8-225">Saiba como muito[gerenciar registros DNS reversos para os serviços do Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="72ee8-225">Learn how too[manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
