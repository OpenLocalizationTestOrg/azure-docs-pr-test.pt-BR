---
title: aaaManage DNS zonas no DNS do Azure - 1.0 da CLI do Azure | Microsoft Docs
description: "Você pode gerenciar zonas DNS usando a CLI do Azure 1.0. Este artigo mostra como tooupdate, excluir e criar zonas DNS no DNS do Azure."
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
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a><span data-ttu-id="eaa69-104">Como toomanage zonas de DNS no DNS do Azure usando Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="eaa69-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="eaa69-105">Portal</span><span class="sxs-lookup"><span data-stu-id="eaa69-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="eaa69-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eaa69-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="eaa69-107">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="eaa69-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="eaa69-108">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="eaa69-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="eaa69-109">Este guia mostra como toomanage suas zonas DNS usando Olá multiplataforma CLI do Azure 1.0, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="eaa69-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="eaa69-110">Você também pode gerenciar as zonas DNS usando [Azure PowerShell](dns-operations-dnszones.md) ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eaa69-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="eaa69-111">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="eaa69-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="eaa69-112">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="eaa69-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="eaa69-113">[1.0 de CLI do Azure](dns-operations-dnszones-cli-nodejs.md) -nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de hello.</span><span class="sxs-lookup"><span data-stu-id="eaa69-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="eaa69-114">[2.0 do CLI do Azure](dns-operations-dnszones-cli.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="eaa69-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="eaa69-115">Introdução</span><span class="sxs-lookup"><span data-stu-id="eaa69-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="eaa69-116">Obtendo ajuda</span><span class="sxs-lookup"><span data-stu-id="eaa69-116">Getting help</span></span>

<span data-ttu-id="eaa69-117">Todos os comandos de CLI 1.0 relacionadas tooAzure DNS iniciam com `azure network dns`.</span><span class="sxs-lookup"><span data-stu-id="eaa69-117">All CLI 1.0 commands relating tooAzure DNS start with `azure network dns`.</span></span> <span data-ttu-id="eaa69-118">A Ajuda está disponível para cada comando usando Olá `--help` opção (forma abreviada `-h`).</span><span class="sxs-lookup"><span data-stu-id="eaa69-118">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="eaa69-119">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="eaa69-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="eaa69-120">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="eaa69-120">Create a DNS zone</span></span>

<span data-ttu-id="eaa69-121">Uma zona DNS é criada usando Olá `azure network dns zone create` comando.</span><span class="sxs-lookup"><span data-stu-id="eaa69-121">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="eaa69-122">Para obter ajuda, consulte `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="eaa69-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="eaa69-123">Olá, exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos de saudação chamado *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="eaa69-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="eaa69-124">toocreate uma zona DNS com marcas</span><span class="sxs-lookup"><span data-stu-id="eaa69-124">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="eaa69-125">Olá exemplo a seguir mostra como toocreate um DNS da zona com dois [do Azure Resource Manager marcas](dns-zones-records.md#tags), *projeto = demonstração* e *env = test*, usando Olá `--tags` parâmetro (forma abreviada `-t`):</span><span class="sxs-lookup"><span data-stu-id="eaa69-125">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="eaa69-126">Obter uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="eaa69-126">Get a DNS zone</span></span>

<span data-ttu-id="eaa69-127">tooretrieve uma zona DNS, use `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="eaa69-127">tooretrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="eaa69-128">Para obter ajuda, consulte `azure network dns zone show -h`.</span><span class="sxs-lookup"><span data-stu-id="eaa69-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="eaa69-129">Olá, exemplo a seguir retorna zona do DNS Olá *contoso.com* e seus dados associados do grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="eaa69-129">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="eaa69-130">saudação de exemplo a seguir é a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="eaa69-130">hello following example is hello response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
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

<span data-ttu-id="eaa69-131">Observe que registros DNS não são retornados por `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="eaa69-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="eaa69-132">registros DNS toolist, use `azure network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="eaa69-132">toolist DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="eaa69-133">Listar as zonas DNS</span><span class="sxs-lookup"><span data-stu-id="eaa69-133">List DNS zones</span></span>

