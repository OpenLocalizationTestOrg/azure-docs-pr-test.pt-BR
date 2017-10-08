---
title: aaaManage DNS de registros no DNS do Azure usando o Azure PowerShell | Microsoft Docs
description: "Gerenciando conjuntos de registros DNS e registros no DNS do Azure ao hospedar seu domínio no DNS do Azure. Todos os comandos do PowerShell para operações em conjuntos de registros e registros."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="691cc-104">Gerenciar registros e conjuntos de registros DNS no DNS do Azure usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="691cc-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="691cc-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="691cc-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="691cc-106">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="691cc-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="691cc-107">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="691cc-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="691cc-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="691cc-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="691cc-109">Este artigo mostra como toomanage DNS registros para a zona DNS usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="691cc-109">This article shows you how toomanage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="691cc-110">Registros DNS também podem ser gerenciados por meio de plataforma cruzada Olá [CLI do Azure](dns-operations-recordsets-cli.md) ou hello [portal do Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="691cc-110">DNS records can also be managed by using hello cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="691cc-111">exemplos de saudação neste artigo presumem que você já tiver [instalado Azure PowerShell, conectado e criar uma zona DNS](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="691cc-111">hello examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="691cc-112">Introdução</span><span class="sxs-lookup"><span data-stu-id="691cc-112">Introduction</span></span>

