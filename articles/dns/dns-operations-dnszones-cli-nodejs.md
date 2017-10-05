---
title: Gerenciar as zonas DNS no DNS do Azure - CLI do Azure 1.0 | Microsoft Docs
description: "Você pode gerenciar zonas DNS usando a CLI do Azure 1.0. Este artigo mostra como atualizar, excluir e criar zonas DNS no DNS do Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: 588c87749f049eff5b9e0729f6769c8367ba41e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="4ad03-104">Como gerenciar Zonas DNS no DNS do Azure usando a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="4ad03-104">How to manage DNS Zones in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ad03-105">Portal</span><span class="sxs-lookup"><span data-stu-id="4ad03-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="4ad03-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ad03-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="4ad03-107">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="4ad03-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="4ad03-108">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="4ad03-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="4ad03-109">Este guia mostra como gerenciar as zonas DNS usando a CLI do Azure 1.0 entre plataformas, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="4ad03-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="4ad03-110">Você também pode gerenciar seus registros DNS usando o [Azure PowerShell](dns-operations-dnszones.md) ou o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ad03-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="4ad03-111">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="4ad03-111">CLI versions to complete the task</span></span>

<span data-ttu-id="4ad03-112">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="4ad03-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="4ad03-113">[CLI do Azure 1.0](dns-operations-dnszones-cli-nodejs.md) – nossa CLI para os modelos de implantação clássico e do resource manager.</span><span class="sxs-lookup"><span data-stu-id="4ad03-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="4ad03-114">[CLI do Azure 2.0](dns-operations-dnszones-cli.md) – nossa próxima geração de CLI para o modelo de implantação do resource manager.</span><span class="sxs-lookup"><span data-stu-id="4ad03-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="4ad03-115">Introdução</span><span class="sxs-lookup"><span data-stu-id="4ad03-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="4ad03-116">Obtendo ajuda</span><span class="sxs-lookup"><span data-stu-id="4ad03-116">Getting help</span></span>

<span data-ttu-id="4ad03-117">Todos os comandos da CLI 1.0 relacionados ao DNS do Azure começam com `azure network dns`.</span><span class="sxs-lookup"><span data-stu-id="4ad03-117">All CLI 1.0 commands relating to Azure DNS start with `azure network dns`.</span></span> <span data-ttu-id="4ad03-118">A ajuda está disponível para cada comando usando a opção `--help` (forma abreviada `-h`).</span><span class="sxs-lookup"><span data-stu-id="4ad03-118">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="4ad03-119">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4ad03-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="4ad03-120">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="4ad03-120">Create a DNS zone</span></span>

<span data-ttu-id="4ad03-121">Uma zona DNS é criada usando o comando `azure network dns zone create` .</span><span class="sxs-lookup"><span data-stu-id="4ad03-121">A DNS zone is created using the `azure network dns zone create` command.</span></span> <span data-ttu-id="4ad03-122">Para obter ajuda, consulte `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="4ad03-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="4ad03-123">O exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos chamado *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="4ad03-123">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="4ad03-124">Para criar uma zona DNS com marcas</span><span class="sxs-lookup"><span data-stu-id="4ad03-124">To create a DNS zone with tags</span></span>

<span data-ttu-id="4ad03-125">O exemplo a seguir mostra como criar uma zona DNS com duas [marcas do Azure Resource Manager](dns-zones-records.md#tags), *project = demo* e *env = test*, usando o parâmetro `--tags` (forma abreviada `-t`):</span><span class="sxs-lookup"><span data-stu-id="4ad03-125">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="4ad03-126">Obter uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="4ad03-126">Get a DNS zone</span></span>

<span data-ttu-id="4ad03-127">Para recuperar uma zona DNS, use `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="4ad03-127">To retrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="4ad03-128">Para obter ajuda, consulte `azure network dns zone show -h`.</span><span class="sxs-lookup"><span data-stu-id="4ad03-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="4ad03-129">O exemplo a seguir retorna a zona DNS *contoso.com* e seus dados associados do grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="4ad03-129">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="4ad03-130">O exemplo a seguir é a resposta.</span><span class="sxs-lookup"><span data-stu-id="4ad03-130">The following example is the response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

