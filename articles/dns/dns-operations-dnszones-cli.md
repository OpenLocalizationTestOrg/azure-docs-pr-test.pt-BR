---
title: Gerenciar as zonas DNS no DNS do Azure - CLI do Azure 2.0 | Microsoft Docs
description: "Você pode gerenciar zonas DNS usando a CLI do Azure 2.0. Este artigo mostra como atualizar, excluir e criar zonas DNS no DNS do Azure."
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
ms.openlocfilehash: 1414baf9e51d648cc3a46c4f8635040b4d276910
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-20"></a><span data-ttu-id="3f150-104">Como gerenciar Zonas DNS no DNS do Azure usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="3f150-104">How to manage DNS Zones in Azure DNS using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3f150-105">Portal</span><span class="sxs-lookup"><span data-stu-id="3f150-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="3f150-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f150-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="3f150-107">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="3f150-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="3f150-108">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="3f150-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="3f150-109">Este guia mostra como gerenciar as zonas DNS usando a CLI do Azure entre plataformas, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="3f150-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="3f150-110">Você também pode gerenciar seus registros DNS usando o [Azure PowerShell](dns-operations-dnszones.md) ou o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3f150-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="3f150-111">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="3f150-111">CLI versions to complete the task</span></span>

<span data-ttu-id="3f150-112">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="3f150-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="3f150-113">[CLI do Azure 1.0](dns-operations-dnszones-cli-nodejs.md) – nossa CLI para os modelos de implantação clássico e do resource manager.</span><span class="sxs-lookup"><span data-stu-id="3f150-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="3f150-114">[CLI do Azure 2.0](dns-operations-dnszones-cli.md) – nossa próxima geração de CLI para o modelo de implantação do resource manager.</span><span class="sxs-lookup"><span data-stu-id="3f150-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="3f150-115">Introdução</span><span class="sxs-lookup"><span data-stu-id="3f150-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="3f150-116">Configurar a CLI do Azure 2.0 para DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="3f150-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="3f150-117">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="3f150-117">Before you begin</span></span>

