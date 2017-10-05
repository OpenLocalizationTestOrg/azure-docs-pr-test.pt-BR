---
title: Gerenciar registros DNS no DNS do Azure usando a CLI do Azure 1.0| Microsoft Docs
description: "Gerenciando conjuntos de registros DNS e registros no DNS do Azure ao hospedar seu domínio no DNS do Azure. Todos os comandos da CLI 1.0 para operações em conjuntos de registros e registros."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 307b327e4c04a0461e39930114eb193791cbda9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="bcd87-104">Gerenciar registros DNS no DNS do Azure usando a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="bcd87-104">Manage DNS records in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bcd87-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bcd87-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="bcd87-106">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="bcd87-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="bcd87-107">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="bcd87-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="bcd87-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bcd87-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="bcd87-109">Este artigo mostra como gerenciar registros DNS para sua zona DNS usando a CLI (interface de linha de comando) do Azure de plataforma cruzada, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="bcd87-109">This article shows you how to manage DNS records for your DNS zone by using the cross-platform Azure command-line interface (CLI), which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="bcd87-110">Você também pode gerenciar seus registros DNS usando o [Azure PowerShell](dns-operations-recordsets.md) ou o [Portal do Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bcd87-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="bcd87-111">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="bcd87-111">CLI versions to complete the task</span></span>

<span data-ttu-id="bcd87-112">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="bcd87-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="bcd87-113">[CLI do Azure 1.0](dns-operations-recordsets-cli-nodejs.md) – nossa CLI para os modelos de implantação clássico e do resource manager.</span><span class="sxs-lookup"><span data-stu-id="bcd87-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="bcd87-114">[CLI do Azure 2.0](dns-operations-recordsets-cli.md) – nossa próxima geração de CLI para o modelo de implantação do resource manager.</span><span class="sxs-lookup"><span data-stu-id="bcd87-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="bcd87-115">Os exemplos neste artigo pressupõem que você já [instalou a CLI do Azure 1.0, entrou e criou uma zona DNS](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="bcd87-115">The examples in this article assume you have already [installed the Azure CLI 1.0, signed in, and created a DNS zone](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="bcd87-116">Introdução</span><span class="sxs-lookup"><span data-stu-id="bcd87-116">Introduction</span></span>