<span data-ttu-id="4ad03-131">Observe que registros DNS não são retornados por `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="4ad03-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="4ad03-132">Para listar registros DNS, use `azure network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="4ad03-132">To list DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="4ad03-133">Listar as zonas DNS</span><span class="sxs-lookup"><span data-stu-id="4ad03-133">List DNS zones</span></span>

<span data-ttu-id="4ad03-134">Para enumerar zonas DNS, use `azure network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="4ad03-134">To enumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="4ad03-135">Para obter ajuda, consulte `azure network dns zone list -h`.</span><span class="sxs-lookup"><span data-stu-id="4ad03-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="4ad03-136">Especificar o grupo de recursos lista apenas as zonas dentro do grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="4ad03-136">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="4ad03-137">Omitir o grupo de recursos lista todas as zonas na assinatura:</span><span class="sxs-lookup"><span data-stu-id="4ad03-137">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="4ad03-138">Atualizar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="4ad03-138">Update a DNS zone</span></span>

<span data-ttu-id="4ad03-139">As alterações a um recurso da zona DNS podem ser feitas usando o `azure network dns zone set`.</span><span class="sxs-lookup"><span data-stu-id="4ad03-139">Changes to a DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="4ad03-140">Para obter ajuda, consulte `azure network dns zone set -h`.</span><span class="sxs-lookup"><span data-stu-id="4ad03-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="4ad03-141">Esse comando não atualiza nenhum dos conjuntos de registros DNS dentro da zona (consulte [Como gerenciar registros DNS](dns-operations-recordsets-cli-nodejs.md)).</span><span class="sxs-lookup"><span data-stu-id="4ad03-141">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="4ad03-142">Ele só é usado para atualizar as propriedades do recurso da zona em si.</span><span class="sxs-lookup"><span data-stu-id="4ad03-142">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="4ad03-143">Atualmente, essas propriedades são limitadas às [“marcas” do Azure Resource Manager](dns-zones-records.md#tags) para o recurso de zona.</span><span class="sxs-lookup"><span data-stu-id="4ad03-143">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="4ad03-144">O exemplo a seguir mostra como atualizar as marcas em uma zona DNS.</span><span class="sxs-lookup"><span data-stu-id="4ad03-144">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="4ad03-145">As marcas existentes são substituídas pelo valor especificado.</span><span class="sxs-lookup"><span data-stu-id="4ad03-145">The existing tags are replaced by the value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="4ad03-146">Excluir uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="4ad03-146">Delete a DNS Zone</span></span>

<span data-ttu-id="4ad03-147">As zonas DNS podem ser excluídas por meio do `azure network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="4ad03-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="4ad03-148">Para obter ajuda, consulte `azure network dns zone delete -h`.</span><span class="sxs-lookup"><span data-stu-id="4ad03-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="4ad03-149">Excluir uma zona DNS também excluirá todos os registros DNS na zona.</span><span class="sxs-lookup"><span data-stu-id="4ad03-149">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="4ad03-150">Essa operação não pode ser desfeita.</span><span class="sxs-lookup"><span data-stu-id="4ad03-150">This operation cannot be undone.</span></span> <span data-ttu-id="4ad03-151">Se a zona DNS estiver em uso, serviços que usam a zona falharão quando a zona for excluída.</span><span class="sxs-lookup"><span data-stu-id="4ad03-151">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="4ad03-152">Para se proteger contra a exclusão acidental da zona, consulte [Proteger registros e zonas DNS](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="4ad03-152">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="4ad03-153">Esse comando solicita uma confirmação.</span><span class="sxs-lookup"><span data-stu-id="4ad03-153">This command prompts for confirmation.</span></span> <span data-ttu-id="4ad03-154">A opção `--quiet` (forma abreviada `-q`) suprime esse prompt.</span><span class="sxs-lookup"><span data-stu-id="4ad03-154">The optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="4ad03-155">O exemplo a seguir mostra como excluir a zona *contoso.com* de grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="4ad03-155">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="4ad03-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4ad03-156">Next steps</span></span>

<span data-ttu-id="4ad03-157">Saiba como [gerenciar conjuntos de registros e registros](dns-getstarted-create-recordset-cli-nodejs.md) em sua zona DNS.</span><span class="sxs-lookup"><span data-stu-id="4ad03-157">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="4ad03-158">Saiba como [delegar seu domínio ao DNS do Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="4ad03-158">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