<span data-ttu-id="3f150-118">Antes de começar a configurar, verifique se você tem os itens a seguir.</span><span class="sxs-lookup"><span data-stu-id="3f150-118">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="3f150-119">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="3f150-119">An Azure subscription.</span></span> <span data-ttu-id="3f150-120">Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3f150-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="3f150-121">Instale a versão mais recente da CLI do Azure 2.0, disponível para Windows, Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="3f150-121">Install the latest version of the Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="3f150-122">Mais informações estão disponíveis em [Instalar a CLI do Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="3f150-122">More information is available at [Install the Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="3f150-123">Entre na sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="3f150-123">Sign in to your Azure account</span></span>

<span data-ttu-id="3f150-124">Abra uma janela do console e autentique com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="3f150-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="3f150-125">Para saber mais, confira Conectar-se ao Azure desde a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3f150-125">For more information, see Log in to Azure from the Azure CLI</span></span>

```
az login
```

### <a name="select-the-subscription"></a><span data-ttu-id="3f150-126">Selecionar a assinatura</span><span class="sxs-lookup"><span data-stu-id="3f150-126">Select the subscription</span></span>

<span data-ttu-id="3f150-127">Verificar as assinaturas da conta.</span><span class="sxs-lookup"><span data-stu-id="3f150-127">Check the subscriptions for the account.</span></span>

```
az account list
```

<span data-ttu-id="3f150-128">Escolha quais das suas assinaturas do Azure deseja usar.</span><span class="sxs-lookup"><span data-stu-id="3f150-128">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="3f150-129">Criar um grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="3f150-129">Create a resource group</span></span>

<span data-ttu-id="3f150-130">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="3f150-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="3f150-131">Ele é usado como o local padrão para os recursos do grupo de recursos em questão.</span><span class="sxs-lookup"><span data-stu-id="3f150-131">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="3f150-132">No entanto, como todos os recursos de DNS são globais, não regionais, a escolha do local do grupo de recursos não afeta o DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="3f150-132">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="3f150-133">Você pode ignorar esta etapa se está usando um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="3f150-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="3f150-134">Obtendo ajuda</span><span class="sxs-lookup"><span data-stu-id="3f150-134">Getting help</span></span>

<span data-ttu-id="3f150-135">Todos os comandos da CLI 2.0 relacionados ao DNS do Azure começam com `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="3f150-135">All CLI 2.0 commands relating to Azure DNS start with `az network dns`.</span></span> <span data-ttu-id="3f150-136">A ajuda está disponível para cada comando usando a opção `--help` (forma abreviada `-h`).</span><span class="sxs-lookup"><span data-stu-id="3f150-136">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="3f150-137">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3f150-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="3f150-138">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="3f150-138">Create a DNS zone</span></span>

<span data-ttu-id="3f150-139">Uma zona DNS é criada usando o comando `az network dns zone create` .</span><span class="sxs-lookup"><span data-stu-id="3f150-139">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="3f150-140">Para obter ajuda, consulte `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="3f150-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="3f150-141">O exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos chamado *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="3f150-141">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="3f150-142">Para criar uma zona DNS com marcas</span><span class="sxs-lookup"><span data-stu-id="3f150-142">To create a DNS zone with tags</span></span>

<span data-ttu-id="3f150-143">O exemplo a seguir mostra como criar uma zona DNS com duas [marcas do Azure Resource Manager](dns-zones-records.md#tags), *project = demo* e *env = test*, usando o parâmetro `--tags` (forma abreviada `-t`):</span><span class="sxs-lookup"><span data-stu-id="3f150-143">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="3f150-144">Obter uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="3f150-144">Get a DNS zone</span></span>

<span data-ttu-id="3f150-145">Para recuperar uma zona DNS, use `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="3f150-145">To retrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="3f150-146">Para obter ajuda, consulte `az network dns zone show --help`.</span><span class="sxs-lookup"><span data-stu-id="3f150-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="3f150-147">O exemplo a seguir retorna a zona DNS *contoso.com* e seus dados associados do grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="3f150-147">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="3f150-148">O exemplo a seguir é a resposta.</span><span class="sxs-lookup"><span data-stu-id="3f150-148">The following example is the response.</span></span>

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

<span data-ttu-id="3f150-149">Observe que registros DNS não são retornados por `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="3f150-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="3f150-150">Para listar registros DNS, use `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="3f150-150">To list DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="3f150-151">Listar as zonas DNS</span><span class="sxs-lookup"><span data-stu-id="3f150-151">List DNS zones</span></span>

<span data-ttu-id="3f150-152">Para enumerar zonas DNS, use `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="3f150-152">To enumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="3f150-153">Para obter ajuda, consulte `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="3f150-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="3f150-154">Especificar o grupo de recursos lista apenas as zonas dentro do grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="3f150-154">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="3f150-155">Omitir o grupo de recursos lista todas as zonas na assinatura:</span><span class="sxs-lookup"><span data-stu-id="3f150-155">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="3f150-156">Atualizar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="3f150-156">Update a DNS zone</span></span>

<span data-ttu-id="3f150-157">As alterações a um recurso da zona DNS podem ser feitas usando o `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="3f150-157">Changes to a DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="3f150-158">Para obter ajuda, consulte `az network dns zone update --help`.</span><span class="sxs-lookup"><span data-stu-id="3f150-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="3f150-159">Esse comando não atualiza nenhum dos conjuntos de registros DNS dentro da zona (consulte [Como gerenciar registros DNS](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="3f150-159">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="3f150-160">Ele só é usado para atualizar as propriedades do recurso da zona em si.</span><span class="sxs-lookup"><span data-stu-id="3f150-160">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="3f150-161">Atualmente, essas propriedades são limitadas às [“marcas” do Azure Resource Manager](dns-zones-records.md#tags) para o recurso de zona.</span><span class="sxs-lookup"><span data-stu-id="3f150-161">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="3f150-162">O exemplo a seguir mostra como atualizar as marcas em uma zona DNS.</span><span class="sxs-lookup"><span data-stu-id="3f150-162">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="3f150-163">As marcas existentes são substituídas pelo valor especificado.</span><span class="sxs-lookup"><span data-stu-id="3f150-163">The existing tags are replaced by the value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="3f150-164">Excluir uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="3f150-164">Delete a DNS zone</span></span>

<span data-ttu-id="3f150-165">As zonas DNS podem ser excluídas por meio do `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="3f150-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="3f150-166">Para obter ajuda, consulte `az network dns zone delete --help`.</span><span class="sxs-lookup"><span data-stu-id="3f150-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="3f150-167">Excluir uma zona DNS também excluirá todos os registros DNS na zona.</span><span class="sxs-lookup"><span data-stu-id="3f150-167">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="3f150-168">Essa operação não pode ser desfeita.</span><span class="sxs-lookup"><span data-stu-id="3f150-168">This operation cannot be undone.</span></span> <span data-ttu-id="3f150-169">Se a zona DNS estiver em uso, serviços que usam a zona falharão quando a zona for excluída.</span><span class="sxs-lookup"><span data-stu-id="3f150-169">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="3f150-170">Para se proteger contra a exclusão acidental da zona, consulte [Proteger registros e zonas DNS](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="3f150-170">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="3f150-171">Esse comando solicita uma confirmação.</span><span class="sxs-lookup"><span data-stu-id="3f150-171">This command prompts for confirmation.</span></span> <span data-ttu-id="3f150-172">A opção `--yes` opcional suprime esse prompt.</span><span class="sxs-lookup"><span data-stu-id="3f150-172">The optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="3f150-173">O exemplo a seguir mostra como excluir a zona *contoso.com* de grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="3f150-173">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="3f150-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3f150-174">Next steps</span></span>

<span data-ttu-id="3f150-175">Saiba como [gerenciar conjuntos de registros e registros](dns-getstarted-create-recordset-cli.md) em sua zona DNS.</span><span class="sxs-lookup"><span data-stu-id="3f150-175">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="3f150-176">Saiba como [delegar seu domínio ao DNS do Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="3f150-176">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

