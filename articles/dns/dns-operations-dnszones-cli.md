---
title: aaaManage DNS zonas no DNS do Azure - 2.0 do CLI do Azure | Microsoft Docs
description: "Você pode gerenciar zonas DNS usando a CLI do Azure 2.0. Este artigo mostra como tooupdate, excluir e criar zonas DNS no DNS do Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="7d182-104">Como toomanage zonas de DNS no DNS do Azure usando Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7d182-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d182-105">Portal</span><span class="sxs-lookup"><span data-stu-id="7d182-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="7d182-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d182-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="7d182-107">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="7d182-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="7d182-108">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="7d182-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="7d182-109">Este guia mostra como toomanage suas zonas DNS usando Olá multiplataforma CLI do Azure, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="7d182-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="7d182-110">Você também pode gerenciar as zonas DNS usando [Azure PowerShell](dns-operations-dnszones.md) ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7d182-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="7d182-111">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="7d182-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="7d182-112">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="7d182-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="7d182-113">[1.0 de CLI do Azure](dns-operations-dnszones-cli-nodejs.md) -nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de hello.</span><span class="sxs-lookup"><span data-stu-id="7d182-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="7d182-114">[2.0 do CLI do Azure](dns-operations-dnszones-cli.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d182-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="7d182-115">Introdução</span><span class="sxs-lookup"><span data-stu-id="7d182-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="7d182-116">Configurar a CLI do Azure 2.0 para DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="7d182-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="7d182-117">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="7d182-117">Before you begin</span></span>

<span data-ttu-id="7d182-118">Verifique se você tem Olá itens a seguir antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="7d182-118">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="7d182-119">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="7d182-119">An Azure subscription.</span></span> <span data-ttu-id="7d182-120">Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7d182-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="7d182-121">Instale a versão mais recente Olá de saudação 2.0 do CLI do Azure, disponível para Windows, Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="7d182-121">Install hello latest version of hello Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="7d182-122">Mais informações estão disponíveis em [instalação hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="7d182-122">More information is available at [Install hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="7d182-123">Entrar tooyour conta do Azure</span><span class="sxs-lookup"><span data-stu-id="7d182-123">Sign in tooyour Azure account</span></span>

<span data-ttu-id="7d182-124">Abra uma janela do console e autentique com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="7d182-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="7d182-125">Para obter mais informações, consulte o Log em tooAzure de saudação CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7d182-125">For more information, see Log in tooAzure from hello Azure CLI</span></span>

```
az login
```

### <a name="select-hello-subscription"></a><span data-ttu-id="7d182-126">Selecione a assinatura de saudação</span><span class="sxs-lookup"><span data-stu-id="7d182-126">Select hello subscription</span></span>

<span data-ttu-id="7d182-127">Verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d182-127">Check hello subscriptions for hello account.</span></span>

```
az account list
```

<span data-ttu-id="7d182-128">Escolha qual toouse suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="7d182-128">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="7d182-129">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="7d182-129">Create a resource group</span></span>

<span data-ttu-id="7d182-130">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="7d182-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="7d182-131">Isso é usado como o local padrão de saudação para recursos desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7d182-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="7d182-132">No entanto, como todos os recursos DNS são globais, não regional, escolha de saudação do local do grupo de recursos não tem impacto no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="7d182-132">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="7d182-133">Você pode ignorar esta etapa se está usando um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="7d182-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="7d182-134">Obtendo ajuda</span><span class="sxs-lookup"><span data-stu-id="7d182-134">Getting help</span></span>

<span data-ttu-id="7d182-135">Todos os comandos de CLI 2.0 relacionadas tooAzure DNS iniciam com `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="7d182-135">All CLI 2.0 commands relating tooAzure DNS start with `az network dns`.</span></span> <span data-ttu-id="7d182-136">A Ajuda está disponível para cada comando usando Olá `--help` opção (forma abreviada `-h`).</span><span class="sxs-lookup"><span data-stu-id="7d182-136">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="7d182-137">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7d182-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="7d182-138">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="7d182-138">Create a DNS zone</span></span>

<span data-ttu-id="7d182-139">Uma zona DNS é criada usando Olá `az network dns zone create` comando.</span><span class="sxs-lookup"><span data-stu-id="7d182-139">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="7d182-140">Para obter ajuda, consulte `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="7d182-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="7d182-141">Olá, exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos de saudação chamado *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="7d182-141">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="7d182-142">toocreate uma zona DNS com marcas</span><span class="sxs-lookup"><span data-stu-id="7d182-142">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="7d182-143">Olá exemplo a seguir mostra como toocreate um DNS da zona com dois [do Azure Resource Manager marcas](dns-zones-records.md#tags), *projeto = demonstração* e *env = test*, usando Olá `--tags` parâmetro (forma abreviada `-t`):</span><span class="sxs-lookup"><span data-stu-id="7d182-143">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="7d182-144">Obter uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="7d182-144">Get a DNS zone</span></span>

<span data-ttu-id="7d182-145">tooretrieve uma zona DNS, use `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="7d182-145">tooretrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="7d182-146">Para obter ajuda, consulte `az network dns zone show --help`.</span><span class="sxs-lookup"><span data-stu-id="7d182-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="7d182-147">Olá, exemplo a seguir retorna zona do DNS Olá *contoso.com* e seus dados associados do grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="7d182-147">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="7d182-148">saudação de exemplo a seguir é a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d182-148">hello following example is hello response.</span></span>

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="7d182-149">Observe que registros DNS não são retornados por `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="7d182-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="7d182-150">registros DNS toolist, use `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="7d182-150">toolist DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="7d182-151">Listar as zonas DNS</span><span class="sxs-lookup"><span data-stu-id="7d182-151">List DNS zones</span></span>

<span data-ttu-id="7d182-152">zonas DNS tooenumerate, use `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="7d182-152">tooenumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="7d182-153">Para obter ajuda, consulte `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="7d182-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="7d182-154">Grupo de recursos de saudação especificando lista apenas as zonas no grupo de recursos de saudação:</span><span class="sxs-lookup"><span data-stu-id="7d182-154">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="7d182-155">Grupo de recursos de saudação omitindo lista todas as zonas na assinatura hello:</span><span class="sxs-lookup"><span data-stu-id="7d182-155">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="7d182-156">Atualizar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="7d182-156">Update a DNS zone</span></span>

<span data-ttu-id="7d182-157">Alterações tooa recurso de zona do DNS pode ser feito usando `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="7d182-157">Changes tooa DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="7d182-158">Para obter ajuda, consulte `az network dns zone update --help`.</span><span class="sxs-lookup"><span data-stu-id="7d182-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="7d182-159">Este comando não atualizar conjuntos de registros de DNS hello dentro da zona de saudação (consulte [como registros DNS tooManage](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="7d182-159">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="7d182-160">É tooupdate usadas somente propriedades do próprio recurso de zona hello.</span><span class="sxs-lookup"><span data-stu-id="7d182-160">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="7d182-161">Essas propriedades são atualmente limitado toohello [do Azure Resource Manager 'tags'](dns-zones-records.md#tags) para o recurso de zona hello.</span><span class="sxs-lookup"><span data-stu-id="7d182-161">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="7d182-162">Olá exemplo a seguir mostra como tooupdate Olá marcas em uma zona DNS.</span><span class="sxs-lookup"><span data-stu-id="7d182-162">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="7d182-163">marcas existentes Hello serão substituídas por Olá valor especificado.</span><span class="sxs-lookup"><span data-stu-id="7d182-163">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="7d182-164">Excluir uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="7d182-164">Delete a DNS zone</span></span>

<span data-ttu-id="7d182-165">As zonas DNS podem ser excluídas por meio do `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="7d182-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="7d182-166">Para obter ajuda, consulte `az network dns zone delete --help`.</span><span class="sxs-lookup"><span data-stu-id="7d182-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="7d182-167">Excluir uma zona DNS também exclui todos os registros DNS na zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d182-167">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="7d182-168">Essa operação não pode ser desfeita.</span><span class="sxs-lookup"><span data-stu-id="7d182-168">This operation cannot be undone.</span></span> <span data-ttu-id="7d182-169">Se a zona DNS de saudação está em uso, serviços usando zona Olá falhará quando Olá zona é excluída.</span><span class="sxs-lookup"><span data-stu-id="7d182-169">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="7d182-170">tooprotect contra a exclusão acidental de zona, consulte [como tooprotect DNS zonas e os registros](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="7d182-170">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="7d182-171">Esse comando solicita uma confirmação.</span><span class="sxs-lookup"><span data-stu-id="7d182-171">This command prompts for confirmation.</span></span> <span data-ttu-id="7d182-172">Olá opcional `--yes` suprime esse prompt.</span><span class="sxs-lookup"><span data-stu-id="7d182-172">hello optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="7d182-173">Olá exemplo a seguir mostra como toodelete Olá zona *contoso.com* do grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="7d182-173">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="7d182-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7d182-174">Next steps</span></span>

<span data-ttu-id="7d182-175">Saiba como muito[gerenciar conjuntos de registros e registros](dns-getstarted-create-recordset-cli.md) na zona DNS.</span><span class="sxs-lookup"><span data-stu-id="7d182-175">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="7d182-176">Saiba como muito[delegar tooAzure seu domínio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="7d182-176">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