<span data-ttu-id="bcd87-117">Antes de criar registros DNS no DNS do Azure, primeiro você precisa entender como o DNS do Azure organiza registros DNS em conjuntos de registros DNS.</span><span class="sxs-lookup"><span data-stu-id="bcd87-117">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="bcd87-118">Para obter mais informações sobre os registros DNS no DNS do Azure, confira [Zonas e registros DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="bcd87-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="bcd87-119">Criar um registro DNS</span><span class="sxs-lookup"><span data-stu-id="bcd87-119">Create a DNS record</span></span>

<span data-ttu-id="bcd87-120">Para criar um registro DNS, use o comando `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-120">To create a DNS record, use the `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="bcd87-121">Para obter ajuda, consulte `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-121">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="bcd87-122">Ao criar um registro, você precisa especificar o nome do grupo de recursos, o nome da zona, o nome do conjunto de registros, o tipo do registro e os detalhes do registro que está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="bcd87-122">When creating a record, you need to specify the resource group name, zone name, record set name, the record type, and the details of the record being created.</span></span> <span data-ttu-id="bcd87-123">O nome do conjunto de registros fornecido deve ser um nome *relativo*, significando que ele deve excluir o nome da zona.</span><span class="sxs-lookup"><span data-stu-id="bcd87-123">The record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span>

<span data-ttu-id="bcd87-124">Se o conjunto de registros não existir, este comando o criará para você.</span><span class="sxs-lookup"><span data-stu-id="bcd87-124">If the record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="bcd87-125">Se o conjunto de registros já existir, este comando adicionará o registro que você especificar para o conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="bcd87-125">If the record set already exists, this command adda the record you specify to the existing record set.</span></span>

<span data-ttu-id="bcd87-126">Se um novo conjunto de registros for criado, um TTL padrão de 3600 será usado.</span><span class="sxs-lookup"><span data-stu-id="bcd87-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="bcd87-127">Para obter instruções sobre como usar TTLs diferentes, consulte [Criar um conjunto de registros DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="bcd87-127">For instructions on how to use different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="bcd87-128">O exemplo a seguir cria um registro A chamado *www* na zona *contoso.com* no grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="bcd87-128">The following example creates an A record called *www* in the zone *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="bcd87-129">O endereço IP do registro A é *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="bcd87-129">The IP address of the A record is *1.2.3.4*.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="bcd87-130">Para criar um registro no vértice da zona (nesse caso, "contoso.com"), use o nome do registro “@”, incluindo as aspas:</span><span class="sxs-lookup"><span data-stu-id="bcd87-130">To create a record in the apex of the zone (in this case, "contoso.com"), use the record name "@", including the quotation marks:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="bcd87-131">Criar um conjunto de registros DNS</span><span class="sxs-lookup"><span data-stu-id="bcd87-131">Create a DNS record set</span></span>

<span data-ttu-id="bcd87-132">Nos exemplos acima, o registro DNS ou foi adicionado a um conjunto de registros existente ou então o conjunto de registros foi criado *implicitamente*.</span><span class="sxs-lookup"><span data-stu-id="bcd87-132">In the above examples, the DNS record was either added to an existing record set, or the record set was created *implicitly*.</span></span> <span data-ttu-id="bcd87-133">Você também pode criar o conjunto de registros *explicitamente* antes de adicionar registros a ele.</span><span class="sxs-lookup"><span data-stu-id="bcd87-133">You can also create the record set *explicitly* before adding records to it.</span></span> <span data-ttu-id="bcd87-134">O DNS do Azure também dá suporte a conjuntos de registros 'vazios', que podem agir como um espaço reservado para reservar um nome DNS antes da criação de registros DNS.</span><span class="sxs-lookup"><span data-stu-id="bcd87-134">Azure DNS supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="bcd87-135">Os conjuntos de registros vazios são visíveis no painel de controle do DNS do Azure, mas não aparecem nos servidores de nome DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd87-135">Empty record sets are visible in the Azure DNS control plane, but do not appear on the Azure DNS name servers.</span></span>

<span data-ttu-id="bcd87-136">Os conjuntos de registros são criados usando o comando `azure network dns record-set create`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-136">Record sets are created using the `azure network dns record-set create` command.</span></span> <span data-ttu-id="bcd87-137">Para obter ajuda, consulte `azure network dns record-set create -h`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-137">For help, see `azure network dns record-set create -h`.</span></span>

<span data-ttu-id="bcd87-138">Criar o registro definido explicitamente permite que você especifique propriedades do conjunto de registros como o [TTL (vida útil)](dns-zones-records.md#time-to-live) e os metadados.</span><span class="sxs-lookup"><span data-stu-id="bcd87-138">Creating the record set explicitly allows you to specify record set properties such as the [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="bcd87-139">Os [metadados do conjunto de registros](dns-zones-records.md#tags-and-metadata) podem ser usados para associar os dados específicos do aplicativo com cada conjunto de registros, como pares de chave-valor.</span><span class="sxs-lookup"><span data-stu-id="bcd87-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="bcd87-140">O exemplo a seguir cria um conjunto de registros vazio com um TTL de 60 segundos, usando o parâmetro `--ttl` (forma abreviada `-l`):</span><span class="sxs-lookup"><span data-stu-id="bcd87-140">The following example creates an empty record set with a 60-second TTL, by using the `--ttl` parameter (short form `-l`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

<span data-ttu-id="bcd87-141">O exemplo a seguir cria um conjunto de registros com duas entradas de metadados, "dept=finance" e "environment=production", pelo uso do parâmetro `--metadata` (forma abreviada `-m`):</span><span class="sxs-lookup"><span data-stu-id="bcd87-141">The following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

<span data-ttu-id="bcd87-142">Depois de criar um conjunto de registros vazio, registros podem ser adicionados usando `azure network dns record-set add-record` conforme descrito em [Criar um registro DNS](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="bcd87-142">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="bcd87-143">Criar outros tipos de registro</span><span class="sxs-lookup"><span data-stu-id="bcd87-143">Create records of other types</span></span>

<span data-ttu-id="bcd87-144">Depois de ter visto detalhadamente como criar os registros 'A', os exemplos a seguir mostram como criar registros de outros tipos, aos quais o DNS do Azure dá suporte.</span><span class="sxs-lookup"><span data-stu-id="bcd87-144">Having seen in detail how to create 'A' records, the following examples show how to create record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="bcd87-145">Os parâmetros usados para especificar os dados de registro variam dependendo do tipo de registro.</span><span class="sxs-lookup"><span data-stu-id="bcd87-145">The parameters used to specify the record data vary depending on the type of the record.</span></span> <span data-ttu-id="bcd87-146">Por exemplo, para um registro do tipo "A", você especifica o endereço IPv4 com o parâmetro `-a <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-146">For example, for a record of type "A", you specify the IPv4 address with the parameter `-a <IPv4 address>`.</span></span> <span data-ttu-id="bcd87-147">Os parâmetros para cada tipo de registro podem ser listados usando `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-147">The parameters for each record type can be listed using `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="bcd87-148">Em cada caso, mostraremos como criar um único registro.</span><span class="sxs-lookup"><span data-stu-id="bcd87-148">In each case, we show how to create a single record.</span></span> <span data-ttu-id="bcd87-149">O registro é adicionado ao conjunto de registros existente ou um conjunto de registros é criado implicitamente.</span><span class="sxs-lookup"><span data-stu-id="bcd87-149">The record is added to the existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="bcd87-150">Para obter mais informações sobre como criar conjuntos de registros e definir o parâmetro do conjunto de registros explicitamente, consulte [Criar um conjunto de registros DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="bcd87-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="bcd87-151">Não podemos dar um exemplo para criar um conjunto de registros SOA, pois os SOAs são criados e excluídos com cada zona DNS e não podem ser criados ou excluídos separadamente.</span><span class="sxs-lookup"><span data-stu-id="bcd87-151">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="bcd87-152">No entanto, [o SOA pode ser modificado, como mostrado no exemplo mais adiante](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="bcd87-152">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="bcd87-153">Criar um registro AAAA</span><span class="sxs-lookup"><span data-stu-id="bcd87-153">Create an AAAA record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="bcd87-154">Criar um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="bcd87-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="bcd87-155">Os padrões do DNS não permitem registros CNAME no ápice de uma zona (`-Name "@"`), nem permitem conjuntos de registros que contêm mais de um registro.</span><span class="sxs-lookup"><span data-stu-id="bcd87-155">The DNS standards do not permit CNAME records at the apex of a zone (`-Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="bcd87-156">Para obter mais informações, consulte [Registros CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="bcd87-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="bcd87-157">Criar um registro MX</span><span class="sxs-lookup"><span data-stu-id="bcd87-157">Create an MX record</span></span>

<span data-ttu-id="bcd87-158">Neste exemplo, usamos o nome do conjunto de registros "@" para criar o registro MX no vértice da zona (nesse caso, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="bcd87-158">In this example, we use the record set name "@" to create the MX record at the zone apex (in this case, "contoso.com").</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="bcd87-159">Criar um registro NS</span><span class="sxs-lookup"><span data-stu-id="bcd87-159">Create an NS record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="bcd87-160">Criar um registro PTR</span><span class="sxs-lookup"><span data-stu-id="bcd87-160">Create a PTR record</span></span>

<span data-ttu-id="bcd87-161">Neste caso, 'minha-zona-arpa.com' representa a zona ARPA que apresenta o intervalo de IP.</span><span class="sxs-lookup"><span data-stu-id="bcd87-161">In this case, 'my-arpa-zone.com' represents the ARPA zone representing your IP range.</span></span> <span data-ttu-id="bcd87-162">Cada registro PTR definido nesta zona corresponde a um endereço IP nesse intervalo de IP.</span><span class="sxs-lookup"><span data-stu-id="bcd87-162">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span>  <span data-ttu-id="bcd87-163">O nome do registro '10' é o último octeto do endereço IP dentro desse intervalo IP representado por esse registro.</span><span class="sxs-lookup"><span data-stu-id="bcd87-163">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a><span data-ttu-id="bcd87-164">Criar um registro SRV</span><span class="sxs-lookup"><span data-stu-id="bcd87-164">Create an SRV record</span></span>

<span data-ttu-id="bcd87-165">Ao criar um [conjunto de registros SRV](dns-zones-records.md#srv-records), especifique o *\_serviço* e o *\_protocolo* no nome do conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="bcd87-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="bcd87-166">Não é necessário incluir “@” no nome do conjunto de registros ao criar um conjunto de registros SRV definido no ápice da zona.</span><span class="sxs-lookup"><span data-stu-id="bcd87-166">There is no need to include "@" in the record set name when creating an SRV record set at the zone apex.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a><span data-ttu-id="bcd87-167">Criar um registro TXT</span><span class="sxs-lookup"><span data-stu-id="bcd87-167">Create a TXT record</span></span>

<span data-ttu-id="bcd87-168">O exemplo a seguir mostra como criar um registro TXT.</span><span class="sxs-lookup"><span data-stu-id="bcd87-168">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="bcd87-169">Para obter mais informações sobre o tamanho máximo suportado pelos registros TXT, consulte [Registros TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="bcd87-169">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="bcd87-170">Obter um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="bcd87-170">Get a record set</span></span>

<span data-ttu-id="bcd87-171">Para recuperar um conjunto de registros existente, use `azure network dns record-set show`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-171">To retrieve an existing record set, use `azure network dns record-set show`.</span></span> <span data-ttu-id="bcd87-172">Para obter ajuda, consulte `azure network dns record-set show -h`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-172">For help, see `azure network dns record-set show -h`.</span></span>

<span data-ttu-id="bcd87-173">Assim como acontece ao criar um registro ou conjunto de registros, o nome do conjunto de registros fornecido deve ser um nome *relativo*, significando que ele deve excluir o nome da zona.</span><span class="sxs-lookup"><span data-stu-id="bcd87-173">As when creating a record or record set, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="bcd87-174">Você também precisa especificar o tipo de registro, a zona que contém o conjunto de registros e o grupo de recursos que contém a zona.</span><span class="sxs-lookup"><span data-stu-id="bcd87-174">You also need to specify the record type, the zone containing the record set, and the resource group containing the zone.</span></span>

<span data-ttu-id="bcd87-175">O exemplo a seguir recupera o registro *www* de tipo A da zona *contoso.com* no grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="bcd87-175">The following example retrieves the record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a><span data-ttu-id="bcd87-176">Listar os conjuntos de registros</span><span class="sxs-lookup"><span data-stu-id="bcd87-176">List record sets</span></span>

<span data-ttu-id="bcd87-177">Você pode listar todos os registros em uma zona DNS com o comando `azure network dns record-set list` .</span><span class="sxs-lookup"><span data-stu-id="bcd87-177">You can list all records in a DNS zone by using the `azure network dns record-set list` command.</span></span> <span data-ttu-id="bcd87-178">Para obter ajuda, consulte `azure network dns record-set list -h`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-178">For help, see `azure network dns record-set list -h`.</span></span>

<span data-ttu-id="bcd87-179">Este exemplo retorna todos os conjuntos de registros na zona *contoso.com* e no grupo de recursos *MyResourceGroup*, independentemente do nome ou tipo de registro:</span><span class="sxs-lookup"><span data-stu-id="bcd87-179">This example returns all record sets in the zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

<span data-ttu-id="bcd87-180">Este exemplo retorna todos os conjuntos de registros correspondentes ao tipo de registro determinado (nesse caso, registros 'A'):</span><span class="sxs-lookup"><span data-stu-id="bcd87-180">This example returns all record sets that match the given record type (in this case, 'A' records):</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="bcd87-181">Adicionar um registro a um conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="bcd87-181">Add a record to an existing record set</span></span>

<span data-ttu-id="bcd87-182">Você pode usar `azure network dns record-set add-record` tanto para criar um registro em um novo conjunto de registros quanto para adicionar um registro a um conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="bcd87-182">You can use `azure network dns record-set add-record` both to create a record in a new record set, or to add a record to an existing record set.</span></span>

<span data-ttu-id="bcd87-183">Para obter mais informações, consulte [Criar um registro DNS](#create-a-dns-record) e [Criar registros de outros tipos](#create-records-of-other-types), acima.</span><span class="sxs-lookup"><span data-stu-id="bcd87-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="bcd87-184">Remover um registro de um conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="bcd87-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="bcd87-185">Para remover um registro DNS de um conjunto de registros existente, use `azure network dns record-set delete-record`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-185">To remove a DNS record from an existing record set, use `azure network dns record-set delete-record`.</span></span> <span data-ttu-id="bcd87-186">Para obter ajuda, consulte `azure network dns record-set delete-record -h`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-186">For help, see `azure network dns record-set delete-record -h`.</span></span>

<span data-ttu-id="bcd87-187">Esse comando exclui um registro DNS de um conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="bcd87-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="bcd87-188">Se o último registro de um conjunto de registros é excluído, o conjunto de registros em si **não** é excluído.</span><span class="sxs-lookup"><span data-stu-id="bcd87-188">If the last record in a record set is deleted, the record set itself is **not** deleted.</span></span> <span data-ttu-id="bcd87-189">Em vez disso, um conjunto de registros vazio é mantido.</span><span class="sxs-lookup"><span data-stu-id="bcd87-189">Instead, an empty record set is left.</span></span> <span data-ttu-id="bcd87-190">Para em vez disso excluir o conjunto de registros, veja [Excluir um conjunto de registros](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="bcd87-190">To delete the record set instead, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="bcd87-191">Você precisa especificar o registro a ser excluído e a zona da qual ele deve ser excluído, usando os mesmos parâmetros usados ao criar um registro usando `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-191">You need to specify the record to be deleted and the zone it should be deleted from, using the same parameters as when creating a record using `azure network dns record-set add-record`.</span></span> <span data-ttu-id="bcd87-192">Esses parâmetros são descritos em [Criar um registro DNS](#create-a-dns-record) e [Criar registros de outros tipos](#create-records-of-other-types), acima.</span><span class="sxs-lookup"><span data-stu-id="bcd87-192">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="bcd87-193">Esse comando solicita uma confirmação.</span><span class="sxs-lookup"><span data-stu-id="bcd87-193">This command prompts for confirmation.</span></span> <span data-ttu-id="bcd87-194">Esse prompt pode ser suprimido usando a opção `--quiet` (forma abreviada `-q`).</span><span class="sxs-lookup"><span data-stu-id="bcd87-194">This prompt can be suppressed using the `--quiet` switch (short form `-q`).</span></span>

<span data-ttu-id="bcd87-195">O exemplo a seguir cria um registro A com o valor '1.2.3.4' do conjunto de recursos chamado *www* na zona *contoso.com*, no grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="bcd87-195">The following example deletes the A record with value '1.2.3.4' from the record set named *www* in the zone *contoso.com*, in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="bcd87-196">O prompt de confirmação será suprimido.</span><span class="sxs-lookup"><span data-stu-id="bcd87-196">The confirmation prompt is suppressed.</span></span>

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="bcd87-197">Modificar um conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="bcd87-197">Modify an existing record set</span></span>

<span data-ttu-id="bcd87-198">Cada conjunto de registros contém um [TTL (vida útil)](dns-zones-records.md#time-to-live), [metadados](dns-zones-records.md#tags-and-metadata) e registros DNS.</span><span class="sxs-lookup"><span data-stu-id="bcd87-198">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="bcd87-199">As seções a seguir explicam como modificar cada uma dessas propriedades.</span><span class="sxs-lookup"><span data-stu-id="bcd87-199">The following sections explain how to modify each of these properties.</span></span>

### <a name="to-modify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="bcd87-200">Para modificar um registro A, AAAA, MX, NS, PTR, SRV ou TXT</span><span class="sxs-lookup"><span data-stu-id="bcd87-200">To modify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="bcd87-201">Para modificar um registro existente do tipo A, AAAA, MX, NS, PTR, SRV ou TXT, você deve primeiro adicionar um novo registro e, em seguida, excluir o registro existente.</span><span class="sxs-lookup"><span data-stu-id="bcd87-201">To modify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete the existing record.</span></span> <span data-ttu-id="bcd87-202">Para obter instruções detalhadas sobre como excluir e adicionar registros, consulte as seções anteriores deste artigo.</span><span class="sxs-lookup"><span data-stu-id="bcd87-202">For detailed instructions on how to delete and add records, see the earlier sections of this article.</span></span>

<span data-ttu-id="bcd87-203">O exemplo a seguir mostra como modificar um registro 'A', alterando o endereço IP 1.2.3.4 para o endereço IP 5.6.7.8:</span><span class="sxs-lookup"><span data-stu-id="bcd87-203">The following example shows how to modify an 'A' record, from IP address 1.2.3.4 to IP address 5.6.7.8:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="to-modify-a-cname-record"></a><span data-ttu-id="bcd87-204">Para modificar um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="bcd87-204">To modify a CNAME record</span></span>

<span data-ttu-id="bcd87-205">Para modificar um registro CNAME, use `azure network dns record-set add-record` para adicionar o novo valor de registro.</span><span class="sxs-lookup"><span data-stu-id="bcd87-205">To modify a CNAME record, use `azure network dns record-set add-record` to add the new record value.</span></span> <span data-ttu-id="bcd87-206">Ao contrário de outros tipos de registro, um conjunto de registros CNAME pode conter apenas um único registro.</span><span class="sxs-lookup"><span data-stu-id="bcd87-206">Unlike other record types, a CNAME record set can only contain a single record.</span></span> <span data-ttu-id="bcd87-207">Portanto, o registro existente é *substituído* quando o novo registro é adicionado e não precisa ser excluído separadamente.</span><span class="sxs-lookup"><span data-stu-id="bcd87-207">Therefore, the existing record is *replaced* when the new record is added, and does not need to be deleted separately.</span></span>  <span data-ttu-id="bcd87-208">Será solicitado que você aceite essa substituição.</span><span class="sxs-lookup"><span data-stu-id="bcd87-208">You will be prompted to accept this replacement.</span></span>

<span data-ttu-id="bcd87-209">O exemplo modifica o conjunto de registros CNAME *www* na zona *contoso.com*, no grupo de recursos *MyResourceGroup*, para apontar para 'www.fabrikam.net' em vez de seu valor existente:</span><span class="sxs-lookup"><span data-stu-id="bcd87-209">The example modifies the CNAME record set *www* in the zone *contoso.com*, in resource group *MyResourceGroup*, to point to 'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="bcd87-210">Para modificar um registro SOA</span><span class="sxs-lookup"><span data-stu-id="bcd87-210">To modify an SOA record</span></span>

<span data-ttu-id="bcd87-211">Use `azure network dns record-set set-soa-record` para modificar a SOA para uma zona DNS.</span><span class="sxs-lookup"><span data-stu-id="bcd87-211">Use `azure network dns record-set set-soa-record` to modify the SOA for a given DNS zone.</span></span> <span data-ttu-id="bcd87-212">Para obter ajuda, consulte `azure network dns record-set set-soa-record -h`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-212">For help, see `azure network dns record-set set-soa-record -h`.</span></span>

<span data-ttu-id="bcd87-213">O exemplo a seguir mostra como definir a propriedade 'email' do registro SOA para a zona *contoso.com*, no grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="bcd87-213">The following example shows how to set the 'email' property of the SOA record for the zone *contoso.com* in the resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="bcd87-214">Para modificar registros NS no apex da zona</span><span class="sxs-lookup"><span data-stu-id="bcd87-214">To modify NS records at the zone apex</span></span>

<span data-ttu-id="bcd87-215">O registro NS definido no apex da zona é criado automaticamente com cada zona DNS.</span><span class="sxs-lookup"><span data-stu-id="bcd87-215">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="bcd87-216">Ele contém os nomes dos servidores de nome DNS do Azure atribuídos à zona.</span><span class="sxs-lookup"><span data-stu-id="bcd87-216">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="bcd87-217">Você pode adicionar servidores de nome adicionais a esse conjunto de registros NS para dar suporte à co-hospedagem de domínios com mais de um provedor DNS.</span><span class="sxs-lookup"><span data-stu-id="bcd87-217">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="bcd87-218">Você também pode modificar o TTL e os metadados para esse conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="bcd87-218">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="bcd87-219">No entanto, você não pode remover nem modificar os servidores de nome DNS do Azure previamente populados.</span><span class="sxs-lookup"><span data-stu-id="bcd87-219">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="bcd87-220">Observe que isso se aplica somente ao conjunto de registros NS definido no apex da zona.</span><span class="sxs-lookup"><span data-stu-id="bcd87-220">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="bcd87-221">Outros conjuntos de registros NS na sua zona (conforme utilizados para delegar zonas filho) podem ser modificados sem restrição.</span><span class="sxs-lookup"><span data-stu-id="bcd87-221">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="bcd87-222">O exemplo a seguir mostra como adicionar um servidor de nome adicional ao conjunto de registros NS no apex da zona:</span><span class="sxs-lookup"><span data-stu-id="bcd87-222">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="to-modify-the-ttl-of-an-existing-record-set"></a><span data-ttu-id="bcd87-223">Para modificar o TTL de um conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="bcd87-223">To modify the TTL of an existing record set</span></span>

<span data-ttu-id="bcd87-224">Para modificar o TTL de um conjunto de registros existente, use `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-224">To modify the TTL of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="bcd87-225">Para obter ajuda, consulte `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-225">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="bcd87-226">O exemplo a seguir mostra como modificar um conjunto de registros TTL, nesse caso para 60 segundos:</span><span class="sxs-lookup"><span data-stu-id="bcd87-226">The following example shows how to modify a record set TTL, in this case to 60 seconds:</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="to-modify-the-metadata-of-an-existing-record-set"></a><span data-ttu-id="bcd87-227">Para modificar os metadados de um conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="bcd87-227">To modify the metadata of an existing record set</span></span>

<span data-ttu-id="bcd87-228">Os [metadados do conjunto de registros](dns-zones-records.md#tags-and-metadata) podem ser usados para associar os dados específicos do aplicativo com cada conjunto de registros, como pares de chave-valor.</span><span class="sxs-lookup"><span data-stu-id="bcd87-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="bcd87-229">Para modificar os metadados de um conjunto de registros existente, use `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-229">To modify the metadata of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="bcd87-230">Para obter ajuda, consulte `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-230">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="bcd87-231">O exemplo a seguir mostra como modificar um conjunto de registros com duas entradas de metadados, "dept=finance" e "environment=production", pelo uso do parâmetro `--metadata` (forma abreviada `-m`).</span><span class="sxs-lookup"><span data-stu-id="bcd87-231">The following example shows how to modify a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`).</span></span> <span data-ttu-id="bcd87-232">Observe que os metadados existentes são *substituídos* pelos valores fornecidos.</span><span class="sxs-lookup"><span data-stu-id="bcd87-232">Note that any existing metadata is *replaced* by the values given.</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a><span data-ttu-id="bcd87-233">Excluir um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="bcd87-233">Delete a record set</span></span>

<span data-ttu-id="bcd87-234">Os conjuntos de registros podem ser excluídos usando o comando `azure network dns record-set delete`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-234">Record sets can be deleted by using the `azure network dns record-set delete` command.</span></span> <span data-ttu-id="bcd87-235">Para obter ajuda, consulte `azure network dns record-set delete -h`.</span><span class="sxs-lookup"><span data-stu-id="bcd87-235">For help, see `azure network dns record-set delete -h`.</span></span> <span data-ttu-id="bcd87-236">Excluir um conjunto de registros também exclui todos os registros no conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="bcd87-236">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="bcd87-237">Não é possível excluir os conjuntos de registro SOA e NS no ápice da zona (`-Name "@"`).</span><span class="sxs-lookup"><span data-stu-id="bcd87-237">You cannot delete the SOA and NS record sets at the zone apex (`-Name "@"`).</span></span>  <span data-ttu-id="bcd87-238">Eles são criados automaticamente quando a zona foi criada e são excluídos automaticamente quando a zona é excluída.</span><span class="sxs-lookup"><span data-stu-id="bcd87-238">These are created automatically when the zone was created, and are deleted automatically when the zone is deleted.</span></span>

<span data-ttu-id="bcd87-239">O exemplo a seguir exclui o conjunto de registros chamado *www* de tipo A da zona *contoso.com* no grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="bcd87-239">The following example deletes the record set named *www* of type A from the zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

<span data-ttu-id="bcd87-240">Será solicitado que você confirme a operação de exclusão.</span><span class="sxs-lookup"><span data-stu-id="bcd87-240">You are prompted to confirm the delete operation.</span></span> <span data-ttu-id="bcd87-241">Para suprimir esse prompt, use a opção `--quiet` (forma abreviada `-q`).</span><span class="sxs-lookup"><span data-stu-id="bcd87-241">To suppress this prompt, use the `--quiet` switch (short form `-q`).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcd87-242">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bcd87-242">Next steps</span></span>

<span data-ttu-id="bcd87-243">Saiba mais sobre as [zonas e os registros no DNS do Azure](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="bcd87-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="bcd87-244">Saiba como [proteger seus registros e zonas](dns-protect-zones-recordsets.md) ao usar o DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd87-244">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