<span data-ttu-id="691cc-113">Antes de criar os registros DNS no DNS do Azure, primeiro é necessário toounderstand como o DNS do Azure organiza os registros DNS em conjuntos de registros de DNS.</span><span class="sxs-lookup"><span data-stu-id="691cc-113">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="691cc-114">Para obter mais informações sobre os registros DNS no DNS do Azure, confira [Zonas e registros DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="691cc-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="691cc-115">Criar um novo registro DNS</span><span class="sxs-lookup"><span data-stu-id="691cc-115">Create a new DNS record</span></span>

<span data-ttu-id="691cc-116">Se o novo registro tiver Olá mesmo nome e tipo como um registro existente, será necessário muito[adicioná-lo o conjunto de registros existentes toohello](#add-a-record-to-an-existing-record-set).</span><span class="sxs-lookup"><span data-stu-id="691cc-116">If your new record has hello same name and type as an existing record, you need too[add it toohello existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="691cc-117">Se o novo registro tem um tooall diferente do nome e tipo de registros existentes, será necessário toocreate um novo conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="691cc-117">If your new record has a different name and type tooall existing records, you need toocreate a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="691cc-118">Criar registros 'A' em um novo conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="691cc-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="691cc-119">Criar conjuntos de registros usando Olá `New-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="691cc-119">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="691cc-120">Ao criar um conjunto de registros, é necessário toospecify nome de conjunto de registros de hello, zona hello, tempo de saudação toolive (TTL), o tipo de registro hello e Olá registros toobe criados.</span><span class="sxs-lookup"><span data-stu-id="691cc-120">When creating a record set, you need toospecify hello record set name, hello zone, hello time toolive (TTL), hello record type, and hello records toobe created.</span></span>

<span data-ttu-id="691cc-121">parâmetros de saudação para adicionar o conjunto de registros de tooa registros variam dependendo do tipo de saudação do conjunto de registros de saudação.</span><span class="sxs-lookup"><span data-stu-id="691cc-121">hello parameters for adding records tooa record set vary depending on hello type of hello record set.</span></span> <span data-ttu-id="691cc-122">Por exemplo, ao usar um conjunto de registros do tipo 'A', você precisa toospecify Olá IP endereço usando o parâmetro hello `-IPv4Address`.</span><span class="sxs-lookup"><span data-stu-id="691cc-122">For example, when using a record set of type 'A', you need toospecify hello IP address using hello parameter `-IPv4Address`.</span></span> <span data-ttu-id="691cc-123">Outros parâmetros são usados para outros tipos de registro.</span><span class="sxs-lookup"><span data-stu-id="691cc-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="691cc-124">Consulte [Exemplos adicionais dos tipos de registro](#additional-record-type-examples) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="691cc-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="691cc-125">Olá, exemplo a seguir cria um conjunto de registros com o nome relativo do hello "www" hello zona DNS 'contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="691cc-125">hello following example creates a record set with hello relative name 'www' in hello DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="691cc-126">nome totalmente qualificado de saudação do conjunto de registros de saudação é 'www.contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="691cc-126">hello fully-qualified name of hello record set is 'www.contoso.com'.</span></span> <span data-ttu-id="691cc-127">tipo de registro de saudação é 'A' e Olá TTL é 3600 segundos.</span><span class="sxs-lookup"><span data-stu-id="691cc-127">hello record type is 'A', and hello TTL is 3600 seconds.</span></span> <span data-ttu-id="691cc-128">conjunto de registros de saudação contém um único registro com o endereço IP '1.2.3.4'.</span><span class="sxs-lookup"><span data-stu-id="691cc-128">hello record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="691cc-129">toocreate um conjunto de registros no ápice de uma zona de saudação (nesse caso, "contoso.com"), use o nome de conjunto de registros Olá ' @' (excluindo as aspas):</span><span class="sxs-lookup"><span data-stu-id="691cc-129">toocreate a record set at hello 'apex' of a zone (in this case, 'contoso.com'), use hello record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="691cc-130">Se você precisar de um conjunto de registros que contém mais de um registro de toocreate, primeiro crie uma matriz de local e adicionar registros de saudação, passar a matriz de saudação muito`New-AzureRmDnsRecordSet` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="691cc-130">If you need toocreate a record set containing more than one record, first create a local array and add hello records, then pass hello array too`New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="691cc-131">[Metadados de conjunto de registros](dns-zones-records.md#tags-and-metadata) podem ser dados específicos do aplicativo de tooassociate usado com cada conjunto de registros, como pares chave-valor.</span><span class="sxs-lookup"><span data-stu-id="691cc-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="691cc-132">Olá exemplo a seguir mostra como toocreate um conjunto de registros com duas entradas de metadados, ' departamento = Finanças ' e ' ambiente = produção '.</span><span class="sxs-lookup"><span data-stu-id="691cc-132">hello following example shows how toocreate a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="691cc-133">DNS do Azure também oferece suporte a conjuntos de registros 'empty', que podem agir como um espaço reservado tooreserve um nome DNS antes de criar registros DNS.</span><span class="sxs-lookup"><span data-stu-id="691cc-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="691cc-134">Conjuntos de registros vazios são visíveis no plano de controle de DNS do Azure hello, mas aparecem em servidores de nome DNS do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="691cc-134">Empty record sets are visible in hello Azure DNS control plane, but do appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="691cc-135">saudação de exemplo a seguir cria um conjunto vazio de registro:</span><span class="sxs-lookup"><span data-stu-id="691cc-135">hello following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="691cc-136">Criar outros tipos de registro</span><span class="sxs-lookup"><span data-stu-id="691cc-136">Create records of other types</span></span>

<span data-ttu-id="691cc-137">Depois de ter visto em detalhes como registros toocreate 'A', Olá seguintes exemplos mostram como toocreate registros de outros registram tipos suportados pelo DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="691cc-137">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="691cc-138">Em cada caso, mostramos como toocreate um registro de conjunto que contém um único registro.</span><span class="sxs-lookup"><span data-stu-id="691cc-138">In each case, we show how toocreate a record set containing a single record.</span></span> <span data-ttu-id="691cc-139">Hello exemplos anteriores para 'A' registros podem ser adaptada toocreate conjuntos de registros de outros tipos que contém vários registros, com metadados, ou conjuntos de registros de toocreate vazio.</span><span class="sxs-lookup"><span data-stu-id="691cc-139">hello earlier examples for 'A' records can be adapted toocreate record sets of other types containing multiple records, with metadata, or toocreate empty record sets.</span></span>

<span data-ttu-id="691cc-140">Não fornecemos um exemplo toocreate um conjunto de registros SOA, como SOAs são criados e excluídos com cada zona DNS e não pode ser criado ou excluído separadamente.</span><span class="sxs-lookup"><span data-stu-id="691cc-140">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="691cc-141">No entanto, [Olá SOA pode ser modificado, conforme mostrado no exemplo mais adiante](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="691cc-141">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="691cc-142">Criar um conjunto de registros AAAA com um registro único</span><span class="sxs-lookup"><span data-stu-id="691cc-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="691cc-143">Criar um conjunto de registros CNAME com um registro único</span><span class="sxs-lookup"><span data-stu-id="691cc-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="691cc-144">padrões DNS Olá não permitem que os registros CNAME no ápice da saudação de uma zona (`-Name '@'`), nem eles permitem que os conjuntos de registro que contém mais de um registro.</span><span class="sxs-lookup"><span data-stu-id="691cc-144">hello DNS standards do not permit CNAME records at hello apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="691cc-145">Para obter mais informações, consulte [Registros CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="691cc-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="691cc-146">Criar um conjunto de registros MX com um registro único</span><span class="sxs-lookup"><span data-stu-id="691cc-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="691cc-147">Neste exemplo, podemos usar o nome do conjunto de registros de saudação ' @' registro de toocreate um MX no ápice da zona de saudação (nesse caso, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="691cc-147">In this example, we use hello record set name '@' toocreate an MX record at hello zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="691cc-148">Criar um conjunto de registros NS com um registro único</span><span class="sxs-lookup"><span data-stu-id="691cc-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="691cc-149">Criar um conjunto de registros PTR com um único registro</span><span class="sxs-lookup"><span data-stu-id="691cc-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="691cc-150">Nesse caso, ' Meu-arpa-zone.com' representa Olá zona de pesquisa inversa ARPA que representa o intervalo de IP.</span><span class="sxs-lookup"><span data-stu-id="691cc-150">In this case, 'my-arpa-zone.com' represents hello ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="691cc-151">Cada registro PTR definido nesta zona corresponde endereço IP tooan dentro desse intervalo IP.</span><span class="sxs-lookup"><span data-stu-id="691cc-151">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span> <span data-ttu-id="691cc-152">nome do registro Olá '10' é último octeto saudação do endereço IP hello dentro desse intervalo IP representado por esse registro.</span><span class="sxs-lookup"><span data-stu-id="691cc-152">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="691cc-153">Criar um conjunto de registros SRV com um registro único</span><span class="sxs-lookup"><span data-stu-id="691cc-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="691cc-154">Ao criar um [conjunto de registros SRV](dns-zones-records.md#srv-records), especificar Olá  *\_service* e  *\_protocolo* em Olá nome de conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="691cc-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="691cc-155">Não há nenhuma necessidade tooinclude ' @' na Olá registro de nome do conjunto de quando criar um registro SRV definida no ápice da zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="691cc-155">There is no need tooinclude '@' in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="691cc-156">Criar um conjunto de registros TXT com um registro único</span><span class="sxs-lookup"><span data-stu-id="691cc-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="691cc-157">Olá exemplo a seguir mostra como registrar o toocreate um TXT.</span><span class="sxs-lookup"><span data-stu-id="691cc-157">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="691cc-158">Para obter mais informações sobre Olá tamanho máximo com suporte no registros TXT, consulte [registros TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="691cc-158">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="691cc-159">Obter um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="691cc-159">Get a record set</span></span>

<span data-ttu-id="691cc-160">tooretrieve um conjunto de registros existente, use `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="691cc-160">tooretrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="691cc-161">Esse cmdlet retorna um objeto local que representa Olá conjunto de registros em DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="691cc-161">This cmdlet returns a local object that represents hello record set in Azure DNS.</span></span>

<span data-ttu-id="691cc-162">Assim como acontece com `New-AzureRmDnsRecordSet`, nome de conjunto de registros de saudação fornecido deve ser um *relativo* nome, o que significa que ele deve excluir o nome da zona hello.</span><span class="sxs-lookup"><span data-stu-id="691cc-162">As with `New-AzureRmDnsRecordSet`, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="691cc-163">Você também precisa toospecify tipo de registro de saudação e zona Olá que contém o conjunto de registros de saudação.</span><span class="sxs-lookup"><span data-stu-id="691cc-163">You also need toospecify hello record type, and hello zone containing hello record set.</span></span>

<span data-ttu-id="691cc-164">Olá exemplo a seguir mostra como tooretrieve um conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="691cc-164">hello following example shows how tooretrieve a record set.</span></span> <span data-ttu-id="691cc-165">Neste exemplo, zona Olá é especificada usando Olá `-ZoneName` e `-ResourceGroupName` parâmetros.</span><span class="sxs-lookup"><span data-stu-id="691cc-165">In this example, hello zone is specified using hello `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="691cc-166">Como alternativa, você também pode especificar zona hello usando um objeto de zona, passado usando Olá `-Zone` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="691cc-166">Alternatively, you can also specify hello zone using a zone object, passed using hello `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="691cc-167">Listar os conjuntos de registros</span><span class="sxs-lookup"><span data-stu-id="691cc-167">List record sets</span></span>

<span data-ttu-id="691cc-168">Você também pode usar `Get-AzureRmDnsZone` conjuntos de registros de toolist em uma região, omitindo Olá `-Name` e/ou `-RecordType` parâmetros.</span><span class="sxs-lookup"><span data-stu-id="691cc-168">You can also use `Get-AzureRmDnsZone` toolist record sets in a zone, by omitting hello `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="691cc-169">Olá exemplo a seguir retorna conjuntos de todos os registros na zona hello:</span><span class="sxs-lookup"><span data-stu-id="691cc-169">hello following example returns all record sets in hello zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="691cc-170">Olá exemplo a seguir mostra como todos os conjuntos de um determinado tipo de registro pode ser recuperado, especificando o tipo de registro de saudação enquanto o nome do conjunto de registro Olá a omissão:</span><span class="sxs-lookup"><span data-stu-id="691cc-170">hello following example shows how all record sets of a given type can be retrieved by specifying hello record type while omitting hello record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="691cc-171">tooretrieve conjuntos de todos os registros com um determinado nome em todos os tipos de registro, você precisa tooretrieve todos os conjuntos de registros e, em seguida, os resultados de saudação do filtro:</span><span class="sxs-lookup"><span data-stu-id="691cc-171">tooretrieve all record sets with a given name, across record types, you need tooretrieve all record sets and then filter hello results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="691cc-172">Em todos os Olá acima exemplos, zona Olá pode ser especificado usando Olá `-ZoneName` e `-ResourceGroupName`parâmetros (conforme mostrado), ou especificando um objeto de zona:</span><span class="sxs-lookup"><span data-stu-id="691cc-172">In all hello above examples, hello zone can be specified either by using hello `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="691cc-173">Adicionar um registro tooan existente de conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="691cc-173">Add a record tooan existing record set</span></span>

<span data-ttu-id="691cc-174">tooadd um registro existente do registro tooan definido, execute Olá três etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="691cc-174">tooadd a record tooan existing record set, follow hello following three steps:</span></span>

1. <span data-ttu-id="691cc-175">Obter o conjunto de registros existentes Olá</span><span class="sxs-lookup"><span data-stu-id="691cc-175">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="691cc-176">Adicione Olá novo registro toohello local conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="691cc-176">Add hello new record toohello local record set.</span></span> <span data-ttu-id="691cc-177">Esta é uma operação offline.</span><span class="sxs-lookup"><span data-stu-id="691cc-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="691cc-178">Confirme Olá de alteração voltar toohello serviço DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="691cc-178">Commit hello change back toohello Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="691cc-179">Usando `Set-AzureRmDnsRecordSet` *substitui* Olá existente conjunto de registros no DNS do Azure (e todos os registros que ele contém) com o conjunto de registros Olá especificado.</span><span class="sxs-lookup"><span data-stu-id="691cc-179">Using `Set-AzureRmDnsRecordSet` *replaces* hello existing record set in Azure DNS (and all records it contains) with hello record set specified.</span></span> <span data-ttu-id="691cc-180">[Verificações de ETag](dns-zones-records.md#etags) são usadas as alterações simultâneas de tooensure não são substituídas.</span><span class="sxs-lookup"><span data-stu-id="691cc-180">[Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="691cc-181">Você pode usar o hello opcional `-Overwrite` alternar toosuppress essas verificações.</span><span class="sxs-lookup"><span data-stu-id="691cc-181">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="691cc-182">Essa sequência de operações também pode ser *canalizados*, que significa que você passa o objeto de conjunto de registros de saudação usando o pipe de saudação em vez de passá-lo como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="691cc-182">This sequence of operations can also be *piped*, meaning you pass hello record set object by using hello pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="691cc-183">exemplos de saudação acima mostram como tooadd um registro 'A' tooan registro existente definida do tipo 'A'.</span><span class="sxs-lookup"><span data-stu-id="691cc-183">hello examples above show how tooadd an 'A' record tooan existing record set of type 'A'.</span></span> <span data-ttu-id="691cc-184">Uma sequência semelhante de operações é usado tooadd registros toorecord conjuntos de outros tipos, substituindo Olá `-Ipv4Address` parâmetro `Add-AzureRmDnsRecordConfig` com outros parâmetros de tipo de registro de tooeach específico.</span><span class="sxs-lookup"><span data-stu-id="691cc-184">A similar sequence of operations is used tooadd records toorecord sets of other types, substituting hello `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific tooeach record type.</span></span> <span data-ttu-id="691cc-185">Olá parâmetros para cada tipo de registro são Olá mesmo que para hello `New-AzureRmDnsRecordConfig` cmdlet, como mostrado no [exemplos adicionais de tipo de registro](#additional-record-type-examples) acima.</span><span class="sxs-lookup"><span data-stu-id="691cc-185">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="691cc-186">Os conjuntos de registro do tipo 'CNAME' ou 'SOA' não podem conter mais de um registro.</span><span class="sxs-lookup"><span data-stu-id="691cc-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="691cc-187">Essa restrição surge de padrões do DNS hello.</span><span class="sxs-lookup"><span data-stu-id="691cc-187">This constraint arises from hello DNS standards.</span></span> <span data-ttu-id="691cc-188">Não é uma limitação do DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="691cc-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="691cc-189">Remover um registro em um conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="691cc-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="691cc-190">Olá, processo tooremove um registro de um conjunto de registros é semelhante tooadd de processo de toohello um registro tooan existente conjunto de registro:</span><span class="sxs-lookup"><span data-stu-id="691cc-190">hello process tooremove a record from a record set is similar toohello process tooadd a record tooan existing record set:</span></span>

1. <span data-ttu-id="691cc-191">Obter o conjunto de registros existentes Olá</span><span class="sxs-lookup"><span data-stu-id="691cc-191">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="691cc-192">Remova o registro de saudação do objeto de conjunto de registros local hello.</span><span class="sxs-lookup"><span data-stu-id="691cc-192">Remove hello record from hello local record set object.</span></span> <span data-ttu-id="691cc-193">Esta é uma operação offline.</span><span class="sxs-lookup"><span data-stu-id="691cc-193">This is an off-line operation.</span></span> <span data-ttu-id="691cc-194">registro de saudação que está sendo removido deve ser uma correspondência exata com um registro existente em todos os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="691cc-194">hello record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="691cc-195">Confirme Olá de alteração voltar toohello serviço DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="691cc-195">Commit hello change back toohello Azure DNS service.</span></span> <span data-ttu-id="691cc-196">Saudação de uso opcional `-Overwrite` alternar toosuppress [Etag verifica](dns-zones-records.md#etags) alterações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="691cc-196">Use hello optional `-Overwrite` switch toosuppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="691cc-197">Usar Olá acima sequência tooremove Olá último registro de um conjunto de registros não exclui o conjunto de registros hello, em vez disso, ele sai de um conjunto de registros vazio.</span><span class="sxs-lookup"><span data-stu-id="691cc-197">Using hello above sequence tooremove hello last record from a record set does not delete hello record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="691cc-198">tooremove um conjunto de registros totalmente, consulte [excluir um conjunto de registros](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="691cc-198">tooremove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="691cc-199">Da mesma forma tooadding registros tooa registro definir, Olá sequência de operações tooremove também pode ser conectado a um conjunto de registros:</span><span class="sxs-lookup"><span data-stu-id="691cc-199">Similarly tooadding records tooa record set, hello sequence of operations tooremove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="691cc-200">Diferentes tipos de registro são suportados, passando parâmetros de tipo específico apropriados Olá muito`Remove-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="691cc-200">Different record types are supported by passing hello appropriate type-specific parameters too`Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="691cc-201">Olá parâmetros para cada tipo de registro são Olá mesmo que para hello `New-AzureRmDnsRecordConfig` cmdlet, como mostrado no [exemplos adicionais de tipo de registro](#additional-record-type-examples) acima.</span><span class="sxs-lookup"><span data-stu-id="691cc-201">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="691cc-202">Modificar um conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="691cc-202">Modify an existing record set</span></span>

<span data-ttu-id="691cc-203">Olá etapas para modificar um conjunto de registros existente são semelhantes toohello que levar ao adicionar ou remover registros de um conjunto de registros:</span><span class="sxs-lookup"><span data-stu-id="691cc-203">hello steps for modifying an existing record set are similar toohello steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="691cc-204">Recuperar Olá registro existente definido por meio de `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="691cc-204">Retrieve hello existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="691cc-205">Modificar o objeto de conjunto de registros local Olá por:</span><span class="sxs-lookup"><span data-stu-id="691cc-205">Modify hello local record set object by:</span></span>
    * <span data-ttu-id="691cc-206">adicionando ou removendo os registros</span><span class="sxs-lookup"><span data-stu-id="691cc-206">Adding or removing records</span></span>
    * <span data-ttu-id="691cc-207">Alterando os parâmetros de saudação de registros existentes</span><span class="sxs-lookup"><span data-stu-id="691cc-207">Changing hello parameters of existing records</span></span>
    * <span data-ttu-id="691cc-208">Alterando o registro de saudação do conjunto de metadados e tempo toolive (TTL)</span><span class="sxs-lookup"><span data-stu-id="691cc-208">Changing hello record set metadata and time toolive (TTL)</span></span>
3. <span data-ttu-id="691cc-209">Confirmar as alterações usando Olá `Set-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="691cc-209">Commit your changes by using hello `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="691cc-210">Isso *substitui* Olá existente conjunto de registros no DNS do Azure com o conjunto de registros Olá especificado.</span><span class="sxs-lookup"><span data-stu-id="691cc-210">This *replaces* hello existing record set in Azure DNS with hello record set specified.</span></span>

<span data-ttu-id="691cc-211">Ao usar `Set-AzureRmDnsRecordSet`, [Etag verifica](dns-zones-records.md#etags) são usadas as alterações simultâneas de tooensure não são substituídas.</span><span class="sxs-lookup"><span data-stu-id="691cc-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="691cc-212">Você pode usar o hello opcional `-Overwrite` alternar toosuppress essas verificações.</span><span class="sxs-lookup"><span data-stu-id="691cc-212">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

### <a name="tooupdate-a-record-in-an-existing-record-set"></a><span data-ttu-id="691cc-213">Definir tooupdate um registro de um registro existente</span><span class="sxs-lookup"><span data-stu-id="691cc-213">tooupdate a record in an existing record set</span></span>

<span data-ttu-id="691cc-214">Neste exemplo, podemos alterar o endereço IP de saudação de um '' registro existente:</span><span class="sxs-lookup"><span data-stu-id="691cc-214">In this example, we change hello IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="691cc-215">toomodify um registro SOA</span><span class="sxs-lookup"><span data-stu-id="691cc-215">toomodify an SOA record</span></span>

<span data-ttu-id="691cc-216">Você não pode adicionar ou remover registros da saudação criado automaticamente o registro SOA definido no ápice da zona de saudação (`-Name "@"`, incluindo as aspas).</span><span class="sxs-lookup"><span data-stu-id="691cc-216">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="691cc-217">No entanto, você pode modificar qualquer um dos parâmetros de saudação em Olá registro SOA (exceto "Host") e registro Olá definir o TTL.</span><span class="sxs-lookup"><span data-stu-id="691cc-217">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

<span data-ttu-id="691cc-218">Olá mostrado no exemplo a seguir como Olá toochange *Email* propriedade Olá registro SOA:</span><span class="sxs-lookup"><span data-stu-id="691cc-218">hello following example shows how toochange hello *Email* property of hello SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="691cc-219">toomodify NS registros no ápice da zona de saudação</span><span class="sxs-lookup"><span data-stu-id="691cc-219">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="691cc-220">registro de NS Olá definido no ápice da zona de saudação é criado automaticamente com cada zona DNS.</span><span class="sxs-lookup"><span data-stu-id="691cc-220">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="691cc-221">Ela contém nomes de saudação da zona do hello Azure DNS nome servidores toohello atribuído.</span><span class="sxs-lookup"><span data-stu-id="691cc-221">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="691cc-222">Você pode adicionar nome adicionais servidores toothis NS conjunto de registros, toosupport co-hospedagem domínios com mais de um provedor DNS.</span><span class="sxs-lookup"><span data-stu-id="691cc-222">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="691cc-223">Você também pode modificar hello TTL e metadados para esse conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="691cc-223">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="691cc-224">No entanto, você não pode remover ou modificar servidores de nome DNS do Azure preenchidos previamente hello.</span><span class="sxs-lookup"><span data-stu-id="691cc-224">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="691cc-225">Observe que isso se aplica apenas toohello NS conjunto de registros no ápice da zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="691cc-225">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="691cc-226">Outros conjuntos de registros NS na zona (como zonas de filho usado toodelegate) podem ser modificados sem restrição.</span><span class="sxs-lookup"><span data-stu-id="691cc-226">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="691cc-227">saudação de exemplo a seguir mostra como tooadd um registro NS de toohello de servidor de nome adicionais definir no ápice da zona de saudação:</span><span class="sxs-lookup"><span data-stu-id="691cc-227">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a><span data-ttu-id="691cc-228">metadados de conjunto de registros de toomodify</span><span class="sxs-lookup"><span data-stu-id="691cc-228">toomodify record set metadata</span></span>

<span data-ttu-id="691cc-229">[Metadados de conjunto de registros](dns-zones-records.md#tags-and-metadata) podem ser dados específicos do aplicativo de tooassociate usado com cada conjunto de registros, como pares chave-valor.</span><span class="sxs-lookup"><span data-stu-id="691cc-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="691cc-230">Olá exemplo a seguir mostra como definir toomodify Olá metadados de um registro existente:</span><span class="sxs-lookup"><span data-stu-id="691cc-230">hello following example shows how toomodify hello metadata of an existing record set:</span></span>

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="691cc-231">Excluir um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="691cc-231">Delete a record set</span></span>

<span data-ttu-id="691cc-232">Conjuntos de registros podem ser excluídos usando Olá `Remove-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="691cc-232">Record sets can be deleted by using hello `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="691cc-233">Excluir um conjunto de registros também exclui todos os registros no conjunto de registros de saudação.</span><span class="sxs-lookup"><span data-stu-id="691cc-233">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="691cc-234">Você não pode excluir Olá SOA e NS conjuntos de registros no ápice da zona de saudação (`-Name '@'`).</span><span class="sxs-lookup"><span data-stu-id="691cc-234">You cannot delete hello SOA and NS record sets at hello zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="691cc-235">DNS do Azure criado essas automaticamente quando Olá zona foi criada e exclui automaticamente quando Olá zona é excluída.</span><span class="sxs-lookup"><span data-stu-id="691cc-235">Azure DNS created these automatically when hello zone was created, and deletes them automatically when hello zone is deleted.</span></span>

<span data-ttu-id="691cc-236">Olá exemplo a seguir mostra como toodelete um conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="691cc-236">hello following example shows how toodelete a record set.</span></span> <span data-ttu-id="691cc-237">Neste exemplo, nome do conjunto de registros de hello, tipo de conjunto de registros, nome da zona e grupo de recursos são cada especificados explicitamente.</span><span class="sxs-lookup"><span data-stu-id="691cc-237">In this example, hello record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="691cc-238">Como alternativa, o conjunto de registros Olá pode ser especificado por nome e tipo e Olá zona especificada usando um objeto:</span><span class="sxs-lookup"><span data-stu-id="691cc-238">Alternatively, hello record set can be specified by name and type, and hello zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="691cc-239">Como uma terceira opção, o registro Olá definido pode ser especificado usando um objeto de conjunto de registros:</span><span class="sxs-lookup"><span data-stu-id="691cc-239">As a third option, hello record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="691cc-240">Quando você especifica o conjunto de registros de saudação toobe excluído usando um objeto de conjunto de registros, [Etag verifica](dns-zones-records.md#etags) são usadas as alterações simultâneas de tooensure não são excluídas.</span><span class="sxs-lookup"><span data-stu-id="691cc-240">When you specify hello record set toobe deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="691cc-241">Você pode usar o hello opcional `-Overwrite` alternar toosuppress essas verificações.</span><span class="sxs-lookup"><span data-stu-id="691cc-241">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="691cc-242">objeto de conjunto de registros de saudação também pode ser usado em vez de ser passado como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="691cc-242">hello record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="691cc-243">Prompts de confirmação</span><span class="sxs-lookup"><span data-stu-id="691cc-243">Confirmation prompts</span></span>

<span data-ttu-id="691cc-244">Olá `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, e `Remove-AzureRmDnsRecordSet` todos os cmdlets de dar suporte a solicitações de confirmação.</span><span class="sxs-lookup"><span data-stu-id="691cc-244">hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="691cc-245">Cada cmdlet solicita confirmação se hello `$ConfirmPreference` variável de preferência do PowerShell tem um valor de `Medium` ou inferior.</span><span class="sxs-lookup"><span data-stu-id="691cc-245">Each cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="691cc-246">Desde o valor padrão Olá `$ConfirmPreference` é `High`, essas solicitações não estão disponível ao usar configurações de PowerShell saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="691cc-246">Since hello default value for `$ConfirmPreference` is `High`, these prompts are not given when using hello default PowerShell settings.</span></span>

<span data-ttu-id="691cc-247">Você pode substituir o atual Olá `$ConfirmPreference` configuração usando Olá `-Confirm` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="691cc-247">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="691cc-248">Se você especificar `-Confirm` ou `-Confirm:$True` , Olá cmdlet solicita sua confirmação antes que ele é executado.</span><span class="sxs-lookup"><span data-stu-id="691cc-248">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="691cc-249">Se você especificar `-Confirm:$False` , Olá cmdlet não solicita confirmação.</span><span class="sxs-lookup"><span data-stu-id="691cc-249">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="691cc-250">Para obter mais informações sobre `-Confirm` e `$ConfirmPreference`, consulte [Sobre as Variáveis de Preferência](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="691cc-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="691cc-251">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="691cc-251">Next steps</span></span>

<span data-ttu-id="691cc-252">Saiba mais sobre as [zonas e os registros no DNS do Azure](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="691cc-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="691cc-253">Saiba como muito[proteger suas zonas e registros de](dns-protect-zones-recordsets.md) ao usar o DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="691cc-253">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="691cc-254">Saudação de revisão [documentação de referência do PowerShell do Azure DNS](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="691cc-254">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
