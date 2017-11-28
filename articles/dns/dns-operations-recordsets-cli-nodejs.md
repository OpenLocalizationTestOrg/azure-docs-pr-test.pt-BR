---
title: "aaaManage registros DNS no DNS do Azure usando Olá 1.0 da CLI do Azure | Microsoft Docs"
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
ms.openlocfilehash: 1f01450b0839f712cb1d96be318766bac581fea1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-in-azure-dns-using-hello-azure-cli-10"></a><span data-ttu-id="2dd13-104">Gerenciar registros DNS no DNS do Azure usando Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2dd13-104">Manage DNS records in Azure DNS using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2dd13-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2dd13-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="2dd13-106">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="2dd13-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="2dd13-107">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="2dd13-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="2dd13-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2dd13-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="2dd13-109">Este artigo mostra como toomanage registros DNS para a zona DNS usando Olá plataforma cruzada do Azure interface de linha de comando (CLI), que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="2dd13-109">This article shows you how toomanage DNS records for your DNS zone by using hello cross-platform Azure command-line interface (CLI), which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="2dd13-110">Você também pode gerenciar seus registros DNS usando [Azure PowerShell](dns-operations-recordsets.md) ou hello [portal do Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2dd13-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="2dd13-111">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="2dd13-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="2dd13-112">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dd13-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="2dd13-113">[1.0 de CLI do Azure](dns-operations-recordsets-cli-nodejs.md) -nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de hello.</span><span class="sxs-lookup"><span data-stu-id="2dd13-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="2dd13-114">[2.0 do CLI do Azure](dns-operations-recordsets-cli.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dd13-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="2dd13-115">exemplos de saudação neste artigo presumem que você já tiver [instalado hello Azure CLI 1.0, conectado e criar uma zona DNS](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="2dd13-115">hello examples in this article assume you have already [installed hello Azure CLI 1.0, signed in, and created a DNS zone](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="2dd13-116">Introdução</span><span class="sxs-lookup"><span data-stu-id="2dd13-116">Introduction</span></span>

