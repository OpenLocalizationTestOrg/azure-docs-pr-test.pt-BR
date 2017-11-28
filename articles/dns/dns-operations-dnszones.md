---
title: Gerenciar as zonas DNS no DNS do Azure - PowerShell | Microsoft Docs
description: "Você pode gerenciar zonas DNS usando o Azure Powershell. Este artigo descreve como atualizar, excluir e criar zonas DNS no DNS do Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 92f1da660d875c76d5d826669d6c1d12018c3d0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-using-powershell"></a><span data-ttu-id="a0a07-104">Como gerenciar as zonas DNS usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0a07-104">How to manage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0a07-105">Portal</span><span class="sxs-lookup"><span data-stu-id="a0a07-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="a0a07-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0a07-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="a0a07-107">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="a0a07-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="a0a07-108">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="a0a07-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="a0a07-109">Este artigo mostra como gerenciar suas zonas DNS usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0a07-109">This article shows you how to manage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="a0a07-110">Você também pode gerenciar as zonas DNS usando a plataforma cruzada [CLI do Azure](dns-operations-dnszones-cli.md) ou o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0a07-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="a0a07-111">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="a0a07-111">Create a DNS zone</span></span>

<span data-ttu-id="a0a07-112">Uma zona DNS é criada usando o cmdlet `New-AzureRmDnsZone` .</span><span class="sxs-lookup"><span data-stu-id="a0a07-112">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="a0a07-113">O exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos chamado *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="a0a07-113">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="a0a07-114">O exemplo a seguir mostra como criar uma zona DNS com duas [marcas do Azure Resource Manager](dns-zones-records.md#tags), *project = demo* e *env = test*:</span><span class="sxs-lookup"><span data-stu-id="a0a07-114">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="a0a07-115">Obter uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="a0a07-115">Get a DNS zone</span></span>

<span data-ttu-id="a0a07-116">Para recuperar uma zona DNS, use o cmdlet `Get-AzureRmDnsZone` .</span><span class="sxs-lookup"><span data-stu-id="a0a07-116">To retrieve a DNS zone, use the `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="a0a07-117">Esta operação retornará um objeto de zona DNS correspondente a uma zona existente no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0a07-117">This operation returns a DNS zone object corresponding to an existing zone in Azure DNS.</span></span> <span data-ttu-id="a0a07-118">O objeto contém dados sobre a zona (como o número de conjuntos de registros), mas não contém os conjuntos de registro em si (veja `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="a0a07-118">The object contains data about the zone (such as the number of record sets), but does not contain the record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a><span data-ttu-id="a0a07-119">Listar as zonas DNS</span><span class="sxs-lookup"><span data-stu-id="a0a07-119">List DNS zones</span></span>

<span data-ttu-id="a0a07-120">Omitindo o nome da zona de `Get-AzureRmDnsZone`, você pode enumerar todas as zonas em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a0a07-120">By omitting the zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="a0a07-121">Essa operação retorna uma matriz de objetos de zona.</span><span class="sxs-lookup"><span data-stu-id="a0a07-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="a0a07-122">Omitindo o nome da zona e o nome do grupo de recursos do `Get-AzureRmDnsZone`, você pode enumerar todas as regiões na assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0a07-122">By omitting both the zone name and the resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in the Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="a0a07-123">Atualizar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="a0a07-123">Update a DNS zone</span></span>

<span data-ttu-id="a0a07-124">As alterações a um recurso da zona DNS podem ser feitas usando o `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="a0a07-124">Changes to a DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="a0a07-125">Este cmdlet não atualiza nenhum dos conjuntos de registros DNS dentro da zona (consulte [Como gerenciar registros DNS](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="a0a07-125">This cmdlet does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="a0a07-126">Ele só é usado para atualizar as propriedades do recurso da zona em si.</span><span class="sxs-lookup"><span data-stu-id="a0a07-126">It's only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="a0a07-127">As propriedades de zona graváveis são limitadas às [‘marcas’ do Azure Resource Manager para o recurso de zona](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="a0a07-127">The writable zone properties are currently limited to the [Azure Resource Manager ‘tags’ for the zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="a0a07-128">Use um dos dois métodos a seguir para atualizar uma zona DNS:</span><span class="sxs-lookup"><span data-stu-id="a0a07-128">Use one of the following two ways to update a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group"></a><span data-ttu-id="a0a07-129">Especifique a zona usando o nome da zona e o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a0a07-129">Specify the zone using the zone name and resource group</span></span>

<span data-ttu-id="a0a07-130">Essa abordagem substitui as marcas de zona existente com os valores especificados.</span><span class="sxs-lookup"><span data-stu-id="a0a07-130">This approach replaces the existing zone tags with the values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="a0a07-131">Especifique a zona usando um objeto de $zone</span><span class="sxs-lookup"><span data-stu-id="a0a07-131">Specify the zone using a $zone object</span></span>

<span data-ttu-id="a0a07-132">Essa abordagem recupera o objeto de zona existente, modifica as marcas e, em seguida, confirma as alterações.</span><span class="sxs-lookup"><span data-stu-id="a0a07-132">This approach retrieves the existing zone object, modifies the tags, and then commits the changes.</span></span> <span data-ttu-id="a0a07-133">Dessa forma, as marcas existentes podem ser preservadas.</span><span class="sxs-lookup"><span data-stu-id="a0a07-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get the zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="a0a07-134">Ao usar `Set-AzureRmDnsZone` com um objeto $zone, [verificações de Etag](dns-zones-records.md#etags) serão usadas para garantir que as alterações simultâneas não sejam substituídas.</span><span class="sxs-lookup"><span data-stu-id="a0a07-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="a0a07-135">Você pode usar o argumento `-Overwrite` opcional para omitir essas verificações.</span><span class="sxs-lookup"><span data-stu-id="a0a07-135">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="a0a07-136">Excluir uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="a0a07-136">Delete a DNS Zone</span></span>

<span data-ttu-id="a0a07-137">As zonas DNS podem ser excluídas usando o cmdlet `Remove-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="a0a07-137">DNS zones can be deleted using the `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="a0a07-138">Excluir uma zona DNS também excluirá todos os registros DNS na zona.</span><span class="sxs-lookup"><span data-stu-id="a0a07-138">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="a0a07-139">Essa operação não pode ser desfeita.</span><span class="sxs-lookup"><span data-stu-id="a0a07-139">This operation cannot be undone.</span></span> <span data-ttu-id="a0a07-140">Se a zona DNS estiver em uso, serviços que usam a zona falharão quando a zona for excluída.</span><span class="sxs-lookup"><span data-stu-id="a0a07-140">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="a0a07-141">Para se proteger contra a exclusão acidental da zona, consulte [Proteger registros e zonas DNS](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="a0a07-141">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="a0a07-142">Use um dos dois métodos a seguir para excluir uma zona DNS:</span><span class="sxs-lookup"><span data-stu-id="a0a07-142">Use one of the following two ways to delete a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group-name"></a><span data-ttu-id="a0a07-143">Especifique a zona usando o nome da zona e o nome do grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a0a07-143">Specify the zone using the zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="a0a07-144">Especifique a zona usando um objeto de $zone</span><span class="sxs-lookup"><span data-stu-id="a0a07-144">Specify the zone using a $zone object</span></span>

<span data-ttu-id="a0a07-145">Você pode especificar a zona a ser excluído usando um `$zone` objeto retornado por `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="a0a07-145">You can specify the zone to be deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="a0a07-146">O objeto de zona também pode ser redirecionado em vez de ser passado como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="a0a07-146">The zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="a0a07-147">Assim como com `Set-AzureRmDnsZone`, especificar a zona usando um objeto `$zone` habilita as verificações de Etag para garantir que as alterações simultâneas não sejam excluídas.</span><span class="sxs-lookup"><span data-stu-id="a0a07-147">As with `Set-AzureRmDnsZone`, specifying the zone using a `$zone` object enables Etag checks to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="a0a07-148">Use o `-Overwrite` para suprimir essas verificações.</span><span class="sxs-lookup"><span data-stu-id="a0a07-148">Use the `-Overwrite` switch to suppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="a0a07-149">Prompts de confirmação</span><span class="sxs-lookup"><span data-stu-id="a0a07-149">Confirmation prompts</span></span>

<span data-ttu-id="a0a07-150">Os cmdlets `New-AzureRmDnsZone`, `Set-AzureRmDnsZone` e `Remove-AzureRmDnsZone` oferecem suporte aos prompts de confirmação.</span><span class="sxs-lookup"><span data-stu-id="a0a07-150">The `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="a0a07-151">`New-AzureRmDnsZone` e `Set-AzureRmDnsZone` solicitam confirmação caso a variável de preferência do PowerShell `$ConfirmPreference` tenha um valor `Medium` ou inferior.</span><span class="sxs-lookup"><span data-stu-id="a0a07-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="a0a07-152">Dado o impacto potencialmente alto da exclusão de uma zona DNS, o `Remove-AzureRmDnsZone` cmdlet solicita confirmação se a `$ConfirmPreference` variável do PowerShell tem qualquer valor diferente de `None`.</span><span class="sxs-lookup"><span data-stu-id="a0a07-152">Due to the potentially high impact of deleting a DNS zone, the `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="a0a07-153">Desde o valor padrão para `$ConfirmPreference` é `High`, apenas `Remove-AzureRmDnsZone` solicitará uma confirmação por padrão.</span><span class="sxs-lookup"><span data-stu-id="a0a07-153">Since the default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="a0a07-154">Você pode substituir a configuração `$ConfirmPreference` atual usando o parâmetro `-Confirm`.</span><span class="sxs-lookup"><span data-stu-id="a0a07-154">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="a0a07-155">Se você especificar `-Confirm` ou `-Confirm:$True`, o cmdlet solicitará uma confirmação antes de executar.</span><span class="sxs-lookup"><span data-stu-id="a0a07-155">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="a0a07-156">Se você especificar `-Confirm:$False`, o cmdlet não solicitará uma confirmação.</span><span class="sxs-lookup"><span data-stu-id="a0a07-156">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="a0a07-157">Para obter mais informações sobre `-Confirm` e `$ConfirmPreference`, consulte [Sobre as Variáveis de Preferência](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="a0a07-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0a07-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a0a07-158">Next steps</span></span>

<span data-ttu-id="a0a07-159">Saiba como [gerenciar conjuntos de registros e registros](dns-operations-recordsets.md) em sua zona DNS.</span><span class="sxs-lookup"><span data-stu-id="a0a07-159">Learn how to [manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="a0a07-160">Saiba como [delegar seu domínio ao DNS do Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="a0a07-160">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="a0a07-161">Examine a [documentação de referência do PowerShell do DNS do Azure](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="a0a07-161">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