<span data-ttu-id="eaa69-134">zonas DNS tooenumerate, use `azure network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="eaa69-134">tooenumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="eaa69-135">Para obter ajuda, consulte `azure network dns zone list -h`.</span><span class="sxs-lookup"><span data-stu-id="eaa69-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="eaa69-136">Grupo de recursos de saudação especificando lista apenas as zonas no grupo de recursos de saudação:</span><span class="sxs-lookup"><span data-stu-id="eaa69-136">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="eaa69-137">Grupo de recursos de saudação omitindo lista todas as zonas na assinatura hello:</span><span class="sxs-lookup"><span data-stu-id="eaa69-137">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="eaa69-138">Atualizar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="eaa69-138">Update a DNS zone</span></span>

<span data-ttu-id="eaa69-139">Alterações tooa recurso de zona do DNS pode ser feito usando `azure network dns zone set`.</span><span class="sxs-lookup"><span data-stu-id="eaa69-139">Changes tooa DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="eaa69-140">Para obter ajuda, consulte `azure network dns zone set -h`.</span><span class="sxs-lookup"><span data-stu-id="eaa69-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="eaa69-141">Este comando não atualizar conjuntos de registros de DNS hello dentro da zona de saudação (consulte [como registros DNS tooManage](dns-operations-recordsets-cli-nodejs.md)).</span><span class="sxs-lookup"><span data-stu-id="eaa69-141">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="eaa69-142">É tooupdate usadas somente propriedades do próprio recurso de zona hello.</span><span class="sxs-lookup"><span data-stu-id="eaa69-142">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="eaa69-143">Essas propriedades são atualmente limitado toohello [do Azure Resource Manager 'tags'](dns-zones-records.md#tags) para o recurso de zona hello.</span><span class="sxs-lookup"><span data-stu-id="eaa69-143">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="eaa69-144">Olá exemplo a seguir mostra como tooupdate Olá marcas em uma zona DNS.</span><span class="sxs-lookup"><span data-stu-id="eaa69-144">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="eaa69-145">marcas existentes Hello serão substituídas por Olá valor especificado.</span><span class="sxs-lookup"><span data-stu-id="eaa69-145">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="eaa69-146">Excluir uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="eaa69-146">Delete a DNS Zone</span></span>

<span data-ttu-id="eaa69-147">As zonas DNS podem ser excluídas por meio do `azure network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="eaa69-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="eaa69-148">Para obter ajuda, consulte `azure network dns zone delete -h`.</span><span class="sxs-lookup"><span data-stu-id="eaa69-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="eaa69-149">Excluir uma zona DNS também exclui todos os registros DNS na zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="eaa69-149">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="eaa69-150">Essa operação não pode ser desfeita.</span><span class="sxs-lookup"><span data-stu-id="eaa69-150">This operation cannot be undone.</span></span> <span data-ttu-id="eaa69-151">Se a zona DNS de saudação está em uso, serviços usando zona Olá falhará quando Olá zona é excluída.</span><span class="sxs-lookup"><span data-stu-id="eaa69-151">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="eaa69-152">tooprotect contra a exclusão acidental de zona, consulte [como tooprotect DNS zonas e os registros](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="eaa69-152">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="eaa69-153">Esse comando solicita uma confirmação.</span><span class="sxs-lookup"><span data-stu-id="eaa69-153">This command prompts for confirmation.</span></span> <span data-ttu-id="eaa69-154">Olá opcional `--quiet` alternar (forma abreviada `-q`) suprime esse prompt.</span><span class="sxs-lookup"><span data-stu-id="eaa69-154">hello optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="eaa69-155">Olá exemplo a seguir mostra como toodelete Olá zona *contoso.com* do grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="eaa69-155">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="eaa69-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eaa69-156">Next steps</span></span>

<span data-ttu-id="eaa69-157">Saiba como muito[gerenciar conjuntos de registros e registros](dns-getstarted-create-recordset-cli-nodejs.md) na zona DNS.</span><span class="sxs-lookup"><span data-stu-id="eaa69-157">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="eaa69-158">Saiba como muito[delegar tooAzure seu domínio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="eaa69-158">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