<span data-ttu-id="2dd13-117">Antes de criar os registros DNS no DNS do Azure, primeiro é necessário toounderstand como o DNS do Azure organiza os registros DNS em conjuntos de registros de DNS.</span><span class="sxs-lookup"><span data-stu-id="2dd13-117">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="2dd13-118">Para obter mais informações sobre os registros DNS no DNS do Azure, confira [Zonas e registros DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="2dd13-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="2dd13-119">Criar um registro DNS</span><span class="sxs-lookup"><span data-stu-id="2dd13-119">Create a DNS record</span></span>

<span data-ttu-id="2dd13-120">toocreate um registro DNS, use Olá `azure network dns record-set add-record` comando.</span><span class="sxs-lookup"><span data-stu-id="2dd13-120">toocreate a DNS record, use hello `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="2dd13-121">Para obter ajuda, consulte `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-121">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="2dd13-122">Ao criar um registro, é necessário o nome do grupo de recursos do toospecify Olá, nome da zona, conjunto de registros, nome, tipo de registro de saudação e detalhes de saudação do registro de hello está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="2dd13-122">When creating a record, you need toospecify hello resource group name, zone name, record set name, hello record type, and hello details of hello record being created.</span></span> <span data-ttu-id="2dd13-123">Olá nome do conjunto de registros fornecido deve ser um *relativo* nome, o que significa que ele deve excluir o nome da zona hello.</span><span class="sxs-lookup"><span data-stu-id="2dd13-123">hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span>

<span data-ttu-id="2dd13-124">Se o conjunto de registros de saudação ainda não existir, este comando criará para você.</span><span class="sxs-lookup"><span data-stu-id="2dd13-124">If hello record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="2dd13-125">Se já existir um conjunto de registros de hello, este comando denomine Olá registro que você especificar o conjunto de registros existentes toohello.</span><span class="sxs-lookup"><span data-stu-id="2dd13-125">If hello record set already exists, this command adda hello record you specify toohello existing record set.</span></span>

<span data-ttu-id="2dd13-126">Se um novo conjunto de registros for criado, um TTL padrão de 3600 será usado.</span><span class="sxs-lookup"><span data-stu-id="2dd13-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="2dd13-127">Para obter instruções sobre como toouse TTLs diferentes, consulte [criar um conjunto de registros de DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="2dd13-127">For instructions on how toouse different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="2dd13-128">Olá, exemplo a seguir cria um registro chamado *www* na zona Olá *contoso.com* no grupo de recursos de saudação *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="2dd13-128">hello following example creates an A record called *www* in hello zone *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="2dd13-129">Olá Olá é um registro de endereço IP *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="2dd13-129">hello IP address of hello A record is *1.2.3.4*.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="2dd13-130">toocreate um registro no ápice da saudação da zona de saudação (nesse caso, "contoso.com"), use o nome do registro hello "@", incluindo Olá aspas:</span><span class="sxs-lookup"><span data-stu-id="2dd13-130">toocreate a record in hello apex of hello zone (in this case, "contoso.com"), use hello record name "@", including hello quotation marks:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="2dd13-131">Criar um conjunto de registros DNS</span><span class="sxs-lookup"><span data-stu-id="2dd13-131">Create a DNS record set</span></span>

<span data-ttu-id="2dd13-132">Em Olá acima exemplos, registro DNS Olá era o tooan adicionado existente de conjunto de registros ou conjunto de registros de saudação foi criado *implicitamente*.</span><span class="sxs-lookup"><span data-stu-id="2dd13-132">In hello above examples, hello DNS record was either added tooan existing record set, or hello record set was created *implicitly*.</span></span> <span data-ttu-id="2dd13-133">Você também pode criar o conjunto de registros de saudação *explicitamente* antes de adicionar registros tooit.</span><span class="sxs-lookup"><span data-stu-id="2dd13-133">You can also create hello record set *explicitly* before adding records tooit.</span></span> <span data-ttu-id="2dd13-134">DNS do Azure oferece suporte a conjuntos de registros 'empty', que podem agir como um espaço reservado tooreserve um nome DNS antes de criar registros DNS.</span><span class="sxs-lookup"><span data-stu-id="2dd13-134">Azure DNS supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="2dd13-135">Conjuntos de registros vazios são visíveis em Olá DNS do Azure plano de controle, mas não aparecem nos servidores de nome DNS do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2dd13-135">Empty record sets are visible in hello Azure DNS control plane, but do not appear on hello Azure DNS name servers.</span></span>

<span data-ttu-id="2dd13-136">Conjuntos de registros são criados usando Olá `azure network dns record-set create` comando.</span><span class="sxs-lookup"><span data-stu-id="2dd13-136">Record sets are created using hello `azure network dns record-set create` command.</span></span> <span data-ttu-id="2dd13-137">Para obter ajuda, consulte `azure network dns record-set create -h`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-137">For help, see `azure network dns record-set create -h`.</span></span>

<span data-ttu-id="2dd13-138">Criar registro Olá definido explicitamente permite toospecify propriedades de conjunto de registros como Olá [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) e metadados.</span><span class="sxs-lookup"><span data-stu-id="2dd13-138">Creating hello record set explicitly allows you toospecify record set properties such as hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="2dd13-139">[Metadados de conjunto de registros](dns-zones-records.md#tags-and-metadata) podem ser dados específicos do aplicativo de tooassociate usado com cada conjunto de registros, como pares chave-valor.</span><span class="sxs-lookup"><span data-stu-id="2dd13-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="2dd13-140">Olá, exemplo a seguir cria um registro vazio definido com um TTL de 60 segundos, por meio de saudação `--ttl` parâmetro (forma abreviada `-l`):</span><span class="sxs-lookup"><span data-stu-id="2dd13-140">hello following example creates an empty record set with a 60-second TTL, by using hello `--ttl` parameter (short form `-l`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

<span data-ttu-id="2dd13-141">Olá, exemplo a seguir cria um conjunto de registros com duas entradas de metadados, "dept = Finanças" e "ambiente = produção", usando Olá `--metadata` parâmetro (forma abreviada `-m`):</span><span class="sxs-lookup"><span data-stu-id="2dd13-141">hello following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter (short form `-m`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

<span data-ttu-id="2dd13-142">Depois de criar um conjunto de registros vazio, registros podem ser adicionados usando `azure network dns record-set add-record` conforme descrito em [Criar um registro DNS](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="2dd13-142">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="2dd13-143">Criar outros tipos de registro</span><span class="sxs-lookup"><span data-stu-id="2dd13-143">Create records of other types</span></span>

<span data-ttu-id="2dd13-144">Depois de ter visto em detalhes como registros toocreate 'A', Olá seguintes exemplos mostram como suporte para registro de toocreate de outros tipos de registro DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dd13-144">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="2dd13-145">parâmetros de saudação usados toospecify registro de saudação dados variar dependendo do tipo de saudação do registro hello.</span><span class="sxs-lookup"><span data-stu-id="2dd13-145">hello parameters used toospecify hello record data vary depending on hello type of hello record.</span></span> <span data-ttu-id="2dd13-146">Por exemplo, para um registro do tipo "A", você especificar endereço Olá IPv4 com parâmetro hello `-a <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-146">For example, for a record of type "A", you specify hello IPv4 address with hello parameter `-a <IPv4 address>`.</span></span> <span data-ttu-id="2dd13-147">Olá parâmetros para cada tipo de registro pode ser listado usando `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-147">hello parameters for each record type can be listed using `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="2dd13-148">Em cada caso, mostramos como toocreate um único registro.</span><span class="sxs-lookup"><span data-stu-id="2dd13-148">In each case, we show how toocreate a single record.</span></span> <span data-ttu-id="2dd13-149">registro de saudação é adicionado toohello existente de conjunto de registros ou um conjunto de registros criado implicitamente.</span><span class="sxs-lookup"><span data-stu-id="2dd13-149">hello record is added toohello existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="2dd13-150">Para obter mais informações sobre como criar conjuntos de registros e definir o parâmetro do conjunto de registros explicitamente, consulte [Criar um conjunto de registros DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="2dd13-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="2dd13-151">Não fornecemos um exemplo toocreate um conjunto de registros SOA, como SOAs são criados e excluídos com cada zona DNS e não pode ser criado ou excluído separadamente.</span><span class="sxs-lookup"><span data-stu-id="2dd13-151">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="2dd13-152">No entanto, [Olá SOA pode ser modificado, conforme mostrado no exemplo mais adiante](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="2dd13-152">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="2dd13-153">Criar um registro AAAA</span><span class="sxs-lookup"><span data-stu-id="2dd13-153">Create an AAAA record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="2dd13-154">Criar um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="2dd13-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="2dd13-155">padrões DNS Olá não permitem que os registros CNAME no ápice da saudação de uma zona (`-Name "@"`), nem eles permitem que os conjuntos de registro que contém mais de um registro.</span><span class="sxs-lookup"><span data-stu-id="2dd13-155">hello DNS standards do not permit CNAME records at hello apex of a zone (`-Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="2dd13-156">Para obter mais informações, consulte [Registros CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="2dd13-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="2dd13-157">Criar um registro MX</span><span class="sxs-lookup"><span data-stu-id="2dd13-157">Create an MX record</span></span>

<span data-ttu-id="2dd13-158">Neste exemplo, podemos usar o nome do conjunto de registros de hello "@" hello toocreate registro MX no ápice da zona de saudação (nesse caso, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="2dd13-158">In this example, we use hello record set name "@" toocreate hello MX record at hello zone apex (in this case, "contoso.com").</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="2dd13-159">Criar um registro NS</span><span class="sxs-lookup"><span data-stu-id="2dd13-159">Create an NS record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="2dd13-160">Criar um registro PTR</span><span class="sxs-lookup"><span data-stu-id="2dd13-160">Create a PTR record</span></span>

<span data-ttu-id="2dd13-161">Nesse caso, ' Meu-arpa-zone.com' representa Olá zona ARPA que representa o intervalo de IP.</span><span class="sxs-lookup"><span data-stu-id="2dd13-161">In this case, 'my-arpa-zone.com' represents hello ARPA zone representing your IP range.</span></span> <span data-ttu-id="2dd13-162">Cada registro PTR definido nesta zona corresponde endereço IP tooan dentro desse intervalo IP.</span><span class="sxs-lookup"><span data-stu-id="2dd13-162">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span>  <span data-ttu-id="2dd13-163">nome do registro Olá '10' é último octeto saudação do endereço IP hello dentro desse intervalo IP representado por esse registro.</span><span class="sxs-lookup"><span data-stu-id="2dd13-163">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a><span data-ttu-id="2dd13-164">Criar um registro SRV</span><span class="sxs-lookup"><span data-stu-id="2dd13-164">Create an SRV record</span></span>

<span data-ttu-id="2dd13-165">Ao criar um [conjunto de registros SRV](dns-zones-records.md#srv-records), especificar Olá  *\_service* e  *\_protocolo* em Olá nome de conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="2dd13-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="2dd13-166">Não há nenhuma necessidade tooinclude "@" no hello registro de nome do conjunto quando criar um registro SRV definida no ápice da zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dd13-166">There is no need tooinclude "@" in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a><span data-ttu-id="2dd13-167">Criar um registro TXT</span><span class="sxs-lookup"><span data-stu-id="2dd13-167">Create a TXT record</span></span>

<span data-ttu-id="2dd13-168">Olá exemplo a seguir mostra como registrar o toocreate um TXT.</span><span class="sxs-lookup"><span data-stu-id="2dd13-168">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="2dd13-169">Para obter mais informações sobre Olá tamanho máximo com suporte no registros TXT, consulte [registros TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="2dd13-169">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="2dd13-170">Obter um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="2dd13-170">Get a record set</span></span>

<span data-ttu-id="2dd13-171">tooretrieve um conjunto de registros existente, use `azure network dns record-set show`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-171">tooretrieve an existing record set, use `azure network dns record-set show`.</span></span> <span data-ttu-id="2dd13-172">Para obter ajuda, consulte `azure network dns record-set show -h`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-172">For help, see `azure network dns record-set show -h`.</span></span>

<span data-ttu-id="2dd13-173">Ao criar um conjunto de registros ou de registro, registro Olá definir nome fornecido deve ser um *relativo* nome, o que significa que ele deve excluir o nome da zona hello.</span><span class="sxs-lookup"><span data-stu-id="2dd13-173">As when creating a record or record set, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="2dd13-174">Também é necessário o tipo de registro toospecify hello, zona Olá contendo Olá registro definido e Olá que contém a zona de saudação do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2dd13-174">You also need toospecify hello record type, hello zone containing hello record set, and hello resource group containing hello zone.</span></span>

<span data-ttu-id="2dd13-175">Olá, exemplo a seguir recupera o registro de saudação *www* de um tipo de zona *contoso.com* no grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="2dd13-175">hello following example retrieves hello record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a><span data-ttu-id="2dd13-176">Listar os conjuntos de registros</span><span class="sxs-lookup"><span data-stu-id="2dd13-176">List record sets</span></span>

<span data-ttu-id="2dd13-177">Você pode listar todos os registros em uma zona DNS usando Olá `azure network dns record-set list` comando.</span><span class="sxs-lookup"><span data-stu-id="2dd13-177">You can list all records in a DNS zone by using hello `azure network dns record-set list` command.</span></span> <span data-ttu-id="2dd13-178">Para obter ajuda, consulte `azure network dns record-set list -h`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-178">For help, see `azure network dns record-set list -h`.</span></span>

<span data-ttu-id="2dd13-179">Este exemplo retorna conjuntos de todos os registros na zona Olá *contoso.com*, no grupo de recursos *MyResourceGroup*, independentemente do nome ou tipo de registro:</span><span class="sxs-lookup"><span data-stu-id="2dd13-179">This example returns all record sets in hello zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

<span data-ttu-id="2dd13-180">Este exemplo retorna todos os conjuntos de registros que correspondem a saudação considerando o tipo de registro (nesse caso, 'A' registros):</span><span class="sxs-lookup"><span data-stu-id="2dd13-180">This example returns all record sets that match hello given record type (in this case, 'A' records):</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="2dd13-181">Adicionar um registro tooan existente de conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="2dd13-181">Add a record tooan existing record set</span></span>

<span data-ttu-id="2dd13-182">Você pode usar `azure network dns record-set add-record` tanto toocreate um registro em um novo registro ou definidas tooadd um registro existente tooan registro.</span><span class="sxs-lookup"><span data-stu-id="2dd13-182">You can use `azure network dns record-set add-record` both toocreate a record in a new record set, or tooadd a record tooan existing record set.</span></span>

<span data-ttu-id="2dd13-183">Para obter mais informações, consulte [Criar um registro DNS](#create-a-dns-record) e [Criar registros de outros tipos](#create-records-of-other-types), acima.</span><span class="sxs-lookup"><span data-stu-id="2dd13-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="2dd13-184">Remover um registro de um conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="2dd13-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="2dd13-185">registrar tooremove um DNS de um conjunto de registros existente, use `azure network dns record-set delete-record`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-185">tooremove a DNS record from an existing record set, use `azure network dns record-set delete-record`.</span></span> <span data-ttu-id="2dd13-186">Para obter ajuda, consulte `azure network dns record-set delete-record -h`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-186">For help, see `azure network dns record-set delete-record -h`.</span></span>

<span data-ttu-id="2dd13-187">Esse comando exclui um registro DNS de um conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="2dd13-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="2dd13-188">Se o último registro de saudação em um conjunto de registros é excluído, o registro de saudação definido em si é **não** excluído.</span><span class="sxs-lookup"><span data-stu-id="2dd13-188">If hello last record in a record set is deleted, hello record set itself is **not** deleted.</span></span> <span data-ttu-id="2dd13-189">Em vez disso, um conjunto de registros vazio é mantido.</span><span class="sxs-lookup"><span data-stu-id="2dd13-189">Instead, an empty record set is left.</span></span> <span data-ttu-id="2dd13-190">registro de saudação toodelete definido em vez disso, consulte [excluir um conjunto de registros](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="2dd13-190">toodelete hello record set instead, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="2dd13-191">Você precisa toospecify Olá toobe registro excluído e zona Olá deve ser excluída, usando Olá os mesmos parâmetros durante a criação de um registro usando `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-191">You need toospecify hello record toobe deleted and hello zone it should be deleted from, using hello same parameters as when creating a record using `azure network dns record-set add-record`.</span></span> <span data-ttu-id="2dd13-192">Esses parâmetros são descritos em [Criar um registro DNS](#create-a-dns-record) e [Criar registros de outros tipos](#create-records-of-other-types), acima.</span><span class="sxs-lookup"><span data-stu-id="2dd13-192">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="2dd13-193">Esse comando solicita uma confirmação.</span><span class="sxs-lookup"><span data-stu-id="2dd13-193">This command prompts for confirmation.</span></span> <span data-ttu-id="2dd13-194">Esse aviso pode ser suprimido Olá `--quiet` alternar (forma abreviada `-q`).</span><span class="sxs-lookup"><span data-stu-id="2dd13-194">This prompt can be suppressed using hello `--quiet` switch (short form `-q`).</span></span>

<span data-ttu-id="2dd13-195">Olá exclusões de exemplo a seguir Olá um registro com o valor '1.2.3.4' do registro Olá conjunto nomeado *www* na zona Olá *contoso.com*, no grupo de recursos de saudação *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="2dd13-195">hello following example deletes hello A record with value '1.2.3.4' from hello record set named *www* in hello zone *contoso.com*, in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="2dd13-196">prompt de confirmação de saudação é suprimida.</span><span class="sxs-lookup"><span data-stu-id="2dd13-196">hello confirmation prompt is suppressed.</span></span>

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="2dd13-197">Modificar um conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="2dd13-197">Modify an existing record set</span></span>

<span data-ttu-id="2dd13-198">Cada conjunto de registros contém um [TTL (vida útil)](dns-zones-records.md#time-to-live), [metadados](dns-zones-records.md#tags-and-metadata) e registros DNS.</span><span class="sxs-lookup"><span data-stu-id="2dd13-198">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="2dd13-199">Olá seções a seguir explicam como toomodify essas propriedades.</span><span class="sxs-lookup"><span data-stu-id="2dd13-199">hello following sections explain how toomodify each of these properties.</span></span>

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="2dd13-200">toomodify um registro A, AAAA, MX, NS, PTR, SRV ou TXT</span><span class="sxs-lookup"><span data-stu-id="2dd13-200">toomodify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="2dd13-201">toomodify um registro existente do tipo A, AAAA, MX, NS, PTR, SRV ou TXT, você primeiro deve adicionar um novo registro e, em seguida, excluir o registro existente hello.</span><span class="sxs-lookup"><span data-stu-id="2dd13-201">toomodify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete hello existing record.</span></span> <span data-ttu-id="2dd13-202">Para obter instruções detalhadas sobre como toodelete e adicionar registros, consulte Olá seções anteriores deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2dd13-202">For detailed instructions on how toodelete and add records, see hello earlier sections of this article.</span></span>

<span data-ttu-id="2dd13-203">saudação de exemplo a seguir mostra como toomodify um registro de 'A', do IP endereço 1.2.3.4 tooIP endereço 5.6.7.8:</span><span class="sxs-lookup"><span data-stu-id="2dd13-203">hello following example shows how toomodify an 'A' record, from IP address 1.2.3.4 tooIP address 5.6.7.8:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="toomodify-a-cname-record"></a><span data-ttu-id="2dd13-204">toomodify um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="2dd13-204">toomodify a CNAME record</span></span>

<span data-ttu-id="2dd13-205">toomodify um registro CNAME, use `azure network dns record-set add-record` tooadd Olá novo valor de registro.</span><span class="sxs-lookup"><span data-stu-id="2dd13-205">toomodify a CNAME record, use `azure network dns record-set add-record` tooadd hello new record value.</span></span> <span data-ttu-id="2dd13-206">Ao contrário de outros tipos de registro, um conjunto de registros CNAME pode conter apenas um único registro.</span><span class="sxs-lookup"><span data-stu-id="2dd13-206">Unlike other record types, a CNAME record set can only contain a single record.</span></span> <span data-ttu-id="2dd13-207">Portanto, o registro existente Olá é *substituído* quando Olá novo registro é adicionado e não precisa toobe excluído separadamente.</span><span class="sxs-lookup"><span data-stu-id="2dd13-207">Therefore, hello existing record is *replaced* when hello new record is added, and does not need toobe deleted separately.</span></span>  <span data-ttu-id="2dd13-208">Você será solicitado tooaccept essa substituição.</span><span class="sxs-lookup"><span data-stu-id="2dd13-208">You will be prompted tooaccept this replacement.</span></span>

<span data-ttu-id="2dd13-209">exemplo Hello modifica conjunto de registros de CNAME Olá *www* na zona Olá *contoso.com*, no grupo de recursos *MyResourceGroup*, toopoint muito www.fabrikam.net em vez de seu valor existente:</span><span class="sxs-lookup"><span data-stu-id="2dd13-209">hello example modifies hello CNAME record set *www* in hello zone *contoso.com*, in resource group *MyResourceGroup*, toopoint too'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="2dd13-210">toomodify um registro SOA</span><span class="sxs-lookup"><span data-stu-id="2dd13-210">toomodify an SOA record</span></span>

<span data-ttu-id="2dd13-211">Use `azure network dns record-set set-soa-record` toomodify Olá SOA para uma zona DNS.</span><span class="sxs-lookup"><span data-stu-id="2dd13-211">Use `azure network dns record-set set-soa-record` toomodify hello SOA for a given DNS zone.</span></span> <span data-ttu-id="2dd13-212">Para obter ajuda, consulte `azure network dns record-set set-soa-record -h`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-212">For help, see `azure network dns record-set set-soa-record -h`.</span></span>

<span data-ttu-id="2dd13-213">Olá exemplo a seguir mostra como propriedade tooset Olá 'email' de saudação SOA registrar para a zona de saudação *contoso.com* no grupo de recursos de saudação *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="2dd13-213">hello following example shows how tooset hello 'email' property of hello SOA record for hello zone *contoso.com* in hello resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="2dd13-214">toomodify NS registros no ápice da zona de saudação</span><span class="sxs-lookup"><span data-stu-id="2dd13-214">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="2dd13-215">registro de NS Olá definido no ápice da zona de saudação é criado automaticamente com cada zona DNS.</span><span class="sxs-lookup"><span data-stu-id="2dd13-215">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="2dd13-216">Ela contém nomes de saudação da zona do hello Azure DNS nome servidores toohello atribuído.</span><span class="sxs-lookup"><span data-stu-id="2dd13-216">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="2dd13-217">Você pode adicionar nome adicionais servidores toothis NS conjunto de registros, toosupport co-hospedagem domínios com mais de um provedor DNS.</span><span class="sxs-lookup"><span data-stu-id="2dd13-217">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="2dd13-218">Você também pode modificar hello TTL e metadados para esse conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="2dd13-218">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="2dd13-219">No entanto, você não pode remover ou modificar servidores de nome DNS do Azure preenchidos previamente hello.</span><span class="sxs-lookup"><span data-stu-id="2dd13-219">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="2dd13-220">Observe que isso se aplica apenas toohello NS conjunto de registros no ápice da zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dd13-220">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="2dd13-221">Outros conjuntos de registros NS na zona (como zonas de filho usado toodelegate) podem ser modificados sem restrição.</span><span class="sxs-lookup"><span data-stu-id="2dd13-221">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="2dd13-222">saudação de exemplo a seguir mostra como tooadd um registro NS de toohello de servidor de nome adicionais definir no ápice da zona de saudação:</span><span class="sxs-lookup"><span data-stu-id="2dd13-222">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a><span data-ttu-id="2dd13-223">Definir toomodify Olá TTL de um registro existente</span><span class="sxs-lookup"><span data-stu-id="2dd13-223">toomodify hello TTL of an existing record set</span></span>

<span data-ttu-id="2dd13-224">Definir toomodify Olá TTL de um registro existente, use `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-224">toomodify hello TTL of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="2dd13-225">Para obter ajuda, consulte `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-225">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="2dd13-226">saudação de exemplo a seguir mostra como toomodify um conjunto de registros TTL, neste caso, too60 segundos:</span><span class="sxs-lookup"><span data-stu-id="2dd13-226">hello following example shows how toomodify a record set TTL, in this case too60 seconds:</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a><span data-ttu-id="2dd13-227">toomodify Olá metadados de um conjunto de registro existente</span><span class="sxs-lookup"><span data-stu-id="2dd13-227">toomodify hello metadata of an existing record set</span></span>

<span data-ttu-id="2dd13-228">[Metadados de conjunto de registros](dns-zones-records.md#tags-and-metadata) podem ser dados específicos do aplicativo de tooassociate usado com cada conjunto de registros, como pares chave-valor.</span><span class="sxs-lookup"><span data-stu-id="2dd13-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="2dd13-229">Definir toomodify Olá metadados de um registro existente, use `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-229">toomodify hello metadata of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="2dd13-230">Para obter ajuda, consulte `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-230">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="2dd13-231">Olá exemplo a seguir mostra como toomodify um conjunto de registros com duas entradas de metadados, "dept = Finanças" e "ambiente = produção", usando Olá `--metadata` parâmetro (forma abreviada `-m`).</span><span class="sxs-lookup"><span data-stu-id="2dd13-231">hello following example shows how toomodify a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter (short form `-m`).</span></span> <span data-ttu-id="2dd13-232">Observe que os metadados existentes são *substituído* pelos valores hello fornecidos.</span><span class="sxs-lookup"><span data-stu-id="2dd13-232">Note that any existing metadata is *replaced* by hello values given.</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a><span data-ttu-id="2dd13-233">Excluir um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="2dd13-233">Delete a record set</span></span>

<span data-ttu-id="2dd13-234">Conjuntos de registros podem ser excluídos usando Olá `azure network dns record-set delete` comando.</span><span class="sxs-lookup"><span data-stu-id="2dd13-234">Record sets can be deleted by using hello `azure network dns record-set delete` command.</span></span> <span data-ttu-id="2dd13-235">Para obter ajuda, consulte `azure network dns record-set delete -h`.</span><span class="sxs-lookup"><span data-stu-id="2dd13-235">For help, see `azure network dns record-set delete -h`.</span></span> <span data-ttu-id="2dd13-236">Excluir um conjunto de registros também exclui todos os registros no conjunto de registros de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dd13-236">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="2dd13-237">Você não pode excluir Olá SOA e NS conjuntos de registros no ápice da zona de saudação (`-Name "@"`).</span><span class="sxs-lookup"><span data-stu-id="2dd13-237">You cannot delete hello SOA and NS record sets at hello zone apex (`-Name "@"`).</span></span>  <span data-ttu-id="2dd13-238">Eles são criados automaticamente quando Olá zona foi criado e são excluídos automaticamente quando Olá zona é excluída.</span><span class="sxs-lookup"><span data-stu-id="2dd13-238">These are created automatically when hello zone was created, and are deleted automatically when hello zone is deleted.</span></span>

<span data-ttu-id="2dd13-239">Olá, exemplo a seguir exclui conjunto nomeado de registros de saudação *www* de um tipo de zona Olá *contoso.com* no grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="2dd13-239">hello following example deletes hello record set named *www* of type A from hello zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

<span data-ttu-id="2dd13-240">Você está operação de exclusão de saudação tooconfirm solicitada.</span><span class="sxs-lookup"><span data-stu-id="2dd13-240">You are prompted tooconfirm hello delete operation.</span></span> <span data-ttu-id="2dd13-241">toosuppress nesse prompt, use Olá `--quiet` alternar (forma abreviada `-q`).</span><span class="sxs-lookup"><span data-stu-id="2dd13-241">toosuppress this prompt, use hello `--quiet` switch (short form `-q`).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2dd13-242">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2dd13-242">Next steps</span></span>

<span data-ttu-id="2dd13-243">Saiba mais sobre as [zonas e os registros no DNS do Azure](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="2dd13-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="2dd13-244">Saiba como muito[proteger suas zonas e registros de](dns-protect-zones-recordsets.md) ao usar o DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dd13-244">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
