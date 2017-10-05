---
title: Gerenciar registros DNS na DNS do Azure usando o Azure PowerShell | Microsoft Docs
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
ms.openlocfilehash: 2962e30e5d9c60b8e786e2ba79647cabfc5925cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="fcfc9-104">Gerenciar registros e conjuntos de registros DNS no DNS do Azure usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fcfc9-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fcfc9-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fcfc9-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="fcfc9-106">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="fcfc9-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="fcfc9-107">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="fcfc9-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="fcfc9-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fcfc9-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="fcfc9-109">Este artigo mostra como gerenciar os registros de DNS para sua zona de DNS usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-109">This article shows you how to manage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="fcfc9-110">Os registros DNS também podem ser gerenciados usando a [CLI do Azure](dns-operations-recordsets-cli.md) da plataforma cruzada ou o [portal do Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fcfc9-110">DNS records can also be managed by using the cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="fcfc9-111">Os exemplos neste artigo pressupõem que você já [instalou o Azure PowerShell, conectou e criou uma zona DNS](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="fcfc9-111">The examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="fcfc9-112">Introdução</span><span class="sxs-lookup"><span data-stu-id="fcfc9-112">Introduction</span></span>

<span data-ttu-id="fcfc9-113">Antes de criar registros DNS no DNS do Azure, primeiro você precisa entender como o DNS do Azure organiza registros DNS em conjuntos de registros DNS.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-113">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="fcfc9-114">Para obter mais informações sobre os registros DNS no DNS do Azure, confira [Zonas e registros DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="fcfc9-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="fcfc9-115">Criar um novo registro DNS</span><span class="sxs-lookup"><span data-stu-id="fcfc9-115">Create a new DNS record</span></span>

<span data-ttu-id="fcfc9-116">Se o novo registro tem o mesmo nome e tipo de um registro existente, você precisa [adicioná-lo ao conjunto de registros existente](#add-a-record-to-an-existing-record-set).</span><span class="sxs-lookup"><span data-stu-id="fcfc9-116">If your new record has the same name and type as an existing record, you need to [add it to the existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="fcfc9-117">Se o novo registro tiver um nome e tipo diferentes para todos os registros existentes, você precisará criar um novo conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-117">If your new record has a different name and type to all existing records, you need to create a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="fcfc9-118">Criar registros 'A' em um novo conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="fcfc9-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="fcfc9-119">Você cria conjuntos de registros usando o cmdlet `New-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-119">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="fcfc9-120">Ao criar um conjunto de registros, você precisa especificar o nome do conjunto de registros, a zona, o TTL (vida útil), o tipo de registro e os registros a serem criados.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-120">When creating a record set, you need to specify the record set name, the zone, the time to live (TTL), the record type, and the records to be created.</span></span>

<span data-ttu-id="fcfc9-121">Os parâmetros para adicionar registros a um conjunto de registros variam dependendo do tipo de conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-121">The parameters for adding records to a record set vary depending on the type of the record set.</span></span> <span data-ttu-id="fcfc9-122">Por exemplo, ao usar um conjunto de registros do tipo "A", você precisa especificar o endereço IP usando o parâmetro `-IPv4Address`.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-122">For example, when using a record set of type 'A', you need to specify the IP address using the parameter `-IPv4Address`.</span></span> <span data-ttu-id="fcfc9-123">Outros parâmetros são usados para outros tipos de registro.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="fcfc9-124">Consulte [Exemplos adicionais dos tipos de registro](#additional-record-type-examples) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="fcfc9-125">O exemplo a seguir cria um conjunto de registros com o nome relativo "www" na Zona DNS "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="fcfc9-125">The following example creates a record set with the relative name 'www' in the DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="fcfc9-126">O nome totalmente qualificado do conjunto de registros é "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="fcfc9-126">The fully-qualified name of the record set is 'www.contoso.com'.</span></span> <span data-ttu-id="fcfc9-127">O tipo de registro é 'A' e o TTL é 3600 segundos.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-127">The record type is 'A', and the TTL is 3600 seconds.</span></span> <span data-ttu-id="fcfc9-128">O conjunto de registros contém um único registro, com o endereço IP "1.2.3.4".</span><span class="sxs-lookup"><span data-stu-id="fcfc9-128">The record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="fcfc9-129">Para criar um conjunto de registros no "ápice" de uma zona (neste caso, "contoso.com"), use o nome do conjunto de registros '@' (excluindo as aspas):</span><span class="sxs-lookup"><span data-stu-id="fcfc9-129">To create a record set at the 'apex' of a zone (in this case, 'contoso.com'), use the record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="fcfc9-130">Se você precisar criar um conjunto de registros contendo mais de um registro, primeiro deve criar uma matriz local e adicionar os registros e, então, passar a matriz para `New-AzureRmDnsRecordSet` como a seguir:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-130">If you need to create a record set containing more than one record, first create a local array and add the records, then pass the array to `New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="fcfc9-131">Os [metadados do conjunto de registros](dns-zones-records.md#tags-and-metadata) podem ser usados para associar os dados específicos do aplicativo com cada conjunto de registros, como pares de chave-valor.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="fcfc9-132">O exemplo a seguir mostra como criar um conjunto de registros com duas entradas de metadados, "dept=finance" e "environment=production".</span><span class="sxs-lookup"><span data-stu-id="fcfc9-132">The following example shows how to create a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="fcfc9-133">O DNS do Azure também oferece suporte a conjuntos de registros 'vazios', que podem agir como um espaço reservado para reservar um nome DNS antes de criar os registros DNS.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="fcfc9-134">Os conjuntos de registros vazios são visíveis no painel de controle do DNS do Azure, mas aparecem nos servidores de nome DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-134">Empty record sets are visible in the Azure DNS control plane, but do appear on the Azure DNS name servers.</span></span> <span data-ttu-id="fcfc9-135">O exemplo a seguir cria um conjunto de registros vazio:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-135">The following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="fcfc9-136">Criar outros tipos de registro</span><span class="sxs-lookup"><span data-stu-id="fcfc9-136">Create records of other types</span></span>

<span data-ttu-id="fcfc9-137">Depois de ter visto detalhadamente como criar os registros 'A', os exemplos a seguir mostram como criar outros tipos de registro suportados pelo DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-137">Having seen in detail how to create 'A' records, the following examples show how to create records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="fcfc9-138">Em cada caso, mostraremos como criar um conjunto de registro que contém um único registro.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-138">In each case, we show how to create a record set containing a single record.</span></span> <span data-ttu-id="fcfc9-139">Os exemplos anteriores dos registros 'A' podem ser adaptados para criar outros tipos de conjuntos de registros que contêm vários registros, com metadados ou criar conjuntos de registros vazios.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-139">The earlier examples for 'A' records can be adapted to create record sets of other types containing multiple records, with metadata, or to create empty record sets.</span></span>

<span data-ttu-id="fcfc9-140">Não podemos dar um exemplo para criar um conjunto de registros SOA, pois os SOAs são criados e excluídos com cada zona DNS e não podem ser criados ou excluídos separadamente.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-140">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="fcfc9-141">No entanto, [o SOA pode ser modificado, como mostrado no exemplo mais adiante](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="fcfc9-141">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="fcfc9-142">Criar um conjunto de registros AAAA com um registro único</span><span class="sxs-lookup"><span data-stu-id="fcfc9-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="fcfc9-143">Criar um conjunto de registros CNAME com um registro único</span><span class="sxs-lookup"><span data-stu-id="fcfc9-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="fcfc9-144">Os padrões do DNS não permitem registros CNAME no ápice de uma zona (`-Name '@'`), nem permitem conjuntos de registros que contêm mais de um registro.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-144">The DNS standards do not permit CNAME records at the apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="fcfc9-145">Para obter mais informações, consulte [Registros CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="fcfc9-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="fcfc9-146">Criar um conjunto de registros MX com um registro único</span><span class="sxs-lookup"><span data-stu-id="fcfc9-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="fcfc9-147">Neste exemplo, usamos o nome do conjunto de registros '@' para criar um registro MX no ápice da zona (nesse caso, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="fcfc9-147">In this example, we use the record set name '@' to create an MX record at the zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="fcfc9-148">Criar um conjunto de registros NS com um registro único</span><span class="sxs-lookup"><span data-stu-id="fcfc9-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="fcfc9-149">Criar um conjunto de registros PTR com um único registro</span><span class="sxs-lookup"><span data-stu-id="fcfc9-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="fcfc9-150">Neste caso, 'my-arpa-zone.com' representa a zona de pesquisa inversa ARPA que apresenta o intervalo de IPs.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-150">In this case, 'my-arpa-zone.com' represents the ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="fcfc9-151">Cada registro PTR definido nesta zona corresponde a um endereço IP nesse intervalo de IP.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-151">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span> <span data-ttu-id="fcfc9-152">O nome do registro '10' é o último octeto do endereço IP dentro desse intervalo IP representado por esse registro.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-152">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="fcfc9-153">Criar um conjunto de registros SRV com um registro único</span><span class="sxs-lookup"><span data-stu-id="fcfc9-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="fcfc9-154">Ao criar um [conjunto de registros SRV](dns-zones-records.md#srv-records), especifique o *\_serviço* e o *\_protocolo* no nome do conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="fcfc9-155">Não é necessário incluir '@' no nome do conjunto de registros ao criar um conjunto de registros SRV definido no ápice da zona.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-155">There is no need to include '@' in the record set name when creating an SRV record set at the zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="fcfc9-156">Criar um conjunto de registros TXT com um registro único</span><span class="sxs-lookup"><span data-stu-id="fcfc9-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="fcfc9-157">O exemplo a seguir mostra como criar um registro TXT.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-157">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="fcfc9-158">Para obter mais informações sobre o tamanho máximo suportado pelos registros TXT, consulte [Registros TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="fcfc9-158">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="fcfc9-159">Obter um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="fcfc9-159">Get a record set</span></span>

<span data-ttu-id="fcfc9-160">Para recuperar um conjunto de registros existente, use `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-160">To retrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="fcfc9-161">Esse cmdlet retorna um objeto local que representa o conjunto de registros no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-161">This cmdlet returns a local object that represents the record set in Azure DNS.</span></span>

<span data-ttu-id="fcfc9-162">Assim como acontece com `New-AzureRmDnsRecordSet`, o nome do conjunto de registros fornecido deve ser um nome *relativo*, significando que ele deve excluir o nome da zona.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-162">As with `New-AzureRmDnsRecordSet`, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="fcfc9-163">Você também precisa especificar o tipo de registro e a zona que contém o conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-163">You also need to specify the record type, and the zone containing the record set.</span></span>

<span data-ttu-id="fcfc9-164">O exemplo a seguir mostra como recuperar um conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-164">The following example shows how to retrieve a record set.</span></span> <span data-ttu-id="fcfc9-165">Neste exemplo, a zona é especificada usando os parâmetros `-ZoneName` e `-ResourceGroupName`.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-165">In this example, the zone is specified using the `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="fcfc9-166">Como alternativa, você também pode especificar a zona usando um objeto de zona, passado usando o parâmetro `-Zone`.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-166">Alternatively, you can also specify the zone using a zone object, passed using the `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="fcfc9-167">Listar os conjuntos de registros</span><span class="sxs-lookup"><span data-stu-id="fcfc9-167">List record sets</span></span>

<span data-ttu-id="fcfc9-168">Você também pode usar `Get-AzureRmDnsZone` para listar os conjuntos de registros em uma zona, omitindo os parâmetros `-Name` e/ou `-RecordType`.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-168">You can also use `Get-AzureRmDnsZone` to list record sets in a zone, by omitting the `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="fcfc9-169">O exemplo a seguir retorna todos os conjuntos de registro na zona:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-169">The following example returns all record sets in the zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="fcfc9-170">O exemplo a seguir mostra como todos os conjuntos de registro de um determinado tipo podem ser recuperados especificando o tipo de registro ao omitir o nome do conjunto de registros:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-170">The following example shows how all record sets of a given type can be retrieved by specifying the record type while omitting the record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="fcfc9-171">Para recuperar todos os conjuntos de registro com um determinado nome, em todos os tipos de registro, você precisa recuperar todos os conjuntos de registros, em seguida, filtrar os resultados:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-171">To retrieve all record sets with a given name, across record types, you need to retrieve all record sets and then filter the results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="fcfc9-172">Em todos os exemplos acima, a zona pode ser especificada usando os parâmetros `-ZoneName` e `-ResourceGroupName` (como mostrado) ou especificando um objeto da zona:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-172">In all the above examples, the zone can be specified either by using the `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="fcfc9-173">Adicionar um registro a um conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="fcfc9-173">Add a record to an existing record set</span></span>

<span data-ttu-id="fcfc9-174">Para adicionar um registro a um conjunto de registros existente, siga estas três etapas:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-174">To add a record to an existing record set, follow the following three steps:</span></span>

1. <span data-ttu-id="fcfc9-175">Obter o conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="fcfc9-175">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="fcfc9-176">Adicione o novo registro ao conjunto de registros local.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-176">Add the new record to the local record set.</span></span> <span data-ttu-id="fcfc9-177">Esta é uma operação offline.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="fcfc9-178">Confirme a mudança no serviço DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-178">Commit the change back to the Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="fcfc9-179">Usar `Set-AzureRmDnsRecordSet` *substitui* o conjunto de registros existente no DNS do Azure (e todos os registros que ele contém) pelo conjunto de registros especificado.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-179">Using `Set-AzureRmDnsRecordSet` *replaces* the existing record set in Azure DNS (and all records it contains) with the record set specified.</span></span> <span data-ttu-id="fcfc9-180">As [verificações de Etag](dns-zones-records.md#etags) são usadas para garantir que as alterações simultâneas não sejam substituídas.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-180">[Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="fcfc9-181">Você pode usar o argumento `-Overwrite` opcional para omitir essas verificações.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-181">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="fcfc9-182">Esta sequência de operações também pode ser *redirecionada*, significando que você passa o objeto do conjunto de registros usando a barra vertical, em vez de passá-lo como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-182">This sequence of operations can also be *piped*, meaning you pass the record set object by using the pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="fcfc9-183">Os exemplos acima mostram como adicionar um registro 'A' a um conjunto de registros existente do tipo 'A'.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-183">The examples above show how to add an 'A' record to an existing record set of type 'A'.</span></span> <span data-ttu-id="fcfc9-184">Uma sequência de operações parecida é usada para adicionar registros a outros tipos de conjuntos de registro, substituindo o parâmetro `-Ipv4Address` de `Add-AzureRmDnsRecordConfig` por outros parâmetros específicos para cada tipo de registro.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-184">A similar sequence of operations is used to add records to record sets of other types, substituting the `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific to each record type.</span></span> <span data-ttu-id="fcfc9-185">Os parâmetros para cada tipo de registro são iguais para o cmdlet `New-AzureRmDnsRecordConfig`, como mostrado em [Exemplos adicionais dos tipos de registro](#additional-record-type-examples) acima.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-185">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="fcfc9-186">Os conjuntos de registro do tipo 'CNAME' ou 'SOA' não podem conter mais de um registro.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="fcfc9-187">Essa restrição resulta dos padrões do DNS.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-187">This constraint arises from the DNS standards.</span></span> <span data-ttu-id="fcfc9-188">Não é uma limitação do DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="fcfc9-189">Remover um registro em um conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="fcfc9-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="fcfc9-190">O processo para remover um registro de um conjunto de registros é semelhante ao processo para adicionar um registro a um conjunto de registros existente:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-190">The process to remove a record from a record set is similar to the process to add a record to an existing record set:</span></span>

1. <span data-ttu-id="fcfc9-191">Obter o conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="fcfc9-191">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="fcfc9-192">Remova o registro do objeto do conjunto de registros local.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-192">Remove the record from the local record set object.</span></span> <span data-ttu-id="fcfc9-193">Esta é uma operação offline.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-193">This is an off-line operation.</span></span> <span data-ttu-id="fcfc9-194">O registro que está sendo removido deve ser uma correspondência exata com um registro existente, em todos os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-194">The record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="fcfc9-195">Confirme a mudança no serviço DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-195">Commit the change back to the Azure DNS service.</span></span> <span data-ttu-id="fcfc9-196">Use o argumento opcional `-Overwrite` para omitir as [verificações de Etag](dns-zones-records.md#etags) das alterações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-196">Use the optional `-Overwrite` switch to suppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="fcfc9-197">Usar a sequência acima para remover o último registro de um conjunto de registros não exclui o conjunto de registros, ao contrário, deixa um conjunto de registros vazio.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-197">Using the above sequence to remove the last record from a record set does not delete the record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="fcfc9-198">Para remover totalmente um conjunto de registros, consulte [Excluir um conjunto de registros](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="fcfc9-198">To remove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="fcfc9-199">Da mesma forma para adicionar registros a um conjunto de registros, a sequência de operações para remover um conjunto de registros também pode ser redirecionada:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-199">Similarly to adding records to a record set, the sequence of operations to remove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="fcfc9-200">Diferentes tipos de registro são suportados passando os parâmetros específicos do tipo apropriados para `Remove-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-200">Different record types are supported by passing the appropriate type-specific parameters to `Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="fcfc9-201">Os parâmetros para cada tipo de registro são iguais para o cmdlet `New-AzureRmDnsRecordConfig`, como mostrado em [Exemplos adicionais dos tipos de registro](#additional-record-type-examples) acima.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-201">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="fcfc9-202">Modificar um conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="fcfc9-202">Modify an existing record set</span></span>

<span data-ttu-id="fcfc9-203">As etapas para modificar um conjunto de registros existente são semelhantes às etapas realizadas ao adicionar ou remover os registros de um conjunto de registros:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-203">The steps for modifying an existing record set are similar to the steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="fcfc9-204">Recupere o conjunto de registros existente usando `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-204">Retrieve the existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="fcfc9-205">Modifique o objeto do conjunto de registros local:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-205">Modify the local record set object by:</span></span>
    * <span data-ttu-id="fcfc9-206">adicionando ou removendo os registros</span><span class="sxs-lookup"><span data-stu-id="fcfc9-206">Adding or removing records</span></span>
    * <span data-ttu-id="fcfc9-207">alterando os parâmetros dos registros existentes</span><span class="sxs-lookup"><span data-stu-id="fcfc9-207">Changing the parameters of existing records</span></span>
    * <span data-ttu-id="fcfc9-208">alterando os metadados do conjunto de registros e a vida útil (TTL)</span><span class="sxs-lookup"><span data-stu-id="fcfc9-208">Changing the record set metadata and time to live (TTL)</span></span>
3. <span data-ttu-id="fcfc9-209">Confirme as alterações usando o cmdlet `Set-AzureRmDnsRecordSet` .</span><span class="sxs-lookup"><span data-stu-id="fcfc9-209">Commit your changes by using the `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="fcfc9-210">Isso *substitui* o conjunto de registros existente no DNS do Azure pelo conjunto de registros especificado.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-210">This *replaces* the existing record set in Azure DNS with the record set specified.</span></span>

<span data-ttu-id="fcfc9-211">Ao usar `Set-AzureRmDnsRecordSet`, as [verificações de Etag](dns-zones-records.md#etags) são usadas para garantir que as alterações simultâneas não sejam substituídas.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="fcfc9-212">Você pode usar o argumento `-Overwrite` opcional para omitir essas verificações.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-212">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

### <a name="to-update-a-record-in-an-existing-record-set"></a><span data-ttu-id="fcfc9-213">Para atualizar um registro em um conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="fcfc9-213">To update a record in an existing record set</span></span>

<span data-ttu-id="fcfc9-214">Neste exemplo, alteramos o endereço IP de um registro "A" existente:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-214">In this example, we change the IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="fcfc9-215">Para modificar um registro SOA</span><span class="sxs-lookup"><span data-stu-id="fcfc9-215">To modify an SOA record</span></span>

<span data-ttu-id="fcfc9-216">Não é possível adicionar nem remover registros do conjunto de registros SOA criado automaticamente no ápice da zona (`-Name "@"`, incluindo as aspas).</span><span class="sxs-lookup"><span data-stu-id="fcfc9-216">You cannot add or remove records from the automatically created SOA record set at the zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="fcfc9-217">No entanto, é possível modificar qualquer um dos parâmetros no registro SOA (exceto o “Host”) e o TTL do conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-217">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

<span data-ttu-id="fcfc9-218">O exemplo a seguir mostra como alterar a propriedade *Email* do registro SOA:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-218">The following example shows how to change the *Email* property of the SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="fcfc9-219">Para modificar registros NS no apex da zona</span><span class="sxs-lookup"><span data-stu-id="fcfc9-219">To modify NS records at the zone apex</span></span>

<span data-ttu-id="fcfc9-220">O registro NS definido no apex da zona é criado automaticamente com cada zona DNS.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-220">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="fcfc9-221">Ele contém os nomes dos servidores de nome DNS do Azure atribuídos à zona.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-221">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="fcfc9-222">Você pode adicionar servidores de nome adicionais a esse conjunto de registros NS para dar suporte à co-hospedagem de domínios com mais de um provedor DNS.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-222">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="fcfc9-223">Você também pode modificar o TTL e os metadados para esse conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-223">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="fcfc9-224">No entanto, você não pode remover nem modificar os servidores de nome DNS do Azure previamente populados.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-224">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="fcfc9-225">Observe que isso se aplica somente ao conjunto de registros NS definido no apex da zona.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-225">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="fcfc9-226">Outros conjuntos de registros NS na sua zona (conforme utilizados para delegar zonas filho) podem ser modificados sem restrição.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-226">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="fcfc9-227">O exemplo a seguir mostra como adicionar um servidor de nome adicional ao conjunto de registros NS no apex da zona:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-227">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-record-set-metadata"></a><span data-ttu-id="fcfc9-228">Para modificar os metadados do conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="fcfc9-228">To modify record set metadata</span></span>

<span data-ttu-id="fcfc9-229">Os [metadados do conjunto de registros](dns-zones-records.md#tags-and-metadata) podem ser usados para associar os dados específicos do aplicativo com cada conjunto de registros, como pares de chave-valor.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="fcfc9-230">O exemplo a seguir mostra como modificar os metadados de um conjunto de registros existente:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-230">The following example shows how to modify the metadata of an existing record set:</span></span>

```powershell
# Get the record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="fcfc9-231">Excluir um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="fcfc9-231">Delete a record set</span></span>

<span data-ttu-id="fcfc9-232">Os conjuntos de registros podem ser excluídos usando o cmdlet `Remove-AzureRmDnsRecordSet` .</span><span class="sxs-lookup"><span data-stu-id="fcfc9-232">Record sets can be deleted by using the `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="fcfc9-233">Excluir um conjunto de registros também exclui todos os registros no conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-233">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="fcfc9-234">Não é possível excluir os conjuntos de registro SOA e NS no ápice da zona (`-Name '@'`).</span><span class="sxs-lookup"><span data-stu-id="fcfc9-234">You cannot delete the SOA and NS record sets at the zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="fcfc9-235">O DNS do Azure foi criado automaticamente quando a zona foi criada e é excluído automaticamente quando a zona é excluída.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-235">Azure DNS created these automatically when the zone was created, and deletes them automatically when the zone is deleted.</span></span>

<span data-ttu-id="fcfc9-236">O exemplo a seguir mostra como excluir um conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-236">The following example shows how to delete a record set.</span></span> <span data-ttu-id="fcfc9-237">Neste exemplo, o nome do conjunto de registros, tipo, nome da zona e grupo de recursos são especificados explicitamente.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-237">In this example, the record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="fcfc9-238">Como alternativa, o conjunto de registros pode ser especificado pelo nome e tipo, e a zona é especificada usando um objeto:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-238">Alternatively, the record set can be specified by name and type, and the zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="fcfc9-239">Como uma terceira opção, o próprio conjunto de registros pode ser especificado usando um objeto do conjunto de registros:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-239">As a third option, the record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="fcfc9-240">Quando você especifica o conjunto de registros a ser excluído usando um objeto do conjunto de registros,as [verificações de Etag](dns-zones-records.md#etags) são usadas para garantir que as alterações simultâneas não sejam excluídas.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-240">When you specify the record set to be deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="fcfc9-241">Você pode usar o argumento `-Overwrite` opcional para omitir essas verificações.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-241">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="fcfc9-242">O objeto do conjunto de registros também pode ser redirecionado em vez de ser passado como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="fcfc9-242">The record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="fcfc9-243">Prompts de confirmação</span><span class="sxs-lookup"><span data-stu-id="fcfc9-243">Confirmation prompts</span></span>

<span data-ttu-id="fcfc9-244">Os cmdlets `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet` e `Remove-AzureRmDnsRecordSet` oferecem suporte aos prompts de confirmação.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-244">The `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="fcfc9-245">Cada cmdlet solicita confirmação caso a variável de preferência do PowerShell `$ConfirmPreference` tenha um valor `Medium` ou inferior.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-245">Each cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="fcfc9-246">Como o valor padrão para `$ConfirmPreference` é `High`, esses prompts não são fornecidos ao usar as configurações padrão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-246">Since the default value for `$ConfirmPreference` is `High`, these prompts are not given when using the default PowerShell settings.</span></span>

<span data-ttu-id="fcfc9-247">Você pode substituir a configuração `$ConfirmPreference` atual usando o parâmetro `-Confirm`.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-247">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="fcfc9-248">Se você especificar `-Confirm` ou `-Confirm:$True`, o cmdlet solicitará uma confirmação antes de executar.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-248">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="fcfc9-249">Se você especificar `-Confirm:$False`, o cmdlet não solicitará uma confirmação.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-249">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="fcfc9-250">Para obter mais informações sobre `-Confirm` e `$ConfirmPreference`, consulte [Sobre as Variáveis de Preferência](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="fcfc9-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcfc9-251">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fcfc9-251">Next steps</span></span>

<span data-ttu-id="fcfc9-252">Saiba mais sobre as [zonas e os registros no DNS do Azure](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="fcfc9-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="fcfc9-253">Saiba como [proteger seus registros e zonas](dns-protect-zones-recordsets.md) ao usar o DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfc9-253">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="fcfc9-254">Examine a [documentação de referência do PowerShell do DNS do Azure](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="fcfc9-254">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
