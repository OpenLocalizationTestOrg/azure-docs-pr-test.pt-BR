---
title: aaaManage DNS zonas no DNS do Azure - PowerShell | Microsoft Docs
description: "Você pode gerenciar zonas DNS usando o Azure Powershell. Este artigo descreve como tooupdate, excluir e criar zonas DNS no DNS do Azure"
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
ms.openlocfilehash: 261b89f72213aa9784034d47ff9d1c55a4e80d65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-using-powershell"></a><span data-ttu-id="5fe90-104">Como toomanage zonas de DNS usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fe90-104">How toomanage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5fe90-105">Portal</span><span class="sxs-lookup"><span data-stu-id="5fe90-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="5fe90-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fe90-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="5fe90-107">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="5fe90-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="5fe90-108">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="5fe90-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="5fe90-109">Este artigo mostra como toomanage suas zonas DNS usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe90-109">This article shows you how toomanage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="5fe90-110">Você também pode gerenciar as zonas DNS usando multiplataforma Olá [CLI do Azure](dns-operations-dnszones-cli.md) ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe90-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="5fe90-111">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="5fe90-111">Create a DNS zone</span></span>

<span data-ttu-id="5fe90-112">Uma zona DNS é criada usando Olá `New-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5fe90-112">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="5fe90-113">Olá, exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos de saudação chamado *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="5fe90-113">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="5fe90-114">Olá exemplo a seguir mostra como toocreate um DNS da zona com dois [do Azure Resource Manager marcas](dns-zones-records.md#tags), *projeto = demonstração* e *env = test*:</span><span class="sxs-lookup"><span data-stu-id="5fe90-114">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="5fe90-115">Obter uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="5fe90-115">Get a DNS zone</span></span>

<span data-ttu-id="5fe90-116">tooretrieve uma zona DNS, use Olá `Get-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5fe90-116">tooretrieve a DNS zone, use hello `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="5fe90-117">Essa operação retorna um DNS da zona objeto correspondente tooan zona existente no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe90-117">This operation returns a DNS zone object corresponding tooan existing zone in Azure DNS.</span></span> <span data-ttu-id="5fe90-118">Olá objeto contém dados sobre a zona de saudação (como número de saudação de conjuntos de registros), mas não contém conjuntos de registros de saudação próprios (consulte `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="5fe90-118">hello object contains data about hello zone (such as hello number of record sets), but does not contain hello record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

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

## <a name="list-dns-zones"></a><span data-ttu-id="5fe90-119">Listar as zonas DNS</span><span class="sxs-lookup"><span data-stu-id="5fe90-119">List DNS zones</span></span>

<span data-ttu-id="5fe90-120">Omitindo o nome da zona de saudação do `Get-AzureRmDnsZone`, você pode enumerar todas as zonas em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5fe90-120">By omitting hello zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="5fe90-121">Essa operação retorna uma matriz de objetos de zona.</span><span class="sxs-lookup"><span data-stu-id="5fe90-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="5fe90-122">Omitindo o nome da zona hello e o nome do grupo de recursos de saudação do `Get-AzureRmDnsZone`, você pode enumerar todas as zonas em Olá assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe90-122">By omitting both hello zone name and hello resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in hello Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="5fe90-123">Atualizar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="5fe90-123">Update a DNS zone</span></span>

<span data-ttu-id="5fe90-124">Alterações tooa recurso de zona do DNS pode ser feito usando `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="5fe90-124">Changes tooa DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="5fe90-125">Esse cmdlet não atualizar conjuntos de registros de DNS hello dentro da zona de saudação (consulte [como registros DNS tooManage](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="5fe90-125">This cmdlet does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="5fe90-126">Ele só tem usado tooupdate propriedades do próprio recurso de zona hello.</span><span class="sxs-lookup"><span data-stu-id="5fe90-126">It's only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="5fe90-127">Propriedades de zona gravável Olá são atualmente limitado toohello [do Azure Resource Manager 'marcas' para o recurso de zona Olá](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="5fe90-127">hello writable zone properties are currently limited toohello [Azure Resource Manager ‘tags’ for hello zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="5fe90-128">Use uma saudação tooupdate de duas maneiras a seguir uma zona DNS:</span><span class="sxs-lookup"><span data-stu-id="5fe90-128">Use one of hello following two ways tooupdate a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a><span data-ttu-id="5fe90-129">Especificar Olá zona usando o grupo de recursos e o nome da zona de saudação</span><span class="sxs-lookup"><span data-stu-id="5fe90-129">Specify hello zone using hello zone name and resource group</span></span>

<span data-ttu-id="5fe90-130">Essa abordagem substitui marcas existentes de zona Olá com hello valores especificados.</span><span class="sxs-lookup"><span data-stu-id="5fe90-130">This approach replaces hello existing zone tags with hello values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="5fe90-131">Especifique a zona hello usando um objeto $zone</span><span class="sxs-lookup"><span data-stu-id="5fe90-131">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="5fe90-132">Essa abordagem recupera o objeto de zona existente hello, modifica marcas hello e, em seguida, confirma as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fe90-132">This approach retrieves hello existing zone object, modifies hello tags, and then commits hello changes.</span></span> <span data-ttu-id="5fe90-133">Dessa forma, as marcas existentes podem ser preservadas.</span><span class="sxs-lookup"><span data-stu-id="5fe90-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get hello zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="5fe90-134">Ao usar `Set-AzureRmDnsZone` com um objeto $zone, [Etag verifica](dns-zones-records.md#etags) são usadas as alterações simultâneas de tooensure não são substituídas.</span><span class="sxs-lookup"><span data-stu-id="5fe90-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="5fe90-135">Você pode usar o hello opcional `-Overwrite` alternar toosuppress essas verificações.</span><span class="sxs-lookup"><span data-stu-id="5fe90-135">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="5fe90-136">Excluir uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="5fe90-136">Delete a DNS Zone</span></span>

<span data-ttu-id="5fe90-137">As zonas DNS podem ser excluídas usando Olá `Remove-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5fe90-137">DNS zones can be deleted using hello `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="5fe90-138">Excluir uma zona DNS também exclui todos os registros DNS na zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fe90-138">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="5fe90-139">Essa operação não pode ser desfeita.</span><span class="sxs-lookup"><span data-stu-id="5fe90-139">This operation cannot be undone.</span></span> <span data-ttu-id="5fe90-140">Se a zona DNS de saudação está em uso, serviços usando zona Olá falhará quando Olá zona é excluída.</span><span class="sxs-lookup"><span data-stu-id="5fe90-140">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="5fe90-141">tooprotect contra a exclusão acidental de zona, consulte [como tooprotect DNS zonas e os registros](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="5fe90-141">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="5fe90-142">Use uma saudação toodelete de duas maneiras a seguir uma zona DNS:</span><span class="sxs-lookup"><span data-stu-id="5fe90-142">Use one of hello following two ways toodelete a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a><span data-ttu-id="5fe90-143">Especificar Olá zona usando o nome da zona hello e o nome do grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="5fe90-143">Specify hello zone using hello zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="5fe90-144">Especifique a zona hello usando um objeto $zone</span><span class="sxs-lookup"><span data-stu-id="5fe90-144">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="5fe90-145">Você pode especificar Olá zona toobe excluído usando um `$zone` objeto retornado por `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="5fe90-145">You can specify hello zone toobe deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="5fe90-146">objeto de zona Olá também pode ser usado em vez de ser passado como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="5fe90-146">hello zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="5fe90-147">Assim como acontece com `Set-AzureRmDnsZone`, especificando Olá zona usando um `$zone` habilita Etag verifica as alterações simultâneas de tooensure não são excluídas do objeto.</span><span class="sxs-lookup"><span data-stu-id="5fe90-147">As with `Set-AzureRmDnsZone`, specifying hello zone using a `$zone` object enables Etag checks tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="5fe90-148">Saudação de uso `-Overwrite` alternar toosuppress essas verificações.</span><span class="sxs-lookup"><span data-stu-id="5fe90-148">Use hello `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="5fe90-149">Prompts de confirmação</span><span class="sxs-lookup"><span data-stu-id="5fe90-149">Confirmation prompts</span></span>

<span data-ttu-id="5fe90-150">Olá `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, e `Remove-AzureRmDnsZone` todos os cmdlets de dar suporte a solicitações de confirmação.</span><span class="sxs-lookup"><span data-stu-id="5fe90-150">hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="5fe90-151">Ambos `New-AzureRmDnsZone` e `Set-AzureRmDnsZone` solicita confirmação se hello `$ConfirmPreference` variável de preferência do PowerShell tem um valor de `Medium` ou inferior.</span><span class="sxs-lookup"><span data-stu-id="5fe90-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="5fe90-152">Devido a toohello potencialmente alto impacto da exclusão de uma zona DNS, hello `Remove-AzureRmDnsZone` cmdlet solicita confirmação se hello `$ConfirmPreference` variável do PowerShell tem qualquer valor diferente de `None`.</span><span class="sxs-lookup"><span data-stu-id="5fe90-152">Due toohello potentially high impact of deleting a DNS zone, hello `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="5fe90-153">Desde o valor padrão Olá `$ConfirmPreference` é `High`, apenas `Remove-AzureRmDnsZone` solicita confirmação por padrão.</span><span class="sxs-lookup"><span data-stu-id="5fe90-153">Since hello default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="5fe90-154">Você pode substituir o atual Olá `$ConfirmPreference` configuração usando Olá `-Confirm` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="5fe90-154">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="5fe90-155">Se você especificar `-Confirm` ou `-Confirm:$True` , Olá cmdlet solicita sua confirmação antes que ele é executado.</span><span class="sxs-lookup"><span data-stu-id="5fe90-155">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="5fe90-156">Se você especificar `-Confirm:$False` , Olá cmdlet não solicita confirmação.</span><span class="sxs-lookup"><span data-stu-id="5fe90-156">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="5fe90-157">Para obter mais informações sobre `-Confirm` e `$ConfirmPreference`, consulte [Sobre as Variáveis de Preferência](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="5fe90-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fe90-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5fe90-158">Next steps</span></span>

<span data-ttu-id="5fe90-159">Saiba como muito[gerenciar conjuntos de registros e registros](dns-operations-recordsets.md) na zona DNS.</span><span class="sxs-lookup"><span data-stu-id="5fe90-159">Learn how too[manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="5fe90-160">Saiba como muito[delegar tooAzure seu domínio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="5fe90-160">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="5fe90-161">Saudação de revisão [documentação de referência do PowerShell do Azure DNS](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="5fe90-161">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

